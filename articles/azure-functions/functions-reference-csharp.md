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
# <a name="azure-functions-c-script-developer-reference"></a>Guida di riferimento a Funzioni di Azure per sviluppatori di script C#
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Hello esperienza di script c# per le funzioni di Azure si basa su hello Azure WebJobs SDK. I dati vengono trasmessi alla funzione C# tramite argomenti del metodo. I nomi di argomento specificati `function.json`, e non vi sono nomi predefiniti per l'accesso alle operazioni quali hello funzione logger e token di annullamento.

Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).

Per informazioni sull'uso delle librerie di classi di C#, vedere [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Usare le librerie di classi di .NET con Funzioni di Azure).

## <a name="how-csx-works"></a>Funzionamento di CSX
Hello `.csx` formato consente toowrite meno "standard" e lo stato attivo sulla scrittura solo una funzione c#. Includere tutti i riferimenti agli assembly e spazi dei nomi all'inizio di hello del file hello come di consueto. Anziché eseguire il wrapping di tutti gli elementi in un spazio dei nomi e classe, definire semplicemente un metodo `Run`. Se è necessario tooinclude tutte le classi, per gli oggetti vecchio oggetto CLR Object (POCO), è possibile includere una classe all'interno di istanza toodefine normale hello stesso file.   

## <a name="binding-tooarguments"></a>Associazione tooarguments
diverse associazioni Hello sono funzione associata tooa c# tramite hello `name` proprietà hello *function.json* configurazione. Ogni associazione ha i propri tipi supportati; ad esempio un trigger di BLOB può supportare una stringa, un POCO o un CloudBlockBlob. tipi supportato Hello sono documentati nella Guida di riferimento per ogni associazione hello. In un oggetto POCO devono essere definiti un metodo Get e un metodo Set per ogni proprietà.

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

## <a name="using-method-return-value-for-output-binding"></a>Uso del valore restituito del metodo per l'associazione di output

È possibile utilizzare un valore restituito del metodo per un'associazione di output, utilizzando nome hello `$return` in *function.json*:

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

## <a name="writing-multiple-output-values"></a>Scrittura di più valori di output

toowrite tooan di più valori di output di associazione, utilizzare hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipi. Questi tipi sono raccolte di sola scrittura vengono scritta toohello associazione di output quando hello metodo viene completato.

Questo esempio scrive più messaggi in coda usando `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Registrazione
toolog output dei log in streaming tooyour in c#, includere un argomento di tipo `TraceWriter`. È consigliabile denominarlo `log`. Evitare di usare `Console.Write` in Funzioni di Azure. 

`TraceWriter`è definito in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). livello di log di Hello `TraceWriter` possono essere configurate in [host\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Async
toomake una funzione asincrona, utilizzare hello `async` (parola chiave) e restituire un `Task` oggetto.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Token di annullamento
Alcune operazioni richiedono l'arresto normale. Mentre è sempre codice toowrite più in grado di gestire un arresto anomalo, nei casi in cui si desidera che le richieste di arresto normale toohandle, definire un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) digitato l'argomento.  Oggetto `CancellationToken` viene fornito toosignal che viene attivato un arresto dell'host.

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

## <a name="importing-namespaces"></a>Importazione di spazi dei nomi
Se è necessario tooimport gli spazi dei nomi, è possibile utilizzare come di consueto, hello `using` clausola.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello seguenti spazi dei nomi vengono importati automaticamente e sono pertanto facoltativi:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Riferimento ad assembly esterni
Per gli assembly di framework, aggiungere i riferimenti utilizzando hello `#r "AssemblyName"` direttiva.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello agli assembly seguenti vengono aggiunti automaticamente dalle funzioni di Azure hello ambiente di hosting:

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

Hello agli assembly seguenti possono fare riferimento nome semplice (ad esempio, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Fare riferimento ad assembly personalizzati

tooreference un assembly personalizzato, è possibile utilizzare un *condivisa* assembly o un *privata* assembly:
- Gli assembly condivisi sono condivisi da tutte le funzioni all'interno di un'app di funzione. tooreference un assembly personalizzato, caricare hello assembly tooyour funzione app, ad esempio un `bin` cartella nella radice di app di funzione hello. 
- Gli assembly privati fanno parte del contesto di una funzione specificata e supportano il caricamento laterale di versioni diverse. Assembly privati devono essere caricati un `bin` cartella nella directory di funzione hello. Riferimento utilizzando come nome del file hello `#r "MyAssembly.dll"`. 

Per informazioni sul funzionamento dei file di cartella funzione tooyour tooupload, vedere hello seguente sezione gestione dei pacchetti.

### <a name="watched-directories"></a>Directory controllate

directory di Hello che contiene i file di script di funzione hello viene controllata automaticamente tooassemblies le modifiche. toowatch per la modifica di assembly in altre directory, aggiungere toohello `watchDirectories` nell'elenco [host\.json].

## <a name="using-nuget-packages"></a>Uso dei pacchetti NuGet
pacchetti di NuGet toouse in una funzione c#, caricare un *Project* cartella toohello della funzione di file nel sistema di file dell'app di funzione hello. Di seguito è riportato un esempio *Project* file che si aggiunge una riferimento tooMicrosoft.ProjectOxford.Face versione 1.1.0:

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

Solo hello .NET Framework 4.6 è supportato, quindi assicurarsi che il *Project* file specifica `net46` come illustrato di seguito.

Quando si carica un *Project* file, recupera i pacchetti hello hello runtime e aggiunge automaticamente gli assembly di riferimenti toohello pacchetto. Non è necessario tooadd `#r "AssemblyName"` direttive. tipi di hello toouse definiti in pacchetti NuGet hello, aggiungere hello necessario `using` istruzioni tooyour *run.csx* file 

In fase di esecuzione funzioni hello ripristino NuGet funziona confrontando `project.json` e `project.lock.json`. Se gli indicatori di data e ora del file hello hello **non** viene eseguito un ripristino NuGet di corrispondenza, e download NuGet pacchetti di aggiornamento. Tuttavia, se hello timbri data e ora del file hello **si** corrispondenza, NuGet non esegue un ripristino. Pertanto, `project.lock.json` non devono essere distribuiti come fa ripristino del pacchetto NuGet tooskip. distribuzione di blocco hello tooavoid file, aggiungere hello `project.lock.json` toohello `.gitignore` file.

toouse un feed NuGet personalizzato, specificare hello feed in un *NuGet* file nella directory principale dell'App di funzione hello. Per altre informazioni, vedere [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Configurazione del comportamento di NuGet).

### <a name="using-a-projectjson-file"></a>Uso di un file project.json
1. Aprire la funzione hello in hello portale di Azure. Hello registra scheda Visualizza hello pacchetto installazione l'output.
2. tooupload un file Project JSON, utilizzare uno dei metodi hello descritti in hello [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate) nell'argomento di riferimento per sviluppatori di Azure funzioni hello.
3. Dopo aver hello *Project* file viene caricato, viene visualizzato l'output come hello nella funzione di esempio seguente del flusso di log:

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
tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `System.Environment.GetEnvironmentVariable`, come illustrato nell'esempio di codice seguente hello:

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

## <a name="reusing-csx-code"></a>Riutilizzo del codice CSX
È possibile usare classi e metodi definiti in altri file con estensione *.csx* nel file *run.csx*. toodo utilizzati, `#load` direttive il *run.csx* file. Nell'esempio seguente di hello, una routine di registrazione è denominato `MyLogger` è condiviso in *myLogger.csx* e caricati in *run.csx* utilizzando hello `#load` direttiva:

Esempio di *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Esempio di *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Utilizzando un oggetto condiviso *csx* è un modello comune quando si desidera toostrongly digitare gli argomenti tra le funzioni di utilizzo di un oggetto POCO. In hello semplificata di esempio seguente, un trigger HTTP e i trigger di coda condividono un oggetto POCO denominato `Order` dati degli ordini toostrongly tipo hello:

File *run.csx* di esempio per il trigger HTTP:

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

File *run.csx* di esempio per il trigger della coda:

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

File *order.csx* di esempio:

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

È possibile utilizzare un percorso relativo con hello `#load` direttiva:

* `#load "mylogger.csx"`Carica un file nella cartella funzione hello.
* `#load "loadedfiles\mylogger.csx"`Carica un file che si trova in una cartella nella cartella funzione hello.
* `#load "..\shared\mylogger.csx"`Carica un file si trova in una cartella hello stesso livello, ovvero come cartella funzione hello, direttamente sotto *wwwroot*.

Hello `#load` direttiva funziona solo con *csx* file (c# script), non con *cs* file.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Associazione al runtime mediante associazione imperativa

In c# e altri linguaggi .NET, è possibile utilizzare un [imperativo](https://en.wikipedia.org/wiki/Imperative_programming) modello di associazione, come toohello anziché [ *dichiarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) associazioni in *function.json*. Associazione imperativo è utile quando i parametri di associazione necessario toobe calcolato in fase di runtime anziché di progettazione. Con questo modello, è possibile associare toosupported input e output associazione il volo nel codice di funzione.

Definire un'associazione imperativa, come segue:

- **Non** includere una voce in *function.json* per le associazioni imperative da eseguire.
- Passare un parametro di input [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) o [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Utilizzare hello seguente c# modello tooperform hello associazione dati.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

dove `BindingTypeAttribute` hello .NET attributo che definisce l'associazione e `T` è hello input o output di tipo supportato dal tipo di associazione. `T` non può essere un tipo di parametro `out`, ad esempio `out JObject`. L'associazione di output della tabella App per dispositivi mobili, ad esempio, supporta[ sei tipi di output](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ma è possibile usare solo [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) per `T`.

Hello esempio di codice seguente crea un [associazione di output blob di archiviazione](functions-bindings-storage-blob.md#using-a-blob-output-binding) con blob percorso definito in fase di esecuzione, quindi scrive un blob toohello stringa.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definisce hello [blob di archiviazione](functions-bindings-storage-blob.md) input o output, associazione e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) è un tipo di associazione di output supportati.
Così com'è, il codice hello Ottiene hello app impostazione predefinita per hello stringa di connessione di account di archiviazione (ovvero `AzureWebJobsStorage`). È possibile specificare un toouse impostazione app personalizzata aggiungendo il [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passando una matrice di attributi hello in `BindAsync<T>()`. Ad esempio,

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

Hello nella tabella seguente elenca gli attributi di hello .NET per i pacchetti di tipo e hello ogni associazione in cui sono definiti.

> [!div class="mx-codeBreakAll"]
| Associazione | Attributo | Aggiungi riferimento |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Hub eventi | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| App per dispositivi mobili | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Hub di notifica | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Bus di servizio | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Coda di archiviazione | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| BLOB di archiviazione | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Tabella di archiviazione | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

* [Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#](functions-reference-fsharp.md)
* [Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure](functions-reference-node.md)
* [Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
