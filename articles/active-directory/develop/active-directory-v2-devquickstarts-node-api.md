---
title: aaaSecure un'API web v 2.0 di Azure Active Directory con Node.js | Documenti Microsoft
description: Informazioni su come toobuild un Node.js web API che accetta i token da un account Microsoft personale e dagli account aziendale o dell'istituto di istruzione.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Proteggere un'API Web usando node.js
> [!NOTE]
> Non tutti gli scenari di Azure Active Directory e le funzionalità di lavoro con endpoint v 2.0 hello. toodetermine se è necessario utilizzare hello v 2.0 endpoint o hello v 1.0, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

Quando si utilizza l'endpoint di hello Azure Active Directory (Azure AD) v 2.0, è possibile utilizzare [OAuth 2.0](active-directory-v2-protocols.md) token di accesso tooprotect l'API web. Con i token di accesso OAuth 2.0, gli utenti che dispongono sia di un account Microsoft personale che di un account aziendale o dell'istituto di istruzione possono accedere in modo sicuro all'API Web.

*Passport* è il middleware di autenticazione per Node.js. Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify. In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni. È stata sviluppata una strategia per Azure AD. In questo articolo è illustrato come tooinstall hello modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.

## <a name="download"></a>Scaricare
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs). esercitazione di hello toofollow, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), o scheletro hello clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

È anche possibile ottenere un'applicazione hello completata alla fine di hello di questa esercitazione.

## <a name="1-register-an-app"></a>1: Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire [questi passaggi dettagliati](active-directory-v2-app-registration.md) tooregister un'app. Assicurarsi di:

* Hello copia **Id applicazione** assegnato tooyour app. Per questa esercitazione occorre:
* Aggiungere hello **Mobile** piattaforma per l'app.
* Hello copia **URI di reindirizzamento** dal portale hello. È necessario utilizzare hello URI valore predefinito `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-install-nodejs"></a>2: Installare Node.js
esempio di hello toouse per questa esercitazione, è necessario [installare Node.js](http://nodejs.org).

## <a name="3-install-mongodb"></a>3: Installare MongoDB
toosuccessfully usare questo esempio, è necessario [installare MongoDB](http://www.mongodb.org). In questo esempio, si utilizza MongoDB toomake l'API REST persistente tra istanze di server.

> [!NOTE]
> In questo articolo si presuppone che si utilizzino gli endpoint di installazione e il server predefinito hello per MongoDB: mongodb://localhost.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: installazione hello restify moduli in web API
Utilizziamo Resitfy toobuild API REST. Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express, Restify dispone di un set affidabile di funzionalità che è possibile usare le API REST su Connect toobuild.

### <a name="install-restify"></a>Installare Restify
1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

    Se hello **azuread** directory non esiste, crearla:

    `mkdir azuread`

2.  Installare Restify:

    `npm install restify`

    output di Hello di questo comando dovrebbe essere simile al seguente:

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>È stato visualizzato un errore?
In alcuni sistemi operativi, quando si utilizza hello `npm` comando, è possibile che questo messaggio: `Error: EPERM, chmod '/usr/local/bin/..'`. Errore Hello è seguito da una richiesta che si tenta di account hello in esecuzione come amministratore. In questo caso, utilizzare il comando hello `sudo` toorun `npm` a un livello di privilegio superiore.

#### <a name="did-you-get-an-error-related-toodtrace"></a>È stato si verifica un errore correlato tooDTrace?
Quando si installa Restify, è possibile che venga visualizzato questo messaggio:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify ha tootrace un meccanismo avanzato tramite /DTRACE le chiamate REST. Tuttavia, in molti sistemi operativi DTrace non è disponibile. È possibile ignorare questo messaggio di errore.


## <a name="5-install-passportjs-in-your-web-api"></a>5: Installare Passport.js nell'API Web
1.  Al prompt dei comandi di hello, modificare la directory hello troppo**azuread**.

2.  Installare Passport.js:

    `npm install passport`

    output di Hello del comando hello dovrebbe essere simile al seguente:

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: aggiungere le API web tooyour passport-azure Active Directory
Successivamente, aggiungere strategia OAuth hello, utilizzando passport azuread. `passport-azuread` è una suite di strategie che connettono Azure AD a Passport. In questo esempio di API REST tale strategia viene usata per i token di connessione.

> [!NOTE]
> Anche se OAuth 2.0 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, sono comunemente usati alcuni tipi di token. I token di connessione sono endpoint tooprotect comunemente utilizzati. I token di connessione sono tipo hello maggiormente emesso del token OAuth 2.0. Molte implementazioni di OAuth 2.0 si presuppongono che i token di connessione sono hello unico tipo di token rilasciato.
> 
> 

1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**.

    `cd azuread`

2.  Installare hello Passport.js `passport-azure-ad` modulo:

    `npm install passport-azure-ad`

    output di Hello del comando hello dovrebbe essere simile al seguente:

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: aggiungere MongoDB moduli tooyour web API
Questo esempio usa MongoDB come archivio dati. 

1.  Installare Mongoose, ampiamente usati plug-in, i modelli di toomanage e gli schemi: 

    `npm install mongoose`

2.  Installare i driver di database hello per MongoDB, denominato anche MongoDB:

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8. Installare moduli aggiuntivi
Installare hello rimanenti moduli necessari.

1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  Immettere i seguenti comandi hello. i comandi di Hello installano hello moduli nella cartella node_modules di seguito:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9: Creare un file Server.js per le dipendenze
Un file Server.js contiene la maggior parte hello funzionalità hello del server web API. Aggiungere la maggior parte dei file toothis del codice. Ai fini della produzione, è possibile effettuare il refactoring funzionalità hello in file più piccoli, come per i controller e route distinte. Questo articolo usa Server.js a questo scopo.

1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  Usando un editor di propria scelta, creare un file Server.js. Aggiungere i seguenti file di informazioni toohello hello:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Salvare il file hello. Si tornerà tooit a breve.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: creare un toostore di file di configurazione delle impostazioni di Azure AD
Questo file di codice passa i parametri di configurazione hello dal tooPassport.js del portale di Azure AD. Portale di hello web API toohello è stato aggiunto all'inizio di hello dell'articolo hello creato questi valori di configurazione. Dopo aver copiato il codice hello, spiega quali tooput in valori hello di questi parametri.

1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  In un editor creare un file Config.js. Aggiungere hello le seguenti informazioni:

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>Valori richiesti

*   **IdentityMetadata**: questa opzione è quando `passport-azure-ad` cerca i dati di configurazione per il provider di identità hello (IDP) e hello chiavi toovalidate hello token Web JSON (Jwt). Se si utilizza Azure AD, è inoltre possibile nascondere toochange questo.

*   **gruppo di destinatari**: l'URI di reindirizzamento dal portale hello.

> [!NOTE]
> Le chiavi vengono registrate con una certa frequenza. Assicurarsi che sempre possibile mettere dall'URL "openid_keys" hello, e tale applicazione hello può accedere hello Internet.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: aggiungere hello configurazione tooyour Server.js file
L'applicazione richiede valori hello tooread dal file di configurazione hello che appena creato. Aggiungere i file con estensione config hello come una risorsa necessaria nell'applicazione. Impostare toothose variabili globali hello in Config.js.

1.  Al prompt dei comandi di hello, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  In un editor aprire Server.js. Aggiungere hello le seguenti informazioni:

    ```Javascript
    var config = require('./config');
    ```

3.  Aggiungere un nuovo tooServer.js sezione:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: aggiungere informazioni di modello e lo schema di MongoDB hello utilizzando Mongoose
Successivamente, connettere questi tre file in un servizio API REST.

In questo articolo, si usa MongoDB toostore l'attività. Questa operazione viene illustrata nel *passaggio 4*.

Nel file Config.js hello creato nel passaggio 11, il database è denominato *tasklist*. Che è stato inserito alla fine di hello dell'URL di connessione mongoose_auth_local. Non è necessario toocreate questo database in anticipo in MongoDB. Hello database viene creato in hello prima esecuzione dell'applicazione server (supponendo hello database non esiste già).

Si è indicato server hello quali toouse database MongoDB. Successivamente, è necessario toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.

### <a name="hello-model"></a>modello Hello
modello di schema Hello è molto semplice. Se necessario, è possibile espanderlo. 

modello di schema Hello presenta questi valori:

*   **NAME**. attività di Hello persona toohello assegnato. Valore **stringa**.
*   **TASK**. nome di Hello dell'attività hello. Valore **stringa**.
*   **DATE**. Data di Hello tale attività hello è scadenza. Valore **datetime**.
*   **COMPLETED**. Se viene completata l'attività hello. Valore **booleano**.

### <a name="create-hello-schema-in-hello-code"></a>Creare uno schema di hello codice hello
1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  Nell'editor aprire Server.js. Sotto la voce di configurazione hello aggiungere hello le seguenti informazioni:

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

Questo codice si connette toohello MongoDB server. Restituisce inoltre un oggetto schema.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>Usa schema hello, creare il modello nel codice hello
Di sotto di hello codice precedente, aggiungere hello seguente codice:

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

Come si può vedere dal codice hello, prima creare uno schema. Si crea quindi un oggetto modello. Utilizzare hello modello oggetto toostore i dati in tutto hello codice quando si definisce il **route**.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13: Aggiungere le route per il server API REST delle attività
Dopo aver creato un toowork del modello di database con, aggiungere le route hello da usare per il server API REST.

### <a name="about-routes-in-restify"></a>Informazioni sulle route in Restify
Route nella restify lavoro esattamente hello esattamente come quando si utilizza hello stack Express. Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello. Le route si definiscono di solito in un file separato. In questa esercitazione, le route sono inserite in Server.js. È consigliabile fattorizzarle nel relativo file per usarle in fase di produzione.

Un modello tipico per una route Restify è:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Si tratta hello modello al livello più elementare di hello. Restify (ed Express) fornisce funzionalità molto più approfondita, ad esempio i tipi di applicazione hello possibilità toodefine e routing complessa in diversi endpoint.

#### <a name="add-default-routes-tooyour-server"></a>Aggiungere server tooyour di route predefinita
Aggiungere le route CRUD di base hello: **creare**, **recuperare**, **aggiornare**, e **eliminare**.

1.  Al prompt dei comandi, modificare la directory hello troppo**azuread**:

    `cd azuread`

2.  In un editor aprire Server.js. Di seguito hello voci del database eseguite in precedenza, aggiungere hello le seguenti informazioni:

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a>Aggiungere la gestione di route hello
Aggiungere alcuni errori affinché si possa comunicare client toohello indietro problema hello che si è verificato.

Aggiungere hello seguente di codice riportato di seguito codice hello, che è già scritto:

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a>14: Creare il server
ultima operazione toodo Hello è tooadd l'istanza del server. istanza del server Hello gestisce le chiamate.

Restify ed Express hanno un elevato livello di personalizzazione che è possibile usare con un server API REST. In questa esercitazione, si usa il programma di installazione di base hello.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: aggiungere le route hello (senza autenticazione, per ora)
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a>16: eseguire hello server
È una buona idea tootest il server prima di aggiungere l'autenticazione.

tootest modo più semplice Hello del server è tramite curl un prompt dei comandi. toodo, è necessario una semplice utilità che è possibile utilizzare tooparse output in formato JSON. 

1.  Installare utilità JSON hello usata in hello seguono esempi:

    `$npm install -g jsontool`

    Vengono installati lo strumento JSON hello a livello globale.

2.  Assicurarsi che l'istanza di MongoDB sia in esecuzione.

    `$sudo mongod`

3.  Modificare anche le directory hello**azuread**, quindi eseguire curl:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  tooadd un'attività:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    risposta Hello deve essere:

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  Elenco delle attività Brandon:

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Se tutti questi comandi vengono eseguiti senza errori, si è pronti tooadd OAuth toohello server dell'API REST.

*Ora si dispone di un server API REST con MongoDB*.

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: Aggiungi server di autenticazione tooyour API REST
Dopo aver creato un'API REST in esecuzione, configurarlo toouse con Azure AD.

Al prompt dei comandi, modificare la directory hello troppo**azuread**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>Utilizzare oidcbearerstrategy hello che è incluso con passport-azure Active Directory
Nei passaggi precedenti è stato creato un tipico server REST TODO senza alcun tipo di autenticazione. Aggiungere l'autenticazione.

Innanzitutto, consente di indicare che si desidera toouse Passport. Inserire il codice subito dopo la configurazione del server precedente:

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> Quando si scrivono le API, è hello di collegamento tooalways una buona idea toosomething dati univoco da token hello hello utente non può effettuare lo spoofing. Quando il server archivia elementi TODO, li archivia in base all'ID di sottoscrizione utente hello nel token hello (chiamati tramite token.sub). Nel campo "proprietario" hello, inserire token.sub hello. In questo modo si garantisce che solo tale utente può accedere TODOs hello utente. Nessun utente può accedere TODOs hello che sono state immesse. È non presenti rischi in hello API per il "proprietario". Un utente esterno può richiedere gli elementi TODO di altri utenti, anche se sono autenticati.
> 
> 

Successivamente, utilizzare strategia Open ID connessione connessione hello fornita con `passport-azure-ad`. Inserire il codice seguente dopo quanto inserito in precedenza:

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via). Tutti i writer strategia rispettare toohello modello. Passare la strategia di hello un `function()` che utilizza un token e `done` come parametri. strategia di Hello viene restituito dopo esegue automaticamente tutte le relative operazioni. Archivio utente hello e token hello stash pertanto non è necessario tooask per tale nuovamente.

> [!IMPORTANT]
> Hello precedente il codice in tutti gli utenti possono eseguire l'autenticazione server tooyour. Questa operazione è nota come registrazione automatica. In un server di produzione, è preferibile toolet chiunque senza prima li passare attraverso un processo di registrazione desiderato. Si tratta in genere hello modello di App consumer. app Hello potrebbero consentire di tooregister con Facebook, ma viene chiesto di tooenter ulteriori informazioni. Se non è stato utilizzato un programma della riga di comando per questa esercitazione, è stato possibile estrarre posta elettronica hello dall'oggetto hello token restituito. Quindi, è possibile chiedere informazioni aggiuntive di hello utente tooenter. Poiché si tratta di un server di prova, aggiungere l'utente hello toohello direttamente i database di in memoria.
> 
> 

### <a name="protect-endpoints"></a>Proteggere gli endpoint
Proteggere gli endpoint specificando hello **passport.authenticate()** chiamata con protocollo hello che si desidera toouse.

È possibile modificare la route nel codice del server per un'opzione più avanzata:

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18: Eseguire nuovamente l'applicazione server
Usare curl nuovamente toosee se si dispone di OAuth 2.0 protezione contro gli endpoint. Eseguire questa operazione prima di usare uno qualsiasi degli SDK client in questo endpoint. intestazioni Hello restituite dovrebbero essere se l'autenticazione funzioni correttamente.

1.  Assicurarsi che l'istanza di MongoDB sia in esecuzione:

    `$sudo mongod`

2.  Modificare toohello **azuread** directory, quindi usare curl:

    `$ cd azuread`

    `$ node server.js`

3.  Provare un'operazione POST di base:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Una risposta 401 indica il livello di Passport hello tenta tooredirect toohello autorizza un endpoint, che è esattamente quello desiderato.

*Ora è disponibile un servizio API REST che usa OAuth 2.0*.

Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth 2.0. A tale scopo, sarà necessario tooreview un'esercitazione aggiuntiva.

## <a name="next-steps"></a>Passaggi successivi
Per riferimento, l'esempio hello completata (senza i valori di configurazione) viene fornito come [un file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip). È anche possibile clonarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

A questo punto, è possibile passare argomenti avanzati toomore. Potrebbe essere necessario tootry [proteggere un'app web Node. js utilizzando hello v 2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).

Altre risorse:

* [Guida per sviluppatori Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "azure-active-directory"](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Che incoraggia la collaborazione toosign backup toobe notificate quando si verificano eventi di sicurezza. In hello [notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) pagina, la sottoscrizione di avvisi advisory tooSecurity.

