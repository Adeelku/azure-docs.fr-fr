---
title: Présentation du Stockage Table - Stockage d’objets dans Azure | Microsoft Docs
description: Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL.
services: storage
ms.service: storage
author: tamram
ms.author: tamram
ms.devlang: dotnet
ms.topic: overview
ms.date: 04/23/2018
ms.subservice: tables
ms.openlocfilehash: 2670d9ce568195fd97350bf678059ac89610422f
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "88236163"
---
# <a name="what-is-azure-table-storage-"></a>Qu’est-ce que le Stockage Table Azure ? 

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

Le Stockage Table Azure est un service qui stocke des données NoSQL structurées dans le cloud, en fournissant une conception sans schéma à un magasin de clés/attributs. Comme le stockage de tables est sans schéma, il est aisé d’adapter vos données en fonction des besoins de votre application. L’accès aux données du Stockage Table est rapide et économique pour de nombreux types d’applications, et généralement moins coûteux que le SQL traditionnel pour des volumes de données similaires.

Vous pouvez utiliser le Stockage Table pour stocker des jeux de données flexibles, comme des données utilisateur pour des applications Web, des carnets d’adresses, des informations sur les périphériques ou d’autres types de métadonnées requis par votre service. Vous pouvez stocker un nombre quelconque d'entités dans une table, et un compte de stockage peut contenir un nombre quelconque de tables, jusqu'à la limite de capacité du compte de stockage.

[!INCLUDE [storage-table-concepts-include](../../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a>Étapes suivantes

* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.

* [Prise en main de Stockage Table Azure dans .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)

* Pour plus d'informations sur les API disponibles, consultez la documentation de référence du service de Table :

    * [Référence de la bibliothèque cliente de stockage pour .NET](https://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [Référence d’API REST](https://msdn.microsoft.com/library/azure/dd179355)
