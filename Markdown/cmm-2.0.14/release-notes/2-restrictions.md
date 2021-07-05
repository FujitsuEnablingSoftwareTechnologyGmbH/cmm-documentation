## 2 Restrictions

This chapter describes known restrictions of this release.

### Update of Alarm Definitions  

Update of alarm definitions does not work as expected when updating the following parameters:

- Function
- Time/Times
- Deterministic

If you want to change one of these parameters, pls. delete the existing alarm definition and create a new alarm definition.

**Note:**  
Time/Times cannot be specified in CMM UI when you create an alarm definition.  
If you want to specify values for time/times, please use monasca CLI.  
Syntax to create an alarm definition with monasca CLI:  
```
monasca alarm-definition-create [-h] [--description <DESCRIPTION>]  
[--severity <SEVERITY>]  
[--match-by <MATCH_BY_DIMENSION_KEY1,MATCH_BY_DIMENSION_KEY2,...>]  
[--alarm-actions <NOTIFICATION-ID>]  
[--ok-actions <NOTIFICATION-ID>]  
[--undetermined-actions <NOTIFICATION-ID>] [-j]  
<ALARM_DEFINITION_NAME> <EXPRESSION>  
```
Pls. write `<EXPRESSION>` in quotes.  
Simple example:  
`monasca alarm-definition-create TEST-ALARM-DEF "avg(cpu_perc{hostname=host1},120)>90 times 5"`


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


* Workaround:
  For all browser versions supported: Please use the default options of your browser to reload the page.


### Filtering More Than One Element in Kibana Using Firefox

Errors occur due to this known issue in Kibana 7.3.0 [Kibana Issue 41567](https://github.com/elastic/kibana/issues/41567)

* Workaround:
  For filterning more than two elements: Please use the Filter line. Example:
  ```
  hostname: "docker-host" and not (service: "kibana" or service: "logspout")
  ```

### Importing Objects in Kibana
Exported JSON files can only be imported with API, due to a known issue with Kibana 7.3.0:  
When attempting to import from web UI, an error message is shown, including information of "Unsupported Media Type".

* Workaround:  
  Use following `curl` command to import the JSON data from API: 
  ```
  curl –XPOST “<ip-address of kibana server>:5601/api/saved_objects/_import?overwrite=true” -H "kbn-xsrf: true" --form file=@<file to be imported>
  ```
  Replace `<ip-address of kibana server>`with the IP address of the server where Kibana is running and `<file to be imported>` with the local path of the file to be imported.

  
