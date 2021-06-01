## 2 Restrictions

This chapter describes known restrictions of this release.


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

When Chrome 63.0 is used, you have to manually reload the Kibana page. For this purpose, 
click **clear your session** or **Go back** in the message window that is displayed. 
Alternatively, you can also use the default options of your browser to reload the page.

When Firefox 57.0 is used, you have to clear the Firefox cache, close the browser window, and
restart Firefox.
