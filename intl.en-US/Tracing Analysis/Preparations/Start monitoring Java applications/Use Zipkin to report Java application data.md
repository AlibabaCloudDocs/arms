# Use Zipkin to report Java application data

Zipkin is an open source Distributed real-time data tracing System \(Distributed Tracking System\) developed and contributed by Twitter. This function aggregates real-time monitoring data from multiple heterogeneous systems. In Tracing Analysis, you can use Zipkin to report data to Java applications.



Zipkin has been developed for many years and has complete support for various frameworks, such as the [following Java frameworks](https://github.com/openzipkin/brave/tree/master/instrumentation).

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

To report Java application data to the tracing analysis console through Zipkin, you must first complete the tracking function. You can manually record points or use various existing plug-ins to implement tracking.

## Manual burial point

If you select manual tracking, you need to write your own code.

**Note:** To obtain a Demo, click download [source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip) code to go to the manualDemo directory and run the program according to Readme.

1.  Add the dependency Jar package.

    ```
    
            <dependency> <groupId>io.zipkin.brave <artifactId>brave</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.reporter2 <artifactId>zipkin-sender-okhttp3</artifactId> <version>2.7.9</version> </dependency> 
          
    ```

2.  Create a Tracer.

    ```
    
            private static final String zipkinEndPoint = "<endpoint>"; ... // Build a data sending object. OkHttpSender sender = OkHttpSender.newBuilder().endpoint(zipkinEndPoint).build(); // build the data reporting object. Reporter<Span> reporter = AsyncReporter.builder(sender).build(); tracing = Tracing.newBuilder().localServiceName(localServiceName).spanReporter(reporter).build(); 
          
    ```

3.  BUILD Span and Child Span.

    ```
    
            private void firstBiz() { // Create a rootspan. tracing.tracer().startScopedSpan("parentSpan"); Span span = tracing.tracer().currentSpan(); span.tag("key", "firstBiz"); secondBiz(); span.finish(); } private void secondBiz() { tracing.tracer().startScopedSpanWithParent("childSpan", tracing.tracer().currentSpan().context()); Span chindSpan = tracing.tracer().currentSpan(); chindSpan.tag("key", "secondBiz"); chindSpan.finish(); System.out.println("end tracing,id:" + chindSpan.context().traceIdString()); } 
          
    ```

4.  \(Optional\) to quickly troubleshoot the problem, you can add custom tags to a record, such as an error or a response to the request.

    ```
    
            tracer.activeSpan().setTag("http.status_code", "500"); 
          
    ```

5.  When an RPC request is sent in a distributed system, Tracing data \(such as TraceId, ParentSpanId, SpanId, and Sampled\) will be attached to the request. When sending an HTTP Request, you can use the Extract/Inject method to pass data through to the HTTP Request Headers. The overall process is as follows:

    ```
    
            Client Span Server Span ┌──────────────────┐ ┌──────────────────┐ │ │ │ │ │ TraceContext │ Http Request Headers │ TraceContext │ │ ┌──────────────┐ │ ┌───────────────────┐ │ ┌──────────────┐ │ │ │ TraceId │ │ │ X-B3-TraceId │ │ │ TraceId │ │ │ │ │ │ │ │ │ │ │ │ │ │ ParentSpanId │ │ Inject │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │ │ │ ├─┼─────────>│ ├────────┼>│ │ │ │ │ SpanId │ │ │ X-B3-SpanId │ │ │ SpanId │ │ │ │ │ │ │ │ │ │ │ │ │ │ Sampled │ │ │ X-B3-Sampled │ │ │ Sampled │ │ │ └──────────────┘ │ └───────────────────┘ │ └──────────────┘ │ │ │ │ │ └──────────────────┘ └──────────────────┘ 
          
    ```

    1.  Call the Inject method on the client to pass in Context information.

        ```
        
                  // start a new span representing a client request oneWaySend = tracer.nextSpan().name(service + "/" + method).kind(CLIENT); --snip-- // Add the trace context to the request, so it can bepropagated in-band tracing.propagation().injector(Request::addHeader) .inject(oneWaySend.context(), request); // fire off the request asynchronously, totally dropping any response request.execute(); // start the client side and flush instead of finish oneWaySend.start().flush(); 
                
        ```

    2.  Call the Extract method on the server to parse Context Information.

        ```
        
                  // pull the context out of the incoming request extractor = tracing.propagation().extractor(Request::getHeader); // convert that context to a span which you can name and add tags to oneWayReceive = nextSpan(tracer, extractor.extract(request)) .name("process-request") .kind(SERVER) ... add tags etc. // start the server side and flush instead of finish oneWayReceive.start().flush(); // you should not modify this span anymore as it is complete. However, // you can create children to represent follow-up work. next = tracer.newSpan(oneWayReceive.context()).name("step2").start(); 
                
        ```


## Tracking through Spring 2.5 MVC or Spring 3.0 MVC plug-ins

You can Spring 2.5 MVC or Spring 3.0 MVC plug-in to perform tracking.

**Note:** To obtain a Demo, click download [source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip) code to go to the following directory, and run the program according to Readme.

1.  Configure the Tracing object in applicationContext.xml.

    ```
    
            <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean"> <property name="endpoint" value="<endpoint>"/> </bean> <! -- allows us to read the service name from spring config --> <context:property-placeholder/> <bean class="brave.spring.beans.TracingFactoryBean"> <property name="localServiceName" value="brave-webmvc3-example"/> <property name="spanReporter"> <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean"> <property name="encoder" value="JSON_V2"/> <property name="sender" ref="sender"/> <! -- wait up to half a second for any in-flight spans on close --> <property name="closeTimeout" value="500"/> </bean> </property> <property name="propagationFactory"> <bean class="brave.propagation.ExtraFieldPropagation" factory-method="newFactory"> <constructor-arg index="0"> <util:constant static-field="brave.propagation.B3Propagation.FACTORY"/> </constructor-arg> <constructor-arg index="1"> <list> <value>user-name</value> </list> </constructor-arg> </bean> </property> <property name="currentTraceContext"> <bean class="brave.spring.beans.CurrentTraceContextFactoryBean"> <property name="scopeDecorators"> <bean class="brave.context.log4j12.MDCScopeDecorator" factory-method="create"/> </property> </bean> </property> </bean> <bean class="brave.spring.beans.HttpTracingFactoryBean"> <property name="tracing" ref="tracing"/> </bean> 
          
    ```

2.  Add Interceptors objects.

    ```
    
            <bean class="brave.httpclient.TracingHttpClientBuilder" factory-method="create"> <constructor-arg type="brave.http.HttpTracing" ref="httpTracing"/> </bean> <bean factory-bean="httpClientBuilder" factory-method="build"/> <bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping"> <property name="interceptors"> <list> <bean class="brave.spring.webmvc.SpanCustomizingHandlerInterceptor"/> </list> </property> </bean> <! -- Loads the controller --> <context:component-scan base-package="brave.webmvc"/> 
          
    ```

3.  Add Filter objects.

    ```
    
            <! -- Add the delegate to the standard tracing filter and map it to all paths --> <filter> <filter-name>tracingFilter</filter-name> <filter-class>brave.spring.webmvc.DelegatingTracingFilter</filter-class> </filter> <filter-mapping> <filter-name>tracingFilter</filter-name> <url-pattern>/*</url-pattern> </filter-mapping> 
          
    ```


## Spring 4.0 MVC or Spring Boot plug-in tracking

You can configure tracking through Spring 4.0 MVC or the Spring Boot plug-in.

**Note:** To obtain a Demo, click download [source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip) code to go to the following directory, and run the program according to Readme.

1.  Configure the Tracing and Filter functions.

    ```
    
            /** Configuration for how to send spans to Zipkin */ @Bean Sender sender() { return OkHttpSender.create("<endpoint>"); } /** Configuration for how to buffer spans into messages for Zipkin */ @Bean AsyncReporter<Span> spanReporter() { return AsyncReporter.create(sender()); } /** Controls aspects of tracing such as the name that shows up in the UI */ @Bean Tracing tracing(@Value("${spring.application.name}") String serviceName) { return Tracing.newBuilder() .localServiceName(serviceName) .propagationFactory(ExtraFieldPropagation.newFactory(B3Propagation.FACTORY, "user-name")) .currentTraceContext(ThreadLocalCurrentTraceContext.newBuilder() .addScopeDecorator(MDCScopeDecorator.create()) // puts trace IDs into logs .build() ) .spanReporter(spanReporter()).build(); } /** decides how to name and tag spans. By default they are named the same as the http method. */ @Bean HttpTracing httpTracing(Tracing tracing) { return HttpTracing.create(tracing); } /** Creates client spans for http requests */ // We are using a BPP as the Frontend supplies a RestTemplate bean prior to this configuration @Bean BeanPostProcessor connectionFactoryDecorator(final BeanFactory beanFactory) { return new BeanPostProcessor() { @Override public Object postProcessBeforeInitialization(Object bean, String beanName) { return bean; } @Override public Object postProcessAfterInitialization(Object bean, String beanName) { if (!( bean instanceof RestTemplate)) return bean; RestTemplate restTemplate = (RestTemplate) bean; List<ClientHttpRequestInterceptor> interceptors = new ArrayList<>(restTemplate.getInterceptors()); interceptors.add(0, getTracingInterceptor()); restTemplate.setInterceptors(interceptors); return bean; } // Lazy lookup so that the BPP doesn't end up needing to proxy anything. ClientHttpRequestInterceptor getTracingInterceptor() { return TracingClientHttpRequestInterceptor.create(beanFactory.getBean(HttpTracing.class)); } }; } /** Creates server spans for http requests */ @Bean Filter tracingFilter(HttpTracing httpTracing) { return TracingFilter.create(httpTracing); } @Autowired SpanCustomizingAsyncHandlerInterceptor webMvcTracingCustomizer; /** Decorates server spans with application-defined web tags */ @Override public void addInterceptors(InterceptorRegistry registry) { registry.addInterceptor(webMvcTracingCustomizer); } 
          
    ```

2.  Configure autoconfigure\(spring. Factors\).

    ```
    
            org.springframework.boot.autoconfigure.EnableAutoConfiguration=\ brave.webmvc.TracingConfiguration 
          
    ```


## Tracking through Dubbo plug-ins

You can choose to use Dubbo insertion for tracking.

**Note:** To obtain a Demo, click download [source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip) code, go to the dubboDem directory, and run the program according to Readme.

1.  Add the dependency Jar package.

    ```
    
            <dependency> <groupId>io.zipkin.brave <artifactId>brave-instrumentation-dubbo-rpc</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.brave <artifactId>brave-spring-beans</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.brave <artifactId>brave-context-slf4j</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.reporter2 <artifactId>zipkin-sender-okhttp3</artifactId> <version>2.7.9</version> </dependency> <dependency> <groupId>io.zipkin.brave <artifactId>brave</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.reporter2 <artifactId>zipkin-sender-okhttp3</artifactId> <version>2.7.9</version> </dependency> 
          
    ```

2.  Configure Tracing objects.

    ```
    
            <bean class="zipkin2.reporter.beans.OkHttpSenderFactoryBean"> <property name="endpoint" value="<endpoint>"/> </bean> <bean class="brave.spring.beans.TracingFactoryBean"> <property name="localServiceName" value="double-provider"/> <property name="spanReporter"> <bean class="zipkin2.reporter.beans.AsyncReporterFactoryBean"> <property name="sender" ref="sender"/> <! -- wait up to half a second for any in-flight spans on close --> <property name="closeTimeout" value="500"/> </bean> </property> <property name="currentTraceContext"> <bean class="brave.spring.beans.CurrentTraceContextFactoryBean"> <property name="scopeDecorators"> <bean class="brave.context.slf4j.MDCScopeDecorator" factory-method="create"/> </property> </bean> </property> </bean> 
          
    ```

3.  Add a Filter configuration.

    ```
    
            // Server configuration. <dubbo:provider filter="tracing" />// Client configuration. <dubbo:consumer filter="tracing" /> 
          
    ```


## Burial points through the Spring sleauth plug-in

You can choose to use Spring sleauth to insert the Tracking Point.

**Note:** To obtain a Demo, click download [source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingDemo.zip) code, go to the sleepdemo directory, and run the program according to Readme.

1.  Add the dependency Jar package.

    ```
    
            <dependency> <groupId>io.zipkin.brave <artifactId>brave</artifactId> <version>5.4.2</version> </dependency> <dependency> <groupId>io.zipkin.reporter2 <artifactId>zipkin-sender-okhttp3</artifactId> <version>2.7.9</version> </dependency> <dependency> <groupId>org.springframework.boot <artifactId>spring-boot-starter-web</artifactId> <version>2.0.1.RELEASE</version> </dependency> <dependency> <groupId>org.springframework.cloud <artifactId>spring-cloud-sleuth-core</artifactId> <version>2.0.1.RELEASE</version> </dependency> <dependency> <groupId>org.springframework.cloud <artifactId>spring-cloud-sleuth-zipkin</artifactId> <version>2.0.1.RELEASE</version> </dependency> 
          
    ```

2.  Configure the application.yml file.

    **Note:** I should be grateful if you would have `<endpoint_short>`replaces the console overview page on the corresponding region of the access point \("The Internet access point:" and to "api/v2/spans" before the contents of The.

    ```
    
            spring: application: # This ends up as the service name in zipkin name: sleuthDemo zipkin: # Uncomment to send to zipkin, replacing 192.168.99.100 with your zipkin IP address baseUrl: <endpoint_short> sleuth: sampler: probability: 1.0 sample: zipkin: # When enabled=false, traces log to the console. Comment to send to zipkin enabled: true 
          
    ```


## FAQ

Q: The Demo program was successfully executed, but why is there no data on some websites?

Answer: debug the zipkin2.reportter.okhttp3.httpcall method in parseResponse breakpoint to view the returned value when the data is reported. If a 403 error is reported, the username is configured incorrectly, and you need to check the endpoint configuration.

[brave-webmvc-example](https://github.com/openzipkin/brave-webmvc-example)

[brave-instrumentation](https://github.com/openzipkin/brave/tree/master/instrumentation)

[spring-cloud-zipkin-sleuth-tutorial](https://howtodoinjava.com/spring-cloud/spring-cloud-zipkin-sleuth-tutorial/)

