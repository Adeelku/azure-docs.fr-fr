---
title: Créer une machine virtuelle en attachant un disque managé en tant que disque de système d’exploitation – PowerShell
description: Exemple de script Azure PowerShell - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation
documentationcenter: virtual-machines
author: ramankumarlive
manager: kavithag
ms.service: virtual-machines-windows
ms.subservice: disks
ms.topic: sample
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc, devx-track-azurepowershell
ms.openlocfilehash: 038ec433a4f27eec5ace537ff9b08e5ff6c2f6a9
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89322731"
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>Créer une machine virtuelle en utilisant un disque de système d’exploitation géré existant avec PowerShell 

Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation. Utilisez ce script dans des scénarios précédent :
* Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement
* Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé 
* Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour obtenir des propriétés de disque géré, attacher un disque géré à une nouvelle machine virtuelle et créer une machine virtuelle. Chaque élément du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [Get-AzDisk](/powershell/module/az.compute/get-azdisk) | Obtient l’objet disque sur la base du nom et du groupe de ressources d’un disque. La propriété Id de l’objet disque retourné est utilisée pour attacher le disque à une nouvelle machine virtuelle |
| [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) | Crée une configuration de machine virtuelle. Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration. La configuration est utilisée lors de la création de machines virtuelles. |
| [Set-AzVMOSDisk](/powershell/module/az.compute/set-azvmosdisk) | Attache un disque géré en utilisant la propriété Id du disque en tant que disque de système d’exploitation pour une nouvelle machine virtuelle |
| [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) | Crée une adresse IP publique. |
| [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) | Crée une interface réseau. |
| [New-AzVM](/powershell/module/az.compute/new-azvm) | Création d’une machine virtuelle |
|[Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Supprime un groupe de ressources et toutes les ressources contenues. |

Pour les images marketplace, utilisez [Set-AzVMPlan](/powershell/module/az.compute/set-azvmplan) afin de définir les informations de plan.

```powershell
Set-AzVMPlan -VM $VirtualMachine -Publisher $Publisher -Product $Product -Name $Bame
```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/).

Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
