---
title: aaaWork con trigger e le associazioni in funzioni di Azure | Documenti Microsoft
description: Informazioni su come toouse attiva e le associazioni in funzioni di Azure tooconnect l'eventi tooonline esecuzione di codice e i servizi basati su cloud.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Concetti di Trigger e associazioni di Funzioni di Azure
Funzioni di Azure consente toowrite codice in risposta tooevents in Azure e altri servizi, tramite *trigger* e *associazioni*. In questo articolo viene fornita una panoramica concettuale di trigger e associazioni per tutti i linguaggi di programmazione supportati. Funzionalità comuni tooall associazioni sono descritte di seguito.

## <a name="overview"></a>Panoramica

I trigger e le associazioni sono toodefine una modalità dichiarativa per la modalità in cui viene richiamata una funzione e i dati che funziona con. Un *trigger* definisce come viene richiamata una funzione. Una funzione deve avere esattamente un trigger. I trigger sono associati dati, ovvero in genere payload hello che ha attivato la funzione hello. 

Input e output *associazioni* forniscono un toodata tooconnect modalità dichiarativa dall'interno del codice. Tootriggers simile, specificare le stringhe di connessione e altre proprietà nella configurazione di funzione. Le associazioni sono facoltative e una funzione può avere più associazioni di input e output. 

Tramite i trigger e le associazioni, è possibile scrivere codice che è più generico e non impostare come hardcoded i dettagli di hello dei servizi di hello con cui interagisce. I dati provenienti dai servizi diventano semplicemente valori di input per il codice della funzione. servizio di tooanother toooutput dati (ad esempio creando una nuova riga nell'archiviazione tabelle di Azure), utilizzare il valore restituito di hello del metodo hello. In alternativa, se è necessario toooutput più valori, utilizzare un oggetto di supporto. I trigger e le associazioni presentano un **nome** proprietà, che è un identificatore è utilizzare nell'associazione di hello tooaccess codice.

È possibile configurare i trigger e le associazioni in hello **integrazione** scheda nel portale di Azure funzioni hello. In realtà hello, hello dell'interfaccia utente modifica un file denominato *function.json* file nella directory di funzione hello. È possibile modificare questo file modificando toohello **editor avanzato**.

Hello nella tabella seguente mostra i trigger di hello e associazioni che sono supportate con le funzioni di Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Esempio: trigger di coda e tabella di associazione di output

Si supponga toowrite un tooAzure riga nuova archiviazione tabella ogni volta che viene visualizzato un nuovo messaggio nella coda di archiviazione di Azure. Questo scenario può essere implementato tramite un trigger della coda di Azure e una tabella di associazione di output. 

Un trigger di coda richiede le seguenti informazioni in hello hello **integrazione** scheda:

* nome di Hello dell'impostazione di app hello che contiene una stringa di connessione account di archiviazione di hello per coda hello
* nome della coda Hello
* Hello, ad esempio l'identificatore del contenuto di hello tooread codice del messaggio della coda hello `order`.

toowrite tooAzure archiviazione tabelle, utilizzare un'associazione di output con hello seguenti dettagli:

* nome di Hello dell'impostazione di app hello che contiene una stringa di connessione account di archiviazione di hello per tabella hello
* nome della tabella Hello
* Identificatore Hello in toocreate il codice di output elementi o hello il valore restituito dalla funzione hello.

Associazioni utilizzano le impostazioni dell'app per hello tooenforce di connessione stringhe best practice che *function.json* non contiene i segreti di servizio.

Quindi, utilizzare gli identificatori di hello toointegrate fornite con l'archiviazione di Azure nel codice.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Ecco hello *function.json* toohello precedente codice corrispondente. Si noti che è possibile utilizzare configurazione stesso, indipendentemente dal linguaggio hello di implementazione della funzione hello di hello.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
contenuto di hello tooview e modifica di *function.json* in hello portale di Azure, fare clic su hello **editor avanzato** opzione hello **integrazione** scheda della funzione.

Per altri esempi di codice e informazioni dettagliate sull'integrazione con archiviazione di Azure, vedere [Associazioni del BLOB del servizio di archiviazione di Funzioni di Azure](functions-bindings-storage.md).

### <a name="binding-direction"></a>Direzione dell'associazione

Tutti i trigger e le associazioni hanno una proprietà `direction`:

- Per i trigger, è sempre direzione hello`in`
- Le associazioni di input e di output usano `in` e `out`
- Alcune associazioni supportano una direzione speciale `inout`. Se si utilizza `inout`, solo hello **editor avanzato** è disponibile in hello **integrazione** scheda.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Utilizzando tooreturn tipo restituito di funzione hello un singolo output

Hello esempio precedente viene illustrato come toouse hello funzione valore restituito tooprovide output tooa binding, che è possibile utilizzare il parametro di nome speciale hello `$return`. (Questa opzione è supportata solo nei linguaggi che dispongono di un valore restituito, ad esempio C#, JavaScript e F#). Se una funzione include più associazioni di output, utilizzare `$return` per solo una delle associazioni di output di hello. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

esempi di Hello seguente mostra come restituiscono tipi vengono utilizzati con le associazioni di output in c#, JavaScript e F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Proprietà Binding dataType

In .NET, utilizzare hello tipi toodefine hello data type per dati di input. Ad esempio, utilizzare `string` toobind toohello testo di un trigger di coda e un tooread di matrice di byte in formato binario.

Per le lingue che vengono digitate in modo dinamico, ad esempio JavaScript, usare hello `dataType` proprietà nella definizione di associazioni hello. Ad esempio, tooread hello contenuto di una richiesta HTTP in formato binario, utilizzare il tipo di hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Altre opzioni per `dataType` sono `stream` e `string`.

## <a name="resolving-app-settings"></a>Risoluzione di impostazioni app
Come procedura consigliata, i segreti e le stringhe di connessione devono essere gestiti tramite le impostazioni dell'app, invece dei file di configurazione. Questo limita accesso toothese segreti e rende sicuro toostore *function.json* in un repository di controllo del codice sorgente pubblico.

Le impostazioni dell'App sono utili anche ogni volta che si desidera configurazione toochange basata sull'ambiente hello. In un ambiente di test, ad esempio, è consigliabile toomonitor un diverso contenitore di archiviazione blob o coda.

Le impostazioni dell'app vengono risolte ogni volta che un valore è racchiuso tra simboli di percentuale, ad esempio `%MyAppSetting%`. Si noti che hello `connection` proprietà delle associazioni e i trigger è un caso speciale e risolve automaticamente i valori come impostazioni dell'app. 

esempio Hello è un trigger di coda che utilizza un'impostazione app `%input-queue-name%` toodefine hello coda tootrigger in.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Proprietà dei metadati di trigger

In aggiunta toohello payload dei dati forniti da un trigger (ad esempio hello coda dei messaggi che ha attivato una funzione), molti trigger fornire i valori di metadati aggiuntivi. Questi valori possono essere utilizzati come parametri di input in c# e F # o proprietà hello `context.bindings` oggetto in JavaScript. 

Ad esempio, un trigger di coda supporta hello le proprietà seguenti:

* QueueTrigge: attivazione del contenuto del messaggio, se una stringa valida
* DequeueCount
* ExpirationTime
* ID
* InsertionTime
* NextVisibleTime
* PopReceipt

Dettagli delle proprietà dei metadati per tutti i trigger sono descritti nell'argomento di riferimento corrispondente hello. La documentazione è disponibile anche in hello **integrazione** scheda della finestra del portale hello hello **documentazione** sezione sotto l'area di configurazione dell'associazione hello.  

Ad esempio, poiché i trigger di blob presentano alcuni ritardi, è possibile utilizzare un toorun trigger coda la funzione (vedere [Trigger di archiviazione Blob](functions-bindings-storage-blob.md#storage-blob-trigger). messaggio della coda di Hello conterrebbe hello blob filename tootrigger in. Utilizzo di hello `queueTrigger` proprietà dei metadati, è possibile specificare questo comportamento in configurazione, anziché il codice.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Proprietà di metadati da un trigger possono essere utilizzate anche un *espressione dell'associazione* per l'associazione di un altro, come hello descritto nella sezione seguente.

## <a name="binding-expressions-and-patterns"></a>Modelli ed espressioni di associazione

Una delle funzionalità più potenti di hello di trigger e le associazioni è *espressioni di associazione*. All'interno dell'associazione, è possibile definire delle espressioni di modello che possono quindi essere usate in altre associazioni o nel codice. Metadati di trigger possono essere utilizzati anche nell'associazione di espressioni, come illustrato nell'esempio hello nella precedente sezione hello.

Ad esempio, si supponga di voler tooresize immagini nel contenitore di archiviazione blob specifico, simile toohello **dimensioni immagine** modello hello **nuova funzione** pagina. Andare troppo**nuova funzione** -> lingua **c#** -> Scenario **esempi** -> **ImageResizer CSharp**. 

Ecco hello *function.json* definizione:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Si noti che hello `filename` parametro viene utilizzato nella definizione del trigger blob hello nonché a blob hello associazione di output. Questo parametro può essere usato anche nel codice della funzione.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>GUID casuali
Funzioni di Azure fornisce una sintassi pratici per la generazione di GUID nelle associazioni, tramite hello `{rand-guid}` espressione dell'associazione. Hello esempio seguente viene utilizzato questo toogenerate un nome univoco di blob: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Ora corrente

È possibile utilizzare l'espressione di associazione hello `DateTime`, che viene risolta troppo`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Associare le proprietà di input toocustom in un'espressione di associazione

Associazione di espressioni può anche fare riferimento alle proprietà che sono definite nel payload di hello trigger stesso. Ad esempio, è consigliabile toodynamically file di archiviazione blob di tooa binding da un nome specificato in un webhook.

Ad esempio, hello seguente *function.json* Usa una proprietà denominata `BlobName` dal payload trigger hello:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish questo in c# e F #, è necessario definire un POCO che definisce i campi di hello che verranno deserializzati payload trigger hello.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

In JavaScript, viene eseguita automaticamente la deserializzazione JSON ed è possibile utilizzare direttamente le proprietà di hello.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configurazione dell'associazione di dati in fase di runtime

In c# e altri linguaggi .NET, è possibile utilizzare un modello di associazione imperativa, come toohello anziché associazioni dichiarativa *function.json*. Associazione imperativo è utile quando i parametri di associazione necessario toobe calcolato in fase di runtime anziché di progettazione. toolearn informazioni, vedere [associazione in fase di esecuzione tramite i binding imperativo](functions-reference-csharp.md#imperative-bindings) nella Guida di riferimento per sviluppatori hello in c#.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su una particolare associazione, vedere hello seguenti articoli:

- [HTTP e webhook](functions-bindings-http-webhook.md)
- [Timer](functions-bindings-timer.md)
- [Archiviazione code](functions-bindings-storage-queue.md)
- [Archiviazione BLOB](functions-bindings-storage-blob.md)
- [Archiviazione tabelle](functions-bindings-storage-table.md)
- [Hub eventi](functions-bindings-event-hubs.md)
- [Bus di servizio](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Hub di notifica](functions-bindings-notification-hubs.md)
- [App per dispositivi mobili](functions-bindings-mobile-apps.md)
- [File esterno](functions-bindings-external-file.md)
