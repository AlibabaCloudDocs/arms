# Real-time IoV monitoring solution

In this scenario, a solution provider in the Internet of Vehicles \(IoV\) industry from Shanghai adopted a solution based on Application Real-Time Monitoring Service \(ARMS\). This solution is used to collect statistics about online conditions of vehicles.

-   Multidimensional statistics on raw data cannot be implemented based on databases because a large volume of data is involved \(approximately 100,000 vehicle data records per second\).

## ARMS-based IoV monitoring solution

The following figure shows the overall architecture.

![sys_monitor](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2360537751/p43443.png)

-   The platform of the solution provider uploads real-time data of new-energy vehicles to Alibaba Cloud by using Message Queue \(MQ\).
-   The application monitoring feature of ARMS works with MQ to obtain the online data of all vehicles and perform real-time statistics and storage.
    -   Computing orchestration and storage: ARMS provides real-time statistics of the online rate and failure rate based on the reported vehicle information in multiple dimensions, such as the region, vehicle type, and enterprise. ARMS also stores the statistical results in columns by custom aggregation.
    -   Data delivery: ARMS delivers data to downstream applications after the applications call the corresponding API operations.
-   Downstream applications of Enterprise Distributed Application Service \(EDAS\) call API operations to retrieve data from ARMS. The retrieved data is then analyzed and displayed on the user applications.

## Business value of the IoV monitoring solution

-   The monitoring solution allows you to grasp real-time status of vehicles. The solution collects statistics on fault data in real time and reports statistical results based on different vehicle types. This improves the efficiency of quality enhancement.
-   The monitoring solution monitors the status of new-energy vehicles to detect illegal behavior such as subsidy cheating at the earliest opportunity.

## Example

The following figure shows a monitoring report.

![datav_monitor_arms](../images/p43444.png)

