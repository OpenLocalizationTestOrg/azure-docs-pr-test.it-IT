---
title: riferimenti per sviluppatori di funzioni di Script c# aaaAzure | Documenti Microsoft
description: Comprendere come toodevelop le funzioni di Azure tramite c#.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="f00e5-104">Guida di riferimento a Funzioni di Azure per sviluppatori di script C#</span><span class="sxs-lookup"><span data-stu-id="f00e5-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f00e5-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="f00e5-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="f00e5-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="f00e5-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="f00e5-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f00e5-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="f00e5-108">Hello esperienza di script c# per le funzioni di Azure si basa su hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="f00e5-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="f00e5-109">I dati vengono trasmessi alla funzione C# tramite argomenti del metodo.</span><span class="sxs-lookup"><span data-stu-id="f00e5-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="f00e5-110">I nomi di argomento specificati `function.json`, e non vi sono nomi predefiniti per l'accesso alle operazioni quali hello funzione logger e token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="f00e5-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="f00e5-111">Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f00e5-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="f00e5-112">Per informazioni sull'uso delle librerie di classi di C#, vedere [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Usare le librerie di classi di .NET con Funzioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="f00e5-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="f00e5-113">Funzionamento di CSX</span><span class="sxs-lookup"><span data-stu-id="f00e5-113">How .csx works</span></span>
<span data-ttu-id="f00e5-114">Hello `.csx` formato consente toowrite meno "standard" e lo stato attivo sulla scrittura solo una funzione c#.</span><span class="sxs-lookup"><span data-stu-id="f00e5-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="f00e5-115">Includere tutti i riferimenti agli assembly e spazi dei nomi all'inizio di hello del file hello come di consueto.</span><span class="sxs-lookup"><span data-stu-id="f00e5-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="f00e5-116">Anziché eseguire il wrapping di tutti gli elementi in un spazio dei nomi e classe, definire semplicemente un metodo `Run`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="f00e5-117">Se è necessario tooinclude tutte le classi, per gli oggetti vecchio oggetto CLR Object (POCO), è possibile includere una classe all'interno di istanza toodefine normale hello stesso file.</span><span class="sxs-lookup"><span data-stu-id="f00e5-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="f00e5-118">Associazione tooarguments</span><span class="sxs-lookup"><span data-stu-id="f00e5-118">Binding tooarguments</span></span>
<span data-ttu-id="f00e5-119">diverse associazioni Hello sono funzione associata tooa c# tramite hello `name` proprietà hello *function.json* configurazione.</span><span class="sxs-lookup"><span data-stu-id="f00e5-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="f00e5-120">Ogni associazione ha i propri tipi supportati; ad esempio un trigger di BLOB può supportare una stringa, un POCO o un CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="f00e5-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="f00e5-121">tipi supportato Hello sono documentati nella Guida di riferimento per ogni associazione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="f00e5-122">In un oggetto POCO devono essere definiti un metodo Get e un metodo Set per ogni proprietà.</span><span class="sxs-lookup"><span data-stu-id="f00e5-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="f00e5-123">Uso del valore restituito del metodo per l'associazione di output</span><span class="sxs-lookup"><span data-stu-id="f00e5-123">Using method return value for output binding</span></span>

<span data-ttu-id="f00e5-124">È possibile utilizzare un valore restituito del metodo per un'associazione di output, utilizzando nome hello `$return` in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f00e5-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="f00e5-125">Scrittura di più valori di output</span><span class="sxs-lookup"><span data-stu-id="f00e5-125">Writing multiple output values</span></span>

<span data-ttu-id="f00e5-126">toowrite tooan di più valori di output di associazione, utilizzare hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipi.</span><span class="sxs-lookup"><span data-stu-id="f00e5-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="f00e5-127">Questi tipi sono raccolte di sola scrittura vengono scritta toohello associazione di output quando hello metodo viene completato.</span><span class="sxs-lookup"><span data-stu-id="f00e5-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="f00e5-128">Questo esempio scrive più messaggi in coda usando `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="f00e5-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="f00e5-129">Registrazione</span><span class="sxs-lookup"><span data-stu-id="f00e5-129">Logging</span></span>
<span data-ttu-id="f00e5-130">toolog output dei log in streaming tooyour in c#, includere un argomento di tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="f00e5-131">È consigliabile denominarlo `log`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="f00e5-132">Evitare di usare `Console.Write` in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="f00e5-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="f00e5-133">`TraceWriter`è definito in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="f00e5-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="f00e5-134">livello di log di Hello `TraceWriter` possono essere configurate in [host\.json].</span><span class="sxs-lookup"><span data-stu-id="f00e5-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="f00e5-135">Async</span><span class="sxs-lookup"><span data-stu-id="f00e5-135">Async</span></span>
<span data-ttu-id="f00e5-136">toomake una funzione asincrona, utilizzare hello `async` (parola chiave) e restituire un `Task` oggetto.</span><span class="sxs-lookup"><span data-stu-id="f00e5-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="f00e5-137">Token di annullamento</span><span class="sxs-lookup"><span data-stu-id="f00e5-137">Cancellation Token</span></span>
<span data-ttu-id="f00e5-138">Alcune operazioni richiedono l'arresto normale.</span><span class="sxs-lookup"><span data-stu-id="f00e5-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="f00e5-139">Mentre è sempre codice toowrite più in grado di gestire un arresto anomalo, nei casi in cui si desidera che le richieste di arresto normale toohandle, definire un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) digitato l'argomento.</span><span class="sxs-lookup"><span data-stu-id="f00e5-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="f00e5-140">Oggetto `CancellationToken` viene fornito toosignal che viene attivato un arresto dell'host.</span><span class="sxs-lookup"><span data-stu-id="f00e5-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="f00e5-141">Importazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="f00e5-141">Importing namespaces</span></span>
<span data-ttu-id="f00e5-142">Se è necessario tooimport gli spazi dei nomi, è possibile utilizzare come di consueto, hello `using` clausola.</span><span class="sxs-lookup"><span data-stu-id="f00e5-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="f00e5-143">Hello seguenti spazi dei nomi vengono importati automaticamente e sono pertanto facoltativi:</span><span class="sxs-lookup"><span data-stu-id="f00e5-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="f00e5-144">Riferimento ad assembly esterni</span><span class="sxs-lookup"><span data-stu-id="f00e5-144">Referencing External Assemblies</span></span>
<span data-ttu-id="f00e5-145">Per gli assembly di framework, aggiungere i riferimenti utilizzando hello `#r "AssemblyName"` direttiva.</span><span class="sxs-lookup"><span data-stu-id="f00e5-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="f00e5-146">Hello agli assembly seguenti vengono aggiunti automaticamente dalle funzioni di Azure hello ambiente di hosting:</span><span class="sxs-lookup"><span data-stu-id="f00e5-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="f00e5-147">Hello agli assembly seguenti possono fare riferimento nome semplice (ad esempio, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="f00e5-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="f00e5-148">Fare riferimento ad assembly personalizzati</span><span class="sxs-lookup"><span data-stu-id="f00e5-148">Referencing custom assemblies</span></span>

<span data-ttu-id="f00e5-149">tooreference un assembly personalizzato, è possibile utilizzare un *condivisa* assembly o un *privata* assembly:</span><span class="sxs-lookup"><span data-stu-id="f00e5-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="f00e5-150">Gli assembly condivisi sono condivisi da tutte le funzioni all'interno di un'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="f00e5-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="f00e5-151">tooreference un assembly personalizzato, caricare hello assembly tooyour funzione app, ad esempio un `bin` cartella nella radice di app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="f00e5-152">Gli assembly privati fanno parte del contesto di una funzione specificata e supportano il caricamento laterale di versioni diverse.</span><span class="sxs-lookup"><span data-stu-id="f00e5-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="f00e5-153">Assembly privati devono essere caricati un `bin` cartella nella directory di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="f00e5-154">Riferimento utilizzando come nome del file hello `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="f00e5-155">Per informazioni sul funzionamento dei file di cartella funzione tooyour tooupload, vedere hello seguente sezione gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f00e5-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="f00e5-156">Directory controllate</span><span class="sxs-lookup"><span data-stu-id="f00e5-156">Watched directories</span></span>

<span data-ttu-id="f00e5-157">directory di Hello che contiene i file di script di funzione hello viene controllata automaticamente tooassemblies le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f00e5-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="f00e5-158">toowatch per la modifica di assembly in altre directory, aggiungere toohello `watchDirectories` nell'elenco [host\.json].</span><span class="sxs-lookup"><span data-stu-id="f00e5-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="f00e5-159">Uso dei pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="f00e5-159">Using NuGet packages</span></span>
<span data-ttu-id="f00e5-160">pacchetti di NuGet toouse in una funzione c#, caricare un *Project* cartella toohello della funzione di file nel sistema di file dell'app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="f00e5-161">Di seguito è riportato un esempio *Project* file che si aggiunge una riferimento tooMicrosoft.ProjectOxford.Face versione 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="f00e5-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="f00e5-162">Solo hello .NET Framework 4.6 è supportato, quindi assicurarsi che il *Project* file specifica `net46` come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f00e5-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="f00e5-163">Quando si carica un *Project* file, recupera i pacchetti hello hello runtime e aggiunge automaticamente gli assembly di riferimenti toohello pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f00e5-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="f00e5-164">Non è necessario tooadd `#r "AssemblyName"` direttive.</span><span class="sxs-lookup"><span data-stu-id="f00e5-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="f00e5-165">tipi di hello toouse definiti in pacchetti NuGet hello, aggiungere hello necessario `using` istruzioni tooyour *run.csx* file</span><span class="sxs-lookup"><span data-stu-id="f00e5-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="f00e5-166">In fase di esecuzione funzioni hello ripristino NuGet funziona confrontando `project.json` e `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="f00e5-167">Se gli indicatori di data e ora del file hello hello **non** viene eseguito un ripristino NuGet di corrispondenza, e download NuGet pacchetti di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="f00e5-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="f00e5-168">Tuttavia, se hello timbri data e ora del file hello **si** corrispondenza, NuGet non esegue un ripristino.</span><span class="sxs-lookup"><span data-stu-id="f00e5-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="f00e5-169">Pertanto, `project.lock.json` non devono essere distribuiti come fa ripristino del pacchetto NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="f00e5-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="f00e5-170">distribuzione di blocco hello tooavoid file, aggiungere hello `project.lock.json` toohello `.gitignore` file.</span><span class="sxs-lookup"><span data-stu-id="f00e5-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="f00e5-171">toouse un feed NuGet personalizzato, specificare hello feed in un *NuGet* file nella directory principale dell'App di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="f00e5-172">Per altre informazioni, vedere [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Configurazione del comportamento di NuGet).</span><span class="sxs-lookup"><span data-stu-id="f00e5-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="f00e5-173">Uso di un file project.json</span><span class="sxs-lookup"><span data-stu-id="f00e5-173">Using a project.json file</span></span>
1. <span data-ttu-id="f00e5-174">Aprire la funzione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f00e5-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="f00e5-175">Hello registra scheda Visualizza hello pacchetto installazione l'output.</span><span class="sxs-lookup"><span data-stu-id="f00e5-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="f00e5-176">tooupload un file Project JSON, utilizzare uno dei metodi hello descritti in hello [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate) nell'argomento di riferimento per sviluppatori di Azure funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="f00e5-177">Dopo aver hello *Project* file viene caricato, viene visualizzato l'output come hello nella funzione di esempio seguente del flusso di log:</span><span class="sxs-lookup"><span data-stu-id="f00e5-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="f00e5-178">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="f00e5-178">Environment variables</span></span>
<span data-ttu-id="f00e5-179">tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `System.Environment.GetEnvironmentVariable`, come illustrato nell'esempio di codice seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f00e5-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="f00e5-180">Riutilizzo del codice CSX</span><span class="sxs-lookup"><span data-stu-id="f00e5-180">Reusing .csx code</span></span>
<span data-ttu-id="f00e5-181">È possibile usare classi e metodi definiti in altri file con estensione *.csx* nel file *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="f00e5-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="f00e5-182">toodo utilizzati, `#load` direttive il *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="f00e5-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="f00e5-183">Nell'esempio seguente di hello, una routine di registrazione è denominato `MyLogger` è condiviso in *myLogger.csx* e caricati in *run.csx* utilizzando hello `#load` direttiva:</span><span class="sxs-lookup"><span data-stu-id="f00e5-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="f00e5-184">Esempio di *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="f00e5-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="f00e5-185">Esempio di *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="f00e5-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="f00e5-186">Utilizzando un oggetto condiviso *csx* è un modello comune quando si desidera toostrongly digitare gli argomenti tra le funzioni di utilizzo di un oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="f00e5-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="f00e5-187">In hello semplificata di esempio seguente, un trigger HTTP e i trigger di coda condividono un oggetto POCO denominato `Order` dati degli ordini toostrongly tipo hello:</span><span class="sxs-lookup"><span data-stu-id="f00e5-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="f00e5-188">File *run.csx* di esempio per il trigger HTTP:</span><span class="sxs-lookup"><span data-stu-id="f00e5-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="f00e5-189">File *run.csx* di esempio per il trigger della coda:</span><span class="sxs-lookup"><span data-stu-id="f00e5-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="f00e5-190">File *order.csx* di esempio:</span><span class="sxs-lookup"><span data-stu-id="f00e5-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="f00e5-191">È possibile utilizzare un percorso relativo con hello `#load` direttiva:</span><span class="sxs-lookup"><span data-stu-id="f00e5-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="f00e5-192">`#load "mylogger.csx"`Carica un file nella cartella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="f00e5-193">`#load "loadedfiles\mylogger.csx"`Carica un file che si trova in una cartella nella cartella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f00e5-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="f00e5-194">`#load "..\shared\mylogger.csx"`Carica un file si trova in una cartella hello stesso livello, ovvero come cartella funzione hello, direttamente sotto *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="f00e5-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="f00e5-195">Hello `#load` direttiva funziona solo con *csx* file (c# script), non con *cs* file.</span><span class="sxs-lookup"><span data-stu-id="f00e5-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="f00e5-196">Associazione al runtime mediante associazione imperativa</span><span class="sxs-lookup"><span data-stu-id="f00e5-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="f00e5-197">In c# e altri linguaggi .NET, è possibile utilizzare un [imperativo](https://en.wikipedia.org/wiki/Imperative_programming) modello di associazione, come toohello anziché [ *dichiarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) associazioni in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f00e5-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="f00e5-198">Associazione imperativo è utile quando i parametri di associazione necessario toobe calcolato in fase di runtime anziché di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f00e5-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="f00e5-199">Con questo modello, è possibile associare toosupported input e output associazione il volo nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="f00e5-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="f00e5-200">Definire un'associazione imperativa, come segue:</span><span class="sxs-lookup"><span data-stu-id="f00e5-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="f00e5-201">**Non** includere una voce in *function.json* per le associazioni imperative da eseguire.</span><span class="sxs-lookup"><span data-stu-id="f00e5-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="f00e5-202">Passare un parametro di input [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) o [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="f00e5-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="f00e5-203">Utilizzare hello seguente c# modello tooperform hello associazione dati.</span><span class="sxs-lookup"><span data-stu-id="f00e5-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="f00e5-204">dove `BindingTypeAttribute` hello .NET attributo che definisce l'associazione e `T` è hello input o output di tipo supportato dal tipo di associazione.</span><span class="sxs-lookup"><span data-stu-id="f00e5-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="f00e5-205">`T` non può essere un tipo di parametro `out`, ad esempio `out JObject`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="f00e5-206">L'associazione di output della tabella App per dispositivi mobili, ad esempio, supporta[ sei tipi di output](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ma è possibile usare solo [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) per `T`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="f00e5-207">Hello esempio di codice seguente crea un [associazione di output blob di archiviazione](functions-bindings-storage-blob.md#using-a-blob-output-binding) con blob percorso definito in fase di esecuzione, quindi scrive un blob toohello stringa.</span><span class="sxs-lookup"><span data-stu-id="f00e5-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="f00e5-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definisce hello [blob di archiviazione](functions-bindings-storage-blob.md) input o output, associazione e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) è un tipo di associazione di output supportati.</span><span class="sxs-lookup"><span data-stu-id="f00e5-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="f00e5-209">Così com'è, il codice hello Ottiene hello app impostazione predefinita per hello stringa di connessione di account di archiviazione (ovvero `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="f00e5-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="f00e5-210">È possibile specificare un toouse impostazione app personalizzata aggiungendo il [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passando una matrice di attributi hello in `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="f00e5-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="f00e5-211">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="f00e5-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="f00e5-212">Hello nella tabella seguente elenca gli attributi di hello .NET per i pacchetti di tipo e hello ogni associazione in cui sono definiti.</span><span class="sxs-lookup"><span data-stu-id="f00e5-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="f00e5-213">Associazione</span><span class="sxs-lookup"><span data-stu-id="f00e5-213">Binding</span></span> | <span data-ttu-id="f00e5-214">Attributo</span><span class="sxs-lookup"><span data-stu-id="f00e5-214">Attribute</span></span> | <span data-ttu-id="f00e5-215">Aggiungi riferimento</span><span class="sxs-lookup"><span data-stu-id="f00e5-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="f00e5-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f00e5-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="f00e5-217">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f00e5-217">Event Hubs</span></span> | <span data-ttu-id="f00e5-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f00e5-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="f00e5-219">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="f00e5-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="f00e5-220">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="f00e5-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="f00e5-221">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f00e5-221">Service Bus</span></span> | <span data-ttu-id="f00e5-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f00e5-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="f00e5-223">Coda di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f00e5-223">Storage queue</span></span> | <span data-ttu-id="f00e5-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f00e5-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f00e5-225">BLOB di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f00e5-225">Storage blob</span></span> | <span data-ttu-id="f00e5-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f00e5-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f00e5-227">Tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f00e5-227">Storage table</span></span> | <span data-ttu-id="f00e5-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f00e5-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f00e5-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="f00e5-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="f00e5-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f00e5-230">Next steps</span></span>
<span data-ttu-id="f00e5-231">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="f00e5-231">For more information, see hello following resources:</span></span>

* <span data-ttu-id="f00e5-232">[Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)</span><span class="sxs-lookup"><span data-stu-id="f00e5-232">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="f00e5-233">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f00e5-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="f00e5-234">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="f00e5-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="f00e5-235">Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f00e5-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="f00e5-236">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f00e5-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
