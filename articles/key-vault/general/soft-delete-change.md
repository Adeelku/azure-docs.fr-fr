---
title: La suppression réversible sera activée sur tous les coffres de clés Azure | Microsoft Docs
description: Utilisez ce document pour adopter la suppression réversible pour tous les coffres de clés.
services: key-vault
author: ShaneBala-keyvault
manager: ravijan
tags: azure-resource-manager
ms.service: key-vault
ms.topic: conceptual
ms.date: 07/27/2020
ms.author: sudbalas
ms.openlocfilehash: 0e811cc219002c034afb968be760ce2c249b08f3
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91825248"
---
# <a name="soft-delete-will-be-enabled-on-all-key-vaults"></a>La suppression réversible sera activée sur tous les coffres de clés

> [!WARNING]
> **Changement cassant** : La possibilité de refuser la suppression réversible sera dépréciée à la fin de l’année et la protection de la suppression réversible sera automatiquement activée pour tous les coffres de clés.  Il est recommandé aux utilisateurs et aux administrateurs d’Azure Key Vault d’activer immédiatement la suppression réversible sur leurs coffres de clés.
>
> Pour Managed HSM, la suppression réversible est activée par défaut et ne peut pas être désactivée.

Quand un secret est supprimé d’un coffre de clés sans la protection de la suppression réversible, le secret est définitivement supprimé. Les utilisateurs peuvent actuellement refuser la suppression réversible lors de la création du coffre de clés ; cependant, pour protéger vos secrets contre les suppressions accidentelles ou malveillantes par un utilisateur, Microsoft activera prochainement la protection de la suppression réversible sur **tous** les coffres de clés, et les utilisateurs n’auront plus la possibilité de refuser ou de désactiver la suppression réversible.

:::image type="content" source="../media/softdeletediagram.png" alt-text="<texte alternatif>":::

Pour plus d’informations sur la fonctionnalité de suppression réversible, consultez [Vue d’ensemble de la suppression réversible d’Azure Key Vault](soft-delete-overview.md).

## <a name="how-do-i-respond-to-breaking-changes"></a>Comment répondre aux changements cassants

Vous ne pouvez pas créer un objet de coffre de clés avec le même nom qu’un objet de coffre de clés dans l’état de suppression réversible.  Par exemple, si vous supprimez une clé nommée `test key` dans le coffre de clés A, vous ne pouvez pas créer une clé nommée `test key` dans le coffre de clés A tant que l’objet `test key` supprimé de façon réversible n’est pas supprimé définitivement.

### <a name="application-changes"></a>Changements dans l’application

Si votre application suppose que la suppression réversible n’est pas activée, et qu’elle s’attend à ce que les noms de secrets ou de coffres de clés supprimés soient disponibles pour une réutilisation immédiate, la logique de votre application doit implémenter les modifications suivantes afin d’adopter ce changement.

1. Supprimer le coffre de clés ou le secret d’origine
2. Supprimez définitivement le coffre de clés ou le secret qui est dans l’état de suppression réversible.
3. Attendez : la recréation immédiate peut entraîner un conflit.
4. Recréez le coffre de clés avec le même nom.
5. Implémentez de nouvelles tentatives si l’opération de création provoque à nouveau une erreur de conflit de noms : dans le pire des scénarios, jusqu’à 10 minutes peuvent être nécessaires pour que les enregistrements DNS soient mis à jour.

### <a name="administration-changes"></a>Changements au niveau de l’administration

Les principaux de sécurité qui ont besoin d’un accès pour supprimer définitivement des secrets doivent disposer d’autorisations de stratégie d’accès supplémentaires pour supprimer définitivement ces secrets et le coffre de clés.

Si vous avez une stratégie Azure sur vos coffres de clés qui impose que la suppression réversible soit désactivée, cette stratégie doit être désactivée.  Il peut être nécessaire de faire remonter ce problème à un administrateur qui contrôle les stratégies Azure appliquées à votre environnement. Si cette stratégie n’est pas désactivée, vous pouvez perdre la possibilité de créer de nouveaux coffres de clés dans l’étendue de la stratégie appliquée.

Si votre organisation est soumise à des exigences de conformité légales et qu’elle ne peut pas autoriser la suppression des coffres de clés et des secrets de façon à rester dans un état récupérable, pendant une période étendue, vous devez ajuster la période de conservation de la suppression réversible, qui peut être configurée entre 7 et 90 jours, pour répondre aux standards de votre organisation.

## <a name="procedures"></a>Procédures

### <a name="audit-your-key-vaults-to-check-if-soft-delete-is-enabled"></a>Auditer vos coffres de clés pour vérifier si la suppression réversible est activée

1. Connectez-vous au portail Azure.
2. Recherchez « Azure Policy ».
3. Sélectionnez « Définitions ».
4. Sous Catégorie, sélectionnez « Key Vault » dans le filtre.
5. Sélectionnez « Les objets Key Vault doivent être récupérables ».
6. Cliquez sur « Affecter ».
7. Définissez l’étendue à votre abonnement.
8. Sélectionnez « Vérifier + créer ».
9. Une analyse complète de votre environnement peut prendre jusqu’à 24 heures.
10. Dans le panneau Azure Policy, cliquez sur « Conformité ».
11. Sélectionnez la stratégie que vous avez appliquée.

Vous devez maintenant être en mesure de filtrer et de voir les coffres de clés pour lesquels la suppression réversible est activée (ressources conformes) et les coffres de clés pour lesquels la suppression réversible n’est pas activée (ressources non conformes).

### <a name="turn-on-soft-delete-for-an-existing-key-vault"></a>Activer la suppression réversible pour un coffre de clés existant

1. Connectez-vous au portail Azure.
2. Recherchez votre coffre de clés.
3. Sous Paramètres, sélectionnez « Propriétés ».
4. Sous Suppression réversible, sélectionnez la case d’option « Activer la récupération de ce coffre et de ses objets ».
5. Définir la période de conservation pour la suppression réversible.
6. Sélectionnez « Enregistrer ».

### <a name="grant-purge-access-policy-permissions-to-a-security-principal"></a>Accorder des autorisations de stratégie d’accès de suppression définitive à un principal de sécurité

1. Connectez-vous au portail Azure.
2. Recherchez votre coffre de clés.
3. Sélectionnez « Stratégies d’accès » sous Paramètres.
4. Sélectionnez le principal de service auquel vous voulez accorder l’accès.
5. Pour chaque liste déroulante sous les autorisations de clé, de secret et de certificat, faites défiler jusqu’à « Opérations avec privilèges » et sélectionnez l’autorisation « Vider ».

## <a name="frequently-asked-questions"></a>Forum aux questions

### <a name="does-this-change-affect-me"></a>Ce changement m’affecte-t-il ?

Si vous avez déjà activé la suppression réversible, ou si vous ne supprimez pas des objets de coffre de clés pour ensuite les recréer avec le même nom, vous ne remarquerez probablement aucun changement de comportement du coffre de clés.

Si vous avez d’une application qui supprime et recrée fréquemment des objets de coffre de clés avec les mêmes conventions de nommage, vous devrez apporter des modifications à la logique de votre application pour conserver le comportement attendu. Consultez la section « Comment répondre aux changements cassants » ci-dessus.

### <a name="how-do-i-benefit-from-this-change"></a>Quel est le bénéfice de ce changement ?

La protection contre la suppression réversible offre à votre organisation une couche supplémentaire de protection contre la suppression accidentelle ou malveillante. En tant qu’administrateur d’un coffre de clés, vous pouvez restreindre l’accès aux autorisations de récupération et de vidage.

Si un utilisateur supprime accidentellement un coffre de clés ou un secret, vous pouvez lui accorder des autorisations d’accès pour récupérer le secret proprement dit sans créer de risque qu’il supprime définitivement le secret ou le coffre de clés. Ce processus de libre-service permet de réduire le temps d’indisponibilité de votre environnement et de garantir la disponibilité de vos secrets.

### <a name="how-do-i-find-out-if-i-need-to-take-action"></a>Comment savoir si je dois agir ?

Suivez les étapes ci-dessus dans la section intitulée « Procédure pour auditer vos coffres de clés de façon à vérifier si la suppression réversible est activée ». Les coffres de clés pour lesquels la suppression réversible n’est pas activée seront affectés par cette modification. Des outils supplémentaires pour vous aider à effectuer les audits seront bientôt disponibles, et ce document sera alors mis à jour.

### <a name="what-action-do-i-need-to-take"></a>Quelle action dois-je effectuer ?

Vérifiez que vous n’avez pas besoin d’apporter des modifications à la logique de votre application. Une fois que vous avez la confirmation de cela, activez la suppression réversible sur tous vos coffres de clés. Vous êtes ainsi certain que vous ne serez pas affecté par un changement cassant quand la suppression réversible sera activée pour tous les coffres de clés à la fin de l’année.

### <a name="by-when-do-i-need-to-take-action"></a>Quand dois-je agir ?

La suppression réversible sera activée pour tous les coffres de clés à la fin de l’année. Pour garantir que vos applications ne sont pas affectées, activez dès que possible la suppression réversible sur vos coffres de clés.

## <a name="what-will-happen-if-i-dont-take-any-action"></a>Que se passe-t-il si je n’effectue aucune action ?

Si vous n’effectuez aucune action, la suppression réversible sera automatiquement activée pour tous vos coffres de clés à la fin de l’année. Ceci peut entraîner des erreurs de conflit si vous tentez de supprimer un objet de coffre de clés et de le recréer avec le même nom sans d’abord le vider dans l’état de suppression réversible. Cela peut entraîner l’échec de vos applications ou de l’automatisation.

## <a name="next-steps"></a>Étapes suivantes

- Pour toute question concernant ce changement, contactez-nous à l’adresse [akvsoftdelete@microsoft.com](mailto:akvsoftdelete@microsoft.com).
- Lisez [Vue d’ensemble de la suppression réversible](soft-delete-overview.md)
