
# Editing Secrets

1. In the left pane, click **Edge Configurations**, and then select **Secrets**.

2. On the Secrets page, click the ID of the secret you want to edit, and then click the **Change Secret** button. 
   <br><U>OR </u></br>
  In the **Actions** column, click the vertical ellipsis for the secret you want to edit, and then select **Edit**.

<p align="center"><img src="/docs/resources/images/secrets/edit-secrets.png" alt="Edit secrets" width="700"></p>

3. Make your changes in the Update Secret form. Required fields are denoted by an asterisk (\*) and described in [Creating a Secret](</docs/portal/secrets/creating-secrets.md>).

**Note:** If you change the secret name, property versions that refer to that secret will fail [validation](</docs/portal/tasks/validations.md>) and will have to be updated. However, if a property that was using the secret has already been deployed to staging or production, the property is not affected by the name change.

4. Click the **Update** button.