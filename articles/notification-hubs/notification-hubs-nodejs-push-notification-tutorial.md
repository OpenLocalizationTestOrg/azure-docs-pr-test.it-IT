---
title: Invio di notifiche push con Hub di notifica di Azure e Node.js
description: Informazioni su come usare Hub di notifica per inviare notifiche push da un'applicazione Node.js.
keywords: notifica push,notifiche push,push node.js,push ios
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="e684d-104">Invio di notifiche push con Hub di notifica di Azure e Node.js</span><span class="sxs-lookup"><span data-stu-id="e684d-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="e684d-105">Overview</span><span class="sxs-lookup"><span data-stu-id="e684d-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e684d-106">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="e684d-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e684d-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e684d-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e684d-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="e684d-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="e684d-109">Questa guida illustra come inviare notifiche push con Hub di notifica di Azure direttamente da un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="e684d-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="e684d-110">Gli scenari presentati includono l'invio di notifiche push ad applicazioni nelle piattaforme seguenti:</span><span class="sxs-lookup"><span data-stu-id="e684d-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="e684d-111">Android</span><span class="sxs-lookup"><span data-stu-id="e684d-111">Android</span></span>
* <span data-ttu-id="e684d-112">iOS</span><span class="sxs-lookup"><span data-stu-id="e684d-112">iOS</span></span>
* <span data-ttu-id="e684d-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e684d-113">Windows Phone</span></span>
* <span data-ttu-id="e684d-114">Piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="e684d-114">Universal Windows Platform</span></span> 

<span data-ttu-id="e684d-115">Per ulteriori informazioni sugli hub di notifica, vedere la sezione [Passaggi successivi](#next) .</span><span class="sxs-lookup"><span data-stu-id="e684d-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="e684d-116">Informazioni su Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="e684d-116">What are Notification Hubs?</span></span>
<span data-ttu-id="e684d-117">Hub di notifica di Azure offre un'infrastruttura scalabile, multipiattaforma e di semplice utilizzo per l'invio di notifiche push ai dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e684d-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="e684d-118">Per informazioni dettagliate sull'infrastruttura del servizio, vedere la pagina [Hub di notifica di Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e684d-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="e684d-119">Creazione di un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="e684d-119">Create a Node.js Application</span></span>
<span data-ttu-id="e684d-120">Il primo passaggio in questa esercitazione consiste nel creare una nuova applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="e684d-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="e684d-121">Per istruzioni sulla creazione di un'applicazione Node.js, vedere [Creare e distribuire un'applicazione Node.js in un sito Web di Azure][nodejswebsite], [Servizio cloud Node.js][Node.js Cloud Service] con Windows PowerShell o [Sito Web con WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="e684d-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="e684d-122">Configurare l'applicazione per l'uso di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="e684d-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="e684d-123">Per usare Hub di notifica di Azure, è necessario scaricare e usare il [pacchetto Azure](https://www.npmjs.com/package/azure)di Node.js, che comprende un set integrato di librerie di supporto che comunicano con i servizi REST di notifica push.</span><span class="sxs-lookup"><span data-stu-id="e684d-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="e684d-124">Usare Node Package Manager (NPM) per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="e684d-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="e684d-125">Usare un'interfaccia della riga di comando come **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Linux) e passare alla cartella in cui è stata creata l'applicazione vuota.</span><span class="sxs-lookup"><span data-stu-id="e684d-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="e684d-126">Digitare **npm install azure-sb** nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="e684d-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="e684d-127">È possibile eseguire manualmente il comando **ls** o **dir** per verificare che sia stata creata una cartella **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="e684d-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="e684d-128">All'interno di tale cartella trovare il pacchetto **azure** , che contiene le librerie necessarie per accedere a Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e684d-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e684d-129">Altre informazioni sull'installazione di NPM sono disponibili nel [blog NPM](http://blog.npmjs.org/post/85484771375/how-to-install-npm)ufficiale.</span><span class="sxs-lookup"><span data-stu-id="e684d-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="e684d-130">Importare il modulo</span><span class="sxs-lookup"><span data-stu-id="e684d-130">Import the module</span></span>
<span data-ttu-id="e684d-131">Utilizzando un editor di testo, aggiungere quanto segue nella parte superiore del file **server.js** dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="e684d-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="e684d-132">Configurare una connessione all'Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="e684d-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="e684d-133">L'oggetto **NotificationHubService** consente di lavorare con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e684d-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="e684d-134">Il codice seguente consente di creare un oggetto **NotificationHubService** per l'hub di notifica denominato **hubname**.</span><span class="sxs-lookup"><span data-stu-id="e684d-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="e684d-135">Aggiungerlo nella parte superiore del file **server.js** dopo l'istruzione per l'importazione del modulo azure:</span><span class="sxs-lookup"><span data-stu-id="e684d-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="e684d-136">Il valore **connectionstring** della connessione può essere recuperato dal [portale di Azure] seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e684d-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="e684d-137">Nel riquadro di spostamento a sinistra fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="e684d-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="e684d-138">Selezionare **Hub di notifica**e quindi individuare l'hub da utilizzare per l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e684d-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="e684d-139">Per informazioni sulla creazione di un nuovo hub di notifica, vedere l' [esercitazione introduttiva per Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="e684d-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="e684d-140">Selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="e684d-140">Select **Settings**.</span></span>
4. <span data-ttu-id="e684d-141">Fare clic su **Criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e684d-141">Click on **Access Policies**.</span></span> <span data-ttu-id="e684d-142">Verranno visualizzate la stringhe di connessione di accesso completo e condiviso.</span><span class="sxs-lookup"><span data-stu-id="e684d-142">You will see both shared and full access connection strings.</span></span>

![Portale di Azure - Hub di notifica](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="e684d-144">La stringa di connessione può essere recuperata anche usando il cmdlet **Get-AzureSbNamespace** specificato da [Azure PowerShell](/powershell/azureps-cmdlets-docs) o il comando **azure sb namespace show** con l'[interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e684d-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="e684d-145">Architettura generale</span><span class="sxs-lookup"><span data-stu-id="e684d-145">General architecture</span></span>
<span data-ttu-id="e684d-146">L'oggetto **NotificationHubService** espone le istanze seguenti dell'oggetto per l'invio di notifiche push a specifici dispositivi e specifiche applicazioni:</span><span class="sxs-lookup"><span data-stu-id="e684d-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="e684d-147">**Android**: usare l'oggetto **GcmService**, disponibile in **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="e684d-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="e684d-148">**iOS**: usare l'oggetto **ApnsService**, accessibile in **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="e684d-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="e684d-149">**Windows Phone**: usare l'oggetto **MpnsService**, disponibile in **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="e684d-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="e684d-150">**Piattaforma UWP (Universal Windows Platform)**: usare l'oggetto **WnsService** disponibile in **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="e684d-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="e684d-151">Procedura: Inviare notifiche push ad applicazioni Android</span><span class="sxs-lookup"><span data-stu-id="e684d-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="e684d-152">L’oggetto **GcmService** specifica un metodo **send** che è possibile usare per inviare notifiche push alle applicazioni Android.</span><span class="sxs-lookup"><span data-stu-id="e684d-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="e684d-153">Di seguito sono illustrati i parametri accettati dal metodo **send** .</span><span class="sxs-lookup"><span data-stu-id="e684d-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="e684d-154">**Tags** : l'identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="e684d-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="e684d-155">Se non viene specificato alcun tag, la notifica verrà inviata a tutti i client.</span><span class="sxs-lookup"><span data-stu-id="e684d-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="e684d-156">**Payload** : il payload JSON o la stringa non elaborata del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e684d-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="e684d-157">**Callback** : la funzione di richiamata.</span><span class="sxs-lookup"><span data-stu-id="e684d-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="e684d-158">Per altre informazioni sul formato di payload, vedere la sezione **Payload** del documento relativo all' [implementazione del server GCM](http://developer.android.com/google/gcm/server.html#payload) .</span><span class="sxs-lookup"><span data-stu-id="e684d-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="e684d-159">Nel codice seguente viene usata l'istanza **GcmService** esposta dall'oggetto **NotificationHubService** per inviare una notifica push a tutti i client registrati.</span><span class="sxs-lookup"><span data-stu-id="e684d-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="e684d-160">Procedura: Inviare notifiche push ad applicazioni iOS</span><span class="sxs-lookup"><span data-stu-id="e684d-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="e684d-161">Come per le applicazioni Android descritte sopra, l'oggetto **ApnsService** specifica un metodo **send** che è possibile usare per inviare notifiche push alle applicazioni iOS.</span><span class="sxs-lookup"><span data-stu-id="e684d-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="e684d-162">Di seguito sono illustrati i parametri accettati dal metodo **send** .</span><span class="sxs-lookup"><span data-stu-id="e684d-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="e684d-163">**Tags** : l'identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="e684d-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="e684d-164">Se non viene specificato alcun tag, la notifica verrà inviata a tutti i client.</span><span class="sxs-lookup"><span data-stu-id="e684d-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="e684d-165">**Payload** : il payload JSON o stringa del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e684d-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="e684d-166">**Callback** : la funzione di richiamata.</span><span class="sxs-lookup"><span data-stu-id="e684d-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="e684d-167">Per altre informazioni sul formato di payload, vedere la sezione relativa al **payload di notifica** nella [guida alla programmazione di notifiche push e locali](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) .</span><span class="sxs-lookup"><span data-stu-id="e684d-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="e684d-168">Nel codice seguente viene usata l'istanza **ApnsService** esposta dall'oggetto **NotificationHubService** per inviare un messaggio di avviso a tutti i client:</span><span class="sxs-lookup"><span data-stu-id="e684d-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="e684d-169">Procedura: Inviare notifiche push ad applicazioni Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e684d-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="e684d-170">L'oggetto **MpnsService** specifica un metodo **send** che è possibile usare per inviare notifiche push alle applicazioni Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e684d-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="e684d-171">Di seguito sono illustrati i parametri accettati dal metodo **send** .</span><span class="sxs-lookup"><span data-stu-id="e684d-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="e684d-172">**Tags** : l'identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="e684d-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="e684d-173">Se non viene specificato alcun tag, la notifica verrà inviata a tutti i client.</span><span class="sxs-lookup"><span data-stu-id="e684d-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="e684d-174">**Payload** : il payload XML del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e684d-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="e684d-175">**TargetName** - `toast` per le notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="e684d-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="e684d-176">`token` per le notifiche di tipo riquadro.</span><span class="sxs-lookup"><span data-stu-id="e684d-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="e684d-177">**NotificationClass** : la priorità della notifica.</span><span class="sxs-lookup"><span data-stu-id="e684d-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="e684d-178">Per i valori validi, vedere la sezione relativa agli **elementi dell'intestazione HTTP** nel documento sul [push di notifiche da un server](http://msdn.microsoft.com/library/hh221551.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e684d-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="e684d-179">**Options** : intestazioni delle richieste facoltative.</span><span class="sxs-lookup"><span data-stu-id="e684d-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="e684d-180">**Callback** : la funzione di richiamata.</span><span class="sxs-lookup"><span data-stu-id="e684d-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="e684d-181">Per un elenco dei valori validi per **TargetName**, **NotificationClass** e le opzioni di intestazione, vedere la pagina [Pushing Notifications from a Server](http://msdn.microsoft.com/library/hh221551.aspx) (Notifiche push da server).</span><span class="sxs-lookup"><span data-stu-id="e684d-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="e684d-182">Nel codice di esempio seguente viene usata l'istanza **MpnsService** esposta dall'oggetto **NotificationHubService** per inviare una notifica push di tipo avviso popup:</span><span class="sxs-lookup"><span data-stu-id="e684d-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="e684d-183">Procedura: Inviare notifiche push alle applicazioni della piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="e684d-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="e684d-184">L'oggetto **WnsService** specifica un metodo **send** che è possibile usare per inviare notifiche push alle applicazioni della piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="e684d-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="e684d-185">Di seguito sono illustrati i parametri accettati dal metodo **send** .</span><span class="sxs-lookup"><span data-stu-id="e684d-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="e684d-186">**Tags** : l'identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="e684d-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="e684d-187">Se non viene specificato alcun tag, la notifica verrà inviata a tutti i client registrati.</span><span class="sxs-lookup"><span data-stu-id="e684d-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="e684d-188">**Payload** : il payload XML del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e684d-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="e684d-189">**Type** : il tipo di notifica.</span><span class="sxs-lookup"><span data-stu-id="e684d-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="e684d-190">**Options** : intestazioni delle richieste facoltative.</span><span class="sxs-lookup"><span data-stu-id="e684d-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="e684d-191">**Callback** : la funzione di richiamata.</span><span class="sxs-lookup"><span data-stu-id="e684d-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="e684d-192">Per un elenco dei valori validi per i tipi e le intestazioni delle richieste, vedere [Intestazioni delle richieste e delle risposte per il servizio di notifica push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="e684d-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="e684d-193">Nel codice seguente viene usata l'istanza **WnsService** esposta dall'oggetto **NotificationHubService** per inviare una notifica push di tipo avviso popup a un'app UWP:</span><span class="sxs-lookup"><span data-stu-id="e684d-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="e684d-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e684d-194">Next Steps</span></span>
<span data-ttu-id="e684d-195">I frammenti di codice di esempio riportati sopra consentono di creare facilmente l'infrastruttura del servizio per recapitare notifiche push a un'ampia gamma di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e684d-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="e684d-196">A questo punto, dopo aver appreso le nozioni di base dell'uso di Hub di notifica con Node.js, usare i collegamenti seguenti per scoprire come estendere ulteriormente queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e684d-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="e684d-197">Vedere la documentazione MSDN su [Hub di notifica di Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="e684d-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="e684d-198">Visitare il repository [Azure SDK for Node] su GitHub per altri esempi e dettagli relativi all'implementazione.</span><span class="sxs-lookup"><span data-stu-id="e684d-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="e684d-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="e684d-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
<span data-ttu-id="e684d-200">[Sito Web con WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="e684d-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="e684d-201">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e684d-201">[Azure Portal]: https://portal.azure.com</span></span>
