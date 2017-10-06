---
title: aaaOverview di hub di eventi di Azure Capture | Documenti Microsoft
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
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="a86c0-103">Acquisizione di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="a86c0-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="a86c0-104">Acquisizione di hub eventi Azure consente tooautomatically recapito hello flusso di dati in hub eventi tooan [archiviazione Blob di Azure](https://azure.microsoft.com/services/storage/blobs/) o [archivio Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) account desiderato, con hello una maggiore flessibilità specificare un intervallo di tempo o dimensione.</span><span class="sxs-lookup"><span data-stu-id="a86c0-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="a86c0-105">Impostazione di acquisizione è veloce, non esistono toorun i costi amministrativi e viene ridimensionato automaticamente con gli hub di eventi [unità di velocità effettiva](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="a86c0-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="a86c0-106">Acquisire gli hub eventi è tooload modo più semplice hello flusso di dati in Azure e consente toofocus sull'elaborazione dei dati anziché sull'acquisizione di dati.</span><span class="sxs-lookup"><span data-stu-id="a86c0-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="a86c0-107">Acquisire gli hub eventi permette tooprocess in tempo reale e basata su batch pipeline sul hello stesso flusso.</span><span class="sxs-lookup"><span data-stu-id="a86c0-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="a86c0-108">Ciò significa che è possibile compilare soluzioni che si adattano alle esigenze nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="a86c0-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="a86c0-109">Se si sta creando sistemi basati su batch corrente con un occhio verso futura elaborazione in tempo reale, o si desidera tooadd una soluzione di percorso freddo efficiente tooan esistente in tempo reale, acquisire gli hub eventi rende l'uso con il flusso di dati più semplici.</span><span class="sxs-lookup"><span data-stu-id="a86c0-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="a86c0-110">Come funziona Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a86c0-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="a86c0-111">Hub eventi è un buffer di durevole tempo conservazione per l'ingresso di telemetria, log distribuite a tooa simile.</span><span class="sxs-lookup"><span data-stu-id="a86c0-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="a86c0-112">Hello tooscaling chiave in hub eventi è hello [modello consumer partizionato](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="a86c0-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="a86c0-113">Ogni partizione è un segmento di dati indipendente e viene utilizzata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="a86c0-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="a86c0-114">Nel tempo che all'età di dati esterno, in base al periodo di memorizzazione configurabile hello.</span><span class="sxs-lookup"><span data-stu-id="a86c0-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="a86c0-115">Di conseguenza, un determinato hub eventi non sarà mai "troppo pieno".</span><span class="sxs-lookup"><span data-stu-id="a86c0-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="a86c0-116">Acquisizione di hub eventi consente si toospecify proprio account di archiviazione Blob di Azure e un contenitore o un account archivio Azure Data Lake, che vengono utilizzati toostore hello acquisito dati.</span><span class="sxs-lookup"><span data-stu-id="a86c0-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="a86c0-117">Questi account possono essere in hello stessa regione dell'hub eventi o in un'altra area, aggiungendo flessibilità toohello della funzionalità di acquisizione di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a86c0-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="a86c0-118">I dati acquisiti vengono scritti in formato [Apache Avro][Apache Avro], un formato compatto, rapido, binario che offre strutture di dati avanzate con lo schema inline.</span><span class="sxs-lookup"><span data-stu-id="a86c0-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="a86c0-119">Questo formato è ampiamente utilizzato ecosistema Hadoop hello flusso Analitica e Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="a86c0-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="a86c0-120">Altre informazioni sull'uso di Avro sono disponibili più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a86c0-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="a86c0-121">Acquisire windowing</span><span class="sxs-lookup"><span data-stu-id="a86c0-121">Capture windowing</span></span>

<span data-ttu-id="a86c0-122">Acquisizione di hub eventi consente tooset di acquisizione di toocontrol una finestra.</span><span class="sxs-lookup"><span data-stu-id="a86c0-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="a86c0-123">Questa finestra è una dimensione minima e la configurazione di tempo con un "primo wins criteri," vale a dire che hello eseguita trigger durante un'operazione di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="a86c0-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="a86c0-124">Se si dispone di quindici minuti, 100 MB finestra di acquisizione e inviare 1 MB al secondo, i trigger di hello dimensioni finestra prima dell'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="a86c0-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="a86c0-125">Ogni partizione acquisisce in modo indipendente e scrive un blob in blocchi completato al momento di hello dell'acquisizione, denominato per volta hello in cui hello è stata rilevata l'intervallo di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="a86c0-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="a86c0-126">convenzione di denominazione archiviazione Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="a86c0-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="a86c0-127">Unità di scala toothroughput</span><span class="sxs-lookup"><span data-stu-id="a86c0-127">Scaling toothroughput units</span></span>

<span data-ttu-id="a86c0-128">Il traffico di Hub eventi è controllato dalle [unità elaborate](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="a86c0-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="a86c0-129">Una singola unità elaborata consente 1 MB al secondo o 1000 eventi al secondo in ingresso e il doppio in uscita.</span><span class="sxs-lookup"><span data-stu-id="a86c0-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="a86c0-130">Hub eventi Standard può essere configurato con 1-20 unità elaborate e altre possono essere acquistate con una [richiesta di supporto][support request] per l'aumento della quota.</span><span class="sxs-lookup"><span data-stu-id="a86c0-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="a86c0-131">L'uso superiore rispetto alle unità elaborate acquistate è limitato.</span><span class="sxs-lookup"><span data-stu-id="a86c0-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="a86c0-132">Acquisizione di hub eventi copia i dati direttamente da archiviazione di hub eventi interno hello, ignorando le quote in uscita di unità di velocità effettiva e salvando il traffico in uscita per altri lettori di elaborazione, ad esempio flusso Analitica o Spark.</span><span class="sxs-lookup"><span data-stu-id="a86c0-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="a86c0-133">Acquisizione di Hub eventi, dopo essere stata configurata, viene eseguita automaticamente quando si invia il primo evento e continua l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a86c0-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="a86c0-134">toomake più semplice per tooknow l'elaborazione downstream che sia in esecuzione il processo di hello, hub eventi scrive file vuoti quando non sono presenti dati.</span><span class="sxs-lookup"><span data-stu-id="a86c0-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="a86c0-135">Questo processo ottiene una cadenza prevedibile e un marcatore che possono alimentare i processori batch.</span><span class="sxs-lookup"><span data-stu-id="a86c0-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="a86c0-136">Configurazione di Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a86c0-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="a86c0-137">È possibile configurare l'acquisizione al momento della creazione di hello evento hub utilizzando hello [portale di Azure](https://portal.azure.com), o utilizzando i modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a86c0-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="a86c0-138">Per ulteriori informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="a86c0-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="a86c0-139">Abilitare gli hub di eventi Capture utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a86c0-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="a86c0-140">Creare uno spazio dei nomi di Hub eventi con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a86c0-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="a86c0-141">Esplorazione file hello acquisito e l'utilizzo di Avro</span><span class="sxs-lookup"><span data-stu-id="a86c0-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="a86c0-142">Acquisire gli hub di eventi crea un file in formato Avro, come specificato nella finestra temporale hello configurato.</span><span class="sxs-lookup"><span data-stu-id="a86c0-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="a86c0-143">È possibile visualizzare questi file con qualsiasi strumento, ad esempio [Azure Storage Explorer][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="a86c0-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="a86c0-144">È possibile scaricare hello file localmente toowork su di essi.</span><span class="sxs-lookup"><span data-stu-id="a86c0-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="a86c0-145">file Hello generati da acquisire gli hub eventi sono hello seguente schema Avro:</span><span class="sxs-lookup"><span data-stu-id="a86c0-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="a86c0-146">I file Avro tooexplore un modo semplice consiste nell'utilizzare hello [Avro strumenti] [ Avro Tools] file jar di Apache.</span><span class="sxs-lookup"><span data-stu-id="a86c0-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="a86c0-147">Dopo aver scaricato il file jar, è possibile visualizzare schema hello di un file Avro specifico eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a86c0-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="a86c0-148">Questo comando restituisce</span><span class="sxs-lookup"><span data-stu-id="a86c0-148">This command returns</span></span>

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

<span data-ttu-id="a86c0-149">È inoltre possibile utilizzare strumenti Avro tooconvert hello formato tooJSON ed eseguire altre elaborazioni.</span><span class="sxs-lookup"><span data-stu-id="a86c0-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="a86c0-150">tooperform avanzati di elaborazione, scaricare e installare Avro per la scelta della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="a86c0-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="a86c0-151">In fase di hello della redazione del presente documento, sono disponibili le implementazioni per C, C++ e C\#, Java, NodeJS, Perl, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="a86c0-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="a86c0-152">In Apache Avro sono disponibili guide introduttive complete per [Java][Java] e [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="a86c0-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="a86c0-153">È inoltre possibile leggere hello [introduzione acquisire gli hub di eventi](event-hubs-capture-python.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="a86c0-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="a86c0-154">Come viene addebitato l'uso di Acquisizione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a86c0-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="a86c0-155">Acquisizione di hub eventi è a consumo Analogamente toothroughput unità: come tariffa oraria.</span><span class="sxs-lookup"><span data-stu-id="a86c0-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="a86c0-156">addebito Hello è direttamente proporzionale toohello numero di unità di velocità effettiva acquistate per spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="a86c0-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="a86c0-157">Come unità di velocità effettiva vengono aumentate e ridotte, acquisire gli hub eventi metri aumentare e diminuire tooprovide prestazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a86c0-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="a86c0-158">metri Hello si verificano in parallelo.</span><span class="sxs-lookup"><span data-stu-id="a86c0-158">hello meters occur in tandem.</span></span> <span data-ttu-id="a86c0-159">Per i dettagli sui prezzi, vedere [Prezzi di Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a86c0-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a86c0-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a86c0-160">Next steps</span></span>

<span data-ttu-id="a86c0-161">Acquisire gli hub eventi è più semplice modo tooget dati hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="a86c0-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="a86c0-162">Con Azure Data Lake, Azure Data Factory e Azure HDInsight, è possibile eseguire l'elaborazione batch e altre analisi usando strumenti e piattaforme familiari a scelta con la scalabilità necessaria.</span><span class="sxs-lookup"><span data-stu-id="a86c0-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="a86c0-163">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a86c0-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a86c0-164">Introduzione all'invio e alla ricezione di eventi</span><span class="sxs-lookup"><span data-stu-id="a86c0-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="a86c0-165">Un'[applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="a86c0-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="a86c0-166">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a86c0-166">[Event Hubs overview][Event Hubs overview]</span></span>

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
