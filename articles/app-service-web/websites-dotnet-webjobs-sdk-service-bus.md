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
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="ab30c-103">Come toouse del Bus di servizio di Azure con hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="ab30c-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="ab30c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ab30c-104">Overview</span></span>
<span data-ttu-id="ab30c-105">Questa guida fornisce c# degli esempi di codice che mostrano come tootrigger un processo quando viene ricevuto un messaggio di Service Bus di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab30c-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="ab30c-106">utilizzo di esempi di codice Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.</span><span class="sxs-lookup"><span data-stu-id="ab30c-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="ab30c-107">Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab30c-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="ab30c-108">frammenti di codice Hello mostrano solo le funzioni, hello non codice che crea hello `JobHost` oggetto come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="ab30c-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="ab30c-109">Oggetto [esempio di codice completo di Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) nel repository di processi Web di azure-esempi di sdk hello in GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="ab30c-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="ab30c-110"><a id="prerequisites"></a> Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab30c-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="ab30c-111">toowork con il Bus di servizio è hello tooinstall [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet è pacchetto inoltre toohello altri pacchetti WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="ab30c-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="ab30c-112">È anche una stringa di connessione tooset hello AzureWebJobsServiceBus nelle stringhe di connessione di archiviazione toohello aggiunta.</span><span class="sxs-lookup"><span data-stu-id="ab30c-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="ab30c-113">È possibile farlo in hello `connectionStrings` sezione del file app. config hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ab30c-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="ab30c-114">Per un progetto di esempio che include l'impostazione della stringa di connessione hello Bus di servizio nel file app. config hello, vedere [esempio Bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="ab30c-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="ab30c-115">le stringhe di connessione Hello possono essere impostate anche nell'ambiente di runtime di Azure hello, che quindi esegue l'override delle impostazioni di App. config hello quando hello processo Web in esecuzione in Azure; Per ulteriori informazioni, vedere [introduzione hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ab30c-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="ab30c-116"><a id="trigger"></a>Modalità di ricevimento tootrigger una funzione quando un Bus di servizio coda messaggi</span><span class="sxs-lookup"><span data-stu-id="ab30c-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="ab30c-117">chiama una funzione che hello WebJobs SDK toowrite quando viene ricevuto un messaggio nella coda, utilizzare hello `ServiceBusTrigger` attributo.</span><span class="sxs-lookup"><span data-stu-id="ab30c-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="ab30c-118">costruttore di attributo Hello accetta un parametro che specifica il nome di hello di hello coda toopoll.</span><span class="sxs-lookup"><span data-stu-id="ab30c-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="ab30c-119">Funzionamento di ServicebusTrigger</span><span class="sxs-lookup"><span data-stu-id="ab30c-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="ab30c-120">SDK Hello riceve un messaggio in `PeekLock` modalità e le chiamate `Complete` messaggio hello se la funzione hello viene completata correttamente o chiamate `Abandon` se hello funzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ab30c-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="ab30c-121">Se la funzione hello viene eseguito più di hello `PeekLock` timeout blocco hello viene rinnovato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ab30c-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="ab30c-122">Bus di servizio esegue la gestione di coda non elaborabile che non può essere controllata o configurata da hello WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="ab30c-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="ab30c-123">Messaggio stringa in coda</span><span class="sxs-lookup"><span data-stu-id="ab30c-123">String queue message</span></span>
<span data-ttu-id="ab30c-124">Hello nell'esempio di codice seguente legge un messaggio nella coda che contiene una stringa e scrive toohello stringa hello dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="ab30c-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="ab30c-125">**Nota:** se si sta creando coda messaggi hello in un'applicazione che non utilizza hello WebJobs SDK, assicurarsi che tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) troppo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="ab30c-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="ab30c-126">Messaggio POCO in coda</span><span class="sxs-lookup"><span data-stu-id="ab30c-126">POCO queue message</span></span>
<span data-ttu-id="ab30c-127">Hello SDK eseguirà automaticamente la deserializzazione di un messaggio nella coda che contiene JSON per un POCO [(Plain vecchio oggetto CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo.</span><span class="sxs-lookup"><span data-stu-id="ab30c-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="ab30c-128">esempio di codice seguente Hello legge un messaggio nella coda che contiene un `BlobInformation` oggetto che ha un `BlobName` proprietà:</span><span class="sxs-lookup"><span data-stu-id="ab30c-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="ab30c-129">Per esempi di codice che illustra come proprietà toouse di hello POCO toowork con BLOB e tabelle in hello stessa funzione, vedere hello [versione di code di archiviazione di questo articolo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="ab30c-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="ab30c-130">Se il codice che crea il messaggio di coda hello non usa hello WebJobs SDK, usare toohello simili di codice riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ab30c-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="ab30c-131">Tipi con cui funziona ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="ab30c-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="ab30c-132">Oltre a `string` e tipi di POCO, è possibile utilizzare hello `ServiceBusTrigger` attributo con una matrice di byte o un `BrokeredMessage` oggetto.</span><span class="sxs-lookup"><span data-stu-id="ab30c-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="ab30c-133"><a id="create"></a>Accoda i messaggi come toocreate Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ab30c-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="ab30c-134">una funzione che crea un nuovo messaggio nella coda toowrite utilizzare hello `ServiceBus` attributo e passarlo al costruttore di attributo toohello nome coda hello.</span><span class="sxs-lookup"><span data-stu-id="ab30c-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="ab30c-135">Creare un singolo messaggio in coda in una funzione non asincrona</span><span class="sxs-lookup"><span data-stu-id="ab30c-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="ab30c-136">Hello nell'esempio di codice seguente viene utilizzato un toocreate di parametro di output un nuovo messaggio nella coda di hello denominato "outputqueue" con stesso contenuto come hello messaggio ricevuto nella coda di hello denominata "inputqueue" hello.</span><span class="sxs-lookup"><span data-stu-id="ab30c-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="ab30c-137">parametro di output di Hello per la creazione di un messaggio nella coda singola può essere uno dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="ab30c-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="ab30c-138">Un tipo serializzabile POCO definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ab30c-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="ab30c-139">Serializzato automaticamente in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ab30c-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="ab30c-140">Per i parametri di tipo POCO, un messaggio nella coda viene sempre creato quando si termina la funzione hello; Se il parametro hello è null, hello SDK crea un messaggio nella coda che verrà restituito null quando il messaggio hello viene ricevuto e deserializzato.</span><span class="sxs-lookup"><span data-stu-id="ab30c-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="ab30c-141">Per altri tipi di hello, se il parametro hello è null non viene creato alcun messaggio di coda.</span><span class="sxs-lookup"><span data-stu-id="ab30c-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="ab30c-142">Creare più messaggi in coda o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="ab30c-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="ab30c-143">toocreate più messaggi, utilizzare hello `ServiceBus` attributo con `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nel seguente esempio di codice hello:</span><span class="sxs-lookup"><span data-stu-id="ab30c-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="ab30c-144">Ogni messaggio della coda viene creato immediatamente quando hello `Add` metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="ab30c-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="ab30c-145"><a id="topics"></a>Come toowork con gli argomenti del Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ab30c-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="ab30c-146">chiama una funzione che hello SDK toowrite quando viene ricevuto un messaggio in un argomento del Bus di servizio, utilizzare hello `ServiceBusTrigger` attributo con il costruttore hello che accetta il nome dell'argomento e il nome della sottoscrizione, come illustrato nel seguente esempio di codice hello:</span><span class="sxs-lookup"><span data-stu-id="ab30c-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="ab30c-147">un messaggio su un argomento, utilizzare hello toocreate `ServiceBus` stesso attributo con un hello nome argomento modalità di utilizzo con un nome di coda.</span><span class="sxs-lookup"><span data-stu-id="ab30c-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="ab30c-148">Funzionalità aggiunte nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="ab30c-148">Features added in release 1.1</span></span>
<span data-ttu-id="ab30c-149">Nella versione 1.1, sono state aggiunte Hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="ab30c-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="ab30c-150">Personalizzazione completa dell'elaborazione dei messaggi tramite `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="ab30c-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="ab30c-151">`MessagingProvider`supporta la personalizzazione del Bus di servizio hello `MessagingFactory` e `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="ab30c-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="ab30c-152">Oggetto `MessageProcessor` criterio strategia permette toospecify un processore per ogni coda o un argomento.</span><span class="sxs-lookup"><span data-stu-id="ab30c-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="ab30c-153">La concorrenza dell'elaborazione dei messaggi è supportata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ab30c-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="ab30c-154">Semplicità di personalizzazione di `OnMessageOptions` tramite `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="ab30c-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="ab30c-155">Consenti [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specificato in `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (per gli scenari in cui non si dispone di diritti di gestione).</span><span class="sxs-lookup"><span data-stu-id="ab30c-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="ab30c-156">Si noti che i processi Web di Azure è tooautomatically non è possibile eseguire il provisioning inesistente code e argomenti senza gestire AccessRights.</span><span class="sxs-lookup"><span data-stu-id="ab30c-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="ab30c-157"><a id="queues"></a>Argomenti correlati coperti da code di archiviazione hello come-tooarticle</span><span class="sxs-lookup"><span data-stu-id="ab30c-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="ab30c-158">Per informazioni sugli scenari di WebJobs SDK non specifiche tooService Bus, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="ab30c-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="ab30c-159">Gli argomenti trattati in tale articolo includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab30c-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="ab30c-160">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="ab30c-160">Async functions</span></span>
* <span data-ttu-id="ab30c-161">Più istanze</span><span class="sxs-lookup"><span data-stu-id="ab30c-161">Multiple instances</span></span>
* <span data-ttu-id="ab30c-162">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="ab30c-162">Graceful shutdown</span></span>
* <span data-ttu-id="ab30c-163">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="ab30c-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="ab30c-164">Impostare le stringhe di connessione SDK hello nel codice</span><span class="sxs-lookup"><span data-stu-id="ab30c-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="ab30c-165">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="ab30c-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="ab30c-166">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="ab30c-166">Trigger a function manually</span></span>
* <span data-ttu-id="ab30c-167">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="ab30c-167">Write logs</span></span>

## <span data-ttu-id="ab30c-168"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab30c-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="ab30c-169">Questa guida è fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ab30c-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="ab30c-170">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="ab30c-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

