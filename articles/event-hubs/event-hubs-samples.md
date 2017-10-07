---
title: esempi di hub eventi aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="a4e02-103">Esempi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-103">Event Hubs samples</span></span> 

<span data-ttu-id="a4e02-104">set di esempi di hub eventi di Azure Hello illustra le funzionalità chiave di [hub eventi di Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a4e02-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="a4e02-105">In questo articolo vengono suddivisi in categorie e vengono illustrati alcuni esempi di hello disponibili, con collegamenti tooeach.</span><span class="sxs-lookup"><span data-stu-id="a4e02-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="a4e02-106">In fase di hello della redazione del presente documento, gli esempi di hub eventi si trovano in varie posizioni:</span><span class="sxs-lookup"><span data-stu-id="a4e02-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="a4e02-107">Esempi di codice per sviluppatori MSDN</span><span class="sxs-lookup"><span data-stu-id="a4e02-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="a4e02-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="a4e02-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="a4e02-109">Per ulteriori informazioni sulle diverse versioni di .NET Framework hello, vedere [Framework e le destinazioni](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="a4e02-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="a4e02-110">Altri esempi saranno aggiunti in seguito, è consigliabile quindi controllare spesso gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a4e02-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="a4e02-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="a4e02-111">.NET Standard</span></span>

<span data-ttu-id="a4e02-112">Hello seguenti esempi illustrano come toosend e ricevere gli eventi utilizzando hello [client hub eventi](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) per hello [libreria .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="a4e02-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="a4e02-113">Inviare eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-113">Send events</span></span> 

<span data-ttu-id="a4e02-114">Hello [iniziare l'invio di](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) esempio viene illustrato come un .NET Core toowrite console applicazione che invia l'hub di eventi tooan di eventi.</span><span class="sxs-lookup"><span data-stu-id="a4e02-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="a4e02-115">Ricevere eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-115">Receive events</span></span> 

<span data-ttu-id="a4e02-116">Hello [introduzione di ricezione con hello Host processore di eventi](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) esempio è un'applicazione console .NET Core che riceve i messaggi da un hub di eventi utilizzando hello Host processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="a4e02-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="a4e02-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a4e02-117">.NET Framework</span></span>   

<span data-ttu-id="a4e02-118">Questi esempi illustrano altre funzionalità di hub di eventi di Azure, destinazione hello [libreria .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="a4e02-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="a4e02-119">Inviare notifiche agli utenti sugli eventi ricevuti</span><span class="sxs-lookup"><span data-stu-id="a4e02-119">Notify users of events received</span></span>

<span data-ttu-id="a4e02-120">Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) esempio notifica agli utenti dei dati ricevuti da sensori o altri sistemi.</span><span class="sxs-lookup"><span data-stu-id="a4e02-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="a4e02-121">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="a4e02-122">Hello [evento hub Guida introduttiva](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) illustra le funzionalità di base hello degli hub di eventi, ad esempio come inviare l'hub di eventi eventi tooan toocreate un hub di eventi e utilizzare gli eventi utilizzando hello [Hostprocessoredieventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="a4e02-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="a4e02-123">Elaborazione di eventi con aumento delle istanze</span><span class="sxs-lookup"><span data-stu-id="a4e02-123">Scale out event processing</span></span> 

<span data-ttu-id="a4e02-124">Hello [scalabilità l'elaborazione di eventi](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) esempio viene illustrato come hello toouse [Host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) il carico di lavoro di toodistribute hello del consumo di flusso di hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a4e02-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="a4e02-125">Viene illustrato come hello tooimplement **EventProcessor** e **EventProcessorFactory** flusso di eventi oggetti toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="a4e02-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="a4e02-126">Estrazione dei dati da SQL a un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="a4e02-127">Hello [dati pull SQL](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) esempio viene illustrato come toopull dati da un database SQL di tabella e spingono hub eventi tooan, toouse come input in applicazioni analitiche a valle.</span><span class="sxs-lookup"><span data-stu-id="a4e02-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="a4e02-128">Estrarre i dati web in un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="a4e02-129">Hello [importare dati dal web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) esempio viene illustrato come dati toopull da public feed (ad esempio le informazioni sul traffico del reparto di trasporto feed hello) e inviare tooan hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="a4e02-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4e02-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4e02-130">Next steps</span></span>

<span data-ttu-id="a4e02-131">Per ulteriori informazioni sulle versioni di .NET Framework, visitare hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a4e02-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="a4e02-132">Framework e destinazioni</span><span class="sxs-lookup"><span data-stu-id="a4e02-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="a4e02-133">.NET Framework 4.6 e 4.5</span><span class="sxs-lookup"><span data-stu-id="a4e02-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="a4e02-134">È possibile ottenere altre informazioni sugli hub di eventi in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="a4e02-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="a4e02-135">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="a4e02-136">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="a4e02-137">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a4e02-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)