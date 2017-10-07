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
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Ricevere eventi da Hub eventi di Azure usando Java


## <a name="introduction"></a>Introduzione
Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni. Dopo la raccolta nell'hub eventi, i dati possono essere trasformati e archiviati tramite qualsiasi provider di analisi in tempo reale o qualsiasi cluster di archiviazione.

Per ulteriori informazioni, vedere hello [Panoramica di hub eventi][Event Hubs overview].

Questa esercitazione viene illustrato come gli eventi tooreceive in un hub eventi con un'applicazione console scritta in Java.

## <a name="prerequisites"></a>Prerequisiti

In ordine toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* Ambiente di sviluppo in Java. Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).
* Un account Azure attivo. <br/>Se non si ha un account, è possibile creare un account gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Ricevere messaggi con EventProcessorHost in Java

**EventProcessorHost** è una classe Java che semplifica la ricezione di eventi da Hub eventi tramite la gestione di checkpoint persistenti e ricezioni parallele da tali hub. Usando EventProcessorHost è possibile suddividere gli eventi tra più ricevitori, anche se ospitati in nodi diversi. Questo esempio viene illustrato come toouse EventProcessorHost per un singolo destinatario.

### <a name="create-a-storage-account"></a>Creare un account di archiviazione
toouse EventProcessorHost, è necessario disporre di un [account di archiviazione Azure][Azure Storage account]:

1. Accesso toohello [portale di Azure][Azure portal], fare clic su **+ nuovo** nella parte sinistra della schermata di hello hello.
2. Fare clic su **Archiviazione** e quindi su **Account di archiviazione**. In hello **creare account di archiviazione** pannello, digitare un nome per l'account di archiviazione hello. Completare hello altri campi hello, selezionare l'area geografica desiderata e quindi fare clic su **crea**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Fare clic su account di archiviazione hello appena creato e quindi fare clic su **Gestisci chiavi di accesso**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Copiare hello accesso primaria tooa chiave percorso temporaneo toouse più avanti in questa esercitazione.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Creare un progetto Java utilizzando hello EventProcessor Host
Hello Java libreria client per gli hub eventi è disponibile per l'utilizzo nei progetti Maven da hello [Repository centrale Maven][Maven Package]e possono essere utilizzate con hello segue la dichiarazione di dipendenza all'interno del File di progetto di Maven:    

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

Per diversi tipi di ambienti di compilazione, è possibile ottenere in modo esplicito i file JAR hello più recenti rilasciato da hello [Repository centrale Maven] [ Maven Package] o da [hello punto di distribuzione di versione in GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Per hello nel seguente esempio, creare un nuovo progetto di Maven per un'applicazione console/shell nell'ambiente di sviluppo preferita di Java. classe Hello viene chiamato `ErrorNotificationHandler`.     
   
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
2. Esempio di codice seguente hello di utilizzare una nuova classe denominata toocreate `EventProcessor`.
   
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
3. Creare una classe più denominata `EventProcessorSample`, usando hello il codice seguente.
   
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
4. Sostituire i seguenti campi con valori di hello utilizzati durante la creazione di account di archiviazione e hub eventi hello hello.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Questa esercitazione usa una singola istanza di EventProcessorHost. velocità effettiva tooincrease, è consigliabile che eseguire più istanze di EventProcessorHost, preferibilmente in computer separati.  In questo modo si ottiene anche la ridondanza. In questi casi, hello che diverse istanze di coordinano automaticamente tra loro in hello saldo tooload di ordine ricevuto eventi. Se si desidera più ricevitori tooeach processo *tutti* hello eventi, è necessario utilizzare hello **gruppo di consumer per** concetto. Quando si riceve eventi da computer diversi, potrebbe essere utile toospecify nomi per le istanze di EventProcessorHost in base alle macchine hello (o ruoli) in cui vengono distribuiti.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
