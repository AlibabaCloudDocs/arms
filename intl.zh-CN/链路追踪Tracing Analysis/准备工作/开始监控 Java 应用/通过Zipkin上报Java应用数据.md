# 通过Zipkin上报Java应用数据

Zipkin是一款开源的分布式实时数据追踪系统（Distributed Tracking System），由Twitter公司开发和贡献。其主要功能是聚合来自各个异构系统的实时监控数据。在链路追踪Tracing Analysis中，您可以通过Zipkin上报Java应用数据。



Zipkin已经开发多年，对各种框架的支持比较齐全，例如[以下Java框架](https://github.com/openzipkin/brave/tree/master/instrumentation)。

-   Apache HttpClient
-   Dubbo
-   gRPC
-   JAX-RS 2.X
-   Jersey Server
-   JMS \(Java Message Service\)
-   Kafka
-   MySQL
-   Netty
-   OkHttp
-   Servlet
-   Spark
-   Spring Boot
-   Spring MVC

要通过Zipkin将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。您可以手动埋点，也可以利用各种现有插件实现埋点的目的。



## 手动埋点

如果选择手动埋点，您就需要自行编写代码。

**说明：** 如需获取Demo，请单击下载[源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip)，进入manualDemo目录，并根据Readme运行程序。

1.  添加依赖Jar包。

    ```
    <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave</artifactId>
                <version>5.4.2</version>
            </dependency>
            <dependency>
                <groupId>io.zipkin.reporter2</groupId>
                <artifactId>zipkin-sender-okhttp3</artifactId>
                <version>2.7.9</version>
            </dependency>
    ```

2.  创建Tracer。

    ```
    private static final String zipkinEndPoint = "<endpoint>";
      ...
      // 构建数据发送对象。
      OkHttpSender sender = OkHttpSender.newBuilder().endpoint(zipkinEndPoint).build();
    
      // 构建数据上报对象。
      Reporter<Span> reporter = AsyncReporter.builder(sender).build();
    
      tracing = Tracing.newBuilder().localServiceName(localServiceName).spanReporter(reporter).build();
    ```

3.  构建Span和Child Span。

    ```
    private void firstBiz() {
            // 创建rootspan。
            tracing.tracer().startScopedSpan("parentSpan");
            Span span =  tracing.tracer().currentSpan();
            span.tag("key", "firstBiz");
            secondBiz();
            span.finish();
        }
    
        private void secondBiz() {
            tracing.tracer().startScopedSpanWithParent("childSpan", tracing.tracer().currentSpan().context());
            Span chindSpan =  tracing.tracer().currentSpan();
            chindSpan.tag("key", "secondBiz");
            chindSpan.finish();
            System.out.println("end tracing,id:" + chindSpan.context().traceIdString());
        }
    ```

4.  （可选）为了快速排查问题，您可以为某个记录添加一些自定义标签，例如记录是否发生错误、请求的返回值等。

    ```
    tracer.activeSpan().setTag("http.status_code", "500");
    ```

5.  在分布式系统中发送RPC请求时会带上Tracing数据，包括TraceId、ParentSpanId、SpanId、Sampled等。您可以在HTTP请求中使用Extract/Inject方法在HTTP Request Headers上透传数据。总体流程如下：

    ```
       Client Span                                                Server Span
    ┌──────────────────┐                                       ┌──────────────────┐
    │                  │                                       │                  │
    │   TraceContext   │           Http Request Headers        │   TraceContext   │
    │ ┌──────────────┐ │          ┌───────────────────┐        │ ┌──────────────┐ │
    │ │ TraceId      │ │          │ X-B3-TraceId      │        │ │ TraceId      │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ ParentSpanId │ │ Inject   │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │
    │ │              ├─┼─────────>│                   ├────────┼>│              │ │
    │ │ SpanId       │ │          │ X-B3-SpanId       │        │ │ SpanId       │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ Sampled      │ │          │ X-B3-Sampled      │        │ │ Sampled      │ │
    │ └──────────────┘ │          └───────────────────┘        │ └──────────────┘ │
    │                  │                                       │                  │
    └──────────────────┘                                       └──────────────────┘
    ```

    1.  在客户端调用Inject方法传入Context信息。

        ```
        // start a new span representing a client request
            oneWaySend = tracer.nextSpan().name(service + "/" + method).kind(CLIENT);
            --snip--
        
            // Add the trace context to the request, so it can bepropagated in-band
            tracing.propagation().injector(Request::addHeader)
                             .inject(oneWaySend.context(), request);
        
           // fire off the request asynchronously, totally dropping any response
           request.execute();
        
           // start the client side and flush instead of finish
           oneWaySend.start().flush();
        ```

    2.  在服务端调用Extract方法解析Context信息。

        ```
        // pull the context out of the incoming request
        extractor = tracing.propagation().extractor(Request::getHeader);
        
        // convert that context to a span which you can name and add tags to
        oneWayReceive = nextSpan(tracer, extractor.extract(request))
            .name("process-request")
            .kind(SERVER)
            ... add tags etc.
        
        // start the server side and flush instead of finish
        oneWayReceive.start().flush();
        
        // you should not modify this span anymore as it is complete. However,
        // you can create children to represent follow-up work.
        next = tracer.newSpan(oneWayReceive.context()).name("step2").start();
        ```


## 通过Spring 2.5 MVC或Spring 3.0 MVC插件埋点

您可以选择通过Spring 2.5 MVC或Spring 3.0 MVC插件进行埋点。

**说明：** 如需获取Demo，请单击下载[源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip)，进入springMvcDemo\\webmvc3\|webmvc25目录，并根据Readme运行程序。

1.  在applicationContext.xml中配置Tracing对象。

    ```
    <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean">
      <property name="endpoint" value="<endpoint>"/>
    </bean>
    
    <!-- allows us to read the service name from spring config -->
    <context:property-placeholder/>
    
    <bean class="brave.spring.beans.TracingFactoryBean">
      <property name="localServiceName" value="brave-webmvc3-example"/>
      <property name="spanReporter">
        <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean">
          <property name="encoder" value="JSON_V2"/>
          <property name="sender" ref="sender"/>
          <!-- wait up to half a second for any in-flight spans on close -->
          <property name="closeTimeout" value="500"/>
        </bean>
      </property>
      <property name="propagationFactory">
        <bean class="brave.propagation.ExtraFieldPropagation" factory-method="newFactory">
          <constructor-arg index="0">
            <util:constant static-field="brave.propagation.B3Propagation.FACTORY"/>
          </constructor-arg>
          <constructor-arg index="1">
            <list>
              <value>user-name</value>
            </list>
          </constructor-arg>
        </bean>
      </property>
      <property name="currentTraceContext">
        <bean class="brave.spring.beans.CurrentTraceContextFactoryBean">
          <property name="scopeDecorators">
            <bean class="brave.context.log4j12.MDCScopeDecorator" factory-method="create"/>
          </property>
        </bean>
      </property>
    </bean>
    
    <bean class="brave.spring.beans.HttpTracingFactoryBean">
      <property name="tracing" ref="tracing"/>
    </bean>
    ```

2.  添加Interceptors对象。

    ```
    <bean class="brave.httpclient.TracingHttpClientBuilder"
          factory-method="create">
        <constructor-arg type="brave.http.HttpTracing" ref="httpTracing"/>
      </bean>
    
      <bean factory-bean="httpClientBuilder" factory-method="build"/>
    
      <bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">
        <property name="interceptors">
          <list>
            <bean class="brave.spring.webmvc.SpanCustomizingHandlerInterceptor"/>
          </list>
        </property>
      </bean>
    
      <!-- Loads the controller -->
      <context:component-scan base-package="brave.webmvc"/>
    ```

3.  添加Filter对象。

    ```
    <!-- Add the delegate to the standard tracing filter and map it to all paths -->
    <filter>
      <filter-name>tracingFilter</filter-name>
      <filter-class>brave.spring.webmvc.DelegatingTracingFilter</filter-class>
    </filter>
    <filter-mapping>
      <filter-name>tracingFilter</filter-name>
      <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```


## 通过Spring 4.0 MVC或Spring Boot插件埋点

您可以选择通过Spring 4.0 MVC或Spring Boot插件进行埋点。

**说明：** 如需获取Demo，请单击下载[源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip)，进入springMvcDemo\\webmvc4-boot\|webmv4目录，并根据Readme运行程序。

1.  配置Tracing和Filter。

    ```
    /** Configuration for how to send spans to Zipkin */
      @Bean Sender sender() {
        return OkHttpSender.create("<endpoint>");
      }
    
      /** Configuration for how to buffer spans into messages for Zipkin */
      @Bean AsyncReporter<Span> spanReporter() {
        return AsyncReporter.create(sender());
      }
    
      /** Controls aspects of tracing such as the name that shows up in the UI */
      @Bean Tracing tracing(@Value("${spring.application.name}") String serviceName) {
        return Tracing.newBuilder()
            .localServiceName(serviceName)
            .propagationFactory(ExtraFieldPropagation.newFactory(B3Propagation.FACTORY, "user-name"))
            .currentTraceContext(ThreadLocalCurrentTraceContext.newBuilder()
                .addScopeDecorator(MDCScopeDecorator.create()) // puts trace IDs into logs
                .build()
            )
            .spanReporter(spanReporter()).build();
      }
    
      /** decides how to name and tag spans. By default they are named the same as the http method. */
      @Bean HttpTracing httpTracing(Tracing tracing) {
        return HttpTracing.create(tracing);
      }
    
      /** Creates client spans for http requests */
      // We are using a BPP as the Frontend supplies a RestTemplate bean prior to this configuration
      @Bean BeanPostProcessor connectionFactoryDecorator(final BeanFactory beanFactory) {
        return new BeanPostProcessor() {
          @Override public Object postProcessBeforeInitialization(Object bean, String beanName) {
            return bean;
          }
    
          @Override public Object postProcessAfterInitialization(Object bean, String beanName) {
            if (!(bean instanceof RestTemplate)) return bean;
    
            RestTemplate restTemplate = (RestTemplate) bean;
            List<ClientHttpRequestInterceptor> interceptors =
                new ArrayList<>(restTemplate.getInterceptors());
            interceptors.add(0, getTracingInterceptor());
            restTemplate.setInterceptors(interceptors);
            return bean;
          }
    
          // Lazy lookup so that the BPP doesn't end up needing to proxy anything.
          ClientHttpRequestInterceptor getTracingInterceptor() {
            return TracingClientHttpRequestInterceptor.create(beanFactory.getBean(HttpTracing.class));
          }
        };
      }
    
      /** Creates server spans for http requests */
      @Bean Filter tracingFilter(HttpTracing httpTracing) {
        return TracingFilter.create(httpTracing);
      }
    
      @Autowired SpanCustomizingAsyncHandlerInterceptor webMvcTracingCustomizer;
    
      /** Decorates server spans with application-defined web tags */
      @Override public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(webMvcTracingCustomizer);
      }
    ```

2.  配置autoconfigure（spring.factories\)。

    ```
    org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
    brave.webmvc.TracingConfiguration
    ```


## 通过Dubbo插件埋点

您可以选择通过Dubbo插进进行埋点。

**说明：** 如需获取Demo，请单击下载[源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip)，进入dubboDem目录，并根据Readme运行程序。

1.  添加依赖Jar包。

    ```
    <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave-instrumentation-dubbo-rpc</artifactId>
                <version>5.4.2</version>
            </dependency>
    
            <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave-spring-beans</artifactId>
                <version>5.4.2</version>
            </dependency>
    
            <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave-context-slf4j</artifactId>
                <version>5.4.2</version>
            </dependency>
            <dependency>
                <groupId>io.zipkin.reporter2</groupId>
                <artifactId>zipkin-sender-okhttp3</artifactId>
                <version>2.7.9</version>
            </dependency>
            <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave</artifactId>
                <version>5.4.2</version>
            </dependency>
    
            <dependency>
                <groupId>io.zipkin.reporter2</groupId>
                <artifactId>zipkin-sender-okhttp3</artifactId>
                <version>2.7.9</version>
            </dependency>
    ```

2.  配置Tracing对象。

    ```
    <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean">
            <property name="endpoint" value="<endpoint>"/>
        </bean>
    
        <bean class="brave.spring.beans.TracingFactoryBean">
            <property name="localServiceName" value="double-provider"/>
            <property name="spanReporter">
                <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean">
                    <property name="sender" ref="sender"/>
                    <!-- wait up to half a second for any in-flight spans on close -->
                    <property name="closeTimeout" value="500"/>
                </bean>
            </property>
            <property name="currentTraceContext">
                <bean class="brave.spring.beans.CurrentTraceContextFactoryBean">
                    <property name="scopeDecorators">
                        <bean class="brave.context.slf4j.MDCScopeDecorator" factory-method="create"/>
                    </property>
                </bean>
            </property>
        </bean>
    ```

3.  添加Filter配置。

    ```
    // 服务端配置。
    <dubbo:provider filter="tracing" />
    // 客户端配置。
    <dubbo:consumer filter="tracing" />
    ```


## 通过Spring Sleuth插件埋点

您可以选择通过Spring Sleuth插进进行埋点。

**说明：** 如需获取Demo，请单击下载[源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip)，进入sleuthDemo目录，并根据Readme运行程序。

1.  添加依赖Jar包。

    ```
    <dependency>
                <groupId>io.zipkin.brave</groupId>
                <artifactId>brave</artifactId>
                <version>5.4.2</version>
            </dependency>
    
            <dependency>
                <groupId>io.zipkin.reporter2</groupId>
                <artifactId>zipkin-sender-okhttp3</artifactId>
                <version>2.7.9</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
                <version>2.0.1.RELEASE</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-sleuth-core</artifactId>
                <version>2.0.1.RELEASE</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-sleuth-zipkin</artifactId>
                <version>2.0.1.RELEASE</version>
            </dependency>
    ```

2.  配置application.yml。

    **说明：** 请将`<endpoint_short>`替换成控制台概览页面上相应地域的接入点（“公网接入点：”后面到“api/v2/spans”之前的内容）。

    ```
    spring:
       application:
         # This ends up as the service name in zipkin
         name: sleuthDemo
       zipkin:
         # Uncomment to send to zipkin, replacing 192.168.99.100 with your zipkin IP address
         baseUrl: <endpoint_short>
    
       sleuth:
         sampler:
           probability: 1.0
    
     sample:
       zipkin:
         # When enabled=false, traces log to the console. Comment to send to zipkin
         enabled: true
    ```


## 常见问题

问：Demo程序执行成功，但是为什么有的网站上无数据？

答：请断点调试zipkin2.reporter.okhttp3.HttpCall中的parseResponse方法，查看上报数据时返回值。如果报403错误，表示用户名配置不正确，需要检查endpoint配置。

[brave-webmvc-example](https://github.com/openzipkin/brave-webmvc-example)

[brave-instrumentation](https://github.com/openzipkin/brave/tree/master/instrumentation)

[spring-cloud-zipkin-sleuth-tutorial](https://howtodoinjava.com/spring-cloud/spring-cloud-zipkin-sleuth-tutorial/)

