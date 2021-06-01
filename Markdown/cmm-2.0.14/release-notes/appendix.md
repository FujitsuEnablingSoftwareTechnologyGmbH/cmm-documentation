## Appendix A: Open Source Software

The following Open Source Software (OSS) is included in and used by CMM. The list is restricted
to the major OSS projects that are relevant for CMM 2.0:

| Software              | Description                                   | License | Info |
|-----------------------|-----------------------------------------------|---------|-|
| Apache Kafka V0.9.0.1 | A distributed publish-subscribe messaging system. The CMM Message Queue is based on Kafka. | Apache 2.0 | [Info](https://archive.apache.org/dist/kafka/0.9.0.1/RELEASE_NOTES.html) |
| Apache Storm V1.1.1 | An open-source distributed real-time computation system for consuming streams of data and processing them in arbitrarily complex ways. The CMM Threshold Engine is based on Apache Storm. | Apache 2.0 | [Info](http://storm.apache.org/2017/08/01/storm111-released.html) |
| Apache Zookeeper V3.4.11 | A open-source service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. CMM uses Zookeeper for administrating the Message Queue. | Apache 2.0 | [Info](https://zookeeper.apache.org/doc/r3.4.11/releasenotes.html) |
| Elasticsearch V2.4.6 | An open-source application that provides a highly scalable full-text search and analytics engine. CMM uses Elasticsearch as the underlying technology for storing, searching, and analyzing log data. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/elasticsearch/reference/2.4/release-notes-2.4.6.html) |
| Grafana V4.5.2 | An open-source application for visualizing large-scale measurement data. CMM integrates with Grafana for visualizing the CMM monitoring data. |Apache 2.0 | [Info](https://github.com/grafana/grafana/releases/tag/v4.5.2) |
| InfluxDB V1.3.4 | An open-source database specifically designed to handle time series data with high availability and high performance requirements. CMM uses an InfluxDB database for storing metrics and the alarm history. | MIT | [Info](https://github.com/influxdata/influxdb/blob/v1.3.4/CHANGELOG.md) |
| Kibana V4.6.3 | An open-source analytics and visualization platform designed to work with Elasticsearch. CMM integrates with Kibana for visualizing the CMM log data. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/kibana/4.6/releasenotes.html) |
| Logstash V2.4.1 | An open-source application that provides a data collection engine with pipelining capabilities. CMM integrates with Logstash for collecting, processing and outputting logs. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/logstash/2.4/logstash-2-4-1.html) |
| Memcached 1.5.3 | An open-source distributed memory object caching system. CMM uses Memcached for dynamically alleviating the data load that is processed by the log management components. | BSD 3 | [Info](https://github.com/memcached/memcached/wiki/ReleaseNotes153) |
| MySQL V5.5 | Relational database system used by CMM for storing configuration information, alarm definitions, and notification methods. | GNU GPL V2 | [Info](https://dev.mysql.com/doc/relnotes/mysql/5.5/en/) |
