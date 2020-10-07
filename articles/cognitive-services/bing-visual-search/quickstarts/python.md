---
title: 'Démarrage rapide : Obtenir des insights sur des images avec l’API REST et Python - Recherche visuelle Bing'
titleSuffix: Azure Cognitive Services
description: Découvrez comment charger une image à l’aide de l’API Recherche visuelle Bing et Python, puis obtenez des insights sur l’image.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-visual-search
ms.topic: quickstart
ms.date: 05/22/2020
ms.author: scottwhi
ms.custom: devx-track-python
ms.openlocfilehash: ef265ab0cff9514695b40995e842518803e2e4c0
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91324584"
---
# <a name="quickstart-get-image-insights-using-the-bing-visual-search-rest-api-and-python"></a>Démarrage rapide : Obtenir des insights sur les images à l’aide de l’API REST Recherche visuelle Bing et de Python

Utilisez ce guide de démarrage rapide pour effectuer votre premier appel à l’API Recherche visuelle Bing. Cette application Python charge une image dans l’API et affiche les informations qu’elle retourne. Bien que cette application soit écrite en Python, l’API est un service web RESTful compatible avec la plupart des langages de programmation.

## <a name="prerequisites"></a>Prérequis

* [Python 3.x](https://www.python.org/)

[!INCLUDE [cognitive-services-bing-visual-search-signup-requirements](../../../../includes/cognitive-services-bing-visual-search-signup-requirements.md)]

## <a name="initialize-the-application"></a>Initialiser l’application

1. Créez un fichier Python dans votre IDE ou votre éditeur favori, puis ajoutez l’instruction `import` suivante :

    ```python
    import requests, json
    ```

2. Créez les variables pour votre clé d’abonnement, le point de terminaison et le chemin de l’image que vous chargez. Pour la valeur de `BASE_URI`, vous pouvez utiliser le point de terminaison global ci-dessous, ou le point de terminaison de [sous-domaine personnalisé](../../../cognitive-services/cognitive-services-custom-subdomains.md) affiché dans le portail Azure pour votre ressource.

    ```python

    BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'
    SUBSCRIPTION_KEY = 'your-subscription-key'
    imagePath = 'your-image-path'
    ```
    
3. Quand vous chargez une image locale, les données de formulaire doivent inclure l’en-tête `Content-Disposition`. Définissez son paramètre `name` sur « image » et le paramètre `filename` sur le nom de fichier de votre image. Le contenu du formulaire inclut les données binaires de l’image. La taille maximale de l’image que vous chargez est de 1 Mo.
    
    ```
    --boundary_1234-abcd
    Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"
    
    ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...
    
    --boundary_1234-abcd--
    ```

4. Créez un objet de dictionnaire pour stocker les informations d’en-tête de votre demande. Liez votre clé d’abonnement à la chaîne `Ocp-Apim-Subscription-Key`.

    ```python
    HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}
    ```

5. Créez un autre dictionnaire destiné à contenir votre image, qui est ouverte et chargée quand vous envoyez la demande.

    ```python
    file = {'image' : ('myfile', open(imagePath, 'rb'))}
    ```

## <a name="parse-the-json-response"></a>Analyser la réponse JSON

Créez une méthode appelée `print_json()` pour accepter la réponse de l’API et l’afficher au format JSON.

```python
def print_json(obj):
    """Print the object as json"""
    print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))
```

## <a name="send-the-request"></a>Envoyer la demande

Utilisez `requests.post()` pour envoyer une demande à l’API Recherche visuelle Bing. Incluez la chaîne indiquant les informations relatives au point de terminaison, à l’en-tête et au fichier. Affichez `response.json()` avec `print_json()`.

```python
try:
    response = requests.post(BASE_URI, headers=HEADERS, files=file)
    response.raise_for_status()
    print_json(response.json())
    
except Exception as ex:
    raise ex
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créer une application web monopage de recherche visuelle](../tutorial-bing-visual-search-single-page-app.md)
