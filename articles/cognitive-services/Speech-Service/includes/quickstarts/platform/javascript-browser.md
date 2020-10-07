---
title: 'Démarrage rapide : Configuration de la plateforme du kit SDK Speech pour JavaScript (Navigateur) – Service Speech'
titleSuffix: Azure Cognitive Services
description: Utilisez ce guide pour configurer votre plateforme pour JavaScript (Navigateur) avec le kit SDK du service Speech.
services: cognitive-services
author: markamos
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: include
ms.date: 10/11/2019
ms.author: erhopf
ms.custom: devx-track-js
ms.openlocfilehash: 2701b4cd17a132de07c031166bbe4cb1086227e9
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91324748"
---
Ce guide explique comment installer le [Kit de développement logiciel (SDK) Speech](~/articles/cognitive-services/speech-service/speech-sdk.md) pour JavaScript pour une utilisation avec une page web.

[!INCLUDE [License Notice](~/includes/cognitive-services-speech-service-license-notice.md)]

## <a name="create-a-new-website-folder"></a>Créer un dossier de site web

Créez un dossier vide. Si vous souhaitez héberger l’exemple sur un serveur web, vérifiez que le serveur web peut accéder au dossier.

## <a name="unpack-the-speech-sdk-for-javascript-into-that-folder"></a>Décompresser le SDK Speech pour JavaScript dans ce dossier

Téléchargez le SDK Speech en tant que [package .zip](https://aka.ms/csspeech/jsbrowserpackage), puis décompressez-le dans le dossier que vous venez de créer. Les cinq fichiers suivants sont alors décompressés :
* `microsoft.cognitiveservices.speech.sdk.bundle.js` Une version lisible du kit de développement logiciel (SDK) Speech.
* `microsoft.cognitiveservices.speech.sdk.bundle.js.map` Fichier de mappage utilisé pour déboguer le code du kit de développement logiciel (SDK).
* `microsoft.cognitiveservices.speech.sdk.bundle.d.ts` Définitions d’objets à utiliser avec TypeScript
* `microsoft.cognitiveservices.speech.sdk.bundle-min.js` Une version minimisée du kit de développement logiciel (SDK) Speech.
* `speech-processor.js` Code pour améliorer les performances sur certains navigateurs.

## <a name="create-an-indexhtml-page"></a>Créer une page index.html

Créez un fichier nommé `index.html` dans le dossier, puis ouvrez-le dans un éditeur de texte.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [windows](../quickstart-list.md)]