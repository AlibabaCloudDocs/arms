# Use Zipkin to report Java application data

Zipkin is a distributed tracing system. It is an open source system that is developed by Twitter to trace real-time data. Zipkin is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems. You can use Zipkin to report Java application data to Tracing Analysis.

Zipkin has been developed for many years and supports a comprehensive set of frameworks, such as the following Java frameworks. For more information, visit [brave-instrumentation](https://github.com/openzipkin/brave/tree/master/instrumentation).

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

To use Zipkin to report Java application data to the Tracing Analysis console, you must first instrument the application. You can instrument the application manually or by using existing components.

## Manually instrument a Java application

If you want to manually instrument the application, you must write instrumentation code.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip). Go to the manualDemo directory and run the program as instructed in the README.md file.

1.  Add a JAR package as a dependency.

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

2.  Create a tracer.

    ```
    private static final String zipkinEndPoint = "<endpoint>";
      ...
      // Create an object that is used to send data.
      OkHttpSender sender = OkHttpSender.newBuilder().endpoint(zipkinEndPoint).build();
    
      // Create an object that is used to report data.
      Reporter<Span> reporter = AsyncReporter.builder(sender).build();
    
      tracing = Tracing.newBuilder().localServiceName(localServiceName).spanReporter(reporter).build();
    ```

3.  Create a span and a child span.

    ```
    private void firstBiz() {
            // Create a root span.
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

4.  Optional. Add custom tags to a span for quick troubleshooting. For example, you can add a custom tag to check whether an error occurs or to record the return value of a request.

    ```
    tracer.activeSpan().setTag("http.status_code", "500");
    ```

5.  In a distributed system, remote procedure call \(RPC\) requests are sent along with trace data. Trace data contains the values of the TraceId, ParentSpanId, SpanId, and Sampled parameters. You can call the Extract or Inject method to pass data in HTTP request headers. The overall process is as follows.

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

    1.  Call the Inject method on the client to inject the context information.

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

    2.  Call the Extract method on the server to extract the context information.

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


## Use Spring 2.5 MVC or Spring 3.0 MVC to instrument a Java application

You can use Spring 2.5 MVC or Spring 3.0 MVC to instrument the application.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip). Go to the springMvcDemo\\webmvc3\|webmvc25 directory and run the program as instructed in the README.md file.

1.  Configure the tracing object in the applicationContext.xml file.

    ```
    <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean">
      <property name="endpoint" value="<endpoint>"/>
    </bean>
    
    <! -- allows us to read the service name from spring config -->
    <context:property-placeholder/>
    
    <bean class="brave.spring.beans.TracingFactoryBean">
      <property name="localServiceName" value="brave-webmvc3-example"/>
      <property name="spanReporter">
        <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean">
          <property name="encoder" value="JSON_V2"/>
          <property name="sender" ref="sender"/>
          <! -- wait up to half a second for any in-flight spans on close -->
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

2.  Add an interceptors object.

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
    
      <! -- Loads the controller -->
      <context:component-scan base-package="brave.webmvc"/>
    ```

3.  Add a filter object.

    ```
    <! -- Add the delegate to the standard tracing filter and map it to all paths -->
    <filter>
      <filter-name>tracingFilter</filter-name>
      <filter-class>brave.spring.webmvc.DelegatingTracingFilter</filter-class>
    </filter>
    <filter-mapping>
      <filter-name>tracingFilter</filter-name>
      <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```


## Use Spring 4.0 MVC or Spring Boot to instrument a Java application

You can use Spring 4.0 MVC or Spring Boot to instrument the application.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip). Go to the springMvcDemo\\webmvc4-boot\|webmv4 directory and run the program as instructed in the README.md file.

1.  Configure the tracing and filter objects.

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
            if (!( bean instanceof RestTemplate)) return bean;
    
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

2.  Configure auto-configuration in the spring.factories file.

    ```
    org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
    brave.webmvc.TracingConfiguration
    ```


## Use Dubbo to instrument a Java application

You can use Dubbo to instrument the application.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip). Go to the dubboDem directory and run the program as instructed in the README.md file.

1.  Add a JAR package as a dependency.

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

2.  Configure the tracing object.

    ```
    <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean">
            <property name="endpoint" value="<endpoint>"/>
        </bean>
    
        <bean class="brave.spring.beans.TracingFactoryBean">
            <property name="localServiceName" value="double-provider"/>
            <property name="spanReporter">
                <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean">
                    <property name="sender" ref="sender"/>
                    <! -- wait up to half a second for any in-flight spans on close -->
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

3.  Configure the filter object.

    ```
    // Configuration on the server.
    <dubbo:provider filter="tracing" />
    // Configuration on the client.
    <dubbo:consumer filter="tracing" />
    ```


## Use Spring Sleuth to instrument a Java application

You can use Spring Sleuth to instrument the application.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip). Go to the sleuthDemo directory and run the program as instructed in the README.md file.

1.  Add a JAR package as a dependency.

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

2.  Configure the application.yml file.

    **Note:** Replace `<endpoint_short>` with the endpoint for your client and region. You can log on to the Tracing Analysis console and obtain the public endpoint that ends with api/v2/spans on the Access point information tab of the Cluster Configurations page.

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


## FAQ

Q: Why am I unable to find any data on specific websites after the demo program is run?

A: Insert a breakpoint to debug the parseResponse method in zipkin2.reporter.okhttp3.HttpCall and view the return value of the request for reporting data. If a 403 error is returned, the username configuration is invalid. You must check the endpoint configuration.

[brave-webmvc-example](https://github.com/openzipkin/brave-webmvc-example)

[brave-instrumentation](https://github.com/openzipkin/brave/tree/master/instrumentation)

[spring-cloud-zipkin-sleuth-tutorial](https://howtodoinjava.com/spring-cloud/spring-cloud-zipkin-sleuth-tutorial/)

