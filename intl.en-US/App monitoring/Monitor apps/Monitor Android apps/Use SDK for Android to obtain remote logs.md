# Use SDK for Android to obtain remote logs

You can use SDK for app monitoring to obtain comprehensive remote logs.

An app monitoring task is created for the app. For more information, see [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md).

This topic applies to Android Studio projects that use Gradle to manage dependencies. For more information, visit [ha\_android\_demo](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo).

**Note:** Logs can be stored on mobile clients for a maximum of seven days.

## Step 1: Add dependencies

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
    compile('com.aliyun.ams:alicloud-android-ha-tlog:1.1.2.2-open@aar') {
            transitive=true
        }
    ```


## Step 2: Integrate the service

1.  Start the service in onCreate of the custom application class.

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
             config.appVersion = "x.xx";         //The app version.
             config.appSecret = "xxxxxxxxxxxx";  //appsecret
             config.channel = "mqc_test";        //The custom channel ID of the app.
             config.userNick = null;
             config.application = this;
             config.context = getApplicationContext();
             config.isAliyunos = false;          //Specifies whether the app operating system is YunOS.
             config.rsaPublicKey = "xxxxxxx";    //The public key of TLog. This parameter is required. The appmonitor.tlog.rsaSecret field in the aliyun-emas-services.json file downloaded from the Enterprise Mobile Application Studio (EMAS) console indicates the public key information. To download the file, go to the EMAS console, click App Management in the left-side navigation pane, and then find the desired app. In the upper-right corner, click Configuration Download.
             AliHaAdapter.getInstance().addPlugin(Plugin.tlog);
             AliHaAdapter.getInstance().openDebug(true);
             AliHaAdapter.getInstance().start(config);
        }
    }
    ```

    **Note:** You can obtain the key-secret pair of the app from the file downloaded in the [Step 4](/intl.en-US/App monitoring/Create an app monitoring task.mdstep_c3d_tna_qn1) section of the [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md) topic.

2.  Specify the custom application in AndroidManifest.xml.

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

3.  Add the following code to the defaultConfig node of build.gradle in the app module to configure Application Binary Interface \(ABI\):

    ```
    ndk {
            abiFilters 'armeabi-v7a'
        }
    ```


## Step 3: Obtain the remote logs

1.  Import the header file for the workflow to trigger the log information to be exported.

    ```
    import com.alibaba.ha.adapter.service.tlog.TLogService;
    ```

2.  Add code to the appropriate location to export the log information. Sample code:

    ```
    String TAG = "xxx";
    String MODEL = "xxxxx";
    
    TLogService.logv(MODEL,TAG,"test tlog1");
    TLogService.logd(MODEL,TAG,"test tlog2");
    TLogService.logi(MODEL,TAG,"test tlog3");
    TLogService.logw(MODEL,TAG,"test tlog4");
    TLogService.loge(MODEL,TAG,"test tlog5");
    ```


## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home) to view the data reports.

