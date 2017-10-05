---
title: Guida di riferimento per gli sviluppatori di Funzioni di Azure in F# | Documentazione Microsoft
description: Informazioni su come sviluppare Funzioni di Azure in F#.
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: 'Azure funzioni, funzioni, l''elaborazione di eventi, webhook, calcolo dinamico, senza architettura, F #'
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="e6a0b-104">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="e6a0b-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6a0b-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="e6a0b-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="e6a0b-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="e6a0b-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="e6a0b-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e6a0b-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="e6a0b-108">F# per Funzioni di Azure è una soluzione che consente di eseguire facilmente piccole parti di codice, o "funzioni", nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="e6a0b-109">I dati vengono trasmessi alla funzione F# tramite argomenti della funzione.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="e6a0b-110">I nomi di argomento sono specificati in `function.json`e sono disponibili nomi predefiniti per l'accesso a elementi quali il logger delle funzioni e i token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="e6a0b-111">Questo articolo presuppone che l'utente abbia già letto [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e6a0b-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="e6a0b-112">Funzionamento del file con estensione fsx</span><span class="sxs-lookup"><span data-stu-id="e6a0b-112">How .fsx works</span></span>
<span data-ttu-id="e6a0b-113">Un file `.fsx` è uno script F#.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="e6a0b-114">Può essere considerato un progetto F# contenuto in un singolo file.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="e6a0b-115">Il file contiene il codice per il programma (in questo caso la funzione di Azure) e direttive per la gestione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="e6a0b-116">Quando si usa un file `.fsx` per una funzione di Azure, gli assembly normalmente necessari sono inclusi automaticamente, consentendo di concentrarsi sulla funzione anziché sul codice "boilerplate".</span><span class="sxs-lookup"><span data-stu-id="e6a0b-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="e6a0b-117">Associazione agli argomenti</span><span class="sxs-lookup"><span data-stu-id="e6a0b-117">Binding to arguments</span></span>
<span data-ttu-id="e6a0b-118">Ogni associazione supporta set di argomenti, come descritto nei dettagli in [Guida di riferimento per gli sviluppatori di trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="e6a0b-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="e6a0b-119">Ad esempio, una delle associazioni di argomento supportate da un trigger del BLOB è un oggetto POCO, che può essere espresso con un record F#.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="e6a0b-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="e6a0b-121">La funzione F# di Azure richiederà uno o più argomenti.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="e6a0b-122">Per "argomenti di Funzioni di Azure" si intendono argomenti di *input* e argomenti di *output*.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="e6a0b-123">Un argomento di input rappresenta un input per la funzione F# di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="e6a0b-124">Un argomento di *output* è costituito da dati modificabili oppure è un argomento `byref<>` usato per passare di nuovo dati *in uscita* dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="e6a0b-125">Nell'esempio precedente, `blob` è un argomento di input, mentre `output` è un argomento di output.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="e6a0b-126">Si noti che è stato usato `byref<>` per `output`. Non è necessario aggiungere l'annotazione `[<Out>]`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="e6a0b-127">L'uso di un tipo `byref<>` consente alla funzione di cambiare il record o l'oggetto cui l'argomento fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="e6a0b-128">Quando un record F# viene usato come tipo di input, la definizione del record deve essere contrassegnata con `[<CLIMutable>]` per consentire al framework di Funzioni di Azure di impostare i campi in modo appropriato prima di passare il record alla funzione.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="e6a0b-129">`[<CLIMutable>]` genera setter in background per le proprietà del record.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="e6a0b-130">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="e6a0b-131">Una classe F# può essere usata negli argomenti di input e di output.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="e6a0b-132">Per una classe, le proprietà necessitano in genere di getter e setter.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="e6a0b-133">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="e6a0b-134">Registrazione</span><span class="sxs-lookup"><span data-stu-id="e6a0b-134">Logging</span></span>
<span data-ttu-id="e6a0b-135">Per registrare l'output nei [log in streaming](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, la funzione deve accettare un argomento di tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="e6a0b-136">Per coerenza è consigliabile denominare questo argomento `log`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="e6a0b-137">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="e6a0b-138">Async</span><span class="sxs-lookup"><span data-stu-id="e6a0b-138">Async</span></span>
<span data-ttu-id="e6a0b-139">È possibile usare il flusso di lavoro `async`, ma il risultato deve restituire un oggetto `Task`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="e6a0b-140">Questa operazione può essere eseguita con `Async.StartAsTask`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="e6a0b-141">Token di annullamento</span><span class="sxs-lookup"><span data-stu-id="e6a0b-141">Cancellation Token</span></span>
<span data-ttu-id="e6a0b-142">Se la funzione deve gestire l'arresto normale, è possibile assegnarle un argomento [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e6a0b-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="e6a0b-143">È possibile combinare questo argomento con `async`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="e6a0b-144">Importazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="e6a0b-144">Importing namespaces</span></span>
<span data-ttu-id="e6a0b-145">Gli spazi dei nomi possono essere aperti nel modo consueto:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="e6a0b-146">I seguenti spazi dei nomi vengono aperti automaticamente:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="e6a0b-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="e6a0b-148">Riferimento ad assembly esterni</span><span class="sxs-lookup"><span data-stu-id="e6a0b-148">Referencing External Assemblies</span></span>
<span data-ttu-id="e6a0b-149">In maniera analoga, i riferimenti per l'assembly del framework vengono aggiunti con la direttiva `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="e6a0b-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="e6a0b-150">Gli assembly seguenti vengono aggiunti automaticamente dall'ambiente di hosting di Funzioni di Azure:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="e6a0b-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="e6a0b-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="e6a0b-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="e6a0b-153">Gli assembly seguenti sono anche casi speciali ai quali è possibile fare riferimento tramite simplename, ad esempio `#r "AssemblyName"`:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="e6a0b-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="e6a0b-155">Per fare riferimento a un assembly privato è possibile caricare il file dell'assembly in una cartella `bin` relativa alla funzione e farvi riferimento usando il nome file, ad esempio `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="e6a0b-156">Per informazioni su come caricare i file nella cartella della funzione vedere la sezione seguente sulla gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="e6a0b-157">Codice introduttivo dell'editor</span><span class="sxs-lookup"><span data-stu-id="e6a0b-157">Editor Prelude</span></span>
<span data-ttu-id="e6a0b-158">Un editor che supporta i servizi di compilazione F# non è in grado di riconoscere gli spazi dei nomi e gli assembly inclusi automaticamente con Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="e6a0b-159">Può quindi essere utile includere un codice introduttivo che consenta all'editor di trovare gli assembly usati e di aprire in modo esplicito gli spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="e6a0b-160">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="e6a0b-161">Quando esegue il codice, Funzioni di Azure elabora l'origine con `COMPILED` definito, quindi il codice introduttivo dell'editor verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="e6a0b-162">Gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e6a0b-162">Package management</span></span>
<span data-ttu-id="e6a0b-163">Per usare i pacchetti NuGet in una funzione F#, aggiungere un file `project.json` nella cartella della funzione nel file system dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="e6a0b-164">Di seguito è riportato un esempio di file `project.json` che aggiunge un riferimento ai pacchetti NuGet a `Microsoft.ProjectOxford.Face` versione 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="e6a0b-165">È supportato solo .NET Framework 4.6, quindi verificare che nel file `project.json` sia specificato `net46` come qui illustrato.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="e6a0b-166">Quando si carica un file `project.json` , il runtime ottiene i pacchetti e aggiunge automaticamente riferimenti agli assembly dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="e6a0b-167">Non è necessario aggiungere direttive `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="e6a0b-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="e6a0b-168">È sufficiente aggiungere le istruzioni `open` necessarie al file `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="e6a0b-169">Si consiglia di inserire gli assembly con riferimento automatico nel codice introduttivo dell'editor, per migliorare l'interazione dell'editor con i servizi di compilazione F#.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="e6a0b-170">Come aggiungere un file `project.json` alla funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="e6a0b-171">Assicurarsi prima di tutto che l'app di funzione sia in esecuzione aprendo la funzione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="e6a0b-172">In questo modo è anche possibile accedere ai log in streaming in cui verrà visualizzato l'output di installazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="e6a0b-173">Per caricare un file `project.json` , usare uno dei metodi descritti in [Come aggiornare i file delle app per le funzioni](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="e6a0b-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="e6a0b-174">Se si usa la [distribuzione continua per Funzioni di Azure](functions-continuous-deployment.md), è possibile aggiungere un file `project.json` al ramo di staging per eseguire qualche esperimento prima di aggiungerlo al ramo di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="e6a0b-175">Dopo l'aggiunta del file `project.json` , l'output visualizzato nel log in streaming della funzione sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="e6a0b-176">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="e6a0b-176">Environment variables</span></span>
<span data-ttu-id="e6a0b-177">Per ottenere una variabile di ambiente o un valore di impostazione dell'app, usare `System.Environment.GetEnvironmentVariable`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="e6a0b-178">Riutilizzo del codice del file con estensione fsx</span><span class="sxs-lookup"><span data-stu-id="e6a0b-178">Reusing .fsx code</span></span>
<span data-ttu-id="e6a0b-179">È possibile usare il codice di altri file `.fsx` tramite una direttiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="e6a0b-180">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="e6a0b-181">I percorsi specificati per la direttiva `#load` sono relativi alla posizione del file `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="e6a0b-182">`#load "logger.fsx"` carica un file che si trova nella cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="e6a0b-183">`#load "package\logger.fsx"` carica un file che si trova nella sottocartella `package` della cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="e6a0b-184">`#load "..\shared\mylogger.fsx"` carica un file che si trova nella cartella `shared` allo stesso livello della cartella della funzione, ovvero direttamente in `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="e6a0b-185">La direttiva `#load` funziona solo con i file `.fsx` (script F# ), non con i file `.fs`.</span><span class="sxs-lookup"><span data-stu-id="e6a0b-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6a0b-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6a0b-186">Next steps</span></span>
<span data-ttu-id="e6a0b-187">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="e6a0b-187">For more information, see the following resources:</span></span>

* <span data-ttu-id="e6a0b-188">[F# Guide](/dotnet/articles/fsharp/index) (Guida di F#)</span><span class="sxs-lookup"><span data-stu-id="e6a0b-188">[F# Guide](/dotnet/articles/fsharp/index)</span></span>
* <span data-ttu-id="e6a0b-189">[Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)</span><span class="sxs-lookup"><span data-stu-id="e6a0b-189">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="e6a0b-190">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="e6a0b-191">Guida di riferimento per gli sviluppatori C# di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="e6a0b-192">Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="e6a0b-193">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="e6a0b-194">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="e6a0b-195">Scalabilità di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e6a0b-195">Azure Functions scaling</span></span>](functions-scale.md)

