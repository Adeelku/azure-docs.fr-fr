---
title: Limites
description: Limitations du code pour les fonctionnalités du SDK
author: erscorms
ms.author: erscor
ms.date: 02/11/2020
ms.topic: reference
ms.openlocfilehash: e6b12c2bac4a9732f868f6a6ac3491ef993f54c3
ms.sourcegitcommit: bdd5c76457b0f0504f4f679a316b959dcfabf1ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90976566"
---
# <a name="limitations"></a>Limites

Un certain nombre de fonctionnalités ont une taille, un nombre ou d’autres limitations.

## <a name="azure-frontend"></a>Azure Frontend

* Nombre total d’instances AzureFrontend par processus : 16.
* Nombre total d’instances AzureSession par AzureFrontend : 16.

## <a name="objects"></a>Objets

* Nombre total d’objets autorisés d’un même type (Entity, CutPlaneComponent, etc.) : 16 777 215.
* Nombre total de plans de coupe actifs autorisés : 8.

## <a name="geometry"></a>Géométrie

* Nombre total des matériaux autorisés dans une ressource : 65 535. Pour plus d’informations, consultez [Déduplication matérielle](../how-tos/conversion/configure-model-conversion.md#material-de-duplication).
* Dimension maximale d’une texture unique 16 384 x 16 384. Les textures sources plus grandes seront mises à l’échelle par le processus de conversion.

## <a name="overall-number-of-polygons"></a>Nombre total de polygones

Le nombre autorisé de polygones pour tous les modèles chargés dépend de la taille de la machine virtuelle transmise à l’[API REST de gestion des sessions](../how-tos/session-rest-api.md#create-a-session) :

| Taille du serveur | Nombre maximal de polygones |
|:--------|:------------------|
|standard| 20 millions |
|Premium| aucune limite |

Pour plus d’informations sur cette limitation, consultez le chapitre sur la [taille de serveur](../reference/vm-sizes.md).

## <a name="platform-limitations"></a>Limitations de plateforme

**Bureau Windows 10**

* Win32/x64 est la seule plateforme Win32 prise en charge. Win32/x86 n’est pas pris en charge.

**HoloLens 2**

* La fonctionnalité de [rendu à partir de la caméra PV](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-capture-for-developers#render-from-the-pv-camera-opt-in) n’est pas prise en charge.
