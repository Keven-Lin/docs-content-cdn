# Using Properties to Configure the Edge

A "property" is a configuration of one or more hostnames (domains) that need to be deployed to the CDN360 edge servers. A property determines how you want the servers to obtain, cache, modify, and distribute your content to end users. The key elements of a property include:
- Service hostname(s) to be accelerated
- One or more origin servers
- Caching rules for different types of contents
- Modifications to the URL or HTTP header fields
- Whether HTTPS is required, TLS certificates, and TLS protocol version

## Managing Properties

On the CDN360 platform, each property is versioned to track the history of changes and allow rollback if needed. Each version can be deployed independently to the staging or production environment. 

Using the Properties page, you can create, modify, validate, and deploy properties. You can also undeploy and delete properties if needed. To display the Properties page, click **Edge Configurations** in the left pane, and then select **Properties**. The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/edge-configurations/properties-w-numbers.png" alt="properties page" width="900"></p>


| **Fields**   | **Description**                                                                           |
| :----------: | ----------------------------------------------------------------------------------------- |
| 1            | A search box that you can enter any keyword to filter the property list.                  |
| 2            | The list of all properties that are available to you.  |
| 3            | Icons to filter properties by Staging Version and Production Version.                            |
| 4            | Drop-down lists to take actions on each property.       |
| 5            | The button to [create new properties](</docs/portal/edge-configurations/creating-property.md>).    |

## Property Actions
Each property has a vertical ellipsis in the **Actions** column. Clicking the ellipsis shows the available actions that can be performed on the selected property.
- **Edit**: [Update](</docs/portal/edge-configurations/editing-properties.md>) the selected property.
- **Compare Versions**: [Compare](</docs/portal/edge-configurations/comparing-properties.md>) two property versions.
- **Undeploy from Staging**: [Undeploy](</docs/portal/edge-configurations/deploying-property.md>) the selected property from the staging environment.
- **Undeploy from Production**: [Undeploy](</docs/portal/edge-configurations/deploying-property.md>) the selected property from production.
- **Delete**: [Delete](</docs/portal/edge-configurations/deleting-property.md>) the selected property.
- **Deployment History**: [View](</docs/portal/edge-configurations/deploying-property.md>) the deployment history of the selected property.
- **Clone**: [Copy](</docs/portal/edge-configurations/creating-property.md>) settings into the Create a Property form to create a new property.
- **Report**: [Run](</docs/portal/reports.md>) a report using the hostnames of the deployed property. This action is available only for properties that have been deployed to production.

