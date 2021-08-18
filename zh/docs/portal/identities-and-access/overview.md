# About Identities and Access

The Identity & Access Management page defines the users allowed to access the portal and the permissions to view and configure portal settings.


## What are Users?

Anyone who can log in to and be authenticated by the CDN360 portal is a user.


## What are Permissions?

The ability for users to perform actions within the portal is governed by permissions. Each permission has an intuitive name that describes its purpose. For example, certificate.create allows certificates to be created. A user must be granted a permission to perform the corresponding action in the portal.


## What are Roles?

Rather than assigning individual permissions directly to every portal user, permissions are grouped into roles. A role is a collection of users who share the same permissions. When you add a role, you specify a name for the role, select the permissions associated with the role, and then select the users who will be granted those permissions.

Initially, the portal provides three default roles: Admin, Operator, and Viewer.

- Admin can view and make changes to all settings available in the portal.
- Operator can view and make changes to all portal settings, except users and roles.
- Viewer has read-only permission and cannot change any portal settings.

## Identity & Access Management Page

To display the Identity & Access Management page, click your initials (**EM** in the figure below) at the top right of the portal, and then select **Identity & Access Management**.

<p align=center><img src="/docs/resources/images/identities-and-access/iam-user-info.png" alt="select identity management page" width="400"></p>

The following figure shows the key elements on the page, and the table following the figure describes them.

<p align=center><img src="/docs/resources/images/identities-and-access/iam-w-numbers.png" alt="select identity management page" width="900"></p>


| **Fields** | **Description** |
| :----------: | --------------- |
| 1 | Identity and access management tasks are organized into the following tabs:<ul> <li>**Users** allows administrators to manage users. Operators and viewers are limited to seeing other portal users. This tab appears when you click **Identity & Access Management**. <li>**Roles** allows administrators to manage roles. Operators and viewers are limited to seeing roles.|
| 2 | To filter users on the **Users** tab or roles on the **Roles** tab, type characters in this box. All users or roles that do not contain the typed characters are hidden. Filtering is not case-sensitive. To remove the filter, click the **Reset** button.|
| 3 | Each user or role appears on a row within its respective tab.|
| 4 | Drop-down list to take actions on the appropriate item.|
| 5 | The **Users** tab has an **+ Add User** button that allows administrators to [create new users](</docs/portal/identities-and-access/managing-users.md>). Similarly, the **Roles** tab has an **+ Add Role** button that allows administrators to [create new roles](</docs/portal/identities-and-access/managing-roles.md>). These buttons do not appear for viewers.|

