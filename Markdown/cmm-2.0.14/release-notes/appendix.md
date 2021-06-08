## Appendix A: Open Source Software

The following Open Source Software (OSS) is included in and used by CMM. The list is restricted
to the major OSS projects that are relevant for CMM 2.0:

| Software              | Description                                   | License | Info |
|-----------------------|-----------------------------------------------|---------|-|
| Apache Kafka V2.0.1 | A distributed publish-subscribe messaging system. The CMM Message Queue is based on Kafka. | Apache 2.0 | [Info](https://archive.apache.org/dist/kafka/2.0.1/RELEASE_NOTES.html) |
| Apache Storm V1.2.3 | An open-source distributed real-time computation system for consuming streams of data and processing them in arbitrarily complex ways. The CMM Threshold Engine is based on Apache Storm. | Apache 2.0 | [Info](http://storm.apache.org/2019/07/18/storm123-released.html) |
| Apache Zookeeper V3.4.14 | A open-source service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. CMM uses Zookeeper for administrating the Message Queue. | Apache 2.0 | [Info](https://zookeeper.apache.org/doc/r3.4.14/releasenotes.html) |
| Elasticsearch V7.3.0 | An open-source application that provides a highly scalable full-text search and analytics engine. CMM uses Elasticsearch as the underlying technology for storing, searching, and analyzing log data. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/elasticsearch/reference/7.3/release-notes-7.3.0.html) |
| Grafana V7.4.3 | An open-source application for visualizing large-scale measurement data. CMM integrates with Grafana for visualizing the CMM monitoring data. |Apache 2.0 | [Info](https://github.com/grafana/grafana/releases/tag/v7.4.3) |
| InfluxDB V1.8.5 | An open-source database specifically designed to handle time series data with high availability and high performance requirements. CMM uses an InfluxDB database for storing metrics and the alarm history. | MIT | [Info](https://docs.influxdata.com/influxdb/v1.8/about_the_project/releasenotes-changelog/) |
| Kibana V7.3.0 | An open-source analytics and visualization platform designed to work with Elasticsearch. CMM integrates with Kibana for visualizing the CMM log data. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/kibana/7.3/release-notes-7.3.0.html) |
| Logstash V7.3.0 | An open-source application that provides a data collection engine with pipelining capabilities. CMM integrates with Logstash for collecting, processing and outputting logs. | Apache 2.0 | [Info](https://www.elastic.co/guide/en/logstash/7.3/logstash-7-3-0.html) |
| Memcached V1.5.22 | An open-source distributed memory object caching system. CMM uses Memcached for dynamically alleviating the data load that is processed by the log management components. | BSD 3 | [Info](https://github.com/memcached/memcached/wiki/ReleaseNotes1522) |
| MySQL V5.7.34 | Relational database system used by CMM for storing configuration information, alarm definitions, and notification methods. | GNU GPL V2 w. FOSS Exception | [Info](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-34.html) |
| logstash-output-monasca_log_api V2.0.1 | Logstash Output Plugin to communicate with monasca-log-api | Apache 2.0 | [Info](https://github.com/logstash-plugins/logstash-output-monasca_log_api#readme) |
| logspout V3.2.13 | Log routing for Docker container logs | MIT |[Info](https://github.com/gliderlabs/logspout/tree/v3.2.13#readme) |
| cadvisor V0.33 | Analyzes resource usage and performance characteristics of running containers.| Apache 2.0 |[Info](https://github.com/google/cadvisor/tree/v0.33.0#readme) |
| elasticsearch-curator V5.8.3 | Elasticsearch Curator helps you curate, or manage, your Elasticsearch indices and snapshots. | Apache V2.0 | [Info](https://www.elastic.co/guide/en/elasticsearch/client/curator/current/index.html) |
| docker-ce V19.03-15-3 | Docker Engine is an open source containerization technology for building and containerizing your applications. | Apache 2.0 | [Info](https://docs.docker.com/engine/release-notes/19.03/#190315) |
| docker-compose V1.27.4 | Docker Compose is a tool for defining and running multi-container Docker applications. | Apache 2.0 | [Info](https://docs.docker.com/compose/release-notes/#1274)|

