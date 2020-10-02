---
title: Guide de publication d’offres de machine virtuelle pour la Place de marché Azure
description: Cet article décrit les conditions requises pour publier une machine virtuelle et un essai logiciel gratuit à déployer à partir de la Place de marché Azure.
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
author: iqshahmicrosoft
ms.author: iqshah
ms.date: 09/04/2020
ms.openlocfilehash: cc6b040731cbeb7271d7a7c0de1c32fa2d007013
ms.sourcegitcommit: de2750163a601aae0c28506ba32be067e0068c0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89484186"
---
# <a name="publishing-guide-for-virtual-machine-offers"></a>Guide de publication d’offres de machines virtuelles

La publication d’images de machine virtuelle constitue l’un des principaux moyens de publier une solution sur la Place de marché Azure. Utilisez ce guide pour comprendre les exigences propres à ce type d’offre. 

Les offres de machine virtuelle sont des offres de transaction qui sont déployées et facturées via la Place de marché Azure. L’option de référencement qu’un utilisateur voit est *Obtenir maintenant*.

## <a name="free-trial"></a>Essai gratuit 

Pour donner aux utilisateurs la possibilité de tester votre offre, proposez des licences logicielles à durée limitée lorsque vous utilisez le modèle de facturation BYOL (apportez votre propre licence). 

## <a name="test-drive"></a>Test drive

Vous pouvez déployer une ou plusieurs machines virtuelles par le biais d’applications IaaS (infrastructure as a service) ou SaaS (software as a service). L’avantage de l’option de publication *Test drive* est la configuration automatique d’une machine virtuelle ou de la solution complète dirigé par une visite guidée hébergée par un partenaire. Un test drive permet à vos clients d’évaluer des machines virtuelles sans coût supplémentaire. Un client n’est pas tenu d’être un client Azure existant pour opter pour l’expérience d’essai. 

Pour plus d’informations sur les versions d’évaluation, consultez [Qu’est-ce qu’une version d’évaluation ?](what-is-test-drive.md).

|Spécifications  |Détails |
|---------|---------|
| Vous avez une application de la Place de marché Azure   |  Une ou plusieurs machines virtuelles via IaaS ou SaaS.      |

## <a name="interactive-demo"></a>Démonstration interactive

Grâce à cette offre, vous proposez à vos clients une expérience guidée de votre solution à l’aide d’une démonstration interactive. L’avantage de l’option de publication Démonstration interactive est qu’elle propose une expérience d’essai sans avoir à effectuer une configuration compliquée de votre solution complexe. 

## <a name="virtual-machine-offer"></a>Offre de machine virtuelle

Utilisez le type d’offre *Machine virtuelle* si vous déployez une appliance virtuelle dans le cadre de l’abonnement associé à votre client. Les machines virtuelles sont entièrement commercialisables à l’aide des modèles de licence Paiement à l’utilisation ou BYOL (apportez votre propre licence). Microsoft héberge la transaction commerciale et facture votre client pour votre compte. Vous avez ainsi l’avantage utiliser la relation de paiement préférée entre votre client et Microsoft, et notamment un éventuel contrat Entreprise.

> [!NOTE]
> À ce jour, les engagement monétaires associés à un Contrat Entreprise peuvent être utilisés pour l’utilisation par Azure de votre machine virtuelle, mais pas pour vos frais de licence logicielle.  
> 
> [!NOTE]
> Vous pouvez limiter la découverte et le déploiement de votre machine virtuelle à un ensemble spécifique de clients en publiant l’image et les tarifs sous forme d’offre privée. Les offres privées vous permettent de créer des offres exclusives pour vos clients les plus fidèles et de proposer des conditions et des logiciels personnalisés. Les conditions personnalisées vous permettent de présenter différents scénarios, notamment des offres économiques avec des conditions et des tarifs adaptés ainsi qu’un accès en avant-première à des logiciels en version limitée. Les offres privées vous permettent de proposer des tarifs ou des produits spécifiques à un ensemble limité de clients en créant un plan avec ces informations.  
>
> Pour plus d’informations, consultez [Offres privées sur la Place de marché Azure](https://azure.microsoft.com/blog/private-offers-on-azure-marketplace)  

| Condition requise | Détails |  
|:--- |:--- | 
| Facturation et mesure | Votre machine virtuelle doit prendre en charge la facturation mensuelle BYOL ou avec paiement à l’utilisation. |  
| Disque dur virtuel compatible avec Azure | Les machines virtuelles doivent être basées sur Windows ou Linux. Pour plus d'informations sur la création d'un VHD, voir : <ul> <li>[Distributions Linux approuvées sur Azure](../virtual-machines/linux/endorsed-distros.md) (pour les disques durs virtuel Linux).</li> <li>[Créez un disque dur virtuel compatible avec Azure](./partner-center-portal/azure-vm-create-offer.md) (pour les disques durs virtuels Windows).</li> </ul> |  

>[!Note]
>L’abonnement à un réseau de partenaires fournisseurs de solution cloud est maintenant disponible. Pour plus d’informations sur le marketing de votre offre via les réseaux de partenaires fournisseurs de solutions cloud Microsoft, consultez [Fournisseurs de solutions cloud](./cloud-solution-providers.md).

## <a name="next-steps"></a>Étapes suivantes

Si vous ne l’avez pas déjà fait, découvrez comment [développer votre activité dans le cloud avec la Place de marché Azure](https://azuremarketplace.microsoft.com/sell).

Pour vous inscrire à l’Espace partenaires et commencer à travailler dessus :

- [Connectez-vous à l’Espace partenaires](https://partner.microsoft.com/dashboard/account/v3/enrollment/introduction/partnership) pour créer ou terminer votre offre.
- Pour plus d’informations, consultez [Créer une machine virtuelle](./partner-center-portal/azure-vm-create-offer.md).
