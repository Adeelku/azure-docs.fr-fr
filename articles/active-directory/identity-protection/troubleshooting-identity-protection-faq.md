---
title: FAQ sur Identity Protection dans Azure Active Directory
description: Forum Aux Questions sur Azure AD Identity Protection
services: active-directory
ms.service: active-directory
ms.subservice: identity-protection
ms.topic: troubleshooting
ms.date: 10/07/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sahandle
ms.collection: M365-identity-device-management
ms.openlocfilehash: a249d5f3c47e8e8789f91f355c791cc50341ab01
ms.sourcegitcommit: d2222681e14700bdd65baef97de223fa91c22c55
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91827903"
---
# <a name="frequently-asked-questions-identity-protection-in-azure-active-directory"></a>Forum aux questions sur Identity Protection dans Azure Active Directory

## <a name="dismiss-user-risk-known-issues"></a>Faire disparaître les problèmes connus liés aux risques de l’utilisateur

**Ignorer les risques utilisateur** dans la version classique d’Identity Protection définit l’acteur dans l’historique des risques utilisateur d’Identity Protection sur **Azure AD**.

L’option **Ignorer le risque lié à l’utilisateur** dans Identity Protection définit l’acteur dans l’historique des risques de l’utilisateur dans Identity Protection sur **\<Admin’s name with a hyperlink pointing to user’s blade\>** .

Un problème connu occasionne actuellement des latences dans le flux de rejet des risques utilisateur. Si vous disposez d'une « Stratégie de risque utilisateur », celle-ci cessera de s'appliquer aux utilisateurs ignorés quelques minutes après un clic sur « Ignorer le risque lié à l'utilisateur ». Cela dit, des retards d'actualisation de l'« état de risque » des utilisateurs ignorés ont été identifiés. Pour contourner ce problème, actualisez la page au niveau du navigateur afin d'afficher le dernier « État de risque » de l'utilisateur.

## <a name="risky-users-report-known-issues"></a>Les utilisateurs à risque signalent les problèmes connus

Les requêtes sur le champ **Nom d’utilisateur** respectent la casse, alors que les requêtes sur le champ **Nom** ne sont pas sensibles à la casse.

Désactivez **Show dates as** (Afficher les dates en tant que) pour masquer la colonne **RISK LAST UPDATED** (Dernière mise à jour du risque). Pour lire la colonne, cliquez sur **Colonnes** en haut du panneau des utilisateurs à risque.

**Ignorer tous les événements** dans la version classique d’Identity Protection définit l’état des détections de risque sur **Closed (resolved)** (Fermé (résolu)).

## <a name="risky-sign-ins-report-known-issues"></a>Problèmes connus du rapport sur les connexions à risque

**Résoudre** sur une détection de risque définit l’état sur **Users passed MFA driven by risk-based policy** (Les utilisateurs ont passé la MFA pilotée par une stratégie basée sur les risques).

## <a name="frequently-asked-questions"></a>Forum aux questions

### <a name="why-is-a-user-is-at-risk"></a>Pourquoi un utilisateur est-il à risque ?

Si vous êtes un client Azure AD Identity Protection, accédez à la vue [Utilisateurs à risque](howto-identity-protection-investigate-risk.md#risky-users), puis cliquez sur un utilisateur à risque. Dans le tiroir en bas, l’onglet « Historique des risques » affiche tous les événements qui ont entraîné un changement de risque de l’utilisateur. Pour afficher toutes les connexions à risque pour l’utilisateur, cliquez sur « Connexions risquées de l’utilisateur ». Pour afficher toutes les détections de risque pour cet utilisateur, cliquez sur « Détection des risques de l’utilisateur ».

### <a name="how-can-i-get-a-report-of-detections-of-a-specific-type"></a>Comment puis-je obtenir un rapport sur les détections d’un type spécifique ?

Accédez à la vue de détection des risques et filtrez par « Type de détection ». Vous pouvez ensuite télécharger ce rapport au format .CSV ou .JSON à l’aide du bouton **Télécharger** au sommet. Pour plus d’informations, consultez l’article [Guide pratique : Examiner les risques](howto-identity-protection-investigate-risk.md#risk-detections).

### <a name="why-cant-i-set-my-own-risk-levels-for-each-risk-detection"></a>Pourquoi ne puis-je pas définir mes propres niveaux de risque pour chaque détection de risque ?

Les niveaux de risque dans Identity Protection sont basés sur la précision de la détection et développés par notre Machine Learning supervisé. Pour personnaliser l’expérience présentée aux utilisateurs, l’administrateur peut inclure/exclure certains utilisateurs/groupes des stratégies de risque de l’utilisateur et de risque de connexion.

### <a name="why-does-the-location-of-a-sign-in-not-match-where-the-user-truly-signed-in-from"></a>Pourquoi l’emplacement d’une connexion ne correspond pas à l’emplacement à partir duquel l’utilisateur s’est réellement connecté ?

Le mappage de géolocalisation IP est un défi à l’échelle du secteur. Si vous pensez que l’emplacement indiqué dans le rapport de connexions ne correspond pas à l’emplacement réel, contactez le support Microsoft. 

### <a name="how-can-i-close-specific-risk-detections-like-i-did-in-the-old-ui"></a>Comment puis-je fermer des détections de risque spécifiques comme je le faisais dans l’ancienne interface utilisateur ?

Vous pouvez envoyer des commentaires sur les détections des risques en confirmant que la connexion liée est compromise ou sécurisée. Les commentaires fournis sur la connexion sont transmis à toutes les détections effectuées sur cette connexion. Si vous souhaitez fermer les détections qui ne sont pas liées à une connexion, vous pouvez fournir ces retours au niveau de l’utilisateur. Pour plus d’informations, consultez l’article [ Indiquer des commentaires sur les risques dans Azure AD Identity Protection](howto-identity-protection-risk-feedback.md).

### <a name="how-far-can-i-go-back-in-time-to-understand-whats-going-on-with-my-user"></a>Jusqu’à quel point puis-je revenir en arrière pour comprendre ce qui se passe avec mon utilisateur ?

- La vue [Utilisateurs à risque](howto-identity-protection-investigate-risk.md#risky-users) montre les risques d’un utilisateur en fonction de l’ensemble des connexions passées. 
- La vue [Connexions risquées](howto-identity-protection-investigate-risk.md#risky-sign-ins) affiche les signes de risque au cours des 30 derniers jours. 
- La vue [Détections de risques](howto-identity-protection-investigate-risk.md#risk-detections) affiche les détections de risques effectuées au cours des 90 derniers jours.

### <a name="how-can-i-learn-more-about-a-specific-detection"></a>Comment puis-je en savoir plus sur une détection spécifique ?

Toutes les détections de risques sont documentées dans l’article [Qu’est-ce que le risque](concept-identity-protection-risks.md#risk-types-and-detection). Vous pouvez pointer sur le symbole (i) en regard de la détection sur le portail Azure pour en savoir plus sur une détection.

### <a name="how-do-the-feedback-mechanisms-in-identity-protection-work"></a>Comment les mécanismes de commentaires fonctionnent-ils dans Identity Protection ?

**Confirmer comme étant compromise** (sur une connexion) : informe Azure AD Identity Protection que la connexion n’a pas été effectuée par le propriétaire de l’identité et indique un compromis.

- Lors de la réception de ces commentaires, nous définissons le risque de l’utilisateur et de connexion à l’état **État compromis confirmé** et le niveau de risques sur **Élevé**.

- Nous fournissons également les informations à nos systèmes de Machine Learning dans le but d’améliorations futures de l’évaluation des risques.

    > [!NOTE]
    > Si l’utilisateur est déjà corrigé, ne cliquez pas sur **Confirmer comme étant compromise**, car ceci définit l’état du risque de connexion et de l’utilisateur sur **État compromis confirmé** et le niveau de risque sur **Élevé**.

**Confirmer comme étant sécurisée** (sur une connexion) : informe Azure AD Identity Protection que la connexion a été effectuée par le propriétaire de l’identité et n’indique pas de compromis.

- Lors de la réception de ces commentaires, nous définissons le risque de connexion (et non de l’utilisateur) à l’état **Sécurité confirmée** et le niveau de risques sur **-** .

- Nous fournissons également les informations à nos systèmes de Machine Learning dans le but d’améliorations futures de l’évaluation des risques.

    > [!NOTE]
    > Si vous pensez que l’utilisateur n’est pas compromis, utilisez **Ignorer le risque lié à l’utilisateur** au niveau de l’utilisateur plutôt que d’utiliser **Sécurité confirmée** au niveau de la connexion. **Ignorer le risque lié à l’utilisateur** au niveau de l’utilisateur ferme le risque de l’utilisateur, ainsi que toutes les connexions à risque et toutes les détections de risque antérieures.

### <a name="why-am-i-seeing-a-user-with-a-low-or-above-risk-score-even-if-no-risky-sign-ins-or-risk-detections-are-shown-in-identity-protection"></a>Pourquoi un utilisateur avec un faible indice de risque (ou supérieur) s’affiche-t-il même si aucune connexion à risque ni aucune détection de risque n’apparaît dans Identity Protection ?

Étant donné que le risque de l’utilisateur est cumulatif par nature et n’expire pas, un utilisateur peut avoir un risque utilisateur faible ou supérieur même si aucune connexion à risque ni détection de risque récente n’apparaît dans Identity Protection. Cette situation peut se produire si une activité malveillante sur un utilisateur a eu lieu en dehors de la plage de temps pour laquelle nous stockons les détails des connexions à risque et des détections de risque. Nous ne faisons pas expirer le risque de l’utilisateur car les acteurs indélicats sont connus pour rester dans l’environnement des clients plus de 140 jours après une compromission d’identité avant d’attaquer. Les clients peuvent consulter la chronologie du risque de l’utilisateur pour comprendre pourquoi un utilisateur est exposé à un risque en accédant à : `Azure Portal > Azure Active Directory > Risky users’ report > Click on an at-risk user > Details’ drawer > Risk history tab`

### <a name="why-does-a-sign-in-have-a-sign-in-risk-aggregate-score-of-high-when-the-detections-associated-with-it-are-of-low-or-medium-risk"></a>Pourquoi une connexion a-t-elle un indice de « risque de connexion (agrégat) » élevé lorsque les détections qui lui sont associées ont un risque faible ou moyen ?

L’indice de risque d’agrégat élevé peut être basé sur d’autres fonctionnalités de la connexion, ou sur le fait que plusieurs détections ont été déclenchées pour cette connexion. À l’inverse, une connexion peut avoir un risque de connexion (agrégat) moyen même si les détections associées à la connexion sont de risque élevé. 

### <a name="why-is-the-detection-which-is-linked-to-a-risky-sign-in-have-a-different-risk-level-than-the-sign-in-risk-level-real-time"></a>Pourquoi la détection qui est liée à une connexion risquée a-t-elle un niveau de risque différent du niveau de risque de connexion (en temps réel) ? 

Nous avons récemment apporté des améliorations au calcul du risque de connexion en temps réel. Les différences observées entre le niveau de détection des risques et le niveau de risque de connexion résultent de ces modifications. Notez que le risque de connexion en temps réel est la valeur utilisée lors de l’application de la stratégie. 
