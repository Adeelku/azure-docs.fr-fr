---
title: Impossible de supprimer un réseau virtuel dans Azure | Microsoft Docs
description: Découvrez comment résoudre le problème de suppression impossible d’un réseau virtuel dans Azure.
services: virtual-network
documentationcenter: na
author: chadmath
manager: dcscontentpm
editor: ''
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/31/2018
ms.author: genli
ms.openlocfilehash: 8942e9180e87552ec64e0e848751f492778c9993
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "86131653"
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a>Résolution des problèmes : Échec de la suppression d’un réseau virtuel dans Azure

Vous rencontrez peut-être des erreurs lors de vos tentatives de suppression de réseau virtuel dans Microsoft Azure. Cet article fournit les étapes requises pour vous aider à résoudre ce problème.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Instructions pour la résolution des problèmes 

1. [Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Vérifiez si Azure Active Directory Domain Services est activé dans le réseau virtuel](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Vérifiez si le réseau virtuel est connecté à d’autres ressources](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Vérifiez si une machine virtuelle s’exécute toujours dans le réseau virtuel](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Vérifiez si le réseau virtuel est bloqué en cours de migration](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Étapes de dépannage

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a>Vérifier si une passerelle de réseau virtuel s’exécute dans le réseau virtuel

Pour supprimer le réseau virtuel, vous devez d’abord supprimer la passerelle de réseau virtuel.

Pour les réseaux virtuels classiques, accédez à la **Vue d’ensemble** du réseau virtuel classique dans le portail Azure. Si la passerelle est en cours d’exécution dans le réseau virtuel, vous verrez son adresse IP dans la section **Connexions VPN**. 

![Vérifier si la passerelle est en cours d’exécution](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Pour les réseaux virtuels, accédez à la page **Vue d’ensemble** du réseau virtuel. Recherchez la passerelle de réseau virtuel dans les **Appareils connectés**.

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Avant de pouvoir supprimer la passerelle, supprimez d’abord les objets de **connexion** de la passerelle. 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a>Vérifier si une passerelle d’application s’exécute dans le réseau virtuel

Accédez à la page **Vue d’ensemble** du réseau virtuel. Vérifiez les **Appareils connectés** dans la passerelle d’application.

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

S’il existe une passerelle d’application, vous devez la supprimer avant de pouvoir supprimer le réseau virtuel.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a>Vérifier si Azure Active Directory Domain Services est activé dans le réseau virtuel

Si Active Directory Domain Services est activé et connecté au réseau virtuel, vous ne pouvez pas supprimer ce dernier. 

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

Pour désactiver le service, consultez la page [Désactiver Azure Active Directory Domain Services à l’aide du Portail Azure](../active-directory-domain-services/delete-aadds.md).

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a>Vérifier si le réseau virtuel est connecté à d’autres ressources

Recherchez les liaisons de circuit, les connexions et les peerings de réseaux virtuels. Tous ces éléments peuvent empêcher la suppression d’un réseau virtuel. 

Voici la séquence de suppression recommandée :

1. Connexions de passerelle
2. Passerelles
3. Adresses IP
4. Peerings de réseaux virtuels
5. App Service Environment (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a>Vérifier si une machine virtuelle s’exécute toujours dans le réseau virtuel

Vérifiez qu’aucune machine virtuelle ne s’exécute dans le réseau virtuel.

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a>Vérifier si le réseau virtuel est bloqué en cours de migration

Si le réseau virtuel est bloqué dans un état de migration, il ne peut pas être supprimé. Exécutez la commande suivante pour annuler la migration, puis supprimez le réseau virtuel.

```azurepowershell
Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort
```

## <a name="next-steps"></a>Étapes suivantes

- [Réseau virtuel Azure](virtual-networks-overview.md)
- [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)
