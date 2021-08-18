# Check Property Validation Results

A property version must be validated before it can be deployed to staging and/or production environments. CDN360 sends the compiled property and associated certificate(s) to a validation environment and performs basic tests, such as making sure the server does not crash and running artificial traffic to the hostnames associated with the property. The validation process usually takes less than a minute. For more information, see the [CDN360 API](</apidocs#tag/Property-Validation>). 

You can check the status of all property validations using the Tasks.

1. In the left pane, click **Tasks** > **Validation**.

<p align="center"><img src="/docs/resources/images/tasks/tasks-validation.png" alt="Validation Tasks" width="900"></p>
 
2. To filter results by time range, click the icon circled in the figure below and specify a start date and end date for your search.

**Note:** You can also use the **Search** box at the top to filter the results. Filtering is not case-sensitive.

<p align="center"><img src="/docs/resources/images/tasks/validation_time_range_filter.png" alt="Validation Tasks" width="900"></p>

3. To display details about a validation result, click an ID or task name.


