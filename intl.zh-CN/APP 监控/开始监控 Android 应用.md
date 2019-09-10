# 开始监控 Android 应用 {#task_2117993 .task}

本文适用于 Andriod 应用的接入。APP 监控提供了完备的客户端崩溃分析监控，具体包括 JAVA Crash 监控、Native Crash 监控和 ANR 监控等。

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择 **APP 监控** 。
2.  在 APP 监控页面，单击右上角的**添加 APP 监控**。
3.  在弹出的添加 APP 监控对话框的填写应用信息页签输入应用名称和 Android 应用的 PackageName，并选择 **Android** 平台，单击**创建应用**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1680661/156810140059954_zh-CN.png)

4.  在查看配置页签复制 AppKey 和 AppSecret 的值，单击**下一步**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1680661/156810140059955_zh-CN.png)

5.  添加 Android SDK。此内容适用于使用 Gradle 管理依赖的 Android Studio 项目。 
    1.  在程序中引入阿里云 Maven 仓库依赖。 
        1.  在项目 build.gradle 中添加阿里云 Maven 仓库地址。

            ``` {#codeblock_n37_rpg_cwb}
            repositories{
                maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }   
            }
            ```

        2.  在 APP 模块的 build.gradle 的 dependencies 节点中添加以下依赖。

            ``` {#codeblock_pa3_x5u_m8e}
            compile('com.aliyun.ams:alicloud-android-ha-adapter:1.1.2.2-open@aar') {
                transitive=true
            }
            ```

    2.  初始化实例。 
        1.  在自定义 Application 类的 onCreate 里面启动服务。

            ``` {#codeblock_j07_jgj_q72}
            public class MyApplication extends Application {
                @Override
                public void onCreate() {
                    initHa();
                }
            
                private void initHa() {
                   Log.e("ha", "init");
                   //这里必须启动，否则服务端收不到数据
                    AliHaAdapter.getInstance().openPublishEmasHa();
            
                 AliHaConfig config = new AliHaConfig();
                 config.appKey = "<yourAppKeyId>";         //appkey
                   config.appVersion = "x.xx";         //应用的版本号信箱
                   config.appSecret = "<yourAppKeySecret>";  //appsecret
                   config.channel = "<yourChannelId>";        //应用的渠道号标记，自定义
                   config.userNick = null;
                   config.application = this;
                   config.context = getApplicationContext();
                   config.isAliyunos = false;          //是否为yunos
                   AliHaAdapter.getInstance().startCrashReport(config);     //启动CrashReport
                }
            }
            ```

        2.  AndroidManifest.xml 里面指定自定义 Application。

            ``` {#codeblock_cvh_30z_bb4}
            <application
                android:name=".MyApplication"
                android:allowBackup="true"
                android:icon="@mipmap/ic_launcher"
                android:label="@string/app_name"
                android:supportsRtl="true"
                android:theme="@style/AppTheme" >
                ```
                ```
            </application>
            ```

    3.  更新渠道标记。 

        ``` {#codeblock_kjn_k35_g84}
        AliHaAdapter.getInstance().updateChannel("600000");
        ```

    4.  更新自定义标记。 

        ``` {#codeblock_t18_k10_tea}
        AliHaAdapter.getInstance().updateUserNick("aliyun");
        ```


在完成上述步骤之后，您可以对您的 APP 进行测试，并登录 [ARMS 控制台](https://arms-intl.console.aliyun.com/#/home)查看数据报表。

