---
title: Augmenter automatiquement le stockage – Azure PowerShell – Azure Database for MariaDB
description: Cet article explique comment vous pouvez activer la croissance automatique du stockage avec PowerShell dans Azure Database for MariaDB.
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.topic: how-to
ms.date: 5/26/2020
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 2d03a67fc8a8172573598662ad9770b28493e9a2
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87497101"
---
# <a name="auto-grow-storage-in-azure-database-for-mariadb-server-using-powershell"></a>Croissance automatique du stockage sur le serveur Azure Database for MariaDB à l'aide de PowerShell

Cet article explique comment vous pouvez configurer l’augmentation d’un stockage de serveur Azure Database for MariaDB sans affecter la charge de travail.

La croissance automatique du stockage évite à votre serveur d’[atteindre la limite de stockage](/azure/mariadb/concepts-pricing-tiers#reaching-the-storage-limit) et de passer en lecture seule. Pour les serveurs disposant de jusqu’à 100 Go de stockage approvisionné, la taille est augmentée de 5 Go lorsque l’espace libre est inférieur à 10 %. Pour les serveurs disposant de plus de 100 Go de stockage approvisionné, la taille est augmentée de 5 % lorsque l’espace libre est inférieur à 10 Go. Des limites de stockage maximales s’appliquent comme spécifié dans la section relative au stockage des [niveaux tarifaires d’Azure Database for MariaDB](/azure/mariadb/concepts-pricing-tiers#storage).

> [!IMPORTANT]
> N’oubliez pas que le stockage peut seulement monter en puissance.

## <a name="prerequisites"></a>Prérequis

Pour utiliser ce guide pratique, il vous faut :

- Le [module Az PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps) installé localement ou [Azure Cloud Shell](https://shell.azure.com/) dans le navigateur
- Un [serveur Azure Database for MariaDB](quickstart-create-mariadb-server-database-using-azure-powershell.md)

> [!IMPORTANT]
> Tant que le module PowerShell Az.MariaDb est en préversion, vous devez l’installer séparément du module Az PowerShell à l’aide de la commande suivante : `Install-Module -Name Az.MariaDb -AllowPrerelease`.
> Une fois le module PowerShell Az.MariaDb généralement disponible, il devient partie intégrante des versions futures du module Az PowerShell et disponible en mode natif dans Azure Cloud Shell.

Si vous choisissez d’utiliser PowerShell en local, connectez-vous à votre compte Azure à l’aide de la cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount).

## <a name="enable-mariadb-server-storage-auto-grow"></a>Activer la croissance automatique du stockage du serveur MariaDB

Activez le stockage à croissance automatique du serveur sur un serveur existant avec la commande suivante :

```azurepowershell-interactive
Update-AzMariaDbServer -Name mydemoserver -ResourceGroupName myresourcegroup -StorageAutogrow Enabled
```

Activez le stockage à croissance automatique du serveur sur un nouveau serveur avec la commande suivante :

```azurepowershell-interactive
$Password = Read-Host -Prompt 'Please enter your password' -AsSecureString
New-AzMariaDbServer -Name mydemoserver -ResourceGroupName myresourcegroup -Sku GP_Gen5_2 -StorageAutogrow Enabled -Location westus -AdministratorUsername myadmin -AdministratorLoginPassword $Password
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créer et gérer des réplicas en lecture dans Azure Database for MariaDB à l’aide de PowerShell](howto-read-replicas-powershell.md).
