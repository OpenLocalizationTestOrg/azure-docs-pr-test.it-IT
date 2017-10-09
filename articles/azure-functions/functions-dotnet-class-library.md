---
title: librerie di classi .NET aaaUsing con le funzioni di Azure | Documenti Microsoft
description: Informazioni sull'utilizzano di librerie di classi .NET tooauthor per con le funzioni di Azure
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
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="9509e-104">Uso di librerie di classi .NET con Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9509e-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="9509e-105">File tooscript, le funzioni di Azure supporta inoltre la pubblicazione di una libreria di classi come implementazione hello per le funzioni di uno o più.</span><span class="sxs-lookup"><span data-stu-id="9509e-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="9509e-106">È consigliabile usare hello [Azure funzioni 2017 Visual Studio Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="9509e-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9509e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9509e-107">Prerequisites</span></span> 

<span data-ttu-id="9509e-108">In questo articolo presenta hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="9509e-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="9509e-109">[Visual Studio 2017 Preview versione 15.3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="9509e-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="9509e-110">Installare i carichi di lavoro hello **sviluppo web ASP.NET e** e **lo sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9509e-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="9509e-111">Visual Studio 2017 Tools per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9509e-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="9509e-112">Progetto di libreria di classi per Funzioni</span><span class="sxs-lookup"><span data-stu-id="9509e-112">Functions class library project</span></span>

<span data-ttu-id="9509e-113">Creare un progetto per Funzioni di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9509e-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="9509e-114">il nuovo modello di progetto Hello crea file hello *host.json* e *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="9509e-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="9509e-115">È possibile [personalizzare le impostazioni di runtime di Funzioni di Azure nel file host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="9509e-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="9509e-116">file Hello *local.settings.json* archivia le impostazioni dell'app, le stringhe di connessione e le impostazioni per strumenti di base di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9509e-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="9509e-117">toolearn più sulla relativa struttura, vedere [codice e il test funzioni di Azure localmente](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="9509e-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="9509e-118">Attributo FunctionName</span><span class="sxs-lookup"><span data-stu-id="9509e-118">FunctionName attribute</span></span>

<span data-ttu-id="9509e-119">attributo Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) contrassegna un metodo come un punto di ingresso della funzione.</span><span class="sxs-lookup"><span data-stu-id="9509e-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="9509e-120">Deve essere usato con un solo trigger e con 0 o più associazioni di input e di output.</span><span class="sxs-lookup"><span data-stu-id="9509e-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="9509e-121">Conversione toofunction.json</span><span class="sxs-lookup"><span data-stu-id="9509e-121">Conversion toofunction.json</span></span>

<span data-ttu-id="9509e-122">Quando viene compilato un progetto di funzioni di Azure, viene generato un file `function.json` nella directory hello corrisponde al nome della funzione hello è definito da `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="9509e-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="9509e-123">Specifica i trigger e le associazioni e file di assembly progetto toohello punti.</span><span class="sxs-lookup"><span data-stu-id="9509e-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="9509e-124">Questa conversione viene eseguita dal pacchetto NuGet hello [Microsoft\.NET\.Sdk\.funzioni](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="9509e-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="9509e-125">origine Hello è disponibile nel repository GitHub hello [azure\-funzioni\-vs\-compilare\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="9509e-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="9509e-126">Trigger e associazioni</span><span class="sxs-lookup"><span data-stu-id="9509e-126">Triggers and bindings</span></span>

<span data-ttu-id="9509e-127">Hello nella tabella seguente sono elencati i trigger di hello e associazioni che sono disponibili in un progetto libreria di classi di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9509e-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="9509e-128">Tutti gli attributi sono nello spazio dei nomi hello `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="9509e-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="9509e-129">Associazione</span><span class="sxs-lookup"><span data-stu-id="9509e-129">Binding</span></span> | <span data-ttu-id="9509e-130">Attributo</span><span class="sxs-lookup"><span data-stu-id="9509e-130">Attribute</span></span> | <span data-ttu-id="9509e-131">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="9509e-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="9509e-132">Trigger, input e output per archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="9509e-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="9509e-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="9509e-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="9509e-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="9509e-135">[Archiviazione BLOB]</span><span class="sxs-lookup"><span data-stu-id="9509e-135">[Blob storage]</span></span> |
| [<span data-ttu-id="9509e-136">Associazione di input e di output per Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9509e-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="9509e-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="9509e-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="9509e-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="9509e-139">Trigger e output per Hub eventi</span><span class="sxs-lookup"><span data-stu-id="9509e-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="9509e-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="9509e-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="9509e-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="9509e-142">Input e output per file esterni</span><span class="sxs-lookup"><span data-stu-id="9509e-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="9509e-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="9509e-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="9509e-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="9509e-145">Trigger per HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="9509e-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="9509e-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="9509e-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="9509e-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="9509e-148">Input e output per App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="9509e-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="9509e-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="9509e-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="9509e-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="9509e-151">Output per Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="9509e-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="9509e-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="9509e-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="9509e-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="9509e-154">Trigger e output per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="9509e-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="9509e-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="9509e-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="9509e-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="9509e-157">Output SendGrid</span><span class="sxs-lookup"><span data-stu-id="9509e-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="9509e-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-158">[SendGridAttribute]</span></span> | <span data-ttu-id="9509e-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="9509e-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="9509e-160">Trigger e output per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9509e-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="9509e-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="9509e-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="9509e-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="9509e-163">Input e output per l'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="9509e-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="9509e-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="9509e-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="9509e-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="9509e-166">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="9509e-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="9509e-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="9509e-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="9509e-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="9509e-169">Output di Twilio</span><span class="sxs-lookup"><span data-stu-id="9509e-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="9509e-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="9509e-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="9509e-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="9509e-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="9509e-172">Associazioni di trigger, input e output per l'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="9509e-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="9509e-173">Funzioni di Azure supporta i trigger e le associazioni di input e di output per l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9509e-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="9509e-174">Per altre informazioni sulle espressioni di associazione e sui metadati, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="9509e-175">Viene definito un trigger di blob con hello `[BlobTrigger]` attributo.</span><span class="sxs-lookup"><span data-stu-id="9509e-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="9509e-176">È possibile utilizzare l'attributo hello `[StorageAccount]` account di archiviazione hello toodefine utilizzato da un'intera funzione o una classe.</span><span class="sxs-lookup"><span data-stu-id="9509e-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="9509e-177">BLOB di input e output vengono definiti utilizzando hello `[Blob]` attributo, insieme con un `FileAccess` parametro che indica di lettura o scrittura.</span><span class="sxs-lookup"><span data-stu-id="9509e-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="9509e-178">Hello in seguito viene illustrato come utilizzare un trigger di blob e blob di associazione di output.</span><span class="sxs-lookup"><span data-stu-id="9509e-178">hello following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="9509e-179">Associazioni di input e di output per Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9509e-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="9509e-180">Funzioni di Azure supporta le associazioni di input e output per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9509e-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="9509e-181">toolearn più caratteristiche di hello di associazione di hello Cosmos DB, vedere [associazioni Azure funzioni Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="9509e-182">toobind tooa documento Cosmos DB, utilizzare l'attributo hello `[DocumentDB]` nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="9509e-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="9509e-183">Hello di esempio seguente è un trigger di coda e una API DocumentDB associazione di output:</span><span class="sxs-lookup"><span data-stu-id="9509e-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="9509e-184">Trigger e output per Hub eventi</span><span class="sxs-lookup"><span data-stu-id="9509e-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="9509e-185">Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9509e-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="9509e-186">Per altre informazioni, vedere [Associazioni di Hub eventi di Funzioni di Azure](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="9509e-187">tipi di Hello `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` e `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="9509e-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="9509e-188">Hello esempio seguente viene utilizzato un trigger di Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="9509e-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="9509e-189">Hello esempio seguente è presente un Hub di eventi di output, con valore restituito del metodo hello come output di hello:</span><span class="sxs-lookup"><span data-stu-id="9509e-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="9509e-190">Input e output per file esterni</span><span class="sxs-lookup"><span data-stu-id="9509e-190">External file input and output</span></span>

<span data-ttu-id="9509e-191">Funzioni di Azure supporta il trigger e le associazioni di input e di output per file esterni, ad esempio Google Drive, Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="9509e-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="9509e-192">vedere, più toolearn [associazioni di File esterno di Azure funzioni](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="9509e-193">Hello attributi `[ExternalFileTrigger]` e `[ExternalFile]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="9509e-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="9509e-194">Hello esempio c# seguente viene illustrato un file esterno di input e output di associazione.</span><span class="sxs-lookup"><span data-stu-id="9509e-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="9509e-195">copie di codice Hello hello file di output toohello file di input.</span><span class="sxs-lookup"><span data-stu-id="9509e-195">hello code copies hello input file toohello output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="9509e-196">HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="9509e-196">HTTP and webhooks</span></span>

<span data-ttu-id="9509e-197">Hello utilizzare `HttpTrigger` trigger toodefine HTTP attributo o webhook.</span><span class="sxs-lookup"><span data-stu-id="9509e-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="9509e-198">Questo attributo viene definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="9509e-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="9509e-199">È possibile personalizzare il livello di autorizzazione hello, tipo webhook, route e metodi.</span><span class="sxs-lookup"><span data-stu-id="9509e-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="9509e-200">esempio Hello definisce un trigger HTTP con l'autenticazione anonima e _genericJson_ tipo webhook.</span><span class="sxs-lookup"><span data-stu-id="9509e-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="9509e-201">Input e output per App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="9509e-201">Mobile Apps input and output</span></span>

<span data-ttu-id="9509e-202">Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="9509e-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="9509e-203">vedere, più toolearn [associazioni di App mobili di Azure funzioni](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="9509e-204">attributo Hello `[MobileTable]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="9509e-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="9509e-205">esempio Hello illustra un'App per dispositivi mobili associazione di output:</span><span class="sxs-lookup"><span data-stu-id="9509e-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="9509e-206">Output per Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="9509e-206">Notification Hubs output</span></span>

<span data-ttu-id="9509e-207">Funzioni di Azure supporta un'associazione di output per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="9509e-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="9509e-208">vedere, più toolearn [associazione di output di Hub di notifica di Azure funzioni](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="9509e-209">attributo Hello `[NotificationHub]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="9509e-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="9509e-210">Trigger e output per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="9509e-210">Queue storage trigger and output</span></span>

<span data-ttu-id="9509e-211">Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="9509e-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="9509e-212">Per altre informazioni, vedere [Associazioni di archiviazione code in Funzioni di Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="9509e-213">Hello esempio seguente viene illustrato come toouse hello tipo restituito dalla funzione con un coda di output di associazione, tramite hello `[Queue]` attributo.</span><span class="sxs-lookup"><span data-stu-id="9509e-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="9509e-214">toodefine un trigger di coda, utilizzare hello `[QueueTrigger]` attributo.</span><span class="sxs-lookup"><span data-stu-id="9509e-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="9509e-215">Output di SendGrid</span><span class="sxs-lookup"><span data-stu-id="9509e-215">SendGrid output</span></span>

<span data-ttu-id="9509e-216">Funzioni di Azure supporta un'associazione di output di SendGrid per inviare tramite posta elettronica a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="9509e-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="9509e-217">vedere, più toolearn [associazioni Azure funzioni SendGrid](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="9509e-218">attributo Hello `[SendGrid]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="9509e-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="9509e-219">Hello seguito è riportato un esempio di utilizzo di un trigger di coda del Bus di servizio e un'associazione di output SendGrid utilizzando `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="9509e-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="9509e-220">Trigger e output per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="9509e-220">Service Bus trigger and output</span></span>

<span data-ttu-id="9509e-221">Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="9509e-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="9509e-222">Per altre informazioni sulla configurazione delle associazioni, vedere [Associazioni del bus di servizio di Funzioni di Azure](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="9509e-223">Hello attributi `[ServiceBusTrigger]` e `[ServiceBus]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="9509e-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="9509e-224">Hello Ecco un esempio di un trigger di coda del Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="9509e-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="9509e-225">Hello Ecco un esempio di output un Bus di servizio di associazione, utilizzando il tipo restituito del metodo di hello come output di hello:</span><span class="sxs-lookup"><span data-stu-id="9509e-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="9509e-226">Input e output per l'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="9509e-226">Table storage input and output</span></span>

<span data-ttu-id="9509e-227">Funzioni di Azure supporta le associazioni di input e output per l'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="9509e-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="9509e-228">vedere, più toolearn [associazioni di archiviazione di Azure funzioni tabella](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="9509e-229">Hello seguente viene illustrata una classe con due funzioni, che illustra l'output di archiviazione tabella e le associazioni di input.</span><span class="sxs-lookup"><span data-stu-id="9509e-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="9509e-230">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="9509e-230">Timer trigger</span></span>

<span data-ttu-id="9509e-231">Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="9509e-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="9509e-232">toolearn più caratteristiche di hello di associazione di hello, vedere [pianificare l'esecuzione di codice con le funzioni di Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="9509e-233">Piano di consumo hello, è possibile definire pianificazioni con un [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="9509e-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="9509e-234">Se si usa un piano di servizio app, è anche possibile usare una stringa TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="9509e-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="9509e-235">Hello di esempio seguente definisce un trigger timer che viene eseguita ogni 5 minuti:</span><span class="sxs-lookup"><span data-stu-id="9509e-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="9509e-236">Output di Twilio</span><span class="sxs-lookup"><span data-stu-id="9509e-236">Twilio output</span></span>

<span data-ttu-id="9509e-237">I messaggi di testo SMS toosend funzioni di Azure supporta funzioni Twilio output tooenable associazioni.</span><span class="sxs-lookup"><span data-stu-id="9509e-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="9509e-238">vedere, più toolearn [messaggi inviare SMS da funzioni di Azure utilizzando hello Twilio output associazione](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="9509e-239">attributo Hello `[TwilioSms]` è definito nel pacchetto hello [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="9509e-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="9509e-240">esempio c# seguente Hello utilizza una coda trigger e un Twilio associazione di output:</span><span class="sxs-lookup"><span data-stu-id="9509e-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="9509e-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9509e-241">Next steps</span></span>

<span data-ttu-id="9509e-242">Per altre informazioni sull'uso di Funzioni di Azure in script C#, vedere [Guida di riferimento per gli sviluppatori C\# di Funzioni di Azure](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9509e-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
