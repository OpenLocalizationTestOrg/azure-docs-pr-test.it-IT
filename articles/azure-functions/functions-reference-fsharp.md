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
# <a name="azure-functions-f-developer-reference"></a>Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # per le funzioni di Azure è una soluzione per l'esecuzione facilmente piccoli frammenti di codice, o "funzioni", nel cloud hello. I dati vengono trasmessi alla funzione F# tramite argomenti della funzione. I nomi di argomento specificati `function.json`, e non vi sono nomi predefiniti per l'accesso alle operazioni quali hello funzione logger e token di annullamento.

Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).

## <a name="how-fsx-works"></a>Funzionamento del file con estensione fsx
Un file `.fsx` è uno script F#. Può essere considerato un progetto F# contenuto in un singolo file. file Hello contiene sia codice hello per il programma (in questo caso, la funzione di Azure) e direttive per la gestione delle dipendenze.

Quando si utilizza un `.fsx` per una funzione di Azure, in genere gli assembly necessari si automaticamente inclusi automaticamente, consentendo di toofocus sul codice di funzione, anziché "standard" hello.

## <a name="binding-tooarguments"></a>Associazione tooarguments
Ogni associazione supporta un set di argomenti, come descritto in dettaglio nella hello [riferimenti per sviluppatori trigger e le associazioni di funzioni di Azure](functions-triggers-bindings.md). Ad esempio, una delle associazioni degli argomenti hello che supporta un trigger di blob è un POCO, che può essere espresso con un record F #. ad esempio:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

La funzione F# di Azure richiederà uno o più argomenti. Quando si parlerà di argomenti di funzioni di Azure, si fa riferimento troppo*input* argomenti e *output* argomenti. Un argomento di input sia esattamente ciò che può sembrare: input tooyour funzione Azure F #. Un *output* argomento è dati modificabili o `byref<>` argomento che funge da backup dei dati toopass modo *out* della funzione.

Nell'esempio hello sopra, `blob` è un argomento di input e `output` è un argomento di output. Si noti che è stato usato `byref<>` per `output` (non vi è alcun hello tooadd necessità `[<Out>]` annotazione). Utilizzando un `byref<>` tipo consente toochange la funzione fa riferimento l'argomento di hello record o un oggetto a.

Quando un record F # viene utilizzato come un tipo di input, la definizione record hello deve essere contrassegnata con `[<CLIMutable>]` in ordine tooallow hello Azure funzioni framework tooset campi hello in modo appropriato prima che il passaggio di hello tooyour record funzione. Quinte hello, `[<CLIMutable>]` genera metodi di impostazione per le proprietà di record di hello. ad esempio:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Una classe F# può essere usata negli argomenti di input e di output. Per una classe, le proprietà necessitano in genere di getter e setter. Ad esempio:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Registrazione
toolog output tooyour [i log di streaming](../app-service-web/web-sites-streaming-logs-and-console.md) in F #, la funzione deve accettare un argomento di tipo `TraceWriter`. Per coerenza è consigliabile denominare questo argomento `log`. Ad esempio:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Async
Hello `async` flusso di lavoro può essere utilizzato, ma il risultato di hello deve tooreturn un `Task`. Questa operazione può essere eseguita con `Async.StartAsTask`, ad esempio:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Token di annullamento
Se la funzione deve toohandle arresto normale, è possibile assegnare un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argomento. È possibile combinare questo argomento con `async`, ad esempio:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Importazione di spazi dei nomi
Spazi dei nomi può essere aperto in hello come di consueto:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

viene automaticamente aperti Hello spazi dei nomi seguenti:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Riferimento ad assembly esterni
Analogamente, l'assembly framework aggiunti i riferimenti con hello `#r "AssemblyName"` direttiva.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hello agli assembly seguenti vengono aggiunti automaticamente dalle funzioni di Azure hello ambiente di hosting:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Inoltre, hello seguendo gli assembly sono speciale maiuscole/minuscole e possono fare riferimento simplename (ad esempio `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Se è necessario tooreference assembly privato, è possibile caricare il file di assembly hello in un `bin` cartella tooyour relativa funzione e per riferimento usando hello (ad esempio, il nome di file  `#r "MyAssembly.dll"`). Per informazioni sul funzionamento dei file di cartella funzione tooyour tooupload, vedere hello seguente sezione gestione dei pacchetti.

## <a name="editor-prelude"></a>Codice introduttivo dell'editor
Un editor che supporta i servizi del compilatore F # non verrà informato di hello gli spazi dei nomi e assembly che include automaticamente le funzioni di Azure. Di conseguenza, può essere utile tooinclude preludio che consente di trovare gli assembly hello che si utilizza editor hello e tooexplicitly aprire gli spazi dei nomi. ad esempio:

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

Quando le funzioni di Azure esegue il codice, elabora origine hello con `COMPILED` definito, pertanto preludio editor hello verrà ignorato.

<a name="package"></a>

## <a name="package-management"></a>Gestione dei pacchetti
aggiungere pacchetti NuGet toouse in una funzione di F #, un `project.json` cartella della funzione hello toohello file di sistema di file dell'app di funzione hello. Di seguito è riportato un esempio `project.json` file che si aggiunge un riferimento al pacchetto NuGet troppo`Microsoft.ProjectOxford.Face` versione 1.1.0:

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

Solo hello .NET Framework 4.6 è supportato, quindi assicurarsi che il `project.json` file specifica `net46` come illustrato di seguito.

Quando si carica un `project.json` file, recupera i pacchetti hello hello runtime e aggiunge automaticamente gli assembly di riferimenti toohello pacchetto. Non è necessario tooadd `#r "AssemblyName"` direttive. È sufficiente aggiungere hello necessario `open` tooyour istruzioni `.fsx` file.

È possibile tooput automaticamente fa riferimento ad assembly in preludio l'editor, tooimprove l'interazione dell'editor con servizi di compilazione di F #.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Come tooadd un `project.json` file tooyour Azure (funzione)
1. Begin assicurandosi che l'app di funzione è in esecuzione, che è possibile effettuare aprendo la funzione hello portale di Azure. Inoltre fornisce accesso toohello i log in streaming in cui verranno visualizzati output installazione del pacchetto.
2. tooupload un `project.json` file, utilizzare uno dei metodi di hello descritti in [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate). Se si utilizza [distribuzione continua per le funzioni di Azure](functions-continuous-deployment.md), è possibile aggiungere un `project.json` tooyour ramo in ordine tooexperiment con esso prima di aggiungerlo tooyour ramo di distribuzione di gestione temporanea del file.
3. Dopo aver hello `project.json` file viene aggiunto, verrà visualizzato toohello simili di output nella funzione di esempio seguente del flusso di log:

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

## <a name="environment-variables"></a>Variabili di ambiente
tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `System.Environment.GetEnvironmentVariable`, ad esempio:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Riutilizzo del codice del file con estensione fsx
È possibile usare il codice di altri file `.fsx` tramite una direttiva `#load`. ad esempio:

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

Percorsi fornisce toohello `#load` direttiva sono toohello relativo percorso del `.fsx` file.

* `#load "logger.fsx"`Carica un file nella cartella funzione hello.
* `#load "package\logger.fsx"`Carica un file si trova in hello `package` cartella funzione hello.
* `#load "..\shared\mylogger.fsx"`Carica un file si trova in hello `shared` cartella hello stesso livello, ovvero come cartella funzione hello, direttamente sotto `wwwroot`.

Hello `#load` direttiva funziona solo con `.fsx` file (script F #) e non con `.fs` file.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

* [F# Guide](/dotnet/articles/fsharp/index) (Guida di F#)
* [Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)
* [Guida di riferimento per gli sviluppatori C# di Funzioni di Azure](functions-reference-csharp.md)
* [Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure](functions-reference-node.md)
* [Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md)
* [Test di Funzioni di Azure](functions-test-a-function.md)
* [Scalabilità di Funzioni di Azure](functions-scale.md)

