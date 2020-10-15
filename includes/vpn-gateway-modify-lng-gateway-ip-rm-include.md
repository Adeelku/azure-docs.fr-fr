---
title: Fichier Include
description: Fichier Include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 01/15/2020
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 6a90b23c10e08e8b14a18f9619cff5aaeb003cab
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "76045679"
---
### <a name="to-modify-the-local-network-gateway-gatewayipaddress---no-gateway-connection"></a><a name="gwipnoconnection"></a> Pour modifier la passerelle de réseau local GatewayIpAddress - sans connexion de passerelle

Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification. Utilisez l’exemple fourni pour modifier une passerelle de réseau local sans connexion de passerelle.

Lorsque vous modifiez cette valeur, vous pouvez également modifier les préfixes d’adresse en même temps. Veillez à utiliser le nom existant de votre passerelle de réseau local pour remplacer les paramètres actuels. Si vous utilisez un nom différent, vous créerez une nouvelle passerelle de réseau local au lieu de remplacer la passerelle existante.

```azurepowershell-interactive
New-AzLocalNetworkGateway -Name Site1 `
-Location "East US" -AddressPrefix @('10.101.0.0/24','10.101.1.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName TestRG1
```

### <a name="to-modify-the-local-network-gateway-gatewayipaddress---existing-gateway-connection"></a><a name="gwipwithconnection"></a>Pour modifier la passerelle de réseau local GatewayIpAddress - avec une connexion de passerelle existante

Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification. S’il existe déjà une connexion de passerelle, vous devez tout d’abord supprimer la connexion. Une fois la connexion supprimée, vous pouvez modifier l’adresse IP de la passerelle et recréer une connexion. Vous pouvez également modifier les préfixes d’adresse en même temps. Cela entraînera une interruption de votre connexion VPN. Lorsque vous modifiez l’adresse IP de la passerelle, vous n’avez pas besoin de supprimer la passerelle VPN. Vous devez uniquement supprimer la connexion.
 

1. Supprimez la connexion. Pour trouver le nom de votre connexion, exécutez la cmdlet « Get-AzVirtualNetworkGatewayConnection ».

   ```azurepowershell-interactive
   Remove-AzVirtualNetworkGatewayConnection -Name VNet1toSite1 `
   -ResourceGroupName TestRG1
   ```
2. Modifiez la valeur « GatewayIpAddress ». Vous pouvez également modifier les préfixes d’adresse en même temps. Veillez à utiliser le nom existant de votre passerelle de réseau local pour remplacer les paramètres actuels. Si vous ne le faites pas, vous créerez une nouvelle passerelle de réseau local au lieu de remplacer la passerelle existante.

   ```azurepowershell-interactive
   New-AzLocalNetworkGateway -Name Site1 `
   -Location "East US" -AddressPrefix @('10.101.0.0/24','10.101.1.0/24') `
   -GatewayIpAddress "104.40.81.124" -ResourceGroupName TestRG1
   ```
3. Créez la connexion. Dans cet exemple, nous allons configurer un type de connexion IPsec. Lorsque vous recréez votre connexion, utilisez le type de connexion spécifié pour votre configuration. Pour les autres types de connexion, consultez la page sur [les applets de commande PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .  Pour obtenir le nom de la passerelle VirtualNetworkGateway, vous pouvez exécuter la cmdlet « Get-AzVirtualNetworkGateway ».
   
    Définissez les variables.

   ```azurepowershell-interactive
   $local = Get-AzLocalNetworkGateway -Name Site1 -ResourceGroupName TestRG1

   $vnetgw = Get-AzVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
   ```
   
    Créez la connexion.

   ```azurepowershell-interactive 
   New-AzVirtualNetworkGatewayConnection -Name VNet1Site1 -ResourceGroupName TestRG1 `
   -Location "East US" `
   -VirtualNetworkGateway1 $vnetgw `
   -LocalNetworkGateway2 $local `
   -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
   ```