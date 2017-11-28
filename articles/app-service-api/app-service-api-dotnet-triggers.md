---
title: Trigger delle app per le API del servizio app | Documentazione Microsoft
description: Come implementare i trigger in un'app per le API in Servizio app di Azure.
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
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="903e5-103">Trigger delle app per le API del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="903e5-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="903e5-104">Questa versione dell'articolo si applica alla versione dello schema 2014-12-01-preview delle app per le API.</span><span class="sxs-lookup"><span data-stu-id="903e5-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="903e5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="903e5-105">Overview</span></span>
<span data-ttu-id="903e5-106">Questo articolo spiega come implementare i trigger delle app per le API e usarli da un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="903e5-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="903e5-107">Tutti i frammenti di codice in questo argomento sono stati copiati dall' [esempio di codice di app per le API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="903e5-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="903e5-108">Per la corretta compilazione ed esecuzione del codice riportato in questo articolo, sarà inoltre necessario scaricare il pacchetto NuGet seguente: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="903e5-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="903e5-109">Cosa sono i trigger delle app per le API?</span><span class="sxs-lookup"><span data-stu-id="903e5-109">What are API app triggers?</span></span>
<span data-ttu-id="903e5-110">In genere, le app per le API generano eventi in modo che i client dell'app per le API possano eseguire l'azione appropriata in risposta all'evento.</span><span class="sxs-lookup"><span data-stu-id="903e5-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="903e5-111">Il meccanismo basato sull'API REST che supporta questo scenario è definito come trigger dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="903e5-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="903e5-112">Si supponga, ad esempio, che il codice client usi l' [app per le API Twitter Connector](../connectors/connectors-create-api-twitter.md) e che il codice debba eseguire un'azione in base ai nuovi tweet che contengono parole specifiche.</span><span class="sxs-lookup"><span data-stu-id="903e5-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="903e5-113">In questo caso, è possibile configurare un trigger di polling o di push.</span><span class="sxs-lookup"><span data-stu-id="903e5-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="903e5-114">Trigger di polling e trigger di push</span><span class="sxs-lookup"><span data-stu-id="903e5-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="903e5-115">Attualmente sono supportati due tipi di trigger:</span><span class="sxs-lookup"><span data-stu-id="903e5-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="903e5-116">Trigger di polling: il client esegue il polling dell'app per le API per la notifica di un evento generato</span><span class="sxs-lookup"><span data-stu-id="903e5-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="903e5-117">Trigger di push: il client riceve una notifica dall'app per le API quando viene generato un evento</span><span class="sxs-lookup"><span data-stu-id="903e5-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="903e5-118">Trigger di polling</span><span class="sxs-lookup"><span data-stu-id="903e5-118">Poll trigger</span></span>
<span data-ttu-id="903e5-119">Un trigger di polling viene implementato come un'API REST normale e prevede che i client, ad esempio un'app per la logica, ne eseguano il polling per ricevere la notifica.</span><span class="sxs-lookup"><span data-stu-id="903e5-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="903e5-120">Mentre il client può mantenere il suo stato, il trigger di polling stesso è senza stato.</span><span class="sxs-lookup"><span data-stu-id="903e5-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="903e5-121">Le informazioni seguenti relative ai pacchetti di richiesta e di risposta illustrano alcuni aspetti fondamentali del contratto del trigger di polling:</span><span class="sxs-lookup"><span data-stu-id="903e5-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="903e5-122">Richiesta</span><span class="sxs-lookup"><span data-stu-id="903e5-122">Request</span></span>
  * <span data-ttu-id="903e5-123">Metodo HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="903e5-123">HTTP method: GET</span></span>
  * <span data-ttu-id="903e5-124">Parametri</span><span class="sxs-lookup"><span data-stu-id="903e5-124">Parameters</span></span>
    * <span data-ttu-id="903e5-125">triggerState: questo parametro facoltativo consente ai client di specificare il proprio stato in modo che il trigger di polling possa decidere correttamente se restituire o meno una notifica in base allo stato specificato.</span><span class="sxs-lookup"><span data-stu-id="903e5-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="903e5-126">Parametri specifici dell'API</span><span class="sxs-lookup"><span data-stu-id="903e5-126">API-specific parameters</span></span>
* <span data-ttu-id="903e5-127">Response</span><span class="sxs-lookup"><span data-stu-id="903e5-127">Response</span></span>
  * <span data-ttu-id="903e5-128">Codice di stato **200** : la richiesta è valida ed è presente una notifica dal trigger.</span><span class="sxs-lookup"><span data-stu-id="903e5-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="903e5-129">Il contenuto della notifica si troverà nel corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="903e5-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="903e5-130">Un'intestazione "Retry-After" nella risposta indica che è necessario recuperare i dati della notifica aggiuntivi con una chiamata di richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="903e5-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="903e5-131">Codice di stato **202** : la richiesta è valida ma non sono presenti nuove notifiche dal trigger.</span><span class="sxs-lookup"><span data-stu-id="903e5-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="903e5-132">Codice di stato **4xx** : la richiesta non è valida.</span><span class="sxs-lookup"><span data-stu-id="903e5-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="903e5-133">Il client non deve ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="903e5-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="903e5-134">Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo.</span><span class="sxs-lookup"><span data-stu-id="903e5-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="903e5-135">Il client deve ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="903e5-135">The client should retry the request.</span></span>

<span data-ttu-id="903e5-136">Il frammento di codice seguente descrive come implementare un trigger di polling.</span><span class="sxs-lookup"><span data-stu-id="903e5-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="903e5-137">Per testare il trigger di polling, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="903e5-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="903e5-138">Distribuire l'app per le API impostando l'autenticazione sul livello di accesso **Pubblico (anonimo)**.</span><span class="sxs-lookup"><span data-stu-id="903e5-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="903e5-139">Chiamare l'operazione **touch** per creare un file.</span><span class="sxs-lookup"><span data-stu-id="903e5-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="903e5-140">L'immagine seguente illustra una richiesta di esempio tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="903e5-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="903e5-141">![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="903e5-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="903e5-142">Chiamare il trigger di polling con il parametro **triggerState** impostato su un timestamp prima di procedere al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="903e5-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="903e5-143">L'immagine seguente illustra la richiesta di esempio tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="903e5-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="903e5-144">![Chiamata del trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="903e5-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="903e5-145">Trigger di push</span><span class="sxs-lookup"><span data-stu-id="903e5-145">Push trigger</span></span>
<span data-ttu-id="903e5-146">Un trigger di push viene implementato come un'API REST normale che esegue il push delle notifiche ai client registrati per ricevere una notifica quando vengono generati eventi specifici.</span><span class="sxs-lookup"><span data-stu-id="903e5-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="903e5-147">Le informazioni seguenti relative ai pacchetti di richiesta e di risposta illustrano alcuni aspetti fondamentali del contratto del trigger di push:</span><span class="sxs-lookup"><span data-stu-id="903e5-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="903e5-148">Richiesta</span><span class="sxs-lookup"><span data-stu-id="903e5-148">Request</span></span>
  * <span data-ttu-id="903e5-149">Metodo HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="903e5-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="903e5-150">Parametri</span><span class="sxs-lookup"><span data-stu-id="903e5-150">Parameters</span></span>
    * <span data-ttu-id="903e5-151">triggerId: obbligatorio. Si tratta di una stringa opaca (ad esempio un GUID) che rappresenta la registrazione di un trigger di push.</span><span class="sxs-lookup"><span data-stu-id="903e5-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="903e5-152">callbackUrl: obbligatorio. Si tratta dell'URL del callback da richiamare quando viene generato l'evento.</span><span class="sxs-lookup"><span data-stu-id="903e5-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="903e5-153">La chiamata è una semplice chiamata HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="903e5-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="903e5-154">Parametri specifici dell'API</span><span class="sxs-lookup"><span data-stu-id="903e5-154">API-specific parameters</span></span>
* <span data-ttu-id="903e5-155">Response</span><span class="sxs-lookup"><span data-stu-id="903e5-155">Response</span></span>
  * <span data-ttu-id="903e5-156">Codice di stato **200** : la richiesta di registrazione del client è riuscita.</span><span class="sxs-lookup"><span data-stu-id="903e5-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="903e5-157">Codice di stato **4xx** : la richiesta non è valida.</span><span class="sxs-lookup"><span data-stu-id="903e5-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="903e5-158">Il client non deve ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="903e5-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="903e5-159">Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo.</span><span class="sxs-lookup"><span data-stu-id="903e5-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="903e5-160">Il client deve ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="903e5-160">The client should retry the request.</span></span>
* <span data-ttu-id="903e5-161">Callback</span><span class="sxs-lookup"><span data-stu-id="903e5-161">Callback</span></span>
  * <span data-ttu-id="903e5-162">Metodo HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="903e5-162">HTTP method: POST</span></span>
  * <span data-ttu-id="903e5-163">Corpo della richiesta: contenuto della notifica.</span><span class="sxs-lookup"><span data-stu-id="903e5-163">Request body: Notification content.</span></span>

<span data-ttu-id="903e5-164">Il frammento di codice seguente descrive come implementare un trigger di push:</span><span class="sxs-lookup"><span data-stu-id="903e5-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
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
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="903e5-165">Per testare il trigger di polling, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="903e5-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="903e5-166">Distribuire l'app per le API impostando l'autenticazione sul livello di accesso **Pubblico (anonimo)**.</span><span class="sxs-lookup"><span data-stu-id="903e5-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="903e5-167">Passare a [http://requestb.in/](http://requestb.in/) per creare un oggetto RequestBin da usare come URL di callback.</span><span class="sxs-lookup"><span data-stu-id="903e5-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="903e5-168">Chiamare il trigger di push con un GUID come **triggerId** e un URL RequestBin come **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="903e5-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="903e5-169">![Chiamata del trigger di push tramite Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="903e5-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="903e5-170">Chiamare l'operazione **touch** per creare un file.</span><span class="sxs-lookup"><span data-stu-id="903e5-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="903e5-171">L'immagine seguente illustra una richiesta di esempio tramite Postman.</span><span class="sxs-lookup"><span data-stu-id="903e5-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="903e5-172">![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="903e5-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="903e5-173">Controllare l'oggetto RequestBin per assicurarsi che il callback del trigger di push venga richiamato con l'output delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="903e5-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="903e5-174">![Chiamare il trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="903e5-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="903e5-175">Descrivere i trigger nella definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="903e5-175">Describe triggers in API definition</span></span>
<span data-ttu-id="903e5-176">Dopo aver implementato i trigger e distribuito l'app per le API in Azure, passare al pannello **Definizione API** nel portale di anteprima di Azure. Si noterà che i trigger vengono riconosciuti automaticamente nell'interfaccia utente che è basata sulla definizione API Swagger 2.0 dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="903e5-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Pannello Definizione API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="903e5-178">Se si fa clic sul pulsante **Scarica Swagger** e si apre il file JSON, verranno visualizzati risultati simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="903e5-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

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

<span data-ttu-id="903e5-179">La proprietà **x-ms-schedular-trigger** rappresenta il modo in cui i trigger sono descritti nella definizione dell'API e viene aggiunta automaticamente dal gateway dell'app per le API quando si richiede la definizione dell'API tramite il gateway, se la richiesta soddisfa uno dei criteri seguenti.</span><span class="sxs-lookup"><span data-stu-id="903e5-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="903e5-180">È anche possibile aggiungere questa proprietà manualmente.</span><span class="sxs-lookup"><span data-stu-id="903e5-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="903e5-181">Trigger di polling</span><span class="sxs-lookup"><span data-stu-id="903e5-181">Poll trigger</span></span>
  * <span data-ttu-id="903e5-182">Se il metodo HTTP è **GET**.</span><span class="sxs-lookup"><span data-stu-id="903e5-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="903e5-183">Se la proprietà **operationId** contiene la stringa **trigger**.</span><span class="sxs-lookup"><span data-stu-id="903e5-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="903e5-184">Se la proprietà **parameters** include un parametro con una proprietà **name** impostata su **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="903e5-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="903e5-185">Trigger di push</span><span class="sxs-lookup"><span data-stu-id="903e5-185">Push trigger</span></span>
  * <span data-ttu-id="903e5-186">Se il metodo HTTP è **PUT**.</span><span class="sxs-lookup"><span data-stu-id="903e5-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="903e5-187">Se la proprietà **operationId** contiene la stringa **trigger**.</span><span class="sxs-lookup"><span data-stu-id="903e5-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="903e5-188">Se la proprietà **parameters** include un parametro con una proprietà **name** impostata su **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="903e5-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="903e5-189">Usare i trigger di app per le API nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="903e5-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="903e5-190">Elencare e configurare i trigger di app per le API nella finestra di progettazione di app per la logica</span><span class="sxs-lookup"><span data-stu-id="903e5-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="903e5-191">Se si crea un'app per la logica nello stesso gruppo di risorse dell'app per le API, sarà possibile aggiungerla all'area di disegno della finestra di progettazione, semplicemente facendo clic su di essa.</span><span class="sxs-lookup"><span data-stu-id="903e5-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="903e5-192">Vedere le immagini seguenti per un esempio:</span><span class="sxs-lookup"><span data-stu-id="903e5-192">The following images illustrate this:</span></span>

![Trigger nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurazione del trigger di polling nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurazione del trigger di push nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="903e5-196">Ottimizzare i trigger di app per le API per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="903e5-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="903e5-197">Dopo aver aggiunto i trigger a un'app per le API, è possibile eseguire alcune operazioni per migliorare l'esperienza durante l'uso dell'app per le API in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="903e5-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="903e5-198">Ad esempio, impostare il parametro **triggerState** per i trigger di polling sull'espressione seguente nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="903e5-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="903e5-199">Questa espressione deve valutare l'ultima chiamata del trigger dall'app per la logica e restituire il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="903e5-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="903e5-200">NOTA: per una spiegazione delle funzioni usate nell'espressione precedente, fare riferimento alla documentazione relativa al [linguaggio di definizione del flusso di lavoro delle app per la logica](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="903e5-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="903e5-201">Gli utenti dell'app per la logica dovranno specificare l'espressione precedente per il parametro **triggerState** durante l'utilizzo del trigger.</span><span class="sxs-lookup"><span data-stu-id="903e5-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="903e5-202">Questo valore può essere impostato come predefinito dalla finestra di progettazione di app per la logica tramite la proprietà di estensione **x-ms-scheduler-recommendation**.</span><span class="sxs-lookup"><span data-stu-id="903e5-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="903e5-203">È possibile impostare la proprietà di estensione **x-ms-visibility** sul valore *internal* in modo che il parametro stesso non venga visualizzato nella finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="903e5-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="903e5-204">Questo scenario è mostrato nel frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="903e5-204">The following snippet illustrates that.</span></span>

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

<span data-ttu-id="903e5-205">Per i trigger di push, il parametro **triggerId** deve identificare in modo univoco l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="903e5-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="903e5-206">In base a una procedura consigliata, è opportuno impostare questa proprietà sul nome del flusso di lavoro tramite l'espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="903e5-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="903e5-207">Grazie all'uso delle proprietà di estensione **x-ms-scheduler-recommendation** e **x-ms-visibility** nella propria definizione API, l'app per le API può indicare alla finestra di progettazione dell'app per la logica di impostare automaticamente questa espressione.</span><span class="sxs-lookup"><span data-stu-id="903e5-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="903e5-208">Aggiungere le proprietà di estensione nella definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="903e5-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="903e5-209">Per aggiungere altre informazioni sui metadati, ad esempio le proprietà di estensione **x-ms-scheduler-recommendation** e **x-ms-visibility**, alla definizione dell'API sono disponibili due modi, uno statico e uno dinamico.</span><span class="sxs-lookup"><span data-stu-id="903e5-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="903e5-210">Per i metadati statici, è possibile modificare direttamente il file */metadata/apiDefinition.swagger.json* nel progetto e aggiungere manualmente le proprietà.</span><span class="sxs-lookup"><span data-stu-id="903e5-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="903e5-211">Per le app per le API che usano metadati dinamici, è possibile modificare il file SwaggerConfig.cs e aggiungervi un filtro per le operazioni in grado di aggiungere queste estensioni.</span><span class="sxs-lookup"><span data-stu-id="903e5-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="903e5-212">Di seguito è riportato un esempio di come è possibile implementare questa classe per semplificare lo scenario relativo ai metadati dinamici.</span><span class="sxs-lookup"><span data-stu-id="903e5-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
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
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
