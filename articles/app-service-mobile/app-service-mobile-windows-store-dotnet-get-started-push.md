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
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="2a03c-103">Aggiungere app di Windows tooyour le notifiche push</span><span class="sxs-lookup"><span data-stu-id="2a03c-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="2a03c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2a03c-104">Overview</span></span>
<span data-ttu-id="2a03c-105">In questa esercitazione, si aggiunge toohello le notifiche push [avvio rapido di Windows](app-service-mobile-windows-store-dotnet-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="2a03c-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="2a03c-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="2a03c-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="2a03c-107">Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2a03c-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="2a03c-108"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="2a03c-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="2a03c-109">Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="2a03c-109">Register your app for push notifications</span></span>
<span data-ttu-id="2a03c-110">È necessario toosubmit il toohello app Windows Store, quindi configurare il toointegrate di project server con servizi notifica Windows (WNS) toosend push.</span><span class="sxs-lookup"><span data-stu-id="2a03c-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="2a03c-111">In Esplora soluzioni Visual Studio, progetto di app UWP hello pulsante destro del mouse, fare clic su **archivio** > **Associa applicazione a Store hello...** .</span><span class="sxs-lookup"><span data-stu-id="2a03c-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="2a03c-113">Nella procedura guidata hello, fare clic su **Avanti**, accedere con l'account Microsoft, digitare un nome per l'app in **riserva nuovo nome applicazione**, quindi fare clic su **riserva**.</span><span class="sxs-lookup"><span data-stu-id="2a03c-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="2a03c-114">Dopo la registrazione di app hello è nuovo nome di applicazione hello è stata creata, selezionare, fare clic su **Avanti**, quindi fare clic su **associare**.</span><span class="sxs-lookup"><span data-stu-id="2a03c-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="2a03c-115">Consente di aggiungere il manifesto di applicazione toohello hello richiesto Windows Store registrazione informazioni.</span><span class="sxs-lookup"><span data-stu-id="2a03c-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="2a03c-116">Passare toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), accedi al tuo account Microsoft, fare clic su nuova registrazione app hello in **le mie app**, quindi espandere **servizi**  >  **Notifiche push**.</span><span class="sxs-lookup"><span data-stu-id="2a03c-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="2a03c-117">In hello **notifiche Push** pagina, fare clic su **sito Services Live** in **servizi mobili di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a03c-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="2a03c-118">Nella pagina di registrazione hello, prendere nota del valore di hello **segreti applicazione** hello e **SID pacchetto**, che verrà successivamente utilizzato tooconfigure back-end dell'app mobile.</span><span class="sxs-lookup"><span data-stu-id="2a03c-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="2a03c-120">segreto client Hello e il SID pacchetto sono credenziali di sicurezza importanti.</span><span class="sxs-lookup"><span data-stu-id="2a03c-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="2a03c-121">Non condividere questi valori con altri utenti né distribuirli con l'app.</span><span class="sxs-lookup"><span data-stu-id="2a03c-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="2a03c-122">Hello **Id applicazione** utilizzata con autenticazione di Account Microsoft hello tooconfigure segreta.</span><span class="sxs-lookup"><span data-stu-id="2a03c-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="2a03c-123">Configurare le notifiche push toosend di hello back-end</span><span class="sxs-lookup"><span data-stu-id="2a03c-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="2a03c-124"><a id="update-service"></a>Aggiornare le notifiche push di hello server toosend</span><span class="sxs-lookup"><span data-stu-id="2a03c-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="2a03c-125">Utilizzare hello procedura descritta di seguito che corrisponde al tipo di progetto back-end&mdash;entrambi [back-end .NET](#dotnet) o [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="2a03c-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="2a03c-126"><a name="dotnet"></a>Progetto di back-end .NET</span><span class="sxs-lookup"><span data-stu-id="2a03c-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="2a03c-127">In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**, cercare Microsoft.Azure.NotificationHubs, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="2a03c-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="2a03c-128">Libreria di hello hub di notifica client vengono installati.</span><span class="sxs-lookup"><span data-stu-id="2a03c-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="2a03c-129">Espandere **controller**, aprire TodoItemController.cs e aggiungere hello seguenti istruzioni using:</span><span class="sxs-lookup"><span data-stu-id="2a03c-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="2a03c-130">In hello **PostTodoItem** metodo, aggiungere hello seguente codice dopo la chiamata hello troppo**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="2a03c-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

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

    <span data-ttu-id="2a03c-131">Questo codice indica toosend hub di notifica hello una notifica push di una volta un nuovo elemento di inserimento.</span><span class="sxs-lookup"><span data-stu-id="2a03c-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="2a03c-132">Ripubblicare progetto server hello.</span><span class="sxs-lookup"><span data-stu-id="2a03c-132">Republish hello server project.</span></span>

### <span data-ttu-id="2a03c-133"><a name="nodejs"></a>Progetto di back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="2a03c-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="2a03c-134">Se non è già fatto, [scaricare il progetto di avvio rapido hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o altrimenti utilizzare hello [editor online nel portale di Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="2a03c-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="2a03c-135">Sostituire il codice esistente nel file todoitem.js hello hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="2a03c-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

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

    <span data-ttu-id="2a03c-136">Invia una notifica di tipo avviso popup WNS contenente item.text hello quando viene inserito un nuovo elemento di attività.</span><span class="sxs-lookup"><span data-stu-id="2a03c-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="2a03c-137">Quando si modifica il file hello nel computer locale, pubblicare di nuovo progetto server hello.</span><span class="sxs-lookup"><span data-stu-id="2a03c-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="2a03c-138"><a id="update-app"></a>Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="2a03c-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="2a03c-139">L'app dovrà quindi registrarsi per le notifiche push all'avvio.</span><span class="sxs-lookup"><span data-stu-id="2a03c-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="2a03c-140">Quando già stata abilitata l'autenticazione, assicurarsi che tale hello accesso dell'utente prima di tentare di tooregister per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="2a03c-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="2a03c-141">Aprire hello **App.xaml.cs** file di progetto e aggiungere il seguente hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="2a03c-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="2a03c-142">In hello stesso file, aggiungere il seguente hello **InitNotificationsAsync** toohello definizione di metodo **App** classe:</span><span class="sxs-lookup"><span data-stu-id="2a03c-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="2a03c-143">Il codice recupera hello URI di canale per l'applicazione hello da WNS e quindi registra tale canale con l'App Mobile di servizio App.</span><span class="sxs-lookup"><span data-stu-id="2a03c-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="2a03c-144">Nella parte superiore di hello di hello **OnLaunched** gestore dell'evento in **App.xaml.cs**, aggiungere hello **async** la definizione di metodo toohello modificatore e aggiungere i seguenti hello chiamare nuovatoohello **InitNotificationsAsync** (metodo), come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2a03c-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="2a03c-145">In questo modo si garantisce che hello che channeluri di breve durata viene registrato ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a03c-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="2a03c-146">Ricompilare il progetto dell'app UWP.</span><span class="sxs-lookup"><span data-stu-id="2a03c-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="2a03c-147">L'app è pronta tooreceive popup.</span><span class="sxs-lookup"><span data-stu-id="2a03c-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="2a03c-148"><a id="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="2a03c-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="2a03c-149"><a id="more"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a03c-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="2a03c-150">Altre informazioni sulle notifiche push:</span><span class="sxs-lookup"><span data-stu-id="2a03c-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="2a03c-151">Modalità di gestione client per App mobili di Azure hello toouse</span><span class="sxs-lookup"><span data-stu-id="2a03c-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="2a03c-152">I modelli consentono di push multipiattaforma toosend di flessibilità e push localizzata.</span><span class="sxs-lookup"><span data-stu-id="2a03c-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="2a03c-153">Informazioni su come tooregister modelli.</span><span class="sxs-lookup"><span data-stu-id="2a03c-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="2a03c-154">Diagnose push notification issues</span><span class="sxs-lookup"><span data-stu-id="2a03c-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="2a03c-155">(Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2a03c-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="2a03c-156">Questo argomento viene illustrato come tooanalyze e individuare la radice hello causa dell'assenza di errori di notifica push.</span><span class="sxs-lookup"><span data-stu-id="2a03c-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="2a03c-157">È consigliabile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="2a03c-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="2a03c-158">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="2a03c-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="2a03c-159">Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="2a03c-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="2a03c-160">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="2a03c-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="2a03c-161">Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="2a03c-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="2a03c-162">Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="2a03c-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
