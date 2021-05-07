# FUJITSU Software

# Cloud Monitoring Manager v2.0.13

# System Operator's Guide


## Contents

- [About this Manual](./about-this-manual.md#about-this-manual)
- [1 Introduction to CMM](./1-introduction-to-cmm.md#1-introduction-to-cmm)
  - [1.1 Basic Usage Scenario](./1-introduction-to-cmm.md#11-basic-usage-scenario)
  - [1.2 Architecture and Components](./1-introduction-to-cmm.md#12-architecture-and-components)
  - [1.3 User Management](./1-introduction-to-cmm.md#13-user-management)
  - [1.4 Distribution Media](./1-introduction-to-cmm.md#14-distribution-media)

- [2 Installation](./2-installation.md#2-installation)
  - [2.1 Prerequisites and Preparation](./2-installation.md#21-prerequisites-and-preparation)
    - [2.1.1 Hardware and Operating Systems](./2-installation.md#211-hardware-and-operating-systems)
    - [2.1.2 Web Browsers](./2-installation.md#211-hardware-and-operating-systems)
    - [2.1.3 Security](./2-installation.md#213-security)
  - [2.2 Preparing the OpenStack Integration](./2-installation.md#22-preparing-the-openstack-integration)
    - [2.2.1 Setting the Administrator Credentials](./2-installation.md#221-setting-the-administrator-credentials)
    - [2.2.2 Creating Projects, Users, and Roles](./2-installation.md#222-creating-projects-users-and-roles)
    - [2.2.3 Defining Services and Endpoints](./2-installation.md#223-defining-services-and-endpoints)
    - [2.2.4 Configuring the HTTP Proxy](./2-installation.md#224-configuring-the-http-proxy)
  - [2.3 Installing the Monitoring Service](./2-installation.md#23-installing-the-monitoring-service)
    - [2.3.1 Prerequisites](./2-installation.md#231-prerequisites)
    - [2.3.2 Installation](./2-installation.md#232-installation)
  - [2.4 Installing a Metrics Agent on the OpenStack Platform](./2-installation.md#24-installing-a-metrics-agent-on-the-openstack-platform)
    - [2.4.1 Installation](./2-installation.md#241-installation)
    - [2.4.2 Updating the Configuration File](./2-installation.md#242-updating-the-configuration-file)
    - [2.4.3 Activating Additional Metrics](./2-installation.md#243-activating-additional-metrics)
    - [2.4.4 Uninstallation](./2-installation.md#244-uninstallation)
  - [2.5 Installing a Log Agent on the OpenStack Platform](./2-installation.md#25-installing-a-log-agent-on-the-openstack-platform)
    - [2.5.1 Prerequisites](./2-installation.md#251-prerequisites)
    - [2.5.2 Installation](./2-installation.md#252-installation)
    - [2.5.3 Updating the Configuration File](./2-installation.md#253-updating-the-configuration-file)
    - [2.5.4 Uninstallation](./2-installation.md#254-uninstallation)
  - [2.6 Installing the Horizon Plugin](./2-installation.md#26-installing-the-horizon-plugin)
    - [2.6.1 Installation](./2-installation.md#261-installation)
    - [2.6.2 Configuration](./2-installation.md#262-configuration)
    - [2.6.3 Uninstallation](./2-installation.md#263-uninstallation)

- [3 Preparations for Application Operators](./3-preparations-for-application-operators.md#3-preparations-for-application-operators)
  - [3.1 Creating an OpenStack Role](./3-preparations-for-application-operators.md#31-creating-an-openstack-role)
  - [3.2 Installing the Metrics Agent](./3-preparations-for-application-operators.md#32-installing-the-metrics-agent)
  - [3.3 Configuring the Metrics Agent](./3-preparations-for-application-operators.md#33-configuring-the-metrics-agent)

- [4 Operation and Maintenance](./4-operation-and-maintenance.md#4-operation-and-maintenance)
  - [4.1 Managing Projects, Users, and Roles](./4-operation-and-maintenance.md#41-managing-projects-users-and-roles)
  - [4.2 Starting and Stopping Agents and Services](./4-operation-and-maintenance.md#42-starting-and-stopping-agents-and-services)
  - [4.3 Data Retention and Cleanup](./4-operation-and-maintenance.md#43-data-retention-and-cleanup)
    - [4.3.1 Disabling Metrics for a Metrics Agent on the OpenStack Platform](./4-operation-and-maintenance.md#431-disabling-metrics-for-a-metrics-agent-on-the-openstack-platform)
    - [4.3.2 Disabling Log Data for a Log Agent on the OpenStack Platform](./4-operation-and-maintenance.md#432-disabling-log-data-for-a-log-agent-on-the-openstack-platform)
    - [4.3.3 Configuring Metrics Data Retention](./4-operation-and-maintenance.md#433-configuring-metrics-data-retention)
    - [4.3.4 Configuring Log Data Retention](./4-operation-and-maintenance.md#434-configuring-log-data-retention)
    - [4.3.5 Removing Metrics Data](./4-operation-and-maintenance.md#435-removing-metrics-data)
    - [4.3.6 Removing Log Data](./4-operation-and-maintenance.md#436-removing-log-data)
  - [4.4 Log File Handling](./4-operation-and-maintenance.md#44-log-file-handling)
  - [4.5 Backup and Recovery](./4-operation-and-maintenance.md#45-backup-and-recovery)
    - [4.5.1 Databases](./4-operation-and-maintenance.md#451-databases)
    - [4.5.2 Dashboards](./4-operation-and-maintenance.md#452-dashboards)

- [5 Monitoring](./5-monitoring.md#5-monitoring)
  - [5.1 Overview](./5-monitoring.md#51-overview)
  - [5.2 Viewing Metrics Data](./5-monitoring.md#52-viewing-metrics-data)
  - [5.3 Defining Alarms](./5-monitoring.md#53-defining-alarms)
  - [5.4 Defining Notifications](./5-monitoring.md#54-defining-notifications)
  - [5.5 Status of Services, Servers, and Log Data](./5-monitoring.md#55-status-of-services-servers-and-log-data)

- [6 Log Management](./6-log-management.md#6-log-management)
  - [6.1 Working with the Log Management Window](./6-log-management.md#61-working-with-the-log-management-window)
  - [6.2 Configuring Index Patterns](./6-log-management.md#62-configuring-index-patterns)
  - [6.3 Monitoring Log Data](./6-log-management.md#63-monitoring-log-data)

- [Appendix A Supported Metrics](./appendix.md#appendix-a-supported-metrics)
  - [A.1 Standard Metrics](./appendix.md#a1-standard-metrics)
  - [A.2 Additional Metrics](./appendix.md#a2-additional-metrics)

- [Glossary](./glossary.md#glossary)
