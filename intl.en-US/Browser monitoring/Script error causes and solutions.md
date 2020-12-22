# Script error causes and solutions

Script errors are common errors. However, no complete error message \(error stack\) is available for errors of this type. Therefore, it is difficult to troubleshoot the errors. This topic analyzes causes for script errors, provides solutions, and describes how to ignore these errors in Application Real-Time Monitoring Service \(ARMS\).

## Causes of script errors

Script errors are also called cross-origin errors. When a website requests and executes a script hosted under a third-party domain name, a script error may occur. In most cases, a Content Delivery Network \(CDN\) is used to host JavaScript resources.

For an easy description, assume that the following HTML page is deployed in the http://test.com domain:

```
<! doctype html>
<html>
<head>
  <title>Test page in http://test.com</title>
</head>
<body>
  <script src="http://another-domain.com/app.js"></script>
  <script>
  window.onerror = function (message, url, line, column, error) {
    console.log(message, url, line, column, error);
  }
  foo(); // Call the foo method defined in app.js
  </script>
</body>
</html>
```

Assume that the `foo` method calls an undefined `bar` method:

```
// another-domain.com/app.js
function foo() {
  bar(); // ReferenceError: bar is not a function
}
```

After the page is run, the captured exception information is as follows:

```
"Script error.", "", 0, 0, undefined 
```

In fact, this is not a JavaScript bug. For security purposes, the browser deliberately hides specific error messages thrown by JavaScript files of other domains to prevent sensitive information from being captured accidentally by uncontrolled third-party scripts. Therefore, only scripts in the same domain can capture specific error messages, while scripts in other domains can detect errors but cannot capture specific error messages.

For more information, see [Webkit source code](https://trac.webkit.org/browser/branches/chromium/648/Source/WebCore/dom/ScriptExecutionContext.cpp):

```
bool ScriptExecutionContext::sanitizeScriptError(String& errorMessage, int& lineNumber, String& sourceURL)
    {
        KURL targetURL = completeURL(sourceURL);
        if (securityOrigin()->canRequest(targetURL))
            return false;
        errorMessage = "Script error.";
        sourceURL = String();
        lineNumber = 0;
        return true;
    }
```

The following describes how to resolve script errors.

## Solution 1: Enable Cross Origin Resource Sharing \(CORS\)

To capture JavaScript errors across origins, take the following steps:

1.  Add the `crossorigin="anonymous"` attribute.

    ```
    <script src="http://another-domain.com/app.js" crossorigin="anonymous"></script>
    ```

    This step tells the browser to obtain target scripts anonymously. This means that the browser does not send potential user identity information \(for example, cookies and HTTP certificates\) to the server when requesting scripts.

2.  Add the cross-origin HTTP response header

    ```
    Access-Control-Allow-Origin: * 
    ```

    or

    ```
    Access-Control-Allow-Origin: http://test.com 
    ```

    **Note:** By default, most mainstream CDNs have the `Access-Control-Allow-Origin` attribute. The following shows an example of Alibaba Cloud CDN:

    ```
    $ curl --head https://retcode.alicdn.com/retcode/bl.js | grep -i "access-control-allow-origin"
    => access-control-allow-origin: *
    ```


After completing the preceding steps, you can use `window.onerror` to capture cross-origin script error messages. In the preceding example, after the page is run again, the captured result is as follows:

```
=> "ReferenceError: bar is not defined", "http://another-domain.com/app.js", 2, 1, [Object Error]
```

## Solution 2 \(optional \): Use `try catch`

When it is difficult to add a cross-origin attribute to the HTTP request or response header, use `try catch`.

Add `try catch` to the preceding HTML page:

```
<! doctype html>
<html>
<head>
  <title>Test page in http://test.com</title>
</head>
<body>
  <script src="http://another-domain.com/app.js"></script>
  <script>
  window.onerror = function (message, url, line, column, error) {
    console.log(message, url, line, column, error);
  }
  try {
    foo(); // Call the foo method defined in app.js
  } catch (e) {
    console.log(e);
    throw e;
  }
  </script>
</body>
</html>
```

Run the page again. The output results are as follows:

```
=> ReferenceError: bar is not defined
     at foo (http://another-domain.com/app.js:2:3)
     at http://test.com/:15:3
=> "Script error.", "", 0, 0, undefined
```

Complete information is displayed through the console statement of `try catch`, but from `window.onerror`, only "Script error" can be captured. Using this feature, you can manually report captured exceptions in the CATCH statement.

```
// See "Browser monitoring operations" at the end of this topic.
__bl.error(error, pos);
```

**Note:** Although `try catch` can be used to capture some exceptions, we recommend that you use solution 1.

## How do I ignore script errors in ARMS?

Script errors are often caused by scripts in third-party domains. If the errors do not affect the running of your application, you can ignore the errors by using the ignore SDK parameter of ARMS browser monitoring.

The `ignore` parameter is used to ignore JavaScript errors that are reported. The parameter value is an object that comprises three attributes: ignoreUrls, ignoreApis, and ignoreErrors. The default value is as follows:

```
ignore: {
    ignoreUrls: [],
    ignoreApis: [],
    ignoreErrors: []
},
```

You can only use the ignoreErrors attribute for script errors. The ignoreErrors attribute is used to ignore certain JavaScript errors that comply with a specified rule. The value can be String, RegExp, Function or an array composed of the three types. Example:

```
__bl.setConfig({
    ignore: {
        ignoreErrors: /^Script error\.? $/
    }
});
```

