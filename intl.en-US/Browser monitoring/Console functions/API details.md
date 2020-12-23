# API details

The API Details page of Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring shows the success rate of all API requests, average response time \(RT\) of successful calls, average RT of failed calls, number of slow responses, and number of errors in a specified period. This page also shows statistics for API requests initiated in five dimensions such as regions, domain names, and networks.

## Portal

1.  Log on to the[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Browser Monitoring**.
3.  On the **Browser Monitoring** page, click the name of the required application.
4.  In the left-side navigation pane, choose **Application** \> **API Details** to go to the API Details page.

    The page is divided into three sections.

    ![API details](../images/p111559.png "API details")


## Filters

Set filters in different dimensions to view the corresponding API information. Valid values: **API**, **Return Message**, **HTTP Status Code**, **Page**, **Geography**, **OS**, **Domain Name**, **Connection Type**, **Device**, and **Browser**.

To delete a filter, move the pointer over the filter and click the ![delete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3313758061/p175853.png) icon. Click Reset to clear all filters.

![API details filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3993227951/p111568.png)

## Success rate

In the API Request section, select **API Success Rate** to view the success rate, successful requests, error number, and users with API errors.

-   Success rate: The success rate of all API requests to the specified application within a specified period of time is displayed in a line chart, which corresponds to the y-axis on the right side.
-   Successful requests: The number of calls per hour within a specified period of time is displayed in a blue bar chart, which corresponds to the y-axis on the left side.
-   Error number: The number of calls per hour within a specified period of time is displayed in a yellow bar chart, which corresponds to the y-axis on the left side.

Move the pointer over the bar chart to view the success rate, successful requests, error number, and users with API errors within a specified period of time.

## Success RT or failure RT

In the API Request section, select **Success RT** or **Failure RT** to view the average RT of successful calls, average RT of failure calls, count of calls whose RT is smaller than or equal to 1,000ms, and count of calls whose RT is greater than 1,000ms.

-   Success Avg RT or failure Avg RT: The average success RT or failure RT of all API calls in an application within a specified period of time is displayed in a line chart, which corresponds to the y-axis on the right side.
-   Calls <= 1000ms: The total number of successful calls or failed calls smaller than or equal to 1000 ms per hour is displayed in a blue bar chart, which corresponds to the y-axis on the left side.
-   Calls \> 1000ms: The total number of successful calls or failed calls greater than 1000 ms per hour is displayed in a yellow bar chart, which corresponds to the y-axis on the left side.

## Slow responses

**Note:** Slow responses refer to the number of calls that take more than 1000ms.

In the API Request section, select **Slow Responses** to view the slow responses.

Slow responses: The number of all API requests within a specified period of time is displayed in a bar chart, which corresponds to the y-axis on the left side.

## Error number

In the API Request section, select **Error Number** to view the number of failed requests.

Error Number: The number of all API errors within a specified period of time is displayed in a bar chart, which corresponds to the y-axis on the left side.

## API requests

Select **API Requests** in the section ③ to view the requests of each API within a specified period of time.

-   Click the![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over an API alias in the **API** column. Click the ![edit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3313758061/p177320.png) icon to modify the alias of the API. All APIs are displayed by alias. Click **Set To Search Value** to set the API to a filter.
-   Click a number in the **Error Number** column to view the details and distribution of errors within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of failed requests. Click **View Session** to view the session trace of failed requests.
-   Click a number in the **Slow Responses** column to display the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.
-   Click **Analyze** in the **Operation** column to view the API details, API error details, API slow loading details, and distribution.
    -   On the API details page, you can view the API success rate and request details. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. Click **View Session**, you can view the session trace of the API.
    -   On the API Error Details page, you can view the distribution of the error number and request details.
    -   On the API Slow Loading Details page, you can view the response time distribution and network request information.
    -   On the Distribution page, you can view the return message, HTTP status code, page, domain name, and geography. You can also view the proportions by OS, browser, device, or connection type.

## Responses

Select **Responses** in the section ③ to view all response information of each API.

-   Click the![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over a response in the **Responses** column. Click **Set To Search Value** to set the response to a filter.
-   Click a number in the **Slow Responses** column to display the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.
-   Click **Analyze** in the **Operation** column to view the API details, API error details, API slow loading details, and distribution.
    -   On the API details page, you can view the API success rate and request details. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. Click **View Session**, you can view the session trace of the API.
    -   On the API Error Details page, you can view the distribution of the error number and request details.
    -   On the API Slow Loading Details page, you can view the response time distribution and network request information.
    -   On the Distribution page, you can view the return message, HTTP status code, page, domain name, and geography. You can also view the proportions of the OS, browser, device, and connection type.

## HTTP status code

Select an **HTTP Status Code** in section ③ to view all HTTP status codes.

-   Click the![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over an HTTP status code in the **HTTP Status Code** column. Click **Set To Search Value** to set the HTTP status code to a filter.
-   Click a number in the **Slow Responses** column to display the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.
-   Click **Analyze** in the **Operation** column to view the API details, API error details, API slow loading details, and distribution.
    -   On the API details page, you can view the API success rate and request details. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. Click **View Session**, you can view the session trace of the API.
    -   On the API Error Details page, you can view the distribution of the error number and request details.
    -   On the API Slow Lading Details page, you can view the response time distribution and network request information.
    -   On the Distribution page, you can view the return message, HTTP status code, page, domain name, and geography. You can also view the proportions of the OS, browser, device, and connection type.

## Distribution

Select **Distribution** in the section ③. You can view the return message, HTTP status code, page, domain name, and geography. You can also view the proportions of the OS, browser, device, and connection type. Move the pointer over the **Domain Name** or **Page** column. Click **Set To Search Value** to set the domain name or page to a filter.

**Note:**

-   Versions numbers can be displayed only by OS or browser.
-   The pie chart of OS, browser, device, and connection type displays only the dimensional distribution of the first five items. You can click Toggle View in the upper-right corner of each section to view the proportion of all filters in this dimension.

