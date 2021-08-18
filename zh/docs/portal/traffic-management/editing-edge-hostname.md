# Editing an Edge Hostname

1. In the left pane, click **Traffic Management**.
2. Click the edge hostname you want to edit. 
    <br><U>OR </u></br>
  In the **Actions** column, click the vertical ellipsis for the edge hostname you want to edit, and then select **Edit**.
3. At the top right of the page, click the **Edit** button.

The Edge Hostname form appears for creating, editing, and deleting client zone rules and changing advanced settings. For more information, refer to the topics below.
<p align=center><img src="/docs/resources/images/traffic-management/traffic-management-edit-edge-hostname.png" alt="edit cname form"></p>

4. To create one or more client zone rules, perform the following steps.

<ul>a. At the top right of the page, click the <strong>Create Client Zone Rule</strong> button.</ul>
<ul>b. Complete all the fields, and then click the <strong>Create Client Zone Rule</strong> button.</ul>
<ul>c. To add more client zone rules, repeat this step for each additional rule.</ul>

<p align=center><img src="/docs/resources/images/traffic-management/create-client-zone-rule.png" alt="create client region rule"></p>

| **Fields**        | **Description**   |
| ----------------- | ----------------- |
| Client Region     | Select a region that defines this client zone. We currently support country-level granularity.|
| Client ISP        | Select one or more ISPs that define this client zone. |
| Action Type       | Select the type of action to be performed to requests from this client zone. <br><ul><li><strong>Deliver</strong> = contents will be served by CDN360 servers to fulfill the requests from this client zone. Only one delivery action is allowed for each client zone. You need to select the server groups to deliver the contents. </li><li><strong>Redirect</strong> = redirect client requests to another destination specified in the Redirect Target field (see below). This can be your origin site or maybe another CDN provider. There can be multiple redirect actions for each client zone.</li><li><strong>Reject</strong> = client requests will always receive a response with a 403 - forbidden error message. Only one reject action is allowed for each client zone.</li></ul>  
| Server Group      | If <strong>Action Type</strong> is set to <strong>Deliver</strong>, select one or more server groups to handle the traffic for this edge hostname. CDN360 servers are organized into 4 groups based on the traffic cost from low to high: <strong>Standard</strong>, <strong>Premium</strong>, <strong>Premium+</strong> and <strong>Ultra</strong>. When you select one group, all the lower groups will be included automatically. |
| Enable IPv6      | If <strong>Action Type</strong> is set to <strong>Deliver</strong>, select whether you want to enable IPv6 addressing.|
| Redirect Target   | If <strong>Action Type</strong> is set to <strong>Redirect</strong>, specify an IP address or hostname to which CDN360 will redirect your traffic. |
| Weight | When a client zone has multiple rules defined, each of them will be used randomly with a probability proportional to the weight specified here. |

5. To edit an existing client zone rule:

<ul>a. Click the <strong>Actions</strong> drop-down list next to the rule you want to edit, and then select <strong>Edit</strong>.</ul>
<ul>b. Make your changes in the Update Client Zone Rule dialog box (for assistance, see the table above).</ul>
<ul>c. Click the <strong>Update Client Zone Rule</strong> button.</ul>

6. To delete a client zone rule:

<ul>a. Click the <strong>Actions</strong> drop-down list next to the rule you want to delete, and then select <strong>Delete</strong>.</ul>

<p align=center><img src="/docs/resources/images/traffic-management/edge-hostname-delete-zone-rule.png" alt="zone rule delete"></p>

<ul>b. When prompted to confirm the deletion, click <strong>OK</strong> to delete the client zone rule.</ul>

**Note**: A default rule that covers all regions and all ISPs is always required. If you accidentally delete the default rule, the system will create one automatically.

7. To change the ICP Beian setting, expand **Advanced Settings** and make your change.

<p align=center><img src="/docs/resources/images/traffic-management/edge-hostname-advanced-settings.png" alt="edge hostname advanced settings" width="700"></p>

| **Fields**      | **Description**                                              |
| --------------- | ------------------------------------------------------------ |
| Has ICP Beian   |   This setting determines whether end user requests will be directed to and served by PoPs inside mainland China. <br><ul><li><strong>No</strong> = this edge hostname will be used by a service hostname that does not have ICP Beian. It will not resolve to any server IP address in mainland China. Only server IP addresses outside China will be returned. (*default*) <li><strong>Yes</strong> = all service hostnames using this edge hostname have ICP Beian. Visitors in mainland China can be served by local servers in China.</li></br></ul>|  

8. Click **Update**.
9. When a message confirms that the edge hostname was updated, click **OK**.
10.  Click **Close** to return to the main page.

