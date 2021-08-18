# Overview of Secrets

Typically, a secret is a password that you share with CDNetworks in order for the CDN configuration to work. For example, a secret could be a key used to authenticate client requests to your origin server. By creating a secret and referring to it in your Edge Logic using the secret's name via the syntax `$SECRET(secretName)` the key itself would not be exposed when viewing a property through the CDN360 portal or fetching it using the CDN360 API.

## Secrets Page 

Secrets are managed from the Secrets page. To display this page, click **Edge Configurations** in the left pane, and then select **Secrets**. 

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align="center"><img src="/docs/resources/images/secrets/secrets-w-numbers.png" alt="Secret List" width="900"></p>

| **Fields**   | **Description**                                                                                           |
| :----------: | --------------------------------------------------------------------------------------------------------- |
| 1            | A search box that you can enter any keyword to filter the secret list.                               |
| 2            | The list of all secrets that have been created. Click an Id to [query](</docs/portal/secrets/querying-secrets.md>) a secret.  |
| 3            | Drop-down lists to take actions on each secret.                      |
| 4            | The button to [create new secrets](</docs/portal/secrets/creating-secrets.md>).            |



## Secret Actions
Each secret has a vertical ellipsis in the **Actions** column. Clicking the ellipsis shows the available actions that can be performed on the selected secret.
<p align="center"><img src="/docs/resources/images/secrets/secrets-actions.png" alt="Secret Actions" width="900"></p>
The actions are:

- **Edit**: [Update](</docs/portal/secrets/editing-secrets.md>) the selected secret.
- **Delete**: [Delete](</docs/portal/secrets/deleting-secrets.md>) the selected secret.
