---
title: MFA ou 2FA et Privileged Identity Management - Azure AD | Microsoft Docs
description: Découvrez comment Azure AD Privileged Identity Management (PIM) valide l’authentification multifacteur (MFA).
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: how-to
ms.workload: identity
ms.subservice: pim
ms.date: 11/08/2019
ms.author: curtand
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf1113f7b2f396deed849fa46108537f290b53a1
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "84742094"
---
# <a name="multi-factor-authentication-and-privileged-identity-management"></a>Authentification multifacteur et Privileged Identity Management

Nous vous recommandons d’exiger une authentification multifacteur (MFA) pour tous vos administrateurs. Cela réduit le risque d'attaque en raison d'un mot de passe compromis.

Vous pouvez exiger que les utilisateurs se soumettent à une authentification multifacteur lors de leur connexion. Vous pouvez également exiger que les utilisateurs répondent à une demande d’authentification multifacteur quand ils activent un rôle dans Azure Active Directory Privileged Identity Management (PIM). De cette façon, si l’utilisateur n’a pas terminé une demande d’authentification multifacteur lors de sa connexion, il sera invité à le faire par Privileged Identity Management.

> [!IMPORTANT]
> L’authentification multifacteur Azure ne fonctionne actuellement qu’avec des comptes professionnels ou scolaires et pas avec des comptes Microsoft (généralement un compte personnel utilisé pour se connecter à des services Microsoft tels que Skype, Xbox ou Outlook.com). C’est pourquoi une personne disposant d’un compte personnel ne peut pas être un administrateur éligible car elle ne peut pas utiliser l’authentification multifacteur pour activer ses rôles. Si ces utilisateurs doivent continuer à gérer les charges de travail à l’aide d’un compte Microsoft, convertissez-les en administrateurs permanents pour l’instant.

## <a name="how-pim-validates-mfa"></a>Comment PIM valide MFA

Il existe deux options pour valider l’authentification multifacteur lorsqu’un utilisateur active un rôle.

Le plus simple consiste à s’appuyer sur l’authentification multifacteur Azure pour les utilisateurs qui activent un rôle privilégié. Pour ce faire, vérifiez tout d’abord que ces utilisateurs bénéficient d’une licence si nécessaire, et qu’ils se sont enregistrés pour l’authentification multifacteur Azure. Pour plus d’informations sur la façon de déployer l’authentification multifacteur, voir [Déployer une authentification multifacteur Azure basée sur le cloud](../authentication/howto-mfa-getstarted.md). Il est recommandé, mais pas obligatoire, de configurer Azure AD pour appliquer l’authentification multifacteur à ces utilisateurs lorsqu’ils se connectent. Cela est dû au fait que les vérifications de l’authentification multifacteur sont effectuées par Privileged Identity Management lui-même.

Si les utilisateurs s’authentifient en local, vous pouvez également faire en sorte que votre fournisseur d’identité soit responsable de l’authentification multifacteur. Par exemple, si vous avez configuré des services ADFS pour exiger l’authentification par carte à puce avant d’accéder à Azure AD, la section [Sécurisation des ressources de cloud avec le serveur Azure Multi-Factor Authentication et ADFS](../authentication/howto-mfa-adfs.md) inclut des instructions pour configurer ADFS afin d’envoyer les revendications à Azure AD. Quand un utilisateur tente d’activer un rôle, Privileged Identity Management accepte l’authentification multifacteur déjà validée pour l’utilisateur dès réception des revendications appropriées.

## <a name="next-steps"></a>Étapes suivantes

- [Configurer les paramètres des rôles Azure AD dans Privileged Identity Management](pim-how-to-change-default-settings.md)
- [Configurer les paramètres des rôles de ressources Azure dans Privileged Identity Management](pim-resource-roles-configure-role-settings.md)
