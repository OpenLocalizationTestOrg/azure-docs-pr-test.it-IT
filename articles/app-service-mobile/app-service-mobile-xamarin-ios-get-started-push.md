---
title: aaaAdd push notifiche tooyour xamarin app con il servizio App di Azure
description: Informazioni su app xamarin tooyour di notifiche push toouse toosend di servizio App di Azure
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Aggiungere le notifiche di push tooyour Xamarin.iOS App
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, si aggiunge toohello le notifiche push [xamarin introduttiva](app-service-mobile-xamarin-ios-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push. Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.

## <a name="prerequisites"></a>Prerequisiti
* Hello completo [delle Guide rapide xamarin](app-service-mobile-xamarin-ios-get-started.md) esercitazione.
* Un dispositivo iOS fisico. Notifiche push non sono supportate dal simulatore iOS hello.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrare l'applicazione hello per le notifiche push nel portale per sviluppatori di Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Configurare le notifiche push toosend di App per dispositivi mobili
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Aggiornare le notifiche push di hello server progetto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Configurare il progetto Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Aggiungere app tooyour di notifiche push
1. In **QSTodoService**, aggiungere hello seguente proprietà in modo che **AppDelegate** può acquisire client mobili hello:
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Aggiungere il seguente hello `using` hello cima toohello istruzione **appdelegate. cs** file.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. In **AppDelegate**, eseguire l'override di hello **FinishedLaunching** evento:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. In hello stesso file, eseguire l'override di hello **RegisteredForRemoteNotifications** evento. In questo codice si sta registrando per una notifica modello semplice che verrà inviata dal server hello in tutte le piattaforme supportate.
   
    Per ulteriori informazioni sui modelli con Hub di notifica, vedere [Modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. Quindi, eseguire l'override hello **DidReceivedRemoteNotification** evento:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

L'app è notifiche push toosupport aggiornato.

## <a name="test"></a>Testare le notifiche push nell'app
1. Hello premere **eseguire** progetto hello toobuild e avviare l'applicazione hello in un dispositivo in grado di iOS, quindi scegliere **OK** tooaccept le notifiche push.
   
   > [!NOTE]
   > È necessario accettare le notifiche push in modo esplicito dall'app. Questa richiesta si verifica solo hello prima volta che l'esecuzione applicazione hello.
   > 
   > 
2. Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.
3. Verificare che viene ricevuta una notifica, quindi fare clic su **OK** toodismiss hello notifica.
4. Ripetere il passaggio 2 e chiusura immediatamente hello app, quindi verificare che sia visualizzata una notifica.

L'esercitazione è stata completata.

<!-- Images. -->

<!-- URLs. -->



