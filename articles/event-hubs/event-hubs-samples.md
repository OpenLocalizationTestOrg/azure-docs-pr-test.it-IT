---
title: Esempi di Hub eventi di Azure | Microsoft Docs
description: Esempi di Hub eventi di Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="00712-103">Esempi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-103">Event Hubs samples</span></span> 

<span data-ttu-id="00712-104">Il set di esempi di Hub eventi di Azure illustra le funzionalità principali di [Hub eventi di Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="00712-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="00712-105">Questo articolo suddivide gli esempi disponibili in categorie e fornisce una descrizione e un collegamento a ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="00712-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="00712-106">Al momento della stesura di questo articolo, gli esempi di Hub eventi si trovano in diverse posizioni:</span><span class="sxs-lookup"><span data-stu-id="00712-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="00712-107">Esempi di codice per sviluppatori MSDN</span><span class="sxs-lookup"><span data-stu-id="00712-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="00712-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="00712-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="00712-109">Per altre informazioni sulle diverse versioni di .NET Framework, vedere [Frameworks and Targets](/dotnet/articles/standard/frameworks) (Framework e destinazioni).</span><span class="sxs-lookup"><span data-stu-id="00712-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="00712-110">Altri esempi saranno aggiunti in seguito, è consigliabile quindi controllare spesso gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="00712-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="00712-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="00712-111">.NET Standard</span></span>

<span data-ttu-id="00712-112">Negli esempi seguenti viene illustrato come inviare e ricevere eventi tramite il [client di Hub eventi](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) per la [libreria .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="00712-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="00712-113">Inviare eventi</span><span class="sxs-lookup"><span data-stu-id="00712-113">Send events</span></span> 

<span data-ttu-id="00712-114">L'esempio per la [guida introduttiva all'invio](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) illustra come scrivere un'applicazione console .NET Core che invii gli eventi a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="00712-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="00712-115">Ricevere eventi</span><span class="sxs-lookup"><span data-stu-id="00712-115">Receive events</span></span> 

<span data-ttu-id="00712-116">L'esempio [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) (Guida introduttiva alla ricezione con l'host processore di eventi) è un'applicazione console .NET Core che riceve i messaggi da un hub eventi usando l'host processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="00712-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="00712-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="00712-117">.NET Framework</span></span>   

<span data-ttu-id="00712-118">Questi esempi illustrano altre funzionalità di Hub eventi di Azure, indirizzati alla [libreria .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="00712-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="00712-119">Inviare notifiche agli utenti sugli eventi ricevuti</span><span class="sxs-lookup"><span data-stu-id="00712-119">Notify users of events received</span></span>

<span data-ttu-id="00712-120">L'esempio [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) invia notifiche agli utenti sui dati ricevuti dai sensori o da altri sistemi.</span><span class="sxs-lookup"><span data-stu-id="00712-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="00712-121">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="00712-122">L'esempio per l'[introduzione a Hub eventi](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) illustra le funzionalità di base di Hub eventi, come la creazione di un hub eventi, l'invio di eventi a un hub eventi e l'uso di eventi tramite l'[host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="00712-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="00712-123">Elaborazione di eventi con aumento delle istanze</span><span class="sxs-lookup"><span data-stu-id="00712-123">Scale out event processing</span></span> 

<span data-ttu-id="00712-124">L'esempio sull'[elaborazione di eventi con aumento delle istanze](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) illustra come usare l'[Host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) per distribuire il carico di lavoro del consumo di flusso di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="00712-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="00712-125">Viene illustrato come implementare gli oggetti **EventProcessor** e **EventProcessorFactory** per gestire il flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="00712-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="00712-126">Estrazione dei dati da SQL a un hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="00712-127">L'esempio sull'[estrazione dei dati SQL](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) illustra come estrarre i dati da una tabella SQL e inserirli in un hub eventi, da usare come input per applicazioni analitiche downstream.</span><span class="sxs-lookup"><span data-stu-id="00712-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="00712-128">Estrarre i dati web in un hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="00712-129">L'esempio sull'[importazione dei dati dal web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) illustra come estrarre i dati dai feed pubblici (ad esempio, i feed di informazioni sul traffico dal dipartimento dei trasporti) e inserirli in un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="00712-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00712-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00712-130">Next steps</span></span>

<span data-ttu-id="00712-131">Per altre informazioni sulle versioni .NET Framework visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="00712-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="00712-132">Framework e destinazioni</span><span class="sxs-lookup"><span data-stu-id="00712-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="00712-133">.NET Framework 4.6 e 4.5</span><span class="sxs-lookup"><span data-stu-id="00712-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="00712-134">Per altre informazioni su Hub eventi consultare i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="00712-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="00712-135">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="00712-136">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="00712-137">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="00712-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)