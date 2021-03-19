iOS SDK接口说明 
================================



上报自定义信息 
----------------------------

用于在移动应用发生Crash时，保存自定义环境信息，并随异常信息上报至控制台。

接口定义：

    /*!
    * @brief 设置用户信息
    * @details 设置用户信息，崩溃时带上。总数据量要求小于10Kb
    * @param key key
    * @param value value
    */
    + (void)configCustomInfoWithKey:(NSString *)key value:(NSString *)value;



使用示例：

    [AlicloudCrashProvider configCustomInfoWithKey:@"key" value:@"value"];//配置项：自定义环境信息（configCustomInfoWithKey/value）


**说明**

**key** 和 **value** 的字符串长度，合计须小于10Kb；否则，超出部分将被丢弃。

按异常类型上报自定义信息 
---------------------------------

用于在移动应用发生Crash时，针对特定异常类型，保存自定义环境信息，并随异常信息上报至控制台。

接口定义：

    /*!
    * @brief 设置崩溃回调信息
    * @details 设置崩溃回调信息
    * @param crashReporterAdditionalInformationCallBack 返回字典不超过10kb，不要有耗时操作，只支持字符串
    */
    + (void)setCrashCallBack:(NSDictionary * (^)(NSString * type))crashReporterAdditionalInformationCallBack;



使用示例：

    [AlicloudCrashProvider setCrashCallBack:^NSDictionary * _Nonnull(NSString * _Nonnull type) {
        return @{@"key":@"value"};//配置项：异常信息（key/value）
    }];



上报自定义错误 
----------------------------

用于将自定义错误上报至控制台。

接口定义：

    /*!
    * @brief 用户自定义错误上报
    * @details 用户自定义错误上报
    * @param error 用户把错误封装为标准NSError
    */
    + (void)reportCustomError:(NSError *)error;



使用示例：

    NSError *error = [NSError errorWithDomain:@"customError" code:10001 userInfo:@{@"errorInfoKey":@"errorInfoValue"}];
    [AlicloudCrashProvider reportCustomError:error];//配置项：自定义错误信息（errorWithDomain/code/userInfo）


