---
title: 'Passerelle VPN Azure : Supprimer une passerelle : portail'
description: Supprimez une passerelle de réseau virtuel à l’aide du portail Azure dans le modèle de déploiement Gestionnaire des ressources.
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.date: 09/02/2020
ms.author: cherylmc
ms.topic: how-to
ms.openlocfilehash: 7a7eb87f57676b469203e45e48b6f863cdf894c0
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89400651"
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a>Supprimer une passerelle de réseau virtuel à l’aide du portail

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [PowerShell (classique)](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

Cet article fournit les instructions nécessaires pour supprimer une passerelle VPN Azure déployée à l’aide du modèle de déploiement Resource Manager. Deux approches sont possibles afin de supprimer une passerelle de réseau virtuel pour une configuration de passerelle VPN.

- Si vous voulez tout supprimer et recommencer, comme dans le cas d’un environnement de test, vous pouvez supprimer le groupe de ressources. Supprimer un groupe de ressources supprime toutes les ressources du groupe. Cette méthode est recommandée seulement si vous ne voulez conserver aucune des ressources du groupe de ressources. Vous ne pouvez pas choisir de supprimer uniquement certaines ressources avec cette approche.

- Si vous souhaitez conserver certaines ressources de votre groupe de ressources, la suppression d’une passerelle de réseau virtuel devient légèrement plus complexe. Avant de supprimer la passerelle de réseau virtuel, vous devez commencer par supprimer toutes les ressources qui dépendent de la passerelle. Les étapes à suivre dépendent du type de connexions que vous avez créées et des ressources dépendantes de chaque connexion.

> [!IMPORTANT]
> Les instructions ci-dessous décrivent comment supprimer une passerelle VPN Azure déployée à l’aide du modèle de déploiement Resource Manager. Pour supprimer une passerelle VPN déployée à l’aide du modèle de déploiement classique, utilisez Azure PowerShell comme décrit [ici](vpn-gateway-delete-vnet-gateway-classic-powershell.md).


## <a name="delete-a-vpn-gateway"></a>Supprimer une passerelle VPN

Si vous souhaitez supprimer une passerelle de réseau virtuel, vous devez d’abord supprimer chaque ressource liée à la passerelle de réseau virtuel. Les ressources doivent être supprimées dans un certain ordre en raison des dépendances.

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

À ce stade, la passerelle de réseau virtuel est supprimée. Les étapes suivantes vous permettent de supprimer toutes les ressources qui ne sont plus utilisées.

### <a name="to-delete-the-local-network-gateway"></a>Pour supprimer la passerelle de réseau local

1. Sous **Toutes les ressources**, recherchez les passerelles de réseau local associées à chaque connexion.
2. Dans le panneau **Vue d’ensemble** de la passerelle de réseau local, cliquez sur **Supprimer**.

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a>Pour supprimer la ressource de l’adresse IP publique de la passerelle

1. Sous **Toutes les ressources**, recherchez la ressource d’adresse IP publique qui a été associée à la passerelle. Si la passerelle de réseau virtuel était active-active, vous verrez deux adresses IP publiques. 
2. Sur la page **Vue d’ensemble** de l’adresse IP publique, cliquez sur **Supprimer**, puis sur **Oui** pour confirmer.

### <a name="to-delete-the-gateway-subnet"></a>Pour supprimer le sous-réseau de la passerelle

1. Sous **Toutes les ressources**, recherchez le réseau virtuel. 
2. Dans le panneau **Sous-réseaux**, cliquez sur **Sous-réseau de passerelle**, puis cliquez sur **Supprimer**. 
3. Cliquez sur **Oui** pour confirmer que vous souhaitez supprimer le sous-réseau de passerelle.

## <a name="delete-a-vpn-gateway-by-deleting-the-resource-group"></a><a name="deleterg"></a>Supprimer une passerelle VPN en supprimant le groupe de ressources

Si vous n’avez pas besoin de conserver de ressources dans le groupe de ressources et que vous voulez simplement recommencer à zéro, vous pouvez supprimer tout un groupe de ressources. Il s’agit d’un moyen rapide de tout supprimer. Les étapes suivantes s’appliquent uniquement au modèle de déploiement Resource Manager.

1. Sous **Toutes les ressources**, recherchez le groupe de ressources et cliquez pour ouvrir le panneau.
2. Cliquez sur **Supprimer**. Dans le panneau Supprimer, affichez les ressources affectées. Vérifiez que vous voulez supprimer toutes ces ressources. Si ce n'est pas le cas, utilisez les étapes disponibles sous Supprimer une passerelle VPN en haut de cet article.
3. Pour continuer, saisissez le nom du groupe de ressources que vous souhaitez supprimer, puis cliquez sur **Supprimer**.
