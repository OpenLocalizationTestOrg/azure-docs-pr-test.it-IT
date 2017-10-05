---
title: Panoramica di Griglia di eventi di Azure
description: Descrive Griglia di eventi di Azure e ne illustra i principali concetti.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 59a834f32793e349d5639baf3c80dbcba274dfa8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="an-introduction-to-azure-event-grid"></a><span data-ttu-id="8b46e-103">Introduzione a Griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="8b46e-103">An introduction to Azure Event Grid</span></span>

<span data-ttu-id="8b46e-104">Griglia di eventi di Azure consente di compilare facilmente applicazioni con architetture basate su eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-104">Azure Event Grid allows you to easily build applications with event-based architectures.</span></span> <span data-ttu-id="8b46e-105">Si seleziona la risorsa di Azure che si vuole sottoscrivere e si specifica il gestore dell'evento o l'endpoint di webhook a cui inviare l'evento.</span><span class="sxs-lookup"><span data-stu-id="8b46e-105">You select the Azure resource you would like to subscribe to, and give the event handler or WebHook endpoint to send the event to.</span></span> <span data-ttu-id="8b46e-106">Griglia di eventi offre il supporto predefinito per gli eventi generati dai servizi di Azure, ad esempio BLOB di archiviazione e gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="8b46e-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="8b46e-107">Griglia di eventi offre anche il supporto personalizzato per gli eventi dell'applicazione e di terze parti, tramite argomenti personalizzati e webhook personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8b46e-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="8b46e-108">È possibile usare i filtri per instradare eventi specifici a endpoint diversi, trasmetterli a più endpoint e verificare che gli eventi vengano recapitati in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="8b46e-108">You can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="8b46e-109">Griglia di eventi offre anche il supporto predefinito per eventi personalizzati e di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8b46e-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="8b46e-110">Per la versione di anteprima, la griglia di eventi supporta le località **westus2** e **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="8b46e-110">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="8b46e-111">Verranno aggiunte altre aree.</span><span class="sxs-lookup"><span data-stu-id="8b46e-111">Other regions will be added.</span></span>

<span data-ttu-id="8b46e-112">Questo articolo offre una panoramica di Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b46e-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="8b46e-113">Per iniziare a usare Griglia di eventi, vedere [Create and route custom events with Azure Event Grid](custom-event-quickstart.md) (Creare e instradare eventi personalizzati con Griglia di eventi di Azure).</span><span class="sxs-lookup"><span data-stu-id="8b46e-113">If you want to get started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Modello funzionale di Griglia di eventi](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="8b46e-115">Archiviazione Blob non è attualmente disponibile pubblicamente come server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8b46e-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="8b46e-116">Concetti</span><span class="sxs-lookup"><span data-stu-id="8b46e-116">Concepts</span></span>

<span data-ttu-id="8b46e-117">Per iniziare, è opportuno tenere presenti cinque concetti relativi a Griglia di eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="8b46e-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="8b46e-118">**Eventi**: ciò che successo.</span><span class="sxs-lookup"><span data-stu-id="8b46e-118">**Events** - What happened.</span></span>
* <span data-ttu-id="8b46e-119">**Origini/Autori di eventi**: dove si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="8b46e-119">**Event sources/publishers** - Where the event took place.</span></span>
* <span data-ttu-id="8b46e-120">**Argomenti**: l'endpoint a cui gli autori inviano gli eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-120">**Topics** - The endpoint where publishers send events.</span></span>
* <span data-ttu-id="8b46e-121">**Sottoscrizioni agli eventi**: l'endpoint o il meccanismo predefinito per instradare gli eventi, a volte a più gestori.</span><span class="sxs-lookup"><span data-stu-id="8b46e-121">**Event subscriptions** - The endpoint or built-in mechanism to route events, sometimes to multiple handlers.</span></span> <span data-ttu-id="8b46e-122">Le sottoscrizioni vengono usate dai gestori anche per filtrare in modo intelligente gli eventi in ingresso.</span><span class="sxs-lookup"><span data-stu-id="8b46e-122">Subscriptions are also used by handlers to intelligently filter incoming events.</span></span>
* <span data-ttu-id="8b46e-123">**Gestori di eventi**: l'app o il servizio che reagisce all'evento.</span><span class="sxs-lookup"><span data-stu-id="8b46e-123">**Event handlers** - The app or service reacting to the event.</span></span>

<span data-ttu-id="8b46e-124">Per altre informazioni su questi concetti, vedere [Concepts in Azure Event Grid](concepts.md) (Concetti relativi a Griglia di eventi di Azure).</span><span class="sxs-lookup"><span data-stu-id="8b46e-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="8b46e-125">Capabilities</span><span class="sxs-lookup"><span data-stu-id="8b46e-125">Capabilities</span></span>

<span data-ttu-id="8b46e-126">Ecco alcune delle principali funzionalità di Griglia di eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="8b46e-126">Here are some of the key features of Azure Event Grid:</span></span>

* <span data-ttu-id="8b46e-127">**Semplicità**: consente di indirizzare facilmente gli eventi dalla risorsa di Azure a un gestore dell'evento o a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="8b46e-127">**Simplicity** - Point and click to aim events from your Azure resource to any event handler or endpoint.</span></span>
* <span data-ttu-id="8b46e-128">**Filtro avanzato**: consente di filtrare per tipo di evento o per percorso di pubblicazione di un evento per assicurarsi che i gestori di eventi ricevano solo gli eventi pertinenti.</span><span class="sxs-lookup"><span data-stu-id="8b46e-128">**Advanced filtering** - Filter on event type or event publish path to ensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="8b46e-129">**Fan-out**: consente di sottoscrivere più endpoint allo stesso evento per inviare copie dell'evento a tutte le posizioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="8b46e-129">**Fan-out** - Subscribe multiple endpoints to the same event to send copies of the event to as many places as needed.</span></span>
* <span data-ttu-id="8b46e-130">**Affidabilità**: consente di ripetere i tentativi per 24 ore con backoff esponenziale per assicurarsi che gli eventi vengano recapitati.</span><span class="sxs-lookup"><span data-stu-id="8b46e-130">**Reliability** - Utilize 24-hour retry with exponential backoff to ensure events are delivered.</span></span>
* <span data-ttu-id="8b46e-131">**Pagamento per evento** consente di pagare solo in base all'uso di Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-131">**Pay-per-event** - Pay only for the amount you use Event Grid.</span></span>
* <span data-ttu-id="8b46e-132">**Velocità effettiva elevata**: consente di creare carichi di lavoro con volumi elevati in Griglia di eventi con il supporto per milioni di eventi al secondo.</span><span class="sxs-lookup"><span data-stu-id="8b46e-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="8b46e-133">**Eventi predefiniti**: consentono di essere operativi rapidamente con gli eventi predefiniti a livello di risorse.</span><span class="sxs-lookup"><span data-stu-id="8b46e-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="8b46e-134">**Eventi personalizzati**: consentono di usare la route di Griglia di eventi, di filtrare e recapitare in modo affidabile gli eventi personalizzati nell'app.</span><span class="sxs-lookup"><span data-stu-id="8b46e-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="8b46e-135">Integrazione predefinita di gestori e autori</span><span class="sxs-lookup"><span data-stu-id="8b46e-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="8b46e-136">Azure offre il supporto per gli eventi predefiniti grazie a numerosi servizi, inclusi autori e gestori.</span><span class="sxs-lookup"><span data-stu-id="8b46e-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="8b46e-137">Autori</span><span class="sxs-lookup"><span data-stu-id="8b46e-137">Publishers</span></span>

<span data-ttu-id="8b46e-138">Attualmente i servizi di Azure seguenti hanno il supporto predefinito degli autori per Griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="8b46e-138">Currently, the following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="8b46e-139">Gruppi di risorse (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="8b46e-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="8b46e-140">Sottoscrizioni di Azure (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="8b46e-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="8b46e-141">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="8b46e-141">Event Hubs</span></span>
* <span data-ttu-id="8b46e-142">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="8b46e-142">Custom Topics</span></span>

<span data-ttu-id="8b46e-143">Quest'anno verranno aggiunti altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b46e-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="8b46e-144">Gestori</span><span class="sxs-lookup"><span data-stu-id="8b46e-144">Handlers</span></span>

<span data-ttu-id="8b46e-145">Attualmente i servizi di Azure seguenti hanno il supporto predefinito dei gestori per Griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="8b46e-145">Currently, the following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="8b46e-146">Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="8b46e-146">Azure Functions</span></span>
* <span data-ttu-id="8b46e-147">App per la logica</span><span class="sxs-lookup"><span data-stu-id="8b46e-147">Logic Apps</span></span>
* <span data-ttu-id="8b46e-148">Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8b46e-148">Azure Automation</span></span>
* <span data-ttu-id="8b46e-149">Webhook</span><span class="sxs-lookup"><span data-stu-id="8b46e-149">WebHooks</span></span>

<span data-ttu-id="8b46e-150">Quest'anno verranno aggiunti altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b46e-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="8b46e-151">Quali operazioni si possono eseguire con Griglia di eventi?</span><span class="sxs-lookup"><span data-stu-id="8b46e-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="8b46e-152">Griglia di eventi di Azure offre diverse funzionalità che migliorano considerevolmente le attività senza server, di automazione delle operazioni e di integrazione:</span><span class="sxs-lookup"><span data-stu-id="8b46e-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="8b46e-153">Architetture di applicazioni senza server</span><span class="sxs-lookup"><span data-stu-id="8b46e-153">Serverless application architectures</span></span>

![Applicazione senza server](./media/overview/serverless_web_app.png)

<span data-ttu-id="8b46e-155">Griglia di eventi connette le origini dati e i gestori di eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="8b46e-156">Usare, ad esempio, Griglia di eventi per attivare immediatamente una funzione senza server per eseguire l'analisi dell'immagine ogni volta che una nuova foto viene aggiunta a un contenitore di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="8b46e-156">For example, use Event Grid to instantly trigger a serverless function to run image analysis each time a new photo is added to a blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="8b46e-157">Automazione delle operazioni</span><span class="sxs-lookup"><span data-stu-id="8b46e-157">Ops Automation</span></span>

![Automazione delle operazioni](./media/overview/Ops_automation.png)

<span data-ttu-id="8b46e-159">Griglia di eventi consente di velocizzare l'automazione e semplificare l'applicazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="8b46e-159">Event Grid allows you to speed automation and simplify policy enforcement.</span></span> <span data-ttu-id="8b46e-160">Griglia di eventi, ad esempio, può notificare ad Automazione di Azure quando una macchina virtuale viene creata o un database SQL viene attivato.</span><span class="sxs-lookup"><span data-stu-id="8b46e-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="8b46e-161">Questi eventi possono essere usati per controllare automaticamente che le configurazioni dei servizi siano conformi, inserire i metadati negli strumenti per le operazioni, contrassegnare le macchine virtuali o archiviare gli elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b46e-161">These events can be used to automatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="8b46e-162">Integrazione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="8b46e-162">Application integration</span></span>

![Integrazione di applicazioni](./media/overview/app_integration.png)

<span data-ttu-id="8b46e-164">Griglia di eventi connette l'app con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="8b46e-165">Creare, ad esempio, un argomento personalizzato per inviare i dati dell'evento dell'app a Griglia di eventi e sfruttare il recapito affidabile, il routing avanzato e l'integrazione diretta con Azure.</span><span class="sxs-lookup"><span data-stu-id="8b46e-165">For example, create a custom topic to send your app's event data to Event Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="8b46e-166">In alternativa è possibile usare Griglia di eventi con App per la logica per elaborare i dati ovunque, senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="8b46e-166">Alternatively, you can use Event Grid with Logic Apps to process data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="8b46e-167">Differenze tra Griglia di eventi e gli altri servizi di integrazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8b46e-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="8b46e-168">Griglia di eventi è un backplane eventi che abilita la programmazione reattiva basata su eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="8b46e-169">È strettamente integrato con i servizi di Azure e può essere integrato con i servizi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8b46e-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="8b46e-170">Il messaggio dell'evento contiene le informazioni necessarie per reagire alle modifiche apportate ai servizi e alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8b46e-170">The event message contains the information you need to react to changes in services and applications.</span></span> <span data-ttu-id="8b46e-171">Griglia di eventi non è una pipeline di dati e non recapita l'oggetto effettivo aggiornato.</span><span class="sxs-lookup"><span data-stu-id="8b46e-171">Event Grid is not a data pipeline, and does not deliver the actual object that was updated.</span></span>

<span data-ttu-id="8b46e-172">Il bus di servizio è adatto alle tradizionali applicazioni aziendali che richiedono transazioni, ordinamento, rilevamento duplicati e coerenza immediata.</span><span class="sxs-lookup"><span data-stu-id="8b46e-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="8b46e-173">Griglia di eventi è progettato per la velocità, la scalabilità, la varietà e il costo contenuto in un modello reattivo.</span><span class="sxs-lookup"><span data-stu-id="8b46e-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="8b46e-174">È particolarmente adatto per l'architettura senza server.</span><span class="sxs-lookup"><span data-stu-id="8b46e-174">It is well suited to serverless architecture.</span></span>

<span data-ttu-id="8b46e-175">Griglia di eventi è complementare agli altri servizi di Azure, ad esempio App per la logica e Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="8b46e-176">Griglia di eventi attiva l'app per la logica per iniziarne il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b46e-176">Event Grid triggers the logic app to begin its workflow.</span></span> <span data-ttu-id="8b46e-177">Hub eventi interagisce con Griglia di eventi consentendo di reagire agli eventi dalla funzionalità di acquisizione di Hub eventi e di creare pipeline per la trasformazione e l'inserimento di dati.</span><span class="sxs-lookup"><span data-stu-id="8b46e-177">Event Hubs works with Event Grid by enabling you to react to events from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="8b46e-178">Costi di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="8b46e-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="8b46e-179">Griglia di eventi di Azure usa un modello di determinazione prezzi basato sul pagamento per evento, quindi si paga solo per le risorse usate.</span><span class="sxs-lookup"><span data-stu-id="8b46e-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="8b46e-180">Griglia di eventi costa $ 0,60 per milione di operazioni ($ 0,30 durante l'anteprima) e le prime 100.000 operazioni al mese sono gratuite.</span><span class="sxs-lookup"><span data-stu-id="8b46e-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and the first 100,000 operation per month are free.</span></span> <span data-ttu-id="8b46e-181">Le operazioni vengono definite come inserimento di eventi, corrispondenza avanzata, tentativo di recapito e chiamate di gestione.</span><span class="sxs-lookup"><span data-stu-id="8b46e-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="8b46e-182">Per informazioni più dettagliate, vedere la [pagina dedicata ai prezzi](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="8b46e-182">More details can be found on the [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b46e-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b46e-183">Next steps</span></span>

* <span data-ttu-id="8b46e-184">[Create and subscribe to custom events (Creare e sottoscrivere eventi personalizzati)](custom-event-quickstart.md) È possibile iniziare subito a inviare gli eventi personalizzati agli endpoint usando la guida introduttiva di Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b46e-184">[Create and subscribe to custom events](custom-event-quickstart.md) Jump right in and start sending your own custom events to any endpoint using the Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="8b46e-185">[Using Logic Apps as an Event Handler (Uso di App per la logica come gestore dell'evento)](monitor-virtual-machine-changes-event-grid-logic-app.md) Esercitazione sulla compilazione di un'app con App per la logica per reagire agli eventi di cui viene eseguito il push da Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="8b46e-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps to react to events pushed by Event Grid.</span></span>
* [<span data-ttu-id="8b46e-186">Event Grid REST API reference (Informazioni di riferimento sulle API REST di Griglia di eventi)</span><span class="sxs-lookup"><span data-stu-id="8b46e-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="8b46e-187">Offre informazioni più tecniche su Griglia di eventi di Azure e un riferimento per la gestione di sottoscrizioni agli eventi, routing e filtri.</span><span class="sxs-lookup"><span data-stu-id="8b46e-187">Provides more technical information about the Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>