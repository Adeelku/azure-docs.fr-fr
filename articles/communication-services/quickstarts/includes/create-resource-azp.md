---
author: mikben
ms.service: azure-communication-services
ms.topic: include
ms.date: 9/1/2020
ms.author: mikben
ms.openlocfilehash: 11b9c553573d9e6188ba634b4cb966d6a9b850b4
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "90944771"
---
## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. [Créez un compte gratuitement](https://azure.microsoft.com/free/dotnet/).

## <a name="create-azure-communication-resource"></a>Créer une ressource Azure Communication

Pour créer une ressource Azure Communication Services, commencez par vous connecter au [portail Azure](https://portal.azure.com). En haut à gauche de la page, sélectionnez **+ Créer une ressource**. 

:::image type="content" source="../media/create-a-communication-resource/create-resource-plus-sign.png" alt-text="Capture d’écran illustrant le bouton Créer une ressource dans le portail Azure.":::

Tapez **Communication** dans la zone d’entrée **Rechercher dans le marketplace** ou dans la barre de recherche en haut du portail.

:::image type="content" source="../media/create-a-communication-resource/searchbar-communication-portal.png" alt-text="Capture d’écran illustrant le bouton Créer une ressource dans le portail Azure.":::

Sélectionnez **Communication Services** dans les résultats, puis sélectionnez **Ajouter**.

:::image type="content" source="../media/create-a-communication-resource/add-communication-portal.png" alt-text="Capture d’écran illustrant le bouton Créer une ressource dans le portail Azure.":::

Vous pouvez maintenant configurer votre ressource Communication Services. Dans la première page du processus de création, vous êtes invité à spécifier les informations suivantes :

* Abonnement
* Groupe de ressources (vous pouvez en créer un autre ou choisir un groupe de ressources existant)
* Nom de la ressource Communication Services
* Zone géographique à laquelle associer la ressource

À l’étape suivante, vous pouvez attribuer des étiquettes à la ressource. Les étiquettes peuvent être utiles pour organiser vos ressources Azure. Pour plus d’informations sur les étiquettes, consultez la [documentation sur l’étiquetage des ressources](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).

Enfin, vous pouvez vérifier votre configuration et **créer** la ressource. Notez que le déploiement prend quelques minutes.

## <a name="manage-your-communication-services-resource"></a>Gérer la ressource Communication Services

Pour gérer votre ressource Communication Services, accédez au [portail Azure](https://portal.azure.com), puis recherchez et sélectionnez **Azure Communication Services**.

Dans la page **Communication Services**, sélectionnez le nom de votre ressource.

La page **Vue d’ensemble** de votre ressource contient des options de gestion de base, telles que parcourir, arrêter, démarrer, redémarrer et supprimer. Vous trouverez d’autres options de configuration dans le menu de gauche dans la page de la ressource.