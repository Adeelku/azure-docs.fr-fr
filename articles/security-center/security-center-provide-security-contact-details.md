---
title: Fournir les détails du contact de sécurité dans Azure Security Center | Microsoft Docs
description: Ce document vous montre comment fournir les détails du contact de sécurité dans Azure Security Center.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/11/2020
ms.author: memildin
ms.openlocfilehash: aa35d1325e339af515c8bfc052d1af524b464e09
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91446020"
---
# <a name="set-up-email-notifications-for-security-alerts"></a>Configurer des notifications par e-mail pour les alertes de sécurité 

Pour vous assurer que les bonnes personnes au sein de votre organisation sont informées des alertes de sécurité dans votre environnement, entrez leurs adresses e-mail dans la page des paramètres **Notifications par e-mail**.

Lors de la configuration de vos notifications, vous pouvez configurer les e-mails à envoyer à des personnes spécifiques ou à toute personne disposant d’un rôle Azure spécifique pour un abonnement. 

Pour éviter la fatigue liée aux alertes, Security Center limite le volume des e-mails sortants. Pour chaque abonnement, Security Center envoie :

- un maximum de **quatre** e-mails par jour pour les alertes de **gravité élevée**
- un maximum de **deux** e-mails par jour pour les alertes de **gravité moyenne**
- un maximum d’**un** e-mail par jour pour les alertes de **faible gravité**


:::image type="content" source="./media/security-center-provide-security-contacts/email-notification-settings.png" alt-text="Configuration des détails du contact qui recevra les e-mails sur les alertes de sécurité." :::

## <a name="availability"></a>Disponibilité

|Aspect|Détails|
|----|:----|
|État de sortie :|Disponibilité générale (GA)|
|Prix :|Gratuit|
|Rôles et autorisations obligatoires :|**Administrateur de la sécurité**<br>**Propriétaire de l’abonnement** |
|Clouds :|![Oui](./media/icons/yes-icon.png) Clouds commerciaux<br>![Oui](./media/icons/yes-icon.png) US Gov (partiel)<br>![Non](./media/icons/no-icon.png) Chine Gov, autres Gov|
|||


## <a name="set-up-email-notifications-for-alerts"></a>Configurer des notifications par e-mail pour les alertes <a name="email"></a>

Vous pouvez envoyer des notifications par e-mail à des individus ou à tous les utilisateurs ayant des rôles Azure spécifiques.

1. Dans la zone **Tarification et paramètres** de Security Center, sélectionnez l’abonnement approprié, puis **Notifications par e-mail**.

1. Définissez les destinataires de vos notifications :

    - Dans la liste déroulante, sélectionnez parmi les rôles disponibles.
    - Entrez des adresses e-mail spécifiques séparées par des virgules. Vous pouvez entrer autant d’adresses e-mail que vous voulez.

1. Pour appliquer les coordonnées de sécurité à votre abonnement, sélectionnez **Enregistrer**.


## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur les alertes de sécurité, consultez les rubriques suivantes :

* [Alertes de sécurité – guide de référence](alerts-reference.md) : en savoir plus sur les alertes de sécurité possibles du module de protection contre les menaces d’Azure Security Center
* [Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité
* [Automatisation du workflow](workflow-automation.md) – Automatiser les réponses aux alertes avec une logique de notification personnalisée