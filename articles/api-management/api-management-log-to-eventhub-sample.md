---
title: le API di gestione API di Azure, gli hub di eventi e Runscope aaaMonitor | Documenti Microsoft
description: Applicazione di esempio che illustra i criteri di log-a-eventhub hello connessione gestione API di Azure, gli hub di eventi di Azure e Runscope per HTTP di registrazione e monitoraggio
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="0e9e1-103">Monitorare le API con Gestione API di Azure, Hub eventi e Runscope</span><span class="sxs-lookup"><span data-stu-id="0e9e1-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="0e9e1-104">Hello [servizio Gestione API](api-management-key-concepts.md) fornisce molte funzionalità tooenhance hello elaborazione di HTTP le richieste inviate tooyour API HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="0e9e1-105">Hello, tuttavia, l'esistenza di hello richieste e risposte sono temporanee.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="0e9e1-106">viene richiesto di Hello e passano attraverso hello API Gestione servizio tooyour API back-end.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="0e9e1-107">L'API elabora la richiesta di hello e una risposta passa attraverso i consumer toohello API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="0e9e1-108">Servizio gestione API Hello mantiene alcune importanti statistiche sulle hello API per la visualizzazione nel dashboard del portale hello server di pubblicazione, ma che vanno oltre, dettagli hello non sono più disponibili.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="0e9e1-109">Utilizzando hello [log-a-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [criteri](api-management-howto-policies.md) nel servizio Gestione API hello è possibile inviare i dettagli da hello richiesta e risposta tooan [Hub di eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="0e9e1-110">Esistono diversi motivi per cui è possibile toogenerate eventi dai messaggi HTTP inviati tooyour API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="0e9e1-111">ad esempio per ottenere audit trail di aggiornamenti, analisi di utilizzo, avvisi relativi alle eccezioni e integrazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="0e9e1-112">In questo articolo viene illustrato come toocapture hello intera richiesta e risposta messaggio HTTP, inviarlo tooan Hub eventi e quindi tale servizio di terze parti di tooa messaggio che fornisce HTTP registrazione e monitoraggio dei servizi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="0e9e1-113">Vantaggi dell'invio dal servizio Gestione API</span><span class="sxs-lookup"><span data-stu-id="0e9e1-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="0e9e1-114">È possibile toowrite HTTP middleware che può collegare API HTTP Framework toocapture richieste e risposte HTTP e li feed in di registrazione e monitoraggio dei sistemi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="0e9e1-115">approccio di Hello svantaggio toothis è hello HTTP middleware deve toobe integrato nel back-end hello API e deve corrispondere a hello di hello API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="0e9e1-116">Se sono presenti più API ciascuno di essi deve distribuire hello middleware.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="0e9e1-117">Spesso non è possibile aggiornare le API back-end.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="0e9e1-118">Con l'infrastruttura di registrazione toointegrate servizio di gestione API di Azure hello offre una soluzione indipendente dalla piattaforma e centralizzata.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="0e9e1-119">È inoltre scalabile, in parte dovuto toohello [-replica geografica](api-management-howto-deploy-multi-region.md) funzionalità di gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="0e9e1-120">È possibile inviare tooan Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="0e9e1-121">È un tooask ragionevole, motivo per cui creare un criterio che è l'hub di eventi specifici tooAzure?</span><span class="sxs-lookup"><span data-stu-id="0e9e1-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="0e9e1-122">Esistono molte diverse posizioni in cui si desidera conoscere toolog richieste personali.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="0e9e1-123">Perché non è sufficiente inviare hello richiede direttamente la destinazione finale toohello?</span><span class="sxs-lookup"><span data-stu-id="0e9e1-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="0e9e1-124">è una delle opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-124">That is an option.</span></span> <span data-ttu-id="0e9e1-125">Tuttavia, quando si effettua le richieste di registrazione da un servizio Gestione API, è necessario tooconsider come messaggi di registrazione influirà sulle prestazioni di hello di hello API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="0e9e1-126">Gli incrementi graduali nel carico possono essere gestiti da istanze a disponibilità crescente dei componenti di sistema o sfruttando i vantaggi della replica geografica.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="0e9e1-127">Tuttavia, brevi picchi del traffico possono causare richieste toobe ritardato in modo significativo se infrastruttura toologging richieste avvia tooslow sotto carico.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="0e9e1-128">Hello hub eventi di Azure è progettato tooingress grandi volumi di dati, con capacità per la gestione di un numero superiore di eventi del numero di hello di HTTP richiede la maggior parte dei processo API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="0e9e1-129">Hello Hub eventi funge da un tipo di buffer sofisticate tra l'API del servizio e hello infrastruttura di gestione che verrà archiviata e l'elaborazione dei messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="0e9e1-130">In questo modo si garantisce che le prestazioni di API non subiranno scadenza toohello dell'infrastruttura di registrazione.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="0e9e1-131">Una volta passati tooan Hub di eventi è persistente e rimarrà in attesa di tooprocess consumer di Hub eventi, dati hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="0e9e1-132">Hello Hub eventi non è rilevante come verrà elaborata, semplicemente cuore assicurandosi che il messaggio hello verrà recapitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="0e9e1-133">Hub eventi sono i gruppi di consumer toomultiple hello possibilità toostream eventi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="0e9e1-134">In questo modo toobe eventi elaborati da sistemi completamente diversi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="0e9e1-135">In questo modo, che supporta numerosi scenari di integrazione senza inserire ritardi di addizione su hello l'elaborazione della richiesta API hello all'interno del servizio Gestione API di hello quando sono necessari per un solo evento toobe generato.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="0e9e1-136">Un messaggio di applicazione/http toosend criteri</span><span class="sxs-lookup"><span data-stu-id="0e9e1-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="0e9e1-137">Un hub eventi accetta i dati evento sotto forma di semplice stringa.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="0e9e1-138">contenuto Hello di tale stringa è completamente backup tooyou.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="0e9e1-139">toopackage in grado di toobe fino a una richiesta HTTP e inviarla off tooEvent hub dobbiamo stringa hello tooformat con le informazioni di richiesta o risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="0e9e1-140">In situazioni di questo tipo, se è presente un formato esistente, che è possibile riutilizzare, quindi potrebbe non essere toowrite nostro l'analisi codice.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="0e9e1-141">Inizialmente è considerato utilizzando hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) per l'invio di richieste e risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="0e9e1-142">ma questo formato è ottimizzato per l'archiviazione di una sequenza di richieste HTTP in un formato basato su JSON.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="0e9e1-143">Contiene un numero di elementi obbligatori che aggiungere complessità superflua per uno scenario di hello del passaggio di un messaggio hello HTTP rete hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="0e9e1-144">Stato di un'opzione alternativa hello toouse `application/http` tipo di supporto come descritto nella specifica HTTP hello [7230 RFC](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="0e9e1-145">Questo tipo di supporti utilizza hello esatta stesso formato di messaggi HTTP di trasmissione utilizzato tooactually rete hello, ma l'intero messaggio hello può essere inserito nel corpo di hello di un'altra richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="0e9e1-146">In questo caso ci limiteremo corpo hello toouse come nostro tooEvent toosend messaggio hub.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="0e9e1-147">Per praticità, è un parser che esiste nel [Client di Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) librerie che possono analizzare questo formato e convertirlo in hello nativo `HttpRequestMessage` e `HttpResponseMessage` oggetti.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="0e9e1-148">toocreate in grado di toobe questo messaggio è necessario tootake sfruttare basato su c# [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="0e9e1-149">Ecco i criteri di hello che invia un tooAzure messaggio di richiesta HTTP hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="0e9e1-150">Dichiarazione di criteri</span><span class="sxs-lookup"><span data-stu-id="0e9e1-150">Policy declaration</span></span>
<span data-ttu-id="0e9e1-151">È necessario evidenziare alcuni aspetti di questa espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="0e9e1-152">criteri di log-a-eventhub Hello ha un attributo denominato id logger che fa riferimento toohello nome del logger che è stato creato all'interno di hello servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="0e9e1-153">dettagli della modalità toosetup un logger di Hub eventi del servizio Gestione API hello è reperibile nel documento hello Hello [come toolog eventi tooAzure hub eventi in Gestione API di Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="0e9e1-154">secondo attributo Hello è un parametro facoltativo che indica a messaggi hello toostore partizione nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="0e9e1-155">Hub eventi utilizzare partizioni tooenable scalabilty e richiede un minimo di due.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="0e9e1-156">recapito ordinato dei messaggi Hello è garantito solo all'interno di una partizione.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="0e9e1-157">Se non si indicare l'Hub eventi in messaggi hello tooplace partizione, utilizza un carico di hello toodistribute algoritmo round-robin.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="0e9e1-158">Tuttavia, che può causare alcuni dei nostri toobe i messaggi elaborati nell'ordine errato.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="0e9e1-159">Partitions</span><span class="sxs-lookup"><span data-stu-id="0e9e1-159">Partitions</span></span>
<span data-ttu-id="0e9e1-160">tooensure i messaggi vengono recapitati tooconsumers in ordine e usufruire delle funzionalità di distribuzione hello carico delle partizioni, si è deciso di partizione di tooone i messaggi di richiesta di toosend HTTP e HTTP risposta messaggi tooa seconda partizione.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="0e9e1-161">In questo modo si assicurerà una distribuzione uniforme del carico e sarà possibile garantire che tutte le richieste e le risposte vengano utilizzate nell'ordine stabilito.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="0e9e1-162">È possibile che un toobe risposta utilizzati prima della richiesta di hello corrispondente, ma che non è un problema perché è un meccanismo diverso per la correlazione delle richieste tooresponses e sappiamo che le richieste provengano sempre prima le risposte.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="0e9e1-163">Payload HTTP</span><span class="sxs-lookup"><span data-stu-id="0e9e1-163">HTTP payloads</span></span>
<span data-ttu-id="0e9e1-164">Dopo la compilazione di hello `requestLine` controlliamo toosee se il corpo della richiesta hello deve essere troncato.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="0e9e1-165">corpo della richiesta Hello è troncato tooonly 1024.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="0e9e1-166">Questo può essere aumentato, tuttavia i singoli messaggi Hub eventi sono too256KB limitato, dunque è probabile che alcune HTTP corpi verrà non rientrano in un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="0e9e1-167">Quando si esegue una quantità significativa di informazioni di registrazione e analitica può essere derivata da solo riga di richiesta HTTP hello e intestazioni.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="0e9e1-168">Inoltre, molte richieste API restituiranno solo i corpi di piccole dimensioni e pertanto la perdita di hello del valore di informazioni troncando i corpi di grandi dimensioni è piuttosto minima riduzione toohello confronto trasferimento, l'elaborazione e archiviazione costi tookeep tutto il contenuto del corpo.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="0e9e1-169">Una nota finale sull'elaborazione testo hello è toopass `true` toohello come<string>metodo () perché venga letto contenuto del corpo hello, ma è anche desidera hello API back-end toobe tooread in grado di hello corpo.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="0e9e1-170">Passando il metodo toothis true è causare hello corpo toobe memorizzato nel buffer in modo che possa essere letto una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="0e9e1-171">Questo è importante toobe considerare se è disponibile un'API che non il caricamento di file di dimensioni molto grandi o utilizza polling lungo.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="0e9e1-172">In questi casi, sarebbe migliore tooavoid durante la lettura del corpo hello affatto.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="0e9e1-173">Intestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="0e9e1-173">HTTP headers</span></span>
<span data-ttu-id="0e9e1-174">Intestazioni HTTP possono semplicemente trasferite nel formato di messaggio hello in un formato di coppia chiave/valore semplice.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="0e9e1-175">Scelto toostrip out determinate sicurezza campi riservati, tooavoid inutilmente perdita di informazioni sulle credenziali.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="0e9e1-176">È poco probabile che le chiavi API e altre credenziali vengano usate per finalità analitiche.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="0e9e1-177">Se si desiderano toodo analisi per l'utente di hello e prodotto specifico hello in uso, quindi è stato possibile ottenere che da hello `context` e aggiungere tale messaggio toohello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="0e9e1-178">Metadati del messaggio</span><span class="sxs-lookup"><span data-stu-id="0e9e1-178">Message Metadata</span></span>
<span data-ttu-id="0e9e1-179">Quando si compila l'hub di eventi di hello messaggio completo toosend toohello prima riga hello non è parte effettiva di hello `application/http` messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="0e9e1-180">prima riga Hello è metadati aggiuntivi costituito se il messaggio hello è un messaggio di richiesta o risposta e un id di messaggio che è usato toocorrelate richiede tooresponses.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="0e9e1-181">id messaggio Hello viene creato utilizzando un altro criterio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0e9e1-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="0e9e1-182">Avremmo potuto creare messaggio di richiesta di hello, archiviato che in una variabile finché hello risposta è stata restituita e quindi semplicemente inviata hello richiesta e risposta come un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="0e9e1-183">Tuttavia, l'invio in modo indipendente, hello richiesta e risposta e utilizzando un toocorrelate id messaggio hello due, si ottiene una maggiore flessibilità per la dimensione del messaggio hello, hello possibilità tootake sfruttare più partizioni, mantenendo hello e ordine dei messaggi richiesta verrà visualizzato nel dashboard registrazione prima.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="0e9e1-184">Possono essere presenti anche alcuni scenari in cui una risposta valida non viene mai inviata hub eventi toohello, probabilmente a causa di errore irreversibile richiesta tooa nel servizio di gestione API hello, ma sarà ancora un record di richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="0e9e1-185">messaggio di Hello criteri toosend hello risposta HTTP esegue la ricerca richiesta toohello molto simili e pertanto hello completare la configurazione dei criteri è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0e9e1-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="0e9e1-186">Hello `set-variable` criteri creano un valore che sia accessibile da entrambi hello `log-to-eventhub` criteri in hello `<inbound>` sezione e hello `<outbound>` sezione.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="0e9e1-187">Ricezione di eventi dall'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e9e1-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="0e9e1-188">Gli eventi provenienti dall'Hub di eventi di Azure vengono ricevuti utilizzando hello [protocollo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="0e9e1-189">il team di Microsoft Service Bus Hello apportate client hello toomake disponibili librerie utilizzo di eventi più semplici.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="0e9e1-190">Esistono due approcci diversi è supportati, uno è in corso un *Consumer diretto* e altri hello utilizza hello `EventProcessorHost` classe.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="0e9e1-191">Esempi di questi due approcci sono disponibili in hello [Guida per programmatori hub eventi](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="0e9e1-192">versione breve di Hello delle differenze di hello è, `Direct Consumer` offre controllo completo e hello `EventProcessorHost` non le attività di plumbing hello per si ma su alcuni presupposti come elaborare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="0e9e1-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="0e9e1-193">EventProcessorHost</span></span>
<span data-ttu-id="0e9e1-194">In questo esempio, si utilizzerà hello `EventProcessorHost` per semplicità, tuttavia potrebbe non hello ottimale per questo particolare scenario.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="0e9e1-195">`EventProcessorHost`hello lavoro assicurandosi che non si dispone di tooworry informazioni sul threading problemi all'interno di una classe di evento specifico del processore.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="0e9e1-196">Tuttavia, in questo scenario, stiamo semplicemente la conversione del formato tooanother messaggi hello e passarlo lungo tooanother servizio utilizzando un metodo asincrono.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="0e9e1-197">Non è necessario aggiornare lo stato condiviso e quindi non si rischia che si verifichino problemi di threading.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="0e9e1-198">Per la maggior parte degli scenari, `EventProcessorHost` costituisce probabilmente la scelta ideale hello e è certamente l'opzione più semplice hello.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="0e9e1-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="0e9e1-199">IEventProcessor</span></span>
<span data-ttu-id="0e9e1-200">concetto fondamentale di Hello quando si utilizza `EventProcessorHost` è toocreate un un'implementazione di hello `IEventProcessor` interfaccia che contiene il metodo hello `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="0e9e1-201">le tracce di Hello di tale metodo sono illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="0e9e1-201">hello essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="0e9e1-202">Un elenco di oggetti EventData vengono passati nel metodo hello e abbiamo scorrere tale elenco.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="0e9e1-203">byte Hello di ogni metodo di analisi in un oggetto HttpMessage e tale oggetto viene passato l'istanza tooan IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="0e9e1-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="0e9e1-204">HttpMessage</span></span>
<span data-ttu-id="0e9e1-205">Hello `HttpMessage` istanza contiene tre tipi di dati:</span><span class="sxs-lookup"><span data-stu-id="0e9e1-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="0e9e1-206">Hello `HttpMessage` istanza contiene un `MessageId` GUID che consente di elaborare richieste hello HTTP tooconnect risposta HTTP corrispondente toohello e un valore booleano valore che indica se l'oggetto hello contiene un'istanza di un HttpRequestMessage e HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="0e9e1-207">Utilizzando hello compilato nelle classi HTTP da `System.Net.Http`, è stato in grado di tootake sfruttare hello `application/http` l'analisi del codice che è incluso in `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="0e9e1-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="0e9e1-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="0e9e1-209">Hello `HttpMessage` istanza viene quindi inoltrata tooimplementation di `IHttpMessageProcessor` che è un'interfaccia creato ricezione hello toodecouple e interpretazione degli eventi hello da Hub di eventi di Azure e hello effettivi l'elaborazione di esso.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="0e9e1-210">Inoltrare il messaggio hello HTTP</span><span class="sxs-lookup"><span data-stu-id="0e9e1-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="0e9e1-211">Per questo esempio, ho deciso sarebbe interessante toopush hello richiesta HTTP su troppo[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="0e9e1-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="0e9e1-212">Runscope è un servizio basato sul cloud specializzato nel debug, nella registrazione e nel monitoraggio HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="0e9e1-213">Hanno un livello gratuito, è facile tootry e consentirà le richieste HTTP di hello toosee nel flusso in tempo reale tramite il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="0e9e1-214">Hello `IHttpMessageProcessor` implementazione è simile al seguente,</span><span class="sxs-lookup"><span data-stu-id="0e9e1-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="0e9e1-215">È stato in grado di tootake sfruttare un [libreria client esistente per Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) che rende facile toopush `HttpRequestMessage` e `HttpResponseMessage` istanze backup nel proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="0e9e1-216">In ordine tooaccess hello API Runscope sarà necessario un account e una chiave API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="0e9e1-217">È possibile trovare istruzioni per ottenere una chiave API in hello [tooAccess la creazione di applicazioni API Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="0e9e1-218">Esempio completo</span><span class="sxs-lookup"><span data-stu-id="0e9e1-218">Complete sample</span></span>
<span data-ttu-id="0e9e1-219">Hello [codice sorgente](https://github.com/darrelmiller/ApimEventProcessor) e test dell'esempio hello sono su GitHub.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="0e9e1-220">È necessario un [servizio Gestione API](api-management-get-started.md), [un Hub eventi connesso](api-management-howto-log-event-hubs.md)e un [Account di archiviazione](../storage/common/storage-create-storage-account.md) toorun: esempio hello per se stessi.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="0e9e1-221">esempio Hello è sufficiente una semplice applicazione Console è in ascolto per gli eventi provenienti dall'Hub di eventi, li converte in un `HttpRequestMessage` e `HttpResponseMessage` oggetti e quindi li inoltra su toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="0e9e1-222">Nella seguente immagine animata di hello, è possibile visualizzare una richiesta effettuata tooan API nel portale per sviluppatori, messaggio hello hello Console dell'applicazione che mostra la ricezione di hello elaborati e inoltrati e quindi hello richiesta e risposta visualizzati in hello Runscope traffico controllo.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Dimostrazione della richiesta viene inoltrata tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="0e9e1-224">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0e9e1-224">Summary</span></span>
<span data-ttu-id="0e9e1-225">Servizio gestione API di Azure fornisce un traffico di hello HTTP toocapture ideale in viaggio tooand dalle API.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="0e9e1-226">Hub eventi di Azure è una soluzione a scalabilità elevata e costi ridotti per l'acquisizione e l'inserimento del traffico in sistemi di elaborazione secondari per operazioni di registrazione e monitoraggio e per altre analisi avanzate.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="0e9e1-227">Connessione a sistemi Runscope è un semplice come poche decine righe di codice di monitoraggio del traffico di terze parti too3rd.</span><span class="sxs-lookup"><span data-stu-id="0e9e1-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e9e1-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e9e1-228">Next steps</span></span>
* <span data-ttu-id="0e9e1-229">Altre informazioni sull'Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="0e9e1-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="0e9e1-230">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e9e1-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="0e9e1-231">Ricevere messaggi con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="0e9e1-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="0e9e1-232">Guida alla programmazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e9e1-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="0e9e1-233">Altre informazioni sull'integrazione di Gestione API e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0e9e1-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="0e9e1-234">Come toolog eventi tooAzure hub eventi in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="0e9e1-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="0e9e1-235">Informazioni di riferimento per l'entità logger</span><span class="sxs-lookup"><span data-stu-id="0e9e1-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="0e9e1-236">Informazioni di riferimento per i criteri log-to-event</span><span class="sxs-lookup"><span data-stu-id="0e9e1-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
