---
title: Come usare il bus di servizio di Azure con WebJobs SDK
description: Informazioni su come usare le code e gli argomenti del bus di servizio di Azure con WebJobs SDK.
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a>Come usare il bus di servizio di Azure con WebJobs SDK
## <a name="overview"></a>Panoramica
In questa guida vengono forniti esempi di codice C# che illustrano come attivare un processo quando viene ricevuto un messaggio bus di servizio Azure. Gli esempi di codice usano [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1.x.

Nella guida si presuppone che si sappia come [creare un progetto WebJob in Visual Studio con stringhe di connessione che puntano all'account di archiviazione](websites-dotnet-webjobs-sdk-get-started.md).

I frammenti di codice mostrano solo le funzioni e non il codice che crea l’oggetto `JobHost` come nel seguente esempio:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

Un [esempio di codice completo del bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) è disponibile nel repository di esempi azure-webjobs-sdk-samples in GitHub.com.

## <a id="prerequisites"></a> Prerequisiti
Per usare il bus di servizio, è necessario installare il pacchetto NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) oltre agli altri pacchetti di WebJobs SDK. 

È anche necessario impostare la stringa di connessione AzureWebJobsServiceBus oltre alle stringhe di connessione di archiviazione.  Questa operazione può essere effettuata nella sezione `connectionStrings` del file App.config, come mostrato nell'esempio seguente:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Per un progetto di esempio che include l'impostazione della stringa di connessione del bus di servizio nel file App.config, vedere l' [esempio di bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

Le stringhe di connessione possono essere impostate anche nell'ambiente di runtime di Azure, che quindi sostituisce le impostazioni di App.config quando il processo Web viene eseguito in Azure. Per altre informazioni, vedere[Introduzione a WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a> Come attivare una funzione quando viene ricevuto un messaggio di coda del bus di servizio
Per scrivere una funzione che viene chiamata da WebJobs SDK quando viene ricevuto un messaggio di coda, usare l'attributo `ServiceBusTrigger` . Il costruttore di attributo accetta un parametro che specifica il nome della coda di cui eseguire il polling.

### <a name="how-servicebustrigger-works"></a>Funzionamento di ServicebusTrigger
L'SDK riceve un messaggio in modalità `PeekLock` e chiama `Complete` sul messaggio se la funzione viene completata correttamente oppure `Abandon` se la funzione ha esito negativo. Se il tempo di esecuzione della funzione supera il timeout di `PeekLock` , il blocco viene rinnovato automaticamente.

Bus di servizio esegue la gestione della propria coda non elaborabile che non può essere controllata o configurata da WebJobs SDK. 

### <a name="string-queue-message"></a>Messaggio stringa in coda
L'esempio di codice seguente legge un messaggio in coda che contiene una stringa e scrive la stringa nel dashboard WebJobs SDK.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Nota:** se si stanno creando messaggi di coda in un'applicazione che non usa WebJobs SDK, assicurarsi di impostare [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) su "text/plain".

### <a name="poco-queue-message"></a>Messaggio POCO in coda
L'SDK deserializzerà automaticamente un messaggio di coda contenente JSON per un tipo POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)). Il seguente esempio di codice legge un messaggio di coda che contiene un oggetto `BlobInformation` con una proprietà `BlobName`:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

Per esempi di codice che illustrano come usare le proprietà del tipo POCO assieme ai BLOB e alle tabelle nella stessa funzione, vedere la [versione delle code di archiviazione in questo articolo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Se il codice che crea il messaggio in coda non utilizza WebJobs SDK, utilizzare un codice simile al seguente esempio:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Tipi con cui funziona ServiceBusTrigger
Oltre ai tipi `string` e POCO, è possibile usare l'attributo `ServiceBusTrigger` con una matrice di byte o un oggetto `BrokeredMessage`.

## <a id="create"></a> Come creare messaggi di coda del bus di servizio
Per scrivere una funzione che crea un nuovo messaggio di coda, usare l'attributo `ServiceBus` e passare il nome della coda al costruttore dell'attributo. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Creare un singolo messaggio in coda in una funzione non asincrona
L'esempio di codice seguente usa un parametro di output per creare un nuovo messaggio nella coda denominata "outputqueue" con lo stesso contenuto del messaggio ricevuto nella coda denominata "inputqueue".

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

Il parametro di output per la creazione di un singolo messaggio della coda può essere uno dei seguenti tipi:

* `string`
* `byte[]`
* `BrokeredMessage`
* Un tipo serializzabile POCO definito dall'utente. Serializzato automaticamente in formato JSON.

Per i parametri di tipo POCO, viene sempre creato un messaggio in coda quando la funzione termina; se il parametro è null, l'SDK crea un messaggio in coda che restituirà null quando il messaggio viene ricevuto e deserializzato. Per gli altri tipi, se il parametro è null non viene creato alcun messaggio in coda.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Creare più messaggi in coda o in funzioni asincrone
Per creare più messaggi, usare l'attributo `ServiceBus` con `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nel seguente esempio di codice:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Ogni messaggio di coda viene creato immediatamente quando viene chiamato il metodo `Add` .

## <a id="topics"></a>Come usare gli argomenti del bus di servizio
Per scrivere una funzione che l'SDK chiama quando viene ricevuto un messaggio su un argomento del bus di servizio, usare l'attributo `ServiceBusTrigger` con il costruttore che accetta il nome di argomento e sottoscrizione, come illustrato nel seguente esempio di codice:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

Per creare un messaggio su un argomento, usare l'attributo `ServiceBus` con un nome di argomento nello stesso modo in cui viene usato con un nome di coda.

## <a name="features-added-in-release-11"></a>Funzionalità aggiunte nella versione 1.1
Nella versione 1.1 sono state aggiunte le funzionalità seguenti:

* Personalizzazione completa dell'elaborazione dei messaggi tramite `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider` supporta la personalizzazione degli elementi `MessagingFactory` e `NamespaceManager` del bus di servizio.
* Un modello di strategia `MessageProcessor` consente di specificare un processore per ogni coda o argomento.
* La concorrenza dell'elaborazione dei messaggi è supportata per impostazione predefinita. 
* Semplicità di personalizzazione di `OnMessageOptions` tramite `ServiceBusConfiguration.MessageOptions`.
* Possibilità di specificare [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) per `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (per gli scenari in cui non si dispone di diritti di gestione). Si noti che Processi Web di Azure non è in grado di eseguire automaticamente il provisioning di code e argomenti inesistenti senza gestire AccessRights.

## <a id="queues"></a>Argomenti correlati trattati nell'articolo delle procedure per le code di archiviazione
Per informazioni sugli scenari di WebJobs SDK non specifici del bus di servizio, vedere la pagina relativa a [come usare l'archiviazione code di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Gli argomenti trattati in questo articolo includono quanto segue:

* Funzioni asincrone
* Più istanze
* Arresto normale
* Usare gli attributi di WebJobs SDK nel corpo di una funzione
* Impostare le stringhe di connessione SDK nel codice
* Impostare i valori per i parametri del costruttore WebJobs SDK nel codice
* Attivare manualmente una funzione
* Scrivere i log

## <a id="nextsteps"></a> Passaggi successivi
In questa guida sono stati forniti esempi di codice che illustrano come gestire scenari comuni per l'uso del bus di servizio di Azure. Per altre informazioni su come usare i processi Web di Azure e su WebJobs SDK, vedere le [risorse consigliate per i processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

