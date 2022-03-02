---
id: monitor-linux-server-with-snmp
title: Superviser votre premier serveur Linux
---

## Superviser un serveur Linux avec SNMP

Dans ce tutoriel, nous partons du principe que votre plate-forme Centreon est installée et fonctionne correctement, et que vous disposez au moins d'une édition [Centreon IT 100](it100.md) qui fournit les Plugin Packs Centreon (votre [licence](../administration/licenses.md) est déjà en place).

Votre serveur sera supervisé à l'aide du Plugin Pack [Linux SNMP](../integrations/plugin-packs/procedures/operatingsystems-linux-snmp.md). (Plus d'informations sur les Plugin Packs [ici](../monitoring/pluginpacks.md)).

## Prérequis

### Sur le serveur Linux que vous souhaitez superviser

La première étape consiste à activer et à configurer l'agent SNMP sur l'hôte à superviser.
Veuillez vous référer à la documentation de votre distribution Linux pour savoir comment configurer l'agent SNMP.

Voici ci-dessous un fichier de configuration snmpd.conf/net-snmp minimaliste :

- remplacez **my-snmp-community** par la valeur correspondant à votre environnement.
- Ajoutez la ligne **view centreon included .1.3.6.1** pour avoir accès à toutes les informations de la MIB requises par le plugin

```shell
#       sec.name  source          community
com2sec notConfigUser  default       my-snmp-community

####
# Second, map the security name into a group name:

#       groupName      securityModel securityName
group   notConfigGroup v1           notConfigUser
group   notConfigGroup v2c           notConfigUser

####
# Third, create a view for us to let the group have rights to:

# Make at least  snmpwalk -v 1 localhost -c public system fast again.
#       name           incl/excl     subtree         mask(optional)
view centreon included .1.3.6.1
view    systemview    included   .1.3.6.1.2.1.1
view    systemview    included   .1.3.6.1.2.1.25.1.1

```

L'agent SNMP doit être redémarré à chaque fois que la configuration est modifiée. Assurez-vous également que l'agent SNMP est configuré pour démarrer automatiquement au démarrage. Utilisez les commandes suivantes pour les distributions récentes :

```shell
systemctl restart snmpd
systemctl enable snmpd
```

> Le serveur cible doit être accessible depuis le collecteur Centreon sur le port SNMP UDP/161.

### Sur le collecteur

Connectez-vous à votre collecteur en SSH et installez le plugin SNMP Linux (voir la [procédure de surveillance pour le Plugin Pack **Linux SNMP**](../integrations/plugin-packs/procedures/operatingsystems-linux-snmp.md) pour plus d'informations) :

```shell
yum install centreon-plugin-Operatingsystems-Linux-Snmp
```

### Sur le serveur central

Dans l'interface web, allez à la page **Configuration > Plugin Packs** et installez le Plugin Pack **Linux SNMP** :

![image](../assets/getting-started/quick_start_linux_0.gif)

## Configurer l'hôte et déployer la configuration

1. Allez à la page **Configuration > Hôtes > Hôtes** et cliquez sur **Ajouter** :

   ![image](../assets/getting-started/quick_start_linux_1.gif)

2. Remplissez les informations suivantes :

   * Le nom du serveur (1)
   * Une description de celui-ci (2)
   * L'adresse IP du serveur (3)
   * La communauté SNMP et sa version (4)
   * Sélectionnez le collecteur désiré (laissez "Central" si vous n'avez pas d'autre collecteur) (5)

3. Cliquez sur **+ Ajouter une nouvelle entrée** dans le champ **Modèles** (6), puis sélectionnez le modèle **OS-Linux-SNMP-custom** (7) dans la liste :

   ![image](../assets/getting-started/quick_start_linux_2.png)

4. Cliquez sur **Sauvegarder** (8). Votre équipement a été ajouté à la liste des hôtes :

   ![image](../assets/getting-started/quick_start_linux_3.png)

5. Allez à la page **Configuration > Services > Services par hôte**. Un ensemble d'indicateurs a été créé automatiquement.

   ![image](../assets/getting-started/quick_start_linux_4a.png)

   Vous pouvez également utiliser le raccourci situé à côté du nom de l'hôte pour accéder directement à la page **Configuration > Services > Services par hôte**. La liste sera filtrée par le nom de l'hôte :

   ![image](../assets/getting-started/quick_start_linux_4b.png)

   ![image](../assets/getting-started/quick_start_linux_5.png)

6. [Déployez la configuration](first-supervision.md#deployer-une-configuration).

7. Allez à la page **Surveillance > Statut des ressources** et sélectionnez **Toutes** dans le filtre **Statut des ressources**. Dans un premier temps, les ressources apparaissent avec le statut **En attente**, ce qui signifie qu'aucun contrôle n'a encore été exécuté :

   ![image](../assets/getting-started/quick_start_linux_6.png)

   Après quelques minutes, les premiers résultats du contrôle apparaissent :

   ![image](../assets/getting-started/quick_start_linux_7.png)

   Si tous les services ne sont pas dans un état OK, vérifiez la cause de l'erreur et corrigez le problème.


### Pour aller plus loin

Le Plugin Pack **Linux SNMP** apporte de nombreux modèles de supervision. Rendez-vous dans le menu  **Configuration > Services > Modèles** et trouvez la liste complète:

   ![image](../assets/getting-started/quick_start_linux_8.png)

Avec **Centreon IT Edition**, vous pouvez ajouter très rapidement et très simplement la supervision de vos interfaces réseaux, partitions, processus et services en utilisant la fonctionnalité de [découverte des services](../monitoring/discovery/services-discovery).

1. Rendez-vous dans le menu **Configuration > Services > Manuelle**. Commencez à saisir le nom de l’hôte sur lequel réaliser la découverte et l’interface vous proposera de compléter automatiquement ce dernier :

   ![image](../assets/getting-started/quick_start_linux_9.png)

2. Sélectionnez ensuite la commande de découverte à exécuter dans la liste déroulante qui vient d’apparaître en dessous du champ **Rule**. Cliquez sur le bouton **Scan** et patientez durant l’analyse des éléments disponibles. Le résultat s’affiche. Sélectionnez les éléments à intégrer à la supervision et cliquez sur le bouton **Save** :

   ![image](../assets/getting-started/quick_start_linux_10.png)

  Les éléments ont été ajoutés. Vous pouvez sélectionner une autre commande de découverte et répéter le processus.

3. Les services ont été ajoutés et peuvent être affichés dans le menu **Configuration > Services > Services par hôte** :

   ![image](../assets/getting-started/quick_start_linux_11.png)

4. [Déployez la configuration](first-supervision#deploying-a-configuration).