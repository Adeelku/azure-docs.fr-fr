---
title: Opérations Microsoft Graph prises en charge
titleSuffix: Azure AD B2C
description: Index des opérations Microsoft Graph prises en charge pour la gestion des ressources Azure AD B2C, dont les utilisateurs, les flux d’utilisateurs, les fournisseurs d’identité, les stratégies personnalisées, les clés de stratégies et bien plus encore.
services: B2C
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 02/20/2020
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: 27fe1a41365d96a4179f8c659b63dc22c7b9fc93
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "78184246"
---
# <a name="microsoft-graph-operations-available-for-azure-ad-b2c"></a>Opérations Microsoft Graph disponibles pour Azure AD B2C

Les opérations suivantes de l’API Microsoft Graph sont prises en charge pour la gestion de ressources Azure AD B2C, dont les utilisateurs, les fournisseurs d’identité, les flux d’utilisateurs, les stratégies personnalisées et les clés de stratégies.

Chaque lien dans les sections suivantes cible la page correspondante dans la référence de l’API Microsoft Graph pour cette opération.

## <a name="user-management"></a>User Management

- [Répertorier les utilisateurs](https://docs.microsoft.com/graph/api/user-list)
- [Créer un utilisateur consommateur](https://docs.microsoft.com/graph/api/user-post-users)
- [Obtenir un utilisateur](https://docs.microsoft.com/graph/api/user-get)
- [Mettre à jour un utilisateur](https://docs.microsoft.com/graph/api/user-update)
- [Suppression d’un utilisateur](https://docs.microsoft.com/graph/api/user-delete)

Pour plus d’informations sur la gestion des comptes d’utilisateur Azure AD B2C avec l’API Microsoft Graph, voir [Gérer les comptes d’utilisateur Azure AD B2C avec Microsoft Graph](manage-user-accounts-graph-api.md).

## <a name="identity-providers-user-flow"></a>Fournisseurs d’identité (flux d’utilisateurs)

Gérez les fournisseurs d’identité disponibles pour vos flux d’utilisateurs dans votre locataire Azure AD B2C.

- [Répertorier les fournisseurs d’identité inscrits dans le locataire Azure AD B2C](https://docs.microsoft.com/graph/api/identityprovider-list)
- [Créer un fournisseur d’identité](https://docs.microsoft.com/graph/api/identityprovider-post-identityproviders)
- [Obtenir un fournisseur d’identité](https://docs.microsoft.com/graph/api/identityprovider-get)
- [Mettre à jour un fournisseur d’identité](https://docs.microsoft.com/graph/api/identityprovider-update)
- [Supprimer un fournisseur d’identité](https://docs.microsoft.com/graph/api/identityprovider-delete)

## <a name="user-flow"></a>Flux utilisateur

Configurez des stratégies prédéfinies pour l’inscription, la connexion, l’inscription et la connexion combinées, la réinitialisation de mot de passe et la mise à jour de profil.

- [Répertorier des flux d’utilisateur](https://docs.microsoft.com/graph/api/identityuserflow-list)
- [Créer un flux d’utilisateur](https://docs.microsoft.com/graph/api/identityuserflow-post-userflows)
- [Obtenir un flux d’utilisateur](https://docs.microsoft.com/graph/api/identityuserflow-get)
- [Supprimer un flux d’utilisateur](https://docs.microsoft.com/graph/api/identityuserflow-delete)

## <a name="custom-policies"></a>Stratégies personnalisées

Les opérations suivantes vous permettent de gérer vos stratégies d’infrastructure de confiance Azure AD B2C, appelées [stratégies personnalisées](custom-policy-overview.md).

- [Répertorier toutes les stratégies d’infrastructure de confiance configurées dans un locataire](https://docs.microsoft.com/graph/api/trustframework-list-trustframeworkpolicies)
- [Créer une stratégie d’infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframework-post-trustframeworkpolicy)
- [Lire les propriétés d’une stratégie d’infrastructure de confiance existante](https://docs.microsoft.com/graph/api/trustframeworkpolicy-get)
- [Mettre à jour ou créer une stratégie d’infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframework-put-trustframeworkpolicy)
- [Supprimer une stratégie d’infrastructure de confiance existante](https://docs.microsoft.com/graph/api/trustframeworkpolicy-delete)

## <a name="policy-keys"></a>Clés de stratégies

L’infrastructure Identity Experience Framework stocke les secrets référencés dans une stratégie personnalisée pour établir la confiance entre des composants. Ces secrets peuvent être des clés/valeurs symétriques ou asymétriques. Dans le Portail Azure, ces entités sont affichées en tant que **clés de stratégies**.

La ressource de niveau supérieur pour les clés de stratégies dans l’API Microsoft Graph est le [jeu de clés de l’infrastructure de confiance](https://docs.microsoft.com/graph/api/resources/trustframeworkkeyset). Chaque **jeu de clés** contient au moins une **clé**. Pour créer une clé, commencez par créer un jeu de clés vide, puis générez une clé dans celui-ci. Vous pouvez créer un secret manuel, charger un certificat ou une clé PKCS12. La clé peut être un secret généré, une chaîne que vous définissez (par exemple, un secret de l’application Facebook) ou un certificat que vous chargez. Si un jeu de clés compte plusieurs clés, une seule d’entre elles est active.

### <a name="trust-framework-policy-keyset"></a>Jeu de clés de stratégie d’infrastructure de confiance

- [Répertorier les jeux de clés d’infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframework-list-keysets)
- [Créer des jeux de clés d’une infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframework-post-keysets)
- [Obtenir un jeu de clés](https://docs.microsoft.com/graph/api/trustframeworkkeyset-get)
- [Mettre à jour des jeux de clés d’une infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframeworkkeyset-update)
- [Supprimer des jeux de clés d’une infrastructure de confiance](https://docs.microsoft.com/graph/api/trustframeworkkeyset-delete)

### <a name="trust-framework-policy-key"></a>Clé de stratégie d’infrastructure de confiance

- [Obtenir une clé actuellement active dans le jeu de clés](https://docs.microsoft.com/graph/api/trustframeworkkeyset-getactivekey)
- [Générer une clé dans un jeu de clés](https://docs.microsoft.com/graph/api/trustframeworkkeyset-generatekey)
- [Charger un secret basé sur une chaîne](https://docs.microsoft.com/graph/api/trustframeworkkeyset-uploadsecret)
- [Charger un certificat X.509](https://docs.microsoft.com/graph/api/trustframeworkkeyset-uploadcertificate)
- [Charger un certificat au format PKCS12](https://docs.microsoft.com/graph/api/trustframeworkkeyset-uploadpkcs12)

## <a name="applications"></a>Applications

- [Liste des applications](https://docs.microsoft.com/graph/api/application-list)
- [Créer une application](https://docs.microsoft.com/graph/api/resources/application)
- [Mettre à jour une application](https://docs.microsoft.com/graph/api/application-update)
- [Créer un principal de service](https://docs.microsoft.com/graph/api/resources/serviceprincipal)
- [Créer une allocation oauth2Permission](https://docs.microsoft.com/graph/api/resources/oauth2permissiongrant)
- [Supprimer une application](https://docs.microsoft.com/graph/api/application-delete)

## <a name="application-extension-properties"></a>Propriétés d’extension d’application

- [Répertorier des propriétés d’extension](https://docs.microsoft.com/graph/api/application-list-extensionproperty)

Azure AD B2C fournit un annuaire pouvant contenir 100 attributs personnalisés par utilisateur. Pour des flux d’utilisateurs, ces propriétés d’extension sont [gérées à l’aide du portail Azure](custom-policy-custom-attributes.md). Pour des stratégies personnalisées, Azure AD B2C crée la propriété pour vous la première fois que la stratégie écrit une valeur dans la propriété d’extension.

## <a name="audit-logs"></a>Journaux d’audit

- [Répertorier des journaux d’audit](https://docs.microsoft.com/graph/api/directoryaudit-list)

Pour plus d’informations sur l’accès aux journaux d’audit Azure AD B2C à l’aide de l’API Microsoft Graph, voir [Accès aux journaux d’audit Azure AD B2C](view-audit-logs.md).
