---
title: 'Démarrage rapide : Vérifier l’orthographe avec le kit SDK Vérification orthographique Bing pour C#'
titleSuffix: Azure Cognitive Services
description: Commencez à utiliser l’API REST Vérification orthographique Bing pour vérifier l’orthographe et la grammaire.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-spell-check
ms.topic: quickstart
ms.date: 12/16/2019
ms.author: aahi
ms.custom: devx-track-csharp
ms.openlocfilehash: e1e05ca9b63bda3373afb8a090118953d89ad8f9
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "88934223"
---
# <a name="quickstart-check-spelling-with-the-bing-spell-check-sdk-for-c"></a>Démarrage rapide : Vérifier l’orthographe avec le kit SDK Vérification orthographique Bing pour C#

Utilisez ce guide de démarrage rapide pour commencer la vérification orthographique avec le kit SDK Vérification orthographique Bing pour C#. Si l’outil Vérification orthographique Bing a une API REST compatible avec la plupart des langages de programmation, le kit SDK offre quant à lui un moyen facile d’intégrer le service à vos applications. Le code source de cet exemple est disponible sur [GitHub](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/samples/SpellCheck).

## <a name="application-dependencies"></a>Dépendances de l’application

* N’importe quelle édition de [Visual Studio 2017 ou ultérieure](https://visualstudio.microsoft.com/downloads/).
* [Package NuGet](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.SpellCheck) Vérification orthographique Bing

Pour ajouter le kit SDK Vérification orthographique Bing à votre projet, sélectionnez **Gérer les packages NuGet** à partir de l’**Explorateur de solutions** dans Visual Studio. Ajoutez le package `Microsoft.Azure.CognitiveServices.Language.SpellCheck`. Le package installe également les dépendances suivantes :

* Microsoft.Rest.ClientRuntime
* Microsoft.Rest.ClientRuntime.Azure
* Newtonsoft.Json

[!INCLUDE [cognitive-services-bing-spell-check-signup-requirements](../../../includes/cognitive-services-bing-spell-check-signup-requirements.md)]

## <a name="create-and-initialize-the-application"></a>Créer et initialiser l’application

1. Créez une solution console en C# dans Visual Studio. Ajoutez ensuite l’instruction `using` suivante.
    
    ```csharp
    using System;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.Azure.CognitiveServices.Language.SpellCheck;
    using Microsoft.Azure.CognitiveServices.Language.SpellCheck.Models;
    ```

2. Créez une classe. Créez ensuite une fonction asynchrone appelée `SpellCheckCorrection()` qui prend une clé d’abonnement et envoie la demande de vérification orthographique.

3. Instanciez le client en créant un objet `ApiKeyServiceClientCredentials`. 

    ```csharp
    public static class SpellCheckSample{
        public static async Task SpellCheckCorrection(string key){
            var client = new SpellCheckClient(new ApiKeyServiceClientCredentials(key));
        }
        //...
    }
    ```

## <a name="send-the-request-and-read-the-response"></a>Envoyer la demande et lire la réponse

1. Dans la fonction créée ci-dessus, effectuez les étapes suivantes. Envoyez la demande de vérification orthographique avec le client. Ajoutez le texte à vérifier au paramètre `text` et définissez le mode sur `proof`.  
    
    ```csharp
    var result = await client.SpellCheckerWithHttpMessagesAsync(text: "Bill Gatas", mode: "proof");
    ```

2. Obtenez le premier résultat de la vérification orthographique, le cas échéant. Imprimez le premier mot (jeton) mal orthographié retourné, le type de jeton et le nombre de suggestions.

    ```csharp
    var firstspellCheckResult = result.Body.FlaggedTokens.FirstOrDefault();
    
    if (firstspellCheckResult != null)
    {
        Console.WriteLine("SpellCheck Results#{0}", result.Body.FlaggedTokens.Count);
        Console.WriteLine("First SpellCheck Result token: {0} ", firstspellCheckResult.Token);
        Console.WriteLine("First SpellCheck Result Type: {0} ", firstspellCheckResult.Type);
        Console.WriteLine("First SpellCheck Result Suggestion Count: {0} ", firstspellCheckResult.Suggestions.Count);
    }
    ```

3. Obtenez la première suggestion de correction, s’il en existe une. Affichez le score de suggestion et le mot suggéré. 

    ```csharp
    var suggestions = firstspellCheckResult.Suggestions;

    if (suggestions?.Count > 0)
    {
        var firstSuggestion = suggestions.FirstOrDefault();
        Console.WriteLine("First SpellCheck Suggestion Score: {0} ", firstSuggestion.Score);
        Console.WriteLine("First SpellCheck Suggestion : {0} ", firstSuggestion.Suggestion);
    }
    ```

## <a name="run-the-application"></a>Exécution de l'application

Créez et exécutez votre projet. Si vous utilisez Visual Studio, appuyez sur **F5** pour déboguer le fichier.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créer une application web monopage](tutorials/spellcheck.md)

- [Qu’est-ce que l’API Vérification orthographique Bing ?](overview.md)
- [Guide de référence du SDK C# de Vérification orthographique Bing](https://docs.microsoft.com/dotnet/api/overview/azure/cognitiveservices/client/bingspellcheck?view=azure-dotnet)
