---
title: Se connecter avec sqlcmd
description: Utilisez l’utilitaire de ligne de commande sqlcmd pour établir une connexion avec un pool SQL Synapse et l’interroger.
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 04/17/2018
ms.author: xiaoyul
ms.reviewer: igorstan
ms.custom: seo-lt-2019
ms.openlocfilehash: 2e76f48466d084d448cceea0490e44041e7d062e
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "85212137"
---
# <a name="connect-to-synapse-sql-pool-with-sqlcmd"></a>Se connecter au pool SQL Synapse avec sqlcmd

> [!div class="op_single_selector"]
>
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md)
> * [SSMS](sql-data-warehouse-query-ssms.md)

Utilisez l’utilitaire de ligne de commande [sqlcmd][sqlcmd] pour établir une connexion avec un pool SQL et l’interroger.  

## <a name="1-connect"></a>1. Se connecter

Pour commencer à utiliser [sqlcmd][sqlcmd], ouvrez l’invite de commandes et entrez **sqlcmd** suivi de la chaîne de connexion de la base de données de votre pool SQL. La chaîne de connexion requiert les paramètres suivants :

* **Serveur (-S) :** Serveur, sous la forme `<`Nom_serveur`>`.database.windows.net
* **Base de données (-d) :** Nom de la base de données.
* **Activer les identificateurs entre guillemets (-I) :** Les identificateurs entre guillemets doivent être activés pour permettre la connexion à une instance de pool SQL.

Pour utiliser l’authentification SQL Server, vous devez ajouter les paramètres de nom d’utilisateur/mot de passe :

* **Utilisateur (-U) :** Utilisateur du serveur sous la forme `<`Utilisateur`>`
* **Mot de passe (-P) :** Mot de passe associé à l’utilisateur.

Par exemple, votre chaîne de connexion peut ressembler à ceci :

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Pour utiliser l’authentification Azure Active Directory intégrée, vous devez ajouter les paramètres Azure Active Directory :

* **Authentification Azure Active Directory (-G) :** utilisez Azure Active Directory pour l’authentification

Par exemple, votre chaîne de connexion peut ressembler à ceci :

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> Vous devez [activer l’authentification Azure Active Directory](sql-data-warehouse-authentication.md) pour vous authentifier à l’aide d’Active Directory.

## <a name="2-query"></a>2. Requête

Une fois la connexion établie, vous pouvez envoyer des instructions Transact-SQL prises en charge à l’instance.  Dans cet exemple, les requêtes sont soumises en mode interactif.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Les exemples ci-après vous indiquent comment exécuter vos requêtes en mode batch à l’aide de l’option -Q ou en redirigeant votre SQL vers sqlcmd.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les options disponibles dans sqlcmd, consultez la [documentation de sqlcmd](/sql/tools/sqlcmd-utility?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest).
