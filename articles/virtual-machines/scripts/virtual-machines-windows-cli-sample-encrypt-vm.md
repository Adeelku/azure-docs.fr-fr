---
title: Exemple de script Azure CLI - Chiffrement d’une machine virtuelle Windows
description: Exemple de script Azure CLI - Chiffrement d’une machine virtuelle Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: gwallace
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/15/2017
ms.author: cynthn
ms.custom: devx-track-azurecli
ms.openlocfilehash: 0ea6bc61aae45386d2a7b90a32f66ad5de342107
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87494534"
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Chiffrer une machine virtuelle Windows dans Azure

Ce script crée une solution Key Vault sécurisée, des clés de chiffrement, un principal de service Azure Active Directory et une machine virtuelle Windows. La machine virtuelle est ensuite chiffrée à l’aide de la clé de chiffrement de Key Vault et des informations d’identification du principal de service.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour créer un groupe de ressources, une solution Key Vault, un principal de service, une machine virtuelle et toutes les ressources associées. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
| [az group create](/cli/azure/group) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az keyvault create](/cli/azure/keyvault) | Crée une solution Key Vault pour stocker des données sécurisées, telles que des clés de chiffrement. |
| [az keyvault key create](/cli/azure/keyvault/key) | Crée une clé de chiffrement dans Key Vault. |
| [az ad sp create-for-rbac](/cli/azure/ad/sp) | Crée un principal de service Azure Active Directory pour authentifier et contrôler l’accès aux clés de chiffrement en toute sécurité. |
| [az keyvault set-policy](/cli/azure/keyvault) | Définit les autorisations sur Key Vault pour accorder au principal de service l’accès aux clés de chiffrement. |
| [az vm create](/cli/azure/vm) | Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau. Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.  |
| [az vm encryption enable](/cli/azure/vm/encryption) | Active le chiffrement sur une machine virtuelle en utilisant les informations d’identification du principal de service et la clé de chiffrement. |
| [az vm encryption show](/cli/azure/vm/encryption) | Affiche l’état du processus de chiffrement de machine virtuelle. |
| [az group delete](/cli/azure/vm/extension) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
