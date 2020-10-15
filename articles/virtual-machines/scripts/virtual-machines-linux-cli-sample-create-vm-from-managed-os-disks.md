---
title: Créer une machine virtuelle en attachant un disque managé en tant que disque de système d’exploitation - Exemple CLI
description: Exemple de script Azure CLI - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankumarlive
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 83f0ea094c26a1ff664ef27729731b77d987e7ec
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "86501492"
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Créer une machine virtuelle utilisant un disque de système d’exploitation géré existant avec l’interface de ligne de commande

Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation. Utilisez ce script dans des scénarios précédent :
* Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement
* Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé 
* Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour obtenir des propriétés de disque géré, attacher un disque géré à une nouvelle machine virtuelle et créer une machine virtuelle. Chaque élément du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [az disk show](/cli/azure/disk) | Obtient des propriétés de disque géré à l’aide d’un nom de disque et d’un nom de groupe de ressources. La propriété Id est utilisée pour attacher un disque géré à une nouvelle machine virtuelle |
| [az vm create](/cli/azure/vm) | Crée une machine virtuelle à l’aide d’un disque de système d’exploitation géré |
## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
