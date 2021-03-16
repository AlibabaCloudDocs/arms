Reference of the SDK for Android 
=====================================================



Report custom information 
----------------------------------------------

Saves custom environment information and reports the environment information and exception information to the console when a mobile app quits unexpectedly.

    AliHaAdapter.getInstance().addCustomInfo("key", "value"); // Configuration item: the custom environment information.


**Note**

The total size of the values of the **key** and **value** parameters can be up to 10 KB. If the size exceeds 10 KB, the excessive data is discarded.

Report custom information based on the exception type 
--------------------------------------------------------------------------

Saves custom environment information and reports the environment information and exception information to the console when a specific exception occurs on a mobile app.

    AliHaAdapter.getInstance().setErrorCallback(new ErrorCallback() {
        @Override
        public Map<String, String> onError(ErrorInfo callbackInfo) {
            Map<String, String> infos = new HashMap<>();
            infos.put("key", "value"); // Configuration item: the exception information.
            return infos;
        }
    });



Definition of the ErrorCallback interface:

    public interface ErrorCallback {
        Map<String, String> onError(ErrorInfo var1);
    }



Definition of the ErrorInfo class:

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
         * Obtain the error type.
         * @return The error type.
         */
        public int getErrorType() {
            return this.mErrorType;
        }
    
        /**
         * Obtain the exception.
         * @return The exception instance.
         */
        public Throwable getThrowable() {
            return this.mThrowable;
        }
    }



Report a custom error 
------------------------------------------

Reports a custom error to the console.

    AliHaAdapter.getInstance().reportCustomError(new RuntimeException("custom error")); // Configuration item: the custom error information.



