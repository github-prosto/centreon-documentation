---
id: hardware-storage-hitachi-hnas-snmp
title: Hitachi NAS SNMP
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Pack assets

### Templates

The Monitoring Connector **Hitachi NAS** brings a host template:

* **HW-Storage-Hitachi-Hnas-SNMP-custom**

The connector brings the following service templates (sorted by the host template they are attached to):

<Tabs groupId="sync">
<TabItem value="HW-Storage-Hitachi-Hnas-SNMP-custom" label="HW-Storage-Hitachi-Hnas-SNMP-custom">

| Service Alias       | Service Template                                        | Service Description |
|:--------------------|:--------------------------------------------------------|:--------------------|
| Hardware-Global     | HW-Storage-Hitachi-Hnas-Hardware-Global-SNMP-custom     | Check all hardware  |
| Volume-Usage-Global | HW-Storage-Hitachi-Hnas-Volume-Usage-Global-SNMP-custom | Check volume usages |

> The services listed above are created automatically when the **HW-Storage-Hitachi-Hnas-SNMP-custom** host template is used.

</TabItem>
<TabItem value="Not attached to a host template" label="Not attached to a host template">

| Service Alias          | Service Template                                           | Service Description          | Discovery  |
|:-----------------------|:-----------------------------------------------------------|:-----------------------------|:----------:|
| Cluster-Status         | HW-Storage-Hitachi-Hnas-Cluster-Status-SNMP-custom         | Check cluster nodes status   |            |
| Interfaces             | HW-Storage-Hitachi-Hnas-Interfaces-SNMP-custom             | Check interfaces             | X          |
| Virtual-Volumes-Quotas | HW-Storage-Hitachi-Hnas-Virtual-Volumes-Quotas-SNMP-custom | Check virtual volumes quotas |            |

> The services listed above are not created automatically when a host template is applied. To use them, [create a service manually](/docs/monitoring/basic-objects/services), then apply the service template you want.

> If **Discovery** is checked, it means a service discovery rule exists for this service template.

</TabItem>
</Tabs>

### Discovery rules

#### Service discovery

| Rule name                                   | Description                                               |
|:--------------------------------------------|:----------------------------------------------------------|
| HW-Storage-Hitachi-Hnas-SNMP-Interface-Name | Discover the disk partitions and monitor space occupation |

More information about discovering services automatically is available on the [dedicated page](/docs/monitoring/discovery/services-discovery)
and in the [following chapter](/docs/monitoring/discovery/services-discovery/#discovery-rules).

### Collected metrics & status

Here is the list of services for this connector, detailing all metrics linked to each service.

<Tabs groupId="sync">
<TabItem value="Cluster-Status" label="Cluster-Status">

| Metric name | Unit  |
|:------------|:------|
| node#status | N/A   |

> To obtain this new metric format, include **--use-new-perfdata** in the **EXTRAOPTIONS** service macro.

</TabItem>
<TabItem value="Hardware-Global" label="Hardware-Global">

| Metric Name                                       | Unit  |
|:--------------------------------------------------|:------|
| battery status                                    | rpm   |
| fan status                                        | C     |
| *node_name~fan_id*#hardware.fan.speed.rpm         |       |
| power supply status                               |       |
| system drive status                               |       |
| temperature status                                |       |
| *node_name~probe_id*#hardware.temperature.celsius |       |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Metric name                             | Unit  |
|:----------------------------------------|:------|
| int#status                              | N/A   |
| int#interface.traffic.in.bitspersecond  | b/s   |
| int#interface.traffic.out.bitspersecond | b/s   |
| int#interface.packets.in.discard.count  | count |
| int#interface.packets.in.error.count    | count |
| int#interface.packets.out.discard.count | count |
| int#interface.packets.out.error.count   | count |

</TabItem>
<TabItem value="Virtual-Volumes-Quotas" label="Virtual-Volumes-Quotas">

| Metric name                               | Unit  |
|:------------------------------------------|:------|
| virtual_volumes.quotas.detected.count     | count |
| vvq#virtual_volume.quota.usage.bytes      | B     |
| vvq#virtual_volume.quota.free.bytes       | B     |
| vvq#virtual_volume.quota.usage.percentage | %     |
| vvq#virtual_volume.quota.files.count      | count |
| vvq#virtual_volume.quota.files.free.count | count |
| vvq#virtual_volume.quota.files.percentage | %     |

</TabItem>
<TabItem value="Volume-Usage-Global" label="Volume-Usage-Global">

| Metric name   | Unit  |
|:--------------|:------|
| volume#status | N/A   |
| volume#usage  | N/A   |

</TabItem>
</Tabs>

## Prerequisites

### SNMP Configuration

To use this pack, the SNMP service must be properly configured on your ressource.
Please refer to the official documentation from Hitachi.

### Network flow

The target server must be reachable from the Centreon poller on the UDP/161
SNMP port.

## Installing the monitoring connector

### Pack

1. If the platform uses an *online* license, you can skip the package installation
instruction below as it is not required to have the connector displayed within the
**Configuration > Monitoring Connectors Manager** menu.
If the platform uses an *offline* license, install the package on the **central server**
with the command corresponding to the operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-hardware-storage-hitachi-hnas-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-hardware-storage-hitachi-hnas-snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-hardware-storage-hitachi-hnas-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-hardware-storage-hitachi-hnas-snmp
```

</TabItem>
</Tabs>

2. Whatever the license type (*online* or *offline*), install the **Hitachi NAS** connector through
the **Configuration > Monitoring Connectors Manager** menu.

### Plugin

Since Centreon 22.04, you can benefit from the 'Automatic plugin installation' feature.
When this feature is enabled, you can skip the installation part below.

You still have to manually install the plugin on the poller(s) when:
- Automatic plugin installation is turned off
- You want to run a discovery job from a poller that doesn't monitor any resource of this kind yet

> More information in the [Installing the plugin](/docs/monitoring/pluginpacks/#installing-the-plugin) section.

Use the commands below according to your operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Hardware-Storage-Hitachi-Hnas-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Hardware-Storage-Hitachi-Hnas-Snmp
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-hardware-storage-hitachi-hnas-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Hardware-Storage-Hitachi-Hnas-Snmp
```

</TabItem>
</Tabs>

## Using the monitoring connector

### Using a host template provided by the connector

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill the **Name**, **Alias** & **IP Address/DNS** fields according to your ressource settings.
3. Apply the **HW-Storage-Hitachi-Hnas-SNMP-custom** template to the host. 

> When using SNMP v3, use the **SNMPEXTRAOPTIONS** macro to add specific authentication parameters.
> More information in the [Troubleshooting SNMP](../getting-started/how-to-guides/troubleshooting-plugins.md#snmpv3-options-mapping) section.

| Macro            | Description                                                                                           | Default value     | Mandatory   |
|:-----------------|:------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SNMPEXTRAOPTIONS | Any extra option you may want to add to every command (E.g. a --verbose flag). All options are listed [here](#available-options) |                   |             |

4. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The host appears in the list of hosts, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the host: it shows the values of the macros.

### Using a service template provided by the connector

1. If you have used a host template and checked **Create Services linked to the Template too**, the services linked to the template have been created automatically, using the corresponding service templates. Otherwise, [create manually the services you want](/docs/monitoring/basic-objects/services) and apply a service template to them.
2. Fill in the macros you want (e.g. to change the thresholds for the alerts). Some macros are mandatory (see the table below).

<Tabs groupId="sync">
<TabItem value="Cluster-Status" label="Cluster-Status">

| Macro          | Description                                                                                                                                                 | Default value          | Mandatory   |
|:---------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------|:-----------:|
| UNKNOWNSTATUS  | Define the conditions to match for the status to be UNKNOWN (Default: '%{state} =~ /unknown/'). You can use the following variables: %{state}, %{display}   | %{state} =~ /unknown/  |             |
| FILTERNAME     | Filter node name (can be a regexp)                                                                                                                          |                        |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (Default: '%{state} =~ /offline/i'). You can use the following variables: %{state}, %{display} | %{state} =~ /offline/i |             |
| WARNINGSTATUS  | Define the conditions to match for the status to be WARNING (Default: -). You can use the following variables: %{state}, %{display}                         |                        |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (E.g. a --verbose flag). All options are listed [here](#available-options)                                                         | --verbose              |             |

</TabItem>
<TabItem value="Hardware-Global" label="Hardware-Global">

| Macro        | Description                                                                                          | Default value     | Mandatory   |
|:-------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| COMPONENT    | Which component to check (Default: '.*'). Can be: 'temperature', 'fan', 'psu', 'sysdrive', 'battery' |                   |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (E.g. a --verbose flag). All options are listed [here](#available-options)  | --verbose         |             |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Macro              | Description                                                                                                                                                                                                         | Default value                                         | Mandatory   |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------|:-----------:|
| OIDFILTER          | Define the OID to be used to filter interfaces (default: ifDesc) (values: ifDesc, ifAlias, ifName, IpAddr)                                                                                                          | ifdesc                                                |             |
| OIDDISPLAY         | Define the OID that will be used to name the interfaces (default: ifDesc) (values: ifDesc, ifAlias, ifName, IpAddr)                                                                                                 | ifdesc                                                |             |
| INTERFACENAME      | Set the interface (number expected) ex: 1,2,... (empty means 'check all interfaces')                                                                                                                                |                                                       |             |
| WARNINGINDISCARD   | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALINDISCARD  | Thresholds                                                                                                                                                                                                          |                                                       |             |
| WARNINGINERROR     | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALINERROR    | Thresholds                                                                                                                                                                                                          |                                                       |             |
| WARNINGINTRAFFIC   | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALINTRAFFIC  | Thresholds                                                                                                                                                                                                          |                                                       |             |
| WARNINGOUTDISCARD  | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALOUTDISCARD | Thresholds                                                                                                                                                                                                          |                                                       |             |
| WARNINGOUTERROR    | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALOUTERROR   | Thresholds                                                                                                                                                                                                          |                                                       |             |
| WARNINGOUTTRAFFIC  | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALOUTTRAFFIC | Thresholds                                                                                                                                                                                                          |                                                       |             |
| CRITICALSTATUS     | Define the conditions to match for the status to be CRITICAL (Default: '%{admstatus} eq "up" and %{opstatus} ne "up"'). You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display} | %{admstatus} eq "up" and %{opstatus} !~ /up\|dormant/ |             |
| WARNINGSTATUS      | Define the conditions to match for the status to be WARNING. You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                                                            |                                                       |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (E.g. a --verbose flag). All options are listed [here](#available-options)                                                                                                                 | --verbose                                             |             |

</TabItem>
<TabItem value="Virtual-Volumes-Quotas" label="Virtual-Volumes-Quotas">

| Macro                | Description                                                                                         | Default value     | Mandatory   |
|:---------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERVOLUMENAME     | Filter virtual volumes quota by volume name                                                         |                   |             |
| FILTERTARGET         | Filter virtual volumes quota by target                                                              |                   |             |
| FILTERFILESYSTEMNAME |                                                                                                     |                   |             |
| WARNINGVVQDETECTED   | Thresholds                                                                                          |                   |             |
| CRITICALVVQDETECTED  | Thresholds                                                                                          |                   |             |
| WARNINGVVQFILES      | Thresholds                                                                                          |                   |             |
| CRITICALVVQFILES     | Thresholds                                                                                          |                   |             |
| WARNINGVVQFILESFREE  | Thresholds                                                                                          |                   |             |
| CRITICALVVQFILESFREE | Thresholds                                                                                          |                   |             |
| WARNINGVVQFILESPRCT  | Thresholds                                                                                          |                   |             |
| CRITICALVVQFILESPRCT | Thresholds                                                                                          |                   |             |
| WARNINGVVQUSAGE      | Thresholds                                                                                          |                   |             |
| CRITICALVVQUSAGE     | Thresholds                                                                                          |                   |             |
| WARNINGVVQUSAGEFREE  | Thresholds                                                                                          |                   |             |
| CRITICALVVQUSAGEFREE | Thresholds                                                                                          |                   |             |
| WARNINGVVQUSAGEPRCT  | Thresholds                                                                                          |                   |             |
| CRITICALVVQUSAGEPRCT | Thresholds                                                                                          |                   |             |
| EXTRAOPTIONS         | Any extra option you may want to add to the command (E.g. a --verbose flag). All options are listed [here](#available-options) | --verbose         |             |

</TabItem>
<TabItem value="Volume-Usage-Global" label="Volume-Usage-Global">

| Macro          | Description                                                                                                                                                        | Default value                 | Mandatory   |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------|:-----------:|
| FILTERNAME     | Filter volume name (can be a regexp)                                                                                                                               |                               |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (Default: -). You can use the following variables: %{status}, %{display}                              | %{status} =~ /needsChecking/i |             |
| WARNINGSTATUS  | Define the conditions to match for the status to be WARNING (Default: '%{status} =~ /needsChecking/i'). You can use the following variables: %{status}, %{display} |                               |             |
| WARNINGUSAGE   | Thresholds                                                                                                                                                         |                               |             |
| CRITICALUSAGE  | Thresholds                                                                                                                                                         |                               |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (E.g. a --verbose flag). All options are listed [here](#available-options)                                                                | --verbose                     |             |

</TabItem>
</Tabs>

3. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The service appears in the list of services, and on page **Resources Status**. The command that is sent by the connector is displayed in the details panel of the service: it shows the values of the macros.

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`). Test that the connector 
is able to monitor a server using a command like this one (replace the sample values by yours):

```bash
/usr/lib/centreon/plugins//centreon_hitachi_hnas_snmp.pl \
	--plugin=storage::hitachi::hnas::snmp::plugin \
	--mode=volume-usage \
	--hostname='10.0.0.1' \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community'  \
	--filter-name='' \
	--warning-status='' \
	--critical-status='%{status} =~ /needsChecking/i' \
	--warning-usage='' \
	--critical-usage='' \
	--verbose\
	
```

The expected command output is shown below:

```bash
OK:   | 

```

### Troubleshooting

Please find the [troubleshooting documentation](../getting-started/how-to-guides/troubleshooting-plugins.md)
for Centreon Plugins typical issues.

### Available modes

In most cases, a mode corresponds to a service template. The mode appears in the execution command for the connector.
In the Centreon interface, you don't need to specify a mode explicitly: its use is implied when you apply a service template.
However, you will need to specify the correct mode for the template if you want to test the execution command for the 
connector in your terminal.

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins//centreon_hitachi_hnas_snmp.pl \
	--plugin=storage::hitachi::hnas::snmp::plugin \
	--list-mode
```

The plugin brings the following modes:

| Mode                                                                                                                                                     | Linked service template                                    |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------|
| cluster-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/clusterstatus.pm)]                | HW-Storage-Hitachi-Hnas-Cluster-Status-SNMP-custom         |
| hardware [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/hardware.pm)]                           | HW-Storage-Hitachi-Hnas-Hardware-Global-SNMP-custom        |
| interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/interfaces.pm)]                       | HW-Storage-Hitachi-Hnas-Interfaces-SNMP-custom             |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/listinterfaces.pm)]              | Used for service discovery                                 |
| list-volumes [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/listvolumes.pm)]                    | Not used in this Monitoring Connector                      |
| virtual-volumes-quotas [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/virtualvolumesquotas.pm)] | HW-Storage-Hitachi-Hnas-Virtual-Volumes-Quotas-SNMP-custom |
| volume-usage [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/centreon/common/bluearc/snmp/mode/volumeusage.pm)]                    | HW-Storage-Hitachi-Hnas-Volume-Usage-Global-SNMP-custom    |

### Available options

#### Generic options

All generic options are listed here:

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --mode                                     | Define the mode in which you want the plugin to be executed (see--list-mode).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --dyn-mode                                 | Specify a mode with the module's path (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --list-mode                                | List all available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --version                                  | Return the version of the plugin.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --pass-manager                             | Define the password manager you want to use. Supported managers are: environment, file, keepass, hashicorpvault and teampass.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --verbose                                  | Display extended status information (long output).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --debug                                    | Display debug messages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --filter-perfdata                          | Filter perfdata that match the regexp. Eg: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-perfdata-adv                      | Filter perfdata based on a "if" condition using the following variables: label, value, unit, warning, critical, min, max. Variables must be written either %{variable} or %(variable). Eg: adding --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")' will remove all metrics whose value equals 0 and that don't have a maximum value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --explode-perfdata-max                     | Create a new metric for each metric that comes with a maximum limit. The new metric will be named identically with a '\_max' suffix). Eg: it will split 'used\_prct'=26.93%;0:80;0:90;0;100 into 'used\_prct'=26.93%;0:80;0:90;0;100 'used\_prct\_max'=100%;;;;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata=free,used,invert()      Convert storage free perfdata into used:     --change-perfdata=used,free,invert()      Scale traffic values automatically:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()                                                                                                                                                                                                                                                                                                                                                                          |
| --extend-perfdata-group                    | Add new aggregated metrics (min, max, average or sum) for groups of metrics defined by a regex match on the metrics' names. Syntax: --extend-perfdata-group=regex,namesofnewmetrics,calculation\[,\[ne wuom\],\[min\],\[max\]\] regex: regular expression namesofnewmetrics: how the new metrics' names are composed (can use $1, $2... for groups defined by () in regex). calculation: how the values of the new metrics should be calculated newuom (optional): unit of measure for the new metrics min (optional): lowest value the metrics can reach max (optional): highest value the metrics can reach  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'   |
| --change-short-output --change-long-output | Modify the short/long output that is returned by the plugin. Syntax: --change-short-output=pattern~replacement~modifier Most commonly used modifiers are i (case insensitive) and g (replace all occurrences). Eg: adding --change-short-output='OK~Up~gi' will replace all occurrences of 'OK', 'ok', 'Ok' or 'oK' with 'Up'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --change-exit                              | Replace an exit code with one of your choice. Eg: adding --change-exit=unknown=critical will result in a CRITICAL state instead of an UNKNOWN state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --range-perfdata                           | Rewrite the ranges displayed in the perfdata. Accepted values: 0: nothing is changed. 1: if the lower value of the range is equal to 0, it is removed. 2: remove the thresholds from the perfdata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-uom                               | Mask the units when they don't match the given regular expression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --opt-exit                                 | Replace the exit code in case of an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc). Default: unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-ignore-perfdata                   | Remove all the metrics from the service. The service will still have a status and an output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --output-ignore-label                      | Remove the status label ("OK:", "WARNING:", "UNKNOWN:", CRITICAL:") from the beginning of the output. Eg: 'OK: Ram Total:...' will become 'Ram Total:...'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-xml                               | Return the output in XML format (to send to an XML API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --output-json                              | Return the output in JSON format (to send to a JSON API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-openmetrics                       | Return the output in OpenMetrics format (to send to a tool expecting this format).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). E.g.: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-format                             | Applies only to modes beginning with 'list-'. Returns the list of available macros to configure a service discovery rule (formatted in XML).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-show                               | Applies only to modes beginning with 'list-'. Returns the list of discovered objects (formatted in XML) for service discovery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --float-precision                          | Define the float precision for thresholds (default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --hostname                                 | Name or address of the host to monitor (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --snmp-community                           | SNMP community (default value: public). It is recommended to use a read-only community.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-version                             | Version of the SNMP protocol. 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --snmp-port                                | UDP port to send the SNMP request to (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-timeout                             | Time to wait before sending the request again if no reply has been received, in seconds (default: 1). See also --snmp-retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-retries                             | Maximum number of retries (default: 5).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --subsetleef                               | How many OID values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-autoreduce                          | Progressively reduce the number of requested OIDs in bulk mode. Use it in case of SNMP errors (By default, the number is divided by 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-force-getnext                       | Use SNMP getnext function in SNMP v2c and v3. This will request one OID at a time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --snmp-cache-file                          | Use SNMP cache file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-username                            | SNMP v3 only: User name (securityName).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --authpassphrase                           | SNMP v3 only: Pass phrase hashed using the authentication protocol defined in the --authprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --authprotocol                             | SNMP v3 only: Authentication protocol: MD5\|SHA. Since net-snmp 5.9.1: SHA224\|SHA256\|SHA384\|SHA512.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --privpassphrase                           | SNMP v3 only: Privacy pass phrase (privPassword) to encrypt messages using the protocol defined in the --privprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --privprotocol                             | SNMP v3 only: Privacy protocol (privProtocol) used to encrypt messages. Supported protocols are: DES\|AES and since net-snmp 5.9.1: AES192\|AES192C\|AES256\|AES256C.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --contextname                              | SNMP v3 only: Context name (contextName), if relevant for the monitored host.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --contextengineid                          | SNMP v3 only: Context engine ID (contextEngineID), if relevant for the monitored host, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --securityengineid                         | SNMP v3 only: Security engine ID, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --snmp-errors-exit                         | Expected status in case of SNMP error or timeout. Possible values are warning, critical and unknown (default).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-tls-transport                       | Transport protocol for TLS communication (can be: 'dtlsudp', 'tlstcp').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-our-identity                    | X.509 certificate to identify ourselves. Can be the path to the certificate file or its contents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --snmp-tls-their-identity                  | X.509 certificate to identify the remote host. Can be the path to the certificate file or its contents. This option is unnecessary if the certificate is already trusted by your system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-tls-their-hostname                  | Common Name (CN) expected in the certificate sent by the host if it differs from the value of the --hostname parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-trust-cert                      | A trusted CA certificate used to verify a remote host's certificate. If you use this option, you must also define --snmp-tls-their-hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

#### Modes options

All available options for each service template are listed below:

<Tabs groupId="sync">
<TabItem value="Cluster-Status" label="Cluster-Status">

| Option            | Description                                                                                                                                                    |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-name     | Filter node name (can be a regexp).                                                                                                                            |
| --unknown-status  | Define the conditions to match for the status to be UNKNOWN (Default: '%{state} =~ /unknown/'). You can use the following variables: %{state}, %{display}      |
| --warning-status  | Define the conditions to match for the status to be WARNING (Default: -). You can use the following variables: %{state}, %{display}                            |
| --critical-status | Define the conditions to match for the status to be CRITICAL (Default: '%{state} =~ /offline/i'). You can use the following variables: %{state}, %{display}    |

</TabItem>
<TabItem value="Hardware-Global" label="Hardware-Global">

| Option               | Description                                                                                                                                                                                                             |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --component          | Which component to check (Default: '.*'). Can be: 'temperature', 'fan', 'psu', 'sysdrive', 'battery'.                                                                                                                   |
| --filter             | Exclude the items given as a comma-separated list (example: --filter=sysdrive). You can also exclude items from specific instances: --filter=sysdrive,1                                                                 |
| --no-component       | Define the expected status if no components are found (default: critical).                                                                                                                                              |
| --threshold-overload | Use this option to override the status returned by the plugin when the status label matches a regular expression (syntax: section,\[instance,\]status,regexp). Example: --threshold-overload='sysdrive,OK,formatting'   |
| --warning            | Set warning threshold (syntax: type,regexp,threshold) Example: --warning='temperature,.*,30'                                                                                                                            |
| --critical           | Set critical threshold (syntax: type,regexp,threshold) Example: --critical='temperature,.*,40'                                                                                                                          |

</TabItem>
<TabItem value="Interfaces" label="Interfaces">

| Option                   | Description                                                                                                                                                                                                                                                                                |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached              | Memcached server to use (only one server).                                                                                                                                                                                                                                                 |
| --redis-server           | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                                                                            |
| --redis-attribute        | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                    |
| --redis-db               | Set Redis database index.                                                                                                                                                                                                                                                                  |
| --failback-file          | Failback on a local file if redis connection failed.                                                                                                                                                                                                                                       |
| --memexpiration          | Time to keep data in seconds (Default: 86400).                                                                                                                                                                                                                                             |
| --statefile-dir          | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                     |
| --statefile-suffix       | Define a suffix to customize the statefile name (Default: '').                                                                                                                                                                                                                             |
| --statefile-concat-cwd   | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.                                                |
| --statefile-format       | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                                                                      |
| --statefile-key          | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                                                               |
| --statefile-cipher       | Define the cipher algorithm to encrypt the cache (Default: 'AES').                                                                                                                                                                                                                         |
| --add-global             | Check global port statistics (By default if no --add-* option is set).                                                                                                                                                                                                                     |
| --add-status             | Check interface status.                                                                                                                                                                                                                                                                    |
| --add-duplex-status      | Check duplex status (with --warning-status and --critical-status).                                                                                                                                                                                                                         |
| --add-traffic            | Check interface traffic.                                                                                                                                                                                                                                                                   |
| --add-errors             | Check interface errors.                                                                                                                                                                                                                                                                    |
| --add-cast               | Check interface cast.                                                                                                                                                                                                                                                                      |
| --add-speed              | Check interface speed.                                                                                                                                                                                                                                                                     |
| --add-volume             | Check interface data volume between two checks (not supposed to be graphed, useful for BI reporting).                                                                                                                                                                                      |
| --check-metrics          | If the expression is true, metrics are checked (Default: '%{opstatus} eq "up"').                                                                                                                                                                                                           |
| --warning-status         | Define the conditions to match for the status to be WARNING. You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                                                                                                                                   |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (Default: '%{admstatus} eq "up" and %{opstatus} ne "up"'). You can use the following variables: %{admstatus}, %{opstatus}, %{duplexstatus}, %{display}                                                                        |
| --warning-* --critical-* | Thresholds. Can be: 'total-port', 'total-admin-up', 'total-admin-down', 'total-oper-up', 'total-oper-down', 'in-traffic', 'out-traffic', 'in-error', 'in-discard', 'out-error', 'out-discard', 'in-ucast', 'in-bcast', 'in-mcast', 'out-ucast', 'out-bcast', 'out-mcast', 'speed' (b/s).   |
| --units-traffic          | Units of thresholds for the traffic (Default: 'percent\_delta') ('percent\_delta', 'bps', 'counter').                                                                                                                                                                                      |
| --units-errors           | Units of thresholds for errors/discards (Default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                          |
| --units-cast             | Units of thresholds for communication types (Default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                      |
| --nagvis-perfdata        | Display traffic perfdata to be compatible with nagvis widget.                                                                                                                                                                                                                              |
| --interface              | Set the interface (number expected) ex: 1,2,... (empty means 'check all interfaces').                                                                                                                                                                                                      |
| --name                   | Allows you to define the interface (in option --interface) byname instead of OID index. The name matching mode supports regular expressions.                                                                                                                                               |
| --speed                  | Set interface speed for incoming/outgoing traffic (in Mb).                                                                                                                                                                                                                                 |
| --speed-in               | Set interface speed for incoming traffic (in Mb).                                                                                                                                                                                                                                          |
| --speed-out              | Set interface speed for outgoing traffic (in Mb).                                                                                                                                                                                                                                          |
| --map-speed-dsl          | Get interface speed configuration for interface type 'adsl' and 'vdsl2'.  Syntax: --map-speed-dsl=interface-src-name,interface-dsl-name  E.g: --map-speed-dsl=Et0.835,Et0-vdsl2                                                                                                            |
| --force-counters64       | Force to use 64 bits counters only. Can be used to improve performance.                                                                                                                                                                                                                    |
| --force-counters32       | Force to use 32 bits counters (even in snmp v2c and v3). Should be used when 64 bits counters are buggy.                                                                                                                                                                                   |
| --reload-cache-time      | Time in minutes before reloading cache file (default: 180).                                                                                                                                                                                                                                |
| --oid-filter             | Define the OID to be used to filter interfaces (default: ifDesc) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                |
| --oid-display            | Define the OID that will be used to name the interfaces (default: ifDesc) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                       |
| --oid-extra-display      | Add an OID to display.                                                                                                                                                                                                                                                                     |
| --display-transform-src  | Regexp src to transform display value.                                                                                                                                                                                                                                                     |
| --display-transform-dst  | Regexp dst to transform display value.                                                                                                                                                                                                                                                     |
| --show-cache             | Display cache interface datas.                                                                                                                                                                                                                                                             |

</TabItem>
<TabItem value="Virtual-Volumes-Quotas" label="Virtual-Volumes-Quotas">

| Option                    | Description                                                                                                                              |
|:--------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| --filter-filesystem-label | Filter virtual volume quota by filesystem label.                                                                                         |
| --filter-volume-name      | Filter virtual volumes quota by volume name.                                                                                             |
| --filter-target           | Filter virtual volumes quota by target.                                                                                                  |
| --warning-* --critical-*  | Thresholds. Can be: 'vvq-detected', 'vvq-usage', 'vvq-usage-free', 'vvq-usage-prct', 'vvq-files', 'vvq-files-free', 'vvq-files-prct'.    |

</TabItem>
<TabItem value="Volume-Usage-Global" label="Volume-Usage-Global">

| Option                   | Description                                                                                                                                                          |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='^status$'                                                                               |
| --filter-name            | Filter volume name (can be a regexp).                                                                                                                                |
| --warning-status         | Define the conditions to match for the status to be WARNING (Default: '%{status} =~ /needsChecking/i'). You can use the following variables: %{status}, %{display}   |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (Default: -). You can use the following variables: %{status}, %{display}                                |
| --warning-* --critical-* | Thresholds. Can be: 'usage'.                                                                                                                                         |
| --units                  | Units of thresholds (Default: '%') ('%', 'B').                                                                                                                       |
| --free                   | Thresholds are on free space left.                                                                                                                                   |

</TabItem>
</Tabs>

All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins//centreon_hitachi_hnas_snmp.pl \
	--plugin=storage::hitachi::hnas::snmp::plugin \
	--mode=volume-usage \
	--help
```
