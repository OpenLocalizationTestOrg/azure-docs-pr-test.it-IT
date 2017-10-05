---
title: Informazioni su Hub eventi di Azure e relativi vantaggi | Documentazione Microsoft
description: Panoramica e introduzione all'Hub eventi di Azure - Inserimento di telemetria su scala cloud da siti Web, app e dispositivi
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: 1a6bf0a0352e6d9e3a22586ac825558d12e1307a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="47b6b-103">Che cos'è Hub eventi?</span><span class="sxs-lookup"><span data-stu-id="47b6b-103">What is Event Hubs?</span></span>

<span data-ttu-id="47b6b-104">Hub eventi di Azure è una piattaforma di streaming di dati estremamente scalabile e un servizio di inserimento degli eventi che consente di ricevere ed elaborare milioni di eventi al secondo.</span><span class="sxs-lookup"><span data-stu-id="47b6b-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="47b6b-105">Hub eventi consente di elaborare e archiviare eventi, dati o dati di telemetria generati dal software distribuito e dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="47b6b-106">I dati inviati a un hub eventi possono essere trasformati e archiviati usando qualsiasi provider di analisi in tempo reale o adattatori di invio in batch/archiviazione.</span><span class="sxs-lookup"><span data-stu-id="47b6b-106">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="47b6b-107">Con la possibilità di fornire [funzionalità di pubblicazione-sottoscrizione](https://msdn.microsoft.com/library/aa560414.aspx) con una latenza bassa e su larga scala, Hub eventi funge da "rampa di ingresso" per i Big Data.</span><span class="sxs-lookup"><span data-stu-id="47b6b-107">With the ability to provide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="47b6b-108">Vantaggi dell'uso di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="47b6b-108">Why use Event Hubs?</span></span>

<span data-ttu-id="47b6b-109">Gli eventi e le funzionalità di gestione della telemetria di Hub eventi sono particolarmente utili per:</span><span class="sxs-lookup"><span data-stu-id="47b6b-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="47b6b-110">Strumentazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="47b6b-110">Application instrumentation</span></span>
* <span data-ttu-id="47b6b-111">Esperienza dell'utente o l'elaborazione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="47b6b-111">User experience or workflow processing</span></span>
* <span data-ttu-id="47b6b-112">Scenari Internet of Things (IoT)</span><span class="sxs-lookup"><span data-stu-id="47b6b-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="47b6b-113">Hub eventi consente, ad esempio, il rilevamento del comportamento nelle app per dispositivi mobili, il traffico di informazioni da Web farm, l'acquisizione di eventi nei giochi per console e la raccolta di dati di telemetria da computer industriali, veicoli connessi o altri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="47b6b-114">Panoramica di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="47b6b-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="47b6b-115">Il ruolo comune svolto da Hub eventi nelle architetture delle soluzioni è la sua funzione di "porta principale" per una pipeline di eventi, spesso denominata *ingestor evento*.</span><span class="sxs-lookup"><span data-stu-id="47b6b-115">The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="47b6b-116">Un ingestor evento è un componente o servizio che si trova tra gli autori e i consumer di eventi per separare la produzione di un flusso di eventi dal consumo di tali eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-116">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="47b6b-117">Questa architettura è illustrata nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="47b6b-117">The following figure depicts this architecture:</span></span>

![Hub eventi](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="47b6b-119">Hub eventi offre funzionalità di gestione del flusso di messaggi, ma presenta caratteristiche diverse da quelle dei servizi di messaggistica aziendale tradizionale.</span><span class="sxs-lookup"><span data-stu-id="47b6b-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="47b6b-120">Le funzionalità di Hub eventi sono basate su scenari con velocità effettiva elevata ed elaborazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="47b6b-121">Di conseguenza, Hub eventi è diverso dalla messaggistica del [bus di servizio di Azure](https://azure.microsoft.com/services/service-bus/) e non implementa alcune delle funzionalità disponibili per le entità di [messaggistica del bus di servizio](/azure/service-bus-messaging/), ad esempio gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="47b6b-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of the capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="47b6b-122">Funzionalità di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="47b6b-122">Event Hubs features</span></span>

<span data-ttu-id="47b6b-123">Hub eventi contiene gli elementi chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="47b6b-123">Event Hubs contains the following key elements:</span></span>

- <span data-ttu-id="47b6b-124">[**Producer/autori di eventi**](event-hubs-features.md#event-publishers): qualsiasi entità che invia dati a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data to an event hub.</span></span> <span data-ttu-id="47b6b-125">Un evento viene pubblicato tramite AMQP 1.0 o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="47b6b-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="47b6b-126">[**Acquisizione**](event-hubs-features.md#capture): consente di acquisire i dati di streaming di Hub eventi e archiviarli in un account di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="47b6b-126">[**Capture**](event-hubs-features.md#capture): Enables you to capture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="47b6b-127">[**Partizioni**](event-hubs-features.md#partitions): consentono a ogni consumer di leggere solo uno specifico subset, o partizione, del flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer to only read a specific subset, or partition, of the event stream.</span></span>
- <span data-ttu-id="47b6b-128">[**Token di firma di accesso condiviso**](event-hubs-features.md#sas-tokens): consentono di identificare e autenticare l'autore di eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates the event publisher.</span></span>
- <span data-ttu-id="47b6b-129">[**Consumer eventi**](event-hubs-features.md#event-consumers): qualsiasi entità che legge i dati dell'evento da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="47b6b-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="47b6b-130">I consumer eventi si connettono tramite AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="47b6b-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="47b6b-131">[**Gruppi di consumer**](event-hubs-features.md#consumer-groups): offrono a ogni singola applicazione una visualizzazione separata del flusso di eventi, consentendo a tali consumer di operare in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="47b6b-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of the event stream, enabling those consumers to act independently.</span></span>
- <span data-ttu-id="47b6b-132">[**Unità elaborate**](event-hubs-features.md#capacity): unità di capacità pre-acquistate.</span><span class="sxs-lookup"><span data-stu-id="47b6b-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="47b6b-133">Una singola partizione ha una scalabilità massima di 1 unità elaborata.</span><span class="sxs-lookup"><span data-stu-id="47b6b-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="47b6b-134">Per informazioni tecniche dettagliate su queste e altre funzionalità di Hub eventi, vedere la [panoramica sulle funzionalità di Hub eventi](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="47b6b-134">For technical details about these and other Event Hubs features, see the [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="47b6b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47b6b-135">Next steps</span></span>

<span data-ttu-id="47b6b-136">Per informazioni dettagliate sui prezzi di Hub eventi, vedere [Hub eventi Prezzi](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="47b6b-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="47b6b-137">Per altre informazioni su Hub eventi, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="47b6b-137">For more information about Event Hubs, visit the following links:</span></span>

* <span data-ttu-id="47b6b-138">Iniziare con un'[esercitazione di Hub eventi](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="47b6b-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="47b6b-139">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="47b6b-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="47b6b-140">Applicazioni di esempio che usano Hub eventi</span><span class="sxs-lookup"><span data-stu-id="47b6b-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

