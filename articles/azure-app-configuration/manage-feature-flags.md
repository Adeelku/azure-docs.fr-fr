---
title: 'Tutoriel : Utiliser Azure App Configuration pour gérer les indicateurs de fonctionnalités'
titleSuffix: Azure App Configuration
description: Dans ce tutoriel, vous allez découvrir comment gérer les indicateurs de fonctionnalités séparément de votre application à l’aide d’Azure App Configuration.
services: azure-app-configuration
documentationcenter: ''
author: lisaguthrie
manager: maiye
editor: ''
ms.assetid: ''
ms.service: azure-app-configuration
ms.workload: tbd
ms.devlang: csharp
ms.topic: tutorial
ms.date: 04/19/2019
ms.author: lcozzens
ms.custom: devx-track-csharp, mvc
ms.openlocfilehash: dd816ebcf2a40e6a0b7febcc3fe5c1006dac20bb
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88209951"
---
# <a name="tutorial-manage-feature-flags-in-azure-app-configuration"></a>Tutoriel : Gérer les indicateurs de fonctionnalités dans Azure App Configuration

Vous pouvez stocker tous les indicateurs de fonctionnalités dans Azure App Configuration et les gérer à partir d’un emplacement unique. App Configuration propose une interface utilisateur de portail nommée **Gestionnaire de fonctionnalités**, qui est conçue spécifiquement pour les indicateurs de fonctionnalités. App Configuration prend également en charge en mode natif le schéma de données d’indicateurs de fonctionnalités .NET Core.

Dans ce tutoriel, vous allez apprendre à :

> [!div class="checklist"]
> * Définir et gérer des indicateurs de fonctionnalités dans App Configuration.
> * Accéder à des indicateurs de fonctionnalités à partir de votre application.

## <a name="create-feature-flags"></a>Créer des indicateurs de fonctionnalités

Le Gestionnaire de fonctionnalités du portail Azure pour App Configuration fournit une interface utilisateur pour la création et la gestion des indicateurs de fonctionnalités que vous utilisez dans vos applications.

Pour ajouter un nouvel indicateur de fonctionnalité :

1. Sélectionnez **Gestionnaire de fonctionnalités** >  **+Ajouter** pour ajouter un indicateur de fonctionnalité.

    ![Liste d’indicateurs de fonctionnalités](./media/azure-app-configuration-feature-flags.png)

1. Entrez un nom de clé unique pour l’indicateur de fonctionnalité. Vous avez besoin de ce nom pour référencer l’indicateur dans votre code.

1. Si vous le souhaitez, entrez une description pour l’indicateur de fonctionnalité.

1. Définissez l’état initial de l’indicateur de fonctionnalité. Cet état est généralement *Désactivé* (Off) ou *Activé* (On). L’état *Activé* devient *Conditionnel* (Conditional) si vous ajoutez un filtre à l’indicateur de fonctionnalité.

    ![Création d’un indicateur de fonctionnalité](./media/azure-app-configuration-feature-flag-create.png)

1. Quand l’état est *Activé*, sélectionnez **+Ajouter un filtre** pour éventuellement spécifier une condition supplémentaire en vue de qualifier l’état. Entrez une clé de filtre intégrée ou personnalisée, puis sélectionnez **+Ajouter un paramètre** pour associer un ou plusieurs paramètres au filtre. Parmi les filtres intégrés figurent :

    | Clé | Paramètres JSON |
    |---|---|
    | Microsoft.Percentage | {"Value": 0-100 percent} |
    | Microsoft.TimeWindow | {"Start": UTC time, "End": UTC time} |

    ![Filtre d’indicateur de fonctionnalité](./media/azure-app-configuration-feature-flag-filter.png)

## <a name="update-feature-flag-states"></a>Mettre à jour l’état des indicateurs de fonctionnalités

Pour changer la valeur d’état d’un indicateur de fonctionnalité :

1. Sélectionnez **Gestionnaire de fonctionnalités**.

1. À droite d’un indicateur de fonctionnalité que vous souhaitez modifier, sélectionnez les points de suspension ( **...** ), puis sélectionnez **Modifier**.

1. Définissez le nouvel état de l’indicateur de fonctionnalité.

## <a name="access-feature-flags"></a>Accéder à des indicateurs de fonctionnalités

Les indicateurs de fonctionnalités créés par le Gestionnaire de fonctionnalités sont stockés et récupérés sous la forme de valeurs de clés normales. Ils sont conservés sous un préfixe d’espace de noms spécial `.appconfig.featureflag`. Pour voir les valeurs de clés sous-jacentes utilisez l’Explorateur de configuration. Votre application peut récupérer ces valeurs à l’aide des fournisseurs de configuration App Configuration, de kits SDK, d’extensions de ligne de commande et d’API REST.

## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à gérer les indicateurs de fonctionnalités et leurs états à l’aide d’App Configuration. Pour plus d’informations sur la prise en charge de la gestion des fonctionnalités dans App Configuration et ASP.NET Core, consultez l’article suivant :

* [Utiliser des indicateurs de fonctionnalités dans une application ASP.NET Core](./use-feature-flags-dotnet-core.md)
