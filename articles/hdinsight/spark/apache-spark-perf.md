---
title: Optimiser les performances des travaux Spark - Azure HDInsight
description: Présente des stratégies courantes permettant d’optimiser les performances des clusters Apache Spark dans Azure HDInsight.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 08/21/2020
ms.custom: contperfq1
ms.openlocfilehash: fbd0da43e79ee2c27f654f9bd07614e08c12fd30
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88756926"
---
# <a name="optimize-apache-spark-jobs-in-hdinsight"></a>Optimiser les travaux Apache Spark dans Azure HDInsight

Cet article fournit une vue d’ensemble des stratégies permettant d’optimiser les tâches Apache Spark sur Azure HDInsight.

## <a name="overview"></a>Vue d’ensemble

Les performances de vos tâches Apache Spark dépendent de plusieurs facteurs. Ces facteurs de performances incluent la façon dont vos données sont stockées, la façon dont le cluster est configuré et les opérations qui sont utilisées lors du traitement des données.

Les problèmes courants que vous pouvez rencontrer incluent les contraintes de mémoire résultant d’un dimensionnement incorrect des exécuteurs, d’opérations de longue durée et de tâches qui entraînent des opérations cartésiennes.

Il existe également plusieurs optimisations qui peuvent vous aider à surmonter ces défis, telles que la mise en cache et l’autorisation de l’asymétrie des données.

Dans chacun des articles suivants, vous trouverez des informations sur les différents aspects de l’optimisation de Spark.

* [Optimiser le stockage des données pour Apache Spark](optimize-data-storage.md)
* [Optimiser le traitement de données pour Apache Spark](optimize-data-processing.md)
* [Optimiser l’utilisation de la mémoire pour Apache Spark](optimize-memory-usage.md)
* [Optimiser la configuration de cluster HDInsight pour Apache Spark](optimize-cluster-configuration.md)

## <a name="next-steps"></a>Étapes suivantes

* [Déboguer des travaux Apache Spark en cours d’exécution sur Azure HDInsight](apache-spark-job-debugging.md)
* [Gérer les ressources d’un cluster Apache Spark sur HDInsight](apache-spark-resource-manager.md)
* [Configurer les paramètres d’Apache Spark](apache-spark-settings.md)
