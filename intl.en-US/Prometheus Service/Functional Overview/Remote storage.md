# Remote storage

Alibaba Cloud Prometheus Service provides the RemoteWrite feature. You can use this feature to store the monitoring data of Prometheus Service to remote databases. This topic describes how to use the RemoteWrite feature to connect Alibaba Cloud Prometheus Service with the open source Prometheus. The feature provides an efficient solution to store monitoring data.

## Step 1: Create a RemoteWrite and obtain the read and write URLs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner of the page, select the destination region. On the Prometheus Monitoring page, click **Access prometheus monitoring**.

4.  On the Access Prometheus monitoring page, click **Remote Write Prometheus**.

5.  In Step 1 of the wizard, specify the **RemoteWrite Name** parameter and click **Next**.

6.  In Step 2, copy and save the generated value of the Prometheus Remote Write Url parameter, and then click **Next**.

7.  In Step 3, copy and save the generated value of the Prometheus Remote Read Url parameter, and then close the wizard.


## Step 2: Configure Prometheus

1.  Install Prometheus. For information about how to install Prometheus, see [Official documentation](https://prometheus.io/download/).

2.  Open the Prometheus.yaml configuration file and append the following content to the file. Replace the `remote_write` and `remote_read` URLs with the URLs that you obtained in [Step 1: Create a RemoteWrite and obtain the read and write URLs](#section_fnr_zrt_2dg). Then, save the file.

    ```
    global:
      scrape_interval:     15s
      evaluation_interval: 15s
    scrape_configs:
      - job_name: 'prometheus'
        static_configs:
        - targets: ['localhost:9090']
    remote_write:
      - url: "http://ts-xxxxxxxxxxxx.hitsdb.rds.aliyuncs.com:3242/api/prom_write"
        basic_auth:   
          // The username and password must conform to the naming conventions of an AK/SK pair. The AK/SK pair must be authorized to call the [GetPrometheusApiToken](/intl.en-US/API reference/Prometheus/GetPrometheusApiToken.md) operation.
          username: access-key-id
          password: access-key-secret
    remote_read:
      - url: "http://ts-xxxxxxxxxxxx.hitsdb.rds.aliyuncs.com:3242/api/prom_read"
        read_recent: true
    ```


## Use remote storage for OpenTelemetry

1.  Configure OpenTelemetry tracking in the business code. [\[Demo\]](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo/blob/master/pkg/opentelemetry/buy_service.go)

    ```
    package stat
    
    import (
        "context"
        "fmt"
        "go.opentelemetry.io/otel"
        "go.opentelemetry.io/otel/metric"
        "time"
    )
    
    var buyCounter metric.Int64Counter
    
    func init() {
        fmt.Println(time.Now(), " - initMetrics start......")
        meter := otel.GetMeterProvider().Meter("github.com/liguozhong/prometheus-arms-aliyun-go-demo")
        buyCounter = metric.Must(meter).NewInt64Counter(
            "buy_total",
            metric.WithDescription("Measures  buy"),
        )
    }
    
    func DoBuy() (string, error) {
        buyCounter.Add(context.Background(), 1)
        return "buy success", nil
    }
    ```

2.  OpenTelemetry initializes Meter and connects to Prometheus. [\[Demo\]](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo/blob/master/pkg/opentelemetry/meter_config.go)

    ```
    package stat
    
    import (
        "context"
        prometheusPushExporter "go.opentelemetry.io/contrib/exporters/metric/cortex"
        prometheusExporter "go.opentelemetry.io/otel/exporters/metric/prometheus"
    
        "errors"
        "fmt"
        "go.opentelemetry.io/otel"
        "go.opentelemetry.io/otel/exporters/otlp"
        "go.opentelemetry.io/otel/label"
        "go.opentelemetry.io/otel/sdk/metric/controller/pull"
        "go.opentelemetry.io/otel/sdk/metric/controller/push"
        "go.opentelemetry.io/otel/sdk/metric/processor/basic"
        "go.opentelemetry.io/otel/sdk/metric/selector/simple"
        "go.opentelemetry.io/otel/sdk/resource"
        "net/http"
        "time"
    
        _ "net/http/pprof"
    )
    
    func InitMeter(app string, push bool) error {
        fmt.Println(time.Now(), " - initMeter start......")
        if push {
            fmt.Println(time.Now(), " - initMeter opentelemetry push......")
            remoteUrl := "http://region.arms.aliyuncs.com/prometheus/.. /.. /.. /../api/v3/write"
            ak := "ak"
            sk := "sk"
            return initPushMeter(app, remoteUrl, ak, sk)
        }
        fmt.Println(time.Now(), " - initMeter opentelemetry pull......")
        return initPullMeter(app)
    }
    
    func initPushMeter(regionId string, remoteWriteUrl string, ak string, sk string) error {
        fmt.Println(time.Now(), " - initPushMeter start......")
        var validatedStandardConfig = prometheusPushExporter.Config{
            Endpoint:      remoteWriteUrl,
            Name:          "AliyunConfig",
            RemoteTimeout: 30 * time.Second,
            PushInterval:  10 * time.Second,
            Quantiles:     []float64{0.5, 0.9, 0.95, 0.99},
            BasicAuth: map[string]string{
                "username": ak,
                "password": sk,
            },
        }
        if validatedStandardConfig.Endpoint == "" {
            return errors.New(" validatedStandardConfig.Endpoint==empty.regionId:" + regionId)
        }
        fmt.Println("Success: Created Config struct")
        r, err := resource.New(context.Background(),
            resource.WithAttributes(
                label.String("cluster", "test-otel"),
                label.String("app", "buy")))
        if err ! = nil {
            fmt.Println("resource Error:", err)
        }
        pusher, err := prometheusPushExporter.InstallNewPipeline(validatedStandardConfig,
            push.WithPeriod(30*time.Second), push.WithResource(r))
        if err ! = nil {
            fmt.Println("InstallNewPipeline Error:", err)
        }
        otel.SetMeterProvider(pusher.MeterProvider())
        return nil
    }
    
    func initPullMeter(app string) error {
        fmt.Println(time.Now(), " - initPullMeter start......")
        r, err := resource.New(context.Background(),
            resource.WithAttributes(
                label.String("cluster", "test-otel"),
                label.String("app", app)))
        if err ! = nil {
            fmt.Println("resource Error:", err)
        }
        exporter, err := prometheusExporter.NewExportPipeline(
            prometheusExporter.Config{
                DefaultHistogramBoundaries: []float64{-0.5, 1},
            },
            pull.WithCachePeriod(0),
            pull.WithResource(r),
        )
        if err ! = nil {
            return err
        }
        http.HandleFunc("/opentelemetry", exporter.ServeHTTP)
        otel.SetMeterProvider(exporter.MeterProvider())
        return nil
    }
    
    func initOtlpProvider(regionId string) (*push.Controller, error) {
        exporter, err := otlp.NewExporter(
            context.Background(),
            otlp.WithInsecure(),
            otlp.WithAddress(regionId+"-intranet.arms.aliyuncs.com:8000"),
        )
        if err ! = nil {
            return nil, err
        }
    
        pusher := push.New(
            basic.New(
                simple.NewWithExactDistribution(),
                exporter,
            ),
            exporter,
            push.WithPeriod(30*time.Second),
        )
    
        otel.SetMeterProvider(pusher.MeterProvider())
        pusher.Start()
    
        return pusher, err
    }
    ```

3.  Initialize the business endpoint and start the OpenTelemetry function. [\[Demo\]](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo/blob/master/pkg/operator.go)

    ```
    package pkg
    
    import (
        "fmt"
        stat "github.com/liguozhong/prometheus-arms-aliyun-go-demo/pkg/opentelemetry"
        "github.com/prometheus/client_golang/prometheus/promhttp"
        "io"
        "net/http"
        "strconv"
    )
    
    type Server struct {
        port int
    }
    
    func NewServer(port int) *Server {
        return &Server{
            port: port,
        }
    }
    
    func (s *Server) Run() error {
        port := ":" + strconv.Itoa(s.port)
        path := "/metrics"
        service := "/buy"
        http.Handle(path, promhttp.Handler()) // Initializes an HTTP handler.
        http.HandleFunc(service, func(writer http.ResponseWriter, request *http.Request) {
            content, err := stat.DoBuy()
            if err ! = nil {
                io.WriteString(writer, err.Error())
                return
            }
            io.WriteString(writer, content)
        })
        stat.InitMeter("buy2", true)
        fmt.Println("http.url: http://localhost" + port + path)
        fmt.Println("service.url: http://localhost" + port + service)
        err := http.ListenAndServe(port, nil)
        if err ! = nil {
            return err
        }
        return nil
    }
    ```

4.  View the dependencies of the Go module. [\[Demo\]](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo/blob/master/go.mod)

    ```
    module github.com/liguozhong/prometheus-arms-aliyun-go-demo
    
    go 1.12
    
    require (
        github.com/go-kit/kit v0.9.0
        github.com/prometheus/client_golang v1.7.1
        go.opentelemetry.io/contrib/exporters/metric/cortex v0.15.0
        go.opentelemetry.io/otel v0.15.0
        go.opentelemetry.io/otel/exporters/metric/prometheus v0.15.0
        go.opentelemetry.io/otel/exporters/otlp v0.15.0
        go.opentelemetry.io/otel/sdk v0.15.0
        golang.org/x/text v0.3.3 // indirect
    )
    ```

5.  View the data in Grafana.

    ![View the data of OpenTelemetry](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0792088061/p205546.png)




