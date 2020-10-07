---
title: Créer un disque managé à partir d’un fichier VHD dans le même compte - Exemple CLI
description: Exemple de script avec l’interface de ligne de commande Azure CLI - Créer un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement
documentationcenter: storage
author: ramankumarlive
manager: kavithag
ms.service: virtual-machines
ms.subservice: disks
ms.devlang: azurecli
ms.topic: sample
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: d0795f67390faec4a08882adb1f2b15efcbc6619
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91274875"
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli-linux"></a>Créer un disque managé à partir d’un fichier VHD dans un compte de stockage dans le même abonnement avec l’interface de ligne de commande (Linux)

Ce script crée un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement. Utilisez ce script pour importer un VHD spécialisé (non généralisé/préparé avec Sysprep) vers un disque de système d’exploitation managé pour créer une machine virtuelle. Ou bien, utilisez-le pour importer un VHD de données vers un disque de données managées. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explication du script

Ce script a recours aux commandes suivantes pour créer un disque managé à partir d’un VHD. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [az disk create](/cli/azure/disk) | Crée un disque managé en utilisant l’URI d’un VHD dans un compte de stockage dans le même abonnement |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle en joignant un disque managé en tant que disque de système d’exploitation](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
