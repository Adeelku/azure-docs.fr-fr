---
title: Fichier Include
description: Fichier Include
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: include
ms.date: 07/05/2018
ms.author: tomfitz
ms.custom: include file
ms.openlocfilehash: 68a208af1a9aa9e73f2af99021d195f264fb21f1
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "67177679"
---
## <a name="enable-event-grid-resource-provider"></a>Activer le fournisseur de ressources Event Grid

Si vous n’avez jamais utilisé Event Grid dans votre abonnement Azure, vous devrez peut-être inscrire le fournisseur de ressources Event Grid. Exécutez la commande suivante :

```azurepowershell-interactive
Register-AzResourceProvider -ProviderNamespace Microsoft.EventGrid
```

L’inscription peut prendre un certain temps. Pour vérifier l’état, exécutez :

```azurepowershell-interactive
Get-AzResourceProvider -ProviderNamespace Microsoft.EventGrid
```

Lorsque `RegistrationStatus` est `Registered`, vous êtes prêt à continuer.
