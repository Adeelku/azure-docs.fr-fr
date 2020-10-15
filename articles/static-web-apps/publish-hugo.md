---
title: 'Tutoriel : Publier un site Hugo dans Azure Static Web Apps'
description: Découvrez comment déployer une application Hugo surAzure Static Web Apps.
services: static-web-apps
author: aaronpowell
ms.service: static-web-apps
ms.topic: tutorial
ms.date: 05/08/2020
ms.author: aapowell
ms.openlocfilehash: ff408f114784fa3f0b8fab49521b5ec7ec2be102
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88797715"
---
# <a name="tutorial-publish-a-hugo-site-to-azure-static-web-apps-preview"></a>Tutoriel : Publier un site Hugo dans Azure Static Web Apps Preview

Cet article montre comment créer et déployer une application web [Hugo](https://gohugo.io/) dans [Azure Static Web Apps](overview.md). Vous obtenez ainsi une nouvelle application Azure Static Web Apps avec la fonctionnalité GitHub Actions associée, qui vous permet de contrôler la manière dont l’application est générée et publiée.

Dans ce tutoriel, vous allez apprendre à :

> [!div class="checklist"]
>
> - Créer une application Hugo
> - Configurer une application Azure Static Web Apps
> - Déployer une application Hugo sur Azure

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. Si vous n’en avez pas, vous pouvez créer un [compte gratuitement](https://azure.microsoft.com/free/).
- Un compte GitHub. Si vous n’en avez pas, vous pouvez créer un [compte gratuitement](https://github.com/join).

## <a name="create-a-hugo-app"></a>Créer une application Hugo

Créer une application Hugo à l’aide de l’interface de ligne de commande (CLI) Hugo :

1. Suivez le [Guide d’installation](https://gohugo.io/getting-started/installing/) pour Hugo sur votre système d’exploitation.

1. Ouvrez un terminal.

1. Exécutez l’interface CLI Hugo pour créer une application.

   ```bash
   hugo new site static-app
   ```

1. Accédez à l’application nouvellement créée.

   ```bash
   cd static-app
   ```

1. Initialisez un dépôt Git.

   ```bash
    git init
   ```

1. Ensuite, ajoutez un thème au site en installant un thème sous la forme d’un sous-module git, puis en le spécifiant dans le fichier de configuration Hugo.

   ```bash
   git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
   echo 'theme = "ananke"' >> config.toml
   ```

1. Validez les modifications :

   ```bash
   git add -A
   git commit -m "initial commit"
   ```

## <a name="push-your-application-to-github"></a>Transmettre votre application à GitHub

Vous devez avoir un référentiel sur GitHub pour vous connecter à Azure Static Web Apps. Les étapes suivantes vous montrent comment créer un référentiel pour votre site.

1. Créez un référentiel GitHub (ne créez pas de fichier README) sur [https://github.com/new](https://github.com/new) appelé **hugo-static-app**.

1. Ajoutez le référentiel GitHub en tant que référentiel distant pour votre référentiel local. Veillez à remplacer l’espace réservé `<YOUR_USER_NAME>` par votre nom d’utilisateur GitHub dans la commande suivante.

   ```bash
   git remote add origin https://github.com/<YOUR_USER_NAME>/hugo-static-app
   ```

1. Transmettez votre référentiel local à GitHub.

   ```bash
   git push --set-upstream origin master
   ```

## <a name="deploy-your-web-app"></a>Déployez votre application web

Les étapes suivantes vous montrent comment créer une application Static Web Apps et la déployer dans un environnement de production.

### <a name="create-the-application"></a>Création de l'application

1. Accéder au [portail Azure](https://portal.azure.com)
1. Cliquez sur **Create a Resource** (Créer une ressource).
1. Recherchez **Static Web Apps**.
1. Cliquez sur **Static Web Apps (Preview)** (Static Web Apps (préversion))
1. Cliquez sur **Créer**

   :::image type="content" source="./media/publish-hugo/create-in-portal.png" alt-text="Création d’une ressource Azure Static Web Apps dans le portail":::

1. Pour **Abonnement**, acceptez l’abonnement qui est listé ou sélectionnez-en un nouveau dans la liste déroulante.

1. Dans _Groupe de ressources_, sélectionnez **Nouveau**. Dans _New resource group name_ (Nom du nouveau groupe de ressources), entrez **hugo-static-app**, puis sélectionnez **OK**.

1. Ensuite, entrez un nom pour votre application dans la zone **Nom**. Les caractères valides sont `a-z`, `A-Z`, `0-9` et `-`.

1. Dans _Region_ (Région), sélectionnez une région disponible proche de vous.

1. Pour _SKU_, sélectionnez **Free** (Gratuit).

   :::image type="content" source="./media/publish-hugo/basic-app-details.png" alt-text="Création d’une ressource Azure Static Web Apps dans le portail":::

1. Cliquez sur le bouton **Sign in with GitHub** (Se connecter avec GitHub).

1. Sélectionnez l’**organisation** sous laquelle vous avez créé le référentiel.

1. Sélectionnez **hugo-static-app** comme _Repository_ (Référentiel).

1. Pour _Branch_ (Branche), sélectionnez **master** (principale).

   :::image type="content" source="./media/publish-hugo/completed-github-info.png" alt-text="Création d’une ressource Azure Static Web Apps dans le portail":::

### <a name="build"></a>Build

Vous ajoutez ensuite les paramètres de configuration utilisés par le processus de génération pour générer votre application. Les paramètres suivants configurent le fichier de workflow d’action GitHub.

1. Cliquez sur le bouton **Next: Build >** (Suivant : générer >) pour modifier la configuration de la génération.

1. Définissez _App location_ (Emplacement de l’application) sur **/** .

1. Définissez _App artifact location_ (Emplacement de l’artefact de l’application) sur **public**.

   Il n’est pas nécessaire de fournir une valeur pour _API location_ (Emplacement de l’API), puisque vous ne déployez pas d’API pour le moment.

### <a name="review-and-create"></a>Examiner et créer

1. Pour vérifier que les informations sont correctes, cliquez sur le bouton **Review + Create** (Vérifier + créer).

1. Pour démarrer la création de l’application Azure Static Web Apps et la configuration d’une action GitHub pour le déploiement, cliquez sur **Create** (Créer).

1. Attendez que l’action GitHub se termine.

1. Dans la fenêtre _Overview_ (Vue d’ensemble) du portail Azure de la ressource Azure Static Web Apps nouvellement créée, cliquez sur le lien _URL_ pour ouvrir l’application que vous avez déployée.

   :::image type="content" source="./media/publish-hugo/deployed-app.png" alt-text="Création d’une ressource Azure Static Web Apps dans le portail":::

## <a name="clean-up-resources"></a>Nettoyer les ressources

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Ajouter un domaine personnalisé](custom-domain.md)
