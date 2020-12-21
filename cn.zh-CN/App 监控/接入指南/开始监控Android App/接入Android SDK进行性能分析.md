# 接入Android SDK进行性能分析

借助App监控的SDK，您可以获取完备的移动应用性能分析。

已在ARMS中创建App监控任务，请参见[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)。

本文档适用于使用gradle管理依赖的Android Studio项目，请参见Demo工程[ha\_android\_demo](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo)。

## 步骤一：添加依赖

Maven仓库依赖接入：

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
    compile('com.aliyun.ams:alicloud-android-apm:1.0.7.7-open@aar') {
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
                 config.appKey = "xxxxxxxx";         //appKey
                 config.appVersion = "x.xx";           //应用的版本号信息。
                 config.appSecret = "xxxxxxxxxxxx";  //appSecret
                 config.channel = "mqc_test";        //应用的渠道号标记，自定义。
                 config.userNick = null;
                 config.application = this;
                 config.context = getApplicationContext();
                 config.isAliyunos = false;             //是否为yunos。
                 AliHaAdapter.getInstance().addPlugin(Plugin.apm);
                 AliHaAdapter.getInstance().start(config);
            }
        }
    ```

    **说明：** appKey和appSecret，可在[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)中，[步骤](/cn.zh-CN/App 监控/快速入门：创建监控任务.mdstep_c3d_tna_qn1)[4](/cn.zh-CN/App 监控/快速入门：创建监控任务.mdstep_c3d_tna_qn1)下载的配置文件中获得。

2.  AndroidManifest.xml里面指定自定义Application。

    ```
            <application
            android:name=".MyApplication"
            android:allowBackup="true"
            android:icon="@mipmap/ic_launcher"
            android:label="@string/app_name"
            android:supportsRtl="true"
            android:theme="@style/AppTheme" >
        </application>
    ```


## 结果验证

在完成上述步骤之后，您可以对您的App进行测试，并登录[ARMS控制台](https://arms.console.aliyun.com/#/home)查看数据报表。

