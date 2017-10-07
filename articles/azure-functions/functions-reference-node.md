---
title: riferimenti per sviluppatori aaaJavaScript per le funzioni di Azure | Documenti Microsoft
description: Comprendere il funzionamento toodevelop utilizzando JavaScript.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a>Guida per gli sviluppatori JavaScript di Funzioni di Azure
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Hello JavaScript esperienza per le funzioni di Azure rende facile tooexport una funzione, che viene passata come un `context` oggetto per la comunicazione con il runtime hello e per la ricezione e invio di dati tramite i binding.

Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).

## <a name="exporting-a-function"></a>Esportazione di una funzione
Tutte le funzioni JavaScript necessario esportare un singolo `function` tramite `module.exports` per hello runtime toofind hello funzione ed eseguirlo. Questa funzione deve sempre includere un oggetto `context` .

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

Associazioni di `direction === "in"` vengono passate come argomenti della funzione, il che significa che è possibile utilizzare [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically gestire nuovi input (ad esempio, tramite `arguments.length` tooiterate su tutti gli input). Questa funzionalità è utile se si ha solo un trigger e nessun input aggiuntivo, in quanto consente di accedere ai dati del trigger in modo prevedibile senza fare riferimento all'oggetto `context`.

gli argomenti di Hello vengono sempre passati funzione toohello in ordine di hello in cui si trovano in *function.json*, anche se non si specifica li nell'istruzione esportazioni. Ad esempio, se dispone di `function(context, a, b)` e modificarlo troppo`function(context, a)`, è comunque possibile ottenere il valore di hello di `b` nel codice della funzione riferendosi troppo`arguments[3]`.

Tutte le associazioni, indipendentemente dalla direzione, vengono inoltre passate in hello `context` (vedere lo script seguente hello) dell'oggetto. 

## <a name="context-object"></a>Oggetto context
Hello runtime usa un `context` oggetto toopass dati tooand della propria funzione e toolet per comunicare con il runtime di hello.

è sempre funzione tooa hello del primo parametro Hello oggetto di contesto e deve essere incluso perché contiene i metodi, ad esempio `context.done` e `context.log`, che sono necessari toouse hello runtime correttamente. È possibile assegnare un nome oggetto hello qualsiasi desiderato (ad esempio, `ctx` o `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Proprietà context.bindings

```
context.bindings
```
Restituisce un oggetto denominato che contiene tutti i dati di input e output. Ad esempio, hello seguente definizione di associazione nel *function.json* permette di accedere a hello contenuto della coda di hello da hello `context.bindings.myInput` oggetto. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>Metodo context.done
```
context.done([err],[propertyBag])
```

Informa il runtime hello che il codice è stata completata. È necessario chiamare `context.done`, o else hello runtime non sa mai che la funzione è stata completata e il timeout di esecuzione hello. 

Hello `context.done` metodo consente toopass eseguire sia un runtime toohello di errore definiti dall'utente e un elenco di proprietà della proprietà che sovrascrivono proprietà hello hello `context.bindings` oggetto.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Metodo context.log  

```
context.log(message)
```
Consente di toowrite toohello console i log di streaming a livello di traccia predefinito hello. In `context.log`, altri metodi di registrazione sono disponibili che consentono di scrivere log console toohello ad altri livelli di traccia:


| Metodo                 | Descrizione                                |
| ---------------------- | ------------------------------------------ |
| **error(_messaggio_)**   | Scrive tooerror livello di registrazione o inferiore.   |
| **warn(_messaggio_)**    | Scrive toowarning livello di registrazione o inferiore. |
| **info(_messaggio_)**    | Scrive tooinfo livello di registrazione o inferiore.    |
| **verbose(_messaggio_)** | Scrive la registrazione a livello tooverbose.           |

Hello nell'esempio seguente vengono toohello console a livello di traccia di avviso hello:

```javascript
context.log.warn("Something has happened."); 
```
È possibile impostare hello soglia di livello di traccia per la registrazione nel file host.json hello o disattivarla.  Per ulteriori informazioni sulla modalità di registrazione toowrite toohello, vedere la sezione successiva di hello.

## <a name="binding-data-type"></a>Associazione del tipo di dati

toodefine tipo di dati hello per un'associazione di input, utilizzare hello `dataType` proprietà nella definizione di associazioni hello. Ad esempio, tooread hello contenuto di una richiesta HTTP in formato binario, utilizzare il tipo di hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Altre opzioni per `dataType` sono `stream` e `string`.

## <a name="writing-trace-output-toohello-console"></a>Console toohello output di traccia scrittura 

Nelle funzioni, utilizzare hello `context.log` console toohello di metodi toowrite traccia output. A questo punto, è possibile utilizzare `console.log` toowrite toohello console.

Quando si chiama `context.log()`, il messaggio viene scritto toohello console a livello di traccia predefinito hello, ovvero hello _info_ livello di traccia. Hello codice seguente viene scritto toohello console a livello di traccia info hello:

```javascript
context.log({hello: 'world'});  
```

Hello codice precedente è equivalente toohello seguente codice:

```javascript
context.log.info({hello: 'world'});  
```

Hello codice seguente viene scritto toohello console a livello di errore hello:

```javascript
context.log.error("An error has occurred.");  
```

Poiché _errore_ hello traccia di più alto livello, la traccia viene scritto output toohello a tutti i livelli di traccia, purché la registrazione è abilitata.  


Tutti `context.log` metodi supportano hello stesso formato del parametro che è supportato da Node.js hello [util.format metodo](https://nodejs.org/api/util.html#util_util_format_format). Prendere in considerazione hello seguente di codice, che scrive toohello console usando il livello di traccia predefinito hello:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

È inoltre possibile hello scrittura stesso codice in hello seguente formato:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Configurare il livello di traccia hello per registrazione nella console

Funzioni consente di definire il livello di traccia hello soglia per la scrittura di console toohello, che rende facile toocontrol hello le tracce vengono scritte toohello console da funzioni. soglia di hello tooset per tutte le tracce scritto toohello console, utilizzare hello `tracing.consoleLevel` proprietà nel file host.json hello. Questa impostazione si applica a funzioni tooall nell'app (funzione). Hello esempio seguente imposta hello traccia soglia tooenable la registrazione dettagliata:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

I valori di **consoleLevel** corrispondono toohello nomi di hello `context.log` metodi. impostare traccia tutte le console toohello, registrazione toodisable **consoleLevel** too_off_. Per ulteriori informazioni sul file host.json hello, vedere hello [argomento di riferimento host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>Trigger e associazioni HTTP

E trigger webhook HTTP e output associazioni utilizzano richiesta e risposta oggetti toorepresent hello HTTP messaggistica.  

### <a name="request-object"></a>Oggetto della richiesta

Hello `request` oggetto ha hello le proprietà seguenti:

| Proprietà      | Descrizione                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Oggetto che contiene hello corpo della richiesta di hello.               |
| _headers_     | Oggetto che contiene le intestazioni di richiesta di hello.                   |
| _method_      | metodo HTTP della richiesta di hello Hello.                                |
| _originalUrl_ | Hello l'URL della richiesta di hello.                                        |
| _params_      | Oggetto che contiene i parametri di routing della richiesta di hello hello. |
| _query_       | Oggetto che contiene i parametri di query hello.                  |
| _rawBody_     | corpo Hello del messaggio sotto forma di stringa.                           |


### <a name="response-object"></a>Oggetto della risposta

Hello `response` oggetto ha hello le proprietà seguenti:

| Proprietà  | Descrizione                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Oggetto che contiene hello corpo della risposta hello.         |
| _headers_ | Oggetto che contiene le intestazioni di risposta hello.             |
| _isRaw_   | Indica che la formattazione è ignorata per la risposta hello.    |
| _Stato_  | codice di stato HTTP della risposta hello Hello.                     |

### <a name="accessing-hello-request-and-response"></a>L'accesso a hello richiesta e risposta 

Quando si lavora con i trigger HTTP, è possibile accedere a oggetti hello HTTP richiesta e risposta in uno dei tre modi:

+ Dal hello denominato input e output di associazioni. In questo modo, i trigger HTTP hello e associazioni lavoro hello stesso come qualsiasi altra associazione. Hello esempio seguente imposta hello risposta oggetto utilizzando un oggetto denominato `response` associazione: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ Da `req` e `res` proprietà hello `context` oggetto. In questo modo, è possibile utilizzare hello modello convenzionale tooaccess HTTP dati oggetto di contesto hello, invece di dover hello toouse completo `context.bindings.name` modello. Hello seguente esempio viene illustrato come hello tooaccess `req` e `res` oggetti hello `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Oppure chiamando `context.done()`. Un tipo speciale di associazione HTTP restituisce risposta hello passato toohello `context.done()` metodo. output di Hello seguente HTTP associazione definisce un `$return` parametro di output:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    L'associazione di output è prevista è toosupply hello risposta quando si chiama `done()`, come segue:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Versione di Node e gestione dei pacchetti
versione del nodo Hello è attualmente bloccato `6.5.0`. Si sta analizzando la possibilità di aggiungere il supporto per altre versioni e renderle configurabili.

Hello alla procedura seguente consente di includere i pacchetti dell'app di funzione: 

1. Andare troppo`https://<function_app_name>.scm.azurewebsites.net`.

2. Fare clic su **Debug Console** > **CMD** (Console di debug > CMD).

3. Andare troppo`D:\home\site\wwwroot`, quindi trascinare il toohello file package. JSON **wwwroot** cartella nella metà superiore hello pagina hello.  
    Inoltre, è possibile caricare file tooyour funzione app in altri modi. Per ulteriori informazioni, vedere [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate). 

4. Dopo aver caricato il file di package. JSON hello, eseguire hello `npm install` comando hello **console l'esecuzione remota Kudu**.  
    Questa azione Scarica i pacchetti hello indicati nel file package. JSON hello e riavvia hello funzione app.

Dopo aver hello pacchetti necessari sono installati, importarli tooyour funzione chiamando `require('packagename')`, come illustrato nell'esempio seguente hello:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

È necessario definire un `package.json` file alla radice di hello dell'app in funzione. File di definizione hello consente tutte le funzioni nella condivisione di app hello hello stessi pacchetti memorizzati nella cache, che offre prestazioni migliori hello. Se si verifica un conflitto di versione, è possibile risolverlo aggiungendo un `package.json` file nella cartella hello di una funzione specifica.  

## <a name="environment-variables"></a>Variabili di ambiente
tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `process.env`, come illustrato nell'esempio di codice seguente hello:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>Considerazioni per le funzioni JavaScript

Quando si utilizzano le funzioni JavaScript, tenere presenti le considerazioni sulle hello hello nelle due sezioni che seguono.

### <a name="choose-single-core-app-service-plans"></a>Scegliere i piani di servizio app single core

Quando si crea un'app di funzione che usa hello piano di servizio App, si consiglia di selezionare un piano a core singolo anziché un piano con più core. Oggi, funzioni esegue le funzioni JavaScript in modo più efficiente nelle macchine virtuali a core singolo e utilizzando macchine virtuali di dimensioni maggiori non produce hello previsto miglioramento delle prestazioni. Se necessario, è possibile scalare orizzontalmente manualmente aggiungendo altre istanze di macchine virtuali single core oppure abilitare la scalabilità automatica. Per altre informazioni, vedere [Scalare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Supporto TypeScript e CoffeeScript
Poiché il supporto diretto non esiste ancora per la compilazione automatica TypeScript o CoffeeScript tramite il runtime di hello, questo tipo di supporto deve toobe gestite all'esterno di hello runtime, in fase di distribuzione. 

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

* [Procedure consigliate per Funzioni di Azure](functions-best-practices.md)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)
* [Guida di riferimento per gli sviluppatori C# di Funzioni di Azure](functions-reference-csharp.md)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#](functions-reference-fsharp.md)
* [Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md)

