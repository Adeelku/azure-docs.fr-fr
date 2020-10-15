---
title: Fichier Include
description: Fichier Include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 61082333afc88abef0a8d8a57d1f1b1d893b6148
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "67176921"
---
### <a name="to-view-local-network-gateways"></a>Pour afficher les passerelles de réseau local

Pour afficher une liste des passerelles de réseau local, utilisez la commande [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway).

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a>Pour vérifier les valeurs de clé partagée

Vérifiez que la valeur de clé partagée est identique à celle utilisée pour la configuration de votre périphérique VPN. Si ce n’est pas le cas, exécutez à nouveau la connexion en utilisant la valeur du périphérique ou mettez à jour le périphérique avec la valeur obtenue. Les valeurs doivent correspondre. Pour afficher la clé partagée, utilisez [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a>Pour afficher l’adresse IP publique de la passerelle VPN

Pour trouver l’adresse IP publique de votre passerelle de réseau virtuel, utilisez la commande [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip). Pour faciliter la lecture, la sortie de cet exemple est mise en forme pour afficher la liste des adresses IP publiques sous forme de tableau.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
