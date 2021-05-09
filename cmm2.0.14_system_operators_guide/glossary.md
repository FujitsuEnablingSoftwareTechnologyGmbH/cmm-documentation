## Glossary


### Application Operator

A person responsible for providing services to end users or hosting services for development
activities. An application operator has limited access to cloud resources in OpenStack.


### Dimension

A key/value pair that allows for a flexible and concise description of the data to be monitored,
for example, region, availability zone, service tier, or resource ID. Each dimension describes a
specific characteristic of the metrics to be monitored.

In CMM, metrics are uniquely identified by a name and a set of dimensions. Dimensions can serve
as a filter for the monitoring data.


### Elasticsearch

An open-source application that provides a highly scalable full-text search and analytics engine.
CMM uses Elasticsearch as the underlying technology for storing, searching, and analyzing large
volumes of log data.


### Grafana

An open-source application for visualizing large-scale measurement data. CMM integrates with
Grafana for visualizing the monitoring data.


### InfluxDB

An open-source time-series database that supports high write loads and large data set storage.
CMM uses InfluxDB as the underlying technology for storing metrics and the alarm history.


### Infrastructure as a Service (IaaS)

The delivery of computer infrastructure (typically a platform virtualization environment) as a
service.


### Kibana

An open-source analytics and visualization platform designed to work with Elasticsearch. CMM
integrates with Kibana for visualizing the log data.


### Logstash

An open-source application that provides a data collection engine with pipelining capabilities.
CMM integrates with Logstash for collecting, processing, and outputting logs.


### MySQL

An open-source relational database that provides an SQL-compliant interface for accessing data.
CMM uses MySQL as the underlying technology for storing configuration information, alarm
definitions, and notification methods.

### Metrics

Self-describing data structures that allow for a flexible and concise description of the data to be
monitored. Metrics values represent the actual monitoring data that is collected and presented in
CMM.


### Monasca

An open-source Monitoring as a Service solution that integrates with OpenStack. It forms the core
of CMM.


### Monitoring Service Operator

A person responsible for maintaining and administrating CMM.


### OpenStack Operator

A person responsible for maintaining and administrating OpenStack, the underlying platform
technology of CMM.


### Platform as a Service (PaaS)

The delivery of a computing platform and solution stack as a service.


### Software as a Service (SaaS)

A model of software deployment where a provider licenses an application to customers for use as
a service on demand.
