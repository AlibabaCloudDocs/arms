Android SDK接口说明 
====================================



上报自定义信息 
----------------------------

用于在移动应用发生Crash时，保存自定义环境信息，并随异常信息上报至控制台。

    AliHaAdapter.getInstance().addCustomInfo("key", "value"); //配置项：自定义环境信息


**说明**

**key** 和 **value** 的字符串长度，合计须小于10K；否则，超出部分将被丢弃。

按异常类型上报自定义信息 
---------------------------------

用于在移动应用发生Crash时，针对特定异常类型，保存自定义环境信息，并随异常信息上报至控制台。

    AliHaAdapter.getInstance().setErrorCallback(new ErrorCallback() {
        @Override
        public Map<String, String> onError(ErrorInfo callbackInfo) {
            Map<String, String> infos = new HashMap<>();
            infos.put("key", "value"); //配置项：异常信息
            return infos;
        }
    });



其中，Crash回调类定义：

    public interface ErrorCallback {
        Map<String, String> onError(ErrorInfo var1);
    }



异常类型参照ErrorInfo定义：

    public class ErrorInfo {
        /** Java crash */
        public static final int HA_CRASH_JAVA = 1;
        /** Native crash */
        public static final int HA_CRASH_NATIVE = 2;
        /** ANR */
        public static final int HA_CRASH_ANR = 3;
        /** Memory leak */
        public static final int HA_MEM_LEAK = 4;
        /** Main thread block */
        public static final int HA_MAIN_THREAD_BLOCK = 5;
        /** Main thread io */
        public static final int HA_MAIN_THREAD_IO = 6;
        /** Big bitmap*/
        public static final int HA_BIG_BITMAP = 7;
        /** File description over flow*/
        public static final int HA_FD_OVERFLOW = 8;
        /** Resource leak */
        public static final int HA_RESOURCE_LEAK = 9;
        /** Custom error */
        public static final int HA_CUSTOM_ERROR = 10;
    
        /**
         * 获取错误类型
         * @return 返回错误类型
         */
        public int getErrorType() {
            return this.mErrorType;
        }
    
        /**
         * 获取异常信息
         * @return 返回异常实例
         */
        public Throwable getThrowable() {
            return this.mThrowable;
        }
    }



上报自定义错误 
----------------------------

用于将自定义错误上报至控制台。

    AliHaAdapter.getInstance().reportCustomError(new RuntimeException("custom error")); //配置项：自定义错误



