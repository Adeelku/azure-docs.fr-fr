---
title: Fichier include
description: Fichier include
services: active-directory
author: rolyon
ms.service: active-directory
ms.topic: include
ms.date: 05/26/2020
ms.author: barclayn
ms.custom: include file
ms.openlocfilehash: ee02200f1fb32d430a858d218e27534561ebc24a
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "83868069"
---
## <a name="create-one-or-more-access-reviews"></a>Créer une ou plusieurs révisions d’accès

1. Cliquez sur **Nouveau** pour créer une révision d’accès.

1. Nommez la révision d’accès. Si vous le souhaitez, vous pouvez fournir une description de cette révision. Les réviseurs ont accès au nom et à la description de la révision.

    ![Créer une révision d’accès - Nom et description de la révision](./media/active-directory-privileged-identity-management-access-reviews/name-description.png)

1. Définissez la **Date de début**. Par défaut, une révision d’accès se produit une seule fois, démarre le jour même de sa création et s’arrête un mois plus tard. Vous pouvez modifier les dates de début et de fin pour que la révision d’accès démarre ultérieurement et dure le nombre de jours souhaité.

    ![Date de début, fréquence, durée, fin, nombre de tentatives et date de fin](./media/active-directory-privileged-identity-management-access-reviews/start-end-dates.png)

1. Pour que la révision d’accès soit périodique, modifiez le paramètre **Fréquence** en remplaçant la valeur **Une fois** par **Hebdomadaire**, **Mensuel**, **Trimestriel**, **Annuel** ou **Semestriel**. Utilisez la zone de texte ou le curseur **Durée** pour définir le nombre de jours pendant lequel chaque révision de la série périodique pourra être modifiée par les réviseurs. Par exemple, la durée maximale d’une révision mensuelle est de 27 jours, ce qui permet d’éviter le chevauchement des révisions.

1. Utilisez le paramètre **Fin** pour spécifier comment mettre fin à la série de révisions d’accès récurrentes. Les séries accès récurrentes peuvent se terminer de trois façons : elles peuvent s’exécuter de façon continue pour démarrer des révisions indéfiniment, s’exécuter jusqu’à une date spécifique ou s’exécuter jusqu’à ce qu’un nombre défini d’occurrences se soient produites. Un autre administrateur d’utilisateur, ou un autre administrateur d’entreprise ou vous-même pouvez arrêter la série après sa création en modifiant la date définie dans la zone **Paramètres**, afin qu’elle s’arrête à cette date.

1. Dans la section **Utilisateurs**, sélectionnez un ou plusieurs rôles dont vous souhaitez vérifier l’appartenance.

    ![Étendue des utilisateurs pour la révision d’une appartenance à un rôle](./media/active-directory-privileged-identity-management-access-reviews/users.png)

    > [!NOTE]
    > - Les rôles sélectionnés ici incluent des [rôles permanents et éligibles](../articles/active-directory/privileged-identity-management/pim-how-to-add-role-to-user.md).
    > - La sélection de plusieurs rôles crée plusieurs révisions d’accès. Par exemple, en sélectionnant cinq rôles, vous créez cinq révisions d’accès distinctes.

    Si vous créez une révision d’accès des **rôles Azure AD**, l’exemple suivant présente une liste Révision d’appartenance.

    ![Volet Révision d’appartenance répertoriant les rôles Azure AD que vous pouvez sélectionner](./media/active-directory-privileged-identity-management-access-reviews/review-membership.png)

    Si vous créez une révision d’accès des **rôles de ressource Azure**, l’image suivant présente une liste Révision d’appartenance.

    ![Volet Révision d’appartenance répertoriant les rôles de ressource Azure que vous pouvez sélectionner](./media/active-directory-privileged-identity-management-access-reviews/review-membership-azure-resource-roles.png)

1. Dans la section **Réviseurs**, sélectionnez une ou plusieurs personnes pour vérifier tous les utilisateurs. Sinon, vous pouvez choisir de faire en sorte que les membres vérifient leur propre accès.

    ![Liste pour les réviseurs des utilisateurs ou membres sélectionnés (auto)](./media/active-directory-privileged-identity-management-access-reviews/reviewers.png)

    - **Utilisateurs sélectionnés** : utilisez cette option lorsque vous ne savez pas qui a besoin de l’accès. Avec cette option, vous pouvez affecter la révision à un propriétaire de ressource ou un responsable de groupe.
    - **Membres (auto)** : utilisez cette option pour demander aux utilisateurs de réviser leurs propres attributions de rôles.

### <a name="upon-completion-settings"></a>Paramètres de saisie semi-automatique

1. Pour spécifier ce qui se passe après la fin d’une révision, développez la section **Paramètres de saisie semi-automatique**.

    ![Paramètres de saisie semi-automatique pour appliquer automatiquement et « Le réviseur ne doit pas répondre »](./media/active-directory-privileged-identity-management-access-reviews/upon-completion-settings.png)

1. Si vous voulez supprimer automatiquement l’accès pour les utilisateurs qui ont été refusés, définissez **Appliquer automatiquement les résultats à ressource** sur **Activer**. Si vous voulez appliquer manuellement les résultats quand la révision est terminée, cliquez sur **Désactiver**.

1. Utilisez la liste **Le réviseur ne doit pas répondre** pour spécifier ce qui se passe pour les utilisateurs qui ne sont pas vérifiés par le réviseur au cours de la révision. Ce paramètre n’affecte pas les utilisateurs qui ont été vérifiés manuellement par les réviseurs. Si la décision finale du réviseur est Refuser, l’accès de l’utilisateur est supprimé.

    - **Aucune modification** : laisser l’accès de l’utilisateur inchangé
    - **Supprimer l’accès** : supprimer l’accès de l’utilisateur
    - **Approuver l’accès** : approuver l’accès de l’utilisateur
    - **Accepter les recommandations** : accepter la recommandation du système sur le refus ou l’approbation de la prolongation de l’accès de l’utilisateur

### <a name="advanced-settings"></a>Paramètres avancés

1. Pour spécifier d’autres paramètres, développez la section **Paramètres avancés**.

    ![Paramètres avancés pour afficher des recommandations, exiger la raison lors de l’approbation, notifications par courrier électronique et rappels](./media/active-directory-privileged-identity-management-access-reviews/advanced-settings.png)

1. Définissez **Afficher les recommandations** sur **Activer** pour montrer aux réviseurs les recommandations du système basées sur les informations des accès de l’utilisateur.

1. Définissez **Exiger la raison lors de l’approbation** sur **Activer** afin d’exiger que le réviseur indique un motif pour l’approbation.

1. Définissez **Notifications par e-mail** sur **Activer** pour qu’Azure AD envoie des notifications par e-mail aux réviseurs quand une révision d’accès commence et aux administrateurs quand une révision se termine.

1. Définissez **Rappels** sur **Activer** pour qu’Azure AD envoie des rappels concernant les révisions d’accès en cours aux réviseurs qui n’ont pas terminé leur révision.
