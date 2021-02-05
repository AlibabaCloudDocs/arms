# Causes and solutions for script errors

Script errors are common errors. However, no complete error message or error stack is available for errors of this type. Therefore, it is difficult to troubleshoot these errors. This topic analyzes the causes, provides solutions, and shows you how to ignore this type of error in Application Real-Time Monitoring Service \(ARMS\).

## Causes of script errors

Script errors are also called cross-origin errors. When a website requests and executes a script hosted under a third-party domain name, a script error may occur. The most common scenario is to use a content delivery network \(CDN\) to host JavaScript resources.

For better understanding, assume that the following HTML page is deployed in the http://test.com domain:

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
  foo(); // Invokes the foo method defined in app.js.
  </script>
</body>
</html>
```

Assume that the `foo` method invokes an undefined `bar` method:

```
// another-domain.com/app.js
function foo() {
  bar(); // ReferenceError: bar is not a function
}
```

After the page is run, the following error is captured:

```
"Script error.", "", 0, 0, undefined 
```

In fact, this is not a JavaScript bug. For security reasons, browsers deliberately hide specific errors thrown by JavaScript files of other origins. This way, sensitive information can be effectively prevented from being inadvertently captured by uncontrolled third-party scripts. Therefore, only scripts from the same origin can capture specific error messages, whereas scripts from other origins can detect errors but cannot capture specific error messages. For more information, see [Webkit source code](https://trac.webkit.org/browser/branches/chromium/648/Source/WebCore/dom/ScriptExecutionContext.cpp).

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

The following sections describe how to resolve script errors.

## Solution 1: Enable cross-origin resource sharing

To capture JavaScript errors across origins, perform the following steps:

1.  Add the `crossorigin="anonymous"` attribute.

    ```
    <script src="http://another-domain.com/app.js" crossorigin="anonymous"></script>
    ```

    This step tells the browser to anonymously obtain third-party scripts. This means that the browser does not send potential user identity information, such as cookies and HTTP certificates, to the server when the browser requests scripts.

2.  Add the cross-origin HTTP response header.

    ```
    Access-Control-Allow-Origin: * 
    ```

    or

    ```
    Access-Control-Allow-Origin: http://test.com 
    ```

    **Note:** By default, most of mainstream CDNs have the `Access-Control-Allow-Origin` attribute. The following example is from Alibaba Cloud CDN:

    ```
    $ curl --head https://retcode.alicdn.com/retcode/bl.js | grep -i "access-control-allow-origin"
    => access-control-allow-origin: *
    ```


After the preceding two steps are performed, you can capture cross-origin errors by using the `window.onerror` handler. In the preceding example, after the page is run again, the following error is captured:

```
=> "ReferenceError: bar is not defined", "http://another-domain.com/app.js", 2, 1, [Object Error]
```

## Solution 2: Add the `try catch` statement \(Optional\)

When it is difficult to add a cross-origin attribute to the HTTP request or response header, add the `try catch` statement.

Add the `try catch` statement to the preceding HTML page:

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
    foo(); // Invokes the foo method defined in app.js.
  } catch (e) {
    console.log(e);
    throw e;
  }
  </script>
</body>
</html>
```

Run the page again. The following information is returned:

```
=> ReferenceError: bar is not defined
     at foo (http://another-domain.com/app.js:2:3)
     at http://test.com/:15:3
=> "Script error.", "", 0, 0, undefined
```

The `try catch` statement outputs complete error information in the console log, but the `window.onerror` handler outputs only script errors. You can manually report captured exceptions in the catch statement. For more information, see [API reference](/intl.en-US/Browser monitoring/API reference.md).

```
__bl.error(error, pos);
```

**Note:** Although the `try catch` statement can be used to capture some exceptions, we recommend that you use Solution 1.

## How can I ignore script errors in ARMS?

Script errors usually come from scripts under third-party domain names. If script errors does not affect the running of your application, you can ignore them by setting the ignore parameter of ARMS Browser Monitoring SDK.

The `ignore` parameter allows you to ignore the reporting of specified JavaScript errors. The value of this parameter is an object that contains three properties: ignoreUrls, ignoreApis, and ignoreErrors. The following code shows the default value of this parameter:

```
ignore: {
    ignoreUrls: [],
    ignoreApis: [],
    ignoreErrors: []
},
```

Use the ignoreErrors property to ignore script errors. The ignoreErrors property is used to ignore JavaScript errors that comply with a specified rule. The value of this property can be a string \(the String type\), a regular expression \(the RegExp type\), a method \(the Function type\), or an array that includes the preceding three types. The following code provides an example on how to ignore script errors:

```
__bl.setConfig({
    ignore: {
        ignoreErrors: /^Script error\.? $/
    }
});
```

## References

-   [API reference](/intl.en-US/Browser monitoring/API reference.md)
-   [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md)

