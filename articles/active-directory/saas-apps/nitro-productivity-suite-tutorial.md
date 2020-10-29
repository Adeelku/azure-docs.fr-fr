---
title: 'Tutoriel : Intégration de l’authentification unique Azure Active Directory à Nitro Productivity Suite | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Nitro Productivity Suite.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 04/02/2020
ms.author: jeedes
ms.openlocfilehash: 4a4df1ff0561e180ca0a3fd36363ceff7da042df
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92522425"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-nitro-productivity-suite"></a>Tutoriel : Intégration de l’authentification unique Azure Active Directory à Nitro Productivity Suite

Dans ce tutoriel, vous allez découvrir comment intégrer Nitro Productivity Suite à Azure Active Directory (Azure AD). Quand vous intégrez Nitro Productivity Suite à Azure AD, vous pouvez :

* Contrôler dans Azure AD qui a accès à Nitro Productivity Suite.
* Permettre à vos utilisateurs de se connecter automatiquement à Nitro Productivity Suite avec leur compte Azure AD.
* gérer vos comptes à un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour commencer, vous avez besoin des éléments suivants :

* Un abonnement Azure AD Si vous ne disposez d’aucun abonnement, vous pouvez obtenir [un compte gratuit](https://azure.microsoft.com/free/).
* Un [abonnement Enterprise](https://www.gonitro.com/pricing) à Nitro Productivity Suite.

## <a name="scenario-description"></a>Description du scénario

Dans ce tutoriel, vous allez configurer et tester l’authentification unique Azure AD dans un environnement de test.

* Nitro Productivity Suite prend en charge l’authentification unique initiée par le **fournisseur de services** et le **fournisseur d’identité** .
* Nitro Productivity Suite prend en charge le provisionnement des utilisateurs **juste-à-temps** .
* Après avoir configuré Nitro Productivity Suite, vous pouvez appliquer le contrôle de session qui protège contre l’exfiltration et l’infiltration des données sensibles de votre organisation en temps réel. Le contrôle de session est étendu à partir de l’accès conditionnel. Pour plus d’informations, consultez [Découvrir comment appliquer un contrôle de session avec Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).

## <a name="add-nitro-productivity-suite-from-the-gallery"></a>Ajouter Nitro Productivity Suite à partir de la galerie

Pour configurer l’intégration de Nitro Productivity Suite dans Azure AD, vous devez ajouter Nitro Productivity Suite, disponible dans la galerie, à votre liste d’applications SaaS managées.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte professionnel ou scolaire, ou avec un compte personnel Microsoft.
1. Sélectionnez **Azure Active Directory** dans le volet de gauche.
1. Accédez à **Applications d’entreprise** , puis sélectionnez **Toutes les applications** .
1. Pour ajouter une nouvelle application, sélectionnez **Nouvelle application** .
1. Dans la section **Ajouter à partir de la galerie** , tapez **Nitro Productivity Suite** dans la zone de recherche.
1. Sélectionnez **Nitro Productivity Suite** dans les résultats, puis ajoutez l’application. Patientez quelques secondes pendant que l’application est ajoutée à votre locataire.


## <a name="configure-and-test-azure-ad-single-sign-on-for-nitro-productivity-suite"></a>Configurer et tester l’authentification unique Azure AD pour Nitro Productivity Suite

Configurez et testez l’authentification unique Azure AD avec Nitro Productivity Suite à l’aide d’un utilisateur de test appelé **B.Simon** . Pour que l’authentification unique fonctionne, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur Nitro Productivity Suite associé.

Pour configurer et tester l’authentification unique Azure AD avec Nitro Productivity Suite, suivez les indications des sections ci-après :

1. [Configurer l’authentification unique Azure AD](#configure-azure-ad-sso) pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
    1. [Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user) pour tester l’authentification unique Azure AD avec B.Simon.
    1. [Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user) pour permettre à B.Simon d’utiliser l’authentification unique Azure AD.
1. [Configurer l’authentification unique Nitro Productivity Suite](#configure-nitro-productivity-suite-sso) pour configurer les paramètres de l’authentification unique côté application
    1. [Créer un utilisateur de test Nitro Productivity Suite](#create-a-nitro-productivity-suite-test-user) pour avoir un équivalent de B.Simon dans Nitro Productivity Suite lié à la représentation Azure AD de l’utilisateur
1. [Tester l’authentification unique](#test-sso) pour vérifier si la configuration fonctionne.

## <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Effectuez les étapes suivantes pour activer l’authentification unique Azure AD dans le Portail Azure.

1. Dans le [portail Azure](https://portal.azure.com/), accédez à la page d’intégration de l’application **Nitro Productivity Suite** , puis recherchez la section **Gérer** . Sélectionnez **Authentification unique** .
1. Dans la page **Sélectionner une méthode d’authentification unique** , sélectionnez **SAML** .
1. Dans la section **Certificat de signature SAML** , recherchez **Certificat (en base64)** . Sélectionnez **Télécharger** pour télécharger le certificat et l’enregistrer sur votre ordinateur.

    ![Capture d’écran de la section Certificat de signature SAML, avec mise en évidence du lien Télécharger](common/certificatebase64.png)
    
1. Dans la section **Configurer Nitro Productivity Suite** , sélectionnez l’icône de copie en regard du champ **URL de connexion** .
    
    ![Capture d’écran de la section Configurer Nitro Productivity Suite avec les URL et les icônes de copie mises en évidence](common/copy-configuration-urls.png)
    
1. Sur le [portail Nitro Admin](https://admin.gonitro.com/), dans la page **Enterprise Settings** , recherchez la section **Single Sign-On** . Sélectionnez **Setup SAML SSO** .

    a. Collez l’ **URL de connexion** de l’étape précédente dans le champ **Sign In URL** .
    
    b. Chargez le **certificat (en base64)** de l’étape précédente dans le champ **X509 Signing Certificate** .
    
    c. Sélectionnez **Envoyer** .
    
    d. Sélectionnez **Activer l'authentification unique** .


1. Revenez au [portail Azure](https://portal.azure.com/). Dans la page **Configurer l’authentification unique avec SAML** , sélectionnez l’icône de crayon pour **Configuration SAML de base** afin de modifier les paramètres.

   ![Capture d’écran de la page Configurer l’authentification unique avec SAML avec l’icône de crayon mise en évidence](common/edit-urls.png)

1. Dans la section **Configuration SAML de base** , si vous voulez configurer l’application en mode lancé par le **fournisseur d’identité** , entrez les valeurs pour les champs suivants :

    a. Dans la zone de texte **Identificateur** , copiez et collez la valeur du champ **SAML Entity ID** (ID d’entité SAML) à partir du [portail Nitro Admin](https://admin.gonitro.com/). Son modèle doit être le suivant : `urn:auth0:gonitro-prod:<ENVIRONMENT>`

    b. Dans la zone de texte **URL de réponse** , copiez et collez la valeur du champ **ASC URL** (URL ASC) à partir du [portail Nitro Admin](https://admin.gonitro.com/). Son modèle doit être le suivant : `https://gonitro-prod.eu.auth0.com/login/callback?connection=<ENVIRONMENT>`

1. Sélectionnez **Définir des URL supplémentaires** , puis effectuez l’étape suivante si vous voulez configurer l’application en mode initié par le **fournisseur de services**  :

    Dans la zone de texte **URL de connexion** , tapez l’URL : `https://sso.gonitro.com/login`

1. Sélectionnez **Enregistrer** .

1. L’application Nitro Productivity Suite attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration d’attributs de jeton SAML. La capture d’écran suivante montre la liste des attributs par défaut.

    ![Capture d’écran des attributs par défaut](common/default-attributes.png)

1. L’application Nitro Productivity Suite s’attend à ce que certains attributs (en plus des attributs précédents) soient repassés dans la réponse SAML. Ces attributs sont préremplis, mais vous pouvez les rectifier en fonction de vos besoins.
    
    | Nom  |  Attribut source|
    | ---------------| --------------- |
    | employeeNumber |  user.objectid |


### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

Dans cette section, vous allez créer un utilisateur de test appelé B. Simon sur le portail Azure.

1. Dans le volet gauche du portail Azure, sélectionnez **Azure Active Directory** > **Utilisateurs** > **Tous les utilisateurs** .
1. Sélectionnez **Nouvel utilisateur** dans la partie supérieure de l’écran.
1. Dans les propriétés **Utilisateur** , effectuez les étapes suivantes :
   1. Dans le champ **Nom** , entrez `B.Simon`.  
   1. Dans le champ **Nom de l’utilisateur** , entrez username@companydomain.extension. Par exemple : `B.Simon@contoso.com`.
   1. Cochez la case **Afficher le mot de passe** et notez le mot de passe.
   1. Sélectionnez **Create** (Créer).

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous autorisez B.Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Nitro Productivity Suite.

1. Dans le portail Azure, sélectionnez **Applications d’entreprise** > **Toutes les applications** .
1. Dans la liste des applications, sélectionnez **Nitro Productivity Suite** .
1. Dans la page de vue d’ensemble de l’application, recherchez la section **Gérer** et sélectionnez **Utilisateurs et groupes** .

   ![Capture d’écran de la section Gérer, avec Utilisateurs et groupes mis en évidence](common/users-groups-blade.png)

1. Sélectionnez **Ajouter un utilisateur** . Ensuite, dans la boîte de dialogue **Ajouter une attribution** , sélectionnez **Utilisateurs et groupes** .

    ![Capture d’écran de la page Utilisateurs et groupes, avec Ajouter un utilisateur mis en évidence](common/add-assign-user.png)

1. Dans la boîte de dialogue **Utilisateurs et groupes** , sélectionnez **B.Simon** dans la liste des utilisateurs. Choisissez **Sélectionner** au bas de l’écran.
1. Si vous attendez une valeur de rôle dans l’assertion SAML, dans la boîte de dialogue **Sélectionner un rôle** , sélectionnez le rôle approprié pour l’utilisateur dans la liste. Choisissez **Sélectionner** au bas de l’écran.
1. Dans la boîte de dialogue **Ajouter une attribution** , sélectionnez **Affecter** .

## <a name="configure-nitro-productivity-suite-sso"></a>Configurer l’authentification unique Nitro Productivity Suite

Pour configurer l’authentification unique côté Nitro Productivity Suite, envoyez le **certificat (en base64)** téléchargé et les URL appropriées, copiées à partir du portail Azure, à l’ [équipe du support technique Nitro Productivity Suite](https://www.gonitro.com/support). Celle-ci vérifiera que l’authentification unique SAML est configurée correctement des deux côtés.

### <a name="create-a-nitro-productivity-suite-test-user"></a>Créer un utilisateur de test Nitro Productivity Suite

Nitro Productivity Suite prend en charge le provisionnement d’utilisateurs juste-à-temps, qui est activé par défaut. Vous n’avez aucune opération supplémentaire à effectuer. S’il n’existe pas encore d’utilisateur dans Nitro Productivity Suite, il en est créé un après l’authentification.

## <a name="test-sso"></a>Tester l’authentification unique (SSO) 

Dans cette section, vous allez tester votre configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous sélectionnez la vignette Nitro Productivity Suite dans le volet d’accès, vous êtes connecté automatiquement à l’application Nitro Productivity Suite pour laquelle vous avez configuré l’authentification unique. Pour plus d’informations, consultez [Se connecter et démarrer des applications à partir du portail Mes applications](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Ressources supplémentaires

- [Tutoriels pour l’intégration d’applications SaaS avec Azure Active Directory](./tutorial-list.md)

- [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

- [Qu’est-ce que l’accès conditionnel dans Azure Active Directory ?](../conditional-access/overview.md)

- [Essayer Nitro Productivity Suite avec Azure AD](https://aad.portal.azure.com/)

- [Qu’est-ce que le contrôle de session dans Microsoft Cloud App Security ?](/cloud-app-security/proxy-intro-aad)

- [Protéger Nitro Productivity Suite avec une visibilité et des contrôles avancés](/cloud-app-security/proxy-intro-aad)