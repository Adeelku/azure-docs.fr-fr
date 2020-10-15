---
title: Configuration d’Azure Key Vault
description: Comment configurer Key Vault pour une utilisation avec une machine virtuelle.
author: mimckitt
manager: vashan
ms.service: virtual-machines
ms.subservice: security
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 01/24/2017
ms.author: mimckitt
ms.openlocfilehash: d5e4bb1d3f62685c90e95eebf5f8f07720a23b82
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "86086991"
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Dans la pile Azure Resource Manager, les secrets/certificats sont modélisés en tant que ressources fournies par le fournisseur de ressources de Key Vault. Pour en savoir plus sur les coffres de clés, consultez [Qu’est-ce qu’Azure Key Vault ?](../../key-vault/general/overview.md)

> [!NOTE]
> 1. Pour que Key Vault puisse être utilisé avec des machines virtuelles Azure Resource Manager, la propriété **EnabledForDeployment** doit être définie sur true dans Key Vault. Vous pouvez le faire dans différents clients.
> 2. Le coffre de clés doit être créé dans le même abonnement et le même emplacement que la machine virtuelle.
>
>

## <a name="use-powershell-to-set-up-key-vault"></a>Utilisation de PowerShell pour configurer Key Vault
Pour créer un coffre de clés à l’aide de PowerShell, voir [Définir et récupérer un secret depuis Azure Key Vault à l’aide de PowerShell](../../key-vault/secrets/quick-create-powershell.md).

Pour de nouveaux coffres de clé, vous pouvez utiliser l’applet de commande PowerShell suivante :

```azurepowershell
New-AzKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment
```

Pour des coffres de clé existants, vous pouvez utiliser l’applet de commande PowerShell suivante :

```azurepowershell
Set-AzKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment
```

## <a name="use-cli-to-set-up-key-vault"></a>Utilisation de l’interface de ligne de commande pour configurer Key Vault
Pour créer un coffre de clés à l’aide de l’interface de ligne de commande (CLI), consultez la rubrique [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)](../../key-vault/general/manage-with-cli2.md#create-a-key-vault).

Pour l’interface de ligne de commande, vous devez créer d’abord le coffre de clés avant d’affecter la stratégie de déploiement. Pour ce faire, vous pouvez utiliser la commande suivante :

```azurecli
az keyvault create --name "ContosoKeyVault" --resource-group "ContosoResourceGroup" --location "EastAsia"
```

Puis, pour activer Key Vault dans le cadre du déploiement de modèle, exécutez la commande suivante :

```azurecli
az keyvault update --name "ContosoKeyVault" --resource-group "ContosoResourceGroup" --enabled-for-deployment "true"
```

## <a name="use-templates-to-set-up-key-vault"></a>Utilisation de modèles pour configurer Key Vault
Quand vous utilisez un modèle, vous devez définir la propriété `enabledForDeployment` sur `true` pour la ressource Key Vault.

```config
{
  "type": "Microsoft.KeyVault/vaults",
  "name": "ContosoKeyVault",
  "apiVersion": "2015-06-01",
  "location": "<location-of-key-vault>",
  "properties": {
    "enabledForDeployment": "true",
    ....
    ....
  }
}
```

Pour les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Création d’un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
