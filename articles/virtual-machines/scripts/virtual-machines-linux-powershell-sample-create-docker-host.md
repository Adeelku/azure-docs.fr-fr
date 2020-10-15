---
title: Exemple de script Azure PowerShell - Docker
description: Exemple de script Azure PowerShell - Docker
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: gwallace
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: mvc, devx-track-azurepowershell
ms.openlocfilehash: ff42c8be6ba69a7fbd50474756b975067035349c
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89079539"
---
# <a name="create-a-docker-host-with-powershell"></a>Créer un hôte Docker avec PowerShell

Ce script crée une machine virtuelle avec Docker activé et démarre un conteneur exécutant NGINX. Une fois que vous avez exécuté le script, vous pouvez accéder au serveur web NGINX par le biais du nom de domaine complet de la machine virtuelle Azure.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script a recours aux commandes suivantes pour créer le déploiement. Chaque élément du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) | Crée une configuration de sous-réseau. Cette configuration est utilisée avec le processus de création du réseau virtuel. |
| [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) | Créer un réseau virtuel. |
| [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) | Crée une adresse IP publique. |
| [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig) | Crée une configuration de règle de groupe de sécurité réseau. Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau. |
| [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) | Crée un groupe de sécurité réseau. |
| [Get-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/get-azvirtualnetworksubnetconfig) | Obtient les informations du sous-réseau. Ces informations sont utilisées lors de la création d’une interface réseau. |
| [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) | Crée une interface réseau. |
| [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) | Crée une configuration de machine virtuelle. Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration. La configuration est utilisée lors de la création de machines virtuelles. |
| [New-AzVM](/powershell/module/az.compute/new-azvm) | Création d’une machine virtuelle |
| [Set-AzVMExtension](/powershell/module/az.compute/set-azvmextension) | Ajoutez une extension de machine virtuelle à la machine virtuelle. Dans cet exemple, l’extension Docker est utilisée pour configurer Docker et exécuter un conteneur Docker NGINX. |
|[Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Supprime un groupe de ressources et toutes les ressources contenues. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/).

Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
