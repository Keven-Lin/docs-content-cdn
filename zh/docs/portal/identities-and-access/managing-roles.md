# Managing Roles

A role is a collection of one or more permissions that can be performed within the portal. 

## Adding a Role

Administrators add roles from the **Roles** tab on the Identity & Access Management page. As part of this procedure, administrators assign roles to users, which define the activities that users can perform in the portal.

1. At the top right of the portal, click your initials, and then select **Identity & Access Management**.

    <p align=center><img src="/docs/resources/images/identities-and-access/iam-user-info.png" alt="select identity management page" width="400"></p>

2. At the top of the page, click **Roles**. 
3. At the right side of the page, click the **+ Add Role** button.

![null](</docs/resources/images/identities-and-access/iam-roles.png>)

4. Complete the fields in the Add Role form. Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/identities-and-access/iam-add-role.png>)

| **Fields**           | **Description**                   |
| -------------------- |---------------------------------- |
| Role Name            | Enter a name for this role.       |
| Description          | Enter a description for this role.|
| Permissions          | To assign one or more permissions to this role, click **+ Add Permissions**, check one or more permissions in the Add Permissions dialog box, and then click **Save**. If you decide not to add one or more permissions to this role, check them, and then click the **Delete** button in the **Permissions** section.|
| Users                | To assign users to this role, click **+ Assign Users**, check one or more users in the Assign Users dialog box, and then click **Assign**. If you decide not to add one or more users to this role, check them, and then click the **Delete** button in the **Users** section.               |

5. Click **Save**.


## Editing a Role

Administrators edit roles from the **Roles** tab on the Identity & Access Management page.

1. At the top right of the portal, click your initials, and then select **Identity & Access Management**.

    <p align=center><img src="/docs/resources/images/identities-and-access/iam-user-info.png" alt="select identity management page" width="400"></p>

2. At the top of the page, click **Roles**.

3. From the Roles page, click the name of the role you want to edit, and then click **Edit** at the top right of the Role Details page. 
   <br><U>OR </u></br>
   In the **Actions** column, click the vertical ellipsis for the role you want to edit, and then select **Edit**.

4. At the top right, click the **Edit** button.
5. Make your changes in the Edit Role form (for assistance, see the table above). Required fields are denoted by an asterisk (\*).

6. Click **Save**.

## Deleting a Role

Administrators delete roles from the **Roles** tab on the Identity & Access Management page.

1. At the top right of the portal, click your initials, and then select **Identity & Access Management**.

    <p align=center><img src="/docs/resources/images/identities-and-access/iam-user-info.png" alt="select identity management page" width="400"></p>

2. At the top of the page, click **Roles**.

3. Delete one or more roles:<br>

<ul><ul><li>To delete one role from the Roles page, click a role's vertical ellipsis in the <strong>Actions</strong> column, and then select <strong>Delete</strong>.</ul><br>

<ul><u>OR</u></ul></ul>

<ul><ul><li>To delete more than one role from the Roles page, check each role, and then click <strong>Delete</strong> at the top right of the page.</ul><br>

<ul><u>OR</u></ul></ul>

<ul><ul><li>To see the details of a role before deleting it, click the role name. To delete the role, click <strong>Delete</strong> at the top right of the Role Details page.</ul></ul>

4. If the role has no assigned users, click **Yes, delete!** to delete the role. If the role has one or more assigned users, click **Un-assign from all users and delete** to delete the role.

## Permissions That Can Be Assigned to Roles

| **This Permission...**                         | Allows the Role to...|
| ---------------------------------------------- | ---------------------- |
| certificate.create                             | Create certificates    |
| certificate.delete                             | Delete certificates    |
| certificate.deployment.production              | Deploy certificates to production environment |
| certificate.deployment.staging                 | Deploy certificates to staging environment    |
| certificate.download.csr                       | Download CSRs          |
| certificate.read                               | Read certificates      |
| certificate.update                             | Update certificates    |
| dashboard.read                                 | Read the dashboard     |
| edgeHostnames.create                           | Create  edge hostnames |
| edgeHostnames.delete                           | Delete  edge hostnames |
| edgeHostnames.read                             | Read  edge hostnames   |
| edgeHostnames.update                           | Update  edge hostnames |
| notification.create                            | Create notifications   |
| notification.delete                            | Delete notifications   |
| notification.read                              | Read notifications     |
| property.create                                | Create properties      |
| property.delete                                | Delete properties      |
| property.deployment.production                 | Deploy properties to production environment   |
| property.deployment.read                       | Read property deployments |
| property.deployment.staging                    | Deploy properties to staging environment      |
| property.read                                  | Read properties        |
| property.update                                | Update properties      |
| property.validation                            | Validate properties    |
| property.validation.read                       | Read property validations  |
| purge.create                                   | Create purge requests  |
| purge.read                                     | Read purge requests    |
| report.read                                    | Read reports           |
| role.create                                    | Create roles           |
| role.delete                                    | Delete roles           |
| role.read                                      | Read roles             |
| role.update                                    | Update roles           |
| user.create                                    | Create users           |
| user.delete                                    | Delete users           |
| user.read                                      | Read users             |
| user.suspend                                   | Suspend users or reactivate suspended users  |
| user.update                                    | Update users           |

