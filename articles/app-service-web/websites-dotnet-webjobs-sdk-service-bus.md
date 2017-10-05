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
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="6daaf-103">Come usare il bus di servizio di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="6daaf-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="6daaf-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6daaf-104">Overview</span></span>
<span data-ttu-id="6daaf-105">In questa guida vengono forniti esempi di codice C# che illustrano come attivare un processo quando viene ricevuto un messaggio bus di servizio Azure.</span><span class="sxs-lookup"><span data-stu-id="6daaf-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="6daaf-106">Gli esempi di codice usano [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="6daaf-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="6daaf-107">Nella guida si presuppone che si sappia come [creare un progetto WebJob in Visual Studio con stringhe di connessione che puntano all'account di archiviazione](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="6daaf-108">I frammenti di codice mostrano solo le funzioni e non il codice che crea l’oggetto `JobHost` come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="6daaf-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="6daaf-109">Un [esempio di codice completo del bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) è disponibile nel repository di esempi azure-webjobs-sdk-samples in GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="6daaf-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="6daaf-110"><a id="prerequisites"></a> Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6daaf-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="6daaf-111">Per usare il bus di servizio, è necessario installare il pacchetto NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) oltre agli altri pacchetti di WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="6daaf-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="6daaf-112">È anche necessario impostare la stringa di connessione AzureWebJobsServiceBus oltre alle stringhe di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6daaf-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="6daaf-113">Questa operazione può essere effettuata nella sezione `connectionStrings` del file App.config, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6daaf-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="6daaf-114">Per un progetto di esempio che include l'impostazione della stringa di connessione del bus di servizio nel file App.config, vedere l' [esempio di bus di servizio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="6daaf-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="6daaf-115">Le stringhe di connessione possono essere impostate anche nell'ambiente di runtime di Azure, che quindi sostituisce le impostazioni di App.config quando il processo Web viene eseguito in Azure. Per altre informazioni, vedere[Introduzione a WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6daaf-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="6daaf-116"><a id="trigger"></a> Come attivare una funzione quando viene ricevuto un messaggio di coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6daaf-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="6daaf-117">Per scrivere una funzione che viene chiamata da WebJobs SDK quando viene ricevuto un messaggio di coda, usare l'attributo `ServiceBusTrigger` .</span><span class="sxs-lookup"><span data-stu-id="6daaf-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="6daaf-118">Il costruttore di attributo accetta un parametro che specifica il nome della coda di cui eseguire il polling.</span><span class="sxs-lookup"><span data-stu-id="6daaf-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="6daaf-119">Funzionamento di ServicebusTrigger</span><span class="sxs-lookup"><span data-stu-id="6daaf-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="6daaf-120">L'SDK riceve un messaggio in modalità `PeekLock` e chiama `Complete` sul messaggio se la funzione viene completata correttamente oppure `Abandon` se la funzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6daaf-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="6daaf-121">Se il tempo di esecuzione della funzione supera il timeout di `PeekLock` , il blocco viene rinnovato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6daaf-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="6daaf-122">Bus di servizio esegue la gestione della propria coda non elaborabile che non può essere controllata o configurata da WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="6daaf-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="6daaf-123">Messaggio stringa in coda</span><span class="sxs-lookup"><span data-stu-id="6daaf-123">String queue message</span></span>
<span data-ttu-id="6daaf-124">L'esempio di codice seguente legge un messaggio in coda che contiene una stringa e scrive la stringa nel dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="6daaf-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="6daaf-125">**Nota:** se si stanno creando messaggi di coda in un'applicazione che non usa WebJobs SDK, assicurarsi di impostare [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) su "text/plain".</span><span class="sxs-lookup"><span data-stu-id="6daaf-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="6daaf-126">Messaggio POCO in coda</span><span class="sxs-lookup"><span data-stu-id="6daaf-126">POCO queue message</span></span>
<span data-ttu-id="6daaf-127">L'SDK deserializzerà automaticamente un messaggio di coda contenente JSON per un tipo POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)).</span><span class="sxs-lookup"><span data-stu-id="6daaf-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="6daaf-128">Il seguente esempio di codice legge un messaggio di coda che contiene un oggetto `BlobInformation` con una proprietà `BlobName`:</span><span class="sxs-lookup"><span data-stu-id="6daaf-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="6daaf-129">Per esempi di codice che illustrano come usare le proprietà del tipo POCO assieme ai BLOB e alle tabelle nella stessa funzione, vedere la [versione delle code di archiviazione in questo articolo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="6daaf-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="6daaf-130">Se il codice che crea il messaggio in coda non utilizza WebJobs SDK, utilizzare un codice simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="6daaf-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="6daaf-131">Tipi con cui funziona ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="6daaf-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="6daaf-132">Oltre ai tipi `string` e POCO, è possibile usare l'attributo `ServiceBusTrigger` con una matrice di byte o un oggetto `BrokeredMessage`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="6daaf-133"><a id="create"></a> Come creare messaggi di coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6daaf-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="6daaf-134">Per scrivere una funzione che crea un nuovo messaggio di coda, usare l'attributo `ServiceBus` e passare il nome della coda al costruttore dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="6daaf-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="6daaf-135">Creare un singolo messaggio in coda in una funzione non asincrona</span><span class="sxs-lookup"><span data-stu-id="6daaf-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="6daaf-136">L'esempio di codice seguente usa un parametro di output per creare un nuovo messaggio nella coda denominata "outputqueue" con lo stesso contenuto del messaggio ricevuto nella coda denominata "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="6daaf-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="6daaf-137">Il parametro di output per la creazione di un singolo messaggio della coda può essere uno dei seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="6daaf-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="6daaf-138">Un tipo serializzabile POCO definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6daaf-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="6daaf-139">Serializzato automaticamente in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6daaf-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="6daaf-140">Per i parametri di tipo POCO, viene sempre creato un messaggio in coda quando la funzione termina; se il parametro è null, l'SDK crea un messaggio in coda che restituirà null quando il messaggio viene ricevuto e deserializzato.</span><span class="sxs-lookup"><span data-stu-id="6daaf-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="6daaf-141">Per gli altri tipi, se il parametro è null non viene creato alcun messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="6daaf-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="6daaf-142">Creare più messaggi in coda o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="6daaf-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="6daaf-143">Per creare più messaggi, usare l'attributo `ServiceBus` con `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nel seguente esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6daaf-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="6daaf-144">Ogni messaggio di coda viene creato immediatamente quando viene chiamato il metodo `Add` .</span><span class="sxs-lookup"><span data-stu-id="6daaf-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="6daaf-145"><a id="topics"></a>Come usare gli argomenti del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6daaf-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="6daaf-146">Per scrivere una funzione che l'SDK chiama quando viene ricevuto un messaggio su un argomento del bus di servizio, usare l'attributo `ServiceBusTrigger` con il costruttore che accetta il nome di argomento e sottoscrizione, come illustrato nel seguente esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6daaf-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="6daaf-147">Per creare un messaggio su un argomento, usare l'attributo `ServiceBus` con un nome di argomento nello stesso modo in cui viene usato con un nome di coda.</span><span class="sxs-lookup"><span data-stu-id="6daaf-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="6daaf-148">Funzionalità aggiunte nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="6daaf-148">Features added in release 1.1</span></span>
<span data-ttu-id="6daaf-149">Nella versione 1.1 sono state aggiunte le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="6daaf-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="6daaf-150">Personalizzazione completa dell'elaborazione dei messaggi tramite `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="6daaf-151">`MessagingProvider` supporta la personalizzazione degli elementi `MessagingFactory` e `NamespaceManager` del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6daaf-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="6daaf-152">Un modello di strategia `MessageProcessor` consente di specificare un processore per ogni coda o argomento.</span><span class="sxs-lookup"><span data-stu-id="6daaf-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="6daaf-153">La concorrenza dell'elaborazione dei messaggi è supportata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6daaf-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="6daaf-154">Semplicità di personalizzazione di `OnMessageOptions` tramite `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="6daaf-155">Possibilità di specificare [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) per `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (per gli scenari in cui non si dispone di diritti di gestione).</span><span class="sxs-lookup"><span data-stu-id="6daaf-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="6daaf-156">Si noti che Processi Web di Azure non è in grado di eseguire automaticamente il provisioning di code e argomenti inesistenti senza gestire AccessRights.</span><span class="sxs-lookup"><span data-stu-id="6daaf-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="6daaf-157"><a id="queues"></a>Argomenti correlati trattati nell'articolo delle procedure per le code di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6daaf-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="6daaf-158">Per informazioni sugli scenari di WebJobs SDK non specifici del bus di servizio, vedere la pagina relativa a [come usare l'archiviazione code di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="6daaf-159">Gli argomenti trattati in questo articolo includono quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6daaf-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="6daaf-160">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="6daaf-160">Async functions</span></span>
* <span data-ttu-id="6daaf-161">Più istanze</span><span class="sxs-lookup"><span data-stu-id="6daaf-161">Multiple instances</span></span>
* <span data-ttu-id="6daaf-162">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="6daaf-162">Graceful shutdown</span></span>
* <span data-ttu-id="6daaf-163">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="6daaf-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="6daaf-164">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="6daaf-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="6daaf-165">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="6daaf-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6daaf-166">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="6daaf-166">Trigger a function manually</span></span>
* <span data-ttu-id="6daaf-167">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="6daaf-167">Write logs</span></span>

## <span data-ttu-id="6daaf-168"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6daaf-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="6daaf-169">In questa guida sono stati forniti esempi di codice che illustrano come gestire scenari comuni per l'uso del bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="6daaf-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="6daaf-170">Per altre informazioni su come usare i processi Web di Azure e su WebJobs SDK, vedere le [risorse consigliate per i processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6daaf-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

