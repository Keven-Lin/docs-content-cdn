# Manage Traffic with Edge Hostnames

When a content delivery network is not used, your service hostname should always resolve to the IP address of the server hosting the service. <p>To start acceleration with CDN360, end user traffic must be directed to the CDN360 edge servers. This can be done by creating a CNAME record with your DNS service provider that points the end user service hostname to a CDN360 "edge hostname" you create. You can maintain multiple edge hostnames in your account for different traffic management requirements. Each edge hostname can be configured with sophisticated policies to handle end user requests based on their geographic location and ISP. These policies also allow you to control the trade-off between service performance and cost.

In the left pane, click **Traffic Management** to see a page with a list of the edge hostnames in your account. The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/traffic-management/traffic-management-w-numbers.png" alt="edge hostname overview"></p>

| **Fields**   | **Description**                                                                        |
| :----------: | ---------------------------------------------------------------------------------------|
| 1            | A search box that you can enter any keyword to filter the edge hostname list.          |
| 2            | The list of all edge hostnames in your account.                                        |
| 3            | The icon to filter edge hostnames by Has Bien.                                         |
| 4            | Drop-down lists to take actions on each edge hostname.                                 |
| 5            | The button to [create a new edge hostname](</docs/portal/traffic-management/creating-edge-hostname.md>).    |

## Edge Hostname Actions
Each edge hostname has a vertical ellipsis in the **Actions** column. Clicking the ellipsis shows the available actions that can be performed on the selected edge hostname.
- **Edit**: [Update](</docs/portal/traffic-management/editing-edge-hostname.md>) the selected edge hostname.
- **Delete**: [Delete](</docs/portal/traffic-management/deleting-edge-hostname.md>) the selected edge hostname.
- **Clone**: [Copy](</docs/portal/traffic-management/creating-edge-hostname.md>) settings into the Create an Edge Hostname form to create a new edge hostname.
- **Report**: [Display](</docs/portal/reports.md>) the Reports page to run an Edge Hostname Request report on the selected edge hostname.
