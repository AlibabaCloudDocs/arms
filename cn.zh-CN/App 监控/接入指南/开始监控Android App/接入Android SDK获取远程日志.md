# 接入Android SDK获取远程日志

借助App监控的SDK，您可以获取完备的远程日志。

已在ARMS中创建App监控任务。请参见[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)。

本文适用于使用Gradle管理依赖的Android Studio项目，请参见Demo工程[ha\_android\_demo](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo)。

**说明：** 日志在移动端最多存储7天。

## 步骤一：添加依赖

1.  在build.gradle项目中添加阿里云Maven仓库地址。

    ```
    repositories {    
        maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
        }
    ```

2.  在App模块的build.gradle项目的dependencies节点内添加以下代码。

    ```
    compile('com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.2-open@aar') {
            transitive=true
        }
    compile('com.aliyun.ams:alicloud-android-ha-tlog:1.1.2.2-open@aar') {
            transitive=true
        }
    ```


## 步骤二：接入服务

1.  在自定义Application类的onCreate里面启动服务。

    ```
    public class MyApplication extends Application {
        @Override
        public void onCreate() {
            initHa();
        }
        private void initHa() {
             Log.e("ha", "init");
             AliHaConfig config = new AliHaConfig();
             config.appKey = "xxxxxxxx";
             config.appVersion = "x.xx";         //应用的版本号。
             config.appSecret = "xxxxxxxxxxxx";  //appsecret
             config.channel = "mqc_test";        //应用的渠道号标记，自定义。
             config.userNick = null;
             config.application = this;
             config.context = getApplicationContext();
             config.isAliyunos = false;          //是否为yunos。
             config.rsaPublicKey = "xxxxxxx";    //TLog公钥，在控制台下载aliyun-emas-services.json文件，文件内的appmonitor.tlog.rsaSecret字段即为公钥信息（文件下载方式：在EMAS控制台->应用管理找到对应的应用，单击应用所在区块右上角菜单内的“配置下载”），必填。
             AliHaAdapter.getInstance().addPlugin(Plugin.tlog);
             AliHaAdapter.getInstance().openDebug(true);
             AliHaAdapter.getInstance().start(config);
        }
    }
    ```

    **说明：** appKey和appSecret，可在[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)中，[步骤](/cn.zh-CN/App 监控/快速入门：创建监控任务.mdstep_c3d_tna_qn1)[4](/cn.zh-CN/App 监控/快速入门：创建监控任务.mdstep_c3d_tna_qn1)下载的配置文件中获得。

2.  在AndroidManifest.xml里指定自定义Application。

    ```
    <application
        android:name=".MyApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme" >
        ...
    </application>
    ```

3.  在App模块的build.gradle的defaultConfig节点内添加以下代码，根据需要配置abi。

    ```
    ndk {
            abiFilters 'armeabi-v7a'
        }
    ```


## 步骤三：获取远程日志

1.  如业务流程触发日志输出，需引入头文件。

    ```
    import com.alibaba.ha.adapter.service.tlog.TLogService;
    ```

2.  在适当位置添加代码，输出日志信息。示例代码：

    ```
    String TAG = "xxx";
    String MODEL = "xxxxx";
    
    TLogService.logv(MODEL,TAG,"test tlog1");
    TLogService.logd(MODEL,TAG,"test tlog2");
    TLogService.logi(MODEL,TAG,"test tlog3");
    TLogService.logw(MODEL,TAG,"test tlog4");
    TLogService.loge(MODEL,TAG,"test tlog5");
    ```


## 结果验证

在完成上述步骤之后，您可以对您的App进行测试，并登录[ARMS控制台](https://arms.console.aliyun.com/#/home)查看数据报表。

