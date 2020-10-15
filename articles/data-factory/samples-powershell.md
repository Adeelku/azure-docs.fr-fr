---
title: Exemples Azure PowerShell pour Azure Data Factory
description: Exemples Azure PowerShell - Scripts pour vous aider à créer et à gérer des fabriques de données.
services: data-factory
ms.service: data-factory
ms.workload: data-services
author: djpmsft
ms.author: daperlov
manager: jroth
ms.reviewer: maghan
ms.topic: conceptual
ms.date: 01/16/2018
ms.openlocfilehash: 6df400e7ce4b66a1589a0c44089148b33ab88638
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89439059"
---
# <a name="azure-powershell-samples-for-azure-data-factory"></a>Exemples Azure PowerShell pour Azure Data Factory

[!INCLUDE[appliesto-adf-xxx-md](includes/appliesto-adf-xxx-md.md)]

Le tableau suivant comprend des liens vers des exemples de scripts Azure PowerShell pour Azure Data Factory.

| Script | Description  |
|---|---|
|**Copie de données**||
|[Copier des objets blob à partir d’un dossier vers un autre dossier dans un stockage Blob Azure](scripts/copy-azure-blob-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell copie des objets blob depuis un dossier du Stockage Blob Azure vers un autre dossier de ce même stockage. |
|[Copier des données d’une base de données SQL Server vers le Stockage Blob Azure](scripts/hybrid-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell copie des données à partir d’une base de données SQL Server vers un stockage Blob Azure. |
|[Copie en bloc](scripts/bulk-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Cet exemple de script PowerShell copie les données de plusieurs tables dans une base de données Azure SQL Database vers Azure Synapse Analytics (anciennement SQL Data Warehouse). |
|[Copie incrémentielle](scripts/incremental-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Cet exemple de script PowerShell charge uniquement les enregistrements nouveaux ou mis à jour à partir d’un magasin de données source vers un magasin de données récepteur, après la copie initiale complète des données de la source vers le récepteur. |
|**Transformer des données**||
|[Transformer des données à l’aide d’un cluster Spark](scripts/transform-data-spark-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell transforme les données en exécutant un programme sur un cluster Spark. |
|**Intégrer par « lift-and-shift » des packages SSIS sur Azure**||
|[Créer un runtime d’intégration Azure-SSIS](scripts/deploy-azure-ssis-integration-runtime-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell provisionne un runtime d’intégration SSIS-Azure qui exécute les packages SSIS (SQL Server Integration Services) dans Azure. |



