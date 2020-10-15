---
title: Tutoriel - Supprimer un cluster Azure Red Hat OpenShift
description: Dans ce tutoriel, découvrez comment supprimer un cluster Azure Red Hat OpenShift à l’aide d’Azure CLI
author: sakthi-vetrivel
ms.custom: fasttrack-edit
ms.author: suvetriv
ms.topic: tutorial
ms.service: container-service
ms.date: 04/24/2020
ms.openlocfilehash: ae2c1072b9490931609dd61f1cac2a47f1cffef3
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89469947"
---
# <a name="tutorial-delete-an-azure-red-hat-openshift-4-cluster"></a>Tutoriel : Supprimer un cluster Azure Red Hat OpenShift 4

Dans ce tutoriel, en trois parties, un cluster Azure Red Hat OpenShift exécutant OpenShift 4 est supprimé. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Supprimer un cluster Azure Red Hat OpenShift


## <a name="before-you-begin"></a>Avant de commencer

Dans les tutoriels précédents, un cluster Azure Red Hat OpenShift a été créé et rendu accessible au moyen de la console web OpenShift. Si vous n’avez pas effectué ces étapes et que vous souhaitez suivre cette procédure, commencez par le [Tutoriel 1 – Créer un cluster Azure Red Hat OpenShift 4](tutorial-create-cluster.md).

Si vous choisissez d’installer et d’utiliser l’interface CLI localement, ce tutoriel demande au minimum la version 2.6.0 d’Azure CLI. Exécutez `az --version` pour trouver la version. Si vous devez installer ou mettre à niveau, voir [Installer Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="sign-in-to-azure"></a>Connexion à Azure

Si vous utilisez Azure CLI localement, exécutez `az login` pour vous connecter à Azure.

```bash
az login
```

Si vous avez accès à plusieurs abonnements, exécutez `az account set -s {subscription ID}` en remplaçant `{subscription ID}` par l’abonnement que vous souhaitez utiliser.

## <a name="delete-the-cluster"></a>Supprimer le cluster

Dans les tutoriels précédents, les variables suivantes ont été définies.

```bash
CLUSTER=yourclustername
RESOURCE_GROUP=yourresourcegroup
```

À l’aide de ces valeurs, supprimez votre cluster :

```bash
az aro delete --resource-group $RESOURCE_GROUP --name $CLUSTER
```

Vous serez ensuite invité à confirmer la suppression du cluster. Après que vous aurez confirmé avec `y`, la suppression du cluster prendra plusieurs minutes. Quand la commande est terminée, tout le groupe de ressources et toutes les ressources qu’il contient, y compris le cluster, sont supprimés.

## <a name="next-steps"></a>Étapes suivantes

Dans cette partie du tutoriel, vous avez appris à :
> [!div class="checklist"]
> * Supprimer un cluster Azure Red Hat OpenShift 4

En savoir plus sur l’utilisation d’OpenShift avec la [documentation Red Hat OpenShift](https://www.openshift.com/try) officielle