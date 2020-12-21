# Monitoring scenario of user experience

This topic describes the scenario where user experience is monitored.

When you access Application Real-Time Monitoring Service \(ARMS\), the whole process can be divided into three phases: page production phase \(server status\), page loading phase, and page running phase. To ensure stable online services, the server monitors the status of these services. The existing server monitoring system is quite mature, but the monitoring of the page load and run statuses is still unsatisfactory. This is because less emphasis is placed on browser monitoring. Monitoring on the server is mistakenly regarded as a replacement of browser monitoring. As a result, the details of users who access the system cannot be perceived. Therefore, frontend issues encountered by users are difficult to locate.

## Challenges

-   Difficulty in locating performance bottlenecks

    When the loading speed of a page is slow, the performance bottleneck is difficult to identify. Is the slow page loading speed caused by network issues, resource loading issues, or page Document Object Model \(DOM\) parsing issues? Are the issues related to the province and country where the user resides, or the user's browser and device? These issues cannot be reproduced and the causes cannot be identified.

-   Failure to obtain the details of failed user access requests

    If a large number of JavaScript \(JS\) errors occur after a system goes online, users cannot use the system as expected. If you cannot obtain the error details at the earliest opportunity, you may lose a large number of users. When a user gives feedback on page usage, you cannot immediately reproduce the scenario of the user. Even if you obtain an error message from a user, you cannot quickly fix the error. These are difficulties that you may encounter.

-   Failure to obtain the details of asynchronous API calls

    Even if the HTTP status code 200 is returned from an API call, the API may be abnormal. If a business logic exception occurs, can the exception be perceived at the earliest opportunity? If normal responses are returned for all API calls, but the whole process consumes a long time, how can we get the whole picture and reduce the response time? Before you cannot answer these questions, you cannot identify the issues or improve user experience.


## ARMS-based browser monitoring solution

Based on large volumes of real-time log analysis and processing provided by ARMS, the browser monitoring feature monitors the access requests from all real online users and resolves the preceding issues.

-   Check the application overview page to identify exceptions

    You can view the information on the application overview page of the browser monitoring feature. The information includes application satisfaction rate, JS error rate, page speed, API success rate, and page view \(PV\) details. In the following figure, the average JS error rate is 6.68%. The average JS error rate increases 15.56% over the last week.

    ![Browser monitoring overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5360537751/p43320.png)

-   Performance data trend and waterfall chart

    On the Page Speed page, you can view specific metrics related to the page performance and the waterfall chart of page loading. You can then locate the performance bottleneck based on the detailed data.

    ![Performance data trend and waterfall chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5360537751/p43380.png)

-   JS error rate and error aggregation

    On the JS Error Rate page, you can view a ranking on page error rate and a ranking on frequent errors. Therefore, you can get a straightforward impression about which pages have the highest JS error rate, and which errors are the most frequent.

    ![JS error rate and error aggregation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6360537751/p43382.png)

-   API request

    On the API Request page, you can view the success rate and response time of API requests. This allows you to obtain the details of API requests.

    ![API request](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6360537751/p43383.png)

-   Access details

    On the **View Details** page, you can view the details of access requests. For example, you can locate an error based on the error information of stacks, files, lines, and columns.

    ![View details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6360537751/p43385.png)


