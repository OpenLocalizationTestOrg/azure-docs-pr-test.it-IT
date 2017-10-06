---
title: aaaSending le notifiche push con hub di notifica di Azure e Node.js
description: Informazioni su come toouse gli hub di notifica toosend notifiche push da un'applicazione Node.js.
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
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="386f6-104">Invio di notifiche push con Hub di notifica di Azure e Node.js</span><span class="sxs-lookup"><span data-stu-id="386f6-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="386f6-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="386f6-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="386f6-106">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="386f6-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="386f6-107">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="386f6-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="386f6-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="386f6-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="386f6-109">Questa guida illustra come toosend notifiche con l'aiuto di hello Azure degli hub di notifica push direttamente da un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="386f6-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="386f6-110">scenari di Hello trattati includono l'invio di tooapplications notifiche push su hello seguenti piattaforme:</span><span class="sxs-lookup"><span data-stu-id="386f6-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="386f6-111">Android</span><span class="sxs-lookup"><span data-stu-id="386f6-111">Android</span></span>
* <span data-ttu-id="386f6-112">iOS</span><span class="sxs-lookup"><span data-stu-id="386f6-112">iOS</span></span>
* <span data-ttu-id="386f6-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="386f6-113">Windows Phone</span></span>
* <span data-ttu-id="386f6-114">Piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="386f6-114">Universal Windows Platform</span></span> 

<span data-ttu-id="386f6-115">Per ulteriori informazioni sull'hub di notifica, vedere hello [passaggi successivi](#next) sezione.</span><span class="sxs-lookup"><span data-stu-id="386f6-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="386f6-116">Informazioni su Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="386f6-116">What are Notification Hubs?</span></span>
<span data-ttu-id="386f6-117">Hub di notifica di Azure forniscono un'infrastruttura di facile utilizzo, multipiattaforma e scalabile per l'invio di dispositivi toomobile le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="386f6-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="386f6-118">Per informazioni dettagliate sull'infrastruttura del servizio hello, vedere hello [gli hub di notifica di Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="386f6-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="386f6-119">Creazione di un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="386f6-119">Create a Node.js Application</span></span>
<span data-ttu-id="386f6-120">passaggio prima di Hello in questa esercitazione consiste nel creare una nuova applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="386f6-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="386f6-121">Per istruzioni sulla creazione di un'applicazione Node.js, vedere [creare e distribuire un tooAzure di applicazione del sito Web Node.js][nodejswebsite], [servizio Cloud Node.js] [ Node.js Cloud Service] tramite Windows PowerShell, o [sito Web con WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="386f6-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="386f6-122">Configurare gli hub di notifica tooUse dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="386f6-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="386f6-123">toouse gli hub di notifica di Azure, è necessario toodownload e utilizzare hello Node.js [pacchetto azure](https://www.npmjs.com/package/azure), che include un set predefinito di librerie di supporto che comunicano con servizi REST di notifica push di hello.</span><span class="sxs-lookup"><span data-stu-id="386f6-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="386f6-124">Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="386f6-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="386f6-125">Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Linux) e passare toohello cartella in cui viene creata l'applicazione vuota .</span><span class="sxs-lookup"><span data-stu-id="386f6-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="386f6-126">Tipo **npm installare Service bus di azure** nella finestra di comando hello.</span><span class="sxs-lookup"><span data-stu-id="386f6-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="386f6-127">È possibile eseguire manualmente hello **ls** o **dir** comando tooverify che un **nodo\_moduli** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="386f6-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="386f6-128">All'interno di tale cartella, trovare hello **azure** pacchetto che contiene le librerie di hello necessarie tooaccess hello Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="386f6-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="386f6-129">Maggiori informazioni sull'installazione di NPM in ufficiale hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="386f6-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="386f6-130">Modulo di importazione hello</span><span class="sxs-lookup"><span data-stu-id="386f6-130">Import hello module</span></span>
<span data-ttu-id="386f6-131">Utilizzando un editor di testo aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="386f6-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="386f6-132">Configurare una connessione all'Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="386f6-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="386f6-133">Hello **NotificationHubService** oggetto consente di collaborare con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="386f6-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="386f6-134">Hello codice seguente viene creata una **NotificationHubService** oggetto per l'hub nofication hello denominato **hubname**.</span><span class="sxs-lookup"><span data-stu-id="386f6-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="386f6-135">Aggiungerlo parte superiore di hello di hello **server.js** file, dopo il modulo di hello istruzione tooimport hello azure:</span><span class="sxs-lookup"><span data-stu-id="386f6-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="386f6-136">Hello connessione **connectionstring** valore può essere ottenuto dalla hello [portale Azure] eseguendo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="386f6-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="386f6-137">Nel riquadro di spostamento a sinistra di hello, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="386f6-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="386f6-138">Selezionare **gli hub di notifica**e quindi hub hello trova desiderato toouse per esempio hello.</span><span class="sxs-lookup"><span data-stu-id="386f6-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="386f6-139">È possibile fare riferimento toohello [esercitazione Windows Store introduttiva](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se è necessario informazioni sulla creazione di un nuovo Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="386f6-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="386f6-140">Selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="386f6-140">Select **Settings**.</span></span>
4. <span data-ttu-id="386f6-141">Fare clic su **Criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="386f6-141">Click on **Access Policies**.</span></span> <span data-ttu-id="386f6-142">Verranno visualizzate la stringhe di connessione di accesso completo e condiviso.</span><span class="sxs-lookup"><span data-stu-id="386f6-142">You will see both shared and full access connection strings.</span></span>

![Portale di Azure - Hub di notifica](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="386f6-144">È inoltre possibile recuperare stringa di connessione di hello utilizzando hello **Get-AzureSbNamespace** cmdlet forniti da [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello **Mostra lo spazio dei nomi Service bus di azure** con Hello [interfaccia della riga di comando di Azure (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="386f6-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="386f6-145">Architettura generale</span><span class="sxs-lookup"><span data-stu-id="386f6-145">General architecture</span></span>
<span data-ttu-id="386f6-146">Hello **NotificationHubService** oggetto espone hello istanze dell'oggetto per l'invio di dispositivi toospecific di notifiche push e le applicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="386f6-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="386f6-147">**Android** -utilizzare hello **GcmService** oggetto, che è disponibile all'indirizzo **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="386f6-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="386f6-148">**iOS** -utilizzare hello **ApnsService** oggetto, che è possibile accedere al **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="386f6-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="386f6-149">**Windows Phone** -utilizzare hello **MpnsService** oggetto, che è disponibile all'indirizzo **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="386f6-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="386f6-150">**Piattaforma UWP** -utilizzare hello **WnsService** oggetto, che è disponibile all'indirizzo **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="386f6-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="386f6-151">Procedura: inviare le applicazioni di tooAndroid di notifiche push</span><span class="sxs-lookup"><span data-stu-id="386f6-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="386f6-152">Hello **GcmService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooAndroid applicazioni.</span><span class="sxs-lookup"><span data-stu-id="386f6-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="386f6-153">Hello **inviare** accetta hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="386f6-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="386f6-154">**Tag** -hello identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="386f6-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="386f6-155">Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.</span><span class="sxs-lookup"><span data-stu-id="386f6-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="386f6-156">**Payload** -hello JSON del messaggio o il payload di stringa non elaborata.</span><span class="sxs-lookup"><span data-stu-id="386f6-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="386f6-157">**Callback** -hello funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="386f6-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="386f6-158">Per ulteriori informazioni sul formato di payload hello, vedere hello **Payload** sezione di hello [implementazione Server GCM](http://developer.android.com/google/gcm/server.html#payload) documento.</span><span class="sxs-lookup"><span data-stu-id="386f6-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="386f6-159">Hello codice seguente viene utilizzato hello **GcmService** istanza esposto da hello **NotificationHubService** toosend un tooall di notifica push registrato i client.</span><span class="sxs-lookup"><span data-stu-id="386f6-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="386f6-160">Procedura: inviare le applicazioni di tooiOS di notifiche push</span><span class="sxs-lookup"><span data-stu-id="386f6-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="386f6-161">Stesso come descritta in precedenza, le applicazioni Android hello **ApnsService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooiOS applicazioni.</span><span class="sxs-lookup"><span data-stu-id="386f6-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="386f6-162">Hello **inviare** accetta hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="386f6-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="386f6-163">**Tag** -hello identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="386f6-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="386f6-164">Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.</span><span class="sxs-lookup"><span data-stu-id="386f6-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="386f6-165">**Payload** : hello JSON del messaggio o stringa payload.</span><span class="sxs-lookup"><span data-stu-id="386f6-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="386f6-166">**Callback** -hello funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="386f6-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="386f6-167">Per il formato di payload hello ulteriori informazioni, vedere hello **Payload di notifica** sezione di hello [locali e Guida per programmatori notifica Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.</span><span class="sxs-lookup"><span data-stu-id="386f6-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="386f6-168">Hello codice seguente viene utilizzato hello **ApnsService** istanza esposto da hello **NotificationHubService** toosend un avviso messaggio tooall client:</span><span class="sxs-lookup"><span data-stu-id="386f6-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="386f6-169">Procedura: inviare le applicazioni di Phone tooWindows di notifiche push</span><span class="sxs-lookup"><span data-stu-id="386f6-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="386f6-170">Hello **MpnsService** oggetto fornisce un **inviare** metodo che può essere utilizzato toosend push notifiche tooWindows applicazioni Phone.</span><span class="sxs-lookup"><span data-stu-id="386f6-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="386f6-171">Hello **inviare** accetta hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="386f6-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="386f6-172">**Tag** -hello identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="386f6-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="386f6-173">Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.</span><span class="sxs-lookup"><span data-stu-id="386f6-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="386f6-174">**Payload** -hello payload XML del messaggio.</span><span class="sxs-lookup"><span data-stu-id="386f6-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="386f6-175">**TargetName** - `toast` per le notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="386f6-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="386f6-176">`token` per le notifiche di tipo riquadro.</span><span class="sxs-lookup"><span data-stu-id="386f6-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="386f6-177">**Classe di notifica** -hello priorità della notifica hello.</span><span class="sxs-lookup"><span data-stu-id="386f6-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="386f6-178">Vedere hello **gli elementi dell'intestazione HTTP** sezione di hello [notifiche Push da un server](http://msdn.microsoft.com/library/hh221551.aspx) documento per i valori validi.</span><span class="sxs-lookup"><span data-stu-id="386f6-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="386f6-179">**Options** : intestazioni delle richieste facoltative.</span><span class="sxs-lookup"><span data-stu-id="386f6-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="386f6-180">**Callback** -hello funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="386f6-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="386f6-181">Per un elenco di valido **TargetName**, **della classe di notifica** e opzioni di intestazione, estrarre hello [notifiche Push da un server](http://msdn.microsoft.com/library/hh221551.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="386f6-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="386f6-182">Hello seguente codice di esempio utilizza hello **MpnsService** istanza esposto da hello **NotificationHubService** toosend una notifica push di tipo avviso popup:</span><span class="sxs-lookup"><span data-stu-id="386f6-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="386f6-183">Procedura: inviare le applicazioni di Windows Platform (UWP) tooUniversal di notifiche push</span><span class="sxs-lookup"><span data-stu-id="386f6-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="386f6-184">Hello **WnsService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooUniversal piattaforma Windows applicazioni.</span><span class="sxs-lookup"><span data-stu-id="386f6-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="386f6-185">Hello **inviare** accetta hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="386f6-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="386f6-186">**Tag** -hello identificatore tag.</span><span class="sxs-lookup"><span data-stu-id="386f6-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="386f6-187">Se non viene specificato alcun tag, verrà inviata notifica hello client tooall registrato.</span><span class="sxs-lookup"><span data-stu-id="386f6-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="386f6-188">**Payload** -payload del messaggio hello XML.</span><span class="sxs-lookup"><span data-stu-id="386f6-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="386f6-189">**Tipo** -hello tipo di notifica.</span><span class="sxs-lookup"><span data-stu-id="386f6-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="386f6-190">**Options** : intestazioni delle richieste facoltative.</span><span class="sxs-lookup"><span data-stu-id="386f6-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="386f6-191">**Callback** -hello funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="386f6-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="386f6-192">Per un elenco dei valori validi per i tipi e le intestazioni delle richieste, vedere [Intestazioni delle richieste e delle risposte per il servizio di notifica push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="386f6-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="386f6-193">Hello codice seguente viene utilizzato hello **WnsService** istanza esposto da hello **NotificationHubService** toosend un'app UWP tooa di tipo avviso popup push notifica:</span><span class="sxs-lookup"><span data-stu-id="386f6-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="386f6-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="386f6-194">Next Steps</span></span>
<span data-ttu-id="386f6-195">frammenti di esempio Hello precedenti consentono si tooeasily compilazione servizio infrastruttura toodeliver push notifiche tooa vasta gamma di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="386f6-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="386f6-196">Ora che si sono appreso nozioni fondamentali di hello dell'utilizzo degli hub di notifica con node.js, seguire questi toolearn collegamenti con informazioni su come è possibile estendere ulteriormente queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="386f6-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="386f6-197">Vedere hello riferimento MSDN per [gli hub di notifica di Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="386f6-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="386f6-198">Visitare hello [Azure SDK per nodo] repository in GitHub per ulteriori esempi e i dettagli di implementazione.</span><span class="sxs-lookup"><span data-stu-id="386f6-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK per nodo]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
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
[sito Web con WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[portale Azure]: https://portal.azure.com
