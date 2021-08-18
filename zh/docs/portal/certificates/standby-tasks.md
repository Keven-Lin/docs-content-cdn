# Managing Standby Actions

When you deploy and undeploy certificates and properties, you can perform  the action immediately or move it to a standby queue, where it will join other standby actions waiting to be run.

Using the Standby Task page, you can view all standby actions in the queue and run them all at one time.

## Displaying the Standby Task Page
You can display the Standby Task form from the Certificates, Edge Configurations, and Deployment pages.

### Displaying the Standby Task Form from the Certificate or Edge Configurations Page

1. In the left pane, click **Certificate** or **Edge Configurations**.
2. Click a certificate name or property ID.
3. At the bottom-right of the form, click the **Deployment History** button.
4. At the top-right of the Deployment form, click the **Standby Task** button.<p>

### Displaying the Standby Task Form from the Deployment Page

1. In the left pane, click **Tasks > Deployment**.
2. At the top right, click the **Standby Task** button.

## Understanding the Standby Task Form

The Standby Task form is organized into two subqueues.<ul><li>The top subqueue shows actions for the CDN360 staging environment.</ul></li><ul><li>The bottom subqueue shows actions for the production environment.</ul></li>Each subqueue has its own search field for filtering standby actions in that subqueue.

<p align=center><img src="/docs/resources/images/standby_tasks.png" alt="create new cert button menu" width="900"></p>

## Adding Standby Tasks
To add standby tasks to a subqueue:
1. Click the **+ Add** button at the top right of a subqueue. The Add Tasks to Staging dialog box appears.

<p align=center><img src="/docs/resources/images/adding_tasks_to_staging.png" alt="create new cert button menu" width="900"></p>

2. Under **Action**, select an action from the drop-down list.
3. Click **Add new +** and then enter the first few characters in the name of the certificate or property you want to add. When the entire name appears, click it.
4. If deploying a certificate or property, select a version number from the **Version** drop-down list. (This list does not appear when undeploying a certificate or property.)
5. To add more tasks to this action, repeat steps 3 and 4.
6. When you finish adding tasks, click **Add**.

## Deleting Standby Actions
To remove an individual standby action from a subqueue, click the trash icon on the far right side of the action. To remove all standby actions in a subqueue, click the trash icon next to **Version** in the header row.
**Note:** A precautionary message does not appear before you delete standby actions. Therefore, make sure you do not need a standby action before you delete it.
## Running Standby Actions
To run all of the actions under **Destination: Staging** or **Destination: Production**, click the **Run** button for that subqueue. 
**Note:** Running the actions in one subqueue does not run the actions in the other subqueue.
##Exiting the Standby Task Page
At the top-right of the form, click the **< Back** button to exit the Standby Task form.