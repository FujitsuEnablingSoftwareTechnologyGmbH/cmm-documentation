# FUJITSU Software

# Cloud Monitoring Manager v2.0.14-x

# System Operator's Guide


## Contents

- [About this Manual](./about-this-manual.md#about-this-manual)
- [1 Introduction to CMM](./1-introduction-to-cmm.md#1-introduction-to-cmm)
  - [1.1 Basic Usage Scenario](./1-introduction-to-cmm.md#11-basic-usage-scenario)
  - [1.2 Architecture and Components](./1-introduction-to-cmm.md#12-architecture-and-components)
  - [1.3 User Management](./1-introduction-to-cmm.md#13-user-management)
  - [1.4 Distribution Media](./1-introduction-to-cmm.md#14-distribution-media)

- [2 Installation](2-installation.md#2-installation)
  - [2.1 Prerequisites and Preparation](./2-installation.md#21-prerequisites-and-preparation)
    - [2.1.1 Hardware and Operating Systems](./2-installation.md#211-hardware-and-operating-systems)
    - [2.1.2 Web Browsers](./2-installation.md#212-web-browsers)
    - [2.1.3 Security](./2-installation.md#213-security)
    - [2.1.4 Software Prerequisites](./2-installation.md#214-software-prerequisites)
  - [2.2 Preparing the OpenStack Integration](./2-installation.md#22-preparing-the-openstack-integration)
    - [2.2.1 Setting the Administrator Credentials](./2-installation.md#221-setting-the-administrator-credentials)
    - [2.2.2 Creating Projects, Users, and Roles](./2-installation.md#222-creating-projects-users-and-roles)
    - [2.2.3 Defining Services and Endpoints](./2-installation.md#223-defining-services-and-endpoints)
  - [2.3 Installing the Monitoring Service](./2-installation.md#23-installing-the-monitoring-service)
    - [2.3.1 Prerequisites](./2-installation.md#231-prerequisites)
    - [2.3.2 Installation](./2-installation.md#232-installation)
  - [2.4 Metrics Agent on the OpenStack Platform](./2-installation.md#24-metrics-agent-on-the-openstack-platform)
    - [2.4.1 Metric Agent Installation](./2-installation.md#241-metric-agent-installation)
    - [2.4.2 Metric Agent Updating the Configuration File](./2-installation.md#242-metric-agent-updating-the-configuration-file)
    - [2.4.3 Activating Additional Metrics](./2-installation.md#243-activating-additional-metrics)
    - [2.4.4 Metric Agent Uninstallation](./2-installation.md#244-metric-agent-uninstallation)
  - [2.5 Log Agent on the OpenStack Platform](./2-installation.md#25-log-agent-on-the-openstack-platform)
    - [2.5.1 Log Agent Prerequisites](./2-installation.md#251-log-agent-prerequisites)
    - [2.5.2 Log Agent Installation](./2-installation.md#252-log-agent-installation)
    - [2.5.3 Log Agent Updating the Configuration File](./2-installation.md#253-log-agent-updating-the-configuration-file)
    - [2.5.4 Log Agent Uninstallation](./2-installation.md#254-log-agent-uninstallation)
  - [2.6 Horizon Plugin (Monasca-UI)](./2-installation.md#26-horizon-plugin-monasca-ui)
    - [2.6.1 Horizon Plugin (Monasca-UI) Installation and Configuration](./2-installation.md#261-horizon-plugin-monasca-ui-installation-and-configuration)
    - [2.6.2 Horizon Plugin (Monasca-UI) Uninstallation](./2-installation.md#262-horizon-plugin-monasca-ui-uninstallation)

- [3 Preparations for Application Operators](./3-preparations-for-application-operators.md#3-preparations-for-application-operators)
  - [3.1 Creating an OpenStack Role](./3-preparations-for-application-operators.md#31-creating-an-openstack-role)
  - [3.2 Installing the Metrics Agent](./3-preparations-for-application-operators.md#32-installing-the-metrics-agent)
  - [3.3 Configuring the Metrics Agent](./3-preparations-for-application-operators.md#33-configuring-the-metrics-agent)

- [Appendix A Supported Metrics](./appendix.md#appendix-a-supported-metrics)
  - [A.1 Standard Metrics](./appendix.md#a1-standard-metrics)
  - [A.2 Additional Metrics](./appendix.md#a2-additional-metrics)

- [Glossary](./glossary.md#glossary)
