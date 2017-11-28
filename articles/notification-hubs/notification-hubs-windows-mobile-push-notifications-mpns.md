---
title: notifiche push aaaSending con gli hub di notifica di Azure in Windows Phone | Documenti Microsoft
description: "In questa esercitazione, è illustrato come le notifiche di toopush gli hub di notifica di Azure toouse tooa Windows Phone 8 o applicazione Silverlight di Windows Phone 8.1."
services: notification-hubs
documentationcenter: windows
keywords: notifica push, inviare notifiche push, push per windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="9df13-104">Invio di notifiche push con Hub di notifica di Azure in Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9df13-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9df13-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9df13-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="9df13-106">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9df13-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9df13-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9df13-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9df13-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="9df13-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="9df13-109">Questa esercitazione illustra come applicazione Windows Phone 8 o Windows Phone 8.1 Silverlight tooa notifiche push toouse toosend di hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="9df13-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="9df13-110">Se la destinazione è Windows Phone 8.1 (non Silverlight), quindi fare riferimento toohello [universali di Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versione.</span><span class="sxs-lookup"><span data-stu-id="9df13-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="9df13-111">In questa esercitazione, si crea un'app di Windows Phone 8 vuota che riceve le notifiche push tramite hello Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="9df13-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="9df13-112">Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="9df13-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="9df13-113">Hello SDK di Windows Phone hub di notifica non supporta l'utilizzo di hello Windows Push Notification Service (WNS) con App Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="9df13-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="9df13-114">toouse WNS (anziché MPNS) con App Windows Phone 8.1 Silverlight, seguire hello [gli hub di notifica - esercitazione di Windows Phone Silverlight], che utilizza le API REST.</span><span class="sxs-lookup"><span data-stu-id="9df13-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="9df13-115">esercitazione Hello illustra hello semplice scenario di trasmissione con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="9df13-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9df13-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9df13-116">Prerequisites</span></span>
<span data-ttu-id="9df13-117">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9df13-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9df13-118">[Visual Studio 2012 Express per Windows Phone]o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9df13-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="9df13-119">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub notifica relative ad app per Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="9df13-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="9df13-120">Creare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="9df13-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="9df13-121">Fare clic su hello <b>Notification Services</b> sezione (all'interno di <i>impostazioni</i>), fare clic su <b>Windows Phone (MPNS)</b> e quindi fare clic su hello <b>abilitare push non autenticate </b> casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="9df13-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portale di Azure - Abilita notifiche push non autenticate](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="9df13-123">L'hub è creato e configurato toosend non autenticati di notifica per Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="9df13-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="9df13-124">In questa esercitazione verrà usato il Servizio notifica Push Microsoft in modalità senza autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9df13-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="9df13-125">Modalità non autenticata MPNS prevede restrizioni delle notifiche che è possibile inviare tooeach canale.</span><span class="sxs-lookup"><span data-stu-id="9df13-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="9df13-126">Hub di notifica supporta [MPNS autenticato modalità](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) consentendo tooupload il certificato.</span><span class="sxs-lookup"><span data-stu-id="9df13-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="9df13-127">Connessione hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="9df13-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="9df13-128">In Visual Studio creare una nuova applicazione per Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="9df13-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="9df13-129">In Visual Studio 2013 Update 2 o versioni successive verrà invece creata un'applicazione per Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="9df13-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Nuovo progetto - App vuota - Windows Phone Silverlight][11]
2. <span data-ttu-id="9df13-131">In Visual Studio, fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9df13-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="9df13-132">Consente di visualizzare hello **Gestisci pacchetti NuGet** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9df13-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="9df13-133">Cercare `WindowsAzure.Messaging.Managed` e fare clic su **installare**, quindi accettare i termini di hello di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9df13-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio - Gestione pacchetti NuGet][20]
   
    <span data-ttu-id="9df13-135">Questo download, si installa e si aggiunge una raccolta di informazioni di riferimento toohello messaggistica di Azure per Windows utilizzando hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacchetto WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="9df13-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="9df13-136">Aprire il file di hello App.xaml.cs e aggiungere il seguente hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="9df13-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="9df13-137">Aggiungere hello seguente di codice in cima hello **Application_Launching** metodo App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="9df13-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="9df13-138">valore di Hello **MyPushChannel** è un indice che non toolookup usato un canale esistente in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) insieme.</span><span class="sxs-lookup"><span data-stu-id="9df13-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="9df13-139">Se non è disponibile, creare una nuova voce con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="9df13-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="9df13-140">Verificare che la stringa di connessione hub e hello tooinsert hello nome **DefaultListenSharedAccessSignature** ottenuto nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="9df13-141">Questo codice recupera l'URI del canale hello per app hello da MPNS e quindi tale URI del canale viene registrata con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="9df13-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="9df13-142">Garantisce inoltre il canale hello che URI è registrato nell'hub di notifica che viene avviata un'applicazione hello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="9df13-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9df13-143">In questa esercitazione invia un dispositivo toohello notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="9df13-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="9df13-144">Quando si invia una notifica di tipo riquadro, è necessario chiamare invece hello **BindToShellTile** metodo sul canale hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="9df13-145">toosupport le notifiche di tipo avviso popup e riquadro, chiamare sia **BindToShellTile** e **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="9df13-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="9df13-146">In Esplora soluzioni, espandere **proprietà**aprire hello `WMAppManifest.xml` file, fare clic su hello **funzionalità** scheda e verificare che tale hello **ID_CAP_PUSH_NOTIFICATION** funzionalità è selezionata.</span><span class="sxs-lookup"><span data-stu-id="9df13-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="9df13-147">Hello premere `F5` toorun chiave hello app.</span><span class="sxs-lookup"><span data-stu-id="9df13-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="9df13-148">Viene visualizzato un messaggio di registrazione nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="9df13-149">Chiudi hello app.</span><span class="sxs-lookup"><span data-stu-id="9df13-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="9df13-150">tooreceive una notifica push di tipo avviso popup, un'applicazione hello non deve essere in esecuzione in primo piano hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="9df13-151">Inviare notifiche push dal back-end</span><span class="sxs-lookup"><span data-stu-id="9df13-151">Send push notifications from your backend</span></span>
<span data-ttu-id="9df13-152">È possibile inviare notifiche push tramite hub di notifica da qualsiasi back-end tramite hello pubblico <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaccia REST</a>.</span><span class="sxs-lookup"><span data-stu-id="9df13-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="9df13-153">In questa esercitazione vengono inviate notifiche push con un'applicazione console .NET.</span><span class="sxs-lookup"><span data-stu-id="9df13-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="9df13-154">Per un esempio di come toosend notifiche push da un back-end ASP.NET WebAPI integrata con gli hub di notifica, vedere [notifica hub di notifica gli utenti di Azure con back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="9df13-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="9df13-155">Per un esempio di come le notifiche push toosend utilizzando hello [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), estrarre [come toouse gli hub di notifica da Java](notification-hubs-java-push-notification-tutorial.md) e [come toouse gli hub di notifica da PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="9df13-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="9df13-156">Soluzione di hello pulsante destro del mouse, selezionare **Aggiungi** e **nuovo progetto...** , quindi in **Visual c#**, fare clic su **Windows** e **applicazione Console**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9df13-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="9df13-157">Aggiunge una nuovo Visual c# toohello soluzione di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="9df13-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="9df13-158">Questa operazione può essere eseguita anche in una soluzione separata.</span><span class="sxs-lookup"><span data-stu-id="9df13-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="9df13-159">Fare clic su **Strumenti**, su **Gestione pacchetti libreria** e quindi su **Console di Gestione Pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="9df13-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="9df13-160">Consente di visualizzare hello Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9df13-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="9df13-161">In hello **Package Manager Console** finestra, hello set **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9df13-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="9df13-162">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="9df13-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="9df13-163">Aprire hello `Program.cs` file e aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="9df13-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="9df13-164">In hello `Program` classe, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="9df13-164">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="9df13-165">Verificare che hello tooreplace `<hub name>` con nome hello dell'hub di notifica hello visualizzata nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="9df13-166">Inoltre, sostituire i segnaposto di stringa di connessione hello con hello stringa di connessione denominata **DefaultFullSharedAccessSignature** ottenuto nella sezione hello "Configurare l'hub di notifica".</span><span class="sxs-lookup"><span data-stu-id="9df13-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9df13-167">Assicurarsi di utilizzare la stringa di connessione hello con **completo** non accedere **ascolto** accesso.</span><span class="sxs-lookup"><span data-stu-id="9df13-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="9df13-168">stringa di accesso listen Hello non dispone di notifiche push toosend di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="9df13-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="9df13-169">Aggiungere hello seguente riga del `Main` metodo:</span><span class="sxs-lookup"><span data-stu-id="9df13-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="9df13-170">Con il Windows Phone emulatore in esecuzione e il progetto di applicazione console di app hello chiuso, impostare come hello predefinito di progetto di avvio e quindi premere hello `F5` toorun chiave hello app.</span><span class="sxs-lookup"><span data-stu-id="9df13-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="9df13-171">Verrà visualizzata una notifica push di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="9df13-171">You will receive a toast push notification.</span></span> <span data-ttu-id="9df13-172">Toccando il banner di tipo avviso popup hello carica app hello.</span><span class="sxs-lookup"><span data-stu-id="9df13-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="9df13-173">È possibile trovare tutti i payload possibili hello in hello [catalogo toast] e [riquadro catalogo] argomenti su MSDN.</span><span class="sxs-lookup"><span data-stu-id="9df13-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9df13-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9df13-174">Next steps</span></span>
<span data-ttu-id="9df13-175">In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="9df13-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="9df13-176">In ordine tootarget utenti specifici, vedere toohello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9df13-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="9df13-177">Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="9df13-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="9df13-178">Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="9df13-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express per Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers le notifiche di utilizzare gli hub di notifica toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catalogo toast]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[riquadro catalogo]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[gli hub di notifica - esercitazione di Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

