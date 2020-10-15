---
title: Utilisation d’Azure AD pour les applications non répertoriées dans la galerie d’applications
description: Découvrez comment intégrer des applications non répertoriées dans la galerie d’Azure AD.
services: active-directory
author: kenwith
manager: celestedg
ms.service: active-directory
ms.subservice: app-mgmt
ms.topic: conceptual
ms.workload: identity
ms.date: 07/27/2020
ms.author: kenwith
ms.reviewer: arvinh,luleon
ms.openlocfilehash: 262c3a7c8a668ef25d092b5d523743e0ece89cc3
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88641141"
---
# <a name="using-azure-ad-for-applications-not-listed-in-the-app-gallery"></a>Utilisation d’Azure AD pour les applications non répertoriées dans la galerie d’applications

Dans le démarrage rapide [Ajouter une application](add-application-portal.md), vous apprendrez à ajouter une application à votre locataire Azure AD.

En plus des choix offerts dans la [galerie d’applications Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/), vous avez la possibilité d'ajouter une **application ne figurant pas dans la galerie**. 

## <a name="capabilities-for-apps-not-listed-in-the-azure-ad-gallery"></a>Capacités pour les applications non répertoriées dans la galerie d’Azure AD

Vous pouvez ajouter n’importe quelle application déjà présente dans votre organisation, ou n’importe quelle application tierce d’un fournisseur qui ne fait pas déjà partie de la galerie Azure AD. Selon votre [contrat de licence](https://azure.microsoft.com/pricing/details/active-directory/), les fonctionnalités suivantes sont disponibles :

- Intégration libre-service de toute application prenant en charge les fournisseurs d’identité [Security Assertion Markup Language (SAML) 2.0](https://wikipedia.org/wiki/SAML_2.0) (initiée par le fournisseur de services ou par le fournisseur d’identité fédérée)
- Intégration libre-service de toute application Web dont la page de connexion est basée sur le HTML et utilise une [authentification unique par mot de passe](sso-options.md#password-based-sso)
- Connexion libre-service des applications qui utilisent le protocole [System for Cross-Domain Identity Management (SCIM) pour l’approvisionnement d’utilisateurs](../app-provisioning/use-scim-to-provision-users-and-groups.md)
- Possibilité d'ajouter des liens à n'importe quelle application dans le [Lanceur d'application Office 365](https://www.microsoft.com/microsoft-365/blog/2014/10/16/organize-office-365-new-app-launcher-2/) ou [Mes applications](sso-options.md#linked-sign-on)

Si vous recherchez des instructions destinées aux développeurs sur l’intégration d’applications personnalisées avec Azure AD, consultez [Scénarios d’authentification pour Azure AD](../develop/authentication-scenarios.md). Lorsque vous développez une application utilisant un protocole moderne comme [OpenID Connect/OAuth](../develop/active-directory-v2-protocols.md) pour authentifier les utilisateurs, vous pouvez l’inscrire auprès de la plateforme d'identité Microsoft à l'aide de l'expérience [Inscriptions d'applications](../develop/quickstart-register-app.md) du portail Azure.

## <a name="next-steps"></a>Étapes suivantes

- [Série de démarrages rapides sur la gestion des applications](view-applications-portal.md)

