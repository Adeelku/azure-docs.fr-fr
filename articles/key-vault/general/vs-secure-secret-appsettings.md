---
title: Enregistrement sécurisé des paramètres d’application de secret d’une application web - Azure Key Vault | Microsoft Docs
description: Procédure d’enregistrement en toute sécurité des paramètres d’application de secret tels que les informations d’identification Azure ou les clés API tierces à l’aide du fournisseur de Key Vault ASP.NET Core, du secret utilisateur ou des générateurs de configuration .NET 4.7.1
services: visualstudio
author: cawaMS
manager: paulyuk
editor: ''
ms.service: key-vault
ms.subservice: general
ms.topic: how-to
ms.date: 07/17/2019
ms.author: cawa
ms.custom: devx-track-csharp
ms.openlocfilehash: 79fa01e53b53f3066e55736c105d6489ccbd96e7
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89019842"
---
# <a name="securely-save-secret-application-settings-for-a-web-application"></a>Enregistrement en toute sécurité des paramètres d’application de secret d’une application web

## <a name="overview"></a>Vue d’ensemble
Cet article décrit comment enregistrer en toute sécurité des paramètres de configuration d’application de secret pour des applications Azure.

Tous les paramètres de configuration d’application web sont généralement enregistrés dans des fichiers de configuration tels que Web.config. Cette pratique entraîne l’archivage des paramètres de secret tels que les informations d’identification de cloud dans des systèmes de contrôle de code source publics, par exemple GitHub. Il peut toutefois être difficile de suivre les meilleures pratiques de sécurité en raison de la surcharge requise pour modifier le code source et pour reconfigurer des paramètres de développement.

Pour garantir la sécurité des processus de développement, des bibliothèques d’outils et de frameworks sont créées pour enregistrer les paramètres de secret d’application de manière sécurisée avec peu, voire aucun, changement du code source.

## <a name="aspnet-and-net-core-applications"></a>Applications ASP.NET et .NET Core

### <a name="save-secret-settings-in-user-secret-store-that-is-outside-of-source-control-folder"></a>Enregistrer les paramètres de secret dans le magasin de secrets utilisateur qui se trouve en dehors du dossier de contrôle de code source
Si vous créez un prototype rapide ou que vous n’avez pas accès à Internet, commencez par déplacer vos paramètres de secret du dossier de contrôle de code source vers le magasin de secrets utilisateur. Le magasin de secrets utilisateur est un fichier enregistré sous le dossier du générateur de profils utilisateur ; les secrets ne sont donc pas archivés dans le contrôle de code source. Le diagramme suivant illustre le fonctionnement du [Secret utilisateur](https://docs.microsoft.com/aspnet/core/security/app-secrets?tabs=visual-studio).

![Le secret utilisateur stocke les paramètres de secret en dehors du contrôle de code source](../media/vs-secure-secret-appsettings/aspnetcore-usersecret.PNG)

Si vous exécutez une application de console .NET Core, utilisez Key Vault pour enregistrer votre secret en toute sécurité.

### <a name="save-secret-settings-in-azure-key-vault"></a>Enregistrer les paramètres de secret dans Azure Key Vault
Si vous développez un projet et si vous devez partager le code source en toute sécurité, utilisez [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

1. Créez un Key Vault dans votre abonnement Azure. Renseignez tous les champs obligatoires dans l’interface utilisateur et cliquez sur *Créer* au bas du panneau

    ![Créer un Azure Key Vault](../media/vs-secure-secret-appsettings/create-keyvault.PNG)

2. Accordez un accès au Key Vault à vous et aux membres de votre équipe. Si votre équipe est importante, vous pouvez créer un [groupe Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md) et ajouter cet accès de groupe de sécurité au Key Vault. Dans la liste déroulante *Autorisations du secret*, vérifiez *Get* et *Liste* sous *Opérations de gestion des secrets*.
Si vous avez déjà créé votre application web, accordez-lui l'accès au Key Vault afin qu’elle puisse y accéder sans avoir à stocker la configuration secrète dans les paramètres ou les fichiers de l’application. Recherchez votre application Web en utilisant son nom et ajoutez-la de la même façon que vous accordez l’accès aux utilisateurs.

    ![Ajouter une stratégie d’accès à Key Vault](../media/vs-secure-secret-appsettings/add-keyvault-access-policy.png)

3. Ajoutez votre secret à Key Vault sur le portail Azure. Pour les paramètres de configuration imbriqués, remplacez «  : » par  -- » pour que le nom de secret Key Vault soit valide. « : » ne peut pas être le nom d’un secret Key Vault.

    ![Ajouter un secret Key Vault](../media/vs-secure-secret-appsettings/add-keyvault-secret.png)

    > [!NOTE]
    > Avant Visual Studio 2017 V15.6, nous recommandions d’installer l’extension Azure Services Authentication pour Visual Studio. Cela est toutefois maintenant déprécié, car la fonctionnalité est intégrée à Visual Studio. Par conséquent, si vous utilisez une version antérieure de Visual Studio 2017, nous vous suggérons de mettre à jour vers, au minimum, Visual Studio 2017 15.6 ou version supérieure pour pouvoir utiliser cette fonctionnalité en mode natif et accéder au coffre de clés à partir de l’identité de connexion Visual Studio.
    >

4. Ajoutez les packages NuGet suivants à votre projet :

    ```
    Microsoft.Azure.KeyVault
    Microsoft.Azure.Services.AppAuthentication
    Microsoft.Extensions.Configuration.AzureKeyVault
    ```
5. Ajoutez le code suivant au fichier Program.cs :

    ```csharp
    public static IHostBuilder CreateHostBuilder(string[] args) =>
             Host.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((ctx, builder) =>
                {
                    var keyVaultEndpoint = GetKeyVaultEndpoint();
                    if (!string.IsNullOrEmpty(keyVaultEndpoint))
                    {
                        var azureServiceTokenProvider = new AzureServiceTokenProvider();
                        var keyVaultClient = new KeyVaultClient(
                            new KeyVaultClient.AuthenticationCallback(
                                azureServiceTokenProvider.KeyVaultTokenCallback));
                        builder.AddAzureKeyVault(
                        keyVaultEndpoint, keyVaultClient, new DefaultKeyVaultSecretManager());
                    }
                })
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });

        private static string GetKeyVaultEndpoint() => Environment.GetEnvironmentVariable("KEYVAULT_ENDPOINT");
    ```
6. Ajoutez votre URL de Key Vault au fichier launchsettings.json. Le nom de la variable d’environnement *KEYVAULT_ENDPOINT* est défini dans le code que vous avez ajouté à l’étape 6.

    ![Ajouter l’URL de Key Vault comme variable d’environnement de projet](../media/vs-secure-secret-appsettings/add-keyvault-url.png)

7. Démarrez le débogage du projet. Cette opération doit s’exécuter avec succès.

## <a name="aspnet-and-net-applications"></a>Applications ASP.NET et .NET

.NET 4.7.1 prend en charge Key Vault et les générateurs de configuration de secrets, garantissant ainsi de pouvoir déplacer les secrets du dossier de contrôle de code source sans modifier le code.
Pour continuer, [téléchargez .NET 4.7.1](https://www.microsoft.com/download/details.aspx?id=56115) et migrez votre application si elle utilise une version antérieure d’infrastructure .NET.

### <a name="save-secret-settings-in-a-secret-file-that-is-outside-of-source-control-folder"></a>Enregistrer les paramètres de secret dans un fichier de secret qui se trouve en dehors du dossier de contrôle de code source
Si vous écrivez un prototype rapide et que vous ne souhaitez pas approvisionner des ressources Azure, accédez à cette option.

1. Cliquez avec le bouton droit sur le projet et sélectionnez **Gérer les secrets d’utilisateur**. Cela permet d’installer un package NuGet **Microsoft.Configuration.ConfigurationBuilders.UserSecrets**, de créer un fichier pour enregistrer les paramètres de secret en dehors du fichier web.config et d’ajouter une section **ConfigBuilders** dans le fichier web.config.

2. Placez les paramètres de secret sous l’élément racine. voici un exemple

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <root>
      <secrets ver="1.0">
        <secret name="secret" value="foo"/>
        <secret name="secret1" value="foo_one" />
        <secret name="secret2" value="foo_two" />
      </secrets>
    </root>
    ```

3. Précisez que la section appSettings utilise le générateur de configuration de secrets. Vérifiez qu’il existe une entrée pour le paramètre de secret avec une valeur factice.

    ```xml
        <appSettings configBuilders="Secrets">
            <add key="webpages:Version" value="3.0.0.0" />
            <add key="webpages:Enabled" value="false" />
            <add key="ClientValidationEnabled" value="true" />
            <add key="UnobtrusiveJavaScriptEnabled" value="true" />
            <add key="secret" value="" />
        </appSettings>
    ```

5. Déboguez votre application. Cette opération doit s’exécuter avec succès.

### <a name="save-secret-settings-in-an-azure-key-vault"></a>Enregistrer les paramètres de secret dans un Azure Key Vault
Suivez les instructions de la section ASP.NET Core pour configurer un Key Vault pour votre projet.

1. Installer le package NuGet suivant dans votre projet
   ```
   Microsoft.Configuration.ConfigurationBuilders.Azure
   ```

2. Définissez le générateur de configuration de Key Vault dans le fichier Web.config. Placez cette section avant la section *appSettings*. Remplacez *vaultName* par le nom de Key Vault si votre Key Vault se trouve dans Azure global, ou par l’URI complet si vous utilisez un cloud Sovereign.

    ```xml
     <configBuilders>
        <builders>
            <add name="Secrets" userSecretsId="695823c3-6921-4458-b60b-2b82bbd39b8d" type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder, Microsoft.Configuration.ConfigurationBuilders.UserSecrets, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />
            <add name="AzureKeyVault" vaultName="[VaultName]" type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder, Microsoft.Configuration.ConfigurationBuilders.Azure, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />
        </builders>
      </configBuilders>
    ```
3. Précisez que la section appSettings utilise le générateur de configuration de Key Vault. Vérifiez qu’une entrée pour le paramètre de secret avec une valeur factice existe.

   ```xml
   <appSettings configBuilders="AzureKeyVault">
       <add key="webpages:Version" value="3.0.0.0" />
       <add key="webpages:Enabled" value="false" />
       <add key="ClientValidationEnabled" value="true" />
       <add key="UnobtrusiveJavaScriptEnabled" value="true" />
       <add key="secret" value="" />
   </appSettings>
   ```

4. Démarrez le débogage du projet. Cette opération doit s’exécuter avec succès.
