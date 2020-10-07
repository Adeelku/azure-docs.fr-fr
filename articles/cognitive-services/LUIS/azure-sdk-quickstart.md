---
title: 'Démarrage rapide : Bibliothèques de client du SDK Language Understanding (LUIS)'
description: Créez et interrogez une application LUIS avec les bibliothèques de client du SDK LUIS à l’aide de ce guide de démarrage rapide en utilisant C#, Python ou JavaScript.
ms.topic: quickstart
ms.date: 09/14/2020
ms.service: cognitive-services
ms.subservice: language-understanding
keywords: azure, intelligence artificielle, ia, traitement en langage naturel, tln, LUIS azure luis, compréhension du langage naturel, chatbot ia, créateur de chatbot, comprendre le langage naturel
ms.custom: devx-track-python, devx-track-js, devx-track-csharp, cog-serv-seo-aug-2020
zone_pivot_groups: programming-languages-set-diberry-3core
ms.openlocfilehash: c2bc607fb5a5b5b38249453a1d0fce833547191f
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91327270"
---
# <a name="quickstart-language-understanding-luis-sdk-client-libraries-to-create-and-query-your-luis-app"></a>Démarrage rapide : Bibliothèques de client du SDK Language Understanding (LUIS) pour créer et interroger votre application LUIS

Créez et interrogez une application d’IA Azure LUIS avec les bibliothèques de client du SDK LUIS en utilisant ce guide de démarrage rapide avec C#, Python ou JavaScript.

Language Understanding (LUIS) vous permet d’appliquer un traitement en langage naturel au texte en langage naturel des conversations d’un utilisateur afin d’en prédire le sens général, et d’en extraire des informations détaillées et pertinentes.

* La bibliothèque de client du **SDK de création** vous permet de créer, de modifier, d’entraîner et de publier votre application LUIS. * La bibliothèque de client **SDK du runtime de prédiction** vous permet d’interroger l’application publiée.

::: zone pivot="programming-language-csharp"
[!INCLUDE [LUIS development with C# SDK](./includes/sdk-csharp.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [LUIS development with Node.js SDK](./includes/sdk-nodejs.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [LUIS development with Python SDK](./includes/sdk-python.md)]
::: zone-end

## <a name="clean-up-resources"></a>Nettoyer les ressources

Vous pouvez supprimer l’application à partir du [portail LUIS](https://www.luis.ai) et supprimer les ressources Azure du [portail Azure](https://portal.azure.com/).

## <a name="troubleshooting"></a>Dépannage

* Authentification auprès de la bibliothèque de client : les erreurs d’authentification indiquent généralement qu’une clé et un point de terminaison incorrects ont été utilisés. Pour des raisons pratiques, ce guide de démarrage rapide utilise la clé de création et le point de terminaison de création pour le runtime de prédiction, mais elles fonctionneront seulement si vous n’avez pas déjà utilisé le quota mensuel. Si vous ne pouvez pas utiliser la clé et le point de terminaison de création, vous devez utiliser la clé et le point de terminaison du runtime de prédiction lors de l’accès à la bibliothèque de client du SDK du runtime de prédiction.
* Création d’entités : si vous obtenez une erreur lors de la création de l’entité de machine learning imbriquée utilisée dans ce tutoriel, vérifiez que vous avez copié le code et que vous ne l’avez pas modifié pour créer une entité différente.
* Création d’exemples d’énoncés : si vous obtenez une erreur lors de la création de l’exemple d’énoncé étiqueté utilisé dans ce tutoriel, vérifiez que vous avez copié le code et que vous ne l’avez pas modifié pour créer un exemple étiqueté différent.
* Entraînement : si vous obtenez une erreur d’entraînement, cela indique généralement une application vide (sans intentions avec les exemples d’énoncés) ou une application avec des intentions ou des entités mal formées.
* Erreurs diverses : étant donné que le code appelle les bibliothèques de client avec du texte et des objets JSON, vérifiez que vous n’avez pas modifié le code.

Autres erreurs : si une erreur non couverte dans la liste précédente s’affiche, faites-le nous savoir en indiquant vos commentaires en bas de cette page. Incluez le langage de programmation et la version des bibliothèques de client que vous avez installés.

## <a name="next-steps"></a>Étapes suivantes

* [Qu’est-ce que l’API Language Understanding (LUIS) ?](what-is-luis.md)
* [Nouveautés](whats-new.md)
* [Intentions](luis-concept-intent.md), [entités](luis-concept-entity-types.md), [exemples d’énoncés](luis-concept-utterance.md) et [entités prédéfinies](luis-reference-prebuilt-entities.md)
* Le code source de cet exemple est disponible sur [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code).
* Comprendre le langage naturel : [compréhension du langage naturel (CLN) et traitement en langage naturel (TLN)](artificial-intelligence.md)
* Bots : [Chatbots d’IA](luis-csharp-tutorial-bf-v4.md "tutoriel - créateur de chatbot")
