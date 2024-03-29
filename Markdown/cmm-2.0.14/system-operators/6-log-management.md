## 6 Log Management

For managing the log data of your services and the virtual and physical servers on which they are
provisioned, CMM integrates with Kibana, an open-source analytics and visualization platform.
CMM uses Kibana as a front-end application to the log data held in the Elasticsearch database.

Kibana allows you to easily understand large data volumes. Based on the data that is stored in
Elasticsearch indices, you can perform advanced data analysis and visualize your log data in a
variety of charts, tables, or maps. Changes to the Elasticsearch indices are displayed in CMM in
real-time.

The log management features of CMM include:

- Features for searching, visualizing, and analyzing the log data.
- Alerting features for monitoring.

In the following sections, you will find information on the log management window where you
search, visualize, and analyze your log data, as well as details on how to use the alerting features.


### Accessing CMM

For accessing CMM and performing log management tasks, the following prerequisites must be
fulfilled:

- You must have access to the OpenStack platform as a user with the `monasca-user` role, or any
  other role that is authorized to use the CMM monitoring functions. Additional roles are optional.
- You must be assigned to the OpenStack project you want to monitor.

Log in to OpenStack Horizon with your user name and password. The functions you can use in
OpenStack Horizon depend on your access permissions.

The CMM functionality is available on the **Monitoring** tab. It provides access to the log data
of all projects to which you are assigned. Before you start, select the project you want to work
on. The **Log Management** option located at the top part of the **Overview** page displays the log
management window where you can work on the log data of the selected project.


## 6.1 Working with the Log Management Window

Index patterns determine which data from the underlying Elasticsearch database can be viewed
and analyzed in CMM's log management window. Index patterns are used to identify the
Elasticsearch indices to run search and analytics against.

CMM ships with a preconfigured index pattern which allows you to instantly view and analyze
your log data when accessing the log management window for the first time. You can configure
additional index patterns to view and analyze different data from different indices. For details, refer
to *Configuring Index Patterns*.

Search queries allow you to search the Elasticsearch indices for data that match your
information requirements. The query results can be graphically represented in visualizations, and
visualizations can be organized in dashboards.

The log management window provides features for:

- Querying log data.
- Visualizing query results.
- Combining visualizations in dashboards.
- Filtering query results.
- Sharing dashboards.

The following sections provide an introduction to queries, visualizations, and dashboards. For
additional details, refer to the _Kibana documentation_.

### Querying Log Data

For querying log data, you use the **Discover** page in the log management window. It is instantly
displayed when you access the window. It shows the most recently collected log data:

![Querying Log Data](./images/Kibana-Discover.png)

The **Discover** page allows you to access the log data in every index that matches the current
index pattern. In addition to submitting queries, you can view, filter, and analyze the log data that is
returned by your queries.

On the **Discover** page the following elements assist you in analyzing your log data:

- In the header section on top of the window, there is a **search box** for querying the
  log data. By submitting a query, you search all indices that match the current index pattern. The
  name of the current index pattern is displayed below the search box.
  You can select a different index pattern, if required. For details on configuring and selecting
  index patterns, refer to _Configuring Index Patterns_.
  
  For entering strings in the search box, you can  use Kibana Query Language (KQL) or Lucene query syntax. 
  KQL can be switched on or off with a button located besides the search box. For details, refer to the _Elasticsearch Reference documentation_.

- Use the **calender icon** located besides the search box to define a time range for filtering the 
  log data. By default, CMM displays the log data collected during the last 15
  minutes. You can deviate from this default. Multiple options are provided for defining relative or
  absolute time ranges. The time range you define is instantly applied to all log data.

- In the bottom part of the **Discover** page, you can view the **log data** returned by your
  search queries. Depending on whether you have filtered the data by index fields, the log data is
  either restricted to these fields or entire records are displayed.

- Above the histogram of log count, you see the **Selected fields** from the indices that match the 
  current index pattern. You can select individual fields to modify which log data is displayed below.
  
  Select a field from the **Available Fields** section for this purpose and use **add**. To remove a
  field, select it in the **Selected Fields** section and use **remove**.
  
  When selecting a field from the field list, the most common values for the field are shown. You can 
  also set field values as filter, or you can exclude log data with specific field values.

- If a time field is configured for the current index pattern, the distribution of log entries over time
  is displayed in a **histogram** above the display of log data.
  
  By default, the histogram shows the number of logs entries versus time, matched by the
  underlying query and time filter. You can click the bars in the histogram to narrow down the
  time filter.

Queries can be saved and re-used. They can also be shared with other users. For this purpose,
use the options provided above the search box:

- To save a query, use **Save**. Saving a query means saving both the query syntax and
  the current index pattern.

- To load a query, use **Open**. A saved query can be loaded and used by any
  OpenStack or Monitoring Service operator.

- To share a query with other users, use **Share**. The option displays a direct link to the
  query that you can forward. As a prerequisite for using a direct link, a user must have CMM
  access.

### Visualizing Query Results

CMM supports you in building graphical representations of your query results. You can choose
from different visualization types, for example pie charts, data tables, line charts, or vertical bar
charts.  

In order to create a new visualization of your results, please proceed the following way:
- Click on **Visualize** symbol located on the right side
- Confirm "Create New Visualization"

![Visualizing Query Results](./images/Kibana-Visualize.png)

You have to select a visualization type and the query to be used. You can either
create a new query or load a query you have already saved.

Based on the visualization type and the query, you can proceed with designing the graphical
representation in a visualization editor. Multiple design options and a preview function are
provided for creating, modifying, and viewing the graphical representation.

You can save and re-use visualizations. You can also share them with other users. For
this purpose, use the options provided above the search box:

- To save a visualization, use **Save**.
- To load a visualization, use **Open**. A saved visualization can be loaded
  and used by any OpenStack or Monitoring Service operator.
- To share a visualization with other users, use **Share**. The option displays an HTML 
  snippet that can be used to embed the visualization in a Web page. It also displays a
  direct link to the visualization that you can forward. As a prerequisite for using an embedded
  visualization or a direct link, a user must have CMM access.

### Combining Visualizations in Dashboards

For correlating related information or providing an overview, you can combine visualizations in
dashboards. In order to create a new dashboard, please proceed the following way:

- Click on Dashboard symbol located on the right side
- If you want to create a new dashboard: Confirm "Create new dashboard"
- If you want to work with an existing dashboard: Select the dashboard from the list of existing dashboards

![Combining Visualizations in Dashboards](./images/Kibana-Dashboard.png)

Possible operations have been provided above the search box:

- To save a dashboard, use **Save**.
- To add a visualization from a list of existing visualizations to the dashboard, use **Add**.
  Saved visualizations and saved queries can be added.
  You need at least one saved visualization or query to create a dashboard.

- To share a dashboard with other users, use **Share**. The option displays an HTML 
  snippet that can be used to embed the visualization in a Web page. It also displays a
  direct link to the visualization that you can forward. 
  Prerequisites for sharing dashboards:
  - User must have CMM access.
  - User must be logged in to OpenStack before accessing the dashboard.
 
A visualization or query result is displayed in a container on your dashboard. Various options are
provided for arranging containers:

- Move a container by clicking and dragging its title bar.
- Resize a container by dragging its bottom right corner.
- Remove a container by clicking the wheel symbol using in the top right corner of the container and selecting 
  **Delete from dashboard** from **OPTIONS** displayed.
  
**OPTIONS** sub-menu provides other funtionality, like **Edit visualization/saved search**. This allows you 
to design the graphical representation or edit the query.

For each dashboard, you can configure a refresh interval to automatically refresh its content
with the latest data. The current interval is displayed in a box besides the calender button.
If you want to change it, click the calendar button and select the appropriate time interval. 
In the dialog box shown, a refresh interval for automated refresh can be defined to instantly submit the 
underlying queries and refresh the dashboard content.

### Filtering Query Results

By submitting a query on the data displayed in a dashboard, you can filter out specific sets of data
that you want to aggregate while not changing the logic of the individual visualizations.

Use the search box above the Dashboard in the header section of the window for
entering a query on the whole dashboard. If a visualization is already based on a saved query,
both queries apply.

## 6.2 Configuring Index Patterns

CMM ships with a preconfigured index pattern that allows you to instantly explore your
Elasticsearch indices when accessing the dashboard for the first time.  Thus, configuring additional
index patterns is not required.

## 6.3 Monitoring Log Data

CMM provides alerting features for monitoring your log data. Specific log metrics support you
in checking the severity of the entries in your log files. Log metrics are handled like any other
metrics in CMM. They complete the log management features and support you in analyzing and
troubleshooting any issue that you encounter in your log data.

By default, CMM supports the following log metrics:

- `log.warning` to count warnings in your log data.
- `log.error` to count errors in your log data.
- `log.fatal` to count fatal errors in your log data.
- `log.critical` to count critical errors in your log data.

> **Note:** Your installation might deviate from this default. The log levels that can be evaluated have
  been specified during the installation of CMM.

Using the log metrics for monitoring corresponds to using any other metrics:

- Use **Monitoring > Alarm Definitions** to create, edit, and delete alarms for log data.
- Use **Monitoring > Notifications** to create, edit, and delete notifications for alarms.
- Use **Monitoring > Overview** to check whether there are any irregularities in your log data. As
  soon as you have defined an alarm for your log data and metrics data has been received, there
  is status information displayed on the **Overview** page.

For details on using the log metrics, refer to _Monitoring_.
