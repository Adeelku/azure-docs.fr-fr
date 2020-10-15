---
title: Services Azure prenant en charge Azure Data Lake Storage Gen2 | Microsoft Docs
description: Apprenez-en davantage sur les services Azure qui s’intègrent avec Azure Data Lake Storage Gen2
author: normesta
ms.subservice: data-lake-storage-gen2
ms.service: storage
ms.topic: conceptual
ms.date: 08/05/2020
ms.author: normesta
ms.reviewer: stewu
ms.openlocfilehash: c3a5f3a984c95af400c9e0c1543e3c1883290668
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89442954"
---
# <a name="azure-services-that-support-azure-data-lake-storage-gen2"></a>Services Azure qui prennent en charge Azure Data Lake Storage Gen2

Vous pouvez utiliser les services Azure pour ingérer des données, effectuer une analytique et créer des représentations visuelles. Cet article fournit la liste des services Azure pris en charge, indique leur niveau de prise en charge, et fournit des liens vers des articles qui vous aident à utiliser ces services avec Azure Data Lake Storage Gen2.

## <a name="supported-azure-services"></a>Services Azure pris en charge

Ce tableau répertorie les services Azure que vous pouvez utiliser avec Azure Data Lake Storage Gen2. Les éléments figurant dans ces tableaux seront modifiés au fil du temps, car la prise en charge continue de s’étendre.

> [!NOTE]
> Le niveau de prise en charge fait référence uniquement à la façon dont le service est pris en charge avec Data Lake Storage Gen2.

|Service Azure |Niveau de support |Azure AD |Clé partagée| Articles connexes |
|---------------|-------------------|---|---|---|
|Azure Data Factory|Mise à la disposition générale|Oui|Oui|[Charger des données dans Azure Data Lake Storage Gen2 avec Azure Data Factory](https://docs.microsoft.com/azure/data-factory/load-azure-data-lake-storage-gen2?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)|
|Azure Databricks|Mise à la disposition générale|Oui|Oui|[Utiliser avec Azure Databricks](https://docs.azuredatabricks.net/data/data-sources/azure/azure-datalake-gen2.html) <br> [Démarrage rapide : Analyser des données dans Azure Data Lake Storage Gen2 à l'aide d'Azure Databricks](data-lake-storage-quickstart-create-databricks-account.md) <br>[Tutoriel : Extraire, transformer et charger des données à l'aide d'Azure Databricks](https://docs.microsoft.com/azure/azure-databricks/databricks-extract-load-sql-data-warehouse) <br>[Tutoriel : Accéder aux données Data Lake Storage Gen2 avec Azure Databricks à l’aide de Spark](data-lake-storage-use-databricks-spark.md)|
|Azure Event Hub|Mise à la disposition générale|Non|Oui|[Capturer des événements avec Azure Event Hubs dans Stockage Blob Azure ou Azure Data Lake Storage](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)|
|Azure Event Grid|Mise à la disposition générale|Oui|Oui|[Tutoriel : Implémenter le modèle de capture de lac de données pour mettre à jour une table Delta Databricks](data-lake-storage-events.md)|
|Azure Logic Apps|Mise à la disposition générale|Non|Oui|[Vue d’ensemble d’Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview)|
|Azure Machine Learning|Mise à la disposition générale|Oui|Oui|[Accéder aux données dans les services de stockage Azure](https://docs.microsoft.com/azure/machine-learning/how-to-access-data)|
|Azure Stream Analytics|Mise à la disposition générale|Oui|Oui|[Démarrage rapide : Créer un travail Stream Analytics à l’aide du portail Azure](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-quick-create-portal) <br> [Sortie vers Azure Data Lake Gen2](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-define-outputs#blob-storage-and-azure-data-lake-gen2)|
|Data Box|Mise à la disposition générale|Non|Oui|[Utiliser Azure Data Box pour migrer les données d’un magasin HDFS local vers Stockage Azure](data-lake-storage-migrate-on-premises-hdfs-cluster.md)|
|HDInsight |Mise à la disposition générale|Oui|Oui|[Utiliser Azure Data Lake Storage Gen2 avec des clusters Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-data-lake-storage-gen2?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)<br>[Utilisation de l’interface CLI HDFS avec Data Lake Storage Gen2](data-lake-storage-use-hdfs-data-lake-storage.md) <br>[Tutoriel : Extraire, transformer et charger des données à l’aide d’Apache Hive sur Azure HDInsight](data-lake-storage-tutorial-extract-transform-load-hive.md)|
|IoT Hub |Mise à la disposition générale|Non|Oui|[Utiliser le routage des messages IoT Hub pour envoyer des messages appareil-à-cloud à différents points de terminaison](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-messages-d2c)|
|Power BI|Mise à la disposition générale|Oui|Oui|[Analyse des données dans Data Lake Storage Gen2 à l’aide de Power BI](https://docs.microsoft.com/power-query/connectors/datalakestorage)|
|Azure Synapse Analytics (anciennement SQL Data Warehouse)|Mise à la disposition générale|Oui|Oui|[Utiliser avec Azure Synapse Analytics (anciennement SQL Data Warehouse)](https://docs.microsoft.com/azure/sql-database/sql-database-vnet-service-endpoint-rule-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#azure-sql-data-warehouse-polybase)|
|SQL Server Integration Services (SSIS)|Mise à la disposition générale|Oui|Oui|[Gestionnaire de connexions Stockage Azure](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-storage-connection-manager?view=sql-server-2017)|
|Explorateur de données Azure|Mise à la disposition générale|Oui|Oui|[Interroger des données dans Azure Data Lake à l’aide d’Azure Data Explorer](https://docs.microsoft.com/azure/data-explorer/data-lake-query-data)|
|Recherche cognitive Azure|PRÉVERSION|Oui|Oui|[Indexer et parcourir des documents Azure Data Lake Storage Gen2 (préversion)](https://docs.microsoft.com/azure/search/search-howto-index-azure-data-lake-storage)|
|Azure Content Delivery Network|Pas encore pris en charge|Non applicable|Non applicable|[Indexer et parcourir des documents Azure Data Lake Storage Gen2 (préversion)](https://docs.microsoft.com/azure/cdn/cdn-overview)|

## <a name="see-also"></a>Voir aussi

- [Problèmes connus avec Azure Data Lake Storage Gen2](data-lake-storage-known-issues.md)
- [Fonctionnalités de stockage blob disponibles dans Azure Data Lake Storage Gen2](data-lake-storage-supported-blob-storage-features.md)
- [Plateformes open source prenant en charge Azure Data Lake Storage Gen2](data-lake-storage-supported-open-source-platforms.md)
- [Accès multiprotocole pour Azure Data Lake Storage](data-lake-storage-multi-protocol-access.md)