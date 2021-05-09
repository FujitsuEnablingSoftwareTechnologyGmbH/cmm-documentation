## 3 Preparations for Application Operators

Application operators who have booked a virtual machine in OpenStack can monitor their machine
with libvirt. Libvirt provides a comprehensive toolkit for managing virtual machines. The toolkit
includes checks for virtual machines that run on a hypervisor.
As an OpenStack operator, you have to prepare the monitoring environment for your application
operators. A Metrics Agent is required for monitoring the hypervisor on the Nova compute node
on which the virtual machines are provisioned. On behalf of the application operator, the agent
monitors the hypervisor on which it is installed as well as the provisioned virtual machines.
The following steps are required:

1. Create an OpenStack role for libvirt monitoring.
2. Install a Metrics Agent on the hypervisor where virtual machines are to be monitored for the
   application operators.
3. Configure the agent.

For additional information on libvirt monitoring, you can also refer to the _Monasca documentation_.


## 3.1 Creating an OpenStack Role

As a prerequisite for installing a Metrics Agent, you need to take the following preparations.

- Create the `monitoring-delegate` role in OpenStack Keystone.
  This role is required for cross-tenant metrics submission. An application operator who has
  booked a virtual machine must receive only the monitoring data related to his virtual machine.
  This role enables the agent to submit metrics on behalf of an individual application operator.
  
  Example command for creating the `monitoring-delegate` role:

```
openstack role create monitoring-delegate
```

- Assign the monitoring-delegate role to the OpenStack user you have created for
  authenticating an agent against OpenStack Keystone, for example, monasca-agent. The user
  name and password of this user must be specified in the agent configuration when the agent is
  installed. For details, refer to _Creating Projects, Users, and Roles_.
  
  Example command for assigning the `monitoring-delegate` role to the `monasca-agent` user:

```
openstack role add \
--project monasca \
--user monasca-agent monitoring-delegate
```


## 3.2 Installing the Metrics Agent

To enable monitoring for application operators, a Metrics Agent must be installed on the hypervisor
that hosts the virtual machines of the application operator.

Enter the credentials of the OpenStack user you want to use for libvirt monitoring in the agent
configuration. This user is used for the communication between the Monitoring Service and the
agent.

For details on installing a Metrics Agent, refer to _Installing a Metrics Agent on the OpenStack
Platform_.


## 3.3 Configuring the Metrics Agent

The installation of the Metrics Agent includes its initial configuration. To prepare the environment
for application operators, you have to reconfigure the agent. It is necessary to explicitly activate
the libvirt metrics that the application operators use for monitoring.
To reconfigure the agent, proceed as follows:

1. Activate the libvirt metrics. For details, refer to _Activating Additional Metrics_. For
   an example configuration, refer to the information on `libvirt.yml` in _Additional Metrics_.
2. Make sure that the host name specified for the `nova-compute` service is specified as value for
   the hostname parameter in the `agent.yaml` configuration file.
   For this purpose, check the host name for the `nova-compute` service in your environment first.
   You can execute the following command:

```
# nova service-list
```

   The `Host` column in the nova-compute line shows the host name for the `nova-compute` service
   in your environment.
3. To check the `hostname` parameter in the `agent.yaml` configuration file, open the file with your
   favorite editor.
   Example:

```
sudo vim /etc/monasca/agent/agent.yaml
```

4. If the `hostname` parameter does not correspond to the host name for the `nova-compute` service
   in your environment (see Step 2), update it.
5. To start the agent again, execute the following command:

```
sudo systemctl start monasca-agent.target
```

As soon as the agent is started again, it is available with the updated configuration settings. The
application operators can instantly use the libvirt metrics for monitoring.
