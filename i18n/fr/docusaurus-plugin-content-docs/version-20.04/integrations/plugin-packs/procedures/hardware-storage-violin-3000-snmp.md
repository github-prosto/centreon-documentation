---
id: hardware-storage-violin-3000-snmp
title: Violin Memory 3000
---

## Prerequisites

### Centreon Plugin

Install this plugin on each needed poller:

``` shell
yum install centreon-plugin-Hardware-Storage-Violin-3000-Snmp
```

Be sure to have with you the following information:

  - Read-Only SNMP community
  - IP Address of the equipment

### Configure SNMP on your server

Follow constructor procedure for your equipment.

### SNMP Permissions

Read-Only access.

### Troubleshooting

Read [Troubleshooting
SNMP](../tutorials/troubleshooting-plugins.html#snmp-checks).

## Centreon Configuration

### Create a host using the appropriate template

Go to *Configuration \> Hosts* and click *Add*. Then, fill the form as shown by
the following table:

| Field                                | Value                              |
| :----------------------------------- | :--------------------------------- |
| Host name                            | *Name of the host*                 |
| Alias                                | *Host description*                 |
| IP                                   | *Host IP Address*                  |
| Monitored from                       | *Monitoring Poller to use*         |
| Host Multiple Templates              | HW-Storage-Violin-3000-SNMP-custom |

Click on the *Save* button.