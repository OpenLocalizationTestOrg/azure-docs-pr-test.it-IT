---
title: Monitorare le API con Gestione API di Azure, Hub eventi e Runscope | Documentazione Microsoft
description: Applicazione di esempio che illustra il criterio log-to-eventhub con la connessione di Gestione API di Azure, Hub eventi di Azure e Runscope per operazioni di registrazione e monitoraggio HTTP
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
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="2c708-103">Monitorare le API con Gestione API di Azure, Hub eventi e Runscope</span><span class="sxs-lookup"><span data-stu-id="2c708-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="2c708-104">Il [servizio Gestione API](api-management-key-concepts.md) offre molte capacità per migliorare l'elaborazione di richieste HTTP inviate all'API HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c708-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="2c708-105">L'esistenza di richieste e risposte è tuttavia temporanea.</span><span class="sxs-lookup"><span data-stu-id="2c708-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="2c708-106">La richiesta viene effettuata e passa attraverso al servizio Gestione API fino all'API back-end.</span><span class="sxs-lookup"><span data-stu-id="2c708-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="2c708-107">L'API elabora la richiesta e una risposta viene restituita al consumer dell'API.</span><span class="sxs-lookup"><span data-stu-id="2c708-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="2c708-108">Il servizio Gestione API mantiene alcune statistiche importanti sulle API da visualizzare nel dashboard del portale di pubblicazione, ma eventuali altri dettagli verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="2c708-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="2c708-109">L'uso del [criterio](api-management-howto-policies.md) [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) nel servizio Gestione API consente di inviare eventuali dettagli dalla richiesta e dalla risposta a un [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2c708-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="2c708-110">È possibile che si voglia generare eventi dai messaggi HTTP inviati alle API per diversi motivi,</span><span class="sxs-lookup"><span data-stu-id="2c708-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="2c708-111">ad esempio per ottenere audit trail di aggiornamenti, analisi di utilizzo, avvisi relativi alle eccezioni e integrazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="2c708-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="2c708-112">Questo articolo illustra come acquisire l'intero messaggio di richiesta e risposta HTTP, inviarlo a un hub eventi e quindi inoltrare il messaggio a un servizio d terze parti che fornisce servizi di registrazione HTTP e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2c708-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="2c708-113">Vantaggi dell'invio dal servizio Gestione API</span><span class="sxs-lookup"><span data-stu-id="2c708-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="2c708-114">È possibile scrivere middleware HTTP in grado di collegarsi ai framework API HTTP per acquisire richieste e risposte HTTP e fornirle ai sistemi di registrazione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2c708-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="2c708-115">Lo svantaggio di questo approccio consiste nel fatto che il middleware HTTP deve essere integrato nell'API back-end e deve corrispondere alla piattaforma dell'API.</span><span class="sxs-lookup"><span data-stu-id="2c708-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="2c708-116">Se sono disponibili più API, ognuna dovrà distribuire il middleware.</span><span class="sxs-lookup"><span data-stu-id="2c708-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="2c708-117">Spesso non è possibile aggiornare le API back-end.</span><span class="sxs-lookup"><span data-stu-id="2c708-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="2c708-118">L'uso del servizio Gestione API di Azure per l'integrazione con l'infrastruttura di registrazione offre una soluzione centralizzata e indipendente dalla piattaforma,</span><span class="sxs-lookup"><span data-stu-id="2c708-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="2c708-119">oltre alla scalabilità, in parte grazie alla capacità di [replica geografica](api-management-howto-deploy-multi-region.md) di Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c708-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="2c708-120">Vantaggi dell'invio a un Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="2c708-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="2c708-121">È legittimo domandarsi quali siano i vantaggi della creazione di un criterio specifico dell'Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c708-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="2c708-122">È possibile registrare le richieste in molte posizione diverse.</span><span class="sxs-lookup"><span data-stu-id="2c708-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="2c708-123">L'invio delle richieste direttamente alla destinazione finale</span><span class="sxs-lookup"><span data-stu-id="2c708-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="2c708-124">è una delle opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="2c708-124">That is an option.</span></span> <span data-ttu-id="2c708-125">Quando si effettuano richieste di registrazione da un servizio di gestione API, è tuttavia necessario valutare l'impatto della registrazione dei messaggi sulle prestazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="2c708-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="2c708-126">Gli incrementi graduali nel carico possono essere gestiti da istanze a disponibilità crescente dei componenti di sistema o sfruttando i vantaggi della replica geografica.</span><span class="sxs-lookup"><span data-stu-id="2c708-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="2c708-127">I brevi picchi di traffico possono tuttavia provocare un ritardo significativo delle richieste se le richieste all'infrastruttura di registrazione iniziano a rallentare a causa del carico.</span><span class="sxs-lookup"><span data-stu-id="2c708-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="2c708-128">Hub eventi di Azure è stato progettato per inserire volumi elevati di dati, con una capacità sufficiente per la gestione di un numero di eventi molto più elevato rispetto al numero di richieste HTTP elaborate dalla maggior parte delle API.</span><span class="sxs-lookup"><span data-stu-id="2c708-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="2c708-129">L'Hub eventi è analogo a un buffer avanzato tra il servizio di gestione API e l'infrastruttura che archivierà ed elaborerà i messaggi.</span><span class="sxs-lookup"><span data-stu-id="2c708-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="2c708-130">Ciò assicura che le prestazioni dell'API non saranno danneggiate dall'infrastruttura di registrazione.</span><span class="sxs-lookup"><span data-stu-id="2c708-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="2c708-131">Dopo il passaggio a un hub eventi, i dati verranno resi persistenti e rimarranno in attesa di elaborazione da parte dei consumer dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2c708-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="2c708-132">Hub eventi non prevede requisiti specifici per la modalità di elaborazione dei dati, si impegna semplicemente nell'assicurare che il messaggio venga recapitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="2c708-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="2c708-133">Gli hub eventi possono effettuare lo streaming di eventi a più gruppi di consumer.</span><span class="sxs-lookup"><span data-stu-id="2c708-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="2c708-134">Ciò consente l'elaborazione degli eventi da parte di sistemi completamente diversi.</span><span class="sxs-lookup"><span data-stu-id="2c708-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="2c708-135">Sarà quindi possibile supportare molti scenari di integrazione senza ritardare ulteriormente l'elaborazione della richiesta API entro il servizio Gestione API, perché è necessario generare solo un evento.</span><span class="sxs-lookup"><span data-stu-id="2c708-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="2c708-136">Criterio per l'invio di messaggi applicazione/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c708-136">A policy to send application/http messages</span></span>
<span data-ttu-id="2c708-137">Un hub eventi accetta i dati evento sotto forma di semplice stringa.</span><span class="sxs-lookup"><span data-stu-id="2c708-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="2c708-138">I contenuti della stringa possono essere definiti completamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2c708-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="2c708-139">Per potere creare un pacchetto di una richiesta HTTP e inviarlo all'Hub eventi, è necessario formattare la stringa con le informazioni di richiesta o di risposta.</span><span class="sxs-lookup"><span data-stu-id="2c708-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="2c708-140">In situazioni come queste, se è disponibile una formattazione esistente che può essere usata, potrebbe non essere necessario scrivere codice di analisi specifico.</span><span class="sxs-lookup"><span data-stu-id="2c708-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="2c708-141">È stata inizialmente valutata la possibilità di usare [HAR](http://www.softwareishard.com/blog/har-12-spec/) per l'invio di richieste e risposte HTTP,</span><span class="sxs-lookup"><span data-stu-id="2c708-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="2c708-142">ma questo formato è ottimizzato per l'archiviazione di una sequenza di richieste HTTP in un formato basato su JSON.</span><span class="sxs-lookup"><span data-stu-id="2c708-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="2c708-143">Contiene alcuni elementi obbligatori che aggiungono una complessità superflua per lo scenario del passaggio del messaggio HTTP in rete.</span><span class="sxs-lookup"><span data-stu-id="2c708-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="2c708-144">Un'opzione alternativa consiste nell'usare il tipo di dati multimediali `application/http` , come illustrato nella specifica HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="2c708-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="2c708-145">Questo tipo di dati multimediali usa esattamente lo stesso formato adottato per inviare effettivamente i messaggi HTTP in rete, ma l'intero messaggio può essere inserito nel corpo di un'altra richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c708-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="2c708-146">In questo caso il corpo verrà usato come messaggio da inviare all'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2c708-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="2c708-147">Il parser disponibile nelle librerie [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) può essere usato per analizzare questo formato e convertirlo negli oggetti `HttpRequestMessage` e `HttpResponseMessage` nativi.</span><span class="sxs-lookup"><span data-stu-id="2c708-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="2c708-148">Per potere creare questo messaggio, è necessario sfruttare le [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) basate su C# disponibili in Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c708-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="2c708-149">Ecco il criterio che invia un messaggio di richiesta HTTP all'Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c708-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="2c708-150">Dichiarazione di criteri</span><span class="sxs-lookup"><span data-stu-id="2c708-150">Policy declaration</span></span>
<span data-ttu-id="2c708-151">È necessario evidenziare alcuni aspetti di questa espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="2c708-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="2c708-152">Il criterio log-to-eventhub ha un attributo denominato logger-id che fa riferimento al nome del logger creato nel servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2c708-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="2c708-153">I dettagli relativi alla configurazione di un logger dell'Hub eventi nel servizio Gestione API sono disponibili nel documento [Come registrare eventi nell'Hub eventi di Azure in Gestione API di Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2c708-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="2c708-154">Il secondo attributo è un parametro opzionale che indica all'Hub eventi la partizione in cui archiviare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="2c708-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="2c708-155">Hub eventi usa le partizioni per abilitare la scalabilità e richiede almeno due partizioni.</span><span class="sxs-lookup"><span data-stu-id="2c708-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="2c708-156">Il recapito ordinato dei messaggi è garantito solo entro una partizione.</span><span class="sxs-lookup"><span data-stu-id="2c708-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="2c708-157">Se non si indica all'Hub eventi la partizione in cui inserire il messaggio, verrà usato un algoritmo round-robin per distribuire il carico.</span><span class="sxs-lookup"><span data-stu-id="2c708-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="2c708-158">È tuttavia possibile che ciò provochi l'elaborazione non ordinata di alcuni messaggi.</span><span class="sxs-lookup"><span data-stu-id="2c708-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="2c708-159">Partitions</span><span class="sxs-lookup"><span data-stu-id="2c708-159">Partitions</span></span>
<span data-ttu-id="2c708-160">Per assicurarsi che i messaggi vengano recapitati ai consumer in base all'ordine stabilito e sfruttare i vantaggi della capacità di distribuzione del carico delle partizioni, è possibile scegliere di inviare messaggi di richiesta HTTP a una partizione e messaggi di risposta HTTP a una seconda partizione.</span><span class="sxs-lookup"><span data-stu-id="2c708-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="2c708-161">In questo modo si assicurerà una distribuzione uniforme del carico e sarà possibile garantire che tutte le richieste e le risposte vengano utilizzate nell'ordine stabilito.</span><span class="sxs-lookup"><span data-stu-id="2c708-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="2c708-162">È possibile che una risposta venga utilizzata prima della risposta corrispondente, ma questo non costituisce un problema, perché è disponibile un meccanismo diverso per la correlazione delle richieste alle risposte e si sa che le richieste precedono sempre le risposte.</span><span class="sxs-lookup"><span data-stu-id="2c708-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="2c708-163">Payload HTTP</span><span class="sxs-lookup"><span data-stu-id="2c708-163">HTTP payloads</span></span>
<span data-ttu-id="2c708-164">Dopo avere compilato `requestLine` , verificare se il corpo della richiesta deve essere troncato.</span><span class="sxs-lookup"><span data-stu-id="2c708-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="2c708-165">Il corpo della richiesta viene troncato solo a 1024.</span><span class="sxs-lookup"><span data-stu-id="2c708-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="2c708-166">È possibile aumentare questo valore, ma i singoli messaggi dell'Hub eventi sono limitati a 256 KB, quindi è probabile che alcuni corpi di messaggio HTTP non rientrino in un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="2c708-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="2c708-167">Durante la registrazione e l'analisi, è possibile ottenere una quantità significativa di informazioni semplicemente dalla riga e dalle intestazioni della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c708-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="2c708-168">Molte richieste API restituiscono inoltre corpi piccoli, quindi la perdita del valore di informazioni derivante dal troncamento di corpi di grandi dimensioni è abbastanza ridotta rispetto alla riduzione dei costi di trasferimento, elaborazione e archiviazione per la conservazione di tutti i contenuti del corpo.</span><span class="sxs-lookup"><span data-stu-id="2c708-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="2c708-169">È infine necessario notare, in merito all'elaborazione del corpo, che occorre passare `true` al metodo As<string>() poiché si stanno leggendo i contenuti del corpo, ma è anche necessario che l'API back-end sia in grado di leggere il corpo.</span><span class="sxs-lookup"><span data-stu-id="2c708-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="2c708-170">Se si passa true a questo metodo, il corpo verrà sottoposto a buffering, in modo che sia possibile leggerlo una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="2c708-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="2c708-171">È importante tenere in considerazione questo aspetto se si usa un'API che carica file di grandi dimensioni o usa polling di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="2c708-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="2c708-172">In questi casi è consigliabile evitare completamente la lettura del corpo.</span><span class="sxs-lookup"><span data-stu-id="2c708-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="2c708-173">Intestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="2c708-173">HTTP headers</span></span>
<span data-ttu-id="2c708-174">Le intestazioni HTTP possono essere semplicemente trasferite nel formato del messaggio sotto forma di semplice coppia chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="2c708-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="2c708-175">Alcuni campi che richiedono una sicurezza specifica sono stati eliminati per evitare la diffusione non necessaria delle informazioni relative alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="2c708-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="2c708-176">È poco probabile che le chiavi API e altre credenziali vengano usate per finalità analitiche.</span><span class="sxs-lookup"><span data-stu-id="2c708-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="2c708-177">Se si vuole effettuare un'analisi dell'utente e del prodotto specifico usato, sarà possibile ottenere queste informazioni dall'oggetto `context` e aggiungerle al messaggio.</span><span class="sxs-lookup"><span data-stu-id="2c708-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="2c708-178">Metadati del messaggio</span><span class="sxs-lookup"><span data-stu-id="2c708-178">Message Metadata</span></span>
<span data-ttu-id="2c708-179">Durante la creazione del messaggio completo da inviare all'hub eventi, la prima riga non fa effettivamente parte del messaggio `application/http` .</span><span class="sxs-lookup"><span data-stu-id="2c708-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="2c708-180">La prima riga include metadati aggiuntivi che indicano se il messaggio è un messaggio di richiesta o di risposta e l'ID del messaggio, che viene usato per correlare le richieste e l risposte.</span><span class="sxs-lookup"><span data-stu-id="2c708-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="2c708-181">L'ID del messaggio viene creato mediante un altro criterio, analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="2c708-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="2c708-182">È anche possibile creare il messaggio di richiesta, archiviarlo in una variabile fino alla restituzione della risposta e quindi semplicemente inviare la richiesta e la risposta come singolo messaggio,</span><span class="sxs-lookup"><span data-stu-id="2c708-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="2c708-183">ma l'invio indipendente di richiesta e risposta e l'uso di un ID del messaggio per correlarle consente di ottenere una maggiore flessibilità a livello di dimensioni del messaggio, di sfruttare i vantaggi offerti dalle partizioni multiple e di mantenere al tempo stesso l'ordine dei messaggi, oltre a visualizzare più rapidamente la richiesta nel dashboard di registrazione.</span><span class="sxs-lookup"><span data-stu-id="2c708-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="2c708-184">In alcuni scenari è anche possibile che non venga mai inviata all'hub eventi alcuna risposta valida, probabilmente a causa di un errore della richiesta nel servizio Gestione API, ma viene comunque mantenuto un record della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2c708-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="2c708-185">Il criterio per l'invio del messaggio di risposta HTTP è molto simile alla risposta, quindi la configurazione completa del criterio sarà analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="2c708-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="2c708-186">Il criterio `set-variable` crea un valore accessibile dal criterio `log-to-eventhub` nella sezione `<inbound>` e nella sezione `<outbound>`.</span><span class="sxs-lookup"><span data-stu-id="2c708-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="2c708-187">Ricezione di eventi dall'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2c708-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="2c708-188">Gli eventi dall'Hub eventi di Azure vengono ricevuti mediante il [protocollo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="2c708-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="2c708-189">Il team del bus di servizio Microsoft ha reso disponibili le librerie client per semplificare l'utilizzo degli eventi.</span><span class="sxs-lookup"><span data-stu-id="2c708-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="2c708-190">Sono supportati due approcci diversi, ovvero la modalità *consumer diretto* e l'uso della classe `EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="2c708-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="2c708-191">Gli esempi relativi a questi due approcci sono disponibili nella [Guida alla programmazione di Hub eventi](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2c708-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="2c708-192">In breve, `Direct Consumer` offre il controllo completo e `EventProcessorHost` esegue alcune operazioni di base ma include alcune ipotesi in merito al modo in cui gli eventi verranno elaborati.</span><span class="sxs-lookup"><span data-stu-id="2c708-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="2c708-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="2c708-193">EventProcessorHost</span></span>
<span data-ttu-id="2c708-194">Per semplificare, in questo esempio verrà usato l'approccio `EventProcessorHost` , anche se è possibile che non sia ottimale per questo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="2c708-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="2c708-195">`EventProcessorHost` esegue le operazioni necessarie per gestire automaticamente eventuali errori di threading relativi a una classe specifica del processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="2c708-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="2c708-196">In questo scenario, tuttavia, si converte semplicemente il messaggio in un altro formato e lo si passa a un altro servizio mediante un metodo asincrono.</span><span class="sxs-lookup"><span data-stu-id="2c708-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="2c708-197">Non è necessario aggiornare lo stato condiviso e quindi non si rischia che si verifichino problemi di threading.</span><span class="sxs-lookup"><span data-stu-id="2c708-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="2c708-198">Nella maggior parte degli scenari la scelta migliore è probabilmente costituita da `EventProcessorHost` , che è sicuramente l'opzione più semplice.</span><span class="sxs-lookup"><span data-stu-id="2c708-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="2c708-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="2c708-199">IEventProcessor</span></span>
<span data-ttu-id="2c708-200">Il concetto centrale dell'uso di `EventProcessorHost` consiste nel creare un'implementazione dell'interfaccia `IEventProcessor`, che include il metodo `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="2c708-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="2c708-201">Gli elementi fondamentali del metodo sono illustrati di seguito:</span><span class="sxs-lookup"><span data-stu-id="2c708-201">The essence of that method is shown here:</span></span>

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

<span data-ttu-id="2c708-202">Un elenco di oggetti EventData viene passato al metodo e viene eseguita l'iterazione dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c708-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="2c708-203">I byte di ogni metodo vengono analizzati in un oggetto HttpMessage e questo oggetto viene passato a un'istanza di IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="2c708-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="2c708-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="2c708-204">HttpMessage</span></span>
<span data-ttu-id="2c708-205">L'istanza `HttpMessage` contiene tre parti di dati:</span><span class="sxs-lookup"><span data-stu-id="2c708-205">The `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="2c708-206">L'istanza `HttpMessage` contiene un GUID `MessageId` che consente di connettere la richiesta HTTP alla risposta HTTP corrispondente e un valore booleano che indica se l'oggetto contiene un'istanza di HttpRequestMessage e HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="2c708-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="2c708-207">Usando le classi HTTP predefinite da `System.Net.Http`, è possibile sfruttare i vantaggi del codice di analisi `application/http` incluso in `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="2c708-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="2c708-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="2c708-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="2c708-209">L'istanza `HttpMessage` viene quindi inoltrata all'implementazione di `IHttpMessageProcessor`, che è un'interfaccia creata per disaccoppiare la ricezione e l'interpretazione dell'evento dall'Hub eventi di Azure e l'effettiva elaborazione dell'evento.</span><span class="sxs-lookup"><span data-stu-id="2c708-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="2c708-210">Inoltro del messaggio HTTP</span><span class="sxs-lookup"><span data-stu-id="2c708-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="2c708-211">Per questo esempio è possibile provare a effettuare il push della richiesta HTTP in [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="2c708-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="2c708-212">Runscope è un servizio basato sul cloud specializzato nel debug, nella registrazione e nel monitoraggio HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c708-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="2c708-213">È disponibile un livello gratuito, quindi è possibile provare a usarlo per visualizzare il passaggio in tempo reale delle richieste HTTP nel servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2c708-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="2c708-214">L'implementazione `IHttpMessageProcessor` ha un aspetto analogo al seguente,</span><span class="sxs-lookup"><span data-stu-id="2c708-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="2c708-215">È stato possibile sfruttare una [libreria client esistente per Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) che semplifica il push delle istanze `HttpRequestMessage` e `HttpResponseMessage` nel servizio.</span><span class="sxs-lookup"><span data-stu-id="2c708-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="2c708-216">Per accedere all'API Runscope, saranno necessari un account e una chiave API.</span><span class="sxs-lookup"><span data-stu-id="2c708-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="2c708-217">Le istruzioni per ottenere una chiave API sono disponibili nello screencast relativo alla [creazione di applicazioni per l'accesso all'API Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) .</span><span class="sxs-lookup"><span data-stu-id="2c708-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="2c708-218">Esempio completo</span><span class="sxs-lookup"><span data-stu-id="2c708-218">Complete sample</span></span>
<span data-ttu-id="2c708-219">Il [codice sorgente](https://github.com/darrelmiller/ApimEventProcessor) e i test per l'esempio sono disponibili su GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c708-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="2c708-220">Per eseguire l'esempio, è necessario disporre di un [servizio Gestione API](api-management-get-started.md), [un hub eventi connesso](api-management-howto-log-event-hubs.md) e un [account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="2c708-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="2c708-221">L'esempio è costituito da una semplice applicazione console che rimane in attesa di eventi provenienti dall'Hub eventi, quindi li converte in oggetti `HttpRequestMessage` e `HttpResponseMessage` e li inoltra all'API Runscope.</span><span class="sxs-lookup"><span data-stu-id="2c708-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="2c708-222">L'immagine animata seguente illustra l'effettuazione di una richiesta a un'API nel portale per sviluppatori, la ricezione, l'elaborazione e l'inoltro del messaggio nell'applicazione console e quindi la visualizzazione della richiesta e della risposta in Runscope Traffic Inspector.</span><span class="sxs-lookup"><span data-stu-id="2c708-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Illustrazione dell'inoltro di una richiesta a Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="2c708-224">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2c708-224">Summary</span></span>
<span data-ttu-id="2c708-225">Il servizio Gestione API di Azure è la posizione ideale per acquisire il traffico HTTP verso e dalle API.</span><span class="sxs-lookup"><span data-stu-id="2c708-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="2c708-226">Hub eventi di Azure è una soluzione a scalabilità elevata e costi ridotti per l'acquisizione e l'inserimento del traffico in sistemi di elaborazione secondari per operazioni di registrazione e monitoraggio e per altre analisi avanzate.</span><span class="sxs-lookup"><span data-stu-id="2c708-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="2c708-227">La connessione a sistemi di monitoraggio del traffico di terze parti come Runscope è semplice quanto scrivere qualche dozzina di righe di codice.</span><span class="sxs-lookup"><span data-stu-id="2c708-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c708-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c708-228">Next steps</span></span>
* <span data-ttu-id="2c708-229">Altre informazioni sull'Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="2c708-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="2c708-230">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2c708-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="2c708-231">Ricevere messaggi con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="2c708-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="2c708-232">Guida alla programmazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2c708-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="2c708-233">Altre informazioni sull'integrazione di Gestione API e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2c708-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="2c708-234">Come registrare eventi nell'Hub eventi di Azure in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="2c708-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="2c708-235">Informazioni di riferimento per l'entità logger</span><span class="sxs-lookup"><span data-stu-id="2c708-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="2c708-236">Informazioni di riferimento per i criteri log-to-event</span><span class="sxs-lookup"><span data-stu-id="2c708-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
