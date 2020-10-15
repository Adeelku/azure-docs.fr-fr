---
title: Vérification en deux étapes - Azure MFA et ADFS - Azure Active Directory
description: Ceci est la page d'Azure Multi-Factor Authentication qui explique la prise en main d’Azure MFA et des services AD FS.
services: multi-factor-authentication
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 11/21/2019
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.reviewer: michmcla
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fbbba49ddf2252e22cb32a0b8adc6fa2070e999
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "74847131"
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Prise en main d’Azure Multi-Factor Authentication et des services de fédération Active Directory (AD FS)

<center>

![Prise en main d'Azure MFA et d'ADFS](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Si votre organisation a fédéré votre Active Directory local avec Azure Active Directory à l’aide d’AD FS, vous disposez de deux options pour l’utilisation d’Azure Multi-Factor Authentication.

* Sécuriser les ressources de cloud à l’aide de l’authentification multifacteur Azure ou des services de fédération Active Directory (AD FS)
* Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication

Le tableau suivant résume le processus de vérification avec la sécurisation des ressources à l’aide d’Azure Multi-Factor Authentication et AD FS

| Processus de vérification : applications basées sur le navigateur | Processus de vérification : applications hors navigateur |
|:--- |:--- |
| Sécurisation des ressources Azure AD à l'aide d’Azure Multi-Factor Authentication |<li>La première étape de vérification est effectuée en local à l’aide d’AD FS.</li> <li>La seconde étape est une méthode par téléphone effectuée à l’aide de l’authentification cloud.</li> |
| Sécurisation des ressources Azure AD à l'aide des services ADFS |<li>La première étape de vérification est effectuée en local à l’aide d’AD FS.</li><li>La seconde étape est effectuée localement en répondant à la demande.</li> |

Mises en garde relatives aux mots de passe d'application pour les utilisateurs fédérés :

* Les mots de passe d’applications sont vérifiés à l’aide de l’authentification cloud et contournent donc la fédération. La fédération n’est utilisée activement que lorsque vous configurez un mot de passe d’application.
* Les paramètres de contrôle d’accès client locaux ne sont pas honorés par les mots de passe d’application.
* Vous perdez la fonctionnalité de journalisation-authentification locale pour les mots de passe d’application.
* La désactivation/suppression de compte peut mettre jusqu’à 3 heures pour synchroniser les répertoires, ce qui peut retarder la désactivation/suppression des mots de passe d’application dans l’identité de cloud.

Pour plus d’informations sur la configuration d’Azure Multi-Factor Authentication ou du serveur Azure Multi-Factor Authentication avec AD FS, consultez les articles suivants :

* [Sécuriser les ressources cloud à l’aide d’Azure Multi-Factor Authentication et AD FS](howto-mfa-adfs.md)
* [Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec Windows Server 2012 R2 AD FS](howto-mfaserver-adfs-2012.md)
* [Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec AD FS 2.0](howto-mfaserver-adfs-2.md)
