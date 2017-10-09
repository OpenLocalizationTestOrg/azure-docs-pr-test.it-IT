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
# <a name="using-net-class-libraries-with-azure-functions"></a>Uso di librerie di classi .NET con Funzioni di Azure

File tooscript, le funzioni di Azure supporta inoltre la pubblicazione di una libreria di classi come implementazione hello per le funzioni di uno o più. È consigliabile usare hello [Azure funzioni 2017 Visual Studio Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Prerequisiti 

In questo articolo presenta hello seguenti prerequisiti:

- [Visual Studio 2017 Preview versione 15.3](https://www.visualstudio.com/vs/preview/). Installare i carichi di lavoro hello **sviluppo web ASP.NET e** e **lo sviluppo di Azure**.
- [Visual Studio 2017 Tools per Funzioni di Azure](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Progetto di libreria di classi per Funzioni

Creare un progetto per Funzioni di Azure in Visual Studio. il nuovo modello di progetto Hello crea file hello *host.json* e *local.settings.json*. È possibile [personalizzare le impostazioni di runtime di Funzioni di Azure nel file host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

file Hello *local.settings.json* archivia le impostazioni dell'app, le stringhe di connessione e le impostazioni per strumenti di base di funzioni di Azure. toolearn più sulla relativa struttura, vedere [codice e il test funzioni di Azure localmente](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Attributo FunctionName

attributo Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) contrassegna un metodo come un punto di ingresso della funzione. Deve essere usato con un solo trigger e con 0 o più associazioni di input e di output.

### <a name="conversion-toofunctionjson"></a>Conversione toofunction.json

Quando viene compilato un progetto di funzioni di Azure, viene generato un file `function.json` nella directory hello corrisponde al nome della funzione hello è definito da `[FunctionName]`. Specifica i trigger e le associazioni e file di assembly progetto toohello punti.

Questa conversione viene eseguita dal pacchetto NuGet hello [Microsoft\.NET\.Sdk\.funzioni](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). origine Hello è disponibile nel repository GitHub hello [azure\-funzioni\-vs\-compilare\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Trigger e associazioni

Hello nella tabella seguente sono elencati i trigger di hello e associazioni che sono disponibili in un progetto libreria di classi di funzioni di Azure. Tutti gli attributi sono nello spazio dei nomi hello `Microsoft.Azure.WebJobs`.

| Associazione | Attributo | Pacchetto NuGet |
|------   | ------    | ------        |
| [Trigger, input e output per archiviazione BLOB](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Archiviazione BLOB] |
| [Associazione di input e di output per Cosmos DB](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Trigger e output per Hub eventi](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Input e output per file esterni](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Trigger per HTTP e webhook](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Input e output per App per dispositivi mobili](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Output per Hub di notifica](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Trigger e output per l'archiviazione code](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Output SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Trigger e output per il bus di servizio](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Input e output per l'archiviazione tabelle](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Trigger timer](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Output di Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Associazioni di trigger, input e output per l'archiviazione BLOB

Funzioni di Azure supporta i trigger e le associazioni di input e di output per l'archiviazione BLOB di Azure. Per altre informazioni sulle espressioni di associazione e sui metadati, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).

Viene definito un trigger di blob con hello `[BlobTrigger]` attributo. È possibile utilizzare l'attributo hello `[StorageAccount]` account di archiviazione hello toodefine utilizzato da un'intera funzione o una classe.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

BLOB di input e output vengono definiti utilizzando hello `[Blob]` attributo, insieme con un `FileAccess` parametro che indica di lettura o scrittura. Hello in seguito viene illustrato come utilizzare un trigger di blob e blob di associazione di output.

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

### <a name="cosmos-db-input-and-output-bindings"></a>Associazioni di input e di output per Cosmos DB

Funzioni di Azure supporta le associazioni di input e output per Cosmos DB. toolearn più caratteristiche di hello di associazione di hello Cosmos DB, vedere [associazioni Azure funzioni Cosmos DB](functions-bindings-documentdb.md).

toobind tooa documento Cosmos DB, utilizzare l'attributo hello `[DocumentDB]` nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Hello di esempio seguente è un trigger di coda e una API DocumentDB associazione di output:

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

### <a name="event-hubs-trigger-and-output"></a>Trigger e output per Hub eventi

Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi. Per altre informazioni, vedere [Associazioni di Hub eventi di Funzioni di Azure](functions-bindings-event-hubs.md).

tipi di Hello `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` e `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello esempio seguente viene utilizzato un trigger di Hub eventi:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Hello esempio seguente è presente un Hub di eventi di output, con valore restituito del metodo hello come output di hello:

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

### <a name="external-file-input-and-output"></a>Input e output per file esterni

Funzioni di Azure supporta il trigger e le associazioni di input e di output per file esterni, ad esempio Google Drive, Dropbox e OneDrive. vedere, più toolearn [associazioni di File esterno di Azure funzioni](functions-bindings-external-file.md). Hello attributi `[ExternalFileTrigger]` e `[ExternalFile]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hello esempio c# seguente viene illustrato un file esterno di input e output di associazione. copie di codice Hello hello file di output toohello file di input.

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

### <a name="http-and-webhooks"></a>HTTP e webhook

Hello utilizzare `HttpTrigger` trigger toodefine HTTP attributo o webhook. Questo attributo viene definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http]. È possibile personalizzare il livello di autorizzazione hello, tipo webhook, route e metodi. esempio Hello definisce un trigger HTTP con l'autenticazione anonima e _genericJson_ tipo webhook.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Input e output per App per dispositivi mobili

Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili. vedere, più toolearn [associazioni di App mobili di Azure funzioni](functions-bindings-mobile-apps.md). attributo Hello `[MobileTable]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].

esempio Hello illustra un'App per dispositivi mobili associazione di output:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Output per Hub di notifica

Funzioni di Azure supporta un'associazione di output per Hub di notifica. vedere, più toolearn [associazione di output di Hub di notifica di Azure funzioni](functions-bindings-notification-hubs.md). attributo Hello `[NotificationHub]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Trigger e output per l'archiviazione code

Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure. Per altre informazioni, vedere [Associazioni di archiviazione code in Funzioni di Azure](functions-bindings-storage-queue.md).

Hello esempio seguente viene illustrato come toouse hello tipo restituito dalla funzione con un coda di output di associazione, tramite hello `[Queue]` attributo. toodefine un trigger di coda, utilizzare hello `[QueueTrigger]` attributo.

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

### <a name="sendgrid-output"></a>Output di SendGrid

Funzioni di Azure supporta un'associazione di output di SendGrid per inviare tramite posta elettronica a livello di programmazione. vedere, più toolearn [associazioni Azure funzioni SendGrid](functions-bindings-sendgrid.md).

attributo Hello `[SendGrid]` è definito nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Hello seguito è riportato un esempio di utilizzo di un trigger di coda del Bus di servizio e un'associazione di output SendGrid utilizzando `SendGridMessage`:

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

### <a name="service-bus-trigger-and-output"></a>Trigger e output per il bus di servizio

Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio. Per altre informazioni sulla configurazione delle associazioni, vedere [Associazioni del bus di servizio di Funzioni di Azure](functions-bindings-service-bus.md).

Hello attributi `[ServiceBusTrigger]` e `[ServiceBus]` sono definiti nel pacchetto NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello Ecco un esempio di un trigger di coda del Bus di servizio:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Hello Ecco un esempio di output un Bus di servizio di associazione, utilizzando il tipo restituito del metodo di hello come output di hello:

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

### <a name="table-storage-input-and-output"></a>Input e output per l'archiviazione tabelle

Funzioni di Azure supporta le associazioni di input e output per l'archiviazione tabelle di Azure. vedere, più toolearn [associazioni di archiviazione di Azure funzioni tabella](functions-bindings-storage-table.md).

Hello seguente viene illustrata una classe con due funzioni, che illustra l'output di archiviazione tabella e le associazioni di input. 

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

### <a name="timer-trigger"></a>Trigger timer

Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita. toolearn più caratteristiche di hello di associazione di hello, vedere [pianificare l'esecuzione di codice con le funzioni di Azure](functions-bindings-timer.md).

Piano di consumo hello, è possibile definire pianificazioni con un [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Se si usa un piano di servizio app, è anche possibile usare una stringa TimeSpan. 

Hello di esempio seguente definisce un trigger timer che viene eseguita ogni 5 minuti:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Output di Twilio

I messaggi di testo SMS toosend funzioni di Azure supporta funzioni Twilio output tooenable associazioni. vedere, più toolearn [messaggi inviare SMS da funzioni di Azure utilizzando hello Twilio output associazione](functions-bindings-twilio.md). 

attributo Hello `[TwilioSms]` è definito nel pacchetto hello [Microsoft.Azure.WebJobs.Extensions.Twilio].

esempio c# seguente Hello utilizza una coda trigger e un Twilio associazione di output:

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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'uso di Funzioni di Azure in script C#, vedere [Guida di riferimento per gli sviluppatori C\# di Funzioni di Azure](functions-reference-csharp.md).

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
