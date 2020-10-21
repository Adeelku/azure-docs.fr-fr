---
title: Résoudre les problèmes des stratégies personnalisées avec Application Insights
titleSuffix: Azure AD B2C
description: configuration d’Application Insights pour suivre l’exécution de vos stratégies personnalisées.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: troubleshooting
ms.date: 10/12/2020
ms.custom: project-no-code
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: ddc0dc433a5d8c09c692e6304647fb391694e8c8
ms.sourcegitcommit: 83610f637914f09d2a87b98ae7a6ae92122a02f1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91993165"
---
# <a name="collect-azure-active-directory-b2c-logs-with-application-insights"></a>Collecter les journaux Azure Active Directory B2C avec Application Insights

Cet article explique comment collecter les journaux d’activité à partir d’Azure Active Directory B2C (Azure AD B2C) afin que vous puissiez diagnostiquer les problèmes liés à vos stratégies personnalisées. Application Insights permet de diagnostiquer les exceptions et de visualiser les problèmes de performances des applications. Azure AD B2C comprend une fonctionnalité d’envoi de données à Application Insights.

Les journaux d’activité détaillés décrits ici doivent être activés **UNIQUEMENT** lors du développement de vos stratégies personnalisées.

> [!WARNING]
> N’activez pas le mode de développement en production. Les journaux d’activité recueillent toutes les revendications envoyées par et aux fournisseurs d’identité. En tant que développeur, vous assumez la responsabilité des données personnelles collectées dans vos journaux Application Insights. Ces journaux détaillés sont collectés uniquement lorsque la stratégie est placée en **MODE DÉVELOPPEUR**.

## <a name="set-up-application-insights"></a>Configurer Application Insights

Si vous n’en avez pas encore, créez une instance Application Insights dans votre abonnement.

1. Connectez-vous au [portail Azure](https://portal.azure.com).
1. Sélectionnez le filtre **Annuaire et abonnement** dans le menu supérieur, puis l’annuaire qui contient votre abonnement Azure (et non votre annuaire Azure AD B2C).
1. Sélectionnez **Créer une ressource** dans le menu de navigation de gauche.
1. Recherchez et sélectionnez **Application Insights**, puis sélectionnez **Créer**.
1. Remplissez le formulaire, sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.
1. Une fois le déploiement terminé, sélectionnez **Accéder à la ressource**.
1. Sous **Configurer** dans le menu Application Insights, sélectionnez **Propriétés**.
1. Enregistrez la **CLÉ D'INSTRUMENTATION**, que vous utiliserez dans une étape ultérieure.

## <a name="configure-the-custom-policy"></a>Configurer la stratégie personnalisée

1. Ouvrez le fichier de partie de confiance (RP), par exemple, *SignUpOrSignin.xml*.
1. Ajoutez les attributs suivants à l’élément `<TrustFrameworkPolicy>` :

   ```xml
   DeploymentMode="Development"
   UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
   ```

1. S’il n’existe pas déjà, ajoutez un nœud enfant `<UserJourneyBehaviors>` au nœud `<RelyingParty>`. Il doit être placé immédiatement après `<DefaultUserJourney ReferenceId="UserJourney Id" from your extensions policy, or equivalent (for example:SignUpOrSigninWithAAD" />`.
1. Ajoutez le nœud suivant en tant qu’enfant de l’élément `<UserJourneyBehaviors>`. Veillez à remplacer `{Your Application Insights Key}` par la **clé d’instrumentation** Application Insights que vous avez enregistrée précédemment.

    ```xml
    <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
    ```

    * `DeveloperMode="true"` dit à Application Insights d’envoyer la télémétrie par le biais du pipeline de traitement. Adapté au développement, mais restreint à des volumes élevés.
    * `ClientEnabled="true"` envoie le script côté client ApplicationInsights pour l’affichage de la page de suivi et les erreurs côté client. Vous pouvez les afficher dans la table **browserTimings** dans le portail Application Insights. En configurant `ClientEnabled= "true"`, vous ajoutez Application Insights à votre script de page et vous obtenez le minutage des chargements de page et des appels AJAX, le nombre d’exceptions du navigateur et d’échecs d’AJAX et leurs détails, ainsi que les nombres d’utilisateurs et de sessions. Ce champ est **facultatif** et est défini sur `false` par défaut.
    * `ServerEnabled="true"` envoie le JSON UserJourneyRecorder existant en tant qu’événement personnalisé à Application Insights.

    Par exemple :

    ```xml
    <TrustFrameworkPolicy
      ...
      TenantId="fabrikamb2c.onmicrosoft.com"
      PolicyId="SignUpOrSignInWithAAD"
      DeploymentMode="Development"
      UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
    >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="UserJourney ID from your extensions policy, or equivalent (for example: SignUpOrSigninWithAzureAD)" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
    </TrustFrameworkPolicy>
    ```

1. Téléchargez la stratégie.

## <a name="see-the-logs-in-application-insights"></a>Afficher des journaux d’activité dans Application Insights

Il y a un court délai, généralement moins de cinq minutes, avant que les nouveaux journaux d’activité s’affichent dans Application Insights.

1. Ouvrez la ressource Application Insights que vous avez créée sur le [portail Azure](https://portal.azure.com).
1. Dans la page **Vue d’ensemble**, sélectionnez **Journaux d’activité**.
1. Ouvrez un nouvel onglet dans Application Insights.

Voici une liste de requêtes que vous pouvez utiliser pour afficher les journaux d’activité :

| Requête | Description |
|---------------------|--------------------|
`traces` | Consultez tous les journaux d’activité générés par Azure AD B2C |
`traces | where timestamp > ago(1d)` | Consultez tous les journaux d’activité générés par Azure AD B2C pour le dernier jour

Les entrées peuvent être longues. Exporter au format CSV pour une étude plus approfondie.

Pour plus d’informations sur les requêtes, consultez [Vue d’ensemble des requêtes de journal dans Azure Monitor](../azure-monitor/log-query/log-query-overview.md).

## <a name="next-steps"></a>Étapes suivantes

La communauté a développé une visionneuse du parcours utilisateur pour aider les développeurs d’identité. Elle lit les données de votre instance d’Application Insights et présente les événements du parcours utilisateur d’une façon bien structurée. Vous obtenez le code source et le déployez dans votre propre solution.

Le lecteur de parcours utilisateur n’est pas pris en charge par Microsoft et est mis à disposition tel quel.

Vous trouverez la version de la visionneuse qui lit les événements Application Insights sur GitHub ici :

[Azure-Samples/active-directory-b2c-advanced-policies](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/wingtipgamesb2c/src/WingTipUserJourneyPlayerWebApplication)
