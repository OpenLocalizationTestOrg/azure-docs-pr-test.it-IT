---
title: Panoramica di Acquisizione di Hub eventi di Azure | Microsoft Docs
description: Acquisire i dati di telemetria con Acquisizione di Hub eventi
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="01c2d-103">Acquisizione di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="01c2d-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="01c2d-104">Acquisizione di Hub eventi di Azure consente di recapitare automaticamente i dati in streaming di Hub eventi in un account di [Archiviazione BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/) o [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) a scelta, con la possibilità di specificare un intervallo di tempo o di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="01c2d-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="01c2d-105">La configurazione di Acquisizione è rapida, non sono previsti costi amministrativi per l'esecuzione e viene ridimensionata automaticamente con le [unità elaborate](event-hubs-features.md#capacity) in Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="01c2d-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="01c2d-106">Acquisizione di Hub eventi è il modo più semplice per caricare i dati in streaming in Azure e consente di concentrarsi sull'elaborazione dei dati anziché sull'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="01c2d-107">Acquisizione di Hub eventi consente di elaborare pipeline in tempo reale e basate su batch nello stesso flusso.</span><span class="sxs-lookup"><span data-stu-id="01c2d-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="01c2d-108">Ciò significa che è possibile compilare soluzioni che si adattano alle esigenze nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="01c2d-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="01c2d-109">Sia che si debbano compilare oggi sistemi basati su batch con lo sguardo rivolto alla futura elaborazione in tempo reale o che si voglia aggiungere un percorso a freddo efficiente a una soluzione in tempo reale esistente, Acquisizione di Hub eventi semplifica l'uso dei dati in streaming.</span><span class="sxs-lookup"><span data-stu-id="01c2d-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="01c2d-110">Come funziona Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="01c2d-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="01c2d-111">Hub eventi è un buffer permanente di conservazione nel tempo per l'ingresso della telemetria, simile a un log distribuito.</span><span class="sxs-lookup"><span data-stu-id="01c2d-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="01c2d-112">La chiave per ridurre il numero di istanze di Hub eventi è il [modello di consumer partizionato](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="01c2d-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="01c2d-113">Ogni partizione è un segmento di dati indipendente e viene utilizzata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="01c2d-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="01c2d-114">Nel corso del tempo questi dati diventano obsoleti, a seconda del periodo di conservazione configurabile.</span><span class="sxs-lookup"><span data-stu-id="01c2d-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="01c2d-115">Di conseguenza, un determinato hub eventi non sarà mai "troppo pieno".</span><span class="sxs-lookup"><span data-stu-id="01c2d-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="01c2d-116">Acquisizione di Hub eventi consente di specificare un account di Archiviazione BLOB di Azure e un contenitore oppure un account Azure Data Lake Store da usare per archiviare i dati acquisiti.</span><span class="sxs-lookup"><span data-stu-id="01c2d-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="01c2d-117">Questi account possono trovarsi nella stessa area dell'hub eventi o in un'altra area, aumentando così la flessibilità della funzionalità Acquisizione di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="01c2d-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="01c2d-118">I dati acquisiti vengono scritti in formato [Apache Avro][Apache Avro], un formato compatto, rapido, binario che offre strutture di dati avanzate con lo schema inline.</span><span class="sxs-lookup"><span data-stu-id="01c2d-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="01c2d-119">Questo formato è largamente usato nell'ecosistema Hadoop, dall'analisi di flusso e da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01c2d-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="01c2d-120">Altre informazioni sull'uso di Avro sono disponibili più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="01c2d-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="01c2d-121">Acquisire windowing</span><span class="sxs-lookup"><span data-stu-id="01c2d-121">Capture windowing</span></span>

<span data-ttu-id="01c2d-122">Acquisizione di Hub eventi consente di configurare una finestra per controllare l'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="01c2d-123">Questa finestra è una dimensione minima e una configurazione a tempo con un criterio basato sulla precedenza, ovvero il primo trigger rilevato avvia un'operazione di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="01c2d-124">Se si ha una finestra di acquisizione di quindici minuti/100 MB e si invia 1 MB al secondo, la finestra della dimensione viene attivata prima della finestra temporale.</span><span class="sxs-lookup"><span data-stu-id="01c2d-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="01c2d-125">Ogni partizione acquisisce in modo indipendente e scrive un BLOB in blocchi completo al momento dell'acquisizione, denominato in base all'ora in cui è stato rilevato l'intervallo di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="01c2d-126">La convenzione di denominazione dell'archiviazione è la seguente:</span><span class="sxs-lookup"><span data-stu-id="01c2d-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="01c2d-127">Ridimensionamento alle unità elaborate</span><span class="sxs-lookup"><span data-stu-id="01c2d-127">Scaling to throughput units</span></span>

<span data-ttu-id="01c2d-128">Il traffico di Hub eventi è controllato dalle [unità elaborate](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="01c2d-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="01c2d-129">Una singola unità elaborata consente 1 MB al secondo o 1000 eventi al secondo in ingresso e il doppio in uscita.</span><span class="sxs-lookup"><span data-stu-id="01c2d-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="01c2d-130">Hub eventi Standard può essere configurato con 1-20 unità elaborate e altre possono essere acquistate con una [richiesta di supporto][support request] per l'aumento della quota.</span><span class="sxs-lookup"><span data-stu-id="01c2d-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="01c2d-131">L'uso superiore rispetto alle unità elaborate acquistate è limitato.</span><span class="sxs-lookup"><span data-stu-id="01c2d-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="01c2d-132">Acquisizione di Hub eventi copia i dati direttamente dalla memoria di Hub eventi interna, ignorando le quote in uscita di unità elaborate e salvando l'uscita per altri lettori di elaborazione, ad esempio l'analisi di flusso o Spark.</span><span class="sxs-lookup"><span data-stu-id="01c2d-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="01c2d-133">Acquisizione di Hub eventi, dopo essere stata configurata, viene eseguita automaticamente quando si invia il primo evento e continua l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="01c2d-134">Per comunicare facilmente all'elaborazione downstream che il processo è funzionante, Hub eventi scrive file vuoti quando non sono presenti dati.</span><span class="sxs-lookup"><span data-stu-id="01c2d-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="01c2d-135">Questo processo ottiene una cadenza prevedibile e un marcatore che possono alimentare i processori batch.</span><span class="sxs-lookup"><span data-stu-id="01c2d-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="01c2d-136">Configurazione di Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="01c2d-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="01c2d-137">È possibile configurare Acquisizione al momento della creazione dell'hub eventi usando il [portale di Azure](https://portal.azure.com) o i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01c2d-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="01c2d-138">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="01c2d-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="01c2d-139">Abilitare Acquisizione di Hub eventi usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="01c2d-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="01c2d-140">Creare uno spazio dei nomi di Hub eventi con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01c2d-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="01c2d-141">Esplorazione dei file acquisiti e dell'uso di Avro</span><span class="sxs-lookup"><span data-stu-id="01c2d-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="01c2d-142">Acquisizione di Hub eventi crea i file in formato Avro, come specificato nell'intervallo di tempo configurato.</span><span class="sxs-lookup"><span data-stu-id="01c2d-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="01c2d-143">È possibile visualizzare questi file con qualsiasi strumento, ad esempio [Azure Storage Explorer][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="01c2d-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="01c2d-144">È possibile scaricare i file in locale per usarli.</span><span class="sxs-lookup"><span data-stu-id="01c2d-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="01c2d-145">I file generati da Acquisizione di Hub eventi hanno lo schema Avro seguente:</span><span class="sxs-lookup"><span data-stu-id="01c2d-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="01c2d-146">Per esplorare facilmente i file di Avro, è possibile usare il file JAR [Avro Tools][Avro Tools] di Apache.</span><span class="sxs-lookup"><span data-stu-id="01c2d-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="01c2d-147">Dopo avere scaricato questo file JAR, è possibile visualizzare lo schema di un file di Avro eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01c2d-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="01c2d-148">Questo comando restituisce</span><span class="sxs-lookup"><span data-stu-id="01c2d-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="01c2d-149">È anche possibile usare Avro Tools per convertire il file in formato JSON ed eseguire altre operazioni di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="01c2d-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="01c2d-150">Per eseguire operazioni di elaborazione più avanzate, scaricare e installare Avro per la propria piattaforma.</span><span class="sxs-lookup"><span data-stu-id="01c2d-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="01c2d-151">Al momento della stesura di questo articolo, sono disponibili implementazioni per C, C++, C\#, Java, NodeJS, Perl, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="01c2d-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="01c2d-152">In Apache Avro sono disponibili guide introduttive complete per [Java][Java] e [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="01c2d-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="01c2d-153">È anche possibile leggere l'articolo [Acquisizione di Hub eventi di Azure](event-hubs-capture-python.md).</span><span class="sxs-lookup"><span data-stu-id="01c2d-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="01c2d-154">Come viene addebitato l'uso di Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="01c2d-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="01c2d-155">L'uso di Acquisizione di Hub eventi viene registrato in modo simile a quello delle unità elaborate, come tariffa oraria.</span><span class="sxs-lookup"><span data-stu-id="01c2d-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="01c2d-156">L'addebito è direttamente proporzionale al numero di unità elaborate acquistate per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="01c2d-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="01c2d-157">Quando le unità elaborate aumentano o diminuiscono, anche Acquisizione di Hub eventi aumenta o diminuisce per offrire prestazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="01c2d-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="01c2d-158">Le misurazioni vengono eseguite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="01c2d-158">The meters occur in tandem.</span></span> <span data-ttu-id="01c2d-159">Per i dettagli sui prezzi, vedere [Prezzi di Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="01c2d-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="01c2d-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01c2d-160">Next steps</span></span>

<span data-ttu-id="01c2d-161">Acquisizione di Hub eventi rappresenta il modo più facile per ottenere i dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="01c2d-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="01c2d-162">Con Azure Data Lake, Azure Data Factory e Azure HDInsight, è possibile eseguire l'elaborazione batch e altre analisi usando strumenti e piattaforme familiari a scelta con la scalabilità necessaria.</span><span class="sxs-lookup"><span data-stu-id="01c2d-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="01c2d-163">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="01c2d-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="01c2d-164">Introduzione all'invio e alla ricezione di eventi</span><span class="sxs-lookup"><span data-stu-id="01c2d-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="01c2d-165">Un'[applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="01c2d-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="01c2d-166">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="01c2d-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
