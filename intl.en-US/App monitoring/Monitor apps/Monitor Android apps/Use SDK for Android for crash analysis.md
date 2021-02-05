# Use SDK for Android for crash analysis

You can use SDK for app monitoring to obtain comprehensive crash analysis results, such as Java crash, native crash, ANR, and JavaScript errors that are captured.

An app monitoring task is created for the app. For more information, see [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md).

This topic applies to Android Studio projects that use Gradle to manage dependencies. For more information, visit [ha\_android\_demo](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo).

## Step 1: Add dependencies

Add Maven dependencies.

1.  Add the Alibaba Cloud Maven repository URL to the build.gradle project.

    ```
        repositories {    
        maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
        }
    ```

2.  Add the following code to the dependencies\{ \} code segment of the build.gradle project in the app module:

    ```
    compile('com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.2-open@aar') {
            transitive=true
        }
    compile('com.aliyun.ams:alicloud-android-ha-crashreporter:1.2.1-open@aar') {
            transitive=true
        }
    ```


## Step 2: Initialize the instance

1.  Start the crash analysis service in onCreate of the custom application class.

    ```
        public class MyApplication extends Application {
        @Override
        public void onCreate() {
            initHa();
        }
    
        private void initHa() {
           Log.e("ha", "init");
           //The preceding code is required. Otherwise, the server cannot receive data.
            AliHaAdapter.getInstance().openPublishEmasHa();
    
         AliHaConfig config = new AliHaConfig();
         config.appKey = "<yourAppKeyId>";         //appKey
           config.appVersion = "x.xx";         //The app version.
           config.appSecret = "<yourAppKeySecret>";  //appSecret
           config.channel = "<yourChannelId>";        //The custom channel ID of the app.
           config.userNick = null;
           config.application = this;
           config.context = getApplicationContext();
           config.isAliyunos = false;          // Specifies whether the app operating system is YunOS.
           AliHaAdapter.getInstance().startCrashReport(config);     // Starts CrashReport.
        }
    }
    ```

    **Note:** You can obtain the key-secret pair of the app from the file downloaded in the [Step](/intl.en-US/App monitoring/Create an app monitoring task.mdstep_c3d_tna_qn1)[4](/intl.en-US/App monitoring/Create an app monitoring task.mdstep_c3d_tna_qn1) section of the [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md) topic.

2.  Specify the custom application in AndroidManifest.xml.

    ```
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


## Step 3: Update the channel ID

```
AliHaAdapter.getInstance().updateChannel("600000");
```

## Step 4: Update the custom ID

```
AliHaAdapter.getInstance().updateUserNick("aliyun");
```

## Step 5: Add obfuscation rules

```
-keep class com.alibaba.ha.**{*;}
-keep class com.taobao.tlog.**{*;}
-keep class com.ut.device.**{*;}
-keep class com.ta.utdid2.device.**{*;}
-keep public class com.alibaba.mtl.** { *;}
-keep public class com.ut.mini.** { *;}
-keep class com.alibaba.motu.crashreporter.**{ *;}
-keep class com.uc.crashsdk.**{*;}
-keep class com.ali.telescope.**{ *;}
-keep class libcore.io.**{*;}
-keep class android.app.**{*;}
-keep class dalvik.system.**{*;}
-keep class com.taobao.tao.log.**{*;}
-keep class com.taobao.android.tlog.**{*;}
-keep class com.alibaba.motu.**{*;}
-dontwarn com.taobao.orange.**
-dontwarn com.taobao.android.**
-dontwarn com.alibaba.ha.adapter.**
-dontwarn com.taobao.monitor.adapter.**
-dontwarn com.alibaba.fastjson.**
-dontwarn com.ali.alihadeviceevaluator.**
-dontwarn java.nio.file.**
-dontwarn org.codehaus.mojo. **
```

## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home) to view the data reports.

