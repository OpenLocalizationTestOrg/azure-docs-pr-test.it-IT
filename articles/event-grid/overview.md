---
title: Cenni preliminari sulla griglia di eventi aaaAzure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="e40f3-103">Un tooAzure introduzione della griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="e40f3-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="e40f3-104">Griglia di eventi Azure consente tooeasily creare applicazioni con le architetture basato su eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="e40f3-105">Selezionare le risorse di Azure desideri toosubscribe per e assegnare il gestore di eventi hello o WebHook endpoint toosend hello evento hello.</span><span class="sxs-lookup"><span data-stu-id="e40f3-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="e40f3-106">Griglia di eventi offre il supporto predefinito per gli eventi generati dai servizi di Azure, ad esempio BLOB di archiviazione e gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="e40f3-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="e40f3-107">Griglia di eventi offre anche il supporto personalizzato per gli eventi dell'applicazione e di terze parti, tramite argomenti personalizzati e webhook personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e40f3-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="e40f3-108">È possibile utilizzare i filtri tooroute eventi specifici toodifferent endpoint, endpoint multicast toomultiple e assicurarsi che gli eventi vengono recapitati in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="e40f3-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="e40f3-109">Griglia di eventi offre anche il supporto predefinito per eventi personalizzati e di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e40f3-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="e40f3-110">Per la versione di anteprima hello griglia eventi supporta **westus2** e **westcentralus** percorsi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="e40f3-111">Verranno aggiunte altre aree.</span><span class="sxs-lookup"><span data-stu-id="e40f3-111">Other regions will be added.</span></span>

<span data-ttu-id="e40f3-112">Questo articolo offre una panoramica di Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e40f3-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="e40f3-113">Se si desidera tooget avviato con la griglia di eventi, vedere [route e creare eventi personalizzati con griglia di eventi di Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e40f3-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Modello funzionale di Griglia di eventi](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="e40f3-115">Archiviazione Blob non è attualmente disponibile pubblicamente come server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="e40f3-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="e40f3-116">Concetti</span><span class="sxs-lookup"><span data-stu-id="e40f3-116">Concepts</span></span>

<span data-ttu-id="e40f3-117">Per iniziare, è opportuno tenere presenti cinque concetti relativi a Griglia di eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="e40f3-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="e40f3-118">**Eventi**: ciò che successo.</span><span class="sxs-lookup"><span data-stu-id="e40f3-118">**Events** - What happened.</span></span>
* <span data-ttu-id="e40f3-119">**Origini evento/server di pubblicazione** - evento hello ha avuto luogo.</span><span class="sxs-lookup"><span data-stu-id="e40f3-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="e40f3-120">**Argomenti** -hello endpoint in cui i server di pubblicazione invia eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="e40f3-121">**Le sottoscrizioni di eventi** -hello eventi tooroute meccanismo endpoint o incorporato, talvolta toomultiple gestori.</span><span class="sxs-lookup"><span data-stu-id="e40f3-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="e40f3-122">Le sottoscrizioni vengono inoltre utilizzate dagli eventi in ingresso di gestori toointelligently filtro.</span><span class="sxs-lookup"><span data-stu-id="e40f3-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="e40f3-123">**I gestori eventi** : hello app o reazione toohello eventi del servizio.</span><span class="sxs-lookup"><span data-stu-id="e40f3-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="e40f3-124">Per altre informazioni su questi concetti, vedere [Concepts in Azure Event Grid](concepts.md) (Concetti relativi a Griglia di eventi di Azure).</span><span class="sxs-lookup"><span data-stu-id="e40f3-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="e40f3-125">Capabilities</span><span class="sxs-lookup"><span data-stu-id="e40f3-125">Capabilities</span></span>

<span data-ttu-id="e40f3-126">Ecco alcune delle funzionalità chiave di hello di griglia di eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="e40f3-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="e40f3-127">**Semplicità** -punto e fare clic su eventi tooaim dal gestore dell'evento tooany risorse di Azure o endpoint.</span><span class="sxs-lookup"><span data-stu-id="e40f3-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="e40f3-128">**Filtro avanzato** -filtro evento di tipo o un evento pubblicare tooensure percorso gestori di ricezione solo eventi rilevanti.</span><span class="sxs-lookup"><span data-stu-id="e40f3-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="e40f3-129">**Fan-out** -sottoscrizione più endpoint toohello stesso evento toosend copie di hello evento tooas numerose posizioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e40f3-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="e40f3-130">**Affidabilità** -utilizzare 24 ore tentativi con backoff esponenziale tooensure gli eventi vengono recapitati.</span><span class="sxs-lookup"><span data-stu-id="e40f3-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="e40f3-131">**Per ogni evento di retribuzione** : paga solo per quantità hello è possibile utilizzare la griglia evento.</span><span class="sxs-lookup"><span data-stu-id="e40f3-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="e40f3-132">**Velocità effettiva elevata**: consente di creare carichi di lavoro con volumi elevati in Griglia di eventi con il supporto per milioni di eventi al secondo.</span><span class="sxs-lookup"><span data-stu-id="e40f3-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="e40f3-133">**Eventi predefiniti**: consentono di essere operativi rapidamente con gli eventi predefiniti a livello di risorse.</span><span class="sxs-lookup"><span data-stu-id="e40f3-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="e40f3-134">**Eventi personalizzati**: consentono di usare la route di Griglia di eventi, di filtrare e recapitare in modo affidabile gli eventi personalizzati nell'app.</span><span class="sxs-lookup"><span data-stu-id="e40f3-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="e40f3-135">Integrazione predefinita di gestori e autori</span><span class="sxs-lookup"><span data-stu-id="e40f3-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="e40f3-136">Azure offre il supporto per gli eventi predefiniti grazie a numerosi servizi, inclusi autori e gestori.</span><span class="sxs-lookup"><span data-stu-id="e40f3-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="e40f3-137">Autori</span><span class="sxs-lookup"><span data-stu-id="e40f3-137">Publishers</span></span>

<span data-ttu-id="e40f3-138">Hello servizi di Azure seguenti sono attualmente supporto dell'autore incorporati per la griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="e40f3-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="e40f3-139">Gruppi di risorse (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="e40f3-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="e40f3-140">Sottoscrizioni di Azure (operazioni di gestione)</span><span class="sxs-lookup"><span data-stu-id="e40f3-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="e40f3-141">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="e40f3-141">Event Hubs</span></span>
* <span data-ttu-id="e40f3-142">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="e40f3-142">Custom Topics</span></span>

<span data-ttu-id="e40f3-143">Quest'anno verranno aggiunti altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e40f3-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="e40f3-144">Gestori</span><span class="sxs-lookup"><span data-stu-id="e40f3-144">Handlers</span></span>

<span data-ttu-id="e40f3-145">Hello servizi di Azure seguenti sono attualmente supporto per i gestori predefiniti per la griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="e40f3-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="e40f3-146">Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e40f3-146">Azure Functions</span></span>
* <span data-ttu-id="e40f3-147">App per la logica</span><span class="sxs-lookup"><span data-stu-id="e40f3-147">Logic Apps</span></span>
* <span data-ttu-id="e40f3-148">Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e40f3-148">Azure Automation</span></span>
* <span data-ttu-id="e40f3-149">Webhook</span><span class="sxs-lookup"><span data-stu-id="e40f3-149">WebHooks</span></span>

<span data-ttu-id="e40f3-150">Quest'anno verranno aggiunti altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e40f3-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="e40f3-151">Quali operazioni si possono eseguire con Griglia di eventi?</span><span class="sxs-lookup"><span data-stu-id="e40f3-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="e40f3-152">Griglia di eventi di Azure offre diverse funzionalità che migliorano considerevolmente le attività senza server, di automazione delle operazioni e di integrazione:</span><span class="sxs-lookup"><span data-stu-id="e40f3-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="e40f3-153">Architetture di applicazioni senza server</span><span class="sxs-lookup"><span data-stu-id="e40f3-153">Serverless application architectures</span></span>

![Applicazione senza server](./media/overview/serverless_web_app.png)

<span data-ttu-id="e40f3-155">Griglia di eventi connette le origini dati e i gestori di eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="e40f3-156">Ad esempio, utilizzare trigger di evento griglia tooinstantly un'analisi delle immagini toorun senza funzione ogni volta che è una foto di nuovo aggiunto tooa contenitore di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="e40f3-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="e40f3-157">Automazione delle operazioni</span><span class="sxs-lookup"><span data-stu-id="e40f3-157">Ops Automation</span></span>

![Automazione delle operazioni](./media/overview/Ops_automation.png)

<span data-ttu-id="e40f3-159">Griglia di eventi consente di automazione toospeed e semplificare l'applicazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="e40f3-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="e40f3-160">Griglia di eventi, ad esempio, può notificare ad Automazione di Azure quando una macchina virtuale viene creata o un database SQL viene attivato.</span><span class="sxs-lookup"><span data-stu-id="e40f3-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="e40f3-161">Questi eventi possono essere usati tooautomatically verificare che le configurazioni del servizio sono conformi, inserire i metadati in strumenti di operazioni, le macchine virtuali di tag o gli elementi di lavoro di file.</span><span class="sxs-lookup"><span data-stu-id="e40f3-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="e40f3-162">Integrazione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="e40f3-162">Application integration</span></span>

![Integrazione di applicazioni](./media/overview/app_integration.png)

<span data-ttu-id="e40f3-164">Griglia di eventi connette l'app con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="e40f3-165">Ad esempio, creare toosend un argomento personalizzato tooEvent dati di evento dell'app griglia e sfruttare il recapito affidabile, avanzato, routing e integrazione diretta con Azure.</span><span class="sxs-lookup"><span data-stu-id="e40f3-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="e40f3-166">In alternativa, è possibile utilizzare la griglia di eventi con i dati in un punto qualsiasi, di App per la logica tooprocess senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="e40f3-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="e40f3-167">Differenze tra Griglia di eventi e gli altri servizi di integrazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e40f3-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="e40f3-168">Griglia di eventi è un backplane eventi che abilita la programmazione reattiva basata su eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="e40f3-169">È strettamente integrato con i servizi di Azure e può essere integrato con i servizi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e40f3-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="e40f3-170">messaggio evento contiene informazioni hello necessarie toochanges tooreact nei servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e40f3-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="e40f3-171">Griglia di eventi non è una pipeline di dati e il recapito non hello effettivo oggetto che è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e40f3-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="e40f3-172">Il bus di servizio è adatto alle tradizionali applicazioni aziendali che richiedono transazioni, ordinamento, rilevamento duplicati e coerenza immediata.</span><span class="sxs-lookup"><span data-stu-id="e40f3-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="e40f3-173">Griglia di eventi è progettato per la velocità, la scalabilità, la varietà e il costo contenuto in un modello reattivo.</span><span class="sxs-lookup"><span data-stu-id="e40f3-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="e40f3-174">È particolarmente adatta tooserverless architettura.</span><span class="sxs-lookup"><span data-stu-id="e40f3-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="e40f3-175">Griglia di eventi è complementare agli altri servizi di Azure, ad esempio App per la logica e Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="e40f3-176">I trigger di evento griglia hello logica app toobegin relativo flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e40f3-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="e40f3-177">Hub eventi funziona con griglia eventi consentendo tooevents tooreact da acquisire gli hub di eventi e pipeline in ingresso e la trasformazione di dati compilazione.</span><span class="sxs-lookup"><span data-stu-id="e40f3-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="e40f3-178">Costi di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="e40f3-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="e40f3-179">Griglia di eventi di Azure usa un modello di determinazione prezzi basato sul pagamento per evento, quindi si paga solo per le risorse usate.</span><span class="sxs-lookup"><span data-stu-id="e40f3-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="e40f3-180">Griglia eventi costa $0.60 per milione di operazioni ($0,30 durante l'anteprima) e hello 100.000 prima operazione al mese sono gratuiti.</span><span class="sxs-lookup"><span data-stu-id="e40f3-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="e40f3-181">Le operazioni vengono definite come inserimento di eventi, corrispondenza avanzata, tentativo di recapito e chiamate di gestione.</span><span class="sxs-lookup"><span data-stu-id="e40f3-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="e40f3-182">Sono disponibili ulteriori dettagli su hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="e40f3-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e40f3-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e40f3-183">Next steps</span></span>

* <span data-ttu-id="e40f3-184">[Creare ed eseguire la sottoscrizione degli eventi toocustom](custom-event-quickstart.md) subito e iniziare a inviare il proprio endpoint tooany eventi personalizzati utilizzando hello Guida introduttiva di griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e40f3-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="e40f3-185">[Utilizzando la logica App come un gestore eventi](monitor-virtual-machine-changes-event-grid-logic-app.md) un'esercitazione sulla creazione di un'app usando l'App per la logica tooreact tooevents inserito dalla griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="e40f3-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="e40f3-186">Event Grid REST API reference (Informazioni di riferimento sulle API REST di Griglia di eventi)</span><span class="sxs-lookup"><span data-stu-id="e40f3-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="e40f3-187">Fornisce informazioni più tecniche hello griglia di eventi di Azure e un riferimento per la gestione di sottoscrizioni di eventi, routing e il filtraggio.</span><span class="sxs-lookup"><span data-stu-id="e40f3-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
