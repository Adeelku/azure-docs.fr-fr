---
title: Qu’est-ce que l’API Recherche d’entités Bing ?
titleSuffix: Azure Cognitive Services
description: Découvrez l’API Recherche d’entités Bing et la façon d’extraire et de rechercher des entités et des lieux à partir de requêtes de recherche.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-entity-search
ms.topic: overview
ms.date: 12/18/2019
ms.author: scottwhi
ms.openlocfilehash: e0402b1695e1d5f5c9f29d128f4cd405f219e724
ms.sourcegitcommit: 03662d76a816e98cfc85462cbe9705f6890ed638
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90532492"
---
# <a name="what-is-bing-entity-search-api"></a>Qu’est-ce que l’API Recherche d’entités Bing ?

L’API Recherche d’entités Bing envoie une requête de recherche à Bing et obtient des résultats comprenant des entités et des lieux. Les résultats de lieux incluent les restaurants, les hôtels et d’autres commerces locaux. Bing renvoie des lieux si la requête spécifie le nom de l’entreprise locale ou demande un type d’entreprise (par exemple, les restaurants à proximité). Bing renvoie des entités si la requête indique des personnes, des lieux (sites touristiques, États, pays/régions, etc.) ou des éléments connus.

|Fonctionnalité  |Description  |
|---------|---------|
|[Suggestions de recherche en temps réel](concepts/search-for-entities.md#suggest-search-terms-with-the-bing-autosuggest-api)     | Fournir des suggestions de recherche qui peuvent être affichées sous forme de liste déroulante, au fur et à mesure que l’utilisateur tape un texte au clavier.       | 
| [Désambiguïsation d’entités](concepts/search-for-entities.md#the-bing-entity-search-api-response)  | Obtenez plusieurs entités pour les requêtes impliquant plusieurs significations possibles. |
| [Recherche de lieux](concepts/search-for-entities.md#find-places) | Recherchez et retournez des informations sur les entités et les entreprises locales.  |

## <a name="workflow"></a>Workflow

L’API Recherche d’entités Bing étant un service web RESTful, elle peut être facilement appelée à partir de n’importe quel langage de programmation capable d’exécuter des requêtes HTTP et d’analyser des réponses JSON. Vous pouvez utiliser ce service soit par le biais de l’API REST, soit à l’aide du Kit de développement logiciel (SDK).

1. Créez un [compte d’API Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) disposant d’un accès aux API Recherche Bing. Si vous n’avez pas d’abonnement Azure, vous pouvez créer un [compte](https://azure.microsoft.com/free/cognitive-services/) gratuitement.
2. Envoyez une requête à l’API avec une requête de recherche valide.
3. Traitez la réponse de l’API en analysant le message JSON renvoyé.

## <a name="next-steps"></a>Étapes suivantes

* Essayez la [démonstration interactive](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) de l’API Recherche d’entités Bing. 
* Pour configurer rapidement votre première requête, essayez un guide de [démarrage rapide](quickstarts/csharp.md).
* Section de référence sur l’[API Recherche d’entités Bing v7](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-entities-api-v7-reference).
* L’article [Conditions d’utilisation et d’affichage de l’API Recherche Bing](./use-display-requirements.md) spécifie les utilisations acceptables du contenu et des informations obtenus par le biais des API Recherche Bing.
* Visitez la [page hub de l’API Recherche Bing](../bing-web-search/search-the-web.md) pour explorer les autres API disponibles.