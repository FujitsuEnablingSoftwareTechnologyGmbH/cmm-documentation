## About this Manual

This manual describes how service providers on OpenStack platforms can monitor their
applications with FUJITSU Software Cloud Monitoring Manager - hereafter referred to as Cloud
Monitoring Manager (CMM).

The manual is structured as follows:

| Chapter | Description |
|---------|-------------|
| What is CMM? | Introduces CMM, its key features, components, users, and possible add-ons. |
| Monitoring | Describes the basic concepts and features of monitoring. |
| Log Management | Describes the basic concepts and features of log management. |
| Glossary | Defines the central terms relevant for CMM. |


### Readers of this Manual

This manual is written for everybody interested in CMM. It offers an introduction for readers who
do not know CMM and for those who have already started using it. The manual does not require
any special knowledge.


### Notational Conventions

This manual uses the following notational conventions:

| Notation | Description |
|-----|---------------------------------------------|
| `Add` | Names of graphical user interface elements. |
| `init` | System names, for example command names and text that is entered from the keyboard. |
| `<variable>` | Variables for which values must be entered. |
| `[option]` | Optional items, for example optional command parameters. |
| `one \| two` | Alternative entries. |
| `{one \| two}` | Mandatory entries with alternatives. |

### Abbreviations

This manual uses the following abbreviations:

| Abbreviation | Description |
|-----|---------------------------------------------|
| `CMM` | Cloud Monitoring Manager |
| `IaaS` | Infrastructure as a Service |
| `ICMP` | Internet Control Message Protocol |
| `OS` | Operating System |
| `OSS` | Open Source Software |
| `PaaS` | Platform as a Service |
| `SaaS` | Software as a Service |


### Available Documentation

The following documentation on CMM is available:

- _Overview:_ A manual introducing CMM. It is written for everybody interested in CMM.
- _System Operator's Guide:_ A manual for system operators describing how to install, operate,
    and maintain CMM. The manual also describes how to prepare the OpenStack platform for
    CMM and how to use the CMM monitoring functions.
- _Application Operator's Guide:_ A manual for application operators describing how CMM
    supports them in monitoring their services and virtual machines in OpenStack.


### Related Information

The following links provide information on open-source offerings integrated with CMM:

- _OpenStack_ : Documentation on OpenStack, the underlying platform technology.
- _OpenStack Horizon_ : Documentation on the OpenStack Horizon dashboard.
- _Monasca_ : Information on Monasca, the core of CMM.
- _Grafana_ : Documentation on Grafana, the open-source application used for visualizing metrics
    data.
- _Kibana_ : Documentation on Kibana, the open-source application used for visualizing log data.

Links to more detailed information provided in this manual are subject to change without notice.


### Trademarks

LINUX is a registered trademark of Linus Torvalds.

The OpenStack Word Mark and OpenStack logo are registered trademarks/service marks or
trademarks/service marks of the OpenStack Foundation in the United States and other countries
and are used with the OpenStack Foundation's permission. FUJITSU LIMITED is not endorsed or
sponsored by the OpenStack Foundation, or the OpenStack community.

Red Hat is a trademark or a registered trademark of Red Hat Inc. in the United States and other
countries.

Java is a registered trademark of Oracle and/or its affiliates.

Python and PyCon are trademarks or registered trademarks of the Python Software Foundation.

Other company names and product names are trademarks or registered trademarks of their
respective owners.


### Copyright

Copyright FUJITSU ENABLING SOFTWARE TECHNOLOGY GMBH 2018

All rights reserved, including those of translation into other languages. No part of this manual may
be reproduced in any form whatsoever without the written permission of FUJITSU ENABLING
SOFTWARE TECHNOLOGY GMBH.


### High Risk Activity

The Customer acknowledges and agrees that the Product is designed, developed and
manufactured as contemplated for general use, including without limitation, general office use,
personal use, household use, and ordinary industrial use, but is not designed, developed and
manufactured as contemplated for use accompanying fatal risks or dangers that, unless extremely
high safety is secured, could lead directly to death, personal injury, severe physical damage or
other loss (hereinafter "High Safety Required Use"), including without limitation, nuclear reaction
control in nuclear facility, aircraft flight control, air traffic control, mass transport control, medical life
support system, missile launch control in weapon system. The Customer shall not use the Product
without securing the sufficient safety required for the High Safety Required Use. In addition,
FUJITSU (or other affiliate's name) shall not be liable against the Customer and/or any third party
for any claims or damages arising in connection with the High Safety Required Use of the Product.


### Export Restrictions

Exportation/release of this document may require necessary procedures in accordance with the
regulations of your resident country and/or US export control laws.
