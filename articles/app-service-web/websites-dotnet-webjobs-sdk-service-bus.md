---
title: aaaHow toouse Azure Service Bus con hello WebJobs SDK
description: Informazioni su come toouse Azure Service Bus code e argomenti con hello WebJobs SDK.
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
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Come toouse del Bus di servizio di Azure con hello WebJobs SDK
## <a name="overview"></a>Panoramica
Questa guida fornisce c# degli esempi di codice che mostrano come tootrigger un processo quando viene ricevuto un messaggio di Service Bus di Azure. utilizzo di esempi di codice Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.

Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md).

frammenti di codice Hello mostrano solo le funzioni, hello non codice che crea hello `JobHost` oggetto come nel seguente esempio:

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

Oggetto [esempio di codice completo di Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) nel repository di processi Web di azure-esempi di sdk hello in GitHub.com.

## <a id="prerequisites"></a> Prerequisiti
toowork con il Bus di servizio è hello tooinstall [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet è pacchetto inoltre toohello altri pacchetti WebJobs SDK. 

È anche una stringa di connessione tooset hello AzureWebJobsServiceBus nelle stringhe di connessione di archiviazione toohello aggiunta.  È possibile farlo in hello `connectionStrings` sezione del file app. config hello, come illustrato nell'esempio seguente hello:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Per un progetto di esempio che include l'impostazione della stringa di connessione hello Bus di servizio nel file app. config hello, vedere [esempio Bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

le stringhe di connessione Hello possono essere impostate anche nell'ambiente di runtime di Azure hello, che quindi esegue l'override delle impostazioni di App. config hello quando hello processo Web in esecuzione in Azure; Per ulteriori informazioni, vedere [introduzione hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Modalità di ricevimento tootrigger una funzione quando un Bus di servizio coda messaggi
chiama una funzione che hello WebJobs SDK toowrite quando viene ricevuto un messaggio nella coda, utilizzare hello `ServiceBusTrigger` attributo. costruttore di attributo Hello accetta un parametro che specifica il nome di hello di hello coda toopoll.

### <a name="how-servicebustrigger-works"></a>Funzionamento di ServicebusTrigger
SDK Hello riceve un messaggio in `PeekLock` modalità e le chiamate `Complete` messaggio hello se la funzione hello viene completata correttamente o chiamate `Abandon` se hello funzione ha esito negativo. Se la funzione hello viene eseguito più di hello `PeekLock` timeout blocco hello viene rinnovato automaticamente.

Bus di servizio esegue la gestione di coda non elaborabile che non può essere controllata o configurata da hello WebJobs SDK. 

### <a name="string-queue-message"></a>Messaggio stringa in coda
Hello nell'esempio di codice seguente legge un messaggio nella coda che contiene una stringa e scrive toohello stringa hello dashboard WebJobs SDK.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Nota:** se si sta creando coda messaggi hello in un'applicazione che non utilizza hello WebJobs SDK, assicurarsi che tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) troppo "text/plain".

### <a name="poco-queue-message"></a>Messaggio POCO in coda
Hello SDK eseguirà automaticamente la deserializzazione di un messaggio nella coda che contiene JSON per un POCO [(Plain vecchio oggetto CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo. esempio di codice seguente Hello legge un messaggio nella coda che contiene un `BlobInformation` oggetto che ha un `BlobName` proprietà:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Per esempi di codice che illustra come proprietà toouse di hello POCO toowork con BLOB e tabelle in hello stessa funzione, vedere hello [versione di code di archiviazione di questo articolo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Se il codice che crea il messaggio di coda hello non usa hello WebJobs SDK, usare toohello simili di codice riportato di seguito:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Tipi con cui funziona ServiceBusTrigger
Oltre a `string` e tipi di POCO, è possibile utilizzare hello `ServiceBusTrigger` attributo con una matrice di byte o un `BrokeredMessage` oggetto.

## <a id="create"></a>Accoda i messaggi come toocreate Bus di servizio
una funzione che crea un nuovo messaggio nella coda toowrite utilizzare hello `ServiceBus` attributo e passarlo al costruttore di attributo toohello nome coda hello. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Creare un singolo messaggio in coda in una funzione non asincrona
Hello nell'esempio di codice seguente viene utilizzato un toocreate di parametro di output un nuovo messaggio nella coda di hello denominato "outputqueue" con stesso contenuto come hello messaggio ricevuto nella coda di hello denominata "inputqueue" hello.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

parametro di output di Hello per la creazione di un messaggio nella coda singola può essere uno dei seguenti tipi di hello:

* `string`
* `byte[]`
* `BrokeredMessage`
* Un tipo serializzabile POCO definito dall'utente. Serializzato automaticamente in formato JSON.

Per i parametri di tipo POCO, un messaggio nella coda viene sempre creato quando si termina la funzione hello; Se il parametro hello è null, hello SDK crea un messaggio nella coda che verrà restituito null quando il messaggio hello viene ricevuto e deserializzato. Per altri tipi di hello, se il parametro hello è null non viene creato alcun messaggio di coda.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Creare più messaggi in coda o in funzioni asincrone
toocreate più messaggi, utilizzare hello `ServiceBus` attributo con `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nel seguente esempio di codice hello:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Ogni messaggio della coda viene creato immediatamente quando hello `Add` metodo viene chiamato.

## <a id="topics"></a>Come toowork con gli argomenti del Bus di servizio
chiama una funzione che hello SDK toowrite quando viene ricevuto un messaggio in un argomento del Bus di servizio, utilizzare hello `ServiceBusTrigger` attributo con il costruttore hello che accetta il nome dell'argomento e il nome della sottoscrizione, come illustrato nel seguente esempio di codice hello:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

un messaggio su un argomento, utilizzare hello toocreate `ServiceBus` stesso attributo con un hello nome argomento modalità di utilizzo con un nome di coda.

## <a name="features-added-in-release-11"></a>Funzionalità aggiunte nella versione 1.1
Nella versione 1.1, sono state aggiunte Hello seguenti caratteristiche:

* Personalizzazione completa dell'elaborazione dei messaggi tramite `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`supporta la personalizzazione del Bus di servizio hello `MessagingFactory` e `NamespaceManager`.
* Oggetto `MessageProcessor` criterio strategia permette toospecify un processore per ogni coda o un argomento.
* La concorrenza dell'elaborazione dei messaggi è supportata per impostazione predefinita. 
* Semplicità di personalizzazione di `OnMessageOptions` tramite `ServiceBusConfiguration.MessageOptions`.
* Consenti [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specificato in `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (per gli scenari in cui non si dispone di diritti di gestione). Si noti che i processi Web di Azure è tooautomatically non è possibile eseguire il provisioning inesistente code e argomenti senza gestire AccessRights.

## <a id="queues"></a>Argomenti correlati coperti da code di archiviazione hello come-tooarticle
Per informazioni sugli scenari di WebJobs SDK non specifiche tooService Bus, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Gli argomenti trattati in tale articolo includono hello informazioni seguenti:

* Funzioni asincrone
* Più istanze
* Arresto normale
* Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione
* Impostare le stringhe di connessione SDK hello nel codice
* Impostare i valori per i parametri del costruttore WebJobs SDK nel codice
* Attivare manualmente una funzione
* Scrivere i log

## <a id="nextsteps"></a> Passaggi successivi
Questa guida è fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di Azure Service Bus. Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

