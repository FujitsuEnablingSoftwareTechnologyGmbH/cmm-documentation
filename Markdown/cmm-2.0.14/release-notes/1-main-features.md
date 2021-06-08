## 1 Main Features

This chapter outlines the main features of this release.


## 1.1 Multi-Platform Support

CMM comes with a Docker-based installation. Production-ready Docker images are provided for
a single-node installation. Docker accelerates deployment and rollback of the individual services
CMM is composed of.

CMM follows a multi-platform approach. The Docker-based installation can be used for different
OpenStack distributions. CMM supports and has been tested with Red Hat Enterprise Linux
OpenStack Platform 16.1.


## 1.2 Multi Tenancy for Log Management

CMM comes with multi-tenancy support for log management. The log data is securely isolated for
each tenant. Access is provided only to the log data of the project to which the tenant is assigned.
If tenant is assigned to more than one project, the project to be monitored can be selected.

It is not required to configure an index pattern when accessing the log management dashboard in
CMM for the first time. Based on a default index pattern, the user can instantly view and analyze
his log data.


## 1.3 Log Metrics

CMM provides alerting features for monitoring the log data. The Log Metrics component
consumes log data from the Message Queue, filters the data according to severity, and generates
metrics for specific severities, for example, for errors or warnings. The generated metrics are
published to the Message Queue and can be further processed by the Threshold Engine.

CMM users can use the log metrics like any other metrics available in CMM. Alarms can be
defined as well as notifications that specify how CMM users are informed when a threshold value
for the number of warnings or errors is reached or exceeded.

The automation of log handling includes the visualization of log metrics data on the monitoring
dashboards. To make it easy to locate problems in huge amounts of log data, the monitoring
overview in OpenStack Horizon displays any irregularities in the log data of the monitored system
components.


## 1.4 Preconfigured Metrics Dashboards

CMM ships with preconfigured metrics dashboards that are specially geared to the needs of the
system operators.

The dashboards are accessible instantly after installing CMM. The agent installation activates
a set of standard metrics. The data collected by these metrics is automatically visualized in the
dashboards without the need for manual interaction by the operator.


## 1.5 Compound Alarm Definitions

To handle a large variety of monitoring requirements, CMM supports compound alarm definitions.
Compound alarm definitions combine multiple metrics, thus allowing the user to track and process
more complex events.

To facilitate the process of defining alarms, CMM ships with a wizard that leads the user through
the definition process step by step. The wizard splits the task of creating alarm definitions into a
sequence of three chunks, each of which is presented on a separate page.

The page for defining an expression supports the user with comfortable features for building
complex expressions. Subexpressions can be added and connected with AND or OR operators.
Subexpressions can be removed, as required. They can also be reorganized within the
expression.

> **Note:** Restrictions apply to compound alarm definitions. Please refer to  [2 Restrictions](./2-restrictions.md#triggering-alarms-for-compound-alarm-definitions)
for details.

## 1.6 Deterministic Alarms

The `deterministic` property for alarm expressions avoids that an alarm status switches to
`UNDETERMINED` when no metrics data has been received.

CMM distinguishes between two types of metrics:

- Periodic metrics send data on a regular basis without interruption.
  In case of an interruption, i.e. there is no more metrics data for the agent to collect, the alarm
  state changes to `Undetermined`. This ensures that the monitoring user instantly notices that he
  needs to check why no more data is collected and sent.
- Sporadic metrics are not send on a regular basis.
  The data is sent only in certain cases, for example, if an error or warning is found in the log
  data. Expressions related to sporadic metrics can now be marked as `deterministic`. This
  avoids that the alarm state changes to `UNDETERMINED`.

By default, the `deterministic` property is not set for an alarm expression.


## 1.7 Notification Engine Plugin System

Monasca Ussuri comes with a plugin system for the Notification Engine. It facilitates the
development of plugins for additional notification methods, thus also allowing customers to
implement and configure their own notification methods as required.
CMM supports the following notification methods: `Email`, `PagerDuty` and `WebHook`.


## 1.8 Data Retention for the InfluxDB Database

The CMM Operator can configure data retention for the Metrics and Alarms Database. CMM uses
the data retention features offered by InfluxDB.

By default, metrics and alarm history data is automatically deleted from the database if it is older
than 31 days. This default is set with the installation of CMM. The CMM Operator can either
change the default when installing CMM, or update the data retention configuration at a later
stage.


## 1.9 Data Retention for the Elasticsearch Database

The CMM Operator can configure data retention for the Log Database. CMM uses Elasticsearch
Curator for managing data retention of Elasticsearch indices. Elasticsearch Curator jobs are
automatically run by a Cron daemon, a time-based job scheduler that executes commands
defined in a `crontab` configuration file. The file specifies shell commands for running jobs
periodically according to a given schedule.

By default, an Elasticsearch index is automatically deleted if it is older than 31 days. This default is
set with the installation of CMM. The CMM Operator can either change the default when installing
CMM, or update the data retention configuration at a later stage.


## 1.10 Areas of Expertise

CMM comes with expertise and know-how in the following areas. This enables product
customizations and solutions to meet specific customer requirements.


### Log Metrics Component

The Log Metrics component provides metrics for log data to system operators. These metrics
support CMM users in checking the severity of their log data.

Additional evaluations for log data can be prepared and configured by the system operator to
provide further types of metrics. If you want to customize the Log Metrics component, contact your
FUJITSU support organization for information.


### Nagios Plugins

The CMM Metrics Agent can run Nagios plugins and send status codes returned by the plugins as
metrics to the Monitoring API. Information on how to use Nagios checks in CMM can be obtained
from the FUJITSU support organizations.


## 1.11 CMM Components

This release of CMM is based on the Ussuri version of Monasca.

It is based on the following middleware components:

| CMM Component    | CMM 2.0     |
|------------------|-------------|
| Apache Kafka     | V2.11-2.0.11|
| Apache Storm     | V1.2.3      |
| Apache Zookeeper | V3.4.14     |
| Grafana          | V7.4.3      |
| Kibana           | V7.3.0      |
| Logstash         | V7.3.0      |
| Memcached        | 1.5-alpine  |

It is based on the following database components:

| CMM Component    | CMM 2.0    |
|------------------|------------|
| Elasticsearch    | V7.3.0     |
| InfluxDB         | V1.8-alpine |
| MySQL            | V5.7.34    |


## 1.12 System Environment


### Operating Systems

CMM can be installed on a host machine with the following operating systems:

- Red Hat Enterprise Linux 7.7 (for Intel64)


### Supported OpenStack Platforms

As underlying platform technology, the following OpenStack platforms are supported:

- Red Hat Enterprise Linux OpenStack Platform 16.1


### Supported Web Browsers

CMM has been tested with the following Web browsers:

- Google Chrome 90.
- Microsoft Edge 91.
- Mozilla Firefox 58.


## 1.13 Documentation

The following documentation is available for this release:

- _Overview:_ A manual introducing CMM. It is written for everybody interested in CMM.
- _System Operator's Guide:_ A manual for system operators describing how to install, operate,
  and maintain CMM. The manual also describes how to prepare the OpenStack platform for
  CMM and how to use the CMM monitoring functions.
- _Application Operator's Guide:_ A manual for application operators describing how CMM
  supports them in monitoring their services and virtual machines in OpenStack.
