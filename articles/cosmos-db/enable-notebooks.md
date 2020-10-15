---
title: Activer les notebooks dans un compte Azure Cosmos DB (préversion)
description: Les notebooks intégrés d’Azure Cosmos DB vous permettent d’analyser et de visualiser vos données sur le portail. Cet article explique comment activer cette fonctionnalité pour des comptes Cosmos.
author: deborahc
ms.service: cosmos-db
ms.topic: how-to
ms.date: 09/22/2019
ms.author: dech
ms.openlocfilehash: 4c485bf6b9eb34e68e399c24e51286428f47586f
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "85261900"
---
# <a name="enable-notebooks-for-azure-cosmos-db-accounts-preview"></a>Activer les notebooks pour un compte Azure Cosmos DB (préversion)

> [!IMPORTANT]
> Les notebooks intégrés pour Azure Cosmos DB sont actuellement disponibles dans les régions Azure suivantes : Australie Est, USA Est, USA Est 2, Europe Nord, USA Centre Sud, Asie Sud-Est, Royaume-Uni Sud, Europe Ouest et USA Ouest 2. Pour utiliser des notebooks, [créez un compte avec des notebooks](#enable-notebooks-in-a-new-cosmos-account) ou [activez les notebooks sur un compte existant](#enable-notebooks-in-an-existing-cosmos-account) dans l’une de ces régions.

Les notebooks Jupyter intégrés dans Azure Cosmos DB vous permettent d’analyser et de visualiser vos données via le portail Azure. Cet article décrit comment activer cette fonctionnalité pour votre compte Azure Cosmos DB.

## <a name="enable-notebooks-in-a-new-cosmos-account"></a>Activer les notebooks dans un nouveau compte Azure Cosmos

1. Connectez-vous au [portail Azure](https://portal.azure.com/).
1. Sélectionnez **Créer une ressource** > **Bases de données** > **Azure Cosmos DB**.
1. Dans la page **Créer un compte Azure Cosmos DB**, sélectionnez **Notebooks**. 
 
    :::image type="content" source="media/enable-notebooks/create-new-account-with-notebooks.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

1. Sélectionnez **Revoir + créer**. Vous pouvez ignorer les options **Réseau** et **Balises**. 
1. Passez en revue les paramètres du compte, puis sélectionnez **Créer**. La création du compte prend quelques minutes. Attendez que la page du portail affiche **Votre déploiement est terminé**. 

   :::image type="content" source="media/enable-notebooks/create-new-account-with-notebooks-complete.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

1. Sélectionnez **Accéder à la ressource** pour accéder à la page du compte Azure Cosmos DB.

   :::image type="content" source="../../includes/media/cosmos-db-create-dbaccount/azure-cosmos-db-account-created-3.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

1. Accédez au volet **Explorateur de données**. Vous devez maintenant voir votre espace de travail Notebooks.

    :::image type="content" source="media/enable-notebooks/new-notebooks-workspace.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

## <a name="enable-notebooks-in-an-existing-cosmos-account"></a>Activer les notebooks dans un compte Cosmos

Vous pouvez également activer les notebooks sur des comptes existants. Cette opération ne doit être effectuée qu’une seule fois par compte.

1. Accédez au volet **Explorateur de données** de votre compte Cosmos.
1. Sélectionnez **Activer les notebooks**.

    :::image type="content" source="media/enable-notebooks/enable-notebooks-workspace.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

1. Vous êtes invité à créer un espace de travail Notebooks. Sélectionnez **Terminer la configuration**.
1. Votre compte est désormais activé pour l’utilisation des notebooks.

## <a name="create-and-run-your-first-notebook"></a>Créer et exécuter votre premier notebook

Pour vérifier que vous pouvez utiliser les notebooks, sélectionnez l’un d’eux sous Exemples de notebooks. Cela a pour effet d’enregistrer une copie du notebook dans votre espace de travail et de l’ouvrir.

Dans cet exemple, nous allons utiliser **gettingstarted.ipynb**. 

:::image type="content" source="media/enable-notebooks/select-getting-started-notebook.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

Pour exécuter le notebook :
1. Sélectionnez la première cellule de code contenant du code Python. 
1. Sélectionnez **Exécuter** pour exécuter la cellule. Dans la cellule, appuyez sur **Maj+Entrée** pour exécuter la cellule.
1. Actualisez le volet des ressources pour voir la base de données et le conteneur créés.

    :::image type="content" source="media/enable-notebooks/run-first-notebook-cell.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

Vous pouvez également sélectionner **Nouveau notebook** pour créer un notebook ou charger un fichier de notebook (.ipynb) existant en sélectionnant **Charger le fichier** dans le menu **Mes notebooks**. 

:::image type="content" source="media/enable-notebooks/create-or-upload-new-notebook.png" alt-text="Sélectionner l’option Notebooks dans le panneau créer d’Azure Cosmos DB":::

## <a name="next-steps"></a>Étapes suivantes

- Découvrez les avantages de [notebooks Jupyter d’Azure Cosmos DB](cosmosdb-jupyter-notebooks.md)
