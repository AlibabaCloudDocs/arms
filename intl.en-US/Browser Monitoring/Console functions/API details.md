# API details

The API Details page of Application Real-Time Monitoring Service \(ARMS\) frontend monitoring shows the success rate of all API calls, average response time \(RT\) of successful API calls, average RT of failed API calls, number of slow responses, and number of failed API calls in a specified period of time. This page also shows statistics for API calls initiated in five dimensions such as regions, domain names, and network connection types.

## Go to the API Details page

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Browser Monitoring**.
3.  On the **Browser Monitoring** page, click the name of the application that you want to view.
4.  In the left-side navigation pane, choose **Application** \> **API Details** to go to the API Details page.

    The page is divided into three sections.

    ![API details](../images/p111559.png "API Details page")


## Filters

Set filters in different dimensions to view the information about the corresponding API. Valid filters include **API**, **Return Message**, **HTTP Status Code**, **Page**, **Geography**, **OS**, **Domain Name**, **Connection Type**, **Device**, and **Browser**.

To delete a filter, move the pointer over the filter and click the ![delete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3313758061/p175853.png) icon. You can also click Reset to clear all filters.

![API details filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3993227951/p111568.png)

## Success Rate

In the API Request Statistics section, click **Success Rate** to view the success rate of API calls, number of successful API calls, number of failed API calls, and number of users with failures.

![success](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0071378061/p177857.png)

-   Success Rate: The success rate of all API calls in the selected application within a specified period of time is displayed in a curve chart. The data corresponds to the y-axis on the right side.
-   Successful Requests: The number of API calls per hour within a specified period of time is displayed in a blue bar chart. The data corresponds to the y-axis on the left side.
-   Error Number: The number of failed API calls per hour within a specified period of time is displayed in a yellow bar chart. The data corresponds to the y-axis on the left side.

Move the pointer over the chart to view the success rate of API calls, number of successful API calls, number of failed API calls, and number of users with failures.

## Success RT or Failure RT

In the API Request Statistics section, click **Success RT** or **Failure RT** to view the average RT for successful or failed API calls, number of API calls whose RT is smaller than or equal to 1,000 ms, and number of API calls whose RT is greater than 1,000 ms.

![time](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0071378061/p177858.png)

-   Success Avg RT or Failure Avg RT: The average RT for successful or failed API calls in the selected application within a specified period of time is displayed in a curve chart. The data corresponds to the y-axis on the right side.
-   Calls <= 1000ms: The total number of successful or failed API calls whose RT is smaller than or equal to 1,000 ms per hour is displayed in a blue bar chart. The data corresponds to the y-axis on the left side.
-   Calls \> 1000ms: The total number of successful or failed API calls whose RT is greater than 1,000 ms per hour is displayed in a yellow bar chart. The data corresponds to the y-axis on the left side.

## Slow Responses

**Note:** Slow responses refer to the API calls that consume more than 1,000 ms.

In the API Request Statistics section, click **Slow Responses** to view the number of slow responses.

![slow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0071378061/p177859.png)

Slow Responses: The number of slow responses in the selected application within a specified period of time is displayed in a bar chart. The data corresponds to the y-axis on the left side.

## Error Number

In the API Request Statistics section, click **Error Number** to view the number of failed API calls.

![error](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0071378061/p177880.png)

Error Number: The number of failed API calls in the selected application within a specified period of time is displayed in a bar chart. The data corresponds to the y-axis on the left side.

## API Requests

Click **API Requests** in the section marked as ③ to view the information about the calls of each API within a specified period of time.

![API ask](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0071378061/p177860.png)

-   Click the ![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over the display name of an API in the **API** column. Click the ![edit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3313758061/p177320.png) icon to modify the display name. APIs are displayed by display name. Click **Set To Search Value** to set the API as a filter.
-   Click a number in the **Error Number** column to view the details and distribution of failed API calls within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of failed API calls. Click **View Session** to view the session trace of failed API calls.

    ![error details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1071378061/p111587.png)

-   Click a number in the **Slow Responses** column to view the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.

    ![error details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1071378061/p111588.png)

-   Click **Analyze** in the **Operation** column to view the details of API calls, failed API calls, slow responses, and distribution.

    ![analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1071378061/p177862.png)

    -   On the API Details tab, you can view the success rate and details of API calls. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. You can also click **View Session** to view the session trace of the API.
    -   On the API Error Details tab, you can view the distribution of failed API calls and API call details.
    -   On the API Slow Loading Details tab, you can view the response time distribution and network request information.
    -   On the Distribution tab, you can view the return messages, HTTP status codes, pages, domain names, and geographical locations that are related to the API calls. You can also view the proportions of API calls by operating system, browser, device, or network connection type.

## Responses

Click **Responses** in the section marked as ③ to view the information about the responses of each API.

![reback](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8979878061/p177186.png)

-   Click the ![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over a response in the **Return Message** column. Click **Set To Search Value** to set the response as a filter.
-   Click a number in the **Slow Responses** column to view the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.

    ![Slow times](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8979878061/p177282.png)

-   Click **Analyze** in the **Operation** column to view the details of API calls, failed API calls, slow responses, and distribution.
    -   On the API Details tab, you can view the success rate and details of API calls. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. You can also click **View Session** to view the session trace of the API.
    -   On the API Error Details tab, you can view the distribution of failed API calls and API call details.
    -   On the API Slow Loading Details tab, you can view the response time distribution and network request information.
    -   On the Distribution tab, you can view the return messages, HTTP status codes, pages, domain names, and geographical locations that are related to the API calls. You can also view the proportions of API calls by operating system, browser, device, or network connection type.

        ![distributed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9979878061/p177958.png)


## HTTP Status Code

Click **HTTP Status Code** in the section marked as ③ to view all HTTP status codes.

![HTTP](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0860978061/p177332.png)

-   Click the ![icon_up_down](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1654078061/p204946.png) icon to the right of a property in the first row of the list to sort the APIs.
-   Move the pointer over an HTTP status code in the **HTTP Status Code** column. Click **Set To Search Value** to set the HTTP status code as a filter.
-   Click a number in the **Slow Responses** column to view the details and distribution of slow responses within a specified period of time. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of slow responses. Click **View Session** to view the session trace of slow responses.

    ![Slow times](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8979878061/p177282.png)

-   Click **Analyze** in the **Operation** column to view the details of API calls, failed API calls, slow responses, and distribution.
    -   On the API Details tab, you can view the success rate and details of API calls. In the Request Details section, click **Show Invocation Trace** to view the call and business traces of the API. You can also click **View Session** to view the session trace of the API.
    -   On the API Error Details tab, you can view the distribution of failed API calls and API call details.
    -   On the API Slow Loading Details tab, you can view the response time distribution and network request information.
    -   On the Distribution tab, you can view the return messages, HTTP status codes, pages, domain names, and geographical locations that are related to the API calls. You can also view the proportions of API calls by operating system, browser, device, or network connection type.

## Distribution

Click **Distribution** in the section marked as ③. On this tab, you can view the return messages, HTTP status codes, pages, domain names, and geographical locations that are related to the API calls. You can also view the proportions of API calls by operating system, browser, device, or network connection type. Move the pointer over a value in the **Domain Name** or **Page** column. Click **Set To Search Value** to set the domain name or page as a filter.

**Note:**

-   Version numbers can be displayed only by operating system or browser.
-   The pie chart of operating systems, browsers, devices, or connection types displays only the dimensional distribution of the first five items. You can click the Toggle View icon in the upper-right corner of each section to view the proportion of all filters in this dimension.

![distributed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0860978061/p177360.png)

