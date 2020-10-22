---
title: Niveaux de cohérence et API Azure Cosmos DB
description: Comprendre le mappage des niveaux de cohérence entre les différentes API dans Azure Cosmos DB, Apache Cassandra et MongoDB
author: markjbrown
ms.author: mjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 08/6/2020
ms.reviewer: sngun
ms.openlocfilehash: bb8a413f2e2a3aa4a8facd533d822312bb61fa0e
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91613558"
---
# <a name="consistency-levels-and-azure-cosmos-db-apis"></a>Niveaux de cohérence et API Azure Cosmos DB

Azure Cosmos DB fournit la prise en charge native des API compatibles avec les protocoles filaires pour les bases de données les plus courantes. Ces bases de données incluent le stockage Table Azure, MongoDB, Apache Cassandra et Gremlin. Elles n’offrent pas de modèle de cohérence défini avec précision, ni de garantie reposant sur un contrat SLA pour les niveaux de cohérence. Elles ne fournissent généralement qu’un sous-ensemble des cinq modèles de cohérence offerts par Azure Cosmos DB.

Pour les API SQL, Gremlin et Table, le niveau de cohérence configuré par défaut sur le compte Azure Cosmos est utilisé. 

Lorsque vous utilisez l’API Cassandra ou l’API Azure Cosmos DB pour MongoDB, les applications obtiennent un ensemble complet de niveaux de cohérence proposés par Apache Cassandra et MongoDB, respectivement, avec des garanties encore plus fortes de cohérence et de durabilité. Ce document présente les niveaux de cohérence Azure Cosmos DB correspondants pour les niveaux de cohérence Apache Cassandra et MongoDB.

> [!NOTE]
> Le modèle de cohérence par défaut pour Azure Cosmos DB est Session. Session est un modèle de cohérence centré sur le client qui n’est pas pris en charge nativement par Cassandra ni MongoDB. Pour plus d’informations sur le modèle de cohérence à choisir, consultez [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).

## <a name="mapping-between-apache-cassandra-and-azure-cosmos-db-consistency-levels"></a><a id="cassandra-mapping"></a>Mappage entre les niveaux de cohérence Apache Cassandra et Azure Cosmos DB

Contrairement à Azure Cosmos DB, Apache Cassandra ne fournit pas en mode natif des garanties de cohérence précises.  Au lieu de cela, Apache Cassandra fournit un niveau de cohérence d’écriture et un niveau de cohérence de lecture, pour permettre les compromis de haute disponibilité, de cohérence et de latence. Lors de l’utilisation de l’API Cassandra Azure Cosmos DB : 

* Le niveau de cohérence d’écriture d’Apache Cassandra est mappé au niveau de cohérence par défaut configuré sur votre compte Azure Cosmos. La cohérence d’une opération d’écriture ne peut pas être changée en fonction de la demande.

* Azure Cosmos DB mappe de manière dynamique le niveau de cohérence de lecture spécifié par le pilote client Cassandra à l’un des niveaux de cohérence Azure Cosmos DB configurés dynamiquement sur une requête de lecture. 

Le tableau suivant illustre le mappage des niveaux de cohérence Cassandra en mode natif aux niveaux de cohérence d’Azure Cosmos DB lors de l’utilisation de l’API Cassandra :  

:::image type="content" source="./media/consistency-levels-across-apis/consistency-model-mapping-cassandra.png" alt-text="Mappage du modèle de cohérence Cassandra" lightbox="./media/consistency-levels-across-apis/consistency-model-mapping-cassandra.png" :::

## <a name="mapping-between-mongodb-and-azure-cosmos-db-consistency-levels"></a><a id="mongo-mapping"></a>Mappage entre les niveaux de cohérence MongoDB et Azure Cosmos DB

Contrairement à Azure Cosmos DB, MongoDB en mode natif ne fournit pas de garanties de cohérence précises. Au lieu de cela, MongoDB en mode natif permet aux utilisateurs de configurer les garanties de cohérence suivantes : problème d’écriture, problème de lecture et directive isMaster - pour diriger les opérations de lecture vers les réplicas principaux ou secondaires dans l’optique d’atteindre le niveau de cohérence souhaité.

Lorsque vous utilisez l’API Azure Cosmos DB pour MongoDB, le pilote MongoDB traite votre région d’écriture en tant que réplica principal, et toutes les autres régions sont des réplicas en lecture. Vous pouvez choisir la région associée à votre compte Azure Cosmos en tant que réplica principal. 

Lors de l’utilisation de l’API Azure Cosmos DB pour MongoDB :

* Le problème d’écriture est mappé au niveau de cohérence par défaut configuré sur votre compte Azure Cosmos.

* Azure Cosmos DB mappe de manière dynamique le problème de lecture spécifié par le pilote client MongoDB à l’un des niveaux de cohérence Azure Cosmos DB configurés dynamiquement sur une requête de lecture.  

* Vous pouvez annoter une région associée à votre compte Azure Cosmos comme étant « Primaire », en la désignant comme première région accessible en écriture. 

Le tableau suivant illustre le mappage des problèmes d’écriture/lecture Cassandra en mode natif aux niveaux de cohérence d’Azure Cosmos lors de l’utilisation de l’API Azure Cosmos DB pour MongoDB :

:::image type="content" source="./media/consistency-levels-across-apis/consistency-model-mapping-mongodb.png" alt-text="Mappage du modèle de cohérence Cassandra" lightbox= "./media/consistency-levels-across-apis/consistency-model-mapping-mongodb.png":::

## <a name="next-steps"></a>Étapes suivantes

Apprenez-en davantage sur les niveaux de cohérence et la compatibilité entre les API Cosmos DB et les API open source. Voir les articles suivants :

* [Compromis entre disponibilité et performance pour différents niveaux de cohérence](consistency-levels-tradeoffs.md)
* [Fonctionnalités MongoDB prises en charge par l’API d’Azure Cosmos DB pour MongoDB](mongodb-feature-support.md)
* [Fonctionnalités Apache Cassandra prises en charge par l’API Cassandra pour Azure Cosmos DB](cassandra-support.md)
