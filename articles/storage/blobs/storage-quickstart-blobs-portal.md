---
title: 'Démarrage rapide : Créer un blob avec le portail Azure'
titleSuffix: Azure Storage
description: Dans ce Démarrage rapide, vous utilisez le portail Azure dans un stockage d’objets (blob). Ensuite, vous utilisez le portail Azure pour charger un objet blob dans Stockage Azure, télécharger un objet blob et répertorier les objets blob dans un conteneur.
services: storage
author: tamram
ms.service: storage
ms.subservice: blobs
ms.topic: quickstart
ms.date: 04/16/2020
ms.author: tamram
ms.openlocfilehash: f2e18b060aabcb849fb8e17722c530d199ebdbb8
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "88067745"
---
# <a name="quickstart-upload-download-and-list-blobs-with-the-azure-portal"></a>Démarrage rapide : Charger, télécharger et lister les objets blob avec le portail Azure

Dans ce démarrage rapide, vous apprenez à utiliser le [portail Azure](https://portal.azure.com/) pour créer un conteneur dans le stockage Azure, ainsi que pour charger et télécharger des objets blob de blocs dans ce conteneur.

## <a name="prerequisites"></a>Prérequis

[!INCLUDE [storage-quickstart-prereq-include](../../../includes/storage-quickstart-prereq-include.md)]

## <a name="create-a-container"></a>Créez un conteneur.

Pour créer un conteneur dans le portail Azure, procédez comme suit :

1. Accédez à votre nouveau compte de stockage dans le portail Azure.
2. Dans le menu de gauche du compte de stockage, faites défiler jusqu’à la section **Service Blob**, puis sélectionnez **Conteneurs**.
3. Sélectionnez le bouton **+ Conteneur**.
4. Entrez un nom pour votre nouveau conteneur. Le nom du conteneur doit être en minuscules, commencer par une lettre ou un chiffre, et peut comporter uniquement des lettres, des chiffres et des tirets (-). Pour plus d’informations sur les noms des conteneurs et des objets blob, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).
5. Définissez le niveau d’accès public sur le conteneur. Le niveau par défaut est **Private (no anonymous access)** (Privé (aucun accès anonyme)).
6. Sélectionnez **OK** pour créer le conteneur.

    ![Capture d’écran montrant comment créer un conteneur dans le portail Azure](media/storage-quickstart-blobs-portal/create-container.png)

## <a name="upload-a-block-blob"></a>Charger un objet blob de blocs

Les objets blob de blocs sont constitués de blocs de données assemblés pour former un objet blob. La plupart des scénarios utilisant le stockage Blob se servent d’objets blob de blocs. Les objets blob de blocs sont idéaux pour le stockage des données texte et binaires dans le cloud, telles que des fichiers, des images et des vidéos. Ce démarrage rapide montre comment utiliser des objets blob de blocs.

Pour charger un objet blob de blocs dans votre nouveau conteneur dans le portail Azure, procédez comme suit :

1. Dans le portail Azure, accédez au conteneur que vous avez créé dans la section précédente.
1. Sélectionnez le conteneur pour afficher une liste des objets blob qu’il contient. Comme ce conteneur est nouveau, il ne contient pas encore d’objets blob.
1. Sélectionnez le bouton **Charger** pour ouvrir le panneau Charger et naviguez dans votre système de fichiers local pour rechercher un fichier à charger en tant qu’objet blob de blocs. Vous pouvez éventuellement développer la section **Avancé** pour configurer d’autres paramètres pour l’opération de chargement.

    ![Capture d’écran montrant comment charger un objet blob à partir de votre disque local](media/storage-quickstart-blobs-portal/upload-blob.png)

1. Sélectionnez le bouton **Charger** pour charger l’objet blob.
1. Chargez autant d’objets blob que vous le souhaitez en suivant cette méthode. Vous verrez que les nouveaux objets blob sont maintenant répertoriés dans le conteneur.

## <a name="download-a-block-blob"></a>Télécharger un objet blob de blocs

Vous pouvez télécharger un objet blob de blocs à afficher dans le navigateur ou à enregistrer dans votre système de fichiers local. Pour télécharger un objet blob de blocs, procédez comme suit :

1. Accédez à la liste d’objets blob que vous avez chargée dans la section précédente.
1. Cliquez avec le bouton droit sur l’objet blob que vous souhaitez télécharger, puis sélectionnez **Télécharger**.

    ![Capture d’écran montrant comment télécharger un blob](media/storage-quickstart-blobs-portal/download-blob.png)

## <a name="delete-a-block-blob"></a>Supprimer un objet blob de blocs

Vous pouvez télécharger un objet blob de blocs à afficher dans le navigateur ou à enregistrer dans votre système de fichiers local. Pour télécharger un objet blob de blocs, procédez comme suit :

1. Accédez à la liste d’objets blob que vous avez chargée dans la section précédente.
1. Sélectionnez les objets blobs que vous souhaitez supprimer, puis choisissez **Supprimer** dans la barre d’action supérieure.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Pour supprimer toutes les ressources que vous avez créées dans ce démarrage rapide, vous pouvez simplement supprimer le conteneur. Tous les objets blob dans le conteneur seront également supprimés.

Pour supprimer le conteneur :

1. Dans le portail Azure, accédez à la liste des conteneurs dans votre compte de stockage.
1. Sélectionnez le conteneur à supprimer.
1. Sélectionnez le bouton **Plus** ( **...** ), puis sélectionnez **Supprimer**.
1. Confirmez que vous souhaitez supprimer le conteneur.

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez appris à transférer des fichiers entre un disque local et le stockage blob Azure avec le portail Azure. Pour en savoir plus sur l’utilisation de Stockage Blob, consultez le Guide pratique de Stockage Blob.

> [!div class="nextstepaction"]
> [Guide pratique des opérations Stockage Blob](storage-dotnet-how-to-use-blobs.md)
