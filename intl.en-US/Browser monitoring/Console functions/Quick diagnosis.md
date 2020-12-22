# Quick diagnosis

A diagnostic report summarizes the data collected by browser monitoring during a past period of time. Such a report analyzes and displays the website performance based on JS error logs, the success rate of API requests, and the page speed. This helps you understand the key monitoring metrics for websites and troubleshoot the issues.

## Enter the page for the feature

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application that you want to view.

3.  In the upper-right corner of the page, click **One-click diagnosis**.

4.  On the **Diagnostic Report** page, view the diagnostic report.


## JS error logs

JS Error Logs uses the number of JS errors as a metric, and collects information about the error page views \(PVs\), exception PVs, and normal PVs. This feature displays the diagnostic result of each page, including the number of error PVs, the JS error rate, and the number of new error PVs. The following formula is used to calculate the JS error rate: JS error rate = Number of error PVs/Total number of PVs.

![dg_JS error logs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3543468061/p201745.png)

## Success rate of API requests

API Success Rate uses the number of API requests as a metric, and counts the failed, abnormal, and successful API requests. This feature displays the diagnostic result of each API. For example, the result may indicate that the success rate of requests on an API is low or the success rate encounters an abrupt decrease. The result also contains the average and lowest success rates of API requests. The following formula is used: Success rate of API requests = Number of successful API requests/Total number of API requests.

![dg_Success rate of API requests](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3543468061/p201796.png)

## Page speed

Page Speed provides the PV information of each page, including the numbers of failed, exception, and successful PVs. This feature calculates the page speed based on the PV information, and provides the diagnostic result. The information about the first paint time \(FTP\) of PVs is displayed, including the PVs that have a long FTP. The result also displays the average FTP, maximum FTP, and the time point when the maximum FTP occurs. The following formula is used: FTP = responseEnd - fetchStart.

![dg_Page speed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3543468061/p201797.png)

