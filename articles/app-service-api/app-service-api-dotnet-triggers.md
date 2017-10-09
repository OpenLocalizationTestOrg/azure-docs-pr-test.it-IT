---
title: i trigger di app API del servizio aaaApp | Documenti Microsoft
description: Come tooimplement attivi in un'applicazione API in Azure App Service
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="a983b-103">Trigger delle app per le API del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a983b-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="a983b-104">Questa versione di hello articolo applica versione dello schema di tooAPI App 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="a983b-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="a983b-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a983b-105">Overview</span></span>
<span data-ttu-id="a983b-106">Questo articolo spiega come app tooimplement API attiva e utilizzarli da un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="a983b-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="a983b-107">Tutti i frammenti di codice hello in questo argomento vengono copiati dal hello [nell'esempio di codice App per le API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="a983b-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="a983b-108">Si noti che è necessario hello toodownload seguendo il pacchetto nuget per il codice hello in questo articolo di toobuild ed eseguire: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="a983b-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="a983b-109">Cosa sono i trigger delle app per le API?</span><span class="sxs-lookup"><span data-stu-id="a983b-109">What are API app triggers?</span></span>
<span data-ttu-id="a983b-110">È uno scenario comune per un toofire app API un evento in modo che i client di app per le API hello possono intraprendere l'azione appropriata hello nell'evento toohello di risposta.</span><span class="sxs-lookup"><span data-stu-id="a983b-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="a983b-111">Hello meccanismo API REST in base che supporta questo scenario viene chiamato un trigger di app di API.</span><span class="sxs-lookup"><span data-stu-id="a983b-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="a983b-112">Ad esempio, supponiamo che il codice client utilizza hello [Twitter API connettore app](../connectors/connectors-create-api-twitter.md) e il codice deve tooperform un'azione in base alle nuove TWEET contenenti parole specifiche.</span><span class="sxs-lookup"><span data-stu-id="a983b-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="a983b-113">In questo caso, è possibile impostare un toofacilitate trigger polling o di push questa esigenza.</span><span class="sxs-lookup"><span data-stu-id="a983b-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="a983b-114">Trigger di polling e trigger di push</span><span class="sxs-lookup"><span data-stu-id="a983b-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="a983b-115">Attualmente sono supportati due tipi di trigger:</span><span class="sxs-lookup"><span data-stu-id="a983b-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="a983b-116">Trigger di polling - Client esegue il polling app hello per le API per la notifica di un evento che è stata attivata</span><span class="sxs-lookup"><span data-stu-id="a983b-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="a983b-117">Trigger di push - Client riceve una notifica tramite app hello API quando viene generato un evento</span><span class="sxs-lookup"><span data-stu-id="a983b-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="a983b-118">Trigger di polling</span><span class="sxs-lookup"><span data-stu-id="a983b-118">Poll trigger</span></span>
<span data-ttu-id="a983b-119">Un trigger di polling viene implementato come un'API REST regolari e prevede toopoll relativo client (ad esempio un'app di logica) nella notifica tooget ordine.</span><span class="sxs-lookup"><span data-stu-id="a983b-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="a983b-120">Mentre il client hello può mantenere lo stato, i trigger di polling hello stesso è senza stato.</span><span class="sxs-lookup"><span data-stu-id="a983b-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="a983b-121">le seguenti informazioni riguardanti i pacchetti di richiesta e risposta hello Hello vengono illustrati alcuni aspetti chiave del contratto di hello polling trigger:</span><span class="sxs-lookup"><span data-stu-id="a983b-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="a983b-122">Richiesta</span><span class="sxs-lookup"><span data-stu-id="a983b-122">Request</span></span>
  * <span data-ttu-id="a983b-123">Metodo HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="a983b-123">HTTP method: GET</span></span>
  * <span data-ttu-id="a983b-124">parameters</span><span class="sxs-lookup"><span data-stu-id="a983b-124">Parameters</span></span>
    * <span data-ttu-id="a983b-125">Questo parametro facoltativo di triggerState - consente ai client toospecify il proprio stato in modo che i trigger di polling di hello correttamente è possibile decidere se tooreturn notifica o hello non in base a stato specificato.</span><span class="sxs-lookup"><span data-stu-id="a983b-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="a983b-126">Parametri specifici dell'API</span><span class="sxs-lookup"><span data-stu-id="a983b-126">API-specific parameters</span></span>
* <span data-ttu-id="a983b-127">Response</span><span class="sxs-lookup"><span data-stu-id="a983b-127">Response</span></span>
  * <span data-ttu-id="a983b-128">Codice di stato **200** - richiesta è valida e vi è una notifica da trigger hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="a983b-129">il contenuto di Hello della notifica hello sarà corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="a983b-130">Un'intestazione "Retry-After" in risposta hello indica che è necessario recuperare i dati di notifica aggiuntivo con una chiamata di richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="a983b-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="a983b-131">Codice di stato **202** : richiesta è valida, ma non è presente alcuna notifica nuovo da un trigger di hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="a983b-132">Codice di stato **4xx** : la richiesta non è valida.</span><span class="sxs-lookup"><span data-stu-id="a983b-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="a983b-133">client Hello non deve ripetere la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="a983b-134">Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo.</span><span class="sxs-lookup"><span data-stu-id="a983b-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="a983b-135">Hello client deve tentare nuovamente hello richieste.</span><span class="sxs-lookup"><span data-stu-id="a983b-135">hello client should retry hello request.</span></span>

<span data-ttu-id="a983b-136">Hello frammento di codice seguente è riportato un esempio di come un sondaggio tooimplement trigger.</span><span class="sxs-lookup"><span data-stu-id="a983b-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="a983b-137">attivare il polling di tootest, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a983b-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="a983b-138">Distribuire hello API App con un'impostazione di autenticazione di **pubblico anonimo**.</span><span class="sxs-lookup"><span data-stu-id="a983b-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="a983b-139">Chiamare hello **tocco** tootouch operazione un file.</span><span class="sxs-lookup"><span data-stu-id="a983b-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="a983b-140">Hello seguente immagine mostra una richiesta di esempio tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="a983b-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="a983b-141">![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="a983b-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="a983b-142">Chiamata hello polling trigger con hello **triggerState** parametro impostato tooa ora timbro precedente tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="a983b-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="a983b-143">Hello immagine seguente mostra la richiesta di esempio hello tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="a983b-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="a983b-144">![Chiamata del trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="a983b-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="a983b-145">Trigger di push</span><span class="sxs-lookup"><span data-stu-id="a983b-145">Push trigger</span></span>
<span data-ttu-id="a983b-146">Un trigger di push viene implementato come un'API REST regolari che effettua il push delle notifiche tooclients che hanno registrato toobe una notifica quando vengono generati eventi specifici.</span><span class="sxs-lookup"><span data-stu-id="a983b-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="a983b-147">le seguenti informazioni riguardanti i pacchetti di richiesta e risposta hello Hello vengono illustrati alcuni aspetti chiave del contratto di trigger push hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="a983b-148">Richiesta</span><span class="sxs-lookup"><span data-stu-id="a983b-148">Request</span></span>
  * <span data-ttu-id="a983b-149">Metodo HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="a983b-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="a983b-150">parameters</span><span class="sxs-lookup"><span data-stu-id="a983b-150">Parameters</span></span>
    * <span data-ttu-id="a983b-151">triggerId: obbligatorio - opaco stringa (ad esempio un GUID) che rappresenta hello registrazione di un trigger di push.</span><span class="sxs-lookup"><span data-stu-id="a983b-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="a983b-152">callbackUrl: obbligatorio - URL di hello callback tooinvoke quando viene generato l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="a983b-153">chiamata di Hello è una semplice chiamata HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a983b-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="a983b-154">Parametri specifici dell'API</span><span class="sxs-lookup"><span data-stu-id="a983b-154">API-specific parameters</span></span>
* <span data-ttu-id="a983b-155">Response</span><span class="sxs-lookup"><span data-stu-id="a983b-155">Response</span></span>
  * <span data-ttu-id="a983b-156">Codice di stato **200** -client tooregister richiesta ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="a983b-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="a983b-157">Codice di stato **4xx** : la richiesta non è valida.</span><span class="sxs-lookup"><span data-stu-id="a983b-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="a983b-158">client Hello non deve ripetere la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="a983b-159">Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo.</span><span class="sxs-lookup"><span data-stu-id="a983b-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="a983b-160">Hello client deve tentare nuovamente hello richieste.</span><span class="sxs-lookup"><span data-stu-id="a983b-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="a983b-161">Callback</span><span class="sxs-lookup"><span data-stu-id="a983b-161">Callback</span></span>
  * <span data-ttu-id="a983b-162">Metodo HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="a983b-162">HTTP method: POST</span></span>
  * <span data-ttu-id="a983b-163">Corpo della richiesta: contenuto della notifica.</span><span class="sxs-lookup"><span data-stu-id="a983b-163">Request body: Notification content.</span></span>

<span data-ttu-id="a983b-164">Hello seguente frammento di codice è riportato un esempio di come un push tooimplement trigger:</span><span class="sxs-lookup"><span data-stu-id="a983b-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="a983b-165">attivare il polling di tootest, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a983b-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="a983b-166">Distribuire hello API App con un'impostazione di autenticazione di **pubblico anonimo**.</span><span class="sxs-lookup"><span data-stu-id="a983b-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="a983b-167">Sfoglia troppo[http://requestb.in/](http://requestb.in/) toocreate un RequestBin che verrà utilizzata come l'URL callback.</span><span class="sxs-lookup"><span data-stu-id="a983b-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="a983b-168">Chiamare il trigger di push hello con un GUID come **triggerId** e hello RequestBin URL come **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="a983b-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="a983b-169">![Chiamata del trigger di push tramite Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="a983b-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="a983b-170">Chiamare hello **tocco** tootouch operazione un file.</span><span class="sxs-lookup"><span data-stu-id="a983b-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="a983b-171">Hello seguente immagine mostra una richiesta di esempio tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="a983b-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="a983b-172">![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="a983b-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="a983b-173">Controllo hello RequestBin tooconfirm che hello push trigger callback viene richiamato con l'output di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a983b-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="a983b-174">![Chiamare il trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="a983b-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="a983b-175">Descrivere i trigger nella definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="a983b-175">Describe triggers in API definition</span></span>
<span data-ttu-id="a983b-176">Dopo l'implementazione di trigger hello e distribuendo il tooAzure app API, passare toohello **di definizione dell'API** pannello nel portale di anteprima di Azure hello e si noterà che i trigger vengono riconosciuti automaticamente nell'interfaccia utente, che si basa sulle hello Hello definizione Swagger 2.0 API dell'applicazione hello API.</span><span class="sxs-lookup"><span data-stu-id="a983b-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Pannello Definizione API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="a983b-178">Se si fa clic hello **scaricare Swagger** pulsante e i file JSON hello aperto, si noterà toohello simile di risultati seguente:</span><span class="sxs-lookup"><span data-stu-id="a983b-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="a983b-179">proprietà di estensione Hello **x-ms-schedular-trigger** è come i trigger sono descritti nella definizione dell'API e viene aggiunta automaticamente dal gateway app hello API quando si richiede la definizione hello API tramite il gateway hello se hello richiesta tooone di Hello seguenti criteri.</span><span class="sxs-lookup"><span data-stu-id="a983b-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="a983b-180">È anche possibile aggiungere questa proprietà manualmente.</span><span class="sxs-lookup"><span data-stu-id="a983b-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="a983b-181">Trigger di polling</span><span class="sxs-lookup"><span data-stu-id="a983b-181">Poll trigger</span></span>
  * <span data-ttu-id="a983b-182">Se il metodo HTTP hello **ottenere**.</span><span class="sxs-lookup"><span data-stu-id="a983b-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="a983b-183">Se hello **operationId** proprietà contiene la stringa hello **trigger**.</span><span class="sxs-lookup"><span data-stu-id="a983b-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="a983b-184">Se hello **parametri** proprietà include un parametro con un **nome** impostata troppo**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="a983b-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="a983b-185">Trigger di push</span><span class="sxs-lookup"><span data-stu-id="a983b-185">Push trigger</span></span>
  * <span data-ttu-id="a983b-186">Se il metodo HTTP hello **inserire**.</span><span class="sxs-lookup"><span data-stu-id="a983b-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="a983b-187">Se hello **operationId** proprietà contiene la stringa hello **trigger**.</span><span class="sxs-lookup"><span data-stu-id="a983b-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="a983b-188">Se hello **parametri** proprietà include un parametro con un **nome** impostata troppo**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="a983b-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="a983b-189">Usare i trigger di app per le API nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="a983b-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="a983b-190">Elencare e configurare i trigger di app API nella finestra di progettazione di hello logica App</span><span class="sxs-lookup"><span data-stu-id="a983b-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="a983b-191">Se si crea un'app per la logica in hello app per le API di hello stesso gruppo di risorse, sarà in grado di tooadd è canvas di progettazione toohello semplicemente facendovi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="a983b-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="a983b-192">Hello seguenti immagini illustrare questo concetto:</span><span class="sxs-lookup"><span data-stu-id="a983b-192">hello following images illustrate this:</span></span>

![Trigger nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurazione del trigger di polling nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurazione del trigger di push nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="a983b-196">Ottimizzare i trigger di app per le API per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="a983b-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="a983b-197">Dopo aver aggiunto i trigger tooan API app, esistono alcuni aspetti, è possibile eseguire analisi hello tooimprove quando si utilizza l'applicazione hello API in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="a983b-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="a983b-198">Ad esempio, hello **triggerState** parametro per i trigger di polling deve essere impostato toohello espressione hello logica App seguente.</span><span class="sxs-lookup"><span data-stu-id="a983b-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="a983b-199">Questa espressione deve valutare l'ultima chiamata di hello del trigger hello dall'app logica hello e restituiscono tale valore.</span><span class="sxs-lookup"><span data-stu-id="a983b-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="a983b-200">Nota: Per una spiegazione delle funzioni hello utilizzate nell'espressione hello precedente, vedere la documentazione di toohello su [linguaggio di definizione del flusso di lavoro logica App](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="a983b-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="a983b-201">Logica app utenti devono espressione hello tooprovide sopra per hello **triggerState** parametro durante l'utilizzo di trigger hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="a983b-202">È possibile toohave questo valore predefinito dalla finestra di progettazione di hello logica app tramite proprietà di estensione hello **raccomandazione x-ms-utilità di pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="a983b-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="a983b-203">Hello **x-ms-visibilità** estensione può essere impostata tooa valore *interno* in modo che il parametro hello stesso non viene visualizzato nella finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="a983b-204">Hello frammento di codice seguente è illustrata il.</span><span class="sxs-lookup"><span data-stu-id="a983b-204">hello following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="a983b-205">Per i trigger di push, hello **triggerId** parametro deve identificare in modo univoco hello logica app.</span><span class="sxs-lookup"><span data-stu-id="a983b-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="a983b-206">Una procedura consigliata è tooset questo nome della proprietà toohello del flusso di lavoro hello utilizzando hello l'espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="a983b-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="a983b-207">Utilizzando hello **raccomandazione x-ms-utilità di pianificazione** e **x-ms-visibilità** possono trasmettere le proprietà di estensione nella relativa definizione API, hello app per le API toohello logica app progettazione tooautomatically impostare espressione per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="a983b-208">Aggiungere le proprietà di estensione nella definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="a983b-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="a983b-209">Informazioni aggiuntive sui metadati, ad esempio le proprietà di estensione hello **raccomandazione x-ms-utilità di pianificazione** e **x-ms-visibilità** -possono essere aggiunti nella definizione di hello API in uno dei due modi: statico o dinamico.</span><span class="sxs-lookup"><span data-stu-id="a983b-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="a983b-210">Per i metadati statici, è possibile modificare direttamente hello */metadata/apiDefinition.swagger.json* file nel progetto e aggiungere manualmente le proprietà di hello.</span><span class="sxs-lookup"><span data-stu-id="a983b-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="a983b-211">Per App per le API tramite i metadati dinamici, è possibile modificare hello SwaggerConfig.cs file tooadd un filtro di operazione che è possibile aggiungere queste estensioni.</span><span class="sxs-lookup"><span data-stu-id="a983b-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="a983b-212">Hello Ecco un esempio di come questa classe è possibile scenario di metadati dinamici hello toofacilitate implementato.</span><span class="sxs-lookup"><span data-stu-id="a983b-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
