---
title: aaaGet avviato con Azure Mobile Engagement per xamarin
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app xamarin. IOS.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Introduzione ad Azure Mobile Engagement per app Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche in un'applicazione di xamarin. IOS.
In questa esercitazione si creerà un'app Xamarin.iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Questa esercitazione richiede il seguente hello:

* [Xamarin Studio](http://xamarin.com/studio). È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio. Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx). 
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato un "integrazione di base" hello minimo imposta dati toocollect necessarie e invia una notifica push.

Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Xamarin:

### <a name="create-a-new-xamarinios-project"></a>Creare un nuovo progetto Xamarin.iOS
1. Avviare Xamarin Studio. Andare troppo**File** -> **New** -> **soluzione** 
   
    ![][1]
2. Selezionare **singola vista App**, assicurarsi che sia il linguaggio selezionato hello **c#** e quindi fare clic su **Avanti**.
   
    ![][2]
3. Compilare hello **nome App** hello e **identificatore organizzazione** e quindi fare clic su **Avanti**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Verificare che tale hello è alla fine di utilizzare toodeploy che App iOS con un ID di App che corrisponde esattamente hello identificatore Bundle è qui profilo di pubblicazione. 
   > 
   > 
4. Hello aggiornamento **nome progetto**, **Nome soluzione** e **percorso** se necessario, fare clic su **crea**.
   
    ![][4]

Xamarin Studio creerà app demo hello in cui integrare Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Fare clic con il pulsante destro hello **pacchetti** cartella windows soluzione hello e selezionare **Aggiungi pacchetti...**
   
    ![][5]
2. Ricerca di hello **Xamarin SDK di Microsoft Azure Mobile Engagement** e aggiungerlo tooyour soluzione.  
   
    ![][6]
3. Aprire **appdelegate. cs** e aggiungere hello seguente istruzione using:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. In hello **FinishedLaunching** metodo, aggiungere hello seguente connessione di hello tooinitialize con back-end Mobile Engagement. Verificare che tooadd il **ConnectionString**. Questo codice usa anche un dummy **NotificationIcon** che viene aggiunto da Mobile Engagement SDK è hello tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Abilitazione del monitoraggio in tempo reale
In ordine toostart l'invio dei dati e garantire agli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello dello schermo.

1. Aprire **ViewController.cs** e aggiungere hello seguente istruzione using:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Sostituire la classe hello da cui `ViewController` eredita da `UIViewController` troppo`EngagementViewController`. 

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti impostarle backup tooreceive l'app.

### <a name="modify-your-application-delegate"></a>Modificare il delegato dell'applicazione
1. Aprire hello **appdelegate. cs** e aggiungere hello seguente istruzione using:
   
        using System; 
2. A questo punto all'interno di hello `FinishedLaunching` metodo, aggiungere hello seguente tooregister per i messaggi push dopo`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Infine, aggiornare o aggiungere hello dei seguenti metodi:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. Nel **Info. plist** file nella soluzione hello, confermare che hello **identificatore Bundle** corrisponde alla hello **ID App** aver nel profilo di provisioning in hello Dev Apple Al centro. 
   
    ![][7]
5. In hello stesso **Info. plist** , assicurarsi di aver selezionato hello **abilitare la modalità di Background** e **notifiche remoto**. 
   
     ![][8]
6. Eseguire l'applicazione hello sul dispositivo hello che è stata associata a questo profilo di pubblicazione. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
