---
title: 'Démarrage rapide : Configuration de la plateforme du kit SDK Speech pour C# sous Unity – Service Speech'
titleSuffix: Azure Cognitive Services
description: Utilisez ce guide pour configurer votre plateforme pour C# sous Unity avec le kit SDK du service Speech.
services: cognitive-services
author: markamos
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: include
ms.date: 10/10/2019
ms.author: erhopf
ms.custom: devx-track-csharp
ms.openlocfilehash: 7678ffa1684fb1fe1ea198e9e1836a152cd51b4b
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "88926645"
---
Ce guide explique comment installer le [Kit de développement logiciel (SDK) Speech](~/articles/cognitive-services/speech-service/speech-sdk.md) pour [Unity](https://unity3d.com/).

> [!NOTE]
> Le SDK Speech pour Unity prend en charge Windows Desktop (x86 et x64), ou la plateforme Windows universelle (x86, x64, ARM/ARM64), Android (x86, ARM32/64) et iOS (simulateur x64, ARM32 et ARM64).

[!INCLUDE [License Notice](~/includes/cognitive-services-speech-service-license-notice.md)]

## <a name="prerequisites"></a>Prérequis

Ce démarrage rapide nécessite :

- [Unity version 2018.3 ou ultérieure](https://store.unity.com/) avec [Unity 2019.1 pour la prise en charge d’UWP ARM64](https://blogs.unity3d.com/2019/04/16/introducing-unity-2019-1/#universal).
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/). La version 15.9 (ou une version ultérieure) de Visual Studio 2017 peut également être utilisée.
- Pour la prise en charge de Windows ARM64, installez les [outils de génération facultatifs pour ARM64 et le SDK Windows 10 pour ARM64](https://blogs.windows.com/buildingapps/2018/11/15/official-support-for-windows-10-on-arm-development/).

## <a name="install-the-speech-sdk"></a>Installer le Kit de développement logiciel (SDK) Speech

Pour installer le SDK Speech pour Unity, procédez comme suit :

1. Téléchargez et ouvrez le [Kit de développement logiciel (SDK) pour Unity](https://aka.ms/csspeech/unitypackage) fourni sous la forme d’un package de ressources Unity (.unitypackage) qui devrait déjà être associé avec Unity. Une fois le package de ressources ouvert, la boîte de dialogue **Import Unity Package** s’affiche. Pour que cette étape fonctionne, il se peut que vous deviez créer et ouvrir un projet vide.

   [![Boîte de dialogue Import Unity Package de l’éditeur Unity](~/articles/cognitive-services/speech-service/media/sdk/qs-csharp-unity-01-import.png)](~/articles/cognitive-services/speech-service/media/sdk/qs-csharp-unity-01-import.png#lightbox)

1. Vérifiez que tous les fichiers sont sélectionnés, puis cliquez sur **Import**. Après quelques instants, le package de ressources Unity est importé dans votre projet.

Pour plus d’informations sur l’importation de packages de ressources dans Unity, consultez la [documentation Unity](https://docs.unity3d.com/Manual/AssetPackages.html).

Vous pouvez maintenant passer aux [étapes suivantes](#next-steps) ci-dessous.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [windows](../quickstart-list.md)]
