# Reports

CDN360 provides reporting capabilities that allow you to analyze the traffic to your properties, identify trends over time, and pinpoint times when visitors are most likely to land on your site.

Reports are generated from the Reports page. To display this page, click **Reports** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/reports-w-numbers.png" alt="report page" width="900"></p>

| **Fields**   | **Description**                                                                                           |
| :----------: | --------------------------------------------------------------------------------------------------------- |
| 1            | Specify the report type, date range, and other parameters appropriate for the report you want to generate.               |
| 2            | The **Generate Report** button allows you to generate the report defined by the report parameters.        |

## Supported Report Types

The following report types are supported:

| **Report**            | **Description**                                                   |
| --------------------- | ----------------------------------------------------------------- |
| Traffic Volume        | Reports edge versus origin traffic.                                 |
| Traffic Bandwidth     | Reports edge versus origin traffic bandwidth. Lines represent edge traffic from CDN360 servers, traffic from your origin servers, and cache hit rate. The vertical (Y) axis shows the bandwidth and hit ratio, while the horizontal (X) axis shows time. The cache hit rate is computed as (edge traffic - origin traffic) / edge traffic.     |
| Requests              | Reports requests made to the files of your property. Lines show the requests to CDN360 edge servers, requests to your origin servers, and cache hit rate. The cache hit rate is computed as (edge requests - origin requests)/edge requests.              |
| Status Code Details   | Reports the percentage of HTTP status codes returned. For example, code 200 represents a successful request. |
| Origin Status Code Details   | Reports the percentage of HTTP status codes returned in requests to your origin servers. For example, code 200 represents a successful request. |
| Fast Route Traffic Volume   | Reports the traffic to your origin server that use CDNetworks' <a href="/cdn/docs/edge-logic/supported-directives#origin_fast_route">fast route feature</a> to make connections faster and more reliable. |
| Fast Route Requests   | Reports the number of requests to your origin server that uses CDNetworks' <a href="/cdn/docs/edge-logic/supported-directives#origin_fast_route">fast route feature</a> to make connections faster and more reliable. |
| Traffic Volume Summary| Summarizes the edge traffic volume.                               |
| CPU Time| Reports the CPU time consumed in each time interval to serve your properties. You can toggle the unit between **seconds** and **number of cores**. For example, if 3000 seconds of CPU time are reported in a 5-minute interval, it means your properties are maxing out an average of 10 (=3000s/5m) physical CPU cores during that period.                               |
| Edge Hostname Request| Shows the number of requests made to your [edge hostnames](</docs/portal/traffic-management/creating-edge-hostname.md>) over a period of time.                               |
| Access Log Download| Shows what content has been requested and when it was requested, the IP address from which requests were made, the value of the User-Agent HTTP request header, and the size of the content requested.                    |

## Generating Reports

1. In the left pane, click **Reports**. 
2. Complete the fields in the Reports page:

<p align=center><img src="/docs/resources/images/reports-wo-numbers.png" alt="report page" width="900"></p>

| **Fields**      | **Description**                                       |
| --------------- | ----------------------------------------------------- |
| Report Type     | Select the type of report you want to generate.       | 
| Date Range      | Select the start and end dates and the time for the report. |
| Hostname | For Access Log Download reports, select a property hostname. Logs of visitors to the hostname will be generated for you to view and download.
| Report Interval | For all reports except Traffic Volume Summary, select the granularity of the returned data. <li><strong>5 minutes</strong>. *(default)*</li><li><strong>1 Hour</strong>.</li><li><strong>1 Day</strong>.</li><li><strong>1 Month.</li></li>
| Hostnames       | For all reports except Edge Hostname Request, select one or more hostnames defined in your properties.         |
| Edge Hostnames  | For Edge Hostname Request, select one or more edge hostnames.         |
| Scheme        | For all reports except Edge Hostname Request, select the protocol-based data traffic that will be reported. <li><strong>All</strong> = report  HTTP and HTTPS traffic. *(default)*<li><strong>HTTP</strong> = report HTTP traffic only.<br><li><strong>HTTPS</strong> = report HTTPS traffic only.         | 
| Report Range        | If you are a reseller with child accounts, select the account that this report will cover. <li><strong>This Account Only</strong>. *(default)*</li><li><strong>Children Accounts Only</strong>.</li><li><strong>This Account + Children</strong>.
| Server Groups        | By default Traffic Volume Summary reports on all server groups. To choose specific server groups, select them from the available choices.<li><strong>Standard</strong></li><li><strong>Premium</strong>.</li><li><strong>Premium+</strong>.</li><li><strong>Ultra</strong>.|
| Report Range        | If you are a reseller with child accounts, select the account that this report will cover. <li><strong>This Account Only</strong>. *(default)*</li><li><strong>Children Accounts Only</strong>.</li><li><strong>This Account + Children</strong>.|
| Group By       | If **Report Type** is set to **Traffic Volume Summary**, use this field to group the results according to one or more of the following choices. <li><strong>None</strong>.</li><li><strong>Hostnames</strong>.</li><li><strong>Server Groups</strong>.</li><li><strong>Customer Ids</strong>.</li> |

**Note:** All volume and bandwidth report data pertains to the HTTP payload only. It does not include the overhead from TCP, IP, and MAC headers. CDNetworks adds 4.56% (66 bytes) of overhead to each 1448-byte payload to generate the "billing volume" on your invoice.

3. Click the **Generate Report** button to generate the report.
4. After the report is generated, you can:

<ul><li>Mouse over data points in the report to view detailed information.<br>
<li>Drag over the chart to magnify areas, and then use the <strong>Reset zoom</strong> button to return to the default zoom level.<br>
<li>Use the <strong>Download Options</strong> button at the top right of the report to download raw data in comma-separated-value (CSV) format.
