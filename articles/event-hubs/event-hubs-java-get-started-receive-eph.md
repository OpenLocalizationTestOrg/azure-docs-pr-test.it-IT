---
title: Ricevere eventi da Hub eventi di Azure usando Java | Microsoft Docs
description: Guida introduttiva alla ricezione da Hub eventi usando Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="5dc40-103">Ricevere eventi da Hub eventi di Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="5dc40-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="5dc40-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5dc40-104">Introduction</span></span>
<span data-ttu-id="5dc40-105">Hub eventi è un sistema di inserimento a scalabilità elevata, in grado di inserire milioni di eventi al secondo, che permette a un'applicazione di elaborare e analizzare le elevate quantità di dati prodotti dalle applicazioni e dai dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="5dc40-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="5dc40-106">Dopo la raccolta nell'hub eventi, i dati possono essere trasformati e archiviati tramite qualsiasi provider di analisi in tempo reale o qualsiasi cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5dc40-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="5dc40-107">Per altre informazioni, vedere [Panoramica di Hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="5dc40-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="5dc40-108">Questa esercitazione illustra come ricevere eventi in un Hub eventi usando un'applicazione console scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="5dc40-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dc40-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5dc40-109">Prerequisites</span></span>

<span data-ttu-id="5dc40-110">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5dc40-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="5dc40-111">Ambiente di sviluppo in Java.</span><span class="sxs-lookup"><span data-stu-id="5dc40-111">A Java development environment.</span></span> <span data-ttu-id="5dc40-112">Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="5dc40-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="5dc40-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="5dc40-113">An active Azure account.</span></span> <br/><span data-ttu-id="5dc40-114">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5dc40-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="5dc40-115">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="5dc40-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="5dc40-116">Ricevere messaggi con EventProcessorHost in Java</span><span class="sxs-lookup"><span data-stu-id="5dc40-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="5dc40-117">**EventProcessorHost** è una classe Java che semplifica la ricezione di eventi da Hub eventi tramite la gestione di checkpoint persistenti e ricezioni parallele da tali hub.</span><span class="sxs-lookup"><span data-stu-id="5dc40-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="5dc40-118">Usando EventProcessorHost è possibile suddividere gli eventi tra più ricevitori, anche se ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="5dc40-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="5dc40-119">Questo esempio illustra come usare EventProcessorHost per un ricevitore singolo.</span><span class="sxs-lookup"><span data-stu-id="5dc40-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="5dc40-120">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5dc40-120">Create a storage account</span></span>
<span data-ttu-id="5dc40-121">Per usare EventProcessorHost, è necessario un [account di archiviazione di Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="5dc40-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="5dc40-122">Accedere al [portale di Azure][Azure portal] e fare clic su **+ Nuovo** nella parte sinistra della schermata.</span><span class="sxs-lookup"><span data-stu-id="5dc40-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="5dc40-123">Fare clic su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="5dc40-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="5dc40-124">Nel pannello **Crea account di archiviazione** digitare un nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5dc40-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="5dc40-125">Completare il resto dei campi, selezionare l'area geografica desiderata e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5dc40-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="5dc40-126">Fare clic sull'account di archiviazione appena creato e quindi su **Gestisci chiavi di accesso**:</span><span class="sxs-lookup"><span data-stu-id="5dc40-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="5dc40-127">Copiare la chiave di accesso primaria in una posizione temporanea per usarla più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5dc40-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="5dc40-128">Creare un progetto Java usando EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="5dc40-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="5dc40-129">La libreria client Java per Hub eventi è disponibile per l'uso nei progetti Maven dal [Repository centrale di Maven][Maven Package]ed è possibile farvi riferimento usando la seguente dichiarazione di dipendenza all'interno del file di progetto Maven:</span><span class="sxs-lookup"><span data-stu-id="5dc40-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="5dc40-130">Per diversi tipi di ambienti di compilazione, è possibile ottenere in modo esplicito i file JAR rilasciati più recenti dal [repository centrale Maven][Maven Package] o dal [punto di distribuzione rilascio in GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="5dc40-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="5dc40-131">Per l'esempio seguente, creare prima un nuovo progetto Maven per un'applicazione console/shell nell'ambiente di sviluppo Java preferito.</span><span class="sxs-lookup"><span data-stu-id="5dc40-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="5dc40-132">La classe è denominata `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="5dc40-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="5dc40-133">Usare il codice seguente per creare una nuova classe denominata `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="5dc40-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="5dc40-134">Creare un'altra classe denominata `EventProcessorSample` usando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="5dc40-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="5dc40-135">Sostituire i campi seguenti con i valori usati durante la creazione dell'Hub eventi e dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5dc40-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="5dc40-136">Questa esercitazione usa una singola istanza di EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="5dc40-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="5dc40-137">Per aumentare la velocità effettiva è consigliabile eseguire più istanze di EventProcessorHost, preferibilmente in computer separati.</span><span class="sxs-lookup"><span data-stu-id="5dc40-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="5dc40-138">In questo modo si ottiene anche la ridondanza.</span><span class="sxs-lookup"><span data-stu-id="5dc40-138">This provides redundancy as well.</span></span> <span data-ttu-id="5dc40-139">In questi casi, le varie istanze si coordinano automaticamente tra loro per ottenere il bilanciamento del carico relativo agli eventi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="5dc40-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="5dc40-140">Se si vuole che ognuno dei vari ricevitori elabori *tutti* gli eventi, è necessario usare il concetto **ConsumerGroup** .</span><span class="sxs-lookup"><span data-stu-id="5dc40-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="5dc40-141">Quando si ricevono eventi da più macchine, potrebbe risultare utile specificare nomi per le istanze di EventProcessorHost in base alle macchine (o ai ruoli) in cui sono distribuite.</span><span class="sxs-lookup"><span data-stu-id="5dc40-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5dc40-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5dc40-142">Next steps</span></span>
<span data-ttu-id="5dc40-143">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5dc40-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="5dc40-144">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="5dc40-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="5dc40-145">[Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="5dc40-145">[Create an Event Hub](event-hubs-create.md)</span></span>
* [<span data-ttu-id="5dc40-146">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="5dc40-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
