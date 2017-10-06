---
title: "aaaWhat è l'hub eventi di Azure e perché usarlo | Documenti Microsoft"
description: Panoramica e introduzione tooAzure hub eventi - inserimento di dati di telemetria a livello di Cloud di siti Web, applicazioni e dispositivi
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
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="fee38-103">Che cos'è Hub eventi?</span><span class="sxs-lookup"><span data-stu-id="fee38-103">What is Event Hubs?</span></span>

<span data-ttu-id="fee38-104">Hub eventi di Azure è una piattaforma di streaming di dati estremamente scalabile e un servizio di inserimento degli eventi che consente di ricevere ed elaborare milioni di eventi al secondo.</span><span class="sxs-lookup"><span data-stu-id="fee38-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="fee38-105">Hub eventi consente di elaborare e archiviare eventi, dati o dati di telemetria generati dal software distribuito e dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fee38-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="fee38-106">I dati inviati tooan hub di eventi possono essere trasformati e memorizzati tramite qualsiasi provider analitica in tempo reale o schede dell'invio in batch o dell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fee38-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="fee38-107">Con hello possibilità tooprovide [funzionalità di pubblicazione-sottoscrizione](https://msdn.microsoft.com/library/aa560414.aspx) con una latenza bassa e su larga scala, hub eventi funge da hello "on"Preparazione per Big Data.</span><span class="sxs-lookup"><span data-stu-id="fee38-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="fee38-108">Vantaggi dell'uso di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fee38-108">Why use Event Hubs?</span></span>

<span data-ttu-id="fee38-109">Gli eventi e le funzionalità di gestione della telemetria di Hub eventi sono particolarmente utili per:</span><span class="sxs-lookup"><span data-stu-id="fee38-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="fee38-110">Strumentazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fee38-110">Application instrumentation</span></span>
* <span data-ttu-id="fee38-111">Esperienza dell'utente o l'elaborazione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="fee38-111">User experience or workflow processing</span></span>
* <span data-ttu-id="fee38-112">Scenari Internet of Things (IoT)</span><span class="sxs-lookup"><span data-stu-id="fee38-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="fee38-113">Hub eventi consente, ad esempio, il rilevamento del comportamento nelle app per dispositivi mobili, il traffico di informazioni da Web farm, l'acquisizione di eventi nei giochi per console e la raccolta di dati di telemetria da computer industriali, veicoli connessi o altri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fee38-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="fee38-114">Panoramica di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="fee38-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="fee38-115">comune ruolo dell'hub eventi nell'architettura delle soluzioni Hello è hello "porta di ingresso" per una pipeline di eventi, chiamato un *inserimento eventi*.</span><span class="sxs-lookup"><span data-stu-id="fee38-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="fee38-116">Strumento di inserimento di un evento è un componente o servizio che si trova tra i Publisher di eventi e di evento consumer toodecouple hello produzione di un flusso di eventi dal consumo hello di tali eventi.</span><span class="sxs-lookup"><span data-stu-id="fee38-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="fee38-117">Hello nella figura seguente viene illustrata questa architettura:</span><span class="sxs-lookup"><span data-stu-id="fee38-117">hello following figure depicts this architecture:</span></span>

![Hub eventi](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="fee38-119">Hub eventi offre funzionalità di gestione del flusso di messaggi, ma presenta caratteristiche diverse da quelle dei servizi di messaggistica aziendale tradizionale.</span><span class="sxs-lookup"><span data-stu-id="fee38-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="fee38-120">Le funzionalità di Hub eventi sono basate su scenari con velocità effettiva elevata ed elaborazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="fee38-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="fee38-121">Di conseguenza, hub eventi è diverso da [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaggistica e non implementa alcune delle funzionalità disponibili per hello [messaggistica del Bus di servizio](/azure/service-bus-messaging/) entità, ad esempio argomenti.</span><span class="sxs-lookup"><span data-stu-id="fee38-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="fee38-122">Funzionalità di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fee38-122">Event Hubs features</span></span>

<span data-ttu-id="fee38-123">Hub eventi contiene hello seguenti elementi chiave:</span><span class="sxs-lookup"><span data-stu-id="fee38-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="fee38-124">[**Produttori/i Publisher di eventi**](event-hubs-features.md#event-publishers): un'entità che invia l'hub di eventi tooan di dati.</span><span class="sxs-lookup"><span data-stu-id="fee38-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="fee38-125">Un evento viene pubblicato tramite AMQP 1.0 o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fee38-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="fee38-126">[**Acquisire**](event-hubs-features.md#capture): permette di hub di eventi toocapture flusso di dati e archiviarlo in un account di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="fee38-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="fee38-127">[**Partizioni**](event-hubs-features.md#partitions): Abilita tooonly ogni consumer di leggere un sottoinsieme specifico o una partizione, di hello flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="fee38-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="fee38-128">[**Token SAS**](event-hubs-features.md#sas-tokens): identifica e autentica publisher di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="fee38-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="fee38-129">[**Consumer eventi**](event-hubs-features.md#event-consumers): qualsiasi entità che legge i dati dell'evento da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fee38-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="fee38-130">I consumer eventi si connettono tramite AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="fee38-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="fee38-131">[**Gruppi di consumer**](event-hubs-features.md#consumer-groups): fornisce ogni più utilizzo applicazione con una visualizzazione distinta del flusso di eventi hello, abilitare tali tooact consumer in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="fee38-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="fee38-132">[**Unità elaborate**](event-hubs-features.md#capacity): unità di capacità pre-acquistate.</span><span class="sxs-lookup"><span data-stu-id="fee38-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="fee38-133">Una singola partizione ha una scalabilità massima di 1 unità elaborata.</span><span class="sxs-lookup"><span data-stu-id="fee38-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="fee38-134">Per informazioni tecniche dettagliate su queste e altre funzionalità di hub eventi, vedere hello [panoramica delle caratteristiche degli hub di eventi](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="fee38-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fee38-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fee38-135">Next steps</span></span>

<span data-ttu-id="fee38-136">Per informazioni dettagliate sui prezzi di Hub eventi, vedere [Hub eventi Prezzi](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="fee38-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="fee38-137">Per ulteriori informazioni sugli hub di eventi, visitare hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="fee38-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="fee38-138">Iniziare con un'[esercitazione di Hub eventi](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="fee38-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="fee38-139">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fee38-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="fee38-140">Applicazioni di esempio che usano Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fee38-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

