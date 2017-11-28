---
title: Guida di riferimento a Funzioni di Azure per sviluppatori di script C# | Microsoft Docs
description: Informazioni su come sviluppare Funzioni di Azure in C#.
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="d469a-104">Guida di riferimento a Funzioni di Azure per sviluppatori di script C#</span><span class="sxs-lookup"><span data-stu-id="d469a-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d469a-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="d469a-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="d469a-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="d469a-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="d469a-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d469a-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="d469a-108">L'esperienza con gli script C# per Funzioni di Azure si basa su Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="d469a-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="d469a-109">I dati vengono trasmessi alla funzione C# tramite argomenti del metodo.</span><span class="sxs-lookup"><span data-stu-id="d469a-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="d469a-110">I nomi di argomento sono specificati in `function.json`e sono disponibili nomi predefiniti per l'accesso a elementi quali il logger delle funzioni e i token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="d469a-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="d469a-111">Questo articolo presuppone che l'utente abbia già letto [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d469a-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="d469a-112">Per informazioni sull'uso delle librerie di classi di C#, vedere [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Usare le librerie di classi di .NET con Funzioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="d469a-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="d469a-113">Funzionamento di CSX</span><span class="sxs-lookup"><span data-stu-id="d469a-113">How .csx works</span></span>
<span data-ttu-id="d469a-114">Il formato `.csx` consente di scrivere meno "boilerplate" e di concentrarsi solo sulla scrittura di una funzione C#.</span><span class="sxs-lookup"><span data-stu-id="d469a-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="d469a-115">Includere tutti i riferimenti ad assembly e gli spazi dei nomi all'inizio del file come di consueto.</span><span class="sxs-lookup"><span data-stu-id="d469a-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="d469a-116">Anziché eseguire il wrapping di tutti gli elementi in un spazio dei nomi e classe, definire semplicemente un metodo `Run`.</span><span class="sxs-lookup"><span data-stu-id="d469a-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="d469a-117">Se è necessario includere classi, ad esempio per definire oggetti POCO (Plain Old CLR Object), si può includere una classe nello stesso file.</span><span class="sxs-lookup"><span data-stu-id="d469a-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="d469a-118">Associazione agli argomenti</span><span class="sxs-lookup"><span data-stu-id="d469a-118">Binding to arguments</span></span>
<span data-ttu-id="d469a-119">I vari binding sono associati a una funzione C# tramite la proprietà `name` nella configurazione di *function.json*.</span><span class="sxs-lookup"><span data-stu-id="d469a-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="d469a-120">Ogni associazione ha i propri tipi supportati; ad esempio un trigger di BLOB può supportare una stringa, un POCO o un CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="d469a-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="d469a-121">I tipi supportati sono documentati negli argomenti di riferimento per ogni associazione.</span><span class="sxs-lookup"><span data-stu-id="d469a-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="d469a-122">In un oggetto POCO devono essere definiti un metodo Get e un metodo Set per ogni proprietà.</span><span class="sxs-lookup"><span data-stu-id="d469a-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="d469a-123">Uso del valore restituito del metodo per l'associazione di output</span><span class="sxs-lookup"><span data-stu-id="d469a-123">Using method return value for output binding</span></span>

<span data-ttu-id="d469a-124">È possibile usare un valore restituito del metodo per un'associazione di output, usando il nome `$return` in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="d469a-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="d469a-125">Scrittura di più valori di output</span><span class="sxs-lookup"><span data-stu-id="d469a-125">Writing multiple output values</span></span>

<span data-ttu-id="d469a-126">Per scrivere più valori in un'associazione di output, usare i tipi [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="d469a-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="d469a-127">Questi tipi sono raccolte di sola scrittura che vengono scritte nell'associazione di output durante il completamento del metodo.</span><span class="sxs-lookup"><span data-stu-id="d469a-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="d469a-128">Questo esempio scrive più messaggi in coda usando `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="d469a-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="d469a-129">Registrazione</span><span class="sxs-lookup"><span data-stu-id="d469a-129">Logging</span></span>
<span data-ttu-id="d469a-130">Per registrare l'output nei log in streaming in C#, includere un argomento di tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="d469a-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="d469a-131">È consigliabile denominarlo `log`.</span><span class="sxs-lookup"><span data-stu-id="d469a-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="d469a-132">Evitare di usare `Console.Write` in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d469a-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="d469a-133">`TraceWriter` è definito in [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="d469a-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="d469a-134">Il livello di registrazione per `TraceWriter` può essere configurato in [host\.json].</span><span class="sxs-lookup"><span data-stu-id="d469a-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="d469a-135">Async</span><span class="sxs-lookup"><span data-stu-id="d469a-135">Async</span></span>
<span data-ttu-id="d469a-136">Per rendere una funzione asincrona, usare la parola chiave `async` e restituire un oggetto `Task`.</span><span class="sxs-lookup"><span data-stu-id="d469a-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="d469a-137">Token di annullamento</span><span class="sxs-lookup"><span data-stu-id="d469a-137">Cancellation Token</span></span>
<span data-ttu-id="d469a-138">Alcune operazioni richiedono l'arresto normale.</span><span class="sxs-lookup"><span data-stu-id="d469a-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="d469a-139">Mentre è sempre preferibile scrivere il codice per la gestione degli arresti anomali, per gestire le richieste di arresto normale si definisce un argomento tipizzato [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx).</span><span class="sxs-lookup"><span data-stu-id="d469a-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="d469a-140">È fornito un `CancellationToken` per segnalare che viene avviato un arresto dell'host.</span><span class="sxs-lookup"><span data-stu-id="d469a-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="d469a-141">Importazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="d469a-141">Importing namespaces</span></span>
<span data-ttu-id="d469a-142">Se è necessario importare spazi dei nomi, è possibile farlo come al solito con la clausola `using` .</span><span class="sxs-lookup"><span data-stu-id="d469a-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="d469a-143">Gli spazi dei nomi seguenti vengono importati automaticamente e sono quindi facoltativi:</span><span class="sxs-lookup"><span data-stu-id="d469a-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="d469a-144">Riferimento ad assembly esterni</span><span class="sxs-lookup"><span data-stu-id="d469a-144">Referencing External Assemblies</span></span>
<span data-ttu-id="d469a-145">Per gli assembly di framework aggiungere riferimenti usando la direttiva `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="d469a-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="d469a-146">Gli assembly seguenti vengono aggiunti automaticamente dall'ambiente di hosting di Funzioni di Azure:</span><span class="sxs-lookup"><span data-stu-id="d469a-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="d469a-147">È possibile fare riferimento agli assembly seguenti con il nome semplice (ad esempio, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="d469a-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="d469a-148">Fare riferimento ad assembly personalizzati</span><span class="sxs-lookup"><span data-stu-id="d469a-148">Referencing custom assemblies</span></span>

<span data-ttu-id="d469a-149">Per fare riferimento a un assembly personalizzato, è possibile usare un assembly *condiviso* o un assembly *privato*:</span><span class="sxs-lookup"><span data-stu-id="d469a-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="d469a-150">Gli assembly condivisi sono condivisi da tutte le funzioni all'interno di un'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="d469a-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="d469a-151">Per fare riferimento a un assembly personalizzato, caricare l'assembly nell'app di funzione, ad esempio una cartella `bin` nella radice dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d469a-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="d469a-152">Gli assembly privati fanno parte del contesto di una funzione specificata e supportano il caricamento laterale di versioni diverse.</span><span class="sxs-lookup"><span data-stu-id="d469a-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="d469a-153">Gli assembly privati devono essere caricati in una cartella `bin` nella directory di funzione.</span><span class="sxs-lookup"><span data-stu-id="d469a-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="d469a-154">Fare riferimento mediante il nome del file, ad esempio `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="d469a-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="d469a-155">Per informazioni su come caricare i file nella cartella della funzione vedere la sezione seguente sulla gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d469a-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="d469a-156">Directory controllate</span><span class="sxs-lookup"><span data-stu-id="d469a-156">Watched directories</span></span>

<span data-ttu-id="d469a-157">La directory che contiene il file di script della funzione viene controllata automaticamente per le modifiche agli assembly.</span><span class="sxs-lookup"><span data-stu-id="d469a-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="d469a-158">Per controllare le modifiche agli assembly in altre directory, aggiungerle all'elenco `watchDirectories` in [host\.json].</span><span class="sxs-lookup"><span data-stu-id="d469a-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="d469a-159">Uso dei pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="d469a-159">Using NuGet packages</span></span>
<span data-ttu-id="d469a-160">Per usare i pacchetti NuGet in una funzione C#, caricare un file *project.json* nella cartella della funzione nel file system dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d469a-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="d469a-161">Di seguito è riportato un esempio di file *project.json* che aggiunge un riferimento a Microsoft.ProjectOxford.Face versione 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="d469a-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="d469a-162">Poiché è supportato solo .NET Framework 4.6, verificare che nel file *project.json* sia specificato `net46` come illustrato qui.</span><span class="sxs-lookup"><span data-stu-id="d469a-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="d469a-163">Quando si carica un file *project.json* , il runtime ottiene i pacchetti e aggiunge automaticamente riferimenti agli assembly dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d469a-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="d469a-164">Non è necessario aggiungere direttive `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="d469a-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="d469a-165">Per usare i tipi definiti nei pacchetti NuGet è sufficiente aggiungere le istruzioni `using` necessarie al file *run.csx*</span><span class="sxs-lookup"><span data-stu-id="d469a-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="d469a-166">Nel runtime di Funzioni NuGet ripristina le operazioni confrontando `project.json` e `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="d469a-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="d469a-167">Se gli indicatori di data e ora dei file **non** corrispondono, NuGet esegue un ripristino e aggiorna i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d469a-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="d469a-168">In caso contrario, NuGet **non** esegue alcun ripristino.</span><span class="sxs-lookup"><span data-stu-id="d469a-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="d469a-169">Pertanto, `project.lock.json` non deve essere distribuito, in quanto induce NuGet a saltare il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d469a-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="d469a-170">Per evitare la distribuzione del file di blocco, aggiungere `project.lock.json` al `.gitignore` file.</span><span class="sxs-lookup"><span data-stu-id="d469a-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="d469a-171">Per usare un feed NuGet personalizzato, specificare il feed in un *Nuget.Config* nella radice dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d469a-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="d469a-172">Per altre informazioni, vedere [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Configurazione del comportamento di NuGet).</span><span class="sxs-lookup"><span data-stu-id="d469a-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="d469a-173">Uso di un file project.json</span><span class="sxs-lookup"><span data-stu-id="d469a-173">Using a project.json file</span></span>
1. <span data-ttu-id="d469a-174">Aprire la funzione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d469a-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="d469a-175">La scheda dei log mostra l'output di installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d469a-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="d469a-176">Per caricare un file project.json, usare uno dei metodi descritti nella sezione [Come aggiornare i file delle app per le funzioni](functions-reference.md#fileupdate) dell'argomento Guida di riferimento per gli sviluppatori di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d469a-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="d469a-177">Dopo il caricamento del file *project.json* , l'output visualizzato nel log in streaming della funzione è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d469a-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="d469a-178">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="d469a-178">Environment variables</span></span>
<span data-ttu-id="d469a-179">Per ottenere una variabile di ambiente o un valore di impostazione dell'app, usare `System.Environment.GetEnvironmentVariable`come illustrato nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d469a-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="d469a-180">Riutilizzo del codice CSX</span><span class="sxs-lookup"><span data-stu-id="d469a-180">Reusing .csx code</span></span>
<span data-ttu-id="d469a-181">È possibile usare classi e metodi definiti in altri file con estensione *.csx* nel file *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="d469a-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="d469a-182">A questo scopo, usare direttive `#load` nel file *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="d469a-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="d469a-183">Nell'esempio seguente, una routine di registrazione denominata `MyLogger` viene condivisa in *myLogger.csx* e caricata in *run.csx* usando la direttiva `#load`:</span><span class="sxs-lookup"><span data-stu-id="d469a-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="d469a-184">Esempio di *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="d469a-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="d469a-185">Esempio di *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="d469a-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="d469a-186">L'uso di un file *csx* condiviso è una prassi comune quando si vuole tipizzare fortemente gli argomenti tra le funzioni usando un oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="d469a-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="d469a-187">Nell'esempio semplificato seguente, un trigger HTTP e un trigger della coda condividono un oggetto POCO denominato `Order` per tipizzare fortemente i dati dell'ordine:</span><span class="sxs-lookup"><span data-stu-id="d469a-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="d469a-188">File *run.csx* di esempio per il trigger HTTP:</span><span class="sxs-lookup"><span data-stu-id="d469a-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="d469a-189">File *run.csx* di esempio per il trigger della coda:</span><span class="sxs-lookup"><span data-stu-id="d469a-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="d469a-190">File *order.csx* di esempio:</span><span class="sxs-lookup"><span data-stu-id="d469a-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="d469a-191">È possibile usare un percorso relativo con la direttiva `#load` :</span><span class="sxs-lookup"><span data-stu-id="d469a-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="d469a-192">`#load "mylogger.csx"` carica un file che si trova nella cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="d469a-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="d469a-193">`#load "loadedfiles\mylogger.csx"` carica un file che si trova in una sottocartella della cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="d469a-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="d469a-194">`#load "..\shared\mylogger.csx"` carica un file che si trova in una cartella allo stesso livello della cartella della funzione, ovvero direttamente in *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="d469a-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="d469a-195">La direttiva `#load` è compatibile solo con i file con estensione *.csx* (script C# ), non con i file con estensione *.cs*.</span><span class="sxs-lookup"><span data-stu-id="d469a-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="d469a-196">Associazione al runtime mediante associazione imperativa</span><span class="sxs-lookup"><span data-stu-id="d469a-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="d469a-197">In C# e altri linguaggi .NET, è possibile usare un metodo di associazione [imperativa](https://en.wikipedia.org/wiki/Imperative_programming) anziché [ *dichiarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="d469a-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="d469a-198">L'associazione imperativa è utile quando i parametri di associazione devono essere calcolati in fase di runtime invece che in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="d469a-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="d469a-199">Con questo modello è possibile associare rapidamente i dati ad associazioni di input e output supportate nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="d469a-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="d469a-200">Definire un'associazione imperativa, come segue:</span><span class="sxs-lookup"><span data-stu-id="d469a-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="d469a-201">**Non** includere una voce in *function.json* per le associazioni imperative da eseguire.</span><span class="sxs-lookup"><span data-stu-id="d469a-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="d469a-202">Passare un parametro di input [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) o [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="d469a-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="d469a-203">Usare il seguente modello C# per eseguire l'associazione dati.</span><span class="sxs-lookup"><span data-stu-id="d469a-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="d469a-204">dove `BindingTypeAttribute` è l'attributo .NET che definisce l'associazione e `T` è il tipo di input o output supportato da quel tipo di associazione.</span><span class="sxs-lookup"><span data-stu-id="d469a-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="d469a-205">`T` non può essere un tipo di parametro `out`, ad esempio `out JObject`.</span><span class="sxs-lookup"><span data-stu-id="d469a-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="d469a-206">L'associazione di output della tabella App per dispositivi mobili, ad esempio, supporta[ sei tipi di output](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ma è possibile usare solo [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) per `T`.</span><span class="sxs-lookup"><span data-stu-id="d469a-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="d469a-207">L'esempio di codice seguente crea un [associazione di output del BLOB di archiviazione](functions-bindings-storage-blob.md#using-a-blob-output-binding) con percorso del BLOB definito in fase di esecuzione, quindi scrive una stringa per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="d469a-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="d469a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definisce l'associazione di input o output del [BLOB di archiviazione](functions-bindings-storage-blob.md) e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) è un tipo di associazione di output supportato.</span><span class="sxs-lookup"><span data-stu-id="d469a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="d469a-209">Ovvero, il codice ottiene l'impostazione app predefinita per la stringa di connessione dell'account di archiviazione (`AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="d469a-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="d469a-210">È possibile specificare un'impostazione app personalizzata da usare aggiungendo [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passando la matrice di attributi in `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="d469a-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="d469a-211">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="d469a-211">For example,</span></span>

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

<span data-ttu-id="d469a-212">Nella tabella seguente vengono elencati gli attributi .NET per ogni tipo di associazione e i pacchetti in cui sono definiti.</span><span class="sxs-lookup"><span data-stu-id="d469a-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="d469a-213">Associazione</span><span class="sxs-lookup"><span data-stu-id="d469a-213">Binding</span></span> | <span data-ttu-id="d469a-214">Attributo</span><span class="sxs-lookup"><span data-stu-id="d469a-214">Attribute</span></span> | <span data-ttu-id="d469a-215">Aggiungi riferimento</span><span class="sxs-lookup"><span data-stu-id="d469a-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="d469a-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d469a-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="d469a-217">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="d469a-217">Event Hubs</span></span> | <span data-ttu-id="d469a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="d469a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="d469a-219">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="d469a-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="d469a-220">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="d469a-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="d469a-221">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d469a-221">Service Bus</span></span> | <span data-ttu-id="d469a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="d469a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="d469a-223">Coda di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d469a-223">Storage queue</span></span> | <span data-ttu-id="d469a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="d469a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="d469a-225">BLOB di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d469a-225">Storage blob</span></span> | <span data-ttu-id="d469a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="d469a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="d469a-227">Tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d469a-227">Storage table</span></span> | <span data-ttu-id="d469a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="d469a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="d469a-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="d469a-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="d469a-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d469a-230">Next steps</span></span>
<span data-ttu-id="d469a-231">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d469a-231">For more information, see the following resources:</span></span>

* <span data-ttu-id="d469a-232">[Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)</span><span class="sxs-lookup"><span data-stu-id="d469a-232">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="d469a-233">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d469a-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="d469a-234">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="d469a-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="d469a-235">Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d469a-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="d469a-236">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d469a-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
