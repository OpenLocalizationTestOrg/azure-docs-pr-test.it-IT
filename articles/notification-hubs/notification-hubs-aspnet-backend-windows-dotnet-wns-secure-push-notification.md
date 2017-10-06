---
title: aaaAzure notifica hub Secure Push
description: Informazioni su come toosend sicuro le notifiche push in Azure. Esempi di codice scritti in c# utilizzando hello API .NET.
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="fb6a9-104">Push sicuro degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="fb6a9-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb6a9-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="fb6a9-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="fb6a9-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fb6a9-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="fb6a9-107">Android</span><span class="sxs-lookup"><span data-stu-id="fb6a9-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fb6a9-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fb6a9-108">Overview</span></span>
<span data-ttu-id="fb6a9-109">Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura push di semplice utilizzo, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="fb6a9-110">A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="fb6a9-111">In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra il dispositivo di client hello e back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="fb6a9-112">In generale, il flusso di hello è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="fb6a9-113">Hello app back-end:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-113">hello app back-end:</span></span>
   * <span data-ttu-id="fb6a9-114">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="fb6a9-115">Invia ID hello del dispositivo notifica toohello (viene inviata alcuna informazione protetta).</span><span class="sxs-lookup"><span data-stu-id="fb6a9-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="fb6a9-116">Hello app sul dispositivo hello, quando si riceve notifica hello:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="fb6a9-117">dispositivo di Hello contatta hello back-end richiedente hello sicura payload.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="fb6a9-118">app Hello possono mostrare payload hello come una notifica sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="fb6a9-119">È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="fb6a9-120">In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="fb6a9-121">Se l'applicazione non archivia i token di autenticazione nel dispositivo hello, o se i token possono essere scaduti, hello app del dispositivo, al momento della ricezione di notifiche di hello deve essere visualizzato una generica notifica conferma hello utente toolaunch hello app.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="fb6a9-122">app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="fb6a9-123">Questa esercitazione Secure Push viene illustrato come toosend una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="fb6a9-124">Hello esercitazione si basa sulle hello [notifica utenti](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="fb6a9-125">Questa esercitazione presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="fb6a9-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="fb6a9-126">Si noti inoltre che Windows Phone 8.1 richiede le credenziali di Windows (non di Windows Phone) e che le attività in background non funzionano in Windows Phone 8.0 o Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="fb6a9-127">Per le applicazioni Windows Store, è possibile ricevere notifiche tramite un'attività in background solo se l'applicazione hello è abilitato blocco schermo (scegliere la casella di controllo hello in hello Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="fb6a9-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="fb6a9-128">Modificare hello progetto Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fb6a9-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="fb6a9-129">In hello **NotifyUserWindowsPhone** del progetto, aggiungere hello attività in background push hello tooregister tooApp.xaml.cs codice seguente.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="fb6a9-130">Aggiungere hello successiva riga di codice alla fine hello hello `OnLaunched()` metodo:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="fb6a9-131">Ancora in App.xaml.cs, aggiungere hello seguente codice immediatamente dopo hello `OnLaunched()` metodo:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="fb6a9-132">Aggiungere il seguente hello `using` istruzioni alla parte superiore di hello del file App.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="fb6a9-133">Da hello **File** menu in Visual Studio, fare clic su **Salva tutto**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="fb6a9-134">Creare hello Push componente in Background</span><span class="sxs-lookup"><span data-stu-id="fb6a9-134">Create hello Push Background Component</span></span>
<span data-ttu-id="fb6a9-135">passaggio successivo Hello è componente di toocreate hello push in background.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="fb6a9-136">In Esplora soluzioni, fare clic sul nodo di primo livello della soluzione hello hello (**soluzione SecurePush** in questo caso), quindi fare clic su **Aggiungi**, quindi fare clic su **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="fb6a9-137">Espandere **Applicazioni Windows Store**, fare clic su **App di Windows Phone** e quindi su **Componente Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="fb6a9-138">Progetto hello nome **PushBackgroundComponent**, quindi fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="fb6a9-139">In Esplora soluzioni fare doppio clic su hello **PushBackgroundComponent (Windows Phone 8.1)** del progetto, quindi fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="fb6a9-140">Nome nuova classe hello **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="fb6a9-141">Fare clic su **Aggiungi** classe hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="fb6a9-142">Sostituire l'intero contenuto di hello di hello **PushBackgroundComponent** definizione dello spazio dei nomi con hello nel codice seguente, sostituendo i segnaposto hello `{back-end endpoint}` con endpoint di back-end hello ottenuto durante la distribuzione del back-end:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="fb6a9-143">In Esplora soluzioni fare doppio clic su hello **PushBackgroundComponent (Windows Phone 8.1)** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="fb6a9-144">Sul lato sinistro di hello, fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="fb6a9-145">In hello **ricerca** digitare **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="fb6a9-146">Nell'elenco risultati hello, fare clic su **Microsoft HTTP Client Libraries**, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="fb6a9-147">Completare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-147">Complete hello installation.</span></span>
9. <span data-ttu-id="fb6a9-148">In hello NuGet **ricerca** digitare **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="fb6a9-149">Installare hello **Json.NET** pacchetto, quindi finestra di gestione pacchetti NuGet hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="fb6a9-150">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **PushBackgroundTask.cs** file:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="fb6a9-151">In Esplora soluzioni, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** del progetto, fare doppio clic su **riferimenti**, quindi fare clic su **Aggiungi riferimento...** . Nella finestra di dialogo Gestione riferimenti hello casella di controllo hello accanto troppo**PushBackgroundComponent**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="fb6a9-152">In Esplora soluzioni fare doppio clic su **package. appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** progetto.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="fb6a9-153">In **notifiche**, impostare **in grado di tipo avviso popup** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="fb6a9-154">Ancora in **package. appxmanifest**, fare clic su hello **dichiarazioni** menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="fb6a9-155">In hello **dichiarazioni disponibili** elenco a discesa, fare clic su **attività in Background**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="fb6a9-156">In **Package.appxmanifest**, in **Proprietà** selezionare **Notifica Push**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="fb6a9-157">In **package. appxmanifest**in **impostazioni App**, tipo **PushBackgroundComponent.PushBackgroundTask** in hello **punto di ingresso** campo.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="fb6a9-158">Da hello **File** menu, fare clic su **Salva tutto**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="fb6a9-159">Eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fb6a9-159">Run hello Application</span></span>
<span data-ttu-id="fb6a9-160">toorun applicazione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb6a9-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="fb6a9-161">In Visual Studio, eseguire hello **AppBackend** applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="fb6a9-162">Verrà visualizzata una pagina Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="fb6a9-163">In Visual Studio, eseguire hello **NotifyUserWindowsPhone (Windows Phone 8.1)** app di Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="fb6a9-164">emulatore Windows Phone Hello viene eseguito e carica app hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="fb6a9-165">In hello **NotifyUserWindowsPhone** app dell'interfaccia utente, immettere un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="fb6a9-166">Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="fb6a9-167">In hello **NotifyUserWindowsPhone** app dell'interfaccia utente, fare clic su **Accedi e registrare**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="fb6a9-168">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="fb6a9-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
