# Use SDK for Android for performance analysis

You can use SDK for app monitoring to obtain comprehensive performance analysis results for mobile apps.

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

2.  Add the following code to the dependency node of the build.gradle project in the app module:

    ```
    compile('com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.2-open@aar') {
            transitive=true
        }
    compile('com.aliyun.ams:alicloud-android-apm:1.0.7.7-open@aar') {
            transitive=true
        }
    ```


## Step 2: Integrate the service

1.  Start the performance analysis service in onCreate of the custom application class.

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
                 config.appVersion = "x.xx";         //The app version.
                 config.appSecret = "xxxxxxxxxxxx";  //appSecret
                 config.channel = "mqc_test";        //The custom channel ID of the app.
                 config.userNick = null;
                 config.application = this;
                 config.context = getApplicationContext();
                 config.isAliyunos = false;          // Specifies whether the app  operating system is YunOS.
                 AliHaAdapter.getInstance().addPlugin(Plugin.apm);
                 AliHaAdapter.getInstance().start(config);
            }
        }
    ```

    **Note:** You can obtain the key-secret pair of the app from the file downloaded in the [Step 4](/intl.en-US/App monitoring/Create an app monitoring task.mdstep_c3d_tna_qn1)[4](/intl.en-US/App monitoring/Create an app monitoring task.mdstep_c3d_tna_qn1) section of the [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md) topic.

2.  Specify the custom application in AndroidManifest.xml.

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


## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home)to view the data reports.

