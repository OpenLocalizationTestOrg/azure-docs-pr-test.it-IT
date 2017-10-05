---
title: Push sicuro degli hub di notifica di Azure
description: Informazioni su come inviare notifiche push sicure in Azure. Gli esempi di codice sono scritti in C# mediante l'API .NET.
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="18dd2-104">Push sicuro degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="18dd2-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18dd2-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="18dd2-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="18dd2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="18dd2-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="18dd2-107">Android</span><span class="sxs-lookup"><span data-stu-id="18dd2-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="18dd2-108">Overview</span><span class="sxs-lookup"><span data-stu-id="18dd2-108">Overview</span></span>
<span data-ttu-id="18dd2-109">Il supporto per le notifiche push in Microsoft Azure consente di accedere a un'infrastruttura push di facile utilizzo, multipiattaforma con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="18dd2-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="18dd2-110">A causa di vincoli normativi o di sicurezza, un'applicazione potrebbe talvolta includere nella notifica informazioni che non è possibile trasmettere attraverso l'infrastruttura di notifiche push standard.</span><span class="sxs-lookup"><span data-stu-id="18dd2-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="18dd2-111">In questa esercitazione viene descritto come conseguire la stessa esperienza inviando informazioni sensibili attraverso una connessione autenticata e sicura tra il dispositivo client e il back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="18dd2-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="18dd2-112">A livello generale, il flusso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="18dd2-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="18dd2-113">Il back-end dell'app:</span><span class="sxs-lookup"><span data-stu-id="18dd2-113">The app back-end:</span></span>
   * <span data-ttu-id="18dd2-114">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="18dd2-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="18dd2-115">Invia l'ID di questa notifica al dispositivo (non vengono inviate informazioni sicure).</span><span class="sxs-lookup"><span data-stu-id="18dd2-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="18dd2-116">L'app sul dispositivo, quando riceve la notifica:</span><span class="sxs-lookup"><span data-stu-id="18dd2-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="18dd2-117">Il dispositivo contatta il back-end richiedendo il payload sicuro.</span><span class="sxs-lookup"><span data-stu-id="18dd2-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="18dd2-118">L'app può indicare il payload come una notifica sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="18dd2-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="18dd2-119">È importante notare che nel flusso precedente e in questa esercitazione si presuppone che il dispositivo archivi un token di autenticazione nella memoria locale, dopo l’accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="18dd2-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="18dd2-120">Ciò garantisce un'esperienza completamente lineare, in quanto il dispositivo può recuperare il payload sicuro della notifica tramite questo token.</span><span class="sxs-lookup"><span data-stu-id="18dd2-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="18dd2-121">Se invece l'applicazione non archivia i token di autenticazione nel dispositivo o se questi hanno una scadenza, l'app per dispositivo, alla ricezione della notifica, dovrà visualizzare una notifica generica in cui si richiede all'utente di avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="18dd2-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="18dd2-122">L'app autentica quindi l'utente e mostra il payload di notifica.</span><span class="sxs-lookup"><span data-stu-id="18dd2-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="18dd2-123">In questa esercitazione sul push sicuro viene illustrato come inviare una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="18dd2-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="18dd2-124">Poiché i passaggi qui descritti si basano sull'esercitazione [Utilizzo di Hub di notifica per inviare notifiche agli utenti](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) , sarà prima necessario completare i passaggi di quest'ultima.</span><span class="sxs-lookup"><span data-stu-id="18dd2-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="18dd2-125">Questa esercitazione presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="18dd2-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="18dd2-126">Si noti inoltre che Windows Phone 8.1 richiede le credenziali di Windows (non di Windows Phone) e che le attività in background non funzionano in Windows Phone 8.0 o Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="18dd2-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="18dd2-127">Per le applicazioni per Windows Store, è possibile ricevere le notifiche tramite un'attività in background solo se per l'app è abilitata la schermata di blocco (fare clic sulla casella di controllo nel manifesto dell'app).</span><span class="sxs-lookup"><span data-stu-id="18dd2-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="18dd2-128">Modificare il progetto dell'app di Windows Phone</span><span class="sxs-lookup"><span data-stu-id="18dd2-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="18dd2-129">Nel progetto **NotifyUserWindowsPhone** aggiungere il codice seguente al file App.xaml.cs per registrare l'attività di push in background.</span><span class="sxs-lookup"><span data-stu-id="18dd2-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="18dd2-130">Aggiungere la seguente riga di codice alla fine del metodo `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="18dd2-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="18dd2-131">Sempre nel file App.xaml.cs aggiungere il seguente codice immediatamente dopo il metodo `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="18dd2-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="18dd2-132">Aggiungere le seguenti istruzioni `using` all'inizio del file App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="18dd2-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="18dd2-133">Scegliere **Salva tutto** dal menu **File** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18dd2-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="18dd2-134">Creare il componente push in background</span><span class="sxs-lookup"><span data-stu-id="18dd2-134">Create the Push Background Component</span></span>
<span data-ttu-id="18dd2-135">Il passaggio successivo consiste nella creazione del componente push in background.</span><span class="sxs-lookup"><span data-stu-id="18dd2-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="18dd2-136">In Esplora soluzioni fare clic con il pulsante destro del mouse sul nodo di primo livello della soluzione (in questo caso **Solution SecurePush**), fare clic su **Aggiungi** e quindi su **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="18dd2-137">Espandere **Applicazioni Windows Store**, fare clic su **App di Windows Phone** e quindi su **Componente Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="18dd2-138">Assegnare al progetto il nome **PushBackgroundComponent** e quindi fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="18dd2-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="18dd2-139">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **PushBackgroundComponent (Windows Phone 8.1)**, quindi fare clic su **Aggiungi** e infine su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="18dd2-140">Assegnare alla nuova classe il nome **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="18dd2-141">Fare clic su **Aggiungi** per generare la classe.</span><span class="sxs-lookup"><span data-stu-id="18dd2-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="18dd2-142">Sostituire l'intero contenuto della definizione dello spazio dei nomi di **PushBackgroundComponent** con il seguente codice e sostituire il segnaposto `{back-end endpoint}` con l'endpoint back-end ottenuto durante la distribuzione del back-end:</span><span class="sxs-lookup"><span data-stu-id="18dd2-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="18dd2-143">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **PushBackgroundComponent (Windows Phone 8.1)**, quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="18dd2-144">Sul lato sinistro fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="18dd2-145">Nella **casella di ricerca** digitare **Client Http**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="18dd2-146">Nell'elenco dei risultati fare clic su **Librerie client HTTP Microsoft** e quindi su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="18dd2-147">Completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="18dd2-147">Complete the installation.</span></span>
9. <span data-ttu-id="18dd2-148">Di nuovo nella **casella di ricerca** di NuGet digitare **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="18dd2-149">Installare il pacchetto **Json.NET** e quindi chiudere la finestra di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="18dd2-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="18dd2-150">Aggiungere le seguenti istruzioni `using` all'inizio del file **PushBackgroundTask.cs** :</span><span class="sxs-lookup"><span data-stu-id="18dd2-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="18dd2-151">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** nella cartella del progetto **NotifyUserWindowsPhone (Windows Phone 8.1)**, quindi scegliere **Aggiungi riferimento...**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="18dd2-152">Nella finestra di dialogo Gestione riferimenti selezionare la casella di controllo accanto a **PushBackgroundComponent**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="18dd2-153">In Esplora soluzioni fare doppio clic sul file **Package.appxmanifest** nel progetto **NotifyUserWindowsPhone (Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="18dd2-154">In **Notifiche** impostare **Popup supportati** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="18dd2-155">Sempre nel file **Package.appxmanifest** fare clic sul menu **Dichiarazioni** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="18dd2-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="18dd2-156">Nell'elenco a discesa **Dichiarazioni disponibili** fare clic su **Attività di background** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="18dd2-157">In **Package.appxmanifest**, in **Proprietà** selezionare **Notifica Push**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="18dd2-158">Nel file **Package.appxmanifest**, in **Impostazioni app** digitare **PushBackgroundComponent.PushBackgroundTask** nel campo **Punto di ingresso**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="18dd2-159">Scegliere **Save All** (Salva tutto) nel menu **File**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="18dd2-160">Esecuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="18dd2-160">Run the Application</span></span>
<span data-ttu-id="18dd2-161">Per eseguire l'applicazione, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="18dd2-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="18dd2-162">In Visual Studio eseguire l'applicazione API Web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="18dd2-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="18dd2-163">Verrà visualizzata una pagina Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18dd2-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="18dd2-164">In Visual Studio eseguire l'app per Windows Phone **NotifyUserWindowsPhone (Windows Phone 8.1)** .</span><span class="sxs-lookup"><span data-stu-id="18dd2-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="18dd2-165">Verrà eseguito l'emulatore di Windows Phone e l'app verrà caricata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="18dd2-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="18dd2-166">Nell'interfaccia utente dell'app **NotifyUserWindowsPhone** immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="18dd2-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="18dd2-167">Può trattarsi di qualsiasi stringa, ma devono avere lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="18dd2-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="18dd2-168">Nell'interfaccia utente dell'app **NotifyUserWindowsPhone** fare clic su **Log in and register**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="18dd2-169">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="18dd2-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
