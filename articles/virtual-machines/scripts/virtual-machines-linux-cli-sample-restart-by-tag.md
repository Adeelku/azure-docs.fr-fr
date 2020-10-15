---
title: Exemple de script Azure CLI - Redémarrage de machines virtuelles
description: Exemple de script Azure CLI - Redémarrer des machines virtuelles par balise et ID
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: gwallace
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: cynthn
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: 03a1e44ee3bdaa168fb3eb17078bfecb1f45c443
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87479487"
---
# <a name="restart-vms"></a>Redémarrer les machines virtuelles

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Cet exemple montre plusieurs façons d’obtenir des machines virtuelles et de les redémarrer.

Le premier redémarre toutes les machines virtuelles dans le groupe de ressources.

```azurecli
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Le second obtient des machines virtuelles marquées à l’aide de `az resource list` et filtre les ressources qui sont des machines virtuelles, puis les redémarre.

```azurecli
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Cet exemple fonctionne dans un interpréteur de commandes Bash. Pour en savoir plus les options d’exécution de scripts Azure CLI dans le client Windows, consultez [Install Azure CLI on Windows](/cli/azure/install-azure-cli-windows) (Installer Azure CLI sur Windows).


## <a name="sample-script"></a>Exemple de script

L’exemple comporte trois scripts.
Le premier configure les machines virtuelles.
Il utilise l’option no-wait. Ainsi, la commande renvoie le résultat sans attendre l’approvisionnement de chaque machine virtuelle.
Le second attend que les machines virtuelles soient entièrement approvisionnées.
Le troisième script redémarre toutes les machines virtuelles qui ont été configurées, puis simplement les machines virtuelles marquées.

### <a name="provision-the-vms"></a>Approvisionnement des machines virtuelles

Ce script crée un groupe de ressources, puis trois machines virtuelles à redémarrer.
Deux présentent un indicateur.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]

### <a name="wait"></a>Wait

Ce script vérifie l’état de configuration toutes les 20 secondes jusqu'à ce que les trois machines virtuelles soient approvisionnées, ou qu’une d’entre elles ne puisse l’être.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]

### <a name="restart-the-vms"></a>Redémarrer les machines virtuelles

Ce script redémarre toutes les machines virtuelles dans le groupe de ressources, puis redémarre uniquement les machines virtuelles marquées.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Une fois l’exemple de script exécuté, la commande suivante permet de supprimer les groupes de ressources, les machines virtuelles et toutes les ressources associées.

```azurecli-interactive
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle, un groupe à haute disponibilité, un équilibreur de charge et toutes les ressources associées. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [az group create](/cli/azure/group) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az vm create](/cli/azure/vm/availability-set) | Crée les machines virtuelles.  |
| [az vm list](/cli/azure/vm) | Utilisé avec `--query` pour garantir que les machines virtuelles sont configurées avant de les redémarrer, puis pour obtenir les ID des machines virtuelles pour les redémarrer. |
| [az resource list](/cli/azure/vm) | Utilisé avec `--query` pour obtenir les ID des machines virtuelles qui utilisent l’indicateur. |
| [az vm restart](/cli/azure/vm) | Redémarre les machines virtuelles. |
| [az group delete](/cli/azure/vm/extension) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
