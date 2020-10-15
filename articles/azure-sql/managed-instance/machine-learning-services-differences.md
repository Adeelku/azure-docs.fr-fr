---
title: Principales différences de Machine Learning Services (préversion)
description: Cette rubrique décrit les principales différences entre la version Azure SQL Managed Instance et la version SQL Server de Machine Learning Services.
services: sql-database
ms.service: sql-managed-instance
ms.subservice: machine-learning
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: sstein, davidph
manager: cgronlun
ms.date: 05/27/2020
ms.openlocfilehash: 9ff2de18042c466bdd8fa6c71194fff4286c820d
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91325094"
---
# <a name="key-differences-between-machine-learning-services-in-azure-sql-managed-instance-and-sql-server"></a>Principales différences entre la version Azure SQL Managed Instance et la version SQL Server de Machine Learning Services

La fonctionnalité [Machine Learning Services dans Azure SQL Managed Instance (préversion)](machine-learning-services-overview.md) est quasiment identique à [SQL Server Machine Learning Services](https://docs.microsoft.com/sql/advanced-analytics/what-is-sql-server-machine-learning). Il existe cependant quelques différences, présentées ci-dessous.

> [!IMPORTANT]
> Machine Learning Services dans Azure SQL Managed Instance est actuellement en préversion publique. Pour vous inscrire, consultez [S'inscrire à la préversion](machine-learning-services-overview.md#signup).

## <a name="preview-limitations"></a>Limitations de la version préliminaire

Pendant la phase de préversion, le service présente les limitations suivantes :

- Les connexions de bouclage ne fonctionnent pas (voir [Connexion de bouclage à SQL Server à partir d'un script Python ou R](/sql/machine-learning/connect/loopback-connection)).
- Les pools de ressources externes ne sont pas pris en charge.
- Seuls Python et R sont pris en charge. Les langages externes tels que Java ne peuvent pas être ajoutés.
- Les scénarios qui utilisent l'[interface de passage de messages](https://docs.microsoft.com/message-passing-interface/microsoft-mpi) (MPI) ne sont pas pris en charge.

En cas de mise à jour de l'objectif de niveau de service (Service Level Objective - SLO), veuillez procéder à la mise à jour et générer un ticket de support afin de réactiver les limites de ressources dédiées pour R/Python.

## <a name="language-support"></a>Support multilingue

Les versions SQL Managed Instance et SQL Server de Machine Learning Services prennent en charge l'[infrastructure d'extensibilité](https://docs.microsoft.com/sql/advanced-analytics/concepts/extensibility-framework) de Python et R. :

- Les versions SQL Managed Instance et SQL Server de Machine Learning Services n'utilisent pas les mêmes versions initiales de Python et R :

  | Système               | Python | R     |
  |----------------------|--------|-------|
  | Instance managée SQL | 3.7.1  | 3.5.2 |
  | SQL Server           | 3.5.2  | 3.3.3 |

- Il n’est pas nécessaire de configurer `external scripts enabled` avec `sp_configure`. Une fois que vous êtes [inscrit](machine-learning-services-overview.md#signup) à la préversion, le machine learning est activé pour SQL Managed Instance.

## <a name="packages"></a>.

La gestion des packages Python et R fonctionne différemment dans SQL Managed Instance et SQL Server. :

- Les packages ne peuvent pas effectuer d’appels réseau sortants. Cette limitation est semblable aux [règles de pare-feu par défaut de Machine Learning Services](https://docs.microsoft.com//sql/advanced-analytics/security/firewall-configuration) dans SQL Server, mais elle n'est pas modifiable dans SQL Managed Instance.
- Les packages qui dépendent de runtimes externes (comme Java) ou dont l’installation ou l’utilisation impliquent un accès à des API de système d’exploitation ne sont pas pris en charge.

Pour plus d'informations sur la gestion des packages Python et R, consultez :

- [Obtenir des informations sur les packages Python](https://docs.microsoft.com/sql/machine-learning/package-management/python-package-information?context=azure/sql-database/context/ml-context&view=sql-server-ver15)
- [Obtenir des informations sur les packages R](https://docs.microsoft.com/sql/machine-learning/package-management/r-package-information?context=azure/sql-database/context/ml-context&view=sql-server-ver15)

## <a name="resource-governance"></a>Gouvernance des ressources

Il n’est pas possible de limiter les ressources R avec [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) et les listes de ressources externes.

Dans le cadre de la préversion publique, les ressources R englobent au maximum 20 % des ressources SQL Managed Instance, et le pourcentage précis dépend du niveau de service choisi. Pour plus d’informations, voir [Modèles d’achat Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers).

### <a name="insufficient-memory-error"></a>Erreur de mémoire insuffisante

Si la mémoire est insuffisante pour R, un message d’erreur s’affiche. Les messages d’erreur courants sont les suivants :

- Impossible de communiquer avec le runtime pour le script « R » et l’ID de demande *******. Vérifiez les exigences du runtime « R »
- Une erreur de script « R » s’est produite lors de l’exécution de « sp_execute_external_script » avec HRESULT 0x80004004. ...Une erreur de script externe s’est produite : « Impossible d’allouer de la mémoire (0 Mb) dans la fonction C 'R_AllocStringBuffer' »
- Une erreur de script externe s’est produite : Erreur : impossible d’allouer un vecteur de taille.

L’utilisation de la mémoire dépend de la quantité de mémoire utilisée dans vos scripts R et du nombre de requêtes parallèles en cours d’exécution. Si les messages d’erreur ci-dessus s’affichent, vous pouvez augmenter l’échelle votre base de données pour l’adapter à un niveau de service supérieur afin de résoudre ce problème.

## <a name="next-steps"></a>Étapes suivantes

- Consultez la vue d'ensemble, [Machine Learning Services dans Azure SQL Managed Instance](machine-learning-services-overview.md).
- Pour apprendre à utiliser Python dans Machine Learning Services, consultez [Exécuter des scripts Python](https://docs.microsoft.com/sql/machine-learning/tutorials/quickstart-python-create-script?context=/azure/azure-sql/managed-instance/context/ml-context&view=sql-server-ver15).
- Pour apprendre à utiliser R dans Machine Learning Services, consultez [Exécuter des scripts R](https://docs.microsoft.com/sql/machine-learning/tutorials/quickstart-r-create-script?context=/azure/azure-sql/managed-instance/context/ml-context&view=sql-server-ver15).
