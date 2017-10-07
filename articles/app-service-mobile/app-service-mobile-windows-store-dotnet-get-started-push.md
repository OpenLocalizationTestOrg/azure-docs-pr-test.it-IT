---
title: app Universal Windows Platform (UWP) di aaaAdd push notifiche tooyour | Documenti Microsoft
description: Informazioni su come toouse App Mobile di servizio App di Azure e gli hub di notifica di Azure toosend push app Universal Windows Platform (UWP) tooyour di notifiche.
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Aggiungere app di Windows tooyour le notifiche push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, si aggiunge toohello le notifiche push [avvio rapido di Windows](app-service-mobile-windows-store-dotnet-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push. Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.

## <a name="configure-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Registrare l'app per le notifiche push
È necessario toosubmit il toohello app Windows Store, quindi configurare il toointegrate di project server con servizi notifica Windows (WNS) toosend push.

1. In Esplora soluzioni Visual Studio, progetto di app UWP hello pulsante destro del mouse, fare clic su **archivio** > **Associa applicazione a Store hello...** .

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. Nella procedura guidata hello, fare clic su **Avanti**, accedere con l'account Microsoft, digitare un nome per l'app in **riserva nuovo nome applicazione**, quindi fare clic su **riserva**.
3. Dopo la registrazione di app hello è nuovo nome di applicazione hello è stata creata, selezionare, fare clic su **Avanti**, quindi fare clic su **associare**. Consente di aggiungere il manifesto di applicazione toohello hello richiesto Windows Store registrazione informazioni.  
4. Passare toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), accedi al tuo account Microsoft, fare clic su nuova registrazione app hello in **le mie app**, quindi espandere **servizi**  >  **Notifiche push**.
5. In hello **notifiche Push** pagina, fare clic su **sito Services Live** in **servizi mobili di Microsoft Azure**.
6. Nella pagina di registrazione hello, prendere nota del valore di hello **segreti applicazione** hello e **SID pacchetto**, che verrà successivamente utilizzato tooconfigure back-end dell'app mobile.

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > segreto client Hello e il SID pacchetto sono credenziali di sicurezza importanti. Non condividere questi valori con altri utenti né distribuirli con l'app. Hello **Id applicazione** utilizzata con autenticazione di Account Microsoft hello tooconfigure segreta.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Configurare le notifiche push toosend di hello back-end
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Aggiornare le notifiche push di hello server toosend
Utilizzare hello procedura descritta di seguito che corrisponde al tipo di progetto back-end&mdash;entrambi [back-end .NET](#dotnet) o [back-end Node.js](#nodejs).

### <a name="dotnet"></a>Progetto di back-end .NET
1. In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**, cercare Microsoft.Azure.NotificationHubs, quindi fare clic su **installare**. Libreria di hello hub di notifica client vengono installati.
2. Espandere **controller**, aprire TodoItemController.cs e aggiungere hello seguenti istruzioni using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. In hello **PostTodoItem** metodo, aggiungere hello seguente codice dopo la chiamata hello troppo**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Questo codice indica toosend hub di notifica hello una notifica push di una volta un nuovo elemento di inserimento.
4. Ripubblicare progetto server hello.

### <a name="nodejs"></a>Progetto di back-end Node.js
1. Se non è già fatto, [scaricare il progetto di avvio rapido hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o altrimenti utilizzare hello [editor online nel portale di Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Sostituire il codice esistente nel file todoitem.js hello hello con seguenti hello:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    Invia una notifica di tipo avviso popup WNS contenente item.text hello quando viene inserito un nuovo elemento di attività.
3. Quando si modifica il file hello nel computer locale, pubblicare di nuovo progetto server hello.

## <a id="update-app"></a>Aggiungere app tooyour di notifiche push
L'app dovrà quindi registrarsi per le notifiche push all'avvio. Quando già stata abilitata l'autenticazione, assicurarsi che tale hello accesso dell'utente prima di tentare di tooregister per le notifiche push.

1. Aprire hello **App.xaml.cs** file di progetto e aggiungere il seguente hello `using` istruzioni:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. In hello stesso file, aggiungere il seguente hello **InitNotificationsAsync** toohello definizione di metodo **App** classe:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Il codice recupera hello URI di canale per l'applicazione hello da WNS e quindi registra tale canale con l'App Mobile di servizio App.
3. Nella parte superiore di hello di hello **OnLaunched** gestore dell'evento in **App.xaml.cs**, aggiungere hello **async** la definizione di metodo toohello modificatore e aggiungere i seguenti hello chiamare nuovatoohello **InitNotificationsAsync** (metodo), come in hello di esempio seguente:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    In questo modo si garantisce che hello che channeluri di breve durata viene registrato ogni volta che viene avviata l'applicazione hello.
4. Ricompilare il progetto dell'app UWP. L'app è pronta tooreceive popup.

## <a id="test"></a>Testare le notifiche push nell'app
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Passaggi successivi
Altre informazioni sulle notifiche push:

* [Modalità di gestione client per App mobili di Azure hello toouse](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  I modelli consentono di push multipiattaforma toosend di flessibilità e push localizzata. Informazioni su come tooregister modelli.
* [Diagnose push notification issues](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  (Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi. Questo argomento viene illustrato come tooanalyze e individuare la radice hello causa dell'assenza di errori di notifica push.

È consigliabile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app tooyour authentication](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.
* [Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile. Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
