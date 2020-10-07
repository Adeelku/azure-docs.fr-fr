---
title: Envoyer des notifications Push vers iOS avec Azure Notification Hubs et le SDK iOS version 2.0.4
description: Dans ce tutoriel, vous allez découvrir comment utiliser Azure Notification Hubs et Apple Push Notification Service pour envoyer des notifications Push à des appareils iOS (version 2.0.4).
author: sethmanheim
ms.author: sethm
ms.date: 06/19/2020
ms.topic: tutorial
ms.service: notification-hubs
ms.reviewer: thsomasu
ms.lastreviewed: 06/01/2020
ms.openlocfilehash: ffa562a734e0e6f898aaff89622362080bf1a053
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91318192"
---
# <a name="tutorial-send-push-notifications-to-ios-apps-using-azure-notification-hubs-version-204"></a>Tutoriel : Envoyer des notifications Push vers des applications iOS avec Azure Notification Hubs (version 2.0.4)

Ce tutoriel montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application iOS à l’aide du SDK Azure Notification Hubs version 2.0.4.

Ce tutoriel couvre les étapes suivantes :

- Créer un exemple d’application iOS
- Connecter votre application iOS à Azure Notification Hubs
- Envoyer des notifications Push de test
- Vérifier la réception des notifications par votre application

Vous pouvez télécharger le code complet pour ce tutoriel à partir de [GitHub](https://github.com/Azure/azure-notificationhubs-ios/tree/v3-preview2/Samples).

## <a name="prerequisites"></a>Prérequis

Pour suivre ce tutoriel, vous devez disposer des prérequis suivants :

- Un Mac exécutant [Xcode](https://go.microsoft.com/fwLink/p/?LinkID=266532), ainsi qu’un certificat de développeur valide installé dans votre trousseau
- Un iPhone ou un iPad exécutant iOS version 10 ou ultérieure
- Votre appareil physique inscrit auprès du [portail Apple](https://developer.apple.com/) et associé à votre certificat

Avant de continuer, veillez à suivre le tutoriel précédent sur la prise en main d’[Azure Notification Hubs pour les applications iOS](ios-sdk-get-started.md) afin de configurer les informations d’identification Push dans votre hub de notification. Même si vous n’avez aucune expérience préalable avec le développement sur iOS, vous devriez être en mesure d’effectuer ces étapes.

> [!NOTE]
> En raison des conditions de configuration requises pour les notifications Push, vous devez déployer et tester les notifications Push sur un appareil iOS physique (iPhone ou iPad) au lieu de l’émulateur iOS.

## <a name="connect-your-ios-app-to-notification-hubs"></a>Connecter votre application iOS à Notification Hubs

1. Dans Xcode, créez un projet iOS et sélectionnez le modèle  **Single View Application**.

   :::image type="content" source="media/ios-sdk/image1.png" alt-text="Sélectionner un modèle":::

2. Au moment de définir les options de votre nouveau projet, veillez à utiliser le même **nom de produit** et le même **identificateur d’organisation** que ceux utilisés quand vous avez défini l’identifiant de bundle dans le portail des développeurs Apple.

3. Sous le navigateur de projet, sélectionnez le nom de votre projet sous **Targets**, puis sélectionnez l’onglet **Signing & Capabilities**. Veillez à sélectionner l’ **équipe** correspondant à votre compte de développeur Apple. XCode doit extraire automatiquement le profil d’approvisionnement que vous avez créé précédemment en fonction de l’identificateur d’offre groupée.

   Si vous ne voyez pas le nouveau profil d’approvisionnement que vous avez créé dans Xcode, essayez d’actualiser les profils pour votre identité de signature. Cliquez sur **Xcode** dans la barre de menus, sur  **Preferences**, sur l’onglet **Account**, sur le bouton **View Details**, sur votre identité de signature, puis cliquez sur le bouton d’actualisation dans le coin inférieur droit.

   :::image type="content" source="media/ios-sdk/image2.png" alt-text="Sélectionner un modèle":::

4. Sous l’onglet **Signing & Capabilities**, sélectionnez **+ Capability**. Double-cliquez sur **Push Notifications** pour l’activer.

   :::image type="content" source="media/ios-sdk/image3.png" alt-text="Sélectionner un modèle"
      ```

      - Ensuite, mettez à jour les dépendances de build :

      ```shell
      $ carthage update
      ```

      Pour plus d’informations sur l’utilisation de Carthage, consultez le [dépôt GitHub Carthage](https://github.com/Carthage/Carthage).

   - Intégration en copiant les binaires dans votre projet : Vous pouvez intégrer en copiant les binaires dans votre projet comme suit :

        - Téléchargez le framework  [SDK Azure Notification Hubs](https://github.com/Azure/azure-notificationhubs-android/releases) fourni dans un fichier zip et décompressez-le.

        - Dans Xcode, cliquez avec le bouton droit sur votre projet et sélectionnez l’option **Add Files to** pour ajouter le dossier **WindowsAzureMessaging.framework** à votre projet Xcode. Sélectionnez  **Options** et vérifiez que l’option **Copy items if needed** est cochée, puis cliquez sur  **Add**.

          :::image type="content" source="media/ios-sdk/image4.png" alt-text="Sélectionner un modèle":::

6. Ajoutez un nouveau fichier d’en-tête au projet nommé **Constants.h**. Pour ce faire, cliquez avec le bouton droit sur le nom du projet et sélectionnez **New File...** . Sélectionnez ensuite **Header File**. Ce fichier contient les constantes de votre hub de notification. Ensuite, sélectionnez  **Suivant**. Nommez le fichier **Constants.h**.

7. Ajoutez le code suivant au fichier Constants.h :

   ```objc
   #ifndef Constants_h
   #define Constants_h
   extern NSString* const NHInfoConnectionString;
   extern NSString* const NHInfoHubName;
   extern NSString* const NHUserDefaultTags;
   #endif /* Constants_h */
   ```

8. Ajoutez le fichier d’implémentation pour Constants.h. Pour ce faire, cliquez avec le bouton droit sur le nom du projet et sélectionnez **New File...** . Sélectionnez **Objective-C File**, puis  **Next**. Nommez le fichier **Constants.m**.

   :::image type="content" source="media/ios-sdk/image5.png" alt-text="Sélectionner un modèle"

   NSString* const NHInfoConnectionString = @"NotificationHubConnectionString";
   NSString* const NHInfoHubName = @"NotificationHubName";NSString* const NHUserDefaultTags = @"notification_tags";
   ```

10. Ouvrez le fichier **AppDelegate.h** de votre projet et remplacez son contenu par le code suivant :

    ```objc
    #import <UIKit/UIKit.h>
    #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
    #import <UserNotifications/UserNotifications.h> 

    @interface AppDelegate : UIResponder <UIApplicationDelegate,   UNUserNotificationCenterDelegate>

    @property (strong, nonatomic) UIWindow *window;

    - (void)handleRegister;
    - (void)handleUnregister;

    @end
    ```

11. Dans le fichier projet **AppDelegate.m**, ajoutez les instructions `import` suivantes :

    ```objc
    #import "Constants.h"
    #import "NotificationDetailViewController.h"
    ```

12. Toujours dans votre fichier **AppDelegate.m**, ajoutez la ligne de code suivante dans la méthode `didFinishLaunchingWithOptions` en fonction de votre version d’iOS. Ce code enregistre le handle de votre appareil avec APNs :

    ```objc
    [[UNUserNotificationCenter currentNotificationCenter] setDelegate:self];
    ```

13. Dans le même fichier **AppDelegate.m**, remplacez tout le code situé après `didFinishLaunchingWithOptions` par le code suivant :

    ```objc
    // Tells the app that a remote notification arrived that indicates there is data to be fetched.

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler {
    NSLog(@"Received remote (silent) notification");
    [self logNotificationDetails:userInfo];

    //
    // Let the system know the silent notification has been processed.
    //
    completionHandler(UIBackgroundFetchResultNoData);
    }

    // Tells the delegate that the app successfully registered with Apple Push Notification service (APNs).

    - (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    NSMutableSet *tags = [[NSMutableSet alloc] init];

    // Load and parse stored tags
    NSString *unparsedTags = [[NSUserDefaults standardUserDefaults] valueForKey:NHUserDefaultTags];
    if (unparsedTags.length > 0) {
        NSArray *tagsArray = [unparsedTags componentsSeparatedByString: @","];
        [tags addObjectsFromArray:tagsArray];
    }

    // Register the device with the Notification Hub.
    // If the device has not already been registered, this will create the registration.
    // If the device has already been registered, this will update the existing registration.
    //
    SBNotificationHub* hub = [self getNotificationHub];
    [hub registerNativeWithDeviceToken:deviceToken tags:tags completion:^(NSError* error) {
        if (error != nil) {
            NSLog(@"Error registering for notifications: %@", error);
        } else {
            [self showAlert:@"Registered" withTitle:@"Registration Status"];
        }
    }];
    }

    // UNUserNotificationCenterDelegate methods
    //
    // Asks the delegate how to handle a notification that arrived while the app was running in the  foreground.

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler {
    NSLog(@"Received notification while the application is in the foreground");

    // The system calls this delegate method when the app is in the foreground. This allows the app to handle the notification
    // itself (and potentially modify the default system behavior).

    // Handle the notification by displaying custom UI.
    //
    [self showNotification:notification.request.content.userInfo];

    // Use 'options' to specify which default behaviors to enable.
    // - UNAuthorizationOptionBadge: Apply the notification's badge value to the app’s icon.
    // - UNAuthorizationOptionSound: Play the sound associated with the notification.
    // - UNAuthorizationOptionAlert: Display the alert using the content provided by the notification.
    //
    // In this case, do not pass UNAuthorizationOptionAlert because the notification was handled by the app.
    //
    completionHandler(UNAuthorizationOptionBadge | UNAuthorizationOptionSound);
    }

    // Asks the delegate to process the user's response to a delivered notification.
    //

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler {
    NSLog(@"Received notification while the application is in the background");

    // The system calls this delegate method when the user taps or responds to the system notification.

    // Handle the notification response by displaying custom UI
    //
    [self showNotification:response.notification.request.content.userInfo];

    // Let the system know the response has been processed.
    //
    completionHandler();
    }

    // App logic and helpers

    - (SBNotificationHub *)getNotificationHub {
    NSString *hubName = [[NSBundle mainBundle] objectForInfoDictionaryKey:NHInfoHubName];
    NSString *connectionString = [[NSBundle mainBundle] objectForInfoDictionaryKey:NHInfoConnectionString];

    return [[SBNotificationHub alloc] initWithConnectionString:connectionString notificationHubPath:hubName];
    }

    - (void)handleRegister {
    UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];

    UNAuthorizationOptions options =  UNAuthorizationOptionAlert | UNAuthorizationOptionSound | UNAuthorizationOptionBadge;
    [center requestAuthorizationWithOptions:(options) completionHandler:^(BOOL granted, NSError * _Nullable error) {
        if (error != nil) {
            NSLog(@"Error requesting for authorization: %@", error);
        }
    }];
    [[UIApplication sharedApplication] registerForRemoteNotifications];
    }

    - (void)handleUnregister {
    //
    // Unregister the device with the Notification Hub.
    //
    SBNotificationHub *hub = [self getNotificationHub];
    [hub unregisterNativeWithCompletion:^(NSError* error) {
        if (error != nil) {
            NSLog(@"Error unregistering for push: %@", error);
        } else {
            [self showAlert:@"Unregistered" withTitle:@"Registration Status"];
        }
    }];
    }

    - (void)logNotificationDetails:(NSDictionary *)userInfo {
    if (userInfo != nil) {
        UIApplicationState state = [UIApplication sharedApplication].applicationState;
        BOOL background = state != UIApplicationStateActive;
        NSLog(@"Received %@notification: \n%@", background ? @"(background) " : @"", userInfo);
    }
    }

    - (void)showAlert:(NSString *)message withTitle:(NSString *)title {
    if (title == nil) {
        title = @"Alert";
    }
    UIAlertController *alert = [UIAlertController alertControllerWithTitle:title message:message preferredStyle:UIAlertControllerStyleAlert];
    [alert addAction:[UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault handler:nil]];
    [[[[UIApplication sharedApplication] keyWindow] rootViewController] presentViewController:alert animated:YES completion:nil];
    }

    - (void)showNotification:(NSDictionary *)userInfo {
    [self logNotificationDetails:userInfo];

    NotificationDetailViewController *notificationDetail = [[NotificationDetailViewController alloc] initWithUserInfo:userInfo];
    [[[[UIApplication sharedApplication] keyWindow] rootViewController] presentViewController:notificationDetail animated:YES completion:nil];
    }

    @end
    ```

    Ce code se connecte au hub de notification en utilisant les informations de connexion que vous avez spécifiées dans **Constants.h**. Il transmet ensuite le jeton de l’appareil au hub de notification de sorte que ce dernier puisse envoyer des notifications.

### <a name="create-notificationdetailviewcontroller-header-file"></a>Créer le fichier d’en-tête NotificationDetailViewController

1. En suivant les mêmes instructions que ci-dessus, ajoutez un autre fichier d’en-tête nommé **NotificationDetailViewController.h**. Remplacez le contenu du nouveau fichier d’en-tête par le code suivant :

   ```objc
   #import <UIKit/UIKit.h>

   NS_ASSUME_NONNULL_BEGIN

   @interface NotificationDetailViewController : UIViewController

   @property (strong, nonatomic) IBOutlet UILabel *titleLabel;
   @property (strong, nonatomic) IBOutlet UILabel *bodyLabel;
   @property (strong, nonatomic) IBOutlet UIButton *dismissButton;

   @property (strong, nonatomic) NSDictionary *userInfo;

   - (id)initWithUserInfo:(NSDictionary *)userInfo;

   @end

   NS_ASSUME_NONNULL_END
   ```

2. Ajoutez le fichier d’implémentation **NotificationDetailViewController.m**. Remplacez le contenu du fichier par le code suivant, qui implémente les méthodes UIViewController :

   ```objc
   #import "NotificationDetailViewController.h"

   @interface NotificationDetailViewController ()

   @end

   @implementation NotificationDetailViewController

   - (id)initWithUserInfo:(NSDictionary *)userInfo {
    self = [super initWithNibName:@"NotificationDetail" bundle:nil];
    if (self) {
        _userInfo = userInfo;
    }
    return self;
   }

   - (void)viewDidLayoutSubviews {
    [self.titleLabel sizeToFit];
    [self.bodyLabel sizeToFit];
   }

   - (void)viewDidLoad {
    [super viewDidLoad];

    NSString *title = nil;
    NSString *body = nil;

    NSDictionary *aps = [_userInfo valueForKey:@"aps"];
    NSObject *alertObject = [aps valueForKey:@"alert"];
    if (alertObject != nil) {
        if ([alertObject isKindOfClass:[NSDictionary class]]) {
            NSDictionary *alertDict = (NSDictionary *)alertObject;
            title = [alertDict valueForKey:@"title"];
            body = [alertObject valueForKey:@"body"];
        } else if ([alertObject isKindOfClass:[NSString class]]) {
            body = (NSString *)alertObject;
        } else {
            NSLog(@"Unable to parse notification content. Unexpected format: %@", alertObject);
        }
    }

    if (title == nil) {
        title = @"<unset>";
    }

    if (body == nil) {
        body = @"<unset>";
    }

    self.titleLabel.text = title;
    self.bodyLabel.text = body;
   }

   - (IBAction)handleDismiss:(id)sender {
    [self dismissViewControllerAnimated:YES completion:nil];
   }

   @end
   ```

### <a name="viewcontroller"></a>ViewController

1. Dans le fichier projet **ViewController.h**, ajoutez les instructions `import` suivantes :

   ```objc
   #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
   #import <UserNotifications/UserNotifications.h>
   ```

2. Toujours dans **ViewController.h**, ajoutez les déclarations de propriétés suivantes après la déclaration `@interface`  :

   ```objc
   @property (strong, nonatomic) IBOutlet UITextField *tagsTextField;
   @property (strong, nonatomic) IBOutlet UIButton *registerButton;
   @property (strong, nonatomic) IBOutlet UIButton *unregisterButton;
   ```

3. Dans le fichier d’implémentation **ViewController.m** du projet, remplacez le contenu du fichier par le code suivant :

   ```objc
   #import "ViewController.h"
   #import "Constants.h"
   #import "AppDelegate.h"

   @interface ViewController ()

   @end

   @implementation ViewController

   // UIViewController methods

   - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    // Simple method to dismiss keyboard when user taps outside of the UITextField.
    [self.view endEditing:YES];
   }

   - (void)viewDidLoad {
    [super viewDidLoad];

    // Load raw tags text from storage and initialize the text field
    self.tagsTextField.text = [[NSUserDefaults standardUserDefaults] valueForKey:NHUserDefaultTags];
   }

   - (IBAction)handleRegister:(id)sender {
    // Save raw tags text in storage
    [[NSUserDefaults standardUserDefaults] setValue:self.tagsTextField.text forKey:NHUserDefaultTags];

   // Delegate processing the register action to the app delegate.
   [[[UIApplication sharedApplication] delegate] performSelector:@selector(handleRegister)];
   }

   - (IBAction)handleUnregister:(id)sender {
    [[[UIApplication sharedApplication] delegate] performSelector:@selector(handleUnregister)];
   }

   @end
   ```

4. Pour vérifier l’absence d’échecs, générez et exécutez l’application sur votre appareil.

## <a name="send-test-push-notifications"></a>Envoi de notifications Push de test

Vous pouvez tester la réception de notifications dans votre application avec l’option **Envoi de test** dans le [portail Azure](https://portal.azure.com/). Cette option envoie une notification Push de test à votre appareil.

:::image type="content" source="media/ios-sdk/image6.png" alt-text="Sélectionner un modèle":::

Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Apps ou ASP.NET à l’aide d’une bibliothèque compatible. Si aucune bibliothèque n’est disponible pour votre backend, vous pouvez également utiliser l’API REST directement pour envoyer des messages de notification.

La liste ci-dessous répertorie certains autres didacticiels, que vous pouvez consulter pour envoyer des notifications :

- Azure Mobile Apps : pour obtenir un exemple d’envoi de notifications à partir d’un back-end Mobile Apps intégré à Notification Hubs, consultez [Ajout de notifications Push à votre application iOS](/previous-versions/azure/app-service-mobile/app-service-mobile-ios-get-started-push).
- ASP.NET :  [Utiliser Notification Hubs pour envoyer des notifications Push à des utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md).
- SDK Java Azure Notification Hubs : consultez [Guide pratique pour utiliser Notification Hubs à partir de Java](notification-hubs-java-push-notification-tutorial.md) pour envoyer des notifications à partir de Java. Il a été testé dans Eclipse pour le développement Android.
- PHP :  [Guide pratique pour utiliser Notification Hubs à partir de PHP](notification-hubs-php-push-notification-tutorial.md).

## <a name="verify-that-your-app-receives-push-notifications"></a>Vérification de la réception des notifications Push par votre application

Pour tester les notifications Push sur iOS, vous devez déployer l’application sur un appareil iOS physique. Vous ne pouvez pas envoyer de notifications Push Apple en utilisant le simulateur iOS.

1. Exécutez l’application, vérifiez que l’inscription est effectuée, puis appuyez sur **OK**.

   :::image type="content" source="media/ios-sdk/image7.png" alt-text="Sélectionner un modèle":::

2. Ensuite, envoyez une notification Push de test à partir du [portail Azure](https://portal.azure.com/), comme indiqué dans la section précédente.

3. La notification Push est envoyée à tous les appareils qui sont inscrits pour recevoir les notifications à partir du hub de notification donné.

   :::image type="content" source="media/ios-sdk/image8.png" alt-text="Sélectionner un modèle":::

## <a name="next-steps"></a>Étapes suivantes

Dans cet exemple simple, vous avez envoyé des notifications Push à tous vos appareils iOS inscrits. Pour découvrir comment envoyer des notifications à des appareils iOS spécifiques, passez au tutoriel suivant :

[Tutoriel : Notifications Push vers des appareils spécifiques](notification-hubs-ios-xplat-segmented-apns-push-notification.md)

Pour plus d’informations, consultez les articles suivants :

- [Vue d’ensemble d’Azure Notification Hubs](notification-hubs-push-notification-overview.md)
- [API REST de Notification Hubs](/rest/api/notificationhubs/)
- [Kit de développement logiciel (SDK) Notification Hubs pour opérations backend](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)
- [Kit de développement logiciel (SDK) Notification Hubs sur GitHub](https://github.com/Azure/azure-notificationhubs)
- [S’inscrire auprès du principal d’application](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
- [Gestion des inscriptions](notification-hubs-push-notification-registration-management.md)
- [Utilisation de balises](notification-hubs-tags-segment-push-message.md)
- [Utilisation des modèles personnalisés](notification-hubs-templates-cross-platform-push-messages.md)
- [Contrôle d’accès Service Bus avec des signatures d’accès partagé](../service-bus-messaging/service-bus-sas.md)
- [Générer des jetons SAS par programme](/rest/api/eventhub/generate-sas-token)
- [Sécurité Apple : CommonCrypto](https://developer.apple.com/security/)
- [Heure d’époque Unix](https://en.wikipedia.org/wiki/Unix_time)
- [HMAC](https://en.wikipedia.org/wiki/HMAC)