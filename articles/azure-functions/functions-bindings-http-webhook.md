---
title: associazioni di funzioni HTTP e webhook aaaAzure | Documenti Microsoft
description: Comprendere come toouse HTTP e webhook i trigger e le associazioni in funzioni di Azure.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: funzioni di Azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server, HTTP, API, REST
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Associazioni HTTP e webhook in Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come tooconfigure e funziona con HTTP attiva e le associazioni in funzioni di Azure.
Queste operazioni, è possibile utilizzare funzioni di Azure toobuild senza server API e rispondere toowebhooks.

Funzioni di Azure fornisce hello seguenti associazioni:
- Un [trigger HTTP](#httptrigger) consente di richiamare una funzione con una richiesta HTTP Può essere personalizzato toorespond troppo[webhook](#hooktrigger).
- Un [associazione di output HTTP](#output) consente toorespond toohello richiesta.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Trigger HTTP
trigger HTTP Hello eseguirà la funzione nella richiesta HTTP tooan di risposta. È possibile personalizzarlo toorespond tooa determinato URL o un set di metodi HTTP. Un trigger HTTP può anche essere toowebhooks toorespond configurato. 

Se tramite il portale di funzioni hello, è possibile inoltre iniziare subito usando un modello predefinito. Selezionare **nuova funzione** e scegliere "Webhook & API" hello **Scenario** elenco a discesa. Selezionare uno dei modelli di hello e fare clic su **crea**.

Per impostazione predefinita, un trigger HTTP risponderà toohello richiesta con un codice di stato HTTP 200 OK e un corpo vuoto. toomodify risposta hello, configurare un [associazione di output HTTP](#output)

### <a name="configuring-an-http-trigger"></a>Configurazione di un trigger HTTP
Includendo un toohello simile oggetto JSON seguente in hello è definito un trigger HTTP `bindings` matrice function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
associazione di Hello supporta hello le proprietà seguenti:

* **nome** : obbligatorio - nome della variabile hello utilizzati nel codice della funzione per richiesta hello o il corpo della richiesta. Vedere [Uso di un trigger HTTP dal codice](#httptriggerusage).
* **tipo** : obbligatorio - deve essere impostato troppo "httpTrigger".
* **direzione** : obbligatorio - deve essere impostato troppo "in".
* _authLevel_ : questo parametro determina quali tasti, se presente, è necessario toobe presente nella richiesta di hello nella funzione di ordine tooinvoke hello. Vedere [Uso delle chiavi](#keys) più avanti. il valore di Hello può essere uno dei seguenti hello:
    * _anonymous_: nessuna chiave API obbligatoria.
    * _function_: è obbligatoria una chiave API specifica della funzione. Questo è il valore di predefinito hello se non è specificato.
    * _amministrazione_ : hello master chiave è obbligatoria.
* **metodi** : si tratta di una matrice di metodi HTTP hello funzione hello toowhich risponderà. Se non specificato, la funzione hello risponderà metodi tooall HTTP. Vedere [personalizzazione endpoint HTTP hello](#url).
* **route** : definisce il modello di route hello, controllo toowhich URL risponderà la funzione richiesta. Hello valore predefinito se non è specificato è `<functionname>`. Vedere [personalizzazione endpoint HTTP hello](#url).
* **webHookType** : hello HTTP trigger tooact viene quindi configurato come il ricevitore un webhook per provider specificato hello. Hello _metodi_ proprietà non deve essere impostata se si è scelto. Vedere [toowebhooks risposta](#hooktrigger). il valore di Hello può essere uno dei seguenti hello:
    * _genericJson_: endpoint di webhook per utilizzo generico senza logica per un provider specifico.
    * _github_ : funzione hello risponderà tooGitHub webhook. Hello _authLevel_ proprietà non deve essere impostata se si è scelto.
    * _il margine di flessibilità_ : funzione hello risponderà tooSlack webhook. Hello _authLevel_ proprietà non deve essere impostata se si è scelto.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Uso di un trigger HTTP dal codice
Per le funzioni di c# e F #, è possibile dichiarare il tipo di hello di toobe di input il trigger è `HttpRequestMessage` o un tipo personalizzato. Se si sceglie `HttpRequestMessage`, si otterrà un oggetto di richiesta di accesso completo toohello. Per un tipo personalizzato (ad esempio un POCO), funzioni tenterà il corpo della richiesta hello tooparse come proprietà dell'oggetto JSON toopopulate hello.

Per le funzioni di Node.js, hello funzioni runtime fornisce il corpo della richiesta hello anziché l'oggetto richiesta hello.

Vedere [Esempi di trigger HTTP](#httptriggersample) per gli utilizzi di esempio.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Associazione di output della risposta HTTP
Utilizzare hello output associazione toorespond toohello HTTP richiesta mittente HTTP. Questa associazione consente risposta hello toocustomize associata alla richiesta del trigger hello e richiede un trigger HTTP. Se non viene specificata un'associazione di output HTTP, un trigger HTTP restituirà HTTP 200 OK con un corpo vuoto. 

### <a name="configuring-an-http-output-binding"></a>Configurazione di un'associazione di output HTTP
output di Hello HTTP viene definita l'associazione includendo un toohello simile oggetto JSON seguente in hello `bindings` matrice function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
associazione di Hello contiene hello le proprietà seguenti:

* **nome** : obbligatorio - hello nome della variabile utilizzata nel codice di funzione per hello risposta. Vedere [Uso di un'associazione di output HTTP dal codice](#outputusage).
* **tipo** : obbligatorio - deve essere impostato troppo "http".
* **direzione** : obbligatorio - deve essere impostato troppo "out".

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Uso di un'associazione di output HTTP dal codice
È possibile utilizzare hello output parametro (ad esempio, "Risoluzione") toorespond toohello http o webhook chiamante. In alternativa, è possibile utilizzare lo standard `Request.CreateResponse()` (c#) o `context.res` tooreturn modello (Node.JS) nella risposta. Per esempi su come toouse hello quest'ultimo metodo, vedere [esempi di trigger HTTP](#httptriggersample) e [esempi di trigger Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Risponde toowebhooks
Un trigger HTTP con hello _webHookType_ proprietà sarà configurato toorespond troppo[webhook](https://en.wikipedia.org/wiki/Webhook). configurazione di base Hello utilizza l'impostazione "genericJson" hello. Questo limita richieste tooonly quelle che usano HTTP POST e con hello `application/json` tipo di contenuto.

Hello trigger può inoltre essere personalizzati tooa webhook specifici provider (ad esempio, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)). Se viene specificato un provider, hello funzioni runtime può svolgere della logica di convalida del provider di hello automaticamente.  

### <a name="configuring-github-as-a-webhook-provider"></a>Configurazione di GitHub come provider di webhook
toorespond tooGitHub webhook, innanzitutto creare una funzione con un Trigger di HTTP e imposta hello _webHookType_ proprietà troppo "github". Copiare quindi l'[URL](#url) e la [chiave API](#keys) nella pagina **Add webhook** (Aggiungi webhook) del repository GitHub. Per altre informazioni, vedere la documentazione [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) (Creazione di webhook) di GitHub.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Configurazione di Slack come provider di webhook
Hello Slack webhook genera un token per l'utente invece che consente di specificare, pertanto è necessario configurare una chiave specifica con token hello da Slack. Vedere [Uso delle chiavi](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Personalizzazione di endpoint HTTP hello
Per impostazione predefinita quando si crea una funzione per un trigger HTTP o WebHook, la funzione hello è indirizzabile tramite una route di form hello:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

È possibile personalizzare questa route tramite hello facoltativo `route` proprietà trigger hello HTTP l'input dell'associazione. Ad esempio, hello seguente *function.json* file definisce un `route` proprietà per un trigger HTTP:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Con questa configurazione, la funzione hello è indirizzabile con hello successivo itinerario anziché route originale hello.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

In questo modo il codice di funzione hello toosupport due parametri indirizzo hello, "category" e "id". I parametri sono compatibili con qualsiasi [vincolo di route dell'API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints). Hello seguente di codice della funzione in c# si avvalgono di entrambi i parametri.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Qui è Node.js funzione codice toouse hello stessi parametri di route.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Per impostazione predefinita, tutte le route di funzione sono precedute da *api*. È anche possibile personalizzare o rimuovere il prefisso di hello utilizzando hello `http.routePrefix` proprietà il *host.json* file. esempio Hello rimuove hello *api* prefisso della route utilizzando una stringa vuota per il prefisso di hello in hello *host.json* file.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Per informazioni dettagliate su come hello tooupdate *host.json* file per la funzione, vedere [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate). 

Per informazioni su altre proprietà che è possibile configurare nel file *host.json*, vedere il [riferimento su host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Uso delle chiavi
Gli elementi HttpTrigger possono sfruttare le chiavi per una maggiore sicurezza. Un HttpTrigger standard possibile utilizzare queste informazioni come una chiave API, che richiedono toobe chiave hello hello richiesta. Webhook è possono utilizzare chiavi tooauthorize richieste in diversi modi, a seconda di quale provider hello supporta.

Le chiavi vengono archiviate come parte dell'app per le funzioni in Azure e crittografate inattive. tooview le chiavi, creare nuovi o toonew valori delle chiavi di raggruppamento, passare tooone delle funzioni nel portale di hello e selezionare "Gestisci". 

Esistono due tipi di chiavi:
- **Host chiavi**: queste chiavi sono condivisi da tutte le funzioni all'interno di app di funzione hello. Quando viene utilizzata come una chiave API, questi consente accesso tooany funzione all'interno di app di funzione hello.
- **Tasti funzione**: queste chiavi si applicano solo toohello funzioni specifiche in cui sono definiti. Quando viene utilizzata come una chiave API, solo consente accesso toothat funzione.

Ogni chiave è denominato per riferimento e a livello di funzione e host hello è una chiave predefinita (denominata "default"). Hello **chiave master** è una chiave host predefinita denominata "_master" che è definita per ogni app di funzione e non può essere revocata. Fornisce l'API di runtime toohello accesso amministrativo. Utilizzando `"authLevel": "admin"` in hello associazione JSON richiederà questa chiave toobe presentato su richiesta hello; qualsiasi altro tasto comporterà un errore di autorizzazione.

> [!NOTE]
> Scadenza toohello elevati le autorizzazioni consentite dalla chiave master di hello, è consigliabile non condividono questa chiave con terze parti o distribuirlo nelle applicazioni client native. Prestare attenzione quando si sceglie di livello di autorizzazione di amministratore hello.
> 
> 

### <a name="api-key-authorization"></a>Autorizzazione della chiave API
Per impostazione predefinita, un HttpTrigger richiede una chiave API nella richiesta HTTP hello. La richiesta HTTP in genere è quindi simile alla seguente:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

chiave Hello può essere incluso in una variabile di stringa di query denominata `code`, come sopra, o può essere incluso un `x-functions-key` intestazione HTTP. il valore di Hello della chiave hello può essere qualsiasi tasto di funzione definiti per la funzione hello o qualsiasi chiave host.

È possibile scegliere le richieste di tooallow senza chiavi o specificare la chiave master di hello deve essere usata da modifica hello `authLevel` proprietà hello associazione JSON (vedere [trigger HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Chiavi e webhook
Parte di hello HttpTrigger e il meccanismo di hello varia in base al tipo webhook hello Webhook l'autorizzazione viene gestita dal componente di hello webhook il ricevitore. Ogni meccanismo tuttavia si basa su una chiave. Per impostazione predefinita, verrà utilizzato il tasto di funzione hello denominato "default". Se si desidera toouse una chiave diversa, occorre tooconfigure hello webhook toosend hello Nome chiave del provider con richiesta di hello in uno dei seguenti modi hello:

- **Stringa di query**: provider hello passa nome della chiave hello hello `clientid` parametro della stringa di query (ad esempio, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Intestazione della richiesta**: provider hello passa nome della chiave hello hello `x-functions-clientid` intestazione.

> [!NOTE]
> Le chiavi di funzione hanno la precedenza sulle chiavi host. Se due chiavi sono definite con stesso nome, hello hello funzione chiave verrà usata.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Esempi di trigger HTTP
Si supponga di avere seguito trigger HTTP hello hello `bindings` matrice function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Vedere l'esempio specifico del linguaggio hello che cerca un `name` parametro nella stringa di query hello o corpo hello della richiesta HTTP hello.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.JS](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Esempio di trigger HTTP in C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

È anche possibile associare tooa POCO anziché `HttpRequestMessage`. Questo sarà possibile Alluminosilicato dal corpo hello della richiesta di hello, analizzato come JSON. Analogamente, un tipo può essere passato a un output di risposta HTTP toohello associazione e verrà restituito come corpo della risposta hello, con un codice di 200 stato.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Esempio di trigger HTTP in F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

È necessario un `project.json` file che usa NuGet tooreference hello `FSharp.Interop.Dynamic` e `Dynamitey` assembly, simile al seguente:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Si utilizzeranno toofetch NuGet le dipendenze e farà riferimento a essi nello script.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Esempio di trigger HTTP in Node.JS
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Esempi di webhook
Si supponga di avere seguito trigger webhook hello hello `bindings` matrice function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Vedere l'esempio specifico del linguaggio hello che registra i commenti problema GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Esempio di webhook in C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Esempio di webhook in F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Esempio di webhook in Node.JS
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

