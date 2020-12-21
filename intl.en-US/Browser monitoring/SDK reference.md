# SDK reference

The browser monitoring feature of Application Real-time Monitoring Service \(ARMS\) allows you to configure a variety of SDK parameters to meet additional requirements, such as ignoring the reports of specific URLs, API operations, and JS errors, aggregating pages by filtering non-key characters from URLs, and reducing reports and loads by using random sampling.

## Index

[pid](#sc_pid) \| [uid](#sc_uid) \| [tag](#sc_tag) \| [page](#sc_page) \| [setUsername](#sc_setusername) \| [enableSPA](#sc_enablespa) \| [parseHash](#sc_parsehash) \| [disableHook](#sc_disablehook) \| [ignoreUrlCase](#sc_ignoreurlcase) \| [urlHelper](#sc_urlhelper) \| [apiHelper](#sc_apihelper) \| [parseResponse](#sc_parseresponse) \| [ignore](#sc_ignore) \| [disabled](#sc_disabled) \| [sample](#sc_sample) \| [sendResource](#sc_sendresource) \| [useFmp](#sc_usefmp) \| [enableLinkTrace](#sc_enablelinktrace) \| [release](#sc_release) \| [environment](#sc_environment) \| [behavior](#sc_behavior) \| [c1\\c2\\c3](#sc_custom) \| [autoSendPerf](#sc_autosendperf)

## Configure browser monitoring SDK parameters

You can configure browser monitoring SDK parameters in one of the following ways:

-   When you install an ARMS browser monitoring agent to a page, add extra parameters to config.

    For example, in the following sample code, in addition to the default pid parameter, the enableSPA parameter for single page application \(SPA\) is added to config.

    ```
    <script>
    !( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxxxxx",enableSPA:true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>                    
    ```

-   After the page is initialized, call the setConfig method in the JS code to modify the parameters.

    The following table describes the parameters that the `__bl.setConfig(next)` method calls.

    |Parameter|Type|Description|Required|Default value|
    |---------|----|-----------|--------|-------------|
    |next|Object|The configuration item and its value that you want to modify.|Yes|None|

    The following code provides an example on how to modify the disableHook parameter to disable automatic API reporting:

    ```
    __bl.setConfig({
        disableHook: true
    });            
    ```


## pid |
| |

[\[Back to the top\]](#sc_index)

## uid |
| |

[\[Back to the top\]](#sc_index)

## tag |
| |

[\[Back to the top\]](#sc_index)

## page |
| |

[\[Back to the top\]](#sc_index)

## setUsername |
| |

This parameter is used to configure a method that returns a user name as a string. After you configure this parameter, you can use the returned user name to perform full link tracing on the user and query the sessions related to the user.

**Note:** If the user name cannot be obtained when the page starts to be loaded, you can set the return value to null rather than a temporary user name. In general, the SDK calls the setUsername method to obtain the user name when it sends logs. However, if you set the return value to a temporary user name, the SDK uses the temporary user name and does not call setUsername to obtain the user name.

The following code provides an example on how to call the setConfig method to modify SDK parameters:

```
// Call the setConfig method to modify the SDK parameters.
__bl.setConfig({
    setUsername: function () {
        return "username_xxx";
    }
});            
```

[\[Back to the top\]](#sc_index)

## enableSPA |
| |

[\[Back to the top\]](#sc_index)

## parseHash |
| |

In SPA scenarios \(see [t152282.md\#](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md)\), if enableSPA is set to `true` and the page triggers a hashchange event, the parseHash parameter is used to resolve the URL hash into Page.

**Default value**

The default value is obtained using the following string processing method:

```
function (hash) {
    var page = hash ? hash.replace(/^#/, '').replace(/\?.*$/, '') : '';
    return page || '[index]';
}           
```

You do not need to modify this parameter in most cases. However, if you want to use a custom page name to report data or the URL hash is complex, you can modify this parameter. Example:

```
// Define the mapping between the hash values and pages.
var PAGE_MAP = {
    '/': 'Homepage',
    '/contact': 'Contact us',
    '/list': 'Data list',
    // ...
};
// Call the SDK method after the page is loaded.
window.addEventListener('load', function (e) {
    // Call the setConfig method to modify the SDK parameters.
    __bl.setConfig({
        parseHash: function (hash) {
            key = hash.replace(/\?.*$/, '');
            return PAGE_MAP[key] || 'Unknown page';
        }
    });
});
```

[\[Back to the top\]](#sc_index)

## disableHook |
| |

[\[Back to the top\]](#sc_index)

## ignoreUrlCase |
| |

[\[Back to the top\]](#sc_index)

## urlHelper |
| |

When a page URL is in a similar format as `http://xxx.com/projects/123456` \(projects is followed by the project ID\) and `xxx.com/projects/123456` is reported as a page, the page cannot be aggregated during data browsing. To implement page aggregation, set the urlHelper parameter to filter non-key characters such as the project ID in this example.

**Note:**

-   The parameter ignoreUrlPath was used to configure URL filtering rules and is replaced by the urlHelper parameter. If you use the ignoreUrlPath parameter, the configuration still takes effect. If you use the ignoreUrlPath and urlHelper parameters at the same time, the configuration specified by urlHelper takes effect.
-   This parameter is valid only when the page URL is automatically obtained and used as Page. This parameter is invalid if you manually modify Page by calling the setPage or setConfig method \(see [API reference](/intl.en-US/Browser monitoring/Methods user guide.md)\) or the enableSPA parameter is set to `true`.

**Default value**

The default value of this parameter is the following array and does not need to be modified.

```
[
    // Replace all numbers in the URL with asterisks (*).
    {rule: /\/([a-z\-_]+)? \d{2,20}/g, target: '/$1**'},
    // Remove the forward slash (/) at the end of the URL.
    /\/$/
]                    
```

The default value of this parameter filters out the numbers in strings such as `xxxx/123456`. For example, `xxxx/00001` and `xxxx/00002` are modified to `xxxx/**`.

**Value type**

The value of urlHelper can be one of the following types:

-   `String` or `RegExp` \(regular expression\): The matched strings are removed.
-   `Object<rule, target>`: The object contains two keys: rule and target, which are the input parameters of the replace method of the JS string. For more information, see the String::replace method described in related JS tutorials.
-   `Function`: The original string is used as the input parameter for method execution, and the execution result is used as Page.
-   `Array`: This type is used to set multiple rules. The type of each rule can be one of the preceding types.

[\[Back to the top\]](#sc_index)

## apiHelper |
| |

This parameter filters out non-key characters in API URLs when the results of API operations are automatically reported. The usage and function of this parameter are the same as those of [urlHelper](#sc_urlhelper).

**Note:** The parameter ignoreApiPath was used to configure API filtering rules and is replaced by the apiHelper parameter. If you use the ignoreApiPath parameter, the configuration still takes effect. If you use the ignoreApiPath and apiHelper parameters at the same time, the configuration specified by apiHelper takes effect.

**Default value**

The default value of this parameter is an object and does not need to be modified.

```
{rule: /(\w+)\/\d{2,}/g, target: '$1'}                    
```

The default value of this parameter filters out the numbers in strings such as `xxxx/123456`.

[\[Back to the top\]](#sc_index)

## parseResponse |
| |

This parameter parses the data returned when the results of API operations are automatically reported.

**Default value**

The following code shows the default value of this parameter:

```
function (res) {
    if (! res || typeof res ! == 'object') return {};
    var code = res.code;
    var msg = res.msg || res.message || res.subMsg || res.errorMsg || res.ret || res.errorResponse || '';
    if (typeof msg === 'object') {
        code = code || msg.code;
        msg = msg.msg || msg.message || msg.info || msg.ret || JSON.stringify(msg);
    }
    return {msg: msg, code: code, success: true};
}                    
```

The preceding code parses the returned data and tries to extract `msg` and `code`. For common applications, the default value of this parameter does not need to be modified. If the default value cannot meet your business requirements, you can set a new value.

[\[Back to the top\]](#sc_index)

## ignore |
| |

The value of ignore is an object that contains four attributes: ignoreUrls, ignoreApis, ignoreErrors, and ignoreResErrors. You can set one or more attributes of the parameter value.

**Default value**

The following code shows the default value of this parameter:

```
ignore: {
        ignoreUrls: [],
        ignoreApis: [],
        ignoreErrors: [],
        ignoreResErrors: []
    },                    
```

ignoreUrls

The ignoreUrls attribute is used to ignore reports from specific URLs. Logs from the URLs that comply with the specified rule are not reported. The value of this attribute can be a string \(the `String` type\), a regular expression \(the `RegExp` type\), a method \(the `Function` type\), or an array that includes the preceding three types. Example:

```
__bl.setConfig({
                ignore: {
                    ignoreUrls: [
                    'http://host1/',  // Character string
                    /. +? host2. +/,     // Regular expression
                    function(str) {   // Method
                        if (str && str.indexOf('host3') >= 0) {
                            return true; // The data is not reported.
                        }
                        return false; // The data is reported.
                    }]
                }
            });                    
```

ignoreApis

The ignoreApis attribute is used to ignore the reports from APIs that comply with a specified rule. The value of this attribute can be a string \(the `String` type\), a regular expression \(the `RegExp` type\), a method \(the `Function` type\), or an array that includes the preceding three types. Example:

```
__bl.setConfig({
                ignore: {
                    ignoreApis: [
                    'api1','api2','api3', // Character string
                    /^random/,  // Regular expression
                    function(str) { // Method
                        if (str && str.indexOf('api3') >= 0) return true; // The data is not reported.
                        return false; // The data is reported.
                    }]
                }
            });                    
```

ignoreErrors

The ignoreErrors attribute is used to ignore JS errors that comply with a specified rule. The value of this attribute can be a string \(the `String` type\), a regular expression \(the `RegExp` type\), a method \(the `Function` type\), or an array that includes the preceding three types. Example:

```
__bl.setConfig({
                ignore: {
                    ignoreErrors: [
                    'test error', // Character string
                    /^Script error\.? $/, // Regular expression
                    function(str) { // Method
                        if (str && str.indexOf('Unknown error') >= 0) return true;   // The error is not reported.
                        return false;   // The error is reported.
                    }]
                }
            });            
```

ignoreResErrors

The ignoreErrors attribute is used to ignore resource errors that comply with a specified rule. The value of this attribute can be a string \(the `String` type\), a regular expression \(the `RegExp` type\), a method \(the `Function` type\), or an array that includes the preceding three types. Example:

```
__bl.setConfig({
                ignore: {
                    ignoreResErrors: [
                    ' http://xx/picture.jpg ', // String
                    /jpg$/, // Regular expression
                    function(str) { // Method
                        if (str && str.indexOf('xx.jpg') >= 0) return true;   // The error is not reported.
                        return false;   // The error is reported.
                    }]
                }
            });
```

[\[Back to the top\]](#sc_index)

## disabled |
| |

[\[Back to the top\]](#sc_index)

## sample |
| |

You can configure this parameter to randomly sample and report performance logs and successful API logs to reduce the number of reports and the load. ARMS restores the data based on the sampling configuration when ARMS processes the reported logs in the background. Therefore, this parameter does not affect the reporting of other types of logs such as JS error logs and failed API logs.

The default value of `sample` is `1`. The valid values of this parameter are `1`, `10`, and `100`, which separately indicate the sampling rates of 100%, 10%, and 1%. The sampling rate can be calculated using the following formula: `1/Value of sample`.``````

**Warning:** Sampling is performed randomly. If the number of reported items is small, this parameter may cause large statistical result errors. We recommend that you use this parameter for the websites whose daily average PV is more than 1 million.

[\[Back to the top\]](#sc_index)

## sendResource |
| |

If sendResource is set to `true`, the static resources loaded to the current page are reported when the load event of the page is triggered. If the page loading speed is slow, you can view the static resource waterfall chart on the Session Traces page to determine the cause.

The following code provides an example on how to configure the sendResource parameter:

```
<script>
!( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxxxxx",sendResource:true};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>            
```

**Note:** The value of this parameter is checked when the load event of the page is triggered. Therefore, configure sendResource in config as shown in the preceding example. Do not use the setConfig method because this method may check the value of this parameter after the load event of the page is complete. In this case, the configuration of this parameter does not take effect.

[\[Back to the top\]](#sc_index)

## useFmp |
| |

[\[Back to the top\]](#sc_index)

## enableLinkTrace |
| |

[\[Back to the top\]](#sc_index)

## release |
| |

[\[Back to the top\]](#sc_index)

## environment |
| |

[\[Back to the top\]](#sc_index)

## behavior |
| |

[\[Back to the top\]](#sc_index)

## autoSendPerf |
| |

[\[Back to the top\]](#sc_index)

## c1\\c2\\c3

In addition to the preceding parameters, you may need to specify more information to handle business problems. Therefore, ARMS SDK provides three parameters for which you can customize fields. After you configure a custom parameter, the fields of the parameter are included in each reported log. |
| |
| |

[\[Back to the top\]](#sc_index)

**Related topics**  


[API reference](/intl.en-US/Browser monitoring/Methods user guide.md)

[t152282.md\#](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md)

[Pre-report data]()

