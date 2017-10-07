---
title: aaaGet avviato con Azure notifica hub per App universali di Windows piattaforma | Documenti Microsoft
description: "In questa esercitazione, è illustrato come toouse gli hub di notifica di Azure toopush notifiche tooa applicazione piattaforma universale di Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="0d187-103">Introduzione ad Hub di notifica per le app della piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="0d187-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0d187-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0d187-104">Overview</span></span>
<span data-ttu-id="0d187-105">Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push app Universal Windows Platform (UWP) tooa di notifiche.</span><span class="sxs-lookup"><span data-stu-id="0d187-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="0d187-106">In questa esercitazione, si crea un'app di Windows Store vuota che riceve le notifiche push tramite servizio notifica Push Windows (WNS) hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="0d187-107">Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="0d187-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0d187-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0d187-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0d187-109">codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="0d187-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d187-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d187-110">Prerequisites</span></span>
<span data-ttu-id="0d187-111">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0d187-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0d187-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) o versione successiva</span><span class="sxs-lookup"><span data-stu-id="0d187-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="0d187-113">Strumenti per lo sviluppo di app di Windows universale</span><span class="sxs-lookup"><span data-stu-id="0d187-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="0d187-114">Account Azure attivo </span><span class="sxs-lookup"><span data-stu-id="0d187-114">An active Azure account</span></span> <br/><span data-ttu-id="0d187-115">Se non si dispone di un account Azure, è possibile creare un account di valutazione gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0d187-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d187-116">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="0d187-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="0d187-117">Account di Windows Store attivo</span><span class="sxs-lookup"><span data-stu-id="0d187-117">An active Windows Store account</span></span>

<span data-ttu-id="0d187-118">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app della piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="0d187-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="0d187-119">Registrare l'app per Windows Store hello</span><span class="sxs-lookup"><span data-stu-id="0d187-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="0d187-120">toosend le app tooUWP le notifiche push, è necessario associare il toohello app Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0d187-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="0d187-121">È quindi necessario configurare il toointegrate di hub di notifica con WNS.</span><span class="sxs-lookup"><span data-stu-id="0d187-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="0d187-122">Se non è già stato registrato l'app, passare toohello [Windows Dev Center](https://dev.windows.com/overview), accedere con l'account Microsoft e quindi fare clic su **crea una nuova app**.</span><span class="sxs-lookup"><span data-stu-id="0d187-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="0d187-123">Digitare un nome per l'app e fare clic su **Riserva nome dell'app**.</span><span class="sxs-lookup"><span data-stu-id="0d187-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="0d187-124">Verrà creata una nuova registrazione a Windows Store per l'app.</span><span class="sxs-lookup"><span data-stu-id="0d187-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="0d187-125">In Visual Studio, creare un nuovo progetto di Visual c# di App Store utilizzando universali di Windows hello **applicazione vuota** modello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d187-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="0d187-126">Accettare i valori predefiniti di hello per le versioni di piattaforma minimo e di destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="0d187-127">In Esplora soluzioni, progetti di app Windows Store hello pulsante destro del mouse, fare clic su **archivio**, quindi fare clic su **Associa applicazione a Store hello...** . hello **associare un'App con Windows Store hello** procedura guidata viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="0d187-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="0d187-128">Nella procedura guidata hello, accedere con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d187-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="0d187-129">Fare clic su app hello registrato nel passaggio 2, fare clic su **Avanti**, quindi fare clic su **associare**.</span><span class="sxs-lookup"><span data-stu-id="0d187-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="0d187-130">Consente di aggiungere il manifesto di applicazione toohello hello richiesto Windows Store registrazione informazioni.</span><span class="sxs-lookup"><span data-stu-id="0d187-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="0d187-131">In hello [Windows Dev Center](http://dev.windows.com/overview) pagina per la nuova app, fare clic su **servizi**, fare clic su **notifiche Push**, quindi fare clic su **WNS o MPNS**.</span><span class="sxs-lookup"><span data-stu-id="0d187-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="0d187-132">Fare clic su **Nuova notifica**.</span><span class="sxs-lookup"><span data-stu-id="0d187-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="0d187-133">Fare clic sul modello **Blank (Toast)** (Vuoto - Avviso popup) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d187-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="0d187-134">Immettere un **nome** per la notifica e un messaggio **contesto** visivo.</span><span class="sxs-lookup"><span data-stu-id="0d187-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="0d187-135">Fare clic su **Salva come bozza**.</span><span class="sxs-lookup"><span data-stu-id="0d187-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="0d187-136">Passare toohello [portale di registrazione applicazione](http://apps.dev.microsoft.com) ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="0d187-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="0d187-137">Fare clic sul nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d187-137">Click on your application name.</span></span> <span data-ttu-id="0d187-138">Prendere nota di hello **segreto dell'applicazione** password e hello **ID di pacchetto sicurezza (SID)** si trova in hello **Windows Store** impostazioni piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0d187-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="0d187-139">segreto dell'applicazione Hello e il SID pacchetto sono credenziali di sicurezza importanti.</span><span class="sxs-lookup"><span data-stu-id="0d187-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="0d187-140">Non condividere questi valori con altri utenti né distribuirli con l'app.</span><span class="sxs-lookup"><span data-stu-id="0d187-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="0d187-141">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="0d187-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="0d187-142">Seleziona hello <b>Notification Services</b> opzione e hello <b>Windows (WNS)</b> opzione.</span><span class="sxs-lookup"><span data-stu-id="0d187-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="0d187-143">Immettere quindi hello <b>segreto dell'applicazione</b> password in hello <b>chiave di sicurezza</b> campo.</span><span class="sxs-lookup"><span data-stu-id="0d187-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="0d187-144">Immettere il <b>SID pacchetto</b> valore che è stato ottenuto da WNS nella sezione precedente hello e quindi fare clic su <b>salvare</b>.</span><span class="sxs-lookup"><span data-stu-id="0d187-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="0d187-145">Hub di notifica è ora configurato toowork con WNS e aver tooregister stringhe di connessione hello app e inviare notifiche.</span><span class="sxs-lookup"><span data-stu-id="0d187-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="0d187-146">Connettere l'hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="0d187-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="0d187-147">In Visual Studio, fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0d187-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="0d187-148">Consente di visualizzare hello **Gestisci pacchetti NuGet** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0d187-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="0d187-149">Cercare `WindowsAzure.Messaging.Managed` e fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="0d187-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="0d187-150">Questo download, si installa e si aggiunge una raccolta di informazioni di riferimento toohello messaggistica di Azure per Windows utilizzando hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacchetto WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="0d187-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="0d187-151">Aprire il file di progetto App.xaml.cs hello e aggiungere il seguente hello `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="0d187-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="0d187-152">Anche in App.xaml.cs, aggiungere il seguente hello **InitNotificationsAsync** toohello definizione di metodo **App** classe:</span><span class="sxs-lookup"><span data-stu-id="0d187-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="0d187-153">Questo codice recupera l'URI del canale hello per app hello da WNS e quindi tale URI del canale viene registrata con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0d187-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0d187-154">Verificare che tooreplace hello segnaposto "il nome hub" con il nome di hello dell'hub di notifica hello che viene visualizzato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="0d187-155">Sostituire i segnaposto di stringa di connessione hello anche con hello **DefaultListenSharedAccessSignature** stringa di connessione che è stato ottenuto da hello **criteri di accesso** pagina dell'Hub di notifica in un sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="0d187-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="0d187-156">Nella parte superiore di hello di hello **OnLaunched** gestore dell'evento in App.xaml.cs, aggiungere hello seguente chiamata toohello nuova **InitNotificationsAsync** metodo:</span><span class="sxs-lookup"><span data-stu-id="0d187-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="0d187-157">In questo modo si garantisce il canale hello che URI è registrato nell'hub di notifica che viene avviata un'applicazione hello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="0d187-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="0d187-158">Hello premere **F5** toorun chiave hello app.</span><span class="sxs-lookup"><span data-stu-id="0d187-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="0d187-159">Viene visualizzata una finestra di dialogo popup che contiene la chiave di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="0d187-160">L'app è pronta tooreceive popup.</span><span class="sxs-lookup"><span data-stu-id="0d187-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="0d187-161">Inviare notifiche</span><span class="sxs-lookup"><span data-stu-id="0d187-161">Send notifications</span></span>
<span data-ttu-id="0d187-162">È possibile verificare rapidamente la ricezione di notifiche nell'app mediante l'invio di notifiche in hello [portale Azure](https://portal.azure.com/) utilizzando hello **invio di Test** pulsante hub di notifica hello, come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d187-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="0d187-163">Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile.</span><span class="sxs-lookup"><span data-stu-id="0d187-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="0d187-164">È inoltre possibile utilizzare hello API REST direttamente i messaggi di notifica toosend se una raccolta non è disponibile per il back-end.</span><span class="sxs-lookup"><span data-stu-id="0d187-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="0d187-165">In questa esercitazione verrà semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="0d187-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="0d187-166">Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d187-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="0d187-167">Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:</span><span class="sxs-lookup"><span data-stu-id="0d187-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="0d187-168">**Interfaccia REST**: È possibile supportare la notifica su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d187-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="0d187-169">**Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="0d187-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="0d187-170">**Node.js** : [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0d187-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="0d187-171">**App per dispositivi mobili Azure**: per un esempio di come le notifiche di toosend da un'App Mobile di Azure è integrato con hub di notifica, vedere [aggiungere notifiche push per App per dispositivi mobili](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="0d187-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="0d187-172">**Java o PHP**: per un esempio di come le notifiche toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="0d187-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="0d187-173">(Facoltativo) Inviare notifiche da un'app console</span><span class="sxs-lookup"><span data-stu-id="0d187-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="0d187-174">le notifiche toosend tramite un'applicazione console .NET seguono questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="0d187-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="0d187-175">Soluzione di hello pulsante destro del mouse, selezionare **Aggiungi** e **nuovo progetto...** , quindi in **Visual c#**, fare clic su **Windows** e **applicazione Console**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d187-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="0d187-176">Aggiunge una nuovo Visual c# toohello soluzione di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="0d187-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="0d187-177">Questa operazione può essere eseguita anche in una soluzione separata.</span><span class="sxs-lookup"><span data-stu-id="0d187-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="0d187-178">In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="0d187-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="0d187-179">Consente di visualizzare la Console di gestione pacchetti hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d187-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="0d187-180">Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d187-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0d187-181">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="0d187-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="0d187-182">Aprire il file Program.cs hello e aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="0d187-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0d187-183">In hello **programma** classe, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="0d187-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="0d187-184">Assicurarsi di utilizzare una stringa di connessione hello è **completo** non accedere **ascolto** accesso.</span><span class="sxs-lookup"><span data-stu-id="0d187-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="0d187-185">stringa di accesso listen Hello è notifiche toosend autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="0d187-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="0d187-186">Aggiungere hello seguenti righe hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="0d187-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0d187-187">Fare clic sul progetto applicazione console hello in Visual Studio e fare clic su **imposta come progetto di avvio** tooset come progetto di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="0d187-188">Premere quindi hello **F5** applicazione hello toorun della chiave.</span><span class="sxs-lookup"><span data-stu-id="0d187-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="0d187-189">Tutti i dispositivi registrati riceveranno una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="0d187-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="0d187-190">Banner di tipo avviso popup facendo clic o toccando hello carica app hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="0d187-191">È possibile trovare tutti i payload hello è supportato in hello [catalogo toast], [riquadro catalogo], e [badge Panoramica] argomenti su MSDN.</span><span class="sxs-lookup"><span data-stu-id="0d187-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d187-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d187-192">Next steps</span></span>
<span data-ttu-id="0d187-193">In questo semplice esempio è stata inviata notifiche tooall i dispositivi Windows con il portale di hello o un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="0d187-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="0d187-194">Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione come passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="0d187-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="0d187-195">Verrà descritto come toosend notifiche da un back-end ASP.NET usando tag tootarget specifici utenti.</span><span class="sxs-lookup"><span data-stu-id="0d187-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="0d187-196">Se si desidera che gli utenti dai gruppi di interesse toosegment, vedere [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="0d187-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="0d187-197">toolearn informazioni generali sull'hub di notifica, vedere [materiale sussidiario per gli hub di notifica](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d187-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers le notifiche di utilizzare gli hub di notifica toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catalogo toast]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[riquadro catalogo]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[badge Panoramica]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
