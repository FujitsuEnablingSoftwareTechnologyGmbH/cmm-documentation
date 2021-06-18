## Appendix A: Supported Metrics

The sections below describe the metrics supported by CMM:

- Standard metrics for general monitoring of servers and networks.
- Additional metrics for monitoring specific servers and services.

> **Note:** Adding dimensions for metrics is not supported by CMM. The installer auto-detects
  applications and processes that are running on your machine and saves the
  corresponding settings to the agent's configuration file. Additional dimensions cannot be
  specified.


## A.1 Standard Metrics

CMM supports the following standard metrics for monitoring servers and networks. These metrics
usually do not require specific settings. The metrics are grouped by metrics types. Each metrics
type references a set of related metrics.


### cpu.yaml

Metrics on CPU usage, e.g. the percentage of time the CPU is idle when no I/O requests are in
progress, or the percentage of time the CPU is used at system level or user level.


### disk.yaml

Metrics on disk space, e.g. the percentage of disk space that is used on a device, or the total
amount of disk space aggregated across all the disks on a particular node.


### load.yaml

Metrics on the average system load over different periods (e.g. 1 minute, 5 minutes, or 15
minutes).


### memory.yaml

Metrics on memory usage, e.g. the number of megabytes of total memory or free memory, or the
percentage of free swap memory.


### network.yaml

Metrics on the network, e.g. the number of network bytes received or sent per second, or the
number of network errors on incoming or outgoing network traffic per second.


## A.2 Additional Metrics

CMM supports the additional metrics described below for monitoring specific servers and services.
The metrics are grouped by metrics types. Each metrics type references a set of related metrics.
Depending on the services running on the host where you install a Metrics Agent, some or all of
these metrics are automatically added to the agent configuration. You should check the individual
yaml files and change or correct the settings as required, or remove individual `yaml` files from the
agent configuration if you do not want to monitor the metrics they include.

> **Note:** that in addition to the metrics below, many more metrics are provided by the Monasca
  project. These are not automatically installed by CMM. For details on the complete set of metrics
  provided by the Monasca project, refer to the _Monasca documentation_. If you want to extend your
  monitoring environment to perform additional checks, contact your FUJITSU support organization.


### apache.yaml

Apache Web Server checks collect metrics from an Apache Web Server. If you want the installer
to automatically configure the checks, update the `apache.cnf` file in the `root` directory before
installing the agent.

Example configuration for `apache.cnf` with the URL of the server, the user name, and the password:

```
[client]
url=http://localhost/server-status?auto
user=root
password=password
#dimensions:
    #dim1: value1
```

Specify the configuration information in the `apache.yaml` file after the installation.

Example configuration:

```
init_config: null
instances:
- apache_status_url: [http://localhost/server-status?auto](http://localhost/server-status?auto)
  apache_user: root
  apache_password: password
```


### ceph.yaml

Ceph checks provide information on one or more Ceph clusters. The configuration file must
specify the name of the cluster to be monitored. You can configure the agent so that only a
specific set of metrics data is collected.

As a prerequisite, the `ceph-common` package must be installed. In addition, the user running
the agent must have the permission to execute Ceph commands. For this purpose, assign
the `monasca-agent` user to the ceph group, and give read permission to the group in the
`ceph.client.admin.keyring` file:

```
usermod -a -G ceph monasca-agent chmod 0640 /etc/ceph/ceph.client.admin.keyring
```

Alternatively, you can configure `sudo` access for the `monasca-agent` user.

Example configuration with monasca-user assigned to the ceph group:

```
init_config: null
instances:
- cluster_name: ceph
  use_sudo: False
  collect_usage_metrics: True
  collect_stats_metrics: True
  collect_mon_metrics: True
  collect_osd_metrics: False
  collect_pool_metrics: True
```


### crash.yaml

Crash checks provide information on system crash dumps. The default directory where the crash
dumps are provided is `/var/crash`.

The agent installer automatically checks whether a crash kernel is loaded on the machine where
the agent is installed. If so, the detected settings are saved to the `crash.yaml` configuration file,
and the configuration is automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: Crash
  name: crash_stats
```


### elastic.yaml

Elastic checks gather metrics for Elasticsearch databases, such as the Log Database of CMM.
The configuration file must specify the URL for HTTP requests. If basic authentication is used, for
example `elasticsearch-http-basic`, the configuration file must also specify the user name and
password for every instance that requires authentication.

The agent installer automatically creates the `elastic.yaml` configuration file in the `/etc/
monasca/agent/conf.d/` directory. If there is an Elasticsearch database instance installed on
the machine where the agent is installed, you have to specify the configuration information in the
`elastic.yaml` file after the installation.

Example configuration:

```
init_config: null
instances:

- dimensions:
  component: elasticsearch
  service: monitoring
  url: [http://localhost:9200](http://localhost:9200)
  username: username
  password: password
```


### host_alive.yaml

Host alive checks perform checks on a remote host to determine whether it is alive. The checks
use either ping (ICMP) or SSH.

SSH checks provide extensive tests on the availability of remote host machines. They check the
banner that is returned. A remote host machine may still respond to a ping request but may not
return an SSH banner. Therefore it is recommended that you use SSH checks instead of ping
checks.

The agent installer automatically creates the `host_alive.yaml` configuration file in the
`/etc/monasca/agent/conf.d/` directory. If there are applications and processes running on the
machine where the agent is installed, you have to specify the configuration information in the
`host_alive.yaml` file after the installation.

Example configuration:

```
init_config:
  ssh_port:     22
  ssh_timeout:  0.5
  ping_timeout: 1
instances:
# - name: ssh to host1
#   host_name:     host1.domain.net
#   alive_test:    ssh
#   dimensions:
#     dim1: value1

# - name: ping host1
#   host_name:     10.140.16.153
#   alive_test:    ping

- name: ssh to 192.168.0.221
  host_name:     192.168.0.221
  alive_test:    ssh
```

### http_check.yaml

HTTP endpoint checks perform up/down checks on HTTP endpoints. Based on a list of URLs, the
agent sends an HTTP request and reports success or failure to the Monitoring Service.

The agent installer auto-detects HTTP endpoints on the machine where the agent is installed. It
saves the detected settings to the `http_check.yaml` configuration file, and the configuration is
automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: Cinder
  dimensions:
    service: block-storage
  collect_response_time: true
  match_pattern: .*version=[1-3].*
  name: block-storage-api
  timeout: 10
  url: http://localhost:8776/v2
  use_keystone: true
- built_by: Glance
  dimensions:
    service: image-service
  match_pattern: .*v2.0.*
  name: image-service-api
  timeout: 10
  url: http://localhost:9292
  use_keystone: true
```

### http_metrics.yaml

HTTP metrics checks retrieve metrics from any URL that returns a JSON response. Based on
a list of URLs, the agent can dispatch an HTTP request and parse the desired metrics from the
JSON response.

The agent installer auto-detects applications and processes on the machine where the agent
is installed. It saves the detected settings to the `http_metrics.yaml` configuration file, and the
configuration is automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: MonAPI
  dimensions:
  component: monasca-api
  service: monitoring
  name: monitoring-monasca-api metrics
  timeout: 5
  url: http://localhost:8081/metrics
  whitelist:
  - name: jvm.memory.total.max
    path: gauges/jvm.memory.total.max/value
    type: gauge
  - name: jvm.memory.total.used
    path: gauges/jvm.memory.total.used/value
    type: gauge
    - name: metrics.published
    path: meters/monasca.api.app.MetricService.metrics.published/count
    type: rate
```

### kafka_consumer.yaml

Kafka consumer checks gather metrics related to services consuming Kafka topics, such as the
Persister or Notification Engine of CMM.

For Kafka consumer checks, the Kafka consumer module (`kafka-python`) must be installed in
the virtualenv environment of the Metrics Agent. To install it in the default directory, execute the
following command:

```
# source /opt/monasca-agent/bin/activate
# pip install kafka-python
# deactivate
```

The agent installer automatically detects services that are consuming Kafka topics on the machine
where the agent is installed. If such services are detected, the corresponding settings are saved to
the `kafka_consumer.yaml` configuration file, and the configuration is automatically provided in the
`/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: Kafka
  consumer_groups:
    1_alarm-state-transitions:
      alarm-state-transitions: []
    1_metrics:
      metrics: []
    log-metric:
      transformed-log: []
    logstash-persister:
      transformed-log: []
    thresh-event:
      events: []
    thresh-metric:
      metrics: []
    transformer-logstash-consumer:
      log: []
  kafka_connect_str: 10.140.18.49:9092
  name: 10.140.18.49:9092
  per_partition: false
```

### kibana.yaml

Kibana checks gather metrics from a Kibana server. The checks access the status endpoint of
Kibana (`curl -XGET http://localhost:5601/api/status`). The configuration information in the
`kibana.yaml` file corresponds to the Kibana configuration.

The agent installer automatically checks whether a Kibana server instance is installed on the
machine where the agent is installed. If a Kibana server instance is detected, the corresponding
settings are saved to the `kibana.yaml` configuration file, and the configuration is automatically
provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config:
  url: http://10.140.18.49:5601/api/status
instances:
- built_by: Kibana
  metrics:
  - load
  - heap_size
  - heap_used
  - req_sec
  - resp_time_max
  - resp_time_avg
```

### libvirt.yaml

Libvirt checks provide metrics for virtual machines that run on a hypervisor. The checks provide a
set of metrics for the owner of the virtual machine as well as for the owner of the hypervisor. For
details on configuring the metrics, refer to the _Monasca documentation_.

Check the `keystone_authtoken` section in the `nova.conf` file for the `password`, `username`, and
`auth_url` configuration.

The user specified in the configuration file must be assigned the `admin` role.

Replace `<keystone_ip>` in the `libvirt.yaml.example` file by the IP address of the node on
which the OpenStack Keystone service is deployed. Example URL: `http://192.168.1.5:35357`.

With Red Hat Enterprise Linux OpenStack Platform as underlying platform technology, the
`project_name` must be set to `services`.

Example configuration:

```
init_config:
    password: pass
    project_name: services
    username: nova
    auth_url: 'http://<keystone_ip>:35357'
    endpoint_type: 'publicURL'
    cache_dir: /dev/shm
    nova_refresh: 14400
    vm_probation: 300
    ping_check: sudo -n /sbin/ip exec NAMESPACE /usr/bin/fping -n -c1 -t250 -q
    alive_only: false
    metadata:
    - scale_group
    customer_metadata:
    - scale_group
    network_use_bits: false
    vm_cpu_check_enable: True
    vm_disks_check_enable: True
    vm_extended_disks_check_enable: True
    vm_network_check_enable: True
    vm_ping_check_enable: True
    vm_extended_disks_check_enable: False
    host_aggregate_re: None
    disk_collection_period: 0
    vnic_collection_period: 0
instances:
- {}
```


### mysql.yaml

MySQL checks gather metrics from a MySQL database server. The metrics are related to the
server status variables of MySQL.

As a prerequisite, you need to find out the MySQL password credentials stored in 
`/root/.my.cnf` file inside the galera-bundle-podman container.

Run following commands:
```
podman exec -it galera-bundle-podman-0 /bin/sh
cat /root/.my.cnf
```

Example configuration for `/root/.my.cnf`:

```
[client]
user=root
password="FRjSTiKbzaq"

[mysql]
user=root
password="FRjSTiKbzaq"
```
Edit the file `mysql.yaml` in `/etc/monasca/agent/conf.d/` and insert the password as obtained before. 

> **Note:** Make sure that the password is set correctly. The agent installer fails if you specify the
  password enclosed in quotation marks.

In addition, the MySQL module (`PyMySQL`) must be installed in the virtualenv environment of the
Metrics Agent. To install it in the default directory, execute the following command:

```
# source /opt/monasca-agent/bin/activate
# pip install PyMySQL
# deactivate
```

Example configuration for `mysql.yaml`:

```
init_config: null
instances:
- built_by: MySQL
  name: localhost
  pass: FRjSTiKbzaq
  port: 3306
  server: localhost
  sock: /var/lib/mysql/mysql.sock
  ssl_ca: null
  ssl_cert: null
  ssl_key: null
  user: root
```


### ntp.yaml

Network Time Protocol checks monitor the time offset between the NTP server and the host
machine. The configuration file must specify the parameters that you want to monitor.

Example configuration:

```
init_config: null
instances:
- host: pool.ntp.org
  port: ntp
  version: 3
  timeout: 5
# dimensions:
#     dim1: value1
```

> **Note:** To collect the complete set of metrics from the NTP server and the host machine,
  it might additionally be required to update your NTP server configuration. Check whether
  changes resulting from an update are also required in the `ntp.yaml` file.

### ovs.yaml

Open vSwitch Neutron Router Monitoring checks monitor neutron virtual routers implemented with
OpenVSwitch. The checks include rate metrics as well as health-related metrics.

The agent installer automatically checks whether a neutron virtual router is installed on an
OpenStack host. If so, the detected settings are saved to the `ovs.yaml` configuration file, and the
configuration is automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config:
  admin_password: password
  admin_tenant_name: services
  admin_user: neutron
  cache_dir: /dev/shm
  identity_uri: http://10.140.18.53:35357/v2.0
  included_interface_re: qg.*|vhu.*|sg.*
  network_use_bits: false
  neutron_refresh: 14400
  ovs_cmd: sudo /usr/bin/ovs-vsctl
  region_name: RegionOne
  use_absolute_metrics: true
  use_health_metrics: true
  use_rate_metrics: true
instances: {}
```


### postfix.yaml

Postfix checks monitor a Postfix mail server. The agent installer automatically checks whether
a Postfix mail server instance is installed on the machine where the agent is installed. If so, the
detected settings are saved to the `postfix.yaml` configuration file, and the configuration is
automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: Postfix
  directory: /var/spool/postfix
  name: /var/spool/postfix
  queues:
  - incoming
  - active
  - deferred
```

### postgres.yaml

Postgres checks gather metrics from a PostgreSQL database.

For PostgreSQL checks, the `postgresql-devel` RPM package and the `psycopg2` Python
package are required. The Python package must be installed in the virtualenv environment of the
Metrics Agent. To install the packages in the default directory, execute the following command:

```
# yum install postgresql-devel
# source /opt/monasca-agent/bin/activate
# pip install psycopg2
# deactivate
```

Example configuration:

```
init_config: null
instances:
  - host: localhost
    port: 5432
    username: my_username
    password: my_password
    dbname: db_name
    relations:
  - my_table
  - my_other_table
```

### process.yaml

Process checks verify that a defined set of processes is up and running. The processes can be
identified by specifying the process name or a pattern match.

The agent installer auto-detects processes that are running on the machine where the agent
is installed. It saves the detected settings to the `process.yaml` configuration file, and the
configuration is automatically provided in the `/etc/monasca/agent/conf.d/` directory.

Example configuration:

```
init_config: null
instances:
- built_by: MySQL
  detailed: true
  dimensions:
    service: mysql
  exact_match: true
  name: mysqld
  search_string:
  - mysqld
- built_by: Nova
  detailed: true
  dimensions:
  component: nova-compute
  service: compute
  exact_match: false
  name: nova-compute
  search_string:
  - nova-compute
```

### rabbitmq.yaml

RabbitMQ checks gather metrics on nodes, exchanges, and queues from a RabbitMQ server.

As a prerequisite, you need to find out the RabbitMQ password credentials stored in
`/etc/rabbitmq/rabbitmq.config` file inside the rabbitmq-bundle-podman-0 container.

Run following commands:
```
podman exec -it rabbitmq-bundle-podman-0 /bin/sh
cat /etc/rabbitmq/rabbitmq.config

For RabbitMQ checks, the RabbitMQ Management plugin must be installed. It is included in the
RabbitMQ distribution. To enable the plugin, execute the following command:

```
rabbitmq-plugins enable rabbitmq_management
```

Specify the configuration information in the `rabbitmq.yaml` file after the installation.
Replace `<rabbitmq-user>` and `<rabbitmq-password>` with the current RabbitMQ user and
password. It must specify the names of the exchanges and queues to be monitored.

Example configuration:

```
init_config: null
instances:
-  rabbitmq_api_url: http://localhost:15672/api/
   rabbitmq_user: <rabbitmq-user>
   rabbitmq_pass: <rabbitmq-password>
   nodes:
    - rabbit@localhost
    - rabbit2@domain
   queues:
    - queue1
    - queue2
   whitelist:
     queue:
      - message_stats/deliver_details/rate
      - message_stats/publish_details/rate
      - message_stats/redeliver_details/rate
     exchange:
      - message_stats/publish_out
      - message_stats/publish_out_details/rate
      - message_stats/publish_in
      - message_stats/publish_in_details/rate
     node:
      - fd_used
      - mem_used
      - run_queue
      - sockets_used
```

> **Note:** To collect the complete set of metrics from the RabbitMQ server, it might additionally be
  required to update your RabbitMQ server configuration. Check whether changes resulting
  from an update are also required in the `rabbitmq.yaml` file.
