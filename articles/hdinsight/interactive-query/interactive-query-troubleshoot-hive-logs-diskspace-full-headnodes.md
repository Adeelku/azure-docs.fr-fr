---
title: Journaux Apache Hive saturant l’espace disque - Azure HDInsight
description: Les journaux Apache Hive saturent l’espace disque sur les nœuds principaux dans Azure HDInsight.
ms.service: hdinsight
ms.topic: troubleshooting
author: nisgoel
ms.author: nisgoel
ms.reviewer: jasonh
ms.date: 10/05/2020
ms.openlocfilehash: 5554a66927fc70f22ec552b938ae62038a04acb9
ms.sourcegitcommit: d767156543e16e816fc8a0c3777f033d649ffd3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2020
ms.locfileid: "92533017"
---
# <a name="scenario-apache-hive-logs-are-filling-up-the-disk-space-on-the-head-nodes-in-azure-hdinsight"></a>Scénario : Les journaux Apache Hive saturent l’espace disque sur les nœuds principaux dans Azure HDInsight

Cet article décrit les étapes de résolution des problèmes, et les solutions possibles à apporter aux problèmes liés à un espace disque insuffisant sur les nœuds principaux dans les clusters Azure HDInsight.

## <a name="issue"></a>Problème

Sur un cluster Apache Hive/LLAP, des journaux indésirables occupent la totalité de l’espace disque sur les nœuds principaux. Pour cette raison, les problèmes suivants peuvent se produire.

1. L’accès SSH échoue car aucun espace n’est laissé sur le nœud principal.
2. Ambari indique *ERREUR HTTP : 503 Service indisponible* .
3. Le redémarrage de HiveServer2 Interactive échoue.

Les journaux `ambari-agent` signalent les éléments suivants lorsque le problème se produit.
```
ambari_agent - Controller.py - [54697] - Controller - ERROR - Error:[Errno 28] No space left on device
```
```
ambari_agent - HostCheckReportFileHandler.py - [54697] - ambari_agent.HostCheckReportFileHandler - ERROR - Can't write host check file at /var/lib/ambari-agent/data/hostcheck.result
```

## <a name="cause"></a>Cause

Dans les configurations hive-log4j avancées, la planification de suppression par défaut actuelle est définie pour les fichiers de plus de 30 jours en fonction de la date de dernière modification.

## <a name="resolution"></a>Résolution

1. Accédez au résumé du composant Hive sur le portail Ambari, puis cliquez sur l’onglet `Configs`.

2. Accédez à la section `Advanced hive-log4j` dans les paramètres avancés.

3. Définissez le paramètre `appender.RFA.strategy.action.condition.age` sur l’âge de votre choix. Exemple pour 14 jours : `appender.RFA.strategy.action.condition.age = 14D`.

4. Si vous ne voyez aucun paramètre associé, ajoutez les paramètres suivants.
    ```
    # automatically delete hive log
    appender.RFA.strategy.action.type = Delete
    appender.RFA.strategy.action.basePath = ${sys:hive.log.dir}
    appender.RFA.strategy.action.condition.type = IfLastModified
    appender.RFA.strategy.action.condition.age = 30D
    appender.RFA.strategy.action.PathConditions.type = IfFileName
    appender.RFA.strategy.action.PathConditions.regex = hive*.*log.*
    ```

5. Définissez `hive.root.logger` sur `INFO,RFA` comme suit. Le paramètre par défaut est DEBUG, ce qui augmente considérablement la taille des journaux.

    ```
    # Define some default values that can be overridden by system properties
    hive.log.threshold=ALL
    hive.root.logger=INFO,RFA
    hive.log.dir=${java.io.tmpdir}/${user.name}
    hive.log.file=hive.log
    ```

6. Enregistrez les configurations et redémarrez les composants nécessaires.

## <a name="next-steps"></a>Étapes suivantes

Si votre problème ne figure pas dans cet article ou si vous ne parvenez pas à le résoudre, utilisez un des canaux suivants pour obtenir de l’aide :

* Obtenez des réponses de la part d’experts Azure en faisant appel au [Support de la communauté Azure](https://azure.microsoft.com/support/community/).

* Connectez-vous avec [@AzureSupport](https://twitter.com/azuresupport), le compte Microsoft Azure officiel pour améliorer l’expérience client en connectant la communauté Azure aux ressources appropriées (réponses, support et experts).

* Si vous avez besoin d’une aide supplémentaire, vous pouvez envoyer une requête de support à partir du [Portail Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/). Sélectionnez **Support** dans la barre de menus, ou ouvrez le hub **Aide + Support** . Pour en savoir plus, voir [Création d’une requête de support Azure](../../azure-portal/supportability/how-to-create-azure-support-request.md). L’accès au support relatif à la gestion et à la facturation des abonnements est inclus avec votre abonnement Microsoft Azure. En outre, le support technique est fourni avec l’un des [plans de support Azure](https://azure.microsoft.com/support/plans/).