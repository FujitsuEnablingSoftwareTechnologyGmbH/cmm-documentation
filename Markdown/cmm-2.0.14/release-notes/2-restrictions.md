## 2 Restrictions

This chapter describes known restrictions of this release.


### Caching in Internet Explorer 11.

Errors occur due to problems with caching in Internet Explorer 11.0. When the browser accesses
a page, it uses data stored in its cache to load the page. If the page is often receiving new data,
however, the page may appear to be not loading properly.


### Workaround:

Edit your cache configuration. For this purpose, select **Tools** -> **Internet options** in the Internet
Explorer. On the **General** tab, in the **Browsing history** section, click **Settings**. In the **Check for
newer versions of stored pages** section, make sure that **Every time I visit the webpage** is
selected.


### Triggering Alarms for Compound Alarm Definitions

Due to a known issue in the Monasca Threshold Engine, an alarm is not triggered under the
following circumstances:

- The alarm expression combines two metrics using OR as a logical operator.
- The threshold value at which an alarm is to be triggered has been exceeded for one metrics,
  but no metrics data has been received for the other metrics that is combined in the expression.


### Accessing the Kibana Dashboard After Switching the OpenStack Project

Errors occur due to problems with browser caching. When you switch to another OpenStack
project in OpenStack Horizon and then try to access Kibana, the Kibana dashboard may appear to
be not loading properly.


### Workaround:

When Internet Explorer 11.0 or Chrome 63.0 is used, you have to manually reload the Kibana
page. For this purpose, click **clear your session** or **Go back** in the message window that is
displayed. Alternatively, you can also use the default options of your browser to reload the page.

When Firefox 57.0 is used, you have to clear the Firefox cache, close the browser window, and
restart Firefox.


### Accessing the Kibana Dashboard in Internet Explorer 11.

An error occurs when trying to access Kibana. When Internet Explorer 11.0 is used, you are
prompted to download a file and the Kibana dashboard is not loaded.


### Workaround:

Click **Cancel** in the message window that is displayed, or simply close the message window. Then
click **Log Management** on the **Overview** page again.


### Sorting in Wrong Order

Due to a known issue in the Horizon Plugin, alarm definitions, alarms, and notifications are
displayed in a wrong sort order on the **Monitoring** tab in OpenStack Horizon. Alarm definitions,
alarms, and notifications are not sorted by name, but by `alarm_definition_id`, `alarm_id`, and
`notification_method_id`.
