---
author: craigktreasure
ms.service: azure-spatial-anchors
ms.topic: include
ms.date: 12/13/2018
ms.author: crtreasu
ms.openlocfilehash: b2b3ca886359a0b4c906b89ed76f57486fc2c368
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "83638986"
---
## <a name="create-a-spatial-anchors-resource"></a>Créer une ressource Spatial Anchors

Accédez au <a href="https://portal.azure.com" target="_blank">portail Azure</a>.

Dans le volet de navigation gauche du portail Azure, sélectionnez **Créer une ressource**.

Utilisez la zone de recherche pour rechercher **Spatial Anchors**.

   ![Recherche de Spatial Anchors](./media/spatial-anchors-get-started-create-resource/portal-search.png)

Sélectionnez **Spatial Anchors**. Dans la boîte de dialogue, sélectionnez **Créer**.

Dans la boîte de dialogue **Compte Spatial Anchors** :

- Entrez un nom de ressource unique, en utilisant des caractères alphanumériques normaux.
- Sélectionnez l’abonnement auquel attacher la ressource.
- Créer un groupe de ressources en sélectionnant **Créer**. Nommez-le **myResourceGroup** et sélectionnez **OK**.
      [!INCLUDE [resource group intro text](resource-group.md)]
- Sélectionnez un emplacement (région) où placer la ressource.
- Sélectionnez **Nouveau** pour commencer à créer la ressource.

   ![Créer une ressource](./media/spatial-anchors-get-started-create-resource/create-resource-form.png)

Une fois la ressource créée, le portail Azure indique que votre déploiement est terminé. Cliquez sur **Accéder à la ressource**.

![Déploiement terminé](./media/spatial-anchors-get-started-create-resource/deployment-complete.png)

Ensuite, vous pouvez afficher les propriétés de la ressource. Copiez l’**ID de compte** de la ressource dans un éditeur de texte, car vous en aurez besoin par la suite.

   ![Propriétés de la ressource](./media/spatial-anchors-get-started-create-resource/view-resource-properties.png)

Copiez également le **Domaine du compte** de la ressource dans un éditeur de texte, car vous en aurez besoin par la suite.

   ![Domaine du compte](./media/spatial-anchors-get-started-create-resource/view-resource-domain.png)

Sous **Paramètres**, sélectionnez **Clé**. Copiez la valeur de la **Clé primaire** dans un éditeur de texte. Cette valeur est la `Account Key`. Vous en aurez besoin ultérieurement.

   ![Clé de compte](./media/spatial-anchors-get-started-create-resource/view-account-key.png)
