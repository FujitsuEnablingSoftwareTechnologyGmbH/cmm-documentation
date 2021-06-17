## 7 Uninstallation

The uninstallation of CMM and its OpenStack extensions comprises the following steps:

1. Uninstalling a Metrics Agent from an OpenStack node.
2. Uninstalling a Log Agent from an OpenStack node.
3. Uninstalling the Horizon Plugin from the node where the OpenStack Horizon service is
   deployed.
4. Uninstalling the Monitoring Service.
5. Removing the projects, users, and roles prepared for the OpenStack integration.
6. Removing the services and endpoints prepared for the Horizon Plugin in OpenStack Keystone.

## 7.1 Uninstalling a Metrics Agent

Before uninstalling a Metrics Agent from an OpenStack node, it is recommended that you make
a backup of the configuration files created for operation. The configuration files for an agent are
located in the `/etc/monasca/agent/` directory.

CMM does not offer integrated backup and recovery mechanisms. Use the standard file system
mechanisms instead.

To uninstall a Metrics Agent, proceed as follows:

1. Log in to the OpenStack node on which the agent is installed.
2. Stop the `monasca-agent` service and delete all related files:

```
systemctl stop monasca-agent.target
systemctl disable monasca-agent.target
rm -f /etc/systemd/system/monasca-agent.target
rm -f /etc/systemd/system/monasca-collector.service
rm -f /etc/systemd/system/monasca-forwarder.service
rm -f /etc/systemd/system/monasca-statsd.service
systemctl daemon-reload
systemctl reset-failed monasca-agent.target
```

3. Remove all directories and files created by the agent installer:

```
rm -rf /opt/monasca-agent/
rm -rf /etc/monasca/
rm -f /etc/sudoers.d/mon-agent
```

4. Remove the agent's log files and the log directory:

```
rm -rf /var/log/monasca-agent/
```

5. Remove the `mon-agent` user. Use -r to also remove the `mon-agent` user's home directory.

```
userdel -r mon-agent
```

## 7.2 Uninstalling a Log Agent

Before uninstalling a Log Agent from an OpenStack node, it is recommended that you make a
backup of the agent's configuration settings. They are stored in the
`/<installation_dir>/conf/agent.conf` file.

CMM does not offer integrated backup and recovery mechanisms. Use the standard file system
mechanisms instead.

To uninstall a Log Agent, proceed as follows:

1. Log in to the OpenStack node on which the agent is installed.
2. Stop the monasca-log-agent service and delete all related files:

```
systemctl stop monasca-log-agent
systemctl disable monasca-log-agent
rm -f /etc/systemd/system/monasca-log-agent.service
systemctl daemon-reload
systemctl reset-failed monasca-log-agent
```

3. Remove all directories and files created by the agent installer:

```
rm -rf <target_dir>
```

  Replace `<target_dir>` by the directory in which the agent is installed, (e.g.
  `/opt/monasca-log-agent/`).

4. Remove the agent's log files and the log directory:

```
rm -rf /var/log/monasca-log-agent/
```

5. Remove the Logstash script used for defining the position of monitored log files:

```
rm -f /etc/profile.d/logstash_sincedb_dir.sh
```


## 7.3 Uninstalling the Horizon Plugin (Monasca-UI)

To uninstall the Horizon Plugin (Monasca-UI), proceed as follows:

1. Log in as root to the OpenStack node on which the OpenStack Horizon service is installed.
2. Enter into Horizon container:
```
# podman exec -it horizon /bin/sh
```

3. Remove monasca-ui directories:
```
$ rm -rf /opt/monasca-ui/
$ rm -rf /usr/share/openstack-dashboard/static/monitoring
```

4. Uninstall monasca-ui and python-monascaclient:
```
$ python3.6 -m pip uninstall monasca-ui python-monascaclient
```

> **Note:** If the japanese translations were installed, remove this directory: \
> `rm -rf /usr/local/lib/python3.6/site-packages/monitoring`

5. Remove the symbolic links:
```
$ rm /etc/openstack-dashboard/monitoring_policy.json
$ rm /usr/share/openstack-dashboard/openstack_dashboard/local/enabled/_50_admin_add_monitoring_panel.py
$ rm /usr/share/openstack-dashboard/openstack_dashboard/local/local_settings.d/_50_monasca_ui_settings.py
```

6. Update Django settings:
```
$ python3 /usr/share/openstack-dashboard/manage.py collectstatic --noinput
$ python3 /usr/share/openstack-dashboard/manage.py compress --force
```

> **Note:** Expected messages: \
> `WARNING:root:"dashboards" and "default_dashboard" in (local_)settings is DEPRECATED` \
> `ERROR:scss.ast:Function not found: twbs-font-path:1` \
> `ERROR:scss.compiler:Mixin not found: dropdown-arrow:0` \
> `ERROR:scss.compiler:Maximum number of supported selectors in Internet Explorer (4095) exceeded!`


7. Exit from Horizon container:
```
$ exit
```

8. Remove Proxy Modules from file httpd.conf. Location of file:\
`/var/lib/config-data/puppet-generated/horizon/etc/httpd/conf/httpd.conf`

Remove these lines:
```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
```

9. Remove the Proxy configuration inside VirtualHost section in 10-horizon_vhost.conf. Location of file:\
`/var/lib/config-data/puppet-generated/horizon/etc/httpd/conf.d/10-horizon_vhost.conf`

Remove these lines:
```
  ProxyPass        "/grafana" "http://<CMM-SERVER-IP>:3000"
  ProxyPassReverse "/grafana" "http://<CMM-SERVER-IP>:3000"
```

10. Restart Horizon container:
```
# systemctl restart tripleo_horizon
```


## 7.4 Uninstalling the Monitoring Service

To uninstall the Monitoring Service, proceed as follows:

1. Log in to the CMM node as a user with root privileges.
2. Go to the installation directory.
3. To stop all agents and services and remove the containers, the instances of the docker images,
   and any volumes you mounted for CMM, `run docker-compose down` as follows:

```
docker-compose -f docker-compose-metric.yml \
-f docker-compose-log.yml down --rmi all --volumes
```

> **Note:** When running the command, you can ignore warnings about images to be removed not being found. The messages are written because some images
  are used twice, for setting up Kafka for the metrics pipeline as well as for the log pipeline.
  Irrespective of these messages, all docker images are successfully removed.

4. Delete the `docker-compose` file in the `/usr/local/bin/` directory:

```
rm -f /usr/local/bin/docker-compose
```

5. Delete the installation directory of the Monitoring Service to which you extracted the
   `CMM_server_2.0.14-x.tar.gz` archive file from the CMM installation package:

```
rm -rf <path_to_installation_directory>
```

6. Remove the volume you mounted for the data directories of Elasticsearch, InfluxDB, MySQL,
   Kafka, and Grafana. Example with the default volume:

```
rm -rf /opt/monasca-containers/
```

7. Remove the volume you mounted for backing up the databases. Example with the default volume:

```
rm -rf /mount/backup/
```

## 7.5 Removing OpenStack Projects, Users, and Roles

To integrate CMM with the OpenStack Keystone service, you created a project, a user, and two
roles in OpenStack.

To remove them from your OpenStack environment, proceed as follows:

1. Provide the administrator credentials that are required to perform any action in OpenStack
   Keystone. For details, refer to _Setting the Administrator Credentials_.
2. Remove the OpenStack project that was used for the monitoring data retrieved for CMM and
   your OpenStack services and servers. Example with `monasca` as project name:

```
openstack project delete monasca
```

3. Remove the OpenStack user that was used for authenticating an agent against OpenStack
   Keystone. Example with `monasca-agent` as user name:

```
openstack user delete monasca-agent
```

4. Remove the OpenStack roles that were prepared.
   Example with `monasca-user` and `monasca-agent` as role names:

```
openstack role delete monasca-user
openstack role delete monasca-agent
```

## 7.6 Removing Services and Endpoints

For the Horizon Plugin, you defined a set of services and endpoints in OpenStack Keystone.
To remove the services and endpoints from your OpenStack environment, proceed as follows:

1. Provide the administrator credentials that are required to perform any action in OpenStack
   Keystone. For details, refer to Setting the _Administrator Credentials_.

2. For removing the endpoints, you need to know the endpoint IDs:

```
openstack endpoint list | grep monasca
openstack endpoint list | grep logs
```

3. Remove the endpoints as follows:

```
openstack endpoint delete <endpoint-id1> <endpoint-id2>
```

   Replace `<endpoint-id1>` and `<endpoint-id2>` by the endpoints of the two services.

4. Remove the services as follows:

```
openstack service delete monasca logs
```
