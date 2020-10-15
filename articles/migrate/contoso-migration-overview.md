---
title: Série de migration Contoso | Microsoft Docs
description: Liens vers des exemples de scénarios de migration Contoso pour la migration vers Azure.
ms.topic: conceptual
ms.date: 04/20/2020
ms.author: raynew
ms.openlocfilehash: f9f7b3b64cf91019ed4e40d5d52b859419b74836
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "86107629"
---
# <a name="contoso-migration-series"></a>Série de migration Contoso


Nous disposons d’une série d’articles montrant comment l’organisation fictive Contoso migre son infrastructure locale vers le cloud [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/). 

La série comprend des scénarios qui illustrent comment configurer une migration d’infrastructure et exécuter différents types de migrations. Les scénarios augmentent en complexité à mesure qu’ils évoluent. Les articles montrent comment la société Contoso gère la migration, mais des instructions générales et des conseils sont fournis tout au long du document.

## <a name="migration-articles"></a>Articles sur la migration

Les articles de la série sont résumés dans le tableau ci-dessous.  

- Chaque scénario de migration est piloté par des exigences métier légèrement différentes, qui déterminent la stratégie de migration.
- Pour chaque scénario de déploiement, nous fournissons des informations sur les axes stratégiques et les objectifs, une proposition d’architecture, des étapes pour effectuer la migration,ainsi que des recommandations pour le nettoyage et des étapes à effectuer une fois la migration terminée.


**Article** | **Détails** 
--- | --- 
[Article 1 : Vue d’ensemble](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-overview) | Vue d’ensemble de la série d’articles, de la stratégie de migration de Contoso et des exemples d’applications utilisés dans la série. 
[Article 2 : Déployer une infrastructure Azure](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-infrastructure) | Contoso prépare son infrastructure locale et l’infrastructure Azure pour la migration. La même infrastructure est utilisée pour tous les articles de migration de la série. 
[Article 3 : Évaluer les ressources locales à migrer vers Azure](/azure/cloud-adoption-framework/migrate/azure-migration-guide/assess?tabs=Tools)  | Contoso évalue son application locale SmartHotel360 qui s’exécute sur VMware. Contoso évalue les machines virtuelles de l’application à l’aide du service Azure Migrate et la base de données SQL Server de l’application à l’aide de l’Assistant Migration de données.
[Article 4 : Réhéberger une application sur une machine virtuelle Azure et une SQL Managed Instance](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rehost-vm-sql-managed-instance) | Contoso exécute une migration lift-and-shift vers Azure pour son application SmartHotel360 locale. Contoso migre la machine virtuelle front-end de l’application à l’aide d’[Azure Migrate](./migrate-services-overview.md). Contoso migre la base de données d’application vers SQL Managed Instance à l’aide d’[Azure Database Migration Service](../dms/dms-overview.md).
[Article 5 : Réhéberger une application sur des machines virtuelles Azure](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rehost-vm) | Contoso migre les machines virtuelles de son application SmartHotel360 vers des machines virtuelles Azure à l’aide du service Azure Migrate. 
[Article 6 : Réhéberger une application sur des machines virtuelles Azure et dans un groupe de disponibilité SQL Server](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rehost-vm-sql-ag) | Contoso migre l’application SmartHotel360. Contoso utilise Azure Migrate pour migrer les machines virtuelles d’application. La société utilise Database Migration Service pour migrer la base de données d’application vers un cluster SQL Server protégé par un groupe de disponibilité AlwaysOn. 
[Article 7 : Réhéberger une application Linux sur des machines virtuelles Azure](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rehost-linux-vm) | Contoso effectue une migration lift-and-shift de son application osTicket Linux sur des machines virtuelles Azure à l’aide d’Azure Migrate.
[Article 8 : Réhéberger une application Linux sur des machines virtuelles Azure et Azure Database pour MySQL](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rehost-linux-vm-mysql) | Contoso migre son application osTicket Linux vers des machines virtuelles Azure à l’aide d’Azure Migrate. La société migre la base de données de l’application vers Azure Database pour MySQL à l’aide d’Azure Database Migration Service (inclut une autre option utilisant MySQL Workbench).
[Article 9 : Refactoriser une application vers une application web Azure et Azure SQL Database](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-refactor-web-app-sql) | Contoso migre son application SmartHotel360 vers une application web Azure et la base de données de l’application vers Azure SQL Database en utilisant Azure Database Migration Service.
[Article 10 : Refactoriser une application Windows à l’aide d’Azure App Service et d’Azure SQL Database Managed Instance](/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-refactor-web-app-sql-managed-instance) | Contoso migre une application Windows locale vers une application web Azure et la base de données de l’application vers Azure SQL Database Managed Instance à l’aide d’Azure Database Migration Service.
[Article 11 : Refactoriser une application Linux vers une application web Azure et Azure Database pour MySQL](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-refactor-linux-app-service-mysql) | Contoso migre son application osTicket Linux vers une application web Azure dans plusieurs régions Azure à l’aide d’Azure Traffic Manager, intégré à GitHub de façon à assurer une livraison continue. Contoso migre la base de données d’application vers une instance d’Azure Database pour MySQL. 
[Article 12 : Refactoriser Team Foundation Server sur Azure DevOps Services](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-tfs-vsts) | Contoso migre son déploiement local de Team Foundation Server vers Azure DevOps Services dans Azure.
[Article 13 : Regénérer une application dans Azure](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rebuild) | Contoso régénère son application SmartHotel à l’aide d’une série de capacités et services Azure, notamment Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services et Azure Cosmos DB.
[Article 14 : Mettre à l’échelle une migration vers Azure](/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-scale) | Après des essais de différentes combinaisons de migration, Contoso se prépare à une migration complète vers Azure.



## <a name="next-steps"></a>Étapes suivantes

- [Découvrez](/azure/architecture/cloud-adoption/migrate/) la migration cloud.
- Découvrez les stratégies de migration pour les autres scénarios (paires source-cible) dans le [guide de migration de base de données](https://datamigration.microsoft.com/).
