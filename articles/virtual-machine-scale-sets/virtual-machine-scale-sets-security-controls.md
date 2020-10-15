---
title: Contrôles de sécurité pour Azure Virtual Machine Scale Sets
description: Check-list des contrôles de sécurité pour l’évaluation d’Azure Virtual Machine Scale Sets
author: mimckitt
ms.author: mimckitt
ms.topic: conceptual
ms.service: virtual-machine-scale-sets
ms.subservice: security
ms.date: 09/05/2019
ms.reviewer: jushiman
ms.custom: mimckitt
ms.openlocfilehash: 4480ad425d9a3953fd5779f99d27b5b6b037e61e
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87029414"
---
# <a name="security-controls-for-azure-virtual-machine-scale-sets"></a>Contrôles de sécurité pour Azure Virtual Machine Scale Sets

Cet article décrit les contrôles de sécurité intégrés dans Azure Virtual Machine Scale Sets.

[!INCLUDE [Security controls header](../../includes/security-controls-header.md)]

## <a name="network"></a>Réseau

| Contrôle de sécurité | Oui/Non | Notes |
|---|---|--|
| Prise en charge du point de terminaison de service| Oui | |
| Prise en charge de l’injection de réseau virtuel| Oui | |
| Prise en charge de l’isolement réseau et de l’installation de pare-feu| Oui |  |
| Prise en charge du tunneling forcé| Oui | Consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement Azure Resource Manager](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md). |

## <a name="monitoring--logging"></a>Supervision et journalisation

| Contrôle de sécurité | Oui/Non | Notes|
|---|---|--|
| Prise en charge de la supervision Azure (Log analytics, App insights, etc.)| Oui | Consultez [Superviser et mettre à jour une machine virtuelle Linux dans Azure](../virtual-machines/linux/tutorial-monitor.md) et [Superviser et mettre à jour une machine virtuelle Windows dans Azure](../virtual-machines/windows/tutorial-monitor.md). |
| Journalisation et audit du plan de gestion et de contrôle| Oui |  |
| Journalisation et audit du plan de données | Non |  |

## <a name="identity"></a>Identité

| Contrôle de sécurité | Oui/Non | Notes|
|---|---|--|
| Authentification| Oui |  |
| Autorisation| Oui |  |

## <a name="data-protection"></a>Protection de données

| Contrôle de sécurité | Oui/Non | Notes |
|---|---|--|
| Chiffrement côté serveur au repos : Clés managées par Microsoft | Oui | Consultez [Azure Disk Encryption pour les groupes de machines virtuelles identiques](disk-encryption-overview.md). |
| Le chiffrement en transit (tel que le chiffrement ExpressRoute, le chiffrement dans un réseau virtuel, et le chiffrement de réseau virtuel à réseau virtuel)| Oui | Le service Machines virtuelles Azure prend en charge [ExpressRoute](../expressroute/index.yml) et le chiffrement de réseau virtuel. Consultez [Chiffrement en transit sur des machines virtuelles](../security/fundamentals/encryption-overview.md#in-transit-encryption-in-vms). |
| Chiffrement côté serveur au repos : clés gérées par le client (BYOK) | Oui | Les clés gérées par le client sont un scénario de chiffrement Azure pris en charge ; consultez [Azure Disk Encryption pour les groupes de machines virtuelles identiques](disk-encryption-overview.md)|
| Chiffrement au niveau des colonnes (Azure Data Services)| N/A | |
| Appels d’API chiffrés| Oui | Par le biais de HTTPS et de TLS. |

## <a name="configuration-management"></a>Gestion des configurations

| Contrôle de sécurité | Oui/Non | Notes|
|---|---|--|
| Prise en charge de la gestion de la configuration (gestion de version de la configuration, etc.)| Oui |  | 

## <a name="next-steps"></a>Étapes suivantes

- Apprenez-en plus sur les [contrôles de sécurité intégrés des services Azure](../security/fundamentals/security-controls.md).
