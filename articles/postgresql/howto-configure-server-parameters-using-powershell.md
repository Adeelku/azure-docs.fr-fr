---
title: Configurer les paramètres du serveur - Azure PowerShell - Azure Database pour PostgreSQL
description: Cet article décrit comment configurer les paramètres de service dans Azure Database pour PostgreSQL à l’aide de PowerShell.
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.devlang: azurepowershell
ms.topic: how-to
ms.date: 06/08/2020
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 0fa49714365c00060ef7f11f5c9646141f707f4b
ms.sourcegitcommit: 19dce034650c654b656f44aab44de0c7a8bd7efe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2020
ms.locfileid: "91707810"
---
# <a name="customize-azure-database-for-postgresql-server-parameters-using-powershell"></a>Personnaliser les paramètres de serveur Azure Database pour PostgreSQL à l’aide de PowerShell

Vous pouvez lister, afficher et mettre à jour les paramètres de configuration d’un serveur Azure Database pour PostgreSQL à l’aide de PowerShell. Un sous-ensemble de configurations de moteur est exposé au niveau du serveur et peut être modifié.

## <a name="prerequisites"></a>Prérequis

Pour utiliser ce guide pratique, il vous faut :

- Le [module Az PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps) installé localement ou [Azure Cloud Shell](https://shell.azure.com/) dans le navigateur
- Un [serveur Azure Database pour PostgreSQL](quickstart-create-postgresql-server-database-using-azure-powershell.md)

> [!IMPORTANT]
> Tant que le module Az.PostgreSql PowerShell est en préversion, vous devez l’installer séparément du module Az PowerShell à l’aide de la commande suivante : `Install-Module -Name Az.PostgreSql -AllowPrerelease`
> Une fois que le module Az.PostgreSql PowerShell est en disponibilité générale, il devient partie intégrante des versions ultérieures du module Az PowerShell et est disponible en mode natif dans Azure Cloud Shell.

Si vous choisissez d’utiliser PowerShell localement, connectez-vous à votre compte Azure à l’aide de l’applet de commande [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Répertorier les paramètres de configuration de Base de données Azure pour le serveur PostgreSQL

Pour lister tous les paramètres modifiables sur un serveur et leurs valeurs, exécutez l’applet de commande `Get-AzPostgreSqlConfiguration`.

L’exemple suivant liste les paramètres de configuration du serveur **mydemoserver** dans le groupe de ressources **myresourcegroup**.

```azurepowershell-interactive
Get-AzPostgreSqlConfiguration -ResourceGroupName myresourcegroup -ServerName mydemoserver
```

Pour obtenir la définition de chacun des paramètres listés, consultez la section de référence PostgreSQL dans [Variables d’environnement](https://www.postgresql.org/docs/12/libpq-envars.html).

## <a name="show-server-configuration-parameter-details"></a>Affichage des détails des paramètres de configuration du serveur

Pour afficher les détails d’un paramètre de configuration particulier d’un serveur, exécutez l’applet de commande `Get-AzPostgreSqlConfiguration` et spécifiez le paramètre **Name**.

Cet exemple montre les détails du paramètre de configuration **slow\_query\_log** pour le serveur **mydemoserver** dans le groupe de ressources **myresourcegroup**.

```azurepowershell-interactive
Get-AzPostgreSqlConfiguration -Name slow_query_log -ResourceGroupName myresourcegroup -ServerName mydemoserver
```

## <a name="modify-a-server-configuration-parameter-value"></a>Modifier une valeur de paramètre de configuration de serveur

Vous pouvez également modifier la valeur d’un paramètre de configuration du serveur, ce qui a pour effet de mettre à jour la valeur de configuration sous-jacente du moteur du serveur PostgreSQL. Pour mettre à jour la configuration, utilisez l’applet de commande `Update-AzPostgreSqlConfiguration`.

Mettez à jour le paramètre de configuration **slow\_query\_log** du serveur **mydemoserver** dans le groupe de ressources **myresourcegroup**.

```azurepowershell-interactive
Update-AzPostgreSqlConfiguration -Name slow_query_log -ResourceGroupName myresourcegroup -ServerName mydemoserver -Value On
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Croissance automatique du stockage sur le serveur Azure Database pour PostgreSQL à l’aide de PowerShell](howto-auto-grow-storage-powershell.md)
