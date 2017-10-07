---
title: 'riferimenti per sviluppatori funzioni F # aaaAzure | Documenti Microsoft'
description: 'Comprendere come toodevelop le funzioni di Azure tramite F #.'
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: Funzioni di Azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server, F#
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="87f01-104">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="87f01-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87f01-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="87f01-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="87f01-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="87f01-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="87f01-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="87f01-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="87f01-108">F # per le funzioni di Azure è una soluzione per l'esecuzione facilmente piccoli frammenti di codice, o "funzioni", nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="87f01-109">I dati vengono trasmessi alla funzione F# tramite argomenti della funzione.</span><span class="sxs-lookup"><span data-stu-id="87f01-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="87f01-110">I nomi di argomento specificati `function.json`, e non vi sono nomi predefiniti per l'accesso alle operazioni quali hello funzione logger e token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="87f01-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="87f01-111">Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="87f01-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="87f01-112">Funzionamento del file con estensione fsx</span><span class="sxs-lookup"><span data-stu-id="87f01-112">How .fsx works</span></span>
<span data-ttu-id="87f01-113">Un file `.fsx` è uno script F#.</span><span class="sxs-lookup"><span data-stu-id="87f01-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="87f01-114">Può essere considerato un progetto F# contenuto in un singolo file.</span><span class="sxs-lookup"><span data-stu-id="87f01-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="87f01-115">file Hello contiene sia codice hello per il programma (in questo caso, la funzione di Azure) e direttive per la gestione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="87f01-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="87f01-116">Quando si utilizza un `.fsx` per una funzione di Azure, in genere gli assembly necessari si automaticamente inclusi automaticamente, consentendo di toofocus sul codice di funzione, anziché "standard" hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="87f01-117">Associazione tooarguments</span><span class="sxs-lookup"><span data-stu-id="87f01-117">Binding tooarguments</span></span>
<span data-ttu-id="87f01-118">Ogni associazione supporta un set di argomenti, come descritto in dettaglio nella hello [riferimenti per sviluppatori trigger e le associazioni di funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="87f01-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="87f01-119">Ad esempio, una delle associazioni degli argomenti hello che supporta un trigger di blob è un POCO, che può essere espresso con un record F #.</span><span class="sxs-lookup"><span data-stu-id="87f01-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="87f01-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="87f01-121">La funzione F# di Azure richiederà uno o più argomenti.</span><span class="sxs-lookup"><span data-stu-id="87f01-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="87f01-122">Quando si parlerà di argomenti di funzioni di Azure, si fa riferimento troppo*input* argomenti e *output* argomenti.</span><span class="sxs-lookup"><span data-stu-id="87f01-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="87f01-123">Un argomento di input sia esattamente ciò che può sembrare: input tooyour funzione Azure F #.</span><span class="sxs-lookup"><span data-stu-id="87f01-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="87f01-124">Un *output* argomento è dati modificabili o `byref<>` argomento che funge da backup dei dati toopass modo *out* della funzione.</span><span class="sxs-lookup"><span data-stu-id="87f01-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="87f01-125">Nell'esempio hello sopra, `blob` è un argomento di input e `output` è un argomento di output.</span><span class="sxs-lookup"><span data-stu-id="87f01-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="87f01-126">Si noti che è stato usato `byref<>` per `output` (non vi è alcun hello tooadd necessità `[<Out>]` annotazione).</span><span class="sxs-lookup"><span data-stu-id="87f01-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="87f01-127">Utilizzando un `byref<>` tipo consente toochange la funzione fa riferimento l'argomento di hello record o un oggetto a.</span><span class="sxs-lookup"><span data-stu-id="87f01-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="87f01-128">Quando un record F # viene utilizzato come un tipo di input, la definizione record hello deve essere contrassegnata con `[<CLIMutable>]` in ordine tooallow hello Azure funzioni framework tooset campi hello in modo appropriato prima che il passaggio di hello tooyour record funzione.</span><span class="sxs-lookup"><span data-stu-id="87f01-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="87f01-129">Quinte hello, `[<CLIMutable>]` genera metodi di impostazione per le proprietà di record di hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="87f01-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="87f01-131">Una classe F# può essere usata negli argomenti di input e di output.</span><span class="sxs-lookup"><span data-stu-id="87f01-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="87f01-132">Per una classe, le proprietà necessitano in genere di getter e setter.</span><span class="sxs-lookup"><span data-stu-id="87f01-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="87f01-133">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="87f01-134">Registrazione</span><span class="sxs-lookup"><span data-stu-id="87f01-134">Logging</span></span>
<span data-ttu-id="87f01-135">toolog output tooyour [i log di streaming](../app-service-web/web-sites-streaming-logs-and-console.md) in F #, la funzione deve accettare un argomento di tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="87f01-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="87f01-136">Per coerenza è consigliabile denominare questo argomento `log`.</span><span class="sxs-lookup"><span data-stu-id="87f01-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="87f01-137">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="87f01-138">Async</span><span class="sxs-lookup"><span data-stu-id="87f01-138">Async</span></span>
<span data-ttu-id="87f01-139">Hello `async` flusso di lavoro può essere utilizzato, ma il risultato di hello deve tooreturn un `Task`.</span><span class="sxs-lookup"><span data-stu-id="87f01-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="87f01-140">Questa operazione può essere eseguita con `Async.StartAsTask`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="87f01-141">Token di annullamento</span><span class="sxs-lookup"><span data-stu-id="87f01-141">Cancellation Token</span></span>
<span data-ttu-id="87f01-142">Se la funzione deve toohandle arresto normale, è possibile assegnare un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="87f01-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="87f01-143">È possibile combinare questo argomento con `async`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="87f01-144">Importazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="87f01-144">Importing namespaces</span></span>
<span data-ttu-id="87f01-145">Spazi dei nomi può essere aperto in hello come di consueto:</span><span class="sxs-lookup"><span data-stu-id="87f01-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="87f01-146">viene automaticamente aperti Hello spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="87f01-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="87f01-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="87f01-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="87f01-148">Riferimento ad assembly esterni</span><span class="sxs-lookup"><span data-stu-id="87f01-148">Referencing External Assemblies</span></span>
<span data-ttu-id="87f01-149">Analogamente, l'assembly framework aggiunti i riferimenti con hello `#r "AssemblyName"` direttiva.</span><span class="sxs-lookup"><span data-stu-id="87f01-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="87f01-150">Hello agli assembly seguenti vengono aggiunti automaticamente dalle funzioni di Azure hello ambiente di hosting:</span><span class="sxs-lookup"><span data-stu-id="87f01-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="87f01-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="87f01-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="87f01-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="87f01-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="87f01-153">Inoltre, hello seguendo gli assembly sono speciale maiuscole/minuscole e possono fare riferimento simplename (ad esempio `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="87f01-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="87f01-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="87f01-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="87f01-155">Se è necessario tooreference assembly privato, è possibile caricare il file di assembly hello in un `bin` cartella tooyour relativa funzione e per riferimento usando hello (ad esempio, il nome di file  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="87f01-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="87f01-156">Per informazioni sul funzionamento dei file di cartella funzione tooyour tooupload, vedere hello seguente sezione gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="87f01-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="87f01-157">Codice introduttivo dell'editor</span><span class="sxs-lookup"><span data-stu-id="87f01-157">Editor Prelude</span></span>
<span data-ttu-id="87f01-158">Un editor che supporta i servizi del compilatore F # non verrà informato di hello gli spazi dei nomi e assembly che include automaticamente le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="87f01-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="87f01-159">Di conseguenza, può essere utile tooinclude preludio che consente di trovare gli assembly hello che si utilizza editor hello e tooexplicitly aprire gli spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="87f01-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="87f01-160">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-160">For example:</span></span>

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

<span data-ttu-id="87f01-161">Quando le funzioni di Azure esegue il codice, elabora origine hello con `COMPILED` definito, pertanto preludio editor hello verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="87f01-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="87f01-162">Gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="87f01-162">Package management</span></span>
<span data-ttu-id="87f01-163">aggiungere pacchetti NuGet toouse in una funzione di F #, un `project.json` cartella della funzione hello toohello file di sistema di file dell'app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="87f01-164">Di seguito è riportato un esempio `project.json` file che si aggiunge un riferimento al pacchetto NuGet troppo`Microsoft.ProjectOxford.Face` versione 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="87f01-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="87f01-165">Solo hello .NET Framework 4.6 è supportato, quindi assicurarsi che il `project.json` file specifica `net46` come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="87f01-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="87f01-166">Quando si carica un `project.json` file, recupera i pacchetti hello hello runtime e aggiunge automaticamente gli assembly di riferimenti toohello pacchetto.</span><span class="sxs-lookup"><span data-stu-id="87f01-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="87f01-167">Non è necessario tooadd `#r "AssemblyName"` direttive.</span><span class="sxs-lookup"><span data-stu-id="87f01-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="87f01-168">È sufficiente aggiungere hello necessario `open` tooyour istruzioni `.fsx` file.</span><span class="sxs-lookup"><span data-stu-id="87f01-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="87f01-169">È possibile tooput automaticamente fa riferimento ad assembly in preludio l'editor, tooimprove l'interazione dell'editor con servizi di compilazione di F #.</span><span class="sxs-lookup"><span data-stu-id="87f01-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="87f01-170">Come tooadd un `project.json` file tooyour Azure (funzione)</span><span class="sxs-lookup"><span data-stu-id="87f01-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="87f01-171">Begin assicurandosi che l'app di funzione è in esecuzione, che è possibile effettuare aprendo la funzione hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="87f01-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="87f01-172">Inoltre fornisce accesso toohello i log in streaming in cui verranno visualizzati output installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="87f01-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="87f01-173">tooupload un `project.json` file, utilizzare uno dei metodi di hello descritti in [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="87f01-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="87f01-174">Se si utilizza [distribuzione continua per le funzioni di Azure](functions-continuous-deployment.md), è possibile aggiungere un `project.json` tooyour ramo in ordine tooexperiment con esso prima di aggiungerlo tooyour ramo di distribuzione di gestione temporanea del file.</span><span class="sxs-lookup"><span data-stu-id="87f01-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="87f01-175">Dopo aver hello `project.json` file viene aggiunto, verrà visualizzato toohello simili di output nella funzione di esempio seguente del flusso di log:</span><span class="sxs-lookup"><span data-stu-id="87f01-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="87f01-176">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="87f01-176">Environment variables</span></span>
<span data-ttu-id="87f01-177">tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `System.Environment.GetEnvironmentVariable`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="87f01-178">Riutilizzo del codice del file con estensione fsx</span><span class="sxs-lookup"><span data-stu-id="87f01-178">Reusing .fsx code</span></span>
<span data-ttu-id="87f01-179">È possibile usare il codice di altri file `.fsx` tramite una direttiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="87f01-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="87f01-180">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87f01-180">For example:</span></span>

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

<span data-ttu-id="87f01-181">Percorsi fornisce toohello `#load` direttiva sono toohello relativo percorso del `.fsx` file.</span><span class="sxs-lookup"><span data-stu-id="87f01-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="87f01-182">`#load "logger.fsx"`Carica un file nella cartella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="87f01-183">`#load "package\logger.fsx"`Carica un file si trova in hello `package` cartella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="87f01-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="87f01-184">`#load "..\shared\mylogger.fsx"`Carica un file si trova in hello `shared` cartella hello stesso livello, ovvero come cartella funzione hello, direttamente sotto `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="87f01-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="87f01-185">Hello `#load` direttiva funziona solo con `.fsx` file (script F #) e non con `.fs` file.</span><span class="sxs-lookup"><span data-stu-id="87f01-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87f01-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87f01-186">Next steps</span></span>
<span data-ttu-id="87f01-187">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="87f01-187">For more information, see hello following resources:</span></span>

* <span data-ttu-id="87f01-188">[F# Guide](/dotnet/articles/fsharp/index) (Guida di F#)</span><span class="sxs-lookup"><span data-stu-id="87f01-188">[F# Guide](/dotnet/articles/fsharp/index)</span></span>
* <span data-ttu-id="87f01-189">[Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)</span><span class="sxs-lookup"><span data-stu-id="87f01-189">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="87f01-190">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="87f01-191">Guida di riferimento per gli sviluppatori C# di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="87f01-192">Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="87f01-193">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="87f01-194">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="87f01-195">Scalabilità di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="87f01-195">Azure Functions scaling</span></span>](functions-scale.md)

