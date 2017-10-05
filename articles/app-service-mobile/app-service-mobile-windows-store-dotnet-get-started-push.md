---
title: Aggiungere notifiche push all'app UWP (Universal Windows Platform) | Documentazione Microsoft
description: Informazioni su come usare le app per dispositivi mobili del servizio app di Azure e gli hub di notifica di Azure per inviare notifiche push all'app UWP (Universal Windows Platform).
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
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="aae46-103">Aggiungere notifiche push all'app di Windows</span><span class="sxs-lookup"><span data-stu-id="aae46-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="aae46-104">Overview</span><span class="sxs-lookup"><span data-stu-id="aae46-104">Overview</span></span>
<span data-ttu-id="aae46-105">In questa esercitazione vengono aggiunte notifiche push al progetto [avvio rapido di Windows](app-service-mobile-windows-store-dotnet-get-started.md), in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="aae46-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="aae46-106">Se non si usa il progetto server di avvio rapido scaricato, sarà necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="aae46-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="aae46-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="aae46-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="aae46-108"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="aae46-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="aae46-109">Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="aae46-109">Register your app for push notifications</span></span>
<span data-ttu-id="aae46-110">È necessario inviare l'app a Windows Store, quindi configurare il progetto server in modo che venga eseguita l'integrazione con Servizi notifica Windows per l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="aae46-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="aae46-111">In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sul progetto dell'app UWP, quindi scegliere **Store** > **Associa applicazione a Store**.</span><span class="sxs-lookup"><span data-stu-id="aae46-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="aae46-113">Nella procedura guidata fare clic su **Avanti**, effettuare l'accesso con l'account Microsoft, immettere un nome per l'app in **Riserva un nuovo nome dell'app** e quindi fare clic su **Reserva**.</span><span class="sxs-lookup"><span data-stu-id="aae46-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="aae46-114">Dopo la creazione della registrazione dell'app, selezionare il nuovo nome dell'app, fare clic su **Avanti** e quindi su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="aae46-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="aae46-115">Le informazioni di registrazione a Windows Store necessarie verranno aggiunte al manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aae46-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="aae46-116">Passare a [Windows Dev Center](https://dev.windows.com/en-us/overview), accedere con l'account Microsoft, fare clic sulla nuova registrazione di app in **App personali**, quindi espandere **Servizi** > **Notifiche push**.</span><span class="sxs-lookup"><span data-stu-id="aae46-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="aae46-117">Nella pagina **Notifiche push** fare clic su **Sito di servizi Live** in **Servizi mobili di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="aae46-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="aae46-118">Nella pagina di registrazione prendere nota del valore in **Segreti applicazione** e **SID pacchetto**. Questi valori verranno utilizzati successivamente per configurare il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="aae46-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Associa l’app con Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="aae46-120">Il segreto client e il SID di pacchetto sono importanti credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="aae46-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="aae46-121">Non condividere questi valori con altri utenti né distribuirli con l'app.</span><span class="sxs-lookup"><span data-stu-id="aae46-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="aae46-122">L' **ID applicazione** viene usato con il segreto per configurare l'autenticazione dell'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aae46-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="aae46-123">Configurare il back-end per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="aae46-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="aae46-124"><a id="update-service"></a>Aggiornare il server per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="aae46-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="aae46-125">Usare la procedura corrispondente al tipo di progetto di back-end in corso:&mdash; [back-end .NET](#dotnet) o [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="aae46-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="aae46-126"><a name="dotnet"></a>Progetto di back-end .NET</span><span class="sxs-lookup"><span data-stu-id="aae46-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="aae46-127">In Visual Studio fare clic con il pulsante destro del mouse sul progetto server, scegliere **Gestisci pacchetti NuGet**, cercare Microsoft.Azure.NotificationHubs e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="aae46-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="aae46-128">Verrà installata la libreria client dell'Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="aae46-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="aae46-129">Espandere **Controller**, aprire TodoItemController.cs e aggiungere le istruzioni using seguenti:</span><span class="sxs-lookup"><span data-stu-id="aae46-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="aae46-130">Nel metodo **PostTodoItem** aggiungere il codice seguente dopo la chiamata a **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="aae46-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="aae46-131">Questo codice indica all'hub di notifica di inviare una notifica push dopo l'inserimento di un nuovo elemento.</span><span class="sxs-lookup"><span data-stu-id="aae46-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="aae46-132">Pubblicare di nuovo il progetto server.</span><span class="sxs-lookup"><span data-stu-id="aae46-132">Republish the server project.</span></span>

### <span data-ttu-id="aae46-133"><a name="nodejs"></a>Progetto di back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="aae46-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="aae46-134">[Scaricare il progetto di avvio rapido](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) (se non è ancora stato scaricato) oppure usare l'[editor online del portale di Azure](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="aae46-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="aae46-135">Sostituire il codice esistente nel file todoitem.js file con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aae46-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="aae46-136">Ogni volta che viene inserito un nuovo elemento Todo, viene inviata una notifica popup WNS contenente l'elemento item.text.</span><span class="sxs-lookup"><span data-stu-id="aae46-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="aae46-137">Quando si modifica il file nel computer locale, ripubblicare il progetto server.</span><span class="sxs-lookup"><span data-stu-id="aae46-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="aae46-138"><a id="update-app"></a>Aggiungere notifiche push all'app</span><span class="sxs-lookup"><span data-stu-id="aae46-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="aae46-139">L'app dovrà quindi registrarsi per le notifiche push all'avvio.</span><span class="sxs-lookup"><span data-stu-id="aae46-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="aae46-140">Se l'autenticazione è già stata abilitata, verificare che l'utente esegua l'accesso prima di registrarsi per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="aae46-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="aae46-141">Aprire il file di progetto **App.xaml.cs** e aggiungere le istruzioni `using` seguenti:</span><span class="sxs-lookup"><span data-stu-id="aae46-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="aae46-142">Nello stesso file aggiungere la seguente definizione del metodo **InitNotificationsAsync** alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="aae46-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="aae46-143">Questo codice consente di recuperare il valore di ChannelURI per l'app da Servizi notifica Push Windows e quindi di registrarlo con l'app per dispositivi mobili del servizio app.</span><span class="sxs-lookup"><span data-stu-id="aae46-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="aae46-144">All'inizio del gestore eventi **OnLaunched** nel file **App.xaml.cs** aggiungere il modificatore **async** alla definizione del metodo e quindi aggiungere la seguente chiamata al nuovo metodo **InitNotificationsAsync**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aae46-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="aae46-145">In tal modo si garantirà che il valore di ChannelURI temporaneo venga registrato ogni volta che l'applicazione viene avviata.</span><span class="sxs-lookup"><span data-stu-id="aae46-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="aae46-146">Ricompilare il progetto dell'app UWP.</span><span class="sxs-lookup"><span data-stu-id="aae46-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="aae46-147">L'app è ora pronta per ricevere notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="aae46-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="aae46-148"><a id="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="aae46-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="aae46-149"><a id="more"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aae46-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="aae46-150">Altre informazioni sulle notifiche push:</span><span class="sxs-lookup"><span data-stu-id="aae46-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="aae46-151">Come usare il client gestito per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="aae46-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="aae46-152">I modelli offrono flessibilità per inviare notifiche push multipiattaforma e push localizzati.</span><span class="sxs-lookup"><span data-stu-id="aae46-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="aae46-153">Informazioni su come registrare i modelli.</span><span class="sxs-lookup"><span data-stu-id="aae46-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="aae46-154">Diagnose push notification issues</span><span class="sxs-lookup"><span data-stu-id="aae46-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="aae46-155">(Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="aae46-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="aae46-156">Questo argomento illustra come analizzare e capire la causa radice degli errori relativi alle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="aae46-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="aae46-157">È consigliabile proseguire con una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="aae46-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="aae46-158">Aggiungere l'autenticazione all'app Windows</span><span class="sxs-lookup"><span data-stu-id="aae46-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="aae46-159">Informazioni sull'autenticazione degli utenti dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="aae46-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="aae46-160">Abilitare la sincronizzazione offline per l'app</span><span class="sxs-lookup"><span data-stu-id="aae46-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="aae46-161">: informazioni su come aggiungere il supporto offline all'app usando il back-end di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="aae46-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="aae46-162">La sincronizzazione offline consente agli utenti finali di interagire con un'app&mdash;visualizzando, aggiungendo e modificando i dati&mdash;anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="aae46-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
