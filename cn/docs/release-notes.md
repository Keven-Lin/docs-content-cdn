# Release Notes

## July 28, 2021
### API updates
* Fixed [portal user list API](</apidocs#operation/getContacts>)'s handling of the ids query parameter.
* Ensured an operator API account of a reseller can [create an API permission](</apidocs#operation/post-cdn-apiPermissions>) for an API account of their customer.
* Allowed a single task to deploy a new certificate version along with the property using it instead of requiring separate deployment tasks.
* Improved Edge Logic validation to ensure that nested location blocks have a content handler.
* Improved handling of customer deletion when the customer is still using resources.
* Improved validation of hostnames used in a property.
* Updated [deployment](</apidocs#operation/createDeployment>) to support the Check-Certificate header to bypass checking of expired certificates and hostnames missing from the certificate’s SAN. This may be useful in some circumstances for testing, though it should not normally be used in production, since browsers would discourage visitors from accessing your content.
* Improved certificate verification.
* Ensured that query strings of URLs that are purged are respected.

### Portal updates
* Improved report range date picker.
* Added tooltips for Direct Connection origin setting.
* Improved appearance of client zone rules table.
* Added initial Russian language support.
* Added visual cue when loading the list of certificates.
* Show waiting status when saving or validating a property.

## July 15, 2021

### API updates

* Improved validation of API calls made by resellers.
* Improved error handling of [secret management APIs](</apidocs#tag/Secret-Management>).
* Added support for “operation” report annotations that CDNetworks may use to identify operational changes. We expect these to be infrequent.
* Made API query parameters case-insensitive for ease of use.
* Fixed [annotation list](</apidocs#operation/queryAnnotationList>) to include recently updated annotations.
* Fixed [search for secret by its ID](</apidocs#operation/get-cdn-secrets>).

### Portal updates

* Updated the Content Management page so you can search for purge requests by selecting the time range when they were submitted.
* Required you to confirm if you try to delete a recently active hostname or edge hostname. This helps prevent accidental deletion of resources still used by visitors.
* Fixed highlighting of a menu when switching to the standby tasks page.
* Improved the cache settings dialog shown when creating a new property by clicking Wizard.


## June 30, 2021

### API updates

* Added [secret management](</apidocs#tag/Secret-Management>) APIs you can use to improve security by preventing sensitive text from being exposed in Edge Logic.
* Allowed you to show [report annotations](</apidocs#tag/Annotations-for-Reports>) for property deployments, certificate deployments, and edge hostname updates.
* Added “proxy_next_upstream off;” in NGINX configuration to avoid latency related to using the [real-time log feature](</docs/portal/edge-configurations/creating-property#real-time-log>).


### Portal updates

* Added reminder to use directory purge for files with multiple variations.
* Fixed display of IP addresses available for [testing deployments to staging](</docs/portal/edge-configurations/testing-property>).
* Added the "Secret Management" feature so you can hide sensitive text from being exposed in Edge Logic. To access, click “Secrets” under the “Edge Configurations” menu item.
* Improved the cache settings dialog shown when creating a new property by clicking Wizard.
* Improved the display of the property comparison page.
* Added a Video Seeking section to the Advanced Settings of property configurations allowing you to specify parameters related to video content.

## June 14, 2021

### API updates
* Updated a customer's [list of users](</apidocs#operation/getContacts>) to indicate whether the users have full access to all products.
* Ensured an error is returned if you try to create a property with duplicate hostnames.
* Updated [API calls](</apidocs#operation/get-ngadmin-apicalls>) to return data from the last 30 days by default.
* Reduced the latency associated with real-time log implementation.

### Portal updates
* Improved the standby task's interface.
* Improved the property edit page's appearance.
* Improved the property deployment user interface by linking to information about testing staging deployments.
* Added text explaining the ICP Beian setting.
* Improved the sidebar menu icons.
* Fixed the appearance of a long edge hostname in the reports page.
* Ensured the portal shows a property version is frozen once the property is deployed.

## June 4, 2021
### API updates

* Fixed prefetch quota enforcement.
* Added a check for traffic when you try to delete a hostname or edge hostname. This helps reduce accidental deletion of actively used hostnames and edge hostnames.
* Made /ngadmin API query parameters case-insensitive for ease of use.


### Portal updates

* Added a confirmation dialog when you cancel adding to the standby task list.
* Provided additional help in the portal for directory purge.

## May 21, 2021
### API updates

* Added support for $remote_user and $client_real_ip in loadBalancerHashKey.
* Added support for [webhooks](</apidocs#tag/Webhooks>) in asynchronous operations (validation, deployment, purge, prefetch) to notify you when the operations complete.
* Improved [property list API’s](</apidocs#operation/getPropertyList>) "hasConfig" filter to support searching fields.
* Added a check of traffic before deleting an edge hostname to avoid accidental deletion.

### Portal updates
* Added the origin status code report.

## May 5, 2021

### API updates
* Enhanced the property search to allow direct matches including prefacing with ‘^’ to match text at the beginning of fields.
* Fixed a problem with enabling the [HDT (High Speed Data Transmission)](<https://www.cdnetworks.com/high-speed-data-transmission/>) product for a reseller's customer.
* Fixed an error when deploying a property using a certificate without SANs.


### Portal updates

* Fixed an error that could occur while creating a certificate.
* Updated the customer list page to ensure it has at least 10 items per page.
* Ensured that search and filter conditions for certificates are additive.
* Added support for cloning an existing property to create a new one.
* Added "View Report" in the "Actions" menu for properties and edge hostnames.
* Added support for the [CALC_INT and ABS_INT functions](</docs/edge-logic/supported-directives#eval_func>) in Edge Logic.

## April 21, 2021

### API updates
* Added the [requests summary report](</apidocs#operation/post-cdn-report-reqSummary>) to summarize requests to the CDN360 edge servers.
* Ensured the ‘latestVersion’ field is returned when [getting a property’s details](</apidocs#operation/queryProperty>).
* Fixed responses for the [customer list API](</apidocs#operation/get-ngadmin-customers>) when filtering using the regionalOffice parameter.
* Improved management of purge quotas.
* Improved efficiency of [realtime_log_downsample](</docs/edge-logic/supported-directives#realtime_log_downsample>).
* Trimmed real-time log format string.
* Extended [property list API](</apidocs#operation/getPropertyList>)'s hasConfig filter to allow searching subfields of property version.
* Added support for "children-only" Report-Range header in [API account list](</apidocs#operation/get-ngadmin-apiAccounts>) API for resellers.
* Added support for "children-only" Report-Range header in [portal user list](</apidocs#operation/getContacts>) API for resellers.
* Fixed the [property list API](</apidocs#operation/getPropertyList>) to avoid returning property if version matching a hasConfig filter was already deleted.
* Fixed an error in the [log download API](</apidocs#operation/getLogfiles>).

### Portal updates
* Prevented a purge task from being created until at least one file or directory has been specified.
* Improved the text in the standby task confirmation.
* Added the property version description to the dropdown list in the property configuration page.
* Added the portal user's name into descriptions by default when creating and updating properties and other resources.
* Fixed the display of disabled text on Safari browsers so that it is more visible.

## April 9, 2021
### API updates
* Added [prefetch APIs](</apidocs#operation/post-cdn-prefetches>) allowing you to warm up the cache in advance of visitor requests for your content.
* Fixed the [customer list API’s](</apidocs#operation/get-ngadmin-customers>) response to include products used by each customer.
* Allowed resellers to use the Report-Range header in [certificate list API](</apidocs#operation/getCertificates>).

### Portal updates
* Added support for disabling HTTP2.
* Improved validation by rejecting unsuitable certificates.
* Added soft wrap to the real-time log editor to improve usability.

## March 26, 2021
### API updates

* Added support for [custom API account permissions](</apidocs#tag/API-Account-Management>), giving you more control over who can access or update your configurations.
* Fixed the validation of contactLimit and apiAccountLimit when resellers create and update customers.
* Allowed resellers to use the Report-Range header in [deploymentTasks](</apidocs#operation/queryDeploymentTaskList>), [validations](</apidocs#operation/queryPropertyValidationList>), [edge hostnames](</apidocs#operation/getEdgeHostnames>), [hostnames](</apidocs#operation/listhostnames>), and [service quotas](</apidocs#operation/get-cdn-serviceQuotas>) APIs.
* Added support for overriding the sample rate of real-time log in CS.
* Added a check for Beian status when deploying a property to staging.
* Added tlsCertificateId in [property list API](</apidocs#operation/getPropertyList>).

### Portal updates
* Added support for a template to initialize self-signed (“auto-generated”) certificates.
* Improved the deployment user interface.
* Fixed dismissal of progress bar for property deployments that fail.
* Fixed search by report name.
* Allowed you to define a baseline configuration for initializing the Edge Logic of new properties you create.
* Allowed you to clone an edge hostname to make it easier to create a new one based on an existing one's settings.
* Updated the real-time log feature to allow the sample rate to be 0.

## March 12, 2021
### API updates
* Prevented resellers from deleting a suspended customer who still has access to a product like CDN360.
* Fixed an issue affecting generation of a Sectigo DCV file.
* Allowed resellers to use the Report-Range header in [property list API](</apidocs#operation/getPropertyList>).

### Portal updates
* Fixed the display of property and certificate name in standby task.
* Added support for variable auto-completion lists for the Edge Logic and real-time log editors, making them easier to use.

## February 22, 2021

### API updates
* Improved error handling of administration APIs.
* Added an API to [get a specific historical hostname](</apidocs#operation/get-cdn-hostnames-historical-hostname>), so you can check which hostnames were active in the past.
* Improved validation of maxClientSendTimeOut values in [service quota API's](</apidocs#operation/post-cdn-serviceQuotas>) ‘directiveParameterLimits’.
* Added support for "oldestPropertyValidationTime" in [systemConfigs](</apidocs#operation/get-cdn-systemConfigs>).

### Portal updates
* Improved the user interface for creating and updating certificates.
* Fixed the timezone in the deployment and validation list's time range selection interface.
* Reset the time if you clear the date range fields in validation, report, and deployment list pages.
* Allowed validation of a frozen property. This may be necessary due to cache version changes that obsolete previously validated properties.

## February 11, 2021

### API updates
* Improved an error message in [portal user creation API](</apidocs#operation/createContact>).
* Improved property validation.
* Fixed error handling when using invalid or unauthorized Edge Logic directives.
* Fixed enforcement of limits used in timeout related directives such as [client_send_timeout](</docs/edge-logic/supported-directives#client_send_timeout>).
* Fixed CDN serviceQuota's “advancedFeatures” setting.
* Added tracking of recent validation and deployment times of a property.

### Portal updates
* Updated user invitation emails to come from sender ‘CDN360 Admin’.
* Put search and filter parameters into the URLs of the list pages (i.e., property, edge hostname, certificate, purge) .
* Made the certificate creation user interface more consistent with property creation.
* Prevented certificates with the same name from being created.
* Fixed display of version when creating a new version of a certificate.
* Fixed display of certificate and property lists.
* Added a link to create a property to help new CDN360 users.
* Improved the appearance of the validation and deployment pages while they are loading.

## January 25, 2021
### API updates
* Improved validation of Edge Logic in properties.
* Fixed error handling when invalid or unauthorized directives are used in a property.
* Improved validation of timeout related settings in a service quota’s directiveParameterLimits.
* Updated [service quota creation](</apidocs#operation/post-cdn-serviceQuotas>) to support the advancedFeatures field.

### Portal updates
* Added search and filter parameters in URLs of property, edge hostname, certificate, and purge list pages to make them easier to bookmark.
* Improved certificate creation page.
* Prevented a timezone change from affecting impersonation by resellers.
* Prevented certificates of the same name from being created.
* Fixed display of certificate version number when creating a new certificate.
* Allowed manual input in the start and end date fields of the report page.

## January 8, 2021
### API updates
* Improved error message if you attempt to deploy a property with a hostname used by another customer.
* Improved logic to handle hostname conflicts that can occur if using wildcard domains.
* Fixed the default client zone rule for edge hostnames allowing use of all server groups instead of just ‘standard’ to maximize performance. You can create custom client zone rules to maximize performance and minimize costs.

### Portal updates
* Fixed a display issue in the Edge Logic edit field.
* Improved message that appears when a newly invited user tries to use an existing login name.
* Updated implementation of the standby task page.
* Improved the appearance of the upgrade button.
* Improved display of roles and other pages as they are being loaded.
* Added a search button in the validation and deployment pages' time range filter interfaces.
* Fixed the Edge Logic window’s autocomplete support for new directives.
* Added support for dragging to zoom in the CPU and edge hostname request reports.

## December 23, 2020
### API updates
* Improved error handling when creating or updating a portal user with an invalid login name.
* Added a limit on the number of API accounts.
* Removed deleted service quota from API’s results.
* Added a limit on the number of portal users.
* Added support for 6 new Edge Logic directives:
[origin_connect_timeout](</docs/edge-logic/supported-directives#origin_connect_timeout>), [origin_read_timeout](</docs/edge-logic/supported-directives#origin_read_timeout>), and [origin_send_timeout](</docs/edge-logic/supported-directives#origin_send_timeout>) for you to manage communications with your origin servers and  [client_header_timeout](</docs/edge-logic/supported-directives#client_header_timeout>), [client_body_timeout](</docs/edge-logic/supported-directives#client_body_timeout>), and [client_send_timeout](</docs/edge-logic/supported-directives#client_send_timeout>) for you to manage communications with the clients.
* Limited the [realtime_log_downsample](</docs/edge-logic/supported-directives#realtime_log_downsample>) directive to the server block of Edge Logic.
* We now require the isp field to be specified in a client zone rule when [creating an edge hostname](</apidocs#operation/createEdgeHostname>).


### Portal updates
* Added the edge hostname request report.
* Added the CPU time report.
* Enhanced the date picker in reports page.
* Added support for [HDT (High Speed Data Transmission)](<https://www.cdnetworks.com/high-speed-data-transmission/>) in the product selection menu allowing you to switch to the HDT portal.
* Fixed password expiration email’s appearance.
* Implemented notification message when a deployment is added to the standby task.
* Fixed text of standby task confirmation.
* Fixed validation and deployment popup windows’ button labels.
* Improved date range picker in validation and deployment task list pages.
* Fixed display of customers of resellers. 

## December 20, 2020
### API updates
* Removed apiAccountId from responses of API calls directly made by you.
* Limited an edge hostname’s client zone rule to a maximum of 10 ISPs.
* Added impersonatingParentCustomerId to identify the reseller (or parent) customer performing an action like purge, validation, or deployment on behalf of their customer.
* Removed redundant target field returned in the purge summary response.
* Improved [querying for API calls](</apidocs#operation/get-ngadmin-apicalls>) when using a path parameter with an asterisk character.
* Returned customerId field in [API calls](</apidocs#operation/get-ngadmin-apicalls-id>) and [portal users](</apidocs#operation/getContacts>) APIs.
* Returned an error if the user tries to deploy a certificate with an invalid certificate version.
* Added support for advancedFeauresList and directiveParameterLimits in CDN360 [service quota object](</apidocs#operation/post-cdn-serviceQuotas>). These manage access to advanced CDN360 features and specification of limits on some Edge Logic directives.

### Portal updates
* Improved error handling in the property creation and edit pages when an invalid edge hostname is specified.
* Improved the appearance of the verification code email sent to users who forget their passwords.
* Limited selection of ISPs in creation of client zone rule for an edge hostname.
* Improved text in progress popups.
* Cleared the standby task list after the task has been run.
* Fixed standby task field names.
* Fixed overlapping standby task and deploy buttons.

## December 7, 2020

### API updates
* Added support for non-standard HTTP and HTTPS ports by specifying them in a extraServicePorts field of a property configuration. Also return extraServicePorts in the [system configuration API](</apidocs#operation/get-cdn-systemConfigs>). Please contact us if you require a port that isn't yet allowed.
* Prevented deletion of a property whose deployment is still in progress.
* Supported querying validation history of a deleted property.
* Enhanced [property list API](</apidocs#operation/getPropertyList>) to support searching for a value that is not present in the configuration.
* Allowed resellers to use the Report-Range header in [API account list](</apidocs#operation/get-ngadmin-apiAccounts>).
* Updated [traffic volume summary report](</apidocs#operation/getVolSummary>) to support the protocol parameter.
* Modified property validation to allow the 'if' parameter in Edge Logic.

### Portal updates
* Modified order of deployment actions to ensure success of a standby task deploying a property using a certificate.
* Added Enable OCSP Stapling option into the property configuration’s TLS Settings section. This can improve security and performance for large sites serving many users.
* Improved display of confirmation and status popups.
* Implemented ‘standby task’ which is a way to queue up multiple property and certificate deployments and undeployments to be executed in a single task.

## November 18, 2020
### API updates
* Added disableHttp2 property configuration option to allow you to disable support for HTTP/2 and use HTTP 1.1 only.
* Added cacheKeyUri property configuration option to control when the URL is incorporated into the cache key.
* Updated [edge requests report](</apidocs#operation/getEdgeRequests>) to support the Accept HTTP header with quality values.
* Improved validation of Edge Logic using [eval_func](</docs/edge-logic/supported-directives#eval_func>).
* Improved [hostnames API](</apidocs#operation/listhostnames>).
* Added the [origin_selection_algorithm directive](</docs/edge-logic/supported-directives#origin_selection_algorithm>) so you can control the selection of an IP address if an origin resolves to muliple IP addresses.

### Portal updates
* Provided date range selectors in the portal for validation and deployment tasks.
* Improved display of lists of items.
* Supported grouping by customer ID for summary reports.
* Improving searching for deployment tasks.

## November 6, 2020
### API updates
* Updated [get property validation task API](</apidocs#operation/queryValidationTask>) to return cache version as well.
* Allowed a wildcard hostname to overlap with another hostname owned by the same customer.

### Portal updates
* Allow a client zone to support multiple ISPs. (These are specified when creating an edge hostname.)
* Added a banner at the top of the dashboard pointing to the ‘Quick Start’ help.
* Fixed pagination issues.
* Improved display of three Edge Logic directives: [proxy_cache_lock](</docs/edge-logic/supported-directives#proxy_cache_lock>), [proxy_cache_lock_timeout](</docs/edge-logic/supported-directives#proxy_cache_lock_timeout>), and [proxy_cache_lock_age](</docs/edge-logic/supported-directives#proxy_cache_lock_age>).

## October 22, 2020
### API updates
* The [traffic volume summary report](</apidocs#operation/getVolSummary>) now supports grouping of results by customerIds.
* Improved error message when the user uses an unauthorized or unsupported directive.
* If a reseller performs a validation, deployment, or purge on behalf of their customer, we track the caller’s API account.
* Added 3 new Edge Logic directives: [proxy_cache_lock](</docs/edge-logic/supported-directives#proxy_cache_lock>) to better control traffic to the origin servers, [proxy_cache_lock_age](</docs/edge-logic/supported-directives#proxy_cache_lock_age>) to specify a time after which another request may be made, and [proxy_cache_lock_timeout](</docs/edge-logic/supported-directives#proxy_cache_lock_timeout>) to set a timeout for proxy_cache_lock.
* Prevented an acceleration hostname from matching the origin server to avoid a loop.
* Added a property configuration field, disableCertAutomation, which should be set to true if you manage certificate renewals yourself instead of using our certificate auto-renewal via Let’s Encrypt.
* Improved real-time log support.
* Allowed headers to be passed to the notification server in the real-time log feature.

### Portal updates
* Improved certificate selection in the property creation and update pages.
* Improved pagination in pages with lists of items.
* Added “Disable Certificate Renew Automation” setting to advanced settings of properties.
* Prevented the user from creating a property whose hostname is the same that of an origin server.

## October 7, 2020
### API updates
* Added [CPU time report](</apidocs#operation/post-cdn-report-cpuTime>) to display CPU time used to handle requests for your content.
* Allowed resellers to use the ‘Report-Range: children-only’ header in [API calls](</apidocs#operation/get-ngadmin-apicalls>) to get a summary of API calls made in their customers' accounts.
* Enabled the [origin_set_header directive](</docs/edge-logic/supported-directives#origin_set_header>) to support the "Host" header.
* Allowed query of [fast route request](</apidocs#operation/post-cdn-report-fastOriginReq>) and [fast route traffic](</apidocs#operation/post-cdn-report-fastOriginVol>) reports for domain names with wildcard "*".
* Improved error checking of [portal user list](</apidocs#operation/post-cdn-report-fastOriginVol>) and [API account list](</apidocs#operation/get-ngadmin-apiAccounts>).

### Portal updates
* Improved page navigation.
* Improved assignment of multiple portal users to a role.
* Added fast route request and volume reports.

## September 24, 2020
### API updates
* Added support for startdate and enddate parameters for querying [validation](</apidocs#operation/queryPropertyValidationList>) and [deployment task](</apidocs#operation/queryDeploymentTaskList>) lists.
* Allowed deletion of a property version.
* Updated [service quota API](</apidocs#operation/patch-cdn-serviceQuotas-customer-customerId>).
* Added fast route traffic to the [traffic volume summary report](</apidocs#operation/getVolSummary>) to show traffic accelerated by the [High-Speed Data Transmission product](<https://www.cdnetworks.com/high-speed-data-transmission/>).
* Supported CSR validation by more certificate authorities, not just Let’s Encrypt.
* Improved error handling of parameters when [getting purge requests](</apidocs#operation/getPurgeRequestList>).

### Portal updates
* Improved display of pages listing items.
* Updated edge hostname creation button label to be consistent with others.
* Updated colors on edit role page.
* Made redirection of HTTP to HTTPS the default when setting up a property.
* Displayed requests per second in 5 minute interval charts.
* Supported click to copy of hostnames when viewing a property.


## September 10, 2020
### API updates
* Supported specification of weights when defining origin servers of a property.
* Supported X-Forwarded-Scheme header when [purging a file](</apidocs#operation/createPurge>).  This ensures purges work if the property’s Edge Logic does a redirection from HTTP to HTTPS.

### Portal updates
* For usability, supported click to copy hostnames when editing a property.
* Supported specification of weights when defining origin servers of a property.
* Improved usefulness of pie charts by sorting results, showing the top 30 slices, and consolidating the remaining values into another slice.
* Ensured password reset page is accessible in China.

## August 28, 2020
### API updates
* Added support for filtering the [ISPs list](</apidocs#operation/get-cdn-edgeHostnames-isps>) by region.
* Added support for filtering the [region list](</apidocs#operation/get-cdn-edgeHostnames-clientRegions>) by ISP.
* Added support for multiple ISPs in a client zone rule.
* Added support for origin_host in the real-time log feature.
* Allowed all customers to use these directives: [sorted_querystring_filter_parameter](</docs/edge-logic/supported-directives#sorted_querystring_filter_parameter>) to remove some query parameters; [proxy_ignore_cache_control](</docs/edge-logic/supported-directives#proxy_ignore_cache_control>) to disable processing of certain cache-control directives in the response from the origin; [slice](</docs/edge-logic/supported-directives#slice>) to set the size of the slices when fetching large files from the origin; and [origin_header_modify](</docs/edge-logic/supported-directives#origin_header_modify>) to add, delete, or overwrite the response header fields from the origin before any other processing.
* Added [slice_ignore_etag directive](</docs/edge-logic/supported-directives#slice_ignore_etag>) to disable ETag consistency check of sliced files.
* Made it easier for a reseller to purge a directory or file on behalf of their customer.
* Added [fast route origin request report API](</apidocs#operation/post-cdn-report-fastOriginReq>) to show the origin requests accelerated by the High-Speed Data Transmission product.
* Added [fast route origin traffic report API](</apidocs#operation/post-cdn-report-fastOriginVol>) to show the origin traffic accelerated by the High-Speed Data Transmission product.
* Updated report APIs to support UTC+13 and UTC+14 time zones.
* Allowed purging of URLs with upper and lower case characters.
* Fixed [historical hostnames API](</apidocs#operation/getHistoricalHostnames>) to omit properties that have only deployed to staging.
* Supported keepalive_timeout in the origin section of a property definition.

### Portal updates
* Improved display of pages.
* Improved representation of certificate ownership.
* Emailed trial users about upcoming expiration.
* Supported Keep-Alive timeout setting in the advanced property origin section.

## August 12, 2020

### API updates
* Added several advanced Edge Logic directives: [origin_fast_route](</docs/edge-logic/supported-directives#origin_fast_route>) allowing you to use our High-Speed Data Transmission (HDT)-powered solution to provide a more reliable connection with reduced latency; [origin_follow_redirect](</docs/edge-logic/supported-directives#origin_follow_redirect>) if you wish us to follow 30X redirects from the origin; and [custom_log_field](</docs/edge-logic/supported-directives#custom_log_field>) allowing you to add fields to the access logs.
* Fixed error handling when purging files with multiple copies due to the Vary header.
* Added support for access control rules to properties to let you restrict access by IP or regions.
* Improved validation of EC certificates.
* Added support for kilobytes in the [limit_rate directive](</docs/edge-logic/supported-directives#limit_rate>).
* Allowed the redirectHttpToHttps property configuration field to support return codes 302, 307, and 308.
* enableIPv6 is supported only by the deliver action in client zone rules.
* Made 512 kilobytes the minimum value of the [slice directive](</docs/edge-logic/supported-directives#slice>).

### Portal updates
* Added "view deployment history" for properties and certificates.
* Allowed a custom role to deploy a certificate.
* Fixed display issues.
* Made enableIPv6 an option for the deliver action only in client zone rules.
* Fixed deployment related issues.

## July 30, 2020
### API updates
* Added enableOcspStapling field to the property configuration to support OCSP stapling.
* Handled expired trial customers.

### Portal updates
* Improved display of lists in the portal.
* Displayed search and filter parameters in the URL of Task list pages.
* Allowed IPv6 when creating a client zone rule for an edge hostname.
* Added Validation and Deployment submenu items under the Tasks menu.

## July 16, 2020
### API updates
* Updated resellers' creation of customer accounts.
* Used qtlcdn.com domain for new edge hostnames.

### Portal updates
* Improved interface for editing property and certificates.
* Fixed display issue in the client zone rule creation page.
* Added support for Escape key to cancel operations.
* Implemented page for trial users to get information about upgrading.
* Changed Create Purge's default to invalidate instead of delete.
* Improved usability of the Edge Logic editor including more keyboard shortcuts and auto-complete.

## July 1, 2020
### API updates
* Updated support for China PoPs.
* Allowed strings in Edge Logic to span multiple lines.
* Allowed hyphens and periods in an origin name.
* Added the [system configuration API](</apidocs#operation/get-cdn-systemConfigs>) to return system settings.

### Portal updates
* Updated the portal links to help pages.
* Allowed the escape key to be used to cancel operations and close windows.
* Added support for trial accounts.
* Improved the Edge Logic editor to highlight some syntax errors and support auto-completion of directive and variable names.


## June 12, 2020
### API updates
* Updated property validation to show the line number if an error is found in the Edge Logic.
* Added optional tlsSessionTimeout field to the property configuration to control the TLS session ticket timeout.
* Updated [edge hostname request report](</apidocs#operation/post-cdn-report-edgeHostnameReq>) and [edge hostname request summary](</apidocs#operation/post-cdn-report-edgeHostnameReqSummary>) report APIs.

### Portal Updates
* Fixed purge request progress dialog.
* Improved Edge Logic editor to highlight directives and make it more useful.


## June 5, 2020
### API updates
* Improved purge performance.
* Enabled support for the Edge Logic directive, [proxy_cache_methods](</docs/edge-logic/supported-directives#proxy_cache_methods>) so you can specify the HTTP methods whose responses are cached.


## May 22, 2020
### API updates
* Updated limit on purge requests to a maximum of 1000 files and 5 directories at a time.
* Improved [property list API's](</apidocs#operation/getPropertyList>) filtering.
* Introduced [origin_limit_rate directive](</docs/edge-logic/supported-directives#origin_limit_rate>) allowing you to limit the speed at which the response is read from the origin server.
* Introduced [origin_set_header directive](</docs/edge-logic/supported-directives#origin_set_header>) allowing you to redefine or append fields to the request header passed to the origin server.
* Introduced advanced directive [origin_header_modify](</docs/edge-logic/supported-directives#origin_header_modify>) allowing you to add, delete, or overwrite the response header fields from the origin before any other processing.
* Introduced [origin_connect_timeout](</docs/edge-logic/supported-directives#origin_connect_timeout>) allowing you to define a timeout for establishing a connection with the origin server.
* Introduced [origin_read_timeout](</docs/edge-logic/supported-directives#origin_read_timeout>) allowing you to define a timeout for reading a response from the origin server.
* Introduced [origin_send_timeout](</docs/edge-logic/supported-directives#origin_send_timeout>) allowing you to set a timeout for transmitting a request to the origin server. 

### Portal updates
* Updated access control.
* Renamed menu items to better reflect their functionalities.

## May 8, 2020

### API updates
* Fixed the [report APIs’](</apidocs#tag/Reports>) support for wildcards in the hostname filter.
* Implemented a service to monitor Beian status of domains served by PoPs in China. 
* Allowed disabling of  support for IPv6 within a client zone rule.
* Ensured that non-printable characters can only appear in Edge Logic if quoted.
* Improved [property list API](</apidocs#operation/getPropertyList>)'s filtering support.

### Portal updates
* Changed real-time logging format field to make it easier to use.

## April 23, 2020

### API updates
* Allowed notifications to be sent to extra recipients.
* Implemented [CDN product management APIs](</apidocs#tag/CDN-Product-Management>).
* Updated support for trials.
* Fixed validation of Edge Logic to allow non-Latin characters.

### Portal updates
* Added ‘Load Balancer Hash Key’ field to Advanced Settings of properties.
* Improved error handling for client zone rules.
* Fixed list display issue for screens of different sizes.
* Improved forgotten password functionality.

## April 10, 2020
### API updates
* Added support for limiting the number of portal users.
* Made regionalOffice field required.
* Support filtering search of customers based on the regionalOffice field.
* Support [updating an edge hostname using PATCH](</apidocs#operation/patch-cdn-edge-hostname>).
* Enhanced security to provide additional notifications when settings have been changed.
* Supported trial customers.

## March 25, 2020

### API updates
* Increased security of portal users.
* Increased security by notifying of account changes.
* Allowed search of [client regions](</apidocs#operation/get-cdn-edgeHostnames-clientRegions>) by keyword.
* Fixed use of redirectHttpToHttps with multiple hostnames.

### Portal updates
* Fixed issues switching between our [Edge Computing Platform (ECP)](<https://www.cdnetworks.com/edge-computing/>) and CDN360 products.
* Allowed selection of ISPs when defining client region rules for edge hostnames.
* Added support for ‘group by’ to traffic summary report.

## March 10, 2020
### API updates
* Ensured email address is required when [creating an API account](</apidocs#operation/post-ngadmin-apiAccounts>).
* Enhanced [ISP list API](</apidocs#operation/get-cdn-edgeHostnames-isps>) to support search by keyword and sorting of results.
* Improved certificate expiration notice.

### Portal updates
* Improved security.
* Added fields to the edge hostname list.
* Improved display of lists.
* Added “Has ICP Beian” option for edge hostnames.

## February 26, 2020
### API updates
* Allowed filtering by Beian status in [edge hostnames list API](</apidocs#operation/getEdgeHostnames>).
* Enhanced [API call history](</apidocs#operation/get-ngadmin-apicalls>) for resellers. We also updated it to return HTTP response statuses of API calls.
* Enabled [portal user list API](</apidocs#operation/getContacts>) to return results based on status of the user accounts.
* Allowed users of [customer list API](</apidocs#operation/get-ngadmin-customers>) to search by ‘regional offices’.

### Portal updates
* Improved email about expiring password.
* Improved validation of properties.

## February 13, 2020
### API updates
* Fixed [customer update API](</apidocs#operation/patch-ngadmin-customers-id>) to properly handle null fields.
* Improved security of [Get API Account](</apidocs#operation/get-ngadmin-apiAccounts-id>). 
* Enhanced [get edge hostname API](</apidocs#operation/getEdgeHostname>)'s response.

### Portal updates
* Fixed sorting of results on the pages which contain lists of items.
* Enhanced certificate list page.
* Improved display of lists of items.
* Fixed 2FA support.
* Fixed display issue in the password reset page.

## January 29, 2020
### API updates
* Improved support for auto-renewal of SSL certificates.
* Added [edge hostname statistics report](</apidocs#operation/post-cdn-report-edgeHostnameReq>).
* Added [edge hostname summary report API](</apidocs#operation/post-cdn-report-edgeHostnameReqSummary>).
* Supported email notification about TLS certificates that are expiring soon.

### Portal updates
* Fixed issue editing certificates.
* Improved error message for property validation.
* Fixed hint text in search boxes.
* Improved error text for password reset.

## January 10, 2020
### API updates
* Allowed resellers to use the Report-Range header in the [API calls function](</apidocs#operation/get-ngadmin-apicalls>) to further customize their search of API call history.

### Portal updates
* Fixed sorting on Roles page.
* Improved search box behavior.
* Improved display of password reset page.

## January 3, 2020
### API updates
* Enhanced [customer list API](</apidocs#operation/get-ngadmin-customers>)'s filtering.
* Limited API request body size.
* Updated [get service quota API](</apidocs#operation/get-cdn-serviceQuotas-customer-customerId>) to support 'me' as a parameter value allowing you to see your own settings.
* Updated summary report APIs' responses to include a special group __all__ which consists of total traffic or requests of all groups.

### Portal updates
* Added "Validate" link below "Real Time Logging URL".
* Improved forgotten password functionality.

## December 11, 2019
### API updates
* Supported getting expiration times of certificates deployed to production and staging.
* Changed certificate number from decimal to hexadecimal value for consistency with browsers and other tools.
* Allowed resellers to filter results using the Report-Range header when retrieving [API accounts](</apidocs#operation/get-ngadmin-apiAccounts>) and [portal users](</apidocs#operation/getContacts>).
* Supported auto-renewal of certificates.
* Sorted validation task list by submission time by default.
* Ensured that read-only API accounts can make calls to report APIs.

### Portal updates
* Fixed missing information on the View Certificate page.
* Improved validation of real-time logging settings.
* Changed the label of certificate hash to “Fingerprint”.
* Fixed the display of cache hit ratio when origin traffic is larger than edge traffic.

## December 2, 2019
### API updates
* Fixed support for protocol downgrade to apply only if the property has a certificate.
* Added support for ISPs in an edge hostname's client zone rules.
* Supported [search of purge tasks](</apidocs#operation/getPurgeRequestList>) by ID.
* Supported hasConfig query parameter when getting a [list of properties](</apidocs#operation/getPropertyList>).
* Added [system configuration API](</apidocs#operation/get-cdn-systemConfigs>).
* Allowed resellers to use the Report-Range header to filter the [list of properties](</apidocs#operation/getPropertyList>).
* Added [portal user management APIs](</apidocs#tag/Portal-User-Management>) to allow callers to create, update, query, and delete users.

### Portal updates
* Auto-populated form fields when creating a new certificate version.
* Fixed search function on Content Management page.
* Displayed the purge quota on the purge creation page.
* Updated the display of the property list page.
* Updated portal documentation to describe real-time logging feature and AWS authentication support.

## November 14, 2019
### API updates
* Added [staging servers API](</apidocs#operation/getStagingServers>) to get the IP addresses of staging servers you can use to test your properties before deploying to production.
* Fixed impersonation support of [API calls](</apidocs#operation/get-ngadmin-apicalls>).
* Ensure certificates must be <=36kB to avoid problems with IE browser.
* Enhanced [customer list API](</apidocs#operation/post-ngadmin-customers>) to support new filters.
* Updated [customer management API](</apidocs#tag/Customer-Management>) to support portalSettings field which includes enabling two factor authentication, password expiration, session logout, and IP whitelist.
* Added support for separate purge quotas for staging and production.

### Portal updates
* Improved security of notifications.
* Improved signup invitation.
* Added support for authentication of [Amazon S3 servers used as the origin](</docs/recipes/aws-bucket>).
* Added support for real-time log.
* Improved appearance of the property comparison page.
* Allowed customer administrators to change the session logout time.

## November 1, 2019
### API updates
* Ensured customers of resellers can have any of the products available to the reseller.
* Added apiName to the edge hostname deployment history
* Added apiName to the [API calls](</apidocs#operation/get-ngadmin-apicalls-id>) response.
Added [proxy_ignore_cache_control](</docs/edge-logic/supported-directives#proxy_ignore_cache_control>) directive allowing you to disable processing of certain cache control directives in the response from the origin.

### Portal updates
* Updated property version comparison user interface.
* Supported the Korean and Japanese languages.
* Updated the Edit User page.

## October 21, 2019
### API updates
* Improved report API calls.
* Supported sorting of certificates.
* Allowed resellers to use the Report-Range header in [certificate list API](</apidocs#operation/getCertificates>).
* Improved [status code details](</apidocs#operation/getEdgeStatusCodeDetails>) and [origin status code details](</apidocs#operation/getOriginStatusCodeDetails>) reports.
* Allowed all customers to use the [proxy_buffering](</docs/edge-logic/supported-directives#proxy_buffering>) directive.

### Portal updates
* Improved portal security.
* Enabled administrators to invite new users to join by email.
* Fixed search functionality.
* Fixed user suspension and reactivation.

## October 7, 2019
### API updates
* Added support for sorting properties, tasks, edge hostnames, accounts, and customers returned by APIs.
* Improved randomness of property IDs.
* Improved stripping of comments in Edge Logic.
* Allowed the cacheKeyHostname field to support NGINX variables.
* Moved API account limits to the customers API.


### Portal updates

* Supported passing headers in file and directory purges.
* Saved preferred language for each portal user.
* Added “operator” role you can assign to users who are permitted to administer CDN functions but not manage users and roles.

## September 23, 2019
### API updates
* Supported origin server authentication.
* Supported searching for customer by ID.
* Added support for certificate expiration and auto-renewal.
* Made self-signed certificate expire in 10 days.

### Portal updates
* Updated role list page.
* Supported search in the Roles tab.
* Ensured customers have at least one administrator account.

## September 16, 2019
### API updates
* Added support for real-time logs (also known as download notification).
* Improved error handling.
* Added API support for [enabling two factor authentication (2FA)](</apidocs#operation/patch-ngadmin-customers-id>) and [resetting a user](</apidocs#operation/patch-ngadmin-contacts-id>) which is useful if they change phones.

### Portal updates

* Added identity and access management page.
* Added support for role management.

## August 22, 2019
### API updates
* Fixed notification API.
* Relaxed the requirements on content handler in 'if' blocks.
* Made the origin hostHeader support NGINX variables.

### Portal updates
* Updated product logos.
* Supported pagination in list of customers.
* Updated support for editing profile.

## August 13, 2019
### API updates
* Added support for email notifications of events.
* Fixed support for protocol downgrade option.
* Updated [get certificate version API](</apidocs#operation/queryCertificateVersion>).

### Portal updates
* Supported additional languages.
* Supported comparison of different versions of a property.
* Made specifying an origin for a property optional.


## July 29, 2019
### API updates
* Added support for loadBalancerHashKey.
* Fixed protocol downgrade support.
* Returned error code "VariedFile" when purging a file with multiple copies due to the Vary header.
* Updated validation for deleting customers.

### Portal updates
* Enabled gzip in the portal server to compress response of large size.
* Updated access denied page.
* Improved security.
* Updated protocol downgrade support.

## July 17, 2019
### API updates
* Added APIs to support creating and retrieving notifications.
* Supported searches in the portal user list page.
* Supported certificate sharing in the portal.
* Updated authorization to check for assigned product.
* Improved error handling of purge requests.

### Portal updates
* Made “Download Options” on reports functional.
* Implemented contact management UI.
* Added role list page.
* Added validation when using a second TLS certificate.

## July 2, 2019
### API updates
* Added products, emailAddress, and responsiblePerson fields to the customer resource.
* Validated [slice](</docs/edge-logic/supported-directives#slice>), [limit_rate](</docs/edge-logic/supported-directives#limit_rate>), and [limit_rate_after](</docs/edge-logic/supported-directives#limit_rate_after>) Edge Logic directives.
* Added [CDN Product Management APIs](</apidocs#tag/CDN-Product-Management>).

### Portal updates
* Updated client region values.
* Implemented access denial page.
* Fixed display of link to the [Edge Computing Platform (ECP) product](<https://www.cdnetworks.com/edge-computing/>) portal.

## June 17, 2019
### API updates
* Fixed issues related to client region support.
* Added support for redirectHttpToHttps setting.
* Added products, responsiblePerson, and emailAddress fields to API accounts.

### Portal updates
* Updated role and permission management.

## June 3, 2019
### API updates
* Supported pagination and searches in [account list API](</apidocs#operation/get-ngadmin-apiAccounts>).
* Updated support for testing deployments to staging.
* Supported gzip compression in API responses.
* Supported longer origin timeouts.
* Allowed bandwidth and volume reports to be filtered by server groups.
* Ensured that properties can be validated if a shared certificate it is using is no longer shared.
* Added two directives [proxy_cache_vary](/cdn/docs/edge-logic/supported-directives#proxy_cache_vary>), allowing you to control how the 'Vary' response header from the origin is handled, and [eval_func](</docs/edge-logic/supported-directives#eval_func>), allowing you to run some common algorithms in your Edge Logic.

### Portal updates
* Added a link to the Edge Computing Platform portal.
* Added two directives [proxy_cache_min_age](</docs/edge-logic/supported-directives#proxy_cache_min_age>), allowing you to specify the minimum cache time, and [gzip_types](</docs/edge-logic/supported-directives#gzip_types>), allowing you to enable gzip compression on additional MIME types.
* Updated password reset functionality.


## May 16, 2019
### API updates
* Added support for [searching purge history by hostname](</apidocs#operation/getPurgeRequestList>).
* Updated [supported Edge Logic directives](</docs/edge-logic/supported-directives>).
* Updated certificate APIs.
* Fixed purge issues.
* Changed edge hostname TTL to 60 seconds.

### Portal updates
* Allowed resellers to disable customers’ use of a shared certificate.
* Enhanced usability.

## April 16, 2019

### API updates
* Enhanced [get customer API](/cdn/apidocs#operation/get-ngadmin-customers-ID>).
* Fixed directory purge.
* Supported retrieving the identities of properties and domains using a certificate in staging and production.
* Allowed resellers to [search for multiple customers by their IDs](</apidocs#operation/get-ngadmin-customers>).

### Portal updates
* Required users to confirm changes before deploying a property.
* Improved the create property page.
* Supported several additional NGINX directives.
* Improved login page.

## March 31, 2019
### API updates
* Improved validation of the Edge Logic.
* Added support for getting the customer ID that owns various resources.
* Updated the list of [supported NGINX directives](</docs/edge-logic/supported-directives>).
* Fixed purge of URLs with special characters.
* Separated file and directory purge quotas.
* Improved cache key hostname.

### Portal updates
* Improved the certificate sharing UI.
* Improved the layout of the edge hostname client zone rules.
* Improved purge and certificate UI.

## March 18, 2019
### API updates
* Split purge quota into separate file and directory quotas.
* Added support for returning the customer ID that owns various resources.
* Improved [status code details](</apidocs#operation/getEdgeStatusCodeDetails>) report.
* Updated cache key hostname processing.

### Portal updates
* Improved property, report, edge hostname, and certificate pages.

## March 4, 2019
### API updates
* Improved deployment.
* Updated [certificate update API](</apidocs#operation/updateCertificate>).
* Updated [purge API](</apidocs#operation/queryPurgeStatus>) to expose success rate and improve validation of URLs.


## February 19, 2019
### API updates
* Improved validation when [creating a customer account](</apidocs#operation/post-ngadmin-customers>).
* Fixed issues with the property converter.
* Improved the [get property version API](</apidocs#operation/getPropertyVersion>).
* Encoded URI and query string in purge requests.
* Improved purge APIs further.

### Portal updates
* Improved edge hostname creation and edit user interface.
* Improved origin auto-detect UI.
* Allowed the user to delete notifications.
* Improved the edit property page UI.
* Improved the edit certificate UI.
* Improved the add origin UI.

## January 31, 2019
### API updates
* Saved NGINX configurations during the validation step to help with future deployments.
* Supported purge with file headers.
* Improved purge APIs.
* Enhanced report APIs.

### Portal updates
* Supported multiple hostnames.
* Improved report pages.
* Supported notification of events in the portal.

## January 16, 2019
### API updates
* Fixed issue related to certificates.

### Portal updates
* Supported user added headers in purge requests.
* Supported file and folder purge requests.
* Improved report page.

## January 8, 2019
### API updates
* Supported folder [purge](<apidocs#operation/createPurge>).
* Fixed [historical hostname API](</apidocs#operation/get-cdn-hostnames-historical-hostname>).
* Improved security.
* Improved client zone rules of edge hostnames.

## December 20, 2018
### API updates.
* Allowed querying for [purge statistics](</apidocs#operation/queryPurgeSummary>).
* Updated [historical hostname API](</apidocs#operation/getHistoricalHostnames>).
* Improved encryption of certificate keys.
* Added APIs for [logs](</apidocs#operation/getLogfiles>) and [intermediate traffic](</apidocs#operation/getIntermediateTraffic>).
* Added [Get property version list API](</apidocs#operation/getPropertyVersions>).
* Improved error handling.

## December 3, 2018
### API updates
* Updated APIs for auditing.
* Improved identification of failures in property deployment.
* Added [historical hostname list API](</apidocs#operation/getHistoricalHostnames>).
* Supported filtering in [report APIs](</apidocs#tag/Reports>).

## November 19, 2018
### API updates
* Added allowedCacheDirectives to control access to resource-intensive NGINX directives.
* Updated [edge hostname API](</apidocs#operation/createEdgeHostname>).

## November 6, 2018
### API updates
* Improved error messages.
* Improved CSR downloads.
* Improved [edge hostname APIs](</apidocs#tag/Edge-Hostname-Management>).

## October 22, 2018
### API updates
* Updated output of [Get API Account](</apidocs#operation/get-ngadmin-apiAccounts-id>).
* Improved validation of edge hostnames' clientZones.

## September 21, 2018
### API updates
* Updated property validation and conversion.
* Enhanced [customer list API](</apidocs#operation/get-ngadmin-customers>).

## September 13, 2018
### API updates
* Improved validation.
* Updated annotation and [edge hostname creation](</apidocs#operation/createEdgeHostname>). 


## August 30, 2018
### API updates
* Updated report annotation.
* Improved [validation of properties](</apidocs#operation/createValidationTask>).

## August 13, 2018
### API updates
* Updated property validation.
* Updated report annotations.

## July 13, 2018
* Improved property and certificate APIs.

## July 3, 2018
### API updates
* Improved error handling.
* Improved [property creation API](/apidocs#operation/createPropertyVersion>).

## June 18, 2018
### API updates
* Fixed [get hostname API](</apidocs#operation/queryOneHostname>).
* Supported [searching for property validation task](</apidocs#operation/queryPropertyValidationList>) by keyword.

### API updates
* Improved certificate and account management.

## May 18, 2018
### API updates
* Improved deployment task APIs to support our portal.

## May 10, 2018
### API updates
* Improved [property update API](</apidocs#operation/getPropertyVersion>).

## February 23, 2018
### API updates
* Improved error handling when [creating API accounts](</apidocs#operation/deleteApiAccount>).
* Required encryption of private keys
* Improved getting property details.
* Fixed handling of suspended customers.
* Improved report APIs.


## February 9, 2018
### API updates
* Improved API account updates.
* Updated [customer list API](</apidocs#operation/post-ngadmin-customers>).

## January 26, 2018
### API updates
* Fixed issues in [API account list](</apidocs#operation/post-ngadmin-apiAccounts>) and [update API account](</apidocs#operation/patch-ngadmin-apiAccounts-id>).
* Improved error handling of property validations.
