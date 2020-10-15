---
title: Fichier Include
description: Fichier Include
services: notification-hubs
author: sethmanheim
ms.service: notification-hubs
ms.topic: include
ms.date: 11/07/2019
ms.author: sethm
ms.custom: include file
ms.openlocfilehash: 48907713082ebb1008ad963121671b36af7f2731
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "74228178"
---
Dans cette section, vous envoyez les dernières nouvelles sous forme de notifications modèles avec balises à partir de l’application console .NET.

1. Dans Visual Studio, créez une application de console Visual C# :
    1. Dans le menu, sélectionnez **Fichier** > **Nouveau** > **Projet**.
    1. Dans **Créer un projet**, sélectionnez **Application console (.NET Framework)** pour C# dans la liste de modèles, puis **Suivant**.
    1. Entrez un nom pour l’application.
    1. Pour **Solution**, choisissez **Ajouter à la solution**, puis sélectionnez **Créer** afin de créer le projet.

1. Sélectionnez **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**, puis dans la fenêtre de la console, exécutez la commande suivante :

   ```powershell
   Install-Package Microsoft.Azure.NotificationHubs
   ```

   Cette action ajoute une référence au kit SDK Azure Notification Hubs à l’aide du package [Microsoft.Azure.NotificationHubs].

1. Ouvrez le fichier *Program.cs* et ajoutez l’instruction `using` suivante :

   ```csharp
   using Microsoft.Azure.NotificationHubs;
   ```

1. Dans la classe `Program` , ajoutez la méthode suivante ou remplacez-la si elle existe déjà :

    ```csharp
    private static async void SendTemplateNotificationAsync()
    {
        // Define the notification hub.
        NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");

        // Apple requires the apns-push-type header for all requests
        var headers = new Dictionary<string, string> {{"apns-push-type", "alert"}};

        // Create an array of breaking news categories.
        var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};

        // Send the notification as a template notification. All template registrations that contain
        // "messageParam" and the proper tags will receive the notifications.
        // This includes APNS, GCM/FCM, WNS, and MPNS template registrations.

        Dictionary<string, string> templateParams = new Dictionary<string, string>();

        foreach (var category in categories)
        {
            templateParams["messageParam"] = "Breaking " + category + " News!";
            await hub.SendTemplateNotificationAsync(templateParams, category);
        }
    }
    ```

   Ce code envoie une notification de modèle pour chacune des six balises du tableau de chaînes. L’utilisation des balises permet d’envoyer les notifications uniquement aux appareils des catégories inscrites.

1. Dans le code précédent, remplacez les espaces réservés `<hub name>` et `<connection string with full access>` par le nom de votre hub de notification et par la chaîne de connexion pour *DefaultFullSharedAccessSignature* du tableau de bord de votre hub de notifications.

1. Ajoutez les lignes suivantes à la méthode `Main()` :

   ```csharp
    SendTemplateNotificationAsync();
    Console.ReadLine();
    ```

1. Générez l’application console.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST interface]: https://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[How to use Notification Hubs from Java or PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
