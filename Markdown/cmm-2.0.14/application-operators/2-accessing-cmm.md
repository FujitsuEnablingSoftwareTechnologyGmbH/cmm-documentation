## 2 Accessing CMM

As an application operator, you must fulfill the following prerequisites:

- You must have access to the OpenStack platform as a user with the `monasca-user` role or any
  other role that is authorized to use the CMM monitoring functions. Additional roles are optional.
- You must be assigned to the OpenStack project whose resources you want to monitor.

Log in to OpenStack Horizon with your user name and password provided as login information
by OpenStack. For monitoring your services and virtual machines, you use the CMM monitoring
user interface which is integrated into OpenStack Horizon. The CMM functionality is available
on the **Monitoring** tab. It provides access to the monitoring data of all projects to which you are
assigned. Before you start, select the project you want to work on.


### Web Browsers

To perform monitoring tasks, you must use one of the Web browsers supported by CMM:

- Google Chrome 90.
- Microsoft Edge 91.
- Mozilla Firefox 58.  

> **Notes:** 
> - Mozilla Firefox 58: When accessing Grafana, a message is displayed: `Your browser is not fully supported. A newer Browser version is recommended`. 
>   This browser version has been extensively tested. There is no known restriction when using Firefox 58 to access CMM metric information via Grafana.
> - All Browsers: When accessing Kibana, a message is displayed: `Your browser doesn't meet the security requirements for Kibana.` 
>   However, this message is not related to browser versions. Security in CMM is ensured: Only users with access to Horizon can successfully use Kibana to 
>   access CMM log information. Thus, this message can be safely ignored.

