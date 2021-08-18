# Creating an Edge Hostname 

An edge hostname in a CNAME record on your DNS system allows you to route end user requests. When you create an edge hostname, you define rules that determine how CDN360 handles requests from different **client zones**. A client zone is a combination of a geographical region and one or more ISPs (for example, "US+Comcast").

1. In the left pane, click **Traffic Management**.
2. At the top right of the screen, click the **Create Edge Hostname** button. 
3. Complete the fields in the Create an Edge Hostname form. Required fields are denoted by an asterisk (\*).

<p align=center><img src="/docs/resources/images/traffic-management/create-edge-hostname.png" alt="cname overview page"></p>


| **Fields**                               | **Description**                     |
| ---------------------------------------- | ----------------------------------- |
| Description | Enter a description for the edge hostname.  |
| Hostname       | Either enter the first part of the edge hostname manually in the text field or click the **Auto Generate** button to generate a random one. |

4. Click the **Create Client Zone Rule** button. The Create Client Zone Rule dialog box appears, with fields to define the client zone and how to handle requests come from it. Required fields are denoted by an asterisk (\*).

<ul>a. Complete all the fields, and then click the <strong>Create Client Zone Rule</strong> button.</ul>
<ul>b. To specify more client zone rules, repeat steps 4 and 4a for each additional rule.</ul>

**Note**: A default rule covering ALL regions and ALL ISPs will be created automatically if you don't define one.
<p align=center><img src="/docs/resources/images/traffic-management/create-client-zone-rule.png" alt="createclient region rule"></p>

| **Fields**        | **Description**                                                           |
| ----------------- | ------------------------------------------------------------------------- |
| Client Region     | Select a region that defines this client zone.|
| Client ISP        | Select one or more ISPs that define this client zone.|
| Action Type       | Select the type of action to be performed to requests from this client zone. <br><ul><li><strong>Deliver</strong> = contents will be served by CDN360 servers to fulfill the requests from this client zone. Only one delivery action is allowed for each client zone. You need to select the server groups to deliver the contents. </li><li><strong>Redirect</strong> = redirect client requests to another destination specified in the Redirect Target field (see below). This can be your origin site or another CDN provider. There can be multiple redirect actions for each client zone.</li><li><strong>Reject</strong> = client requests will always receive a response with a 403 - forbidden error message. Only one reject action is allowed for each client zone.</li></ul>  
| Server Group      | If <strong>Action Type</strong> is set to <strong>Deliver</strong>, select one or more server groups to deliver the content for this client zone. CDN360 servers are organized into 4 groups based on traffic cost from low to high: <strong>Standard</strong>, <strong>Premium</strong>, <strong>Premium+</strong>, and <strong>Ultra</strong>. When you select one group, all the lower groups will be automatically included. For more information, see [About Server Groups](#about-server-groups) below. To see the location of servers in each group, go to: https://www.cdnetworks.com/cdn360/.|
| Enable IPv6      | If <strong>Action Type</strong> is set to <strong>Deliver</strong>, select whether you want to enable IPv6 addressing.|
| Redirect Target   | If <strong>Action Type</strong> is set to <strong>Redirect</strong>, specify an IP address or hostname to which CDN360 will redirect your traffic. |
| Weight | When a client zone has multiple rules defined, each of them will be used randomly with a probability proportional to the weight specified here. |

5. Expand **Advanced Settings**, and then confirm or change the following field.

<p align=center><img src="/docs/resources/images/traffic-management/edge-hostname-advanced-settings.png" alt="advanced settings" width="700"></p>

| **Fields**      | **Description**                                              |
| --------------- | ------------------------------------------------------------ |
| Has ICP Beian   |   This setting determines whether end user requests will be directed to and served by PoPs inside mainland China. <br><ul><li><strong>No</strong> = this edge hostname will be used by a service hostname that does not have ICP Beian. It will not resolve to any server IP address in mainland China. Only server IP addresses outside China will be returned. (*default*) <li><strong>Yes</strong> = all service hostnames using this edge hostname have ICP Beian. Visitors in mainland China can be served by local servers in China.</li></br></ul>|

6. Click the **Create the Edge Hostname** button.
7. Add a CNAME record on your DNS server to point your service hostname(s) to the newly created edge hostname.
## About Server Groups
When selecting a server group for the first time, we recommend that you create client zone rules that use the **Standard** server group, and then change to another server group if needed later.

If you create a client zone rule and select **Premium**, **Premium+**, or **Ultra**, all the lower priced groups will be included automatically and can be used to deliver content. For example, if you live in North America and want the best possible performance for your users, regardless of cost, choose **Ultra**. <p>When a user requests your content, the CDN360 load balancer makes an intelligent routing decision based on the user's location and current network traffic, and then chooses an appropriate server to handle the request. The server that handles this request is located at any of the CDN360 PoPs around the world and might be one listed as **Standard**, **Premium**, **Premium+**, or **Ultra**. Traffic used by different server groups is reflected in the [Traffic Volume Summary report](</docs/portal/reports.md>) as well as in monthly invoices.
