---
title: Déclencher une tâche Batch à l’aide d’Azure Functions
description: 'Tutoriel : Appliquer la reconnaissance optique de caractères (OCR) à des documents numérisés quand ils sont ajoutés à un objet blob de stockage'
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 05/30/2019
ms.author: peshultz
ms.custom: mvc, devx-track-csharp
ms.openlocfilehash: 6e481219c6be68f9e9da06d92b6c28998cc7a6e2
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88930092"
---
# <a name="tutorial-trigger-a-batch-job-using-azure-functions"></a>Tutoriel : Déclencher une tâche Batch à l’aide d’Azure Functions

Dans ce tutoriel, vous allez apprendre à déclencher une tâche Batch à l’aide d’Azure Functions. Nous allons examiner un exemple dans lequel la reconnaissance optique de caractères (OCR) est appliquée à des documents ajoutés à un conteneur d’objets blob de stockage Azure par le biais d’Azure Batch. Pour rationaliser le traitement OCR, nous allons configurer une fonction Azure qui exécute une tâche OCR Batch chaque fois qu’un fichier est ajouté au conteneur d’objets blob.

## <a name="prerequisites"></a>Prérequis

* Un abonnement Azure. Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.
* Un compte Azure Batch et un compte Stockage Azure lié. Consultez [Créer un compte Batch](quick-create-portal.md#create-a-batch-account) pour plus d’informations sur la façon de créer et lier des comptes.
* [Batch Explorer](https://azure.github.io/BatchExplorer/)
* [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/)

## <a name="sign-in-to-azure"></a>Connexion à Azure

Connectez-vous au [portail Azure](https://portal.azure.com).

## <a name="create-a-batch-pool-and-batch-job-using-batch-explorer"></a>Créer un pool Batch et une tâche Batch avec Batch Explorer

Dans cette section, vous allez utiliser Batch Explorer pour créer le pool Batch et la tâche Batch qui vont exécuter les tâches de reconnaissance optique de caractères (OCR). 

### <a name="create-a-pool"></a>Créer un pool

1. Connectez-vous à Batch Explorer à l’aide de vos informations d’identification Azure.
1. Créez un pool en sélectionnant **Pools** dans la barre de gauche, puis le bouton **Ajouter** au-dessus du formulaire de recherche. 
    1. Choisissez un ID et un nom d’affichage. Pour cet exemple, nous allons utiliser `ocr-pool`.
    1. Définissez le type de mise à l’échelle sur **Taille fixe** et définissez le nombre de nœuds dédiés sur 3.
    1. Sélectionnez **Ubuntu 18.04-LTS** comme système d’exploitation.
    1. Choisissez `Standard_f2s_v2` comme taille de machine virtuelle.
    1. Activez la tâche de démarrage et ajoutez la commande `/bin/bash -c "sudo update-locale LC_ALL=C.UTF-8 LANG=C.UTF-8; sudo apt-get update; sudo apt-get -y install ocrmypdf"`. Veillez à définir l’identité de l’utilisateur sur l’**utilisateur par défaut de la tâche (administrateur)** , ce qui permet aux tâches de démarrage d’inclure des commandes avec `sudo`.
    1. Sélectionnez **OK**.
### <a name="create-a-job"></a>Créer un travail

1. Créez une tâche sur le pool en sélectionnant **Tâches** dans la barre de gauche, puis le bouton **Ajouter** au-dessus du formulaire de recherche. 
    1. Choisissez un ID et un nom d’affichage. Pour cet exemple, nous allons utiliser `ocr-job`.
    1. Définissez le pool sur `ocr-pool` ou tout autre nom que vous avez choisi pour votre pool.
    1. Sélectionnez **OK**.


## <a name="create-blob-containers"></a>Créer des conteneurs d’objets blob

Ici, vous allez créer des conteneurs d’objets blob pour stocker vos fichiers d’entrée et de sortie pour la tâche Batch de reconnaissance optique de caractères (OCR).

1. Connectez-vous à l’Explorateur Stockage à l’aide de vos informations d’identification Azure.
1. À l’aide du compte de stockage lié à votre compte Batch, créez deux conteneurs d’objets blob (un pour les fichiers d’entrée, un pour les fichiers de sortie) en suivant les étapes indiquées dans [Créer un conteneur d’objets blob](../vs-azure-tools-storage-explorer-blobs.md#create-a-blob-container).

Dans cet exemple, le conteneur d’entrée est nommé `input` et correspond à l’emplacement auquel tous les documents sans reconnaissance optique de caractères (OCR) sont initialement chargés à des fins de traitement. Le conteneur de sortie est nommé `output` et correspond à l’emplacement auquel la tâche Batch écrit des documents traités avec la reconnaissance optique de caractères (OCR).  
    * Dans cet exemple, nous allons appeler notre conteneur d’entrée `input`et notre conteneur de sortie `output`.  
    * Le conteneur d’entrée correspond à l’emplacement auquel tous les documents sans reconnaissance optique de caractères (OCR) sont initialement chargés.  
    * Le conteneur de sortie correspond à l’emplacement auquel la tâche Batch écrit des documents avec reconnaissance optique de caractères (OCR).  

Créez une signature d’accès partagé pour votre conteneur de sortie dans l’Explorateur Stockage. Pour cela, cliquez avec le bouton droit sur le conteneur de sortie et sélectionnez **Obtenir une signature d’accès partagé**. Sous **Autorisations**, cochez **Écriture**. Aucune autre autorisation n’est nécessaire.  

## <a name="create-an-azure-function"></a>Création d’une fonction Azure

Dans cette section, vous allez créer la fonction Azure qui déclenche la tâche Batch de reconnaissance optique de caractères (OCR) chaque fois qu’un fichier est chargé dans votre conteneur d’entrée.

1. Suivez les étapes indiquées dans [Créer une fonction déclenchée par un stockage Blob Azure](../azure-functions/functions-create-storage-blob-triggered-function.md) pour créer une fonction.
    1. Lorsque vous êtes invité à indiquer un compte de stockage, utilisez celui que vous avez lié à votre compte Batch.
    1. Pour la **pile d’exécution**, choisissez .NET. Nous allons écrire notre fonction en C# pour exploiter le SDK .NET Batch.
1. Une fois que la fonction déclenchée par un objet blob est créée, utilisez les fichiers [`run.csx`](https://github.com/Azure-Samples/batch-functions-tutorial/blob/master/run.csx) et [`function.proj`](https://github.com/Azure-Samples/batch-functions-tutorial/blob/master/function.proj) de GitHub dans la fonction.
    * `run.csx` est exécuté quand un nouvel objet blob est ajouté à votre conteneur d’objets blob d’entrée.
    * `function.proj` liste les bibliothèques externes dans votre code de fonction, par exemple, le SDK .NET Batch.
1. Modifiez les valeurs des espaces réservés des variables dans la fonction `Run()` du fichier `run.csx` pour qu’elles reflètent vos informations d’identification Batch et de stockage. Celles-ci figurent, dans le portail Azure, dans la section **Clés** de votre compte Batch.
    * Récupérez vos informations d’identification de compte Batch et de stockage dans le portail Azure, dans la section **Clés** de votre compte Batch. 

## <a name="trigger-the-function-and-retrieve-results"></a>Déclencher la fonction et récupérer les résultats

Chargez sur votre conteneur d’entrée une partie ou la totalité des fichiers analysés à partir du répertoire [`input_files`](https://github.com/Azure-Samples/batch-functions-tutorial/tree/master/input_files) de GitHub. Superviser Batch Explorer pour confirmer qu’une tâche est ajoutée à `ocr-pool` pour chaque fichier. À l’issue de quelques secondes, le fichier avec la reconnaissance optique de caractères (OCR) appliquée est ajouté au conteneur de sortie. Ce fichier est alors visible et récupérable sur l’Explorateur Stockage.

De plus, vous pouvez regarder les fichiers journaux défiler au bas de la fenêtre de l’éditeur web Azure Functions, où des messages comme ceux-ci s’affichent pour chaque fichier chargé dans votre conteneur d’entrée :

```
2019-05-29T19:45:25.846 [Information] Creating job...
2019-05-29T19:45:25.847 [Information] Accessing input container <inputContainer>...
2019-05-29T19:45:25.847 [Information] Adding <fileName> as a resource file...
2019-05-29T19:45:25.848 [Information] Name of output text file: <outputTxtFile>
2019-05-29T19:45:25.848 [Information] Name of output PDF file: <outputPdfFile>
2019-05-29T19:45:26.200 [Information] Adding OCR task <taskID> for <fileName> <size of fileName>...
```

Pour télécharger les fichiers de sortie depuis l’Explorateur Stockage vers votre ordinateur local, sélectionnez d’abord les fichiers souhaités, puis sélectionnez **Télécharger** dans le ruban supérieur. 

> [!TIP]
> Les fichiers téléchargés peuvent faire l’objet d’une recherche si vous les ouvrez dans un lecteur PDF.

## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à effectuer les opérations suivantes : 

> [!div class="checklist"]
> * Utiliser Batch Explorer pour créer des pools et des tâches
> * Utiliser l’Explorateur Stockage pour créer des conteneurs d’objets blob et une signature d’accès partagé (SAP)
> * Créer une fonction Azure déclenchée par un objet blob
> * Charger des fichiers d’entrée sur le stockage
> * Surveiller l’exécution d’une tâche
> * Récupérer les fichiers de sortie

* Pour plus d’exemples d’utilisation de l’API .NET pour planifier et traiter les charges de travail Batch, consultez les [exemples sur GitHub](https://github.com/Azure-Samples/azure-batch-samples/tree/master/CSharp). 

* Pour découvrir d’autres déclencheurs Azure Functions que vous pouvez utiliser pour exécuter des charges de travail Batch, consultez la [documentation Azure Functions](../azure-functions/functions-triggers-bindings.md).
