Reference of the SDK for iOS 
=================================================



Report custom information 
----------------------------------------------

Saves custom environment information and reports the environment information and exception information to the console when a mobile app quits unexpectedly.

Definition:

    /*!
    * @ brief Set user information.
    * @ details Set user information, which is reported to the console when a crash occurs. The total data size must be less than 10 KB.
    * @param key key
    * @param value value
    */
    + (void)configCustomInfoWithKey:(NSString *)key value:(NSString *)value;



Example:

    [AlicloudCrashProvider configCustomInfoWithKey:@"key" value:@"value"]; // Configuration item: the custom environment information (configCustomInfoWithKey and value).


**Note**

The total size of the values of the **key** and **value** parameters can be up to 10 KB. If the size exceeds 10 KB, the excessive data is discarded.

Report custom information based on the exception type 
--------------------------------------------------------------------------

Saves custom environment information and reports the environment information and exception information to the console when a specific exception occurs on a mobile app.

Definition:

    /*!
    * @ brief Set a callback message for crashes.
    * @ details Set a callback message for crashes.
    * @ param crashReporterAdditionalInformationCallBack The size of the returned dictionary cannot exceed 10 KB. Do not include a time-consuming operation. Only strings are supported.
    */
    + (void)setCrashCallBack:(NSDictionary * (^)(NSString * type))crashReporterAdditionalInformationCallBack;



Example:

    [AlicloudCrashProvider setCrashCallBack:^NSDictionary * _Nonnull(NSString * _Nonnull type) {
        return @{@"key":@"value"}; // Configuration item: the exception information (key and value).
    }];



Report a custom error 
------------------------------------------

Reports a custom error to the console.

Definition:

    /*!
    * @ brief Report a custom error.
    * @ details Report a custom error.
    * @ param error The error that is encapsulated as a standard NSError.
    */
    + (void)reportCustomError:(NSError *)error;



Example:

    NSError *error = [NSError errorWithDomain:@"customError" code:10001 userInfo:@{@"errorInfoKey":@"errorInfoValue"}];
    [AlicloudCrashProvider reportCustomError:error]; // Configuration item: the custom error information (errorWithDomain, code, and userInfo).


