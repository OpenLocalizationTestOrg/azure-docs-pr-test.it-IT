---
title: Uso di librerie di classi .NET con Funzioni di Azure | Documenti Docs
description: Informazioni su come creare librerie di classi .NET da usare con Funzioni di Azure
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="595ae-104">Uso di librerie di classi .NET con Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="595ae-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="595ae-105">Oltre ai file di script, Funzioni di Azure supporta la pubblicazione di una libreria di classi per l'implementazione di una o più funzioni.</span><span class="sxs-lookup"><span data-stu-id="595ae-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="595ae-106">È consigliabile usare [Visual Studio 2017 Tools per Funzioni di Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="595ae-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="595ae-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="595ae-107">Prerequisites</span></span> 

<span data-ttu-id="595ae-108">I prerequisiti di questo articolo sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="595ae-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="595ae-109">[Visual Studio 2017 Preview versione 15.3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="595ae-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="595ae-110">Installare i carichi di lavoro **Sviluppo Web e ASP.NET** e **Sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="595ae-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="595ae-111">Visual Studio 2017 Tools per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="595ae-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="595ae-112">Progetto di libreria di classi per Funzioni</span><span class="sxs-lookup"><span data-stu-id="595ae-112">Functions class library project</span></span>

<span data-ttu-id="595ae-113">Creare un progetto per Funzioni di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="595ae-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="595ae-114">Il modello del nuovo progetto crea i file *host.json* e *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="595ae-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="595ae-115">È possibile [personalizzare le impostazioni di runtime di Funzioni di Azure nel file host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="595ae-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="595ae-116">Nel file *local.settings.json* vengono archiviate le impostazioni dell'app, le stringhe di connessione e le impostazioni per Strumenti di base di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="595ae-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="595ae-117">Per altre informazioni sulla struttura, vedere [Scrivere codice per le funzioni di Azure e testarle in locale](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="595ae-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="595ae-118">Attributo FunctionName</span><span class="sxs-lookup"><span data-stu-id="595ae-118">FunctionName attribute</span></span>

<span data-ttu-id="595ae-119">L'attributo [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) contrassegna un metodo come punto di ingresso della funzione.</span><span class="sxs-lookup"><span data-stu-id="595ae-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="595ae-120">Deve essere usato con un solo trigger e con 0 o più associazioni di input e di output.</span><span class="sxs-lookup"><span data-stu-id="595ae-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="595ae-121">Conversione in function.json</span><span class="sxs-lookup"><span data-stu-id="595ae-121">Conversion to function.json</span></span>

<span data-ttu-id="595ae-122">Quando viene compilato un progetto di Funzioni di Azure, viene generato un file `function.json` nella directory, che corrisponde al nome della funzione definito da `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="595ae-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="595ae-123">Specifica i trigger, le associazioni e i punti che si riferiscono al file di assembly del progetto.</span><span class="sxs-lookup"><span data-stu-id="595ae-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="595ae-124">Questa conversione viene eseguita dal pacchetto NuGet [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="595ae-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="595ae-125">L'origine è disponibile nel repository di GitHub [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="595ae-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="595ae-126">Trigger e associazioni</span><span class="sxs-lookup"><span data-stu-id="595ae-126">Triggers and bindings</span></span>

<span data-ttu-id="595ae-127">Nella tabella seguente sono elencati i trigger e le associazioni disponibili in un progetto di libreria di classi di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="595ae-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="595ae-128">Tutti gli attributi sono contenuti nello spazio dei nomi `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="595ae-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="595ae-129">Associazione</span><span class="sxs-lookup"><span data-stu-id="595ae-129">Binding</span></span> | <span data-ttu-id="595ae-130">Attributo</span><span class="sxs-lookup"><span data-stu-id="595ae-130">Attribute</span></span> | <span data-ttu-id="595ae-131">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="595ae-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="595ae-132">Trigger, input e output per archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="595ae-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="595ae-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="595ae-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="595ae-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="595ae-135">[Archiviazione BLOB]</span><span class="sxs-lookup"><span data-stu-id="595ae-135">[Blob storage]</span></span> |
| [<span data-ttu-id="595ae-136">Associazione di input e di output per Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="595ae-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="595ae-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="595ae-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="595ae-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="595ae-139">Trigger e output per Hub eventi</span><span class="sxs-lookup"><span data-stu-id="595ae-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="595ae-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="595ae-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="595ae-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="595ae-142">Input e output per file esterni</span><span class="sxs-lookup"><span data-stu-id="595ae-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="595ae-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="595ae-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="595ae-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="595ae-145">Trigger per HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="595ae-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="595ae-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="595ae-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="595ae-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="595ae-148">Input e output per App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="595ae-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="595ae-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="595ae-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="595ae-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="595ae-151">Output per Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="595ae-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="595ae-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="595ae-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="595ae-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="595ae-154">Trigger e output per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="595ae-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="595ae-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="595ae-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="595ae-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="595ae-157">Output SendGrid</span><span class="sxs-lookup"><span data-stu-id="595ae-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="595ae-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-158">[SendGridAttribute]</span></span> | <span data-ttu-id="595ae-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="595ae-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="595ae-160">Trigger e output per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="595ae-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="595ae-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="595ae-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="595ae-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="595ae-163">Input e output per l'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="595ae-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="595ae-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="595ae-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="595ae-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="595ae-166">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="595ae-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="595ae-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="595ae-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="595ae-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="595ae-169">Output di Twilio</span><span class="sxs-lookup"><span data-stu-id="595ae-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="595ae-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="595ae-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="595ae-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="595ae-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="595ae-172">Associazioni di trigger, input e output per l'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="595ae-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="595ae-173">Funzioni di Azure supporta i trigger e le associazioni di input e di output per l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="595ae-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="595ae-174">Per altre informazioni sulle espressioni di associazione e sui metadati, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="595ae-175">Con l'attributo `[BlobTrigger]` viene definito un trigger del BLOB.</span><span class="sxs-lookup"><span data-stu-id="595ae-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="595ae-176">È possibile usare l'attributo `[StorageAccount]` per definire l'account di archiviazione usato da un'intera funzione o classe.</span><span class="sxs-lookup"><span data-stu-id="595ae-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="595ae-177">Gli input e output del BLOB vengono definiti con l'attributo `[Blob]` e con un parametro`FileAccess` che indica la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="595ae-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="595ae-178">L'esempio seguente usa un trigger e un'associazione di output del BLOB.</span><span class="sxs-lookup"><span data-stu-id="595ae-178">The following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="595ae-179">Associazioni di input e di output per Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="595ae-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="595ae-180">Funzioni di Azure supporta le associazioni di input e output per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="595ae-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="595ae-181">Per altre informazioni sulle funzionalità dell'associazione per Cosmos DB, vedere [Associazioni di Funzioni di Azure per Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="595ae-182">Per definire l'associazione a un documento Cosmos DB, usare l'attributo `[DocumentDB]` nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="595ae-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="595ae-183">L'esempio seguente contiene un trigger della coda e un'associazione di output dell'API di DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="595ae-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="595ae-184">Trigger e output per Hub eventi</span><span class="sxs-lookup"><span data-stu-id="595ae-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="595ae-185">Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="595ae-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="595ae-186">Per altre informazioni, vedere [Associazioni di Hub eventi di Funzioni di Azure](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="595ae-187">I tipi `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` e `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` sono definiti nel pacchetto NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="595ae-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="595ae-188">Nell'esempio seguente viene usato un trigger per Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="595ae-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="595ae-189">L'esempio seguente contiene un output per Hub eventi che usa il valore restituito dal metodo come output:</span><span class="sxs-lookup"><span data-stu-id="595ae-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="595ae-190">Input e output per file esterni</span><span class="sxs-lookup"><span data-stu-id="595ae-190">External file input and output</span></span>

<span data-ttu-id="595ae-191">Funzioni di Azure supporta il trigger e le associazioni di input e di output per file esterni, ad esempio Google Drive, Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="595ae-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="595ae-192">Per altre informazioni, vedere [Associazioni di file esterni in Funzioni di Azure](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="595ae-193">Gli attributi `[ExternalFileTrigger]` e `[ExternalFile]` sono definiti nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="595ae-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="595ae-194">Nell'esempio C# seguente viene illustrata l'associazione di input e di output di un file esterno.</span><span class="sxs-lookup"><span data-stu-id="595ae-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="595ae-195">Il codice copia il file di input nel file di output.</span><span class="sxs-lookup"><span data-stu-id="595ae-195">The code copies the input file to the output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="595ae-196">HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="595ae-196">HTTP and webhooks</span></span>

<span data-ttu-id="595ae-197">Usare l'attributo `HttpTrigger` per definire un trigger HTTP o un webhook.</span><span class="sxs-lookup"><span data-stu-id="595ae-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="595ae-198">Questo attributo è definito nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="595ae-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="595ae-199">È possibile personalizzare livello di autorizzazione, tipo di webhook, route e metodi.</span><span class="sxs-lookup"><span data-stu-id="595ae-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="595ae-200">L'esempio seguente definisce un trigger HTTP con autenticazione anonima e tipo di webhook _genericJson_.</span><span class="sxs-lookup"><span data-stu-id="595ae-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="595ae-201">Input e output per App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="595ae-201">Mobile Apps input and output</span></span>

<span data-ttu-id="595ae-202">Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="595ae-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="595ae-203">Per altre informazioni, vedere [Associazioni di app per dispositivi mobili in Funzioni di Azure](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="595ae-204">L'attributo `[MobileTable]` è definito nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="595ae-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="595ae-205">L'esempio seguente illustra un'associazione di output per App per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="595ae-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="595ae-206">Output per Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="595ae-206">Notification Hubs output</span></span>

<span data-ttu-id="595ae-207">Funzioni di Azure supporta un'associazione di output per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="595ae-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="595ae-208">Per altre informazioni, vedere [Associazione di output di Hub di notifica in Funzioni di Azure](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="595ae-209">L'attributo `[NotificationHub]` è definito nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="595ae-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="595ae-210">Trigger e output per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="595ae-210">Queue storage trigger and output</span></span>

<span data-ttu-id="595ae-211">Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="595ae-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="595ae-212">Per altre informazioni, vedere [Associazioni di archiviazione code in Funzioni di Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="595ae-213">Nell'esempio seguente viene illustrato come usare il tipo restituito dalla funzione con un'associazione di output per la coda, tramite l'attributo `[Queue]`.</span><span class="sxs-lookup"><span data-stu-id="595ae-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="595ae-214">Per definire un trigger della coda, usare l'attributo `[QueueTrigger]`.</span><span class="sxs-lookup"><span data-stu-id="595ae-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="595ae-215">Output di SendGrid</span><span class="sxs-lookup"><span data-stu-id="595ae-215">SendGrid output</span></span>

<span data-ttu-id="595ae-216">Funzioni di Azure supporta un'associazione di output di SendGrid per inviare tramite posta elettronica a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="595ae-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="595ae-217">Per altre informazioni, vedere [Associazioni di SendGrid di Funzioni di Azure](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="595ae-218">L'attributo `[SendGrid]` è definito nel pacchetto NuGet [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="595ae-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="595ae-219">Di seguito è riportato un esempio di utilizzo di un trigger della coda per il bus di servizio e di un binding di output di SendGrid mediante `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="595ae-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="595ae-220">Trigger e output per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="595ae-220">Service Bus trigger and output</span></span>

<span data-ttu-id="595ae-221">Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="595ae-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="595ae-222">Per altre informazioni sulla configurazione delle associazioni, vedere [Associazioni del bus di servizio di Funzioni di Azure](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="595ae-223">Gli attributi `[ServiceBusTrigger]` e `[ServiceBus]` sono definiti nel pacchetto NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="595ae-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="595ae-224">Di seguito è riportato un esempio di trigger della coda per il bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="595ae-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="595ae-225">Di seguito è riportato un esempio di un'associazione di output per il bus di servizio che usa il tipo restituito dal metodo come output:</span><span class="sxs-lookup"><span data-stu-id="595ae-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="595ae-226">Input e output per l'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="595ae-226">Table storage input and output</span></span>

<span data-ttu-id="595ae-227">Funzioni di Azure supporta le associazioni di input e output per l'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="595ae-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="595ae-228">Per altre informazioni, vedere [Associazioni di archiviazione tabelle in Funzioni di Azure](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="595ae-229">L'esempio seguente si riferisce a una classe con due funzioni e illustra l'associazione di input e di output per l'archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="595ae-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="595ae-230">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="595ae-230">Timer trigger</span></span>

<span data-ttu-id="595ae-231">Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="595ae-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="595ae-232">Per altre informazioni sulle funzionalità dell'associazione, vedere [Pianificare l'esecuzione di codice con Funzioni di Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="595ae-233">Nel piano a consumo è possibile definire le pianificazioni usando un'[espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="595ae-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="595ae-234">Se si usa un piano di servizio app, è anche possibile usare una stringa TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="595ae-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="595ae-235">L'esempio seguente definisce un trigger del timer eseguito ogni 5 minuti:</span><span class="sxs-lookup"><span data-stu-id="595ae-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="595ae-236">Output di Twilio</span><span class="sxs-lookup"><span data-stu-id="595ae-236">Twilio output</span></span>

<span data-ttu-id="595ae-237">Funzioni di Azure supporta le associazioni di output di Twilio per consentire alle funzioni di inviare SMS.</span><span class="sxs-lookup"><span data-stu-id="595ae-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="595ae-238">Per altre informazioni, vedere [Inviare messaggi SMS da Funzioni di Azure usando l'associazione di output Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="595ae-239">L'attributo `[TwilioSms]` è definito nel pacchetto [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="595ae-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="595ae-240">L'esempio C# seguente usa un trigger della coda e un'associazione di output Twilio:</span><span class="sxs-lookup"><span data-stu-id="595ae-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="595ae-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="595ae-241">Next steps</span></span>

<span data-ttu-id="595ae-242">Per altre informazioni sull'uso di Funzioni di Azure in script C#, vedere [Guida di riferimento per gli sviluppatori C\# di Funzioni di Azure](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="595ae-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="595ae-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="595ae-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="595ae-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="595ae-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="595ae-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="595ae-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="595ae-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="595ae-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="595ae-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="595ae-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="595ae-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="595ae-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="595ae-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="595ae-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="595ae-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="595ae-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="595ae-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="595ae-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="595ae-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="595ae-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="595ae-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="595ae-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="595ae-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="595ae-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="595ae-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="595ae-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="595ae-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="595ae-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="595ae-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="595ae-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="595ae-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
