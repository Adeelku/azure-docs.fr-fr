---
title: Utiliser SQL dynamique dans SQL Synapse
description: Conseils d'utilisation de SQL dynamique dans SQL Synapse.
services: synapse-analytics
author: filippopovic
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql
ms.date: 04/15/2020
ms.author: fipopovi
ms.reviewer: jrasnick
ms.custom: ''
ms.openlocfilehash: 4a4ce92278d5f6704fec4a5b9d30b44ddf89b0ad
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "90033436"
---
# <a name="dynamic-sql-in-synapse-sql"></a>SQL dynamique dans SQL Synapse
Cet article fournit des conseils pour l’utilisation de SQL dynamique et le développement de solutions avec SQL Synapse.

## <a name="dynamic-sql-example"></a>Exemple de SQL dynamique

Lorsque vous développez le code d’une application, vous pouvez avoir besoin d’utiliser un SQL dynamique de façon à offrir des solutions flexibles, génériques et modulaires.

> [!NOTE]
> Actuellement, le pool SQL ne prend pas en charge les types de données blob. Le fait de ne pas prendre en charge les types de données blob peut limiter la taille de vos chaînes, car les types de données blob incluent les types varchar(max) et nvarchar(max). Si vous avez utilisé ces types dans votre code d’application pour générer de grandes chaînes, vous devez arrêter le code en blocs et utiliser l’instruction EXEC à la place.

Voici un exemple simple :

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Si la chaîne est courte, vous pouvez utiliser [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest) normalement.

> [!NOTE]
> Les instructions exécutées en tant que SQL dynamique sont toujours soumises à l’ensemble des règles de validation T-SQL.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des conseils supplémentaires, consultez la [vue d’ensemble du développement](develop-overview.md).
