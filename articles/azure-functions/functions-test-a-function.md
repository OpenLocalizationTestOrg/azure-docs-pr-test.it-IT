---
title: Funzioni di Azure aaaTesting | Documenti Microsoft
description: Testare Funzioni di Azure con Postman, cURL e Node.js.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server, test
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Strategie per il test del codice in Funzioni di Azure

In questo argomento viene illustrato hello si avvicina a diverse funzioni tootest modi, incluso l'utilizzo di hello seguente generale:

+ Strumenti basati su HTTP, ad esempio cURL, Postman e persino un browser Web per i trigger basati sul Web
+ Azure Storage Explorer, i trigger di archiviazione di Azure basato su tootest
+ Scheda test nel portale di Azure funzioni hello
+ Funzione attivata tramite timer
+ Test dell'applicazione o del framework

Tutti questi metodi di test utilizzare una funzione di attivazione HTTP che accetta l'input tramite una query stringa parametro o hello corpo della richiesta. Creare questa funzione nella prima sezione hello.

## <a name="create-a-function-for-testing"></a>Creare una funzione per i test
Per la maggior parte di questa esercitazione, si utilizza una versione leggermente modificata del modello di funzione HttpTrigger JavaScript è disponibile quando si crea una funzione hello. Se occorre assistenza nella creazione di una funzione, rivedere questa [esercitazione](functions-create-first-azure-function.md). Scegliere hello **HttpTrigger - JavaScript** modello quando si crea la funzione di test hello in hello [portale di Azure].

Hello funzione modello predefinito è fondamentalmente una funzione di "hello world" che restituisce il nome di hello indietro dalla richiesta query o corpo stringa parametro hello, `name=<your name>`.  Verrà aggiornata codice hello tooalso consentono tooprovide hello nome e un indirizzo come contenuto JSON nel corpo della richiesta hello. Funzione hello restituisce quindi questi client toohello indietro quando disponibile.   

Aggiornare la funzione hello hello seguente di codice, che verrà utilizzato per il test:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Eseguire il test di una funzione con gli strumenti
All'esterno di hello portale di Azure, sono disponibili diversi strumenti che è possibile utilizzare tootrigger delle funzioni per i test. Questi includono gli strumenti di test HTTP (sia basati su interfaccia utente sia sulla riga di comando), strumenti di accesso all'Archiviazione di Azure e un semplice browser Web.

### <a name="test-with-a-browser"></a>Eseguire il test con un browser
browser web Hello è funzioni di tootrigger un modo semplice tramite HTTP. È possibile usare un browser per le richieste GET per cui non è necessario un payload del corpo e che usi solo i parametri di stringa della query.

funzione hello tootest definita in precedenza, hello copia **funzione Url** dal portale hello. Dispone di hello seguente formato:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Aggiungere hello `name` stringa di query toohello del parametro. Utilizzare un nome effettivo per hello `<Enter a name here>` segnaposto.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Incolla hello URL nel browser ed è necessario ottenere toohello seguito risposta simile.

![Schermata della scheda del browser Chrome con risposta del test](./media/functions-test-a-function/browser-test.png)

Questo esempio è browser Chrome hello, che esegue il wrapping hello ha restituito una stringa in formato XML. Altri browser di visualizzare solo il valore di stringa hello.

Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Eseguire il test con Postman
Hello consigliato strumento tootest la maggior parte delle funzioni è Postman, che si integra con browser Chrome hello. tooinstall Postman, vedere [Postman ottenere](https://www.getpostman.com/). Postman consente di controllare molti più attributi di una richiesta HTTP.

> [!TIP]
> Utilizzare hello HTTP strumento di test che si ha maggiore familiarità con. Ecco alcuni tooPostman alternative:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

funzione di hello tootest con un corpo della richiesta in Postman:

1. Avviare Postman da hello **app** pulsante nell'angolo superiore sinistro hello di una finestra del browser Chrome.
2. Copiare l'**URL funzione** e incollarlo in Postman. Include un parametro di stringa di query di codice di accesso hello.
3. Modificare anche il metodo HTTP hello**POST**.
4. Fare clic su **corpo** > **raw**e aggiungere un JSON richiesta seguente toohello simile corpo:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Fare clic su **Send**.

Hello immagine seguente mostra test hello echo semplice funzione esempio in questa esercitazione.

![Schermata dell'interfaccia utente di Postman](./media/functions-test-a-function/postman-test.png)

Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Eseguire il test con cURL dalla riga di comando hello
Spesso quando si esegue il test del software, non è necessario toolook qualsiasi superiore rispetto a quello hello riga di comando toohelp debug dell'applicazione. L'approccio è analogo per le funzioni. Si noti che cURL hello è disponibile per impostazione predefinita nei sistemi basati su Linux. In Windows, è innanzitutto necessario scaricare e installare hello [cURL strumento](https://curl.haxx.se/).

funzione hello tootest che è stato definito in precedenza, hello copia **funzione URL** dal portale hello. Dispone di hello seguente formato:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Questo è l'URL di hello per l'attivazione di una funzione. Test tramite comando cURL hello in hello toomake di riga di comando, un'operazione GET (`-G` o `--get`) richiesta per la funzione hello:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Questo particolare esempio richiede un parametro di stringa di query, può essere passato come dati (`-d`) in hello cURL comando:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Comando di esecuzione hello e visualizzato dopo l'output della funzione hello nella riga di comando hello hello:

![Schermata dell'output del prompt dei comandi](./media/functions-test-a-function/curl-test.png)

Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Eseguire il test di un trigger del BLOB con Storage Explorer
È possibile testare una funzione trigger del BLOB con [Esplora archivi di Azure](http://storageexplorer.com/).

1. In hello [portale di Azure] per l'app di funzione, creare una funzione di attivazione di un blob di c#, F # o JavaScript. Impostare hello toomonitor toohello percorso del contenitore blob. ad esempio:

        files
2. Fare clic su hello  **+**  pulsante tooselect o creare account di archiviazione hello da toouse. Fare quindi clic su **Crea**.
3. Creare un file di testo con hello segue testo e salvarlo:

        A text file for blob trigger function testing.
4. Eseguire [Azure Storage Explorer](http://storageexplorer.com/)e connettere toohello contenitore di blob nell'account di archiviazione hello monitorato.
5. Fare clic su **caricare** file di testo hello tooupload.

    ![Screenshot di Esplora archivi](./media/functions-test-a-function/azure-storage-explorer-test.png)

codice di funzione trigger blob predefinito Hello segnala l'elaborazione di hello del blob hello nei registri hello:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Eseguire il test di una funzione all'interno di Funzioni
Hello Azure funzioni portale è progettato toolet testi HTTP e timer attivato funzioni. È anche possibile creare funzioni tootrigger altre funzioni che si siano testando.

### <a name="test-with-hello-functions-portal-run-button"></a>Eseguire il test con il pulsante Esegui portale di hello funzioni
portale Hello fornisce un **eseguire** pulsante che è possibile utilizzare alcune toodo limitato di test. È possibile fornire un corpo della richiesta utilizzando il pulsante di hello, ma non è possibile specificare i parametri di stringa di query o aggiornare le intestazioni di richiesta.

Testare hello HTTP trigger funzione creata in precedenza tramite l'aggiunta di un toohello simile stringa JSON seguente hello **corpo della richiesta** campo. Quindi fare clic su hello **eseguire** pulsante.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Eseguire il test con un trigger del timer
Non è possibile testare alcune funzioni in modo adeguato con gli strumenti di hello indicati in precedenza. Prendiamo ad esempio una funzione trigger della coda eseguita quando un messaggio viene inserito in [Archiviazione code di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md). È sempre possibile scrivere codice toodrop un messaggio in coda e viene fornito un esempio in un progetto console più avanti in questo articolo. Esiste tuttavia un altro approccio che può essere usato per eseguire direttamente il test delle funzioni.  

È possibile usare un trigger del timer configurato con un'associazione di output della coda. Il codice del trigger timer è quindi possibile scrivere coda toohello i messaggi di prova hello. In questa sezione ne viene presentato un esempio.

Per informazioni più dettagliate sull'uso di associazioni con le funzioni di Azure, vedere hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Creare trigger della coda per il test
toodemonstrate questo approccio, è necessario creare una funzione di trigger di coda da tootest per una coda denominata `queue-newusers`. Questa funzione elabora le informazioni relative a nome e indirizzo per un nuovo utente inserito nell'archiviazione code di Azure.

> [!NOTE]
> Se si utilizza un nome diverso, verificare che nome hello è utilizzare conforme toohello [denominazione di code e metadati](https://msdn.microsoft.com/library/dd179349.aspx) regole. In caso contrario, viene visualizzato un errore.
>
>

1. In hello [portale di Azure] per l'app di funzione, fare clic su **nuova funzione** > **QueueTrigger - c#**.
2. Immettere toobe nome di coda hello monitorato dalla funzione coda hello:

        queue-newusers
3. Fare clic su hello  **+**  pulsante tooselect o creare account di archiviazione hello da toouse. Fare quindi clic su **Crea**.
4. Lasciare la finestra del browser del portale, è possibile monitorare le voci di log hello codice hello predefinito coda funzione modello.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Creare un toodrop trigger timer, un messaggio nella coda di hello
1. Aprire hello [portale di Azure] in una nuova finestra del browser e passare tooyour funzione app.
2. Fare clic su **Nuova funzione** > **TimerTrigger - C#**. Immettere un tooset espressione cron frequenza hello codice timer verifica la funzione di coda. Fare quindi clic su **Crea**. Se si desidera hello test toorun ogni 30 secondi, è possibile utilizzare la seguente hello [espressione CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Fare clic su hello **integrazione** scheda per il nuovo trigger timer.
4. In **Output** fare clic sul pulsante **+ Nuovo output**. Fare clic su **coda** e quindi su **Seleziona**.
5. Nome di hello nota da usare per hello **oggetto messaggio della coda**. Utilizzare questo codice della funzione hello timer.

        myQueue
6. Immettere il nome di coda hello in cui viene inviato il messaggio hello:

        queue-newusers
7. Fare clic su hello  **+**  pulsante account di archiviazione tooselect hello è usata in precedenza con trigger coda hello. Fare quindi clic su **Salva**.
8. Fare clic su hello **sviluppare** scheda per il trigger timer.
9. È possibile utilizzare hello seguente codice per la funzione di timer hello in c#, purché hello stessa coda nome oggetto del messaggio illustrata in precedenza è stato utilizzato. Fare quindi clic su **Salva**.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

Hello funzione timer c# a questo punto, viene eseguito ogni 30 secondi se è stata utilizzata nell'espressione cron di esempio hello. funzione timer hello nei registri Hello ogni esecuzione del report:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

Nella finestra del browser hello per la funzione di coda hello, è possibile visualizzare ogni messaggio in fase di elaborazione:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Eseguire il test di una funzione con il codice
Potrebbe essere necessario toocreate un tootest applicazioni o framework esterno delle funzioni.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Eseguire il test di una funzione trigger HTTP con il codice Node.js
Utilizzare la funzione un tooexecute app Node.js un tootest di richiesta HTTP.
Verificare che tooset:

* Hello `host` nell'host di hello richiesta opzioni tooyour funzione app.
* Il nome di funzione in hello `path`.
* Il codice di accesso (`<your code>`) in hello `path`.

Esempio di codice:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Output:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Testare una funzione trigger della coda con codice C# #
Indicato in precedenza che è possibile testare un trigger di coda tramite codice toodrop un messaggio nella coda di lavoro. Hello seguente codice di esempio è basato su codice hello c# presentati in hello [Introduzione all'archiviazione di Accodamento Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) esercitazione. Da questo collegamento è disponibile il codice anche per altri linguaggi.

tootest questo codice in un'applicazione console, è necessario:

* [Configurare la stringa di connessione di archiviazione nel file app. config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Passare un `name` e `address` come parametri toohello app. ad esempio `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Questo codice accetta hello nome e l'indirizzo per un nuovo utente come argomenti della riga di comando in fase di esecuzione.)

Codice C# di esempio:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

Nella finestra del browser hello per la funzione di coda hello, è possibile visualizzare ogni messaggio in fase di elaborazione:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portale di Azure]: https://portal.azure.com
