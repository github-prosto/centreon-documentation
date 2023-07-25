---
id: migrate
title: Migrate the extension
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

> If you're updating to a new major or minor version (i.e:A.B.x with A
> or B that changes) you need to contact our Support service to retrieve
> the new repository.

## Update the package

In order to update the Centreon BAM module using an RPM package, execute the
following command:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
dnf update centreon-bam-server
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```shell
dnf update centreon-bam-server
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
apt update && apt upgrade centreon-bam-server
```

</TabItem>
</Tabs>

## Update through the interface

Log on to the Centreon web interface and go to
`Administration > Extension > Manager`.

Click on the orange button to update the module, do the same for the widget.