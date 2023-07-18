---
id: cloud-azure-network-appgateway
title: Azure Application Gateway
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Contenu du pack

### Modèles

Le connecteur de supervision **Azure Application Gateway** apporte 2 modèles d'hôte :

* **Cloud-Azure-Network-AppGateway-V1-custom**
* **Cloud-Azure-Network-AppGateway-V2-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="Cloud-Azure-Network-AppGateway-V1-custom" label="Cloud-Azure-Network-AppGateway-V1-custom">

| Alias          | Modèle de service                                        | Description                                                               |
|:---------------|:---------------------------------------------------------|:--------------------------------------------------------------------------|
| Backend-Health | Cloud-Azure-Network-AppGateway-Backend-Health-Api-custom | Contrôle la disponibilité des hôtes backends Azure Application Gateway v1 |
| Connections    | Cloud-Azure-Network-AppGateway-Connections-Api-custom    | Contrôle les connexions aux ressources Azure Application Gateway          |
| Health         | Cloud-Azure-Network-AppGateway-Health-Api-custom         | Contrôle la santé des ressources Azure Application Gateway                |
| Requests       | Cloud-Azure-Network-AppGateway-Requests-Api-custom       | Contrôle les requêtes des ressources Azure Application Gateway            |
| Throughput     | Cloud-Azure-Network-AppGateway-Throughput-Api-custom     | Contrôle le transit des ressources Azure Application Gateway              |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **Cloud-Azure-Network-AppGateway-V1-custom** est utilisé.

</TabItem>
<TabItem value="Cloud-Azure-Network-AppGateway-V2-custom" label="Cloud-Azure-Network-AppGateway-V2-custom">

| Alias           | Modèle de service                                         | Description                                                           |
|:----------------|:----------------------------------------------------------|:----------------------------------------------------------------------|
| Backend-Status  | Cloud-Azure-Network-AppGateway-Backend-Status-Api-custom  | Contrôle le statut des backends Azure Application Gateway             |
| Backend-Time    | Cloud-Azure-Network-AppGateway-Backend-Time-Api-custom    | Contrôle le temps de réponse des backends Azure Application Gateway   |
| Clients-Traffic | Cloud-Azure-Network-AppGateway-Clients-Traffic-Api-custom | Contrôle le trafic client des ressources Azure Application Gateway    |
| Connections     | Cloud-Azure-Network-AppGateway-Connections-Api-custom     | Contrôle les connexions aux ressources Azure Application Gateway      |
| Gateway-Time    | Cloud-Azure-Network-AppGateway-Gateway-Time-Api-custom    | Contrôle le temps de réponse des ressources Azure Application Gateway |
| Health          | Cloud-Azure-Network-AppGateway-Health-Api-custom          | Contrôle la santé des ressources Azure Application Gateway            |
| Requests        | Cloud-Azure-Network-AppGateway-Requests-Api-custom        | Contrôle les requêtes des ressources Azure Application Gateway        |
| Throughput      | Cloud-Azure-Network-AppGateway-Throughput-Api-custom      | Contrôle le transit des ressources Azure Application Gateway          |
| Units           | Cloud-Azure-Network-AppGateway-Units-Api-custom           | Contrôle les unités des ressources Azure Application Gateway          |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **Cloud-Azure-Network-AppGateway-V2-custom** est utilisé.

</TabItem>
</Tabs>

### Règles de découverte

#### Découverte d'hôtes

Le connecteur de supervision Centreon **Azure Application Gateway** inclut un fournisseur de découverte
d'hôtes nommé **Microsoft Azure Application Gateway**. Celui-ci permet de découvrir l'ensemble des instances
rattachées à une souscription Microsoft Azure donnée et de les ajouter à la liste des hôtes supervisés.

> Cette découverte n'est compatible qu'avec le [mode **api**. Le mode **azcli**](../getting-started/how-to-guides/azure-credential-configuration.md) n'est pas supporté dans le cadre
> de cette utilisation.

Rendez-vous sur la documentation dédiée pour en savoir plus sur la [découverte automatique d'hôtes](/docs/monitoring/discovery/hosts-discovery).

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Backend-Health" label="Backend-Health">

| Métrique                                | Unité |
|:----------------------------------------|:------|
| appgateway.backend.unhealthy.host.count | count |
| appgateway.backend.healthy.host.count   | count |

</TabItem>
<TabItem value="Backend-Status" label="Backend-Status">

| Métrique                                 | Unité |
|:-----------------------------------------|:------|
| appgateway.backend.response.status.count | count |

</TabItem>
<TabItem value="Backend-Time" label="Backend-Time">

| Métrique                                               | Unité |
|:-------------------------------------------------------|:------|
| appgateway.backend.connect.time.milliseconds           | ms    |
| appgateway.backend.firstbyte.responsetime.milliseconds | ms    |
| appgateway.backend.lastbyte.responsetime.milliseconds  | ms    |

</TabItem>
<TabItem value="Clients-Traffic" label="Clients-Traffic">

| Métrique                                  | Unité |
|:------------------------------------------|:------|
| appgateway.traffic.clients.received.bytes | B     |
| appgateway.traffic.clients.sent.bytes     | B     |

</TabItem>
<TabItem value="Connections" label="Connections">

| Métrique                                     | Unité |
|:---------------------------------------------|:------|
| appgateway.backend.connections.current.count | count |

</TabItem>
<TabItem value="Gateway-Time" label="Gateway-Time">

| Métrique                           | Unité |
|:-----------------------------------|:------|
| appgateway.time.total.milliseconds | ms    |

</TabItem>
<TabItem value="Health" label="Health">

| Métrique    | Unité |
|:------------|:------|
| status      | N/A   |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Requests" label="Requests">

| Métrique                         | Unité |
|:---------------------------------|:------|
| appgateway.requests.failed.count | count |
| appgateway.requests.total.count  | count |

</TabItem>
<TabItem value="Throughput" label="Throughput">

| Métrique                             | Unité |
|:-------------------------------------|:------|
| appgateway.throughput.bytespersecond | B/s   |

</TabItem>
<TabItem value="Units" label="Units">

| Métrique                                | Unité |
|:----------------------------------------|:------|
| appgateway.capacity.units.count         | count |
| appgateway.compute.units.count          | count |
| appgateway.billed.units.estimated.count | count |
| appgateway.billable.units.fixed.count   | count |

</TabItem>
</Tabs>

## Prérequis

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/azure-credential-configuration.md) afin d'obtenir
les prérequis nécessaires pour interroger les API d'Azure.

## Installer le connecteur de supervision

### Pack

1. Si la plateforme est configurée avec une licence *online*, l'installation d'un paquet
n'est pas requise pour voir apparaître le connecteur dans le menu **Configuration > Gestionnaire de connecteurs de supervision**.
Au contraire, si la plateforme utilise une licence *offline*, installez le paquet
sur le **serveur central** via la commande correspondant au gestionnaire de paquets
associé à sa distribution :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-cloud-azure-network-appgateway
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-cloud-azure-network-appgateway
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-cloud-azure-network-appgateway
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-cloud-azure-network-appgateway
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Azure Application Gateway**
depuis l'interface web et le menu **Configuration > Gestionnaire de connecteurs de supervision**.

### Plugin

À partir de Centreon 22.04, il est possible de demander le déploiement automatique
du plugin lors de l'utilisation d'un connecteur. Si cette fonctionnalité est activée, et
que vous ne souhaitez pas découvrir des éléments pour la première fois, alors cette
étape n'est pas requise.

> Plus d'informations dans la section [Installer le plugin](/docs/monitoring/pluginpacks/#installer-le-plugin).

Utilisez les commandes ci-dessous en fonction du gestionnaire de paquets de votre système d'exploitation :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Cloud-Azure-Network-AppGateway-Api
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Cloud-Azure-Network-AppGateway-Api
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-cloud-azure-network-appgateway-api
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Cloud-Azure-Network-AppGateway-Api
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

<Tabs groupId="sync">
<TabItem value="Cloud-Azure-Network-AppGateway-V1-custom" label="Cloud-Azure-Network-AppGateway-V1-custom">

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Remplissez le champ **Adresse IP/DNS** avec l'adresse **127.0.0.1**.
3. Appliquez le modèle d'hôte **Cloud-Azure-Network-AppGateway-V1-custom**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.
4. Renseignez les macros désirées. Attention, certaines macros sont obligatoires. Par exemple, pour ce connecteur, **AZURECUSTOMMODE** (valeurs possibles : **api** ou **azcli**). En effet, il existe plusieurs modes de communication avec l'équipement supervisé : soit l'outil en ligne de commande azcli, soit une interrogation directe de l'api.

<Tabs groupId="sync">
<TabItem value="Azure Monitor API" label="Azure Monitor API">

| Macro              | Description                                                                                                                       | Valeur par défaut | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| AZURECLIENTID      | Set Azure client ID                                                                                                               |                   | X           |
| AZURECLIENTSECRET  | Set Azure client secret                                                                                                           |                   | X           |
| AZURECUSTOMMODE    | When a plugin offers several ways (CLI, library, etc.) to get the an information the desired one must be defined with this option | api               |             |
| AZURERESOURCE      | Set resource name or id (Required)                                                                                                |                   |             |
| AZURERESOURCEGROUP | Set resource group (Required if resource's name is used)                                                                          |                   | X           |
| AZURERESOURCETYPE  |                                                                                                                                   |                   |             |
| AZURESUBSCRIPTION  | Set Azure subscription (Required if logged to several subscriptions)                                                              |                   | X           |
| AZURETENANT        | Set Azure tenant ID                                                                                                               |                   | X           |
| PROXYURL           | Proxy URL if any                                                                                                                  |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to every command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                             |                   |             |

</TabItem>
<TabItem value="Azure AZ CLI" label="Azure AZ CLI">

| Macro              | Description                                                                                                                       | Valeur par défaut | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| AZURECUSTOMMODE    | When a plugin offers several ways (CLI, library, etc.) to get the an information the desired one must be defined with this option | api               |             |
| AZURERESOURCE      | Set resource name or id (Required)                                                                                                |                   |             |
| AZURERESOURCEGROUP | Set resource group (Required if resource's name is used)                                                                          |                   | X           |
| AZURERESOURCETYPE  |                                                                                                                                   |                   |             |
| AZURESUBSCRIPTION  | Set Azure subscription (Required if logged to several subscriptions)                                                              |                   | X           |
| PROXYURL           | Proxy URL if any                                                                                                                  |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to every command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                             |                   |             |

</TabItem>
</Tabs>

> Deux méthodes peuvent être utilisées pour définir l'authentification :
>
> * Utilisation de l'ID complet de la ressource (de type `/subscriptions/<subscription_id>/resourceGroups/<resourcegroup_id>/providers/XXXXXX/XXXXXXX/<resource_name>`) dans la macro **AZURERESOURCE**.
> * Utilisation du nom de la ressource dans la macro **AZURERESOURCE** et du nom du groupe de ressources dans la macro **AZURERESOURCEGROUP**.

5. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

</TabItem>
<TabItem value="Cloud-Azure-Network-AppGateway-V2-custom" label="Cloud-Azure-Network-AppGateway-V2-custom">

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Remplissez le champ **Adresse IP/DNS** avec l'adresse **127.0.0.1**.
3. Appliquez le modèle d'hôte **Cloud-Azure-Network-AppGateway-V2-custom**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.
4. Renseignez les macros désirées. Attention, certaines macros sont obligatoires. Par exemple, pour ce connecteur, **AZURECUSTOMMODE** (valeurs possibles : **api** ou **azcli**). En effet, il existe plusieurs modes de communication avec l'équipement supervisé : soit l'outil en ligne de commande azcli, soit une interrogation directe de l'api.

<Tabs groupId="sync">
<TabItem value="Azure Monitor API" label="Azure Monitor API">

| Macro              | Description                                                                                                                       | Valeur par défaut | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| AZURECLIENTID      | Set Azure client ID                                                                                                               |                   | X           |
| AZURECLIENTSECRET  | Set Azure client secret                                                                                                           |                   | X           |
| AZURECUSTOMMODE    | When a plugin offers several ways (CLI, library, etc.) to get the an information the desired one must be defined with this option | api               |             |
| AZURERESOURCE      | Set resource name or id (Required)                                                                                                |                   |             |
| AZURERESOURCEGROUP | Set resource group (Required if resource's name is used)                                                                          |                   | X           |
| AZURERESOURCETYPE  |                                                                                                                                   |                   |             |
| AZURESUBSCRIPTION  | Set Azure subscription (Required if logged to several subscriptions)                                                              |                   | X           |
| AZURETENANT        | Set Azure tenant ID                                                                                                               |                   | X           |
| PROXYURL           | Proxy URL if any                                                                                                                  |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to every command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                             |                   |             |

</TabItem>
<TabItem value="Azure AZ CLI" label="Azure AZ CLI">

| Macro              | Description                                                                                                                       | Valeur par défaut | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| AZURECUSTOMMODE    | When a plugin offers several ways (CLI, library, etc.) to get the an information the desired one must be defined with this option | api               |             |
| AZURERESOURCE      | Set resource name or id (Required)                                                                                                |                   |             |
| AZURERESOURCEGROUP | Set resource group (Required if resource's name is used)                                                                          |                   | X           |
| AZURERESOURCETYPE  |                                                                                                                                   |                   |             |
| AZURESUBSCRIPTION  | Set Azure subscription (Required if logged to several subscriptions)                                                              |                   | X           |
| PROXYURL           | Proxy URL if any                                                                                                                  |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to every command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                             |                   |             |

</TabItem>
</Tabs>

> Deux méthodes peuvent être utilisées pour définir l'authentification :
>
> * Utilisation de l'ID complet de la ressource (de type `/subscriptions/<subscription_id>/resourceGroups/<resourcegroup_id>/providers/XXXXXX/XXXXXXX/<resource_name>`) dans la macro **AZURERESOURCE**.
> * Utilisation du nom de la ressource dans la macro **AZURERESOURCE** et du nom du groupe de ressources dans la macro **AZURERESOURCEGROUP**.

5. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

</TabItem>
</Tabs>

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Backend-Health" label="Backend-Health">

| Macro                      | Description                                                                                         | Valeur par défaut | Obligatoire |
|:---------------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME                  |                                                                                                     | 900               |             |
| INTERVAL                   |                                                                                                     | PT5M              |             |
| AGGREGATION                |                                                                                                     | Average           |             |
| FILTERMETRIC               |                                                                                                     |                   |             |
| FILTERDIMENSION            |                                                                                                     |                   |             |
| WARNINGHEALTHYHOSTCOUNT    |                                                                                                     |                   |             |
| CRITICALHEALTHYHOSTCOUNT   |                                                                                                     |                   |             |
| WARNINGUNHEALTHYHOSTCOUNT  |                                                                                                     |                   |             |
| CRITICALUNHEALTHYHOSTCOUNT |                                                                                                     |                   |             |
| EXTRAOPTIONS               | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Backend-Status" label="Backend-Status">

| Macro                  | Description                                                                                         | Valeur par défaut | Obligatoire |
|:-----------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME              |                                                                                                     | 900               |             |
| INTERVAL               |                                                                                                     | PT5M              |             |
| AGGREGATION            |                                                                                                     | Total             |             |
| FILTERMETRIC           |                                                                                                     |                   |             |
| FILTERDIMENSION        |                                                                                                     |                   |             |
| WARNINGRESPONSESTATUS  | Warning threshold                                                                                   |                   |             |
| CRITICALRESPONSESTATUS | Critical threshold                                                                                  |                   |             |
| EXTRAOPTIONS           | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Backend-Time" label="Backend-Time">

| Macro                         | Description                                                                                         | Valeur par défaut | Obligatoire |
|:------------------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME                     |                                                                                                     | 900               |             |
| INTERVAL                      |                                                                                                     | PT5M              |             |
| AGGREGATION                   |                                                                                                     | Average           |             |
| FILTERMETRIC                  |                                                                                                     |                   |             |
| FILTERDIMENSION               |                                                                                                     |                   |             |
| WARNINGCONNECTTIME            | Warning threshold where '*'                                                                         |                   |             |
| CRITICALCONNECTTIME           | Critical threshold where '*'                                                                        |                   |             |
| WARNINGFIRSTBYTERESPONSETIME  | Warning threshold where '*'                                                                         |                   |             |
| CRITICALFIRSTBYTERESPONSETIME | Critical threshold where '*'                                                                        |                   |             |
| WARNINGLASTBYTERESPONSETIME   | Warning threshold where '*'                                                                         |                   |             |
| CRITICALLASTBYTERESPONSETIME  | Critical threshold where '*'                                                                        |                   |             |
| EXTRAOPTIONS                  | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Clients-Traffic" label="Clients-Traffic">

| Macro                        | Description                                                                                         | Valeur par défaut | Obligatoire |
|:-----------------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME                    |                                                                                                     | 900               |             |
| INTERVAL                     |                                                                                                     | PT5M              |             |
| AGGREGATION                  |                                                                                                     | Total             |             |
| FILTERMETRIC                 |                                                                                                     |                   |             |
| FILTERDIMENSION              |                                                                                                     |                   |             |
| WARNINGCLIENTSBYTESRECEIVED  | Warning threshold where '*'                                                                         |                   |             |
| CRITICALCLIENTSBYTESRECEIVED | Critical threshold where '*'                                                                        |                   |             |
| WARNINGCLIENTSBYTESSENT      | Warning threshold where '*'                                                                         |                   |             |
| CRITICALCLIENTSBYTESSENT     | Critical threshold where '*'                                                                        |                   |             |
| EXTRAOPTIONS                 | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Connections" label="Connections">

| Macro                      | Description                                                                                         | Valeur par défaut | Obligatoire |
|:---------------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME                  |                                                                                                     | 900               |             |
| INTERVAL                   |                                                                                                     | PT5M              |             |
| AGGREGATION                |                                                                                                     | Average           |             |
| FILTERMETRIC               |                                                                                                     |                   |             |
| FILTERDIMENSION            |                                                                                                     |                   |             |
| WARNINGCURRENTCONNECTIONS  | Warning threshold                                                                                   |                   |             |
| CRITICALCURRENTCONNECTIONS | Critical threshold                                                                                  |                   |             |
| EXTRAOPTIONS               | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Gateway-Time" label="Gateway-Time">

| Macro             | Description                                                                                         | Valeur par défaut | Obligatoire |
|:------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME         |                                                                                                     | 900               |             |
| INTERVAL          |                                                                                                     | PT5M              |             |
| AGGREGATION       |                                                                                                     | Average           |             |
| FILTERMETRIC      |                                                                                                     |                   |             |
| FILTERDIMENSION   |                                                                                                     |                   |             |
| WARNINGTOTALTIME  | Warning threshold                                                                                   |                   |             |
| CRITICALTOTALTIME | Critical threshold                                                                                  |                   |             |
| EXTRAOPTIONS      | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Health" label="Health">

| Macro          | Description                                                                                                                                                        | Valeur par défaut            | Obligatoire |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------|:-----------:|
| OKSTATUS       | Define the conditions to match for the status to be OK (Default: '%{status} =~ /^Available$/'). You can use the following variables: %{status}, %{summary}         | %{status} =~ /^Available$/   |             |
| UNKNOWNSTATUS  | Define the conditions to match for the status to be UNKNOWN (Default: '%{status} =~ /^Unknown$/'). You can use the following variables: %{status}, %{summary}      | %{status} =~ /^Unknown$/     |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (Default: '%{status} =~ /^Unavailable$/'). You can use the following variables: %{status}, %{summary} | %{status} =~ /^Unavailable$/ |             |
| WARNINGSTATUS  | Define the conditions to match for the status to be WARNING (Default: ''). You can use the following variables: %{status}, %{summary}                              |                              |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                                |                              |             |

</TabItem>
<TabItem value="Requests" label="Requests">

| Macro                  | Description                                                                                         | Valeur par défaut | Obligatoire |
|:-----------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME              |                                                                                                     | 900               |             |
| INTERVAL               |                                                                                                     | PT5M              |             |
| AGGREGATION            |                                                                                                     | Total             |             |
| FILTERMETRIC           |                                                                                                     |                   |             |
| FILTERDIMENSION        |                                                                                                     |                   |             |
| WARNINGFAILEDREQUESTS  | Warning threshold where '*'                                                                         |                   |             |
| CRITICALFAILEDREQUESTS | Critical threshold where '*'                                                                        |                   |             |
| WARNINGTOTALREQUESTS   | Warning threshold where '*'                                                                         |                   |             |
| CRITICALTOTALREQUESTS  | Critical threshold where '*'                                                                        |                   |             |
| EXTRAOPTIONS           | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Throughput" label="Throughput">

| Macro              | Description                                                                                         | Valeur par défaut | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME          |                                                                                                     | 900               |             |
| INTERVAL           |                                                                                                     | PT5M              |             |
| AGGREGATION        |                                                                                                     | Average           |             |
| FILTERMETRIC       |                                                                                                     |                   |             |
| FILTERDIMENSION    |                                                                                                     |                   |             |
| WARNINGTHROUGHPUT  | Warning threshold                                                                                   |                   |             |
| CRITICALTHROUGHPUT | Critical threshold                                                                                  |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Units" label="Units">

| Macro                        | Description                                                                                                                          | Valeur par défaut | Obligatoire |
|:-----------------------------|:-------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| TIMEFRAME                    | Set timeframe in seconds (i.e. 3600 to check last hour)                                                                              | 900               |             |
| INTERVAL                     | Set interval of the metric query (Can be : PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H, PT24H)                                       | PT5M              |             |
| AGGREGATION                  | Aggregate monitoring. Can apply to: 'minimum', 'maximum', 'average', 'total' and 'count'. Can be called multiple times               | Average           |             |
| FILTERMETRIC                 |                                                                                                                                      |                   |             |
| FILTERDIMENSION              | Specify the metric dimension (required for some specific metrics) Syntax example: --filter-dimension="$metricname eq '$metricvalue'" |                   |             |
| WARNINGCAPACITYUNITS         | Warning threshold where '*'                                                                                                          |                   |             |
| CRITICALCAPACITYUNITS        | Critical threshold where '*'                                                                                                         |                   |             |
| WARNINGCOMPUTEUNITS          | Warning threshold where '*'                                                                                                          |                   |             |
| CRITICALCOMPUTEUNITS         | Critical threshold where '*'                                                                                                         |                   |             |
| WARNINGESTIMATEDBILLEDUNITS  | Warning threshold where '*'                                                                                                          |                   |             |
| CRITICALESTIMATEDBILLEDUNITS | Critical threshold where '*'                                                                                                         |                   |             |
| WARNINGFIXEDBILLABLEUNITS    | Warning threshold where '*'                                                                                                          |                   |             |
| CRITICALFIXEDBILLABLEUNITS   | Critical threshold where '*'                                                                                                         |                   |             |
| EXTRAOPTIONS                 | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                  |                   |             |

</TabItem>
</Tabs>

3. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). Le service apparaît dans la liste des services supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails du service : celle-ci montre les valeurs des macros.

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`). Vous pouvez tester
que le connecteur arrive bien à superviser une instance Azure en utilisant une commande
telle que celle-ci (remplacez les valeurs d'exemple par les vôtres) :

```bash
/usr/lib/centreon/plugins//centreon_azure_network_appgateway_api.pl \
	--plugin=cloud::azure::network::appgateway::plugin \
	--mode=units \
	--custommode='' \
	--resource='' \
	--resource-group='' \
	--subscription='' \
	--tenant='' \
	--client-id='' \
	--client-secret='' \
	--proxyurl=''  \
	--filter-metric='' \
	--filter-dimension='' \
	--timeframe='900' \
	--interval='PT5M' \
	--aggregation='Average' \
	--warning-estimated-billed-units='' \
	--critical-estimated-billed-units='' \
	--warning-fixed-billable-units='' \
	--critical-fixed-billable-units='' \
	--warning-compute-units='' \
	--critical-compute-units='' \
	--warning-capacity-units='' \
	--critical-capacity-units='' \
	
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: Capacity Units consumed: 30 Compute Units consumed: 55 Estimated Billed Capacity Units: 35 Fixed Billable Capacity Units: 0 | 'appgateway.capacity.units.count'=30;;;0; 'appgateway.compute.units.count'=55;;;0; 'appgateway.billed.units.estimated.count'=35;;;0; 'appgateway.billable.units.fixed.count'=0;;;0; 
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks)
des plugins basés sur HTTP/API.

### Modes disponibles

Dans la plupart des cas, un mode correspond à un modèle de service. Le mode est renseigné dans la commande d'exécution 
du connecteur. Dans l'interface de Centreon, il n'est pas nécessaire de les spécifier explicitement, leur utilisation est
implicite dès lors que vous utilisez un modèle de service. En revanche, vous devrez spécifier le mode correspondant à ce
modèle si vous voulez tester la commande d'exécution du connecteur dans votre terminal.

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_azure_network_appgateway_api.pl \
	--plugin=cloud::azure::network::appgateway::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                                          | Modèle de service associé                                 |
|:----------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------|
| backend-health [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/backendhealth.pm)]   | Cloud-Azure-Network-AppGateway-Backend-Health-Api-custom  |
| backend-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/backendstatus.pm)]   | Cloud-Azure-Network-AppGateway-Backend-Status-Api-custom  |
| backend-time [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/backendtime.pm)]       | Cloud-Azure-Network-AppGateway-Backend-Time-Api-custom    |
| clients-traffic [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/clientstraffic.pm)] | Cloud-Azure-Network-AppGateway-Clients-Traffic-Api-custom |
| connections [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/connections.pm)]        | Cloud-Azure-Network-AppGateway-Connections-Api-custom     |
| discovery [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/discovery.pm)]            | Used for host discovery                                   |
| gateway-time [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/gatewaytime.pm)]       | Cloud-Azure-Network-AppGateway-Gateway-Time-Api-custom    |
| health [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/health.pm)]                  | Cloud-Azure-Network-AppGateway-Health-Api-custom          |
| requests [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/requests.pm)]              | Cloud-Azure-Network-AppGateway-Requests-Api-custom        |
| throughput [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/throughput.pm)]          | Cloud-Azure-Network-AppGateway-Throughput-Api-custom      |
| units [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/cloud/azure/network/appgateway/mode/units.pm)]                    | Cloud-Azure-Network-AppGateway-Units-Api-custom           |

### Custom modes disponibles

Ce connecteur offre plusieurs méthodes pour se connecter à la ressource (CLI, bibliothèque, etc.), appelées **custom modes**.
Tous les custom modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-custommode` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_azure_network_appgateway_api.pl \
	--plugin=cloud::azure::network::appgateway::plugin \
	--list-custommode
```

Le plugin apporte les custom modes suivants :

* api
* azcli

### Options disponibles

#### Options génériques

Les options génériques sont listées ci-dessous :

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --mode                                     | Define the mode in which you want the plugin to be executed (see--list-mode).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --dyn-mode                                 | Specify a mode with the module's path (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --list-mode                                | List all available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --version                                  | Return the version of the plugin.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --custommode                               | When a plugin offers several ways (CLI, library, etc.) to get the an information the desired one must be defined with this option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --list-custommode                          | List all available custom modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --multiple                                 | Multiple custom mode objects. This may be required by some specific modes (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
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
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.      Microsoft Azure CLI 2.0      To install the Azure CLI 2.0 in a CentOS/RedHat environment :      (As root)      # rpm --import https://packages.microsoft.com/keys/microsoft.asc      # sh -c 'echo -e "\[azure-cli\]\nname=Azure     CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=     1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc"     \> /etc/yum.repos.d/azure-cli.repo'      # yum install azure-cli      (As centreon-engine)      # az login      Go to https://aka.ms/devicelogin and enter the code given by the last     command.      For futher informations, visit     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-     cli-latest.                                                                                                                   |

#### Options des custom modes

Les options spécifiques aux **custom modes** sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="api" label="api">

| Option                 | Description                                                                                                                                                                                                                                   |
|:-----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --subscription         | Set Azure subscription ID.                                                                                                                                                                                                                    |
| --tenant               | Set Azure tenant ID.                                                                                                                                                                                                                          |
| --client-id            | Set Azure client ID.                                                                                                                                                                                                                          |
| --client-secret        | Set Azure client secret.                                                                                                                                                                                                                      |
| --login-endpoint       | Set Azure login endpoint URL (Default: 'https://login.microsoftonline.com')                                                                                                                                                                   |
| --management-endpoint  | Set Azure management endpoint URL (Default: 'https://management.azure.com')                                                                                                                                                                   |
| --timeframe            | Set timeframe in seconds (i.e. 3600 to check last hour).                                                                                                                                                                                      |
| --interval             | Set interval of the metric query (Can be : PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H, PT24H).                                                                                                                                               |
| --aggregation          | Aggregate monitoring. Can apply to: 'minimum', 'maximum', 'average', 'total' and 'count'. Can be called multiple times.                                                                                                                       |
| --zeroed               | Set metrics value to 0 if they are missing. Useful when some metrics are undefined.                                                                                                                                                           |
| --timeout              | Set timeout in seconds (Default: 10).                                                                                                                                                                                                         |
| --http-peer-addr       | Set the address you want to connect to. Useful if hostname is only a vhost, to avoid IP resolution.                                                                                                                                           |
| --proxyurl             | Proxy URL. Eg: http://my.proxy:3128                                                                                                                                                                                                           |
| --proxypac             | Proxy pac file (can be a URL or a local file).                                                                                                                                                                                                |
| --insecure             | Accept insecure SSL connections.                                                                                                                                                                                                              |
| --http-backend         | Perl library to use for HTTP transactions. Possible values are: lwp (default) and curl.                                                                                                                                                       |
| --ssl-opt              | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                     |
| --curl-opt             | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                              |
| --memcached            | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server         | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute      | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db             | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file        | Failback on a local file if redis connection failed.                                                                                                                                                                                          |
| --memexpiration        | Time to keep data in seconds (Default: 86400).                                                                                                                                                                                                |
| --statefile-dir        | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix     | Define a suffix to customize the statefile name (Default: '').                                                                                                                                                                                |
| --statefile-concat-cwd | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format     | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key        | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher     | Define the cipher algorithm to encrypt the cache (Default: 'AES').                                                                                                                                                                            |
| --filter-dimension     | Specify the metric dimension (required for some specific metrics) Syntax example: --filter-dimension="$metricname eq '$metricvalue'"                                                                                                          |
| --per-sec              | Display the statistics based on a per-second period.                                                                                                                                                                                          |

</TabItem>
<TabItem value="azcli" label="azcli">

| Option             | Description                                                                                                                            |
|:-------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| --subscription     | Set Azure subscription (Required if logged to several subscriptions).                                                                  |
| --timeframe        | Set timeframe in seconds (i.e. 3600 to check last hour).                                                                               |
| --interval         | Set interval of the metric query (Can be : PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H, PT24H).                                        |
| --aggregation      | Aggregate monitoring. Can apply to: 'minimum', 'maximum', 'average', 'total' and 'count'. Can be called multiple times.                |
| --zeroed           | Set metrics value to 0 if they are missing. Useful when some metrics are undefined.                                                    |
| --timeout          | Set timeout in seconds (Default: 50).                                                                                                  |
| --sudo             | Use 'sudo' to execute the command.                                                                                                     |
| --command          | Command to get information (Default: 'az'). Can be changed if you have output in a file.                                               |
| --command-path     | Command path (Default: none).                                                                                                          |
| --command-options  | Command options (Default: none).                                                                                                       |
| --proxyurl         | Proxy URL if any                                                                                                                       |
| --filter-dimension | Specify the metric dimension (required for some specific metrics) Syntax example: --filter-dimension="$metricname eq '$metricvalue'"   |
| --per-sec          | Display the statistics based on a per-second period.                                                                                   |

</TabItem>
</Tabs>

#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Backend-Health" label="Backend-Health">

| Option           | Description                                                                       |
|:-----------------|:----------------------------------------------------------------------------------|
| --resource       | Set resource name or id (Required).                                               |
| --resource-group | Set resource group (Required if resource's name is used).                         |
| --warning-*      | Warning threshold where '*' can be: 'healthyhostcount', 'unhealthyhostcount'.     |
| --critical-*     | Critical threshold where '*' can be: 'healthyhostcount', 'unhealthyhostcount'.    |

</TabItem>
<TabItem value="Backend-Status" label="Backend-Status">

| Option                     | Description                                                 |
|:---------------------------|:------------------------------------------------------------|
| --resource                 | Set resource name or id (Required).                         |
| --resource-group           | Set resource group (Required if resource's name is used).   |
| --warning-response-status  | Warning threshold.                                          |
| --critical-response-status | Critical threshold.                                         |

</TabItem>
<TabItem value="Backend-Time" label="Backend-Time">

| Option           | Description                                                                                                  |
|:-----------------|:-------------------------------------------------------------------------------------------------------------|
| --resource       | Set resource name or id (Required).                                                                          |
| --resource-group | Set resource group (Required if resource's name is used).                                                    |
| --warning-*      | Warning threshold where '*' can be: 'connect-time', 'lastbyte-response-time', 'firstbyte-response-time'.     |
| --critical-*     | Critical threshold where '*' can be: 'connect-time', 'lastbyte-response-time', 'firstbyte-response-time'.    |

</TabItem>
<TabItem value="Clients-Traffic" label="Clients-Traffic">

| Option           | Description                                                                             |
|:-----------------|:----------------------------------------------------------------------------------------|
| --resource       | Set resource name or id (Required).                                                     |
| --resource-group | Set resource group (Required if resource's name is used).                               |
| --warning-*      | Warning threshold where '*' can be: 'clients-bytes-received', 'clients-bytes-sent'.     |
| --critical-*     | Critical threshold where '*' can be: 'clients-bytes-received', 'clients-bytes-sent'.    |

</TabItem>
<TabItem value="Connections" label="Connections">

| Option                         | Description                                                 |
|:-------------------------------|:------------------------------------------------------------|
| --resource                     | Set resource name or id (Required).                         |
| --resource-group               | Set resource group (Required if resource's name is used).   |
| --warning-current-connections  | Warning threshold.                                          |
| --critical-current-connections | Critical threshold.                                         |

</TabItem>
<TabItem value="Gateway-Time" label="Gateway-Time">

| Option                | Description                                                 |
|:----------------------|:------------------------------------------------------------|
| --resource            | Set resource name or id (Required).                         |
| --resource-group      | Set resource group (Required if resource's name is used).   |
| --warning-total-time  | Warning threshold.                                          |
| --critical-total-time | Critical threshold.                                         |

</TabItem>
<TabItem value="Health" label="Health">

| Option            | Description                                                                                                                                                          |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --resource        | Set resource name or id (Required).                                                                                                                                  |
| --resource-group  | Set resource group (Required if resource's name is used).                                                                                                            |
| --warning-status  | Define the conditions to match for the status to be WARNING (Default: ''). You can use the following variables: %{status}, %{summary}                                |
| --critical-status | Define the conditions to match for the status to be CRITICAL (Default: '%{status} =~ /^Unavailable$/'). You can use the following variables: %{status}, %{summary}   |
| --unknown-status  | Define the conditions to match for the status to be UNKNOWN (Default: '%{status} =~ /^Unknown$/'). You can use the following variables: %{status}, %{summary}        |
| --ok-status       | Define the conditions to match for the status to be OK (Default: '%{status} =~ /^Available$/'). You can use the following variables: %{status}, %{summary}           |

</TabItem>
<TabItem value="Requests" label="Requests">

| Option           | Description                                                                  |
|:-----------------|:-----------------------------------------------------------------------------|
| --resource       | Set resource name or id (Required).                                          |
| --resource-group | Set resource group (Required if resource's name is used).                    |
| --warning-*      | Warning threshold where '*' can be: 'failed-requests', 'total-requests'.     |
| --critical-*     | Critical threshold where '*' can be: 'failed-requests', 'total-requests'.    |

</TabItem>
<TabItem value="Throughput" label="Throughput">

| Option                | Description                                                 |
|:----------------------|:------------------------------------------------------------|
| --resource            | Set resource name or id (Required).                         |
| --resource-group      | Set resource group (Required if resource's name is used).   |
| --warning-throughput  | Warning threshold.                                          |
| --critical-throughput | Critical threshold.                                         |

</TabItem>
<TabItem value="Units" label="Units">

| Option           | Description                                                                                                                  |
|:-----------------|:-----------------------------------------------------------------------------------------------------------------------------|
| --resource       | Set resource name or id (Required).                                                                                          |
| --resource-group | Set resource group (Required if resource's name is used).                                                                    |
| --warning-*      | Warning threshold where '*' can be: 'estimated-billed-units', 'fixed-billable-units', 'compute-units', 'capacity-units'.     |
| --critical-*     | Critical threshold where '*' can be: 'estimated-billed-units', 'fixed-billable-units', 'compute-units', 'capacity-units'.    |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins//centreon_azure_network_appgateway_api.pl \
	--plugin=cloud::azure::network::appgateway::plugin \
	--mode=units \
	--custommode='azcli \
	--help
```
