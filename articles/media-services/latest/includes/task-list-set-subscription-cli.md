---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/17/2020
ms.author: inhenkel
ms.custom: CLI
ms.openlocfilehash: aa76f7b85302651f6874747610c3355f0572a7ee
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88556139"
---
<!-- List and set subscriptions -->

1. Obtenez une liste de vos abonnements à l’aide de la commande [az account list](/cli/azure/account#az-account-list) :

    ```
    az account list --output table
    ```

2. Utilisez `az account set` avec l’ID d’abonnement ou le nom avec lequel vous souhaitez effectuer le changement.

    ```
    az account set --subscription "My Demos"
    ```
