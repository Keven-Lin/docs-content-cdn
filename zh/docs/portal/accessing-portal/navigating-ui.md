# Navigating the CDN360 User Interface

When you first log in to the CDN360 portal, menus and submenus appear in the left pane and the dashboard appears in the workspace to the right.

The default menu lists the CDN360 activities you can perform.

<p align=center><img src="/docs/resources/images/accessing-portal/side-menu.png" alt="navigation menu" width="300"></p>

## Dashboard

The dashboard is the default page that appears when you log in to the CDN360 portal. It contains charts that show a snapshot of your account traffic over a recent period of time. For detailed information, hover your mouse over the data entry points. For example:

<p align=center><img src="/docs/resources/images/accessing-portal/total-bandwidth.png" alt="total bandwidth" width="1000"></p>

From the dashboard, you can view:

- Traffic volume, traffic bandwidth, and traffic requests information for all properties.
- Status codes for all properties.

A legend below each chart shows the names of the data entry points in the chart. Clicking a data entry point in the legend removes that data entry point from the chart. Clicking it again redisplays the data entry point. Clicking **View Full Report** below a chart displays the [Reports page](</docs/portal/reports.md>), where you can define report parameters and view a graph that compares the current 5-Minute Edge to the option selected in the drop-down list (Traffic Volume, Traffic Bandwidth, and so on) at the top left of the dashboard chart.

<p align=center><img src="/docs/resources/images/traffic-volume.png" alt="traffic volume" width="1000"></p>

## Reports

The [Reports page](</docs/portal/reports.md>) allows you to generate reports about:

- Traffic volume and bandwidth to your hostnames.
- Number of requests made to the files of your property.
- Percentage of each HTTP status code returned as a result of requests to your content.
- Content that has been requested and when, the IP address from which requests were made, the value of the User-Agent HTTP request header, and the size of the content requested.

## Edge Configurations

In CDN360, you configure the edge servers' behavior by defining [Properties](</docs/portal/edge-configurations/managing-properties.md>). The process of developing a property is very much like developing any other software. You can create and edit a property, and then validate, test, deploy, and upgrade it -- all conveniently from the CDN360 portal. **Edge Configurations** also provides a page where you can create and manage a [secret](</docs/portal/secrets/overview.md>) that you share with CDNetworks in order for the CDN configuration to work.

## Traffic Management

CDN360 gives you full control of its Global Service Load Balancing (GSLB) system through the [Traffic Management page](</docs/portal/traffic-management/overview.md>). Using this page, you create edge hostnames that will be used in CNAME records to map your service hostnames. The rules you specify for each edge hostname control where each end user's request is routed.

## Certificates

The [Certificates page](</docs/portal/certificates/overview.md>) allows you to manage certificates to be used with the TLS protocol.

## Content Management

The [Content Management page](</docs/portal/content-management.md>) allows you to create purge requests and check the status of previously submitted requests. A purge request is used to flush cached contents before they expire in order to make the updated version available to the end users sooner.

## Tasks

On the Tasks page, you can check the status of all previously submitted [validation](</docs/portal/tasks/validations.md>) and [deployment/undeployment](</docs/portal/tasks/deployments.md>) requests. Synchronous tasks can take a few minutes to finish.
