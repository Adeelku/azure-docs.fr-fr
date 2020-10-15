---
title: Ajouter ou supprimer les membres d’un groupe - Azure Active Directory | Microsoft Docs
description: Instructions pour ajouter ou supprimer des membres dans un groupe à l’aide d’Azure Active Directory.
services: active-directory
author: ajburnle
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: how-to
ms.date: 08/23/2018
ms.author: ajburnle
ms.custom: it-pro, seodec18
ms.reviewer: krbain
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbb7b7da4ed5268e66260e48d6367bbe02f0845a
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87797574"
---
# <a name="add-or-remove-group-members-using-azure-active-directory"></a>Ajouter ou supprimer les membres d’un groupe avec Azure Active Directory
À l’aide d’Azure Active Directory, vous pouvez continuer à ajouter et supprimer les membres d’un groupe.

## <a name="to-add-group-members"></a>Pour ajouter des membres à un groupe

1. Connectez-vous au [portail Azure](https://portal.azure.com) à l’aide d’un compte d’administrateur général pour le répertoire.

2. Sélectionnez **Azure Active Directory**, puis **Groupes**.

3. Sur la page **Groupes - Tous les groupes**, recherchez et sélectionnez le groupe auquel vous souhaitez ajouter le membre. Dans le cas présent, utilisez notre groupe créé précédemment, **Stratégie GPM - Ouest**.

    ![Page Groupes - Tous les groupes avec le nom de groupe en surbrillance](media/active-directory-groups-members-azure-portal/group-all-groups-screen.png)

4. Sur la page **Vue d’ensemble de la stratégie GPM - Ouest**, sélectionnez **Membres** dans la zone **Gérer**.

    ![Page Vue d’ensemble de la stratégie GPM - Ouest avec l’option Membres mise en surbrillance](media/active-directory-groups-members-azure-portal/group-overview-blade.png)

5. Sélectionnez **Ajouter des membres**, puis recherchez et sélectionnez chacun des membres que vous souhaitez ajouter au groupe, puis choisissez **Sélectionner**.

    Vous recevrez un message indiquant que les membres ont été ajoutés avec succès.

    ![Page Ajouter des membres avec la recherche de membre affichée](media/active-directory-groups-members-azure-portal/update-members.png)

6. Actualisez l’écran pour voir tous les noms des membres ajoutés au groupe.

## <a name="to-remove-group-members"></a>Pour supprimer des membres du groupe

1. Sur la page **Groupes - Tous les groupes**, recherchez et sélectionnez le groupe duquel vous souhaitez supprimer le membre. Là encore, nous allons utiliser **Stratégie GPM - Ouest**.

2. Sélectionnez **Membres** à partir de la zone **Gérer**. Recherchez et sélectionnez le nom du membre à supprimer, puis sélectionnez **Supprimer**.

    ![Page d’informations sur les membres avec l’option Supprimer](media/active-directory-groups-members-azure-portal/remove-members-from-group.png)

## <a name="next-steps"></a>Étapes suivantes

- [Afficher vos groupes et vos membres](active-directory-groups-view-azure-portal.md)

- [Modifier vos paramètres de groupe](active-directory-groups-settings-azure-portal.md)

- [Gérer l’accès aux ressources à l’aide des groupes](active-directory-manage-groups.md)

- [Gérer les règles dynamiques pour les utilisateurs dans un groupe](../users-groups-roles/groups-create-rule.md)

- [Associer ou ajouter un abonnement Azure à Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
