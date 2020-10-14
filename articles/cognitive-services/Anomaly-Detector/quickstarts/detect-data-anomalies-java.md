---
title: 'Démarrage rapide : Détecter des anomalies dans vos données de séries chronologiques avec l’API Détecteur d’anomalies et Java'
titleSuffix: Azure Cognitive Services
description: Découvrez comment utiliser l’API Détecteur d’anomalies pour détecter les anomalies dans vos séries de données, soit par lot, soit sur des données de streaming.
services: cognitive-services
author: mrbullwinkle
manager: nitinme
ms.service: cognitive-services
ms.subservice: anomaly-detector
ms.topic: quickstart
ms.date: 09/03/2020
ms.custom: devx-track-java
ms.author: mbullwin
ms.openlocfilehash: e23e9016b53a1d9f99809d792d710f865918a098
ms.sourcegitcommit: 2c586a0fbec6968205f3dc2af20e89e01f1b74b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92019679"
---
# <a name="quickstart-detect-anomalies-in-your-time-series-data-using-the-anomaly-detector-rest-api-and-java"></a>Démarrage rapide : Détecter des anomalies dans vos données de séries chronologiques avec l’API Détecteur d’anomalies et Java

Utilisez ce guide de démarrage rapide pour commencer à utiliser les deux modes de détection de l’API Détecteur d’anomalies afin de détecter les anomalies dans vos données de séries chronologiques. Cette application Java envoie les demandes d’API contenant des données de série chronologique au format JSON et obtient les réponses.

| Requête d’API                                        | Sortie de l’application                                                                                                                         |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Détecter des anomalies par lot                        | La réponse JSON contenant l’état de l’anomalie (et d’autres données) pour chaque point de données dans les données de la série chronologique, et les positions des anomalies détectées. |
| Détecter l’état d’anomalie du dernier point de données | La réponse JSON contenant l’état de l’anomalie (et d’autres données) pour le dernier point de données dans les données de série chronologique.   |
| Détecter les points de changement qui marquent les nouvelles tendances des données | Réponse JSON contenant les points de changement détectés dans les données de série chronologique. |

Bien que cette application soit écrite en Java, l’API est un service web RESTful compatible avec la plupart des langages de programmation. Vous trouverez le code source de ce guide de démarrage rapide sur [GitHub](https://github.com/Azure-Samples/AnomalyDetector/blob/master/quickstarts/java-detect-anomalies.java).

## <a name="prerequisites"></a>Prérequis

- Abonnement Azure - [En créer un gratuitement](https://azure.microsoft.com/free/cognitive-services)
- Une fois que vous avez votre abonnement Azure, <a href="https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesAnomalyDetector"  title="Créer une ressource Détecteur d’anomalies"  target="_blank">créez une ressource Détecteur d’anomalies <span class="docon docon-navigate-external x-hidden-focus"></span></a> dans le portail Azure pour obtenir votre clé et votre point de terminaison. Attendez qu’elle se déploie, puis cliquez sur le bouton **Accéder à la ressource**.
    - Vous aurez besoin de la clé et du point de terminaison de la ressource que vous créez pour connecter votre application à l’API Détecteur d’anomalies. Vous collerez votre clé et votre point de terminaison dans le code ci-dessous plus loin dans le guide de démarrage rapide.
    Vous pouvez utiliser le niveau tarifaire Gratuit (`F0`) pour tester le service, puis passer par la suite à un niveau payant pour la production.
- [Kit de développement Java&trade; (JDK) 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) ou version ultérieure
- Importez ces bibliothèques à partir du référentiel Maven :
    - Package [JSON en Java](https://mvnrepository.com/artifact/org.json/json)
    - Package [Apache HttpClient](https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient)

- Fichier JSON contenant des points de données de séries chronologiques. Les exemples de données ce guide de démarrage rapide sont disponibles sur [GitHub](https://github.com/Azure-Samples/anomalydetector/blob/master/example-data/request-data.json).

[!INCLUDE [anomaly-detector-environment-variables](../includes/environment-variables.md)]

## <a name="create-a-new-application"></a>Créer une application

1. Créez un projet Java et importez les bibliothèques suivantes.

    [!code-java[Import statements](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=imports)]

2. Créez des variables pour votre clé d’abonnement et votre point de terminaison. Voici les URI que vous pouvez utiliser pour la détection d’anomalies. Ceux-ci seront ajoutés ultérieurement à votre point de terminaison de service pour créer les URL de requête de l’API.

    |Méthode de détection  |URI  |
    |---------|---------|
    |Détection par lot    | `/anomalydetector/v1.0/timeseries/entire/detect`        |
    |Détection sur le dernier point de données     | `/anomalydetector/v1.0/timeseries/last/detect`        |
    | Détection des points de changement | `/anomalydetector/v1.0/timeseries/changepoint/detect`   |

    [!code-java[Initial key and endpoint variables](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=vars)]

## <a name="create-a-function-to-send-requests"></a>Créer une fonction pour envoyer des requêtes

1. Créez une fonction appelée `sendRequest()` qui sélectionne les variables créées précédemment. Ensuite, effectuez les étapes suivantes.

2. Créez un objet `CloseableHttpClient` qui peut envoyer des requêtes à l’API. Envoyez la requête à un objet de requête `HttpPost` en combinant votre point de terminaison et une URL Détecteur d’anomalies.

3. Utilisez la fonction `setHeader()` de la requête pour affecter la valeur `application/json` à l’en-tête `Content-Type`, et ajoutez votre clé d’abonnement à l’en-tête `Ocp-Apim-Subscription-Key`.

4. Utilisez la fonction `setEntity()` de la requête sur les données à envoyer.

5. Utilisez la fonction `execute()` du client pour envoyer la requête, et enregistrez-la dans un objet `CloseableHttpResponse`.

6. Créez un objet `HttpEntity` pour stocker le contenu de la réponse. Obtenez le contenu avec `getEntity()`. Si la réponse n’est pas vide, retournez-la.

    [!code-java[API request method](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=request)]

## <a name="detect-anomalies-as-a-batch"></a>Détecter des anomalies par lot

1. Créez une méthode appelée `detectAnomaliesBatch()` pour détecter les anomalies dans le jeu de données sous forme de lot. Appelez la méthode `sendRequest()` créée ci-dessus avec votre point de terminaison, l’URL, la clé d’abonnement et les données JSON. Obtenez le résultat et imprimez-le dans la console.

2. Si la réponse contient un champ `code`, imprimez le code d’erreur et le message d’erreur.

3. Sinon, trouvez les positions des anomalies dans le jeu de données. Le champ `isAnomaly` de la réponse contient une valeur booléenne indiquant si un point de données particulier est une anomalie. Obtenez et effectuez une itération au sein du tableau JSON, en imprimant l’index des valeurs `true`. Ces valeurs correspondent à l’index des points de données anormaux, le cas échéant.

    [!code-java[Method for batch detection](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=detectBatch)]

## <a name="detect-the-anomaly-status-of-the-latest-data-point"></a>Détecter l’état d’anomalie du dernier point de données

Créez une méthode appelée `detectAnomaliesLatest()` pour détecter l’état d’anomalie du dernier point de données dans le jeu de données. Appelez la méthode `sendRequest()` créée ci-dessus avec votre point de terminaison, l’URL, la clé d’abonnement et les données JSON. Obtenez le résultat et imprimez-le dans la console.

[!code-java[Latest point detection method](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=detectLatest)]


## <a name="detect-change-points-in-the-data"></a>Détecter les points de changement dans les données

1. Créez une méthode appelée `detectChangePoints()` pour détecter les anomalies dans le jeu de données sous forme de lot. Appelez la méthode `sendRequest()` créée ci-dessus avec votre point de terminaison, l’URL, la clé d’abonnement et les données JSON. Obtenez le résultat et imprimez-le dans la console.

2. Si la réponse contient un champ `code`, imprimez le code d’erreur et le message d’erreur.

3. Sinon, recherchez les positions des points de changement dans le jeu de données. Le champ `isChangePoint` de la réponse contient une valeur booléenne indiquant si un point de données particulier est un point de changement de tendance. Obtenez le tableau JSON et effectuez-y une itération, en imprimant l’indice des valeurs `true`. Ces valeurs correspondent aux indices des points de changement de tendance, si de tels points sont trouvés.

    [!code-java[detect change points](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=detectChangePoint)]

## <a name="load-your-time-series-data-and-send-the-request"></a>Charger vos données de série chronologique et envoyer la requête

1. Dans la méthode Main de votre application, lisez le fichier JSON contenant les données qui seront ajoutées aux requêtes.

2. Appelez les deux fonctions de détection d’anomalie créées plus haut.

    [!code-java[Main method](~/samples-anomaly-detector/quickstarts/java-detect-anomalies.java?name=main)]

### <a name="example-response"></a>Exemple de réponse

Une réponse correcte est retournée au format JSON. Cliquez sur les liens ci-dessous pour afficher la réponse JSON sur GitHub :
* [Exemple de réponse de détection par lots](https://github.com/Azure-Samples/anomalydetector/blob/master/example-data/batch-response.json)
* [Exemple de dernière réponse de détection de points](https://github.com/Azure-Samples/anomalydetector/blob/master/example-data/latest-point-response.json)
* [Exemple de réponse de détection de points de changement](https://github.com/Azure-Samples/anomalydetector/blob/master/example-data/change-point-sample.json)

[!INCLUDE [anomaly-detector-next-steps](../includes/quickstart-cleanup-next-steps.md)]
