---
title: eventi aaaReceive dall'hub di eventi di Azure con Java | Documenti Microsoft
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
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="bd0a0-103">Ricevere eventi da Hub eventi di Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="bd0a0-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="bd0a0-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="bd0a0-104">Introduction</span></span>
<span data-ttu-id="bd0a0-105">Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="bd0a0-106">Dopo la raccolta nell'hub eventi, i dati possono essere trasformati e archiviati tramite qualsiasi provider di analisi in tempo reale o qualsiasi cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="bd0a0-107">Per ulteriori informazioni, vedere hello [Panoramica di hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="bd0a0-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="bd0a0-108">Questa esercitazione viene illustrato come gli eventi tooreceive in un hub eventi con un'applicazione console scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd0a0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd0a0-109">Prerequisites</span></span>

<span data-ttu-id="bd0a0-110">In ordine toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="bd0a0-111">Ambiente di sviluppo in Java.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-111">A Java development environment.</span></span> <span data-ttu-id="bd0a0-112">Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="bd0a0-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-113">An active Azure account.</span></span> <br/><span data-ttu-id="bd0a0-114">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="bd0a0-115">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="bd0a0-116">Ricevere messaggi con EventProcessorHost in Java</span><span class="sxs-lookup"><span data-stu-id="bd0a0-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="bd0a0-117">**EventProcessorHost** è una classe Java che semplifica la ricezione di eventi da Hub eventi tramite la gestione di checkpoint persistenti e ricezioni parallele da tali hub.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="bd0a0-118">Usando EventProcessorHost è possibile suddividere gli eventi tra più ricevitori, anche se ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="bd0a0-119">Questo esempio viene illustrato come toouse EventProcessorHost per un singolo destinatario.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="bd0a0-120">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="bd0a0-120">Create a storage account</span></span>
<span data-ttu-id="bd0a0-121">toouse EventProcessorHost, è necessario disporre di un [account di archiviazione Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="bd0a0-122">Accesso toohello [portale di Azure][Azure portal], fare clic su **+ nuovo** nella parte sinistra della schermata di hello hello.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="bd0a0-123">Fare clic su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="bd0a0-124">In hello **creare account di archiviazione** pannello, digitare un nome per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="bd0a0-125">Completare hello altri campi hello, selezionare l'area geografica desiderata e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="bd0a0-126">Fare clic su account di archiviazione hello appena creato e quindi fare clic su **Gestisci chiavi di accesso**:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="bd0a0-127">Copiare hello accesso primaria tooa chiave percorso temporaneo toouse più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="bd0a0-128">Creare un progetto Java utilizzando hello EventProcessor Host</span><span class="sxs-lookup"><span data-stu-id="bd0a0-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="bd0a0-129">Hello Java libreria client per gli hub eventi è disponibile per l'utilizzo nei progetti Maven da hello [Repository centrale Maven][Maven Package]e possono essere utilizzate con hello segue la dichiarazione di dipendenza all'interno del File di progetto di Maven:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="bd0a0-130">Per diversi tipi di ambienti di compilazione, è possibile ottenere in modo esplicito i file JAR hello più recenti rilasciato da hello [Repository centrale Maven] [ Maven Package] o da [hello punto di distribuzione di versione in GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="bd0a0-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="bd0a0-131">Per hello nel seguente esempio, creare un nuovo progetto di Maven per un'applicazione console/shell nell'ambiente di sviluppo preferita di Java.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="bd0a0-132">classe Hello viene chiamato `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="bd0a0-133">Esempio di codice seguente hello di utilizzare una nuova classe denominata toocreate `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="bd0a0-134">Creare una classe più denominata `EventProcessorSample`, usando hello il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
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
   
            System.out.println("Press enter toostop");
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
4. <span data-ttu-id="bd0a0-135">Sostituire i seguenti campi con valori di hello utilizzati durante la creazione di account di archiviazione e hub eventi hello hello.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="bd0a0-136">Questa esercitazione usa una singola istanza di EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="bd0a0-137">velocità effettiva tooincrease, è consigliabile che eseguire più istanze di EventProcessorHost, preferibilmente in computer separati.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="bd0a0-138">In questo modo si ottiene anche la ridondanza.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-138">This provides redundancy as well.</span></span> <span data-ttu-id="bd0a0-139">In questi casi, hello che diverse istanze di coordinano automaticamente tra loro in hello saldo tooload di ordine ricevuto eventi.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="bd0a0-140">Se si desidera più ricevitori tooeach processo *tutti* hello eventi, è necessario utilizzare hello **gruppo di consumer per** concetto.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="bd0a0-141">Quando si riceve eventi da computer diversi, potrebbe essere utile toospecify nomi per le istanze di EventProcessorHost in base alle macchine hello (o ruoli) in cui vengono distribuiti.</span><span class="sxs-lookup"><span data-stu-id="bd0a0-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bd0a0-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd0a0-142">Next steps</span></span>
<span data-ttu-id="bd0a0-143">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="bd0a0-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="bd0a0-144">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="bd0a0-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="bd0a0-145">[Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="bd0a0-145">[Create an Event Hub](event-hubs-create.md)</span></span>
* [<span data-ttu-id="bd0a0-146">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="bd0a0-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
