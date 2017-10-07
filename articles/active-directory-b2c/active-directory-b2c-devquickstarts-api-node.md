---
title: 'Azure AD B2C: proteggere un''API Web usando Node.js | Microsoft Docs'
description: Come toobuild un Node.js web API che accetta i token da un tenant B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: proteggere un'API Web usando Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0. Questi token consentono le app client che usano Azure Active Directory B2C tooauthenticate toohello API. Questo articolo illustra come toocreate un'API "elenco" che consente agli utenti tooadd ed elenco attività. API web Hello sia protetta con Azure Active Directory B2C e consente solo agli utenti autenticati toomanage proprio elenco di attività da eseguire.

> [!NOTE]
> In questo esempio è stata scritta utilizzando tooby toobe connesso il nostro [iOS B2C applicazione di esempio](active-directory-b2c-devquickstarts-ios.md). Hello prima procedura dettagliata corrente e quindi proseguire con l'esempio in questione.
>
>

**Passport** è il middleware di autenticazione per Node.js. Estremamente flessibile e modulare, Passport può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify. Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora. È stata sviluppata una strategia per Azure Active Directory (Azure AD). Installare il modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.

toodo in questo esempio, è necessario:

1. Registrare un'applicazione con Azure AD.
2. Configurare l'applicazione toouse Passport `azure-ad-passport` plug-in.
3. Configurare un client applicazione toocall hello "elenco" API web.

## <a name="get-an-azure-ad-b2c-directory"></a>Ottenere una directory di Azure AD B2C
Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.  Una directory è un contenitore per utenti, app, gruppi e altro ancora.  Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.

## <a name="create-an-application"></a>Creare un'applicazione
Successivamente, è necessario toocreate un'app nella directory B2C che offre Azure AD alcune informazioni che toosecurely deve comunicare con l'app. In questo caso, le app client hello e API web sono rappresentati da un singolo **ID applicazione**, poiché comprendono una sola app logica. toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md). Assicurarsi di:

* Includere un **web app web e api** in un'applicazione hello
* Immettere `http://localhost/TodoListService` come **URL di risposta**. È l'URL predefinito hello per questo esempio di codice.
* Creare un **segreto applicazione** per l'applicazione e prenderne nota. Questi dati saranno necessari in un secondo momento. Si noti che questo valore deve toobe [XML sottoposto a escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) prima di utilizzarlo.
* Hello copia **ID applicazione** ovvero tooyour assegnato app. Questi dati saranno necessari in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri
In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questa app contiene due esperienze di identità: iscrizione e accesso. È necessario toocreate un criterio di ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Durante la creazione dei tre criteri assicurarsi di:

* Scegliere hello **nome visualizzato** e altri attributi per l'abbonamento nel criterio di iscrizione.
* Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio.  È consentito scegliere anche altre attestazioni.
* Copia verso il basso hello **nome** dei criteri dopo averlo creato. Devono contenere il prefisso hello `b2c_1_`.  I nomi dei criteri saranno necessari in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo aver creato i tre criteri, si è pronti toobuild l'app.

toolearn sul funzionamento dei criteri in Azure Active Directory B2C, iniziare con hello [.NET web app esercitazione introduttiva](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Scaricare codice hello
Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). esempio hello toobuild come si go, è possibile [scaricare un progetto di base come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). È anche possibile clonare scheletro hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

è anche l'applicazione Hello completato [disponibile come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) o hello `complete` ramo di hello stesso repository.

## <a name="download-nodejs-for-your-platform"></a>Scaricare node.js per la piattaforma corrente
toosuccessfully usare questo esempio, è necessario un'installazione funzionante di Node.js.

Installare Node.js da [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Installare MongoDB per la piattaforma corrente
toosuccessfully usare questo esempio, è necessario un'installazione funzionante di MongoDB. Utilizziamo MongoDB toomake l'API REST persistente tra istanze del server.

Installare MongoDB da [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Questa procedura dettagliata si presuppone che si gli endpoint di installazione e il server predefinito hello per MongoDB, ovvero al momento hello `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Installare i moduli Restify hello in web API
Utilizziamo Restify toobuild l'API REST. Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express, che include una gamma completa di funzionalità per la compilazione di API REST basate su Connect.

### <a name="install-restify"></a>Installare Restify
Dalla riga di comando hello, impostare la directory troppo`azuread`. Se hello `azuread` directory non esiste, crearla.

`cd azuread` oppure `mkdir azuread;`

Immettere hello comando seguente:

`npm install restify`

Questo comando installa Restify.

#### <a name="did-you-get-an-error"></a>È stato visualizzato un errore?
In alcuni sistemi operativi, quando si utilizza `npm`, è possibile che venga visualizzato l'errore hello `Error: EPERM, chmod '/usr/local/bin/..'` e una richiesta di account hello eseguire come amministratore. Se si verifica questo problema, utilizzare hello `sudo` toorun comando `npm` a un livello di privilegio superiore.

#### <a name="did-you-get-a-dtrace-error"></a>È stato visualizzato un errore di DTrace?
Durante l'installazione di Restify potrebbe essere visualizzato un testo simile al seguente:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

Restify offre un meccanismo efficace per tenere traccia delle chiamate REST usando DTrace. Tuttavia, per molti sistemi operativi DTrace non è disponibile. È possibile ignorare questi errori.

testo toothis simile viene visualizzato un output di Hello del comando hello:

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Installare Passport nell'API Web
Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente.

Installare Passport utilizzando hello comando seguente:

`npm install passport`

output di Hello del comando hello deve essere un testo simile toothis:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Aggiungere passport azuread tooyour web API
Successivamente, aggiungere strategia OAuth hello utilizzando `passport-azuread`, una suite di strategie che si connettono AD Azure con Passport. Usare questa strategia per i token di connessione di esempio di API REST hello.

> [!NOTE]
> Anche se OAuth2 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, solo determinati tipi di token sono usati su larga scala. i token di Hello per la protezione di endpoint sono token di connessione. Questi tipi di token sono hello maggiormente emesso in OAuth2. Molte implementazioni presuppongono che i token di connessione sono hello unico tipo di token rilasciato.
>
>

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente.

Installare hello Passport `passport-azure-ad` modulo tramite hello comando seguente:

`npm install passport-azure-ad`

output di Hello del comando hello deve essere un testo simile toothis:

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Aggiungere MongoDB moduli tooyour web API
Questo esempio usa MongoDB come archivio dati. A tale scopo installare Mongoose, un plug-in diffuso per la gestione di modelli e schemi.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Installare moduli aggiuntivi
Installare quindi hello rimanenti moduli necessari.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Installare i moduli hello il `node_modules` directory:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Creare un file server.js con le dipendenze
Hello `server.js` file fornisce la maggior parte hello funzionalità hello per il server Web API.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Creare un file `server.js` in un editor. Aggiungere hello le seguenti informazioni:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Salvare il file hello. Tornare tooit in un secondo momento.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Creare un toostore file config.js le impostazioni di Azure AD
Questo file di codice passa i parametri di configurazione hello da toohello il portale di Azure AD `Passport.js` file. Questi valori di configurazione è stato creato quando si aggiunta portale toohello API web di hello nella prima parte di hello di dimostrativo hello. Viene descritto il tooput in valori hello di questi parametri dopo aver copiato il codice hello.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Creare un file `config.js` in un editor. Aggiungere hello le seguenti informazioni:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Valori richiesti
`clientID`: hello ID client dell'applicazione Web API.

`IdentityMetadata`: Questa opzione è quando `passport-azure-ad` cerca i dati di configurazione per il provider di identità hello. Cerca anche hello chiavi toovalidate hello i token web JSON.

`audience`: hello identificatore uniform resource identifier (URI) dal portale hello che identifica l'applicazione chiamante.

`tenantName`: nome del tenant, ad esempio **contoso.onmicrosoft.com**.

`policyName`: hello criteri che si desidera token hello toovalidate entrano tooyour server. Questo criterio deve essere hello stesso criterio usato in un'applicazione hello client per l'accesso.

> [!NOTE]
> Per il momento, utilizzare hello stesso criteri attraverso il programma di installazione client e server. Se sono stati già completati una panoramica e creato questi criteri, non è necessario toodo così nuovamente. Poiché è stata completata la procedura dettagliata hello, occorre non deve tooset i nuovi criteri per procedure client nel sito di hello.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Aggiungere file di configurazione tooyour server.js
i valori hello tooread hello `config.js` file creata, aggiungere hello `.config` file come una risorsa necessaria nell'applicazione e quindi impostare toothose variabili globali hello in hello `config.js` documento.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Aprire hello `server.js` file in un editor. Aggiungere hello le seguenti informazioni:

```Javascript
var config = require('./config');
```
Aggiungere una nuova sezione troppo`server.js` che include hello seguente codice:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Successivamente, aggiungere alcuni segnaposto per gli utenti di hello riceviamo le applicazioni di chiamata.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Creare anche il logger.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Aggiungere le informazioni di modello e dello schema di MongoDB hello utilizzando Mongoose
Hello preparazione precedenti ripaga come connettere questi tre file in un servizio API REST.

Per questa procedura dettagliata, utilizzare MongoDB toostore le attività, come illustrato in precedenza.

In hello `config.js` file, è stato chiamato il database **tasklist**. Tale nome è stato anche gli elementi da inserire alla fine hello hello `mongoose_auth_local` URL di connessione. Non è necessario toocreate questo database in anticipo in MongoDB. Database di hello viene creato automaticamente alla prima esecuzione di hello dell'applicazione server.

Dopo che è indicare il server di hello quali toouse database MongoDB, è necessario toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.

### <a name="expand-hello-model"></a>Espandere il modello di hello
Questo modello di schema è semplice ed è possibile espanderlo in base alle esigenze.

`owner`: Assegnato toohello attività. Questo oggetto è di tipo **stringa**.  

`Text`: attività hello stessa. Questo oggetto è di tipo **stringa**.

`date`: data hello tale attività hello è scadenza. Questo oggetto è di tipo **datetime**.

`completed`: Se l'attività hello è stata completata. Questo oggetto è di tipo **booleano**.

### <a name="create-hello-schema-in-hello-code"></a>Creare uno schema di hello codice hello
Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Aprire hello `server.js` file in un editor. Aggiungere le seguenti informazioni di sotto la voce di configurazione hello hello:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Creare innanzitutto schema hello e quindi si crea un oggetto modello che si utilizza toostore i dati in tutto hello codice quando si definisce il **route**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Aggiungere le route per il server delle attività dell'API REST
Dopo aver creato un toowork del modello di database con, aggiungere le route hello che è utilizzata per il server API REST.

### <a name="about-routes-in-restify"></a>Informazioni sulle route in Restify
Le route funzionano in Restify in hello stesso modo in cui operano quando utilizzano stack Express hello. Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello.

Un modello tipico per una route Restify è:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

Restify ed Express offrono funzionalità molto più avanzate, ad esempio la definizione di tipi di applicazione e l'esecuzione di un routing complesso tra endpoint diversi. Ai fini di hello di questa esercitazione, è semplice queste route.

#### <a name="add-default-routes-tooyour-server"></a>Aggiungere server tooyour di route predefinita
È ora aggiungere route CRUD di base hello **creare** e **elenco** per API REST. Sono disponibili altre route in hello `complete` ramo dell'esempio hello.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

Aprire hello `server.js` file in un editor. Di sotto di voci di database hello apportate sopra aggiungere hello le seguenti informazioni:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a>Aggiungere la gestione di route hello
Aggiungere alcuni gestione degli errori in modo che è possibile comunicare eventuali problemi riscontrati toohello indietro client in modo che è in grado di utilizzare.

Aggiungere hello seguente codice:

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a>Creare il server
Dopo aver definito il database e inserito le route, ultima operazione di Hello per si toodo è tooadd hello server dell'istanza che gestisce le chiamate.

Restify ed Express forniscono personalizzazione completa per un server API REST, ma è utilizzare il programma di installazione di base hello qui.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Aggiungere hello route toohello server (senza autenticazione)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Aggiungi server di autenticazione tooyour API REST
A questo punto, il server API REST in esecuzione può essere usato in Azure AD.

Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Utilizzare hello OIDCBearerStrategy inclusa passport-azure Active Directory
> [!TIP]
> Quando si scrivono le API, è consigliabile collegare sempre toosomething dati hello univoco da token hello hello utente non può effettuare lo spoofing. Server hello Archivia elementi di attività, esegue quindi in base a hello **oid** dell'utente hello nel token hello (chiamati tramite token.oid), che passa nel campo proprietario"hello". Questo valore assicura che solo tale utente possa accedere i propri elementi ToDo. Non è non presenti rischi in hello API di "proprietario", un utente esterno può richiedere attività di altri utenti, anche se vengono autenticati.
>
>

Successivamente, utilizzare strategia connessione hello fornita con `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport utilizza hello stesso modello per tutte le relative strategie. Viene passato un oggetto `function()` con `token` e `done` come parametri. strategia di Hello torna tooyou dopo che ha eseguito tutte le operazioni. Archivio utente hello quindi salvare il token di hello in modo che non sia necessario tooask per tale nuovamente.

> [!IMPORTANT]
> codice Hello precedente accetta qualsiasi utente che si verifica tooauthenticate tooyour server. Questa operazione è nota come registrazione automatica. Nel server di produzione, non lasciare in qualsiasi API hello di accesso agli utenti senza prima li passare attraverso un processo di registrazione. Questo processo è in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere toofill informazioni aggiuntive. Se il programma non è un programma della riga di comando, è possibile estrarre posta elettronica hello dall'oggetto token hello è restituito e quindi richiesto toofill agli utenti informazioni aggiuntive. Poiché si tratta di un campione, aggiungerli database in memoria tooan.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Eseguire il tooverify applicazione server che rifiuta è
È possibile utilizzare `curl` toosee se si dispone ora OAuth2 protezione contro gli endpoint. Hello intestazioni restituite devono essere sufficiente tootell si presenti nel percorso corretto hello.

Assicurarsi che l'istanza di MongoDB sia in esecuzione.

    $sudo mongodb

Modificare la directory toohello e server hello esecuzione:

    $ cd azuread
    $ node server.js

In una nuova finestra del terminale eseguire `curl`

Provare un'operazione POST di base:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

L'errore 401 è risposta hello desiderato. Indica il livello di Passport hello sta tentando di tooredirect toohello autorizza un endpoint.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Ora è disponibile un servizio API REST che usa OAuth2
È stata implementata un'API REST usando Restify e OAuth. È ora sufficiente codice in modo da poter continuare toodevelop il servizio e compilare questo esempio. Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth2. Per il passaggio successivo, utilizzare una procedura dettagliata aggiuntiva come la [connettersi tooa web API con iOS B2C](active-directory-b2c-devquickstarts-ios.md) procedura dettagliata.

## <a name="next-steps"></a>Passaggi successivi
È possibile spostare argomenti toomore avanzate, ad esempio:

[Connettersi con iOS con B2C tooa web API](active-directory-b2c-devquickstarts-ios.md)
