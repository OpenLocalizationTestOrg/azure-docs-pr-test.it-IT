---
title: aaaAzure AD Node.js introduzione | Documenti Microsoft
description: Come toobuild un'API web Node. js REST che si integra con Azure AD per l'autenticazione.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Introduzione alle API Web per Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* è il middleware di autenticazione per Node.js. Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o Restify applicazione web. Una gamma completa di strategie supporta l'autenticazione con nome utente e password, Facebook, Twitter e altro ancora. È stata sviluppata una strategia per Microsoft Azure Active Directory (Azure AD). È installare il modulo e quindi aggiungere hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo, è necessario:

1. Registrare un'applicazione con Azure AD.
2. Configurare l'app toouse Passport `passport-azure-ad` plug-in.
3. Configurare un client applicazione toocall hello tooDo API web elenco.

codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> In questo articolo non copre come tooimplement Accedi, effettua l'iscrizione, o profilo di gestione con Azure Active Directory B2C. Si concentra sulle API web chiamante dopo hello è già autenticato.  È consigliabile iniziare con [come toointegrate con documenti di Azure Active Directory](active-directory-how-to-integrate.md) toolearn sui concetti di base di hello di Azure Active Directory.
>
>

È stato rilasciato tutto il codice sorgente hello per questo esempio in esecuzione in GitHub in base a una licenza MIT, pertanto è possibile tooclone disponibile (o ancora meglio, divisione) e fornire commenti e suggerimenti e le richieste pull.

## <a name="about-nodejs-modules"></a>Informazioni sui moduli Node.js
In questa procedura dettagliata vengono usati i moduli Node.js. I moduli sono pacchetti JavaScript caricabili che forniscono funzionalità specifiche per l'applicazione. È in genere installare moduli utilizzando uno strumento da riga di comando di NPM Node.js hello nella directory di installazione NPM hello. Tuttavia, alcuni moduli, ad esempio modulo HTTP hello, sono inclusi nel pacchetto di Node.js di hello core.

I moduli installati vengono salvati in hello **node_modules** directory principale di hello della directory di installazione di Node.js. Ogni modulo in hello **node_modules** directory mantiene il proprio **node_modules** directory che contiene tutti i moduli da cui dipende. Ogni modulo necessario ha una directory **node_modules**. Questa struttura di directory ricorsiva rappresenta la catena di dipendenze hello.

Questa struttura della catena di dipendenze comporta un footprint maggiore delle applicazioni, Tuttavia, garantisce inoltre che tutte le dipendenze siano soddisfatti e che tale versione di hello dei moduli hello utilizzato in fase di sviluppo viene utilizzato anche nell'ambiente di produzione. Questo rende più prevedibile un comportamento dell'app produzione hello ed evita i problemi di controllo delle versioni che potrebbero interessare gli utenti.

## <a name="step-1-register-an-azure-ad-tenant"></a>Passaggio 1: Registrare un tenant di Azure AD
toouse questo esempio, è necessario un tenant Azure Active Directory. Se non si conosce il tenant è o tooget uno, vedere [come tooget un Azure AD tenant](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Passaggio 2:Creare un'applicazione
Successivamente si crea un'applicazione nella directory di Azure AD offre informazioni talmente toosecurely di comunicare con l'app.  App client hello sia API web sono rappresentate da una singola **ID applicazione** in questo caso, poiché comprendono una sola app logica.  toocreate un'app, seguire [queste istruzioni](active-directory-how-applications-are-added.md). Se si compila un'app line-of-business, [queste istruzioni aggiuntive](../active-directory-applications-guiding-developers-for-lob-applications.md) possono risultare utili.

toocreate un'applicazione:

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel menu superiore hello, selezionare l'account. Quindi, in hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.

3. Dal menu hello hello sinistra, selezionare **più servizi**, quindi selezionare **Azure Active Directory**.

4. Selezionare **Registrazioni per l'app**, quindi scegliere **Aggiungi**.

5. Seguire hello richieste toocreate un **applicazione Web e/o WebAPI**.

      * Hello **nome** di hello applicazione descrive tooend utenti applicazione.

      * Hello **Sign-On URL** hello URL di base dell'app.  URL del codice di esempio hello predefinito è Hello `https://localhost:8080`.

6. Dopo la registrazione, Azure AD assegna all'app un ID applicazione univoco. Questo valore è necessario in hello nelle sezioni seguenti, quindi copiarlo dalla pagina dell'applicazione hello.

7. Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App. Hello **URI ID App** è un identificatore univoco per l'applicazione. convenzione di Hello è toouse `https://<tenant-domain>/<app-name>`, ad esempio: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Creare un **chiave** per l'applicazione dalla hello **impostazioni** pagina e quindi copiarlo in un punto. perché verrà richiesta a breve.

## <a name="step-3-download-nodejs-for-your-platform"></a>Passaggio 3: Scaricare Node.js per la piattaforma corrente
toosuccessfully usare questo esempio, è necessario disporre di un'installazione funzionante di Node.js.

Installare Node.js da [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Passaggio 4: Installare MongoDB nella piattaforma
toosuccessfully usare questo esempio, è necessario disporre di un'installazione funzionante di MongoDB. Utilizzare MongoDB toomake hello API REST persistente tra istanze del server.

Installare MongoDB da [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Questa procedura dettagliata si presuppone che si gli endpoint di installazione e il server predefinito hello per MongoDB, che in fase di hello di questo articolo è mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Passaggio 5: Installare i moduli Restify hello in web API
Si sta usando Restify toobuild API REST. Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express, che include una gamma completa di funzionalità per la compilazione di API REST basate su Connect.

### <a name="install-restify"></a>Installare Restify
1. Dalla riga di comando hello, modificare le directory toohello **azuread** directory. Se hello **azuread** directory non esiste, crearla.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Digitare hello comando seguente:

    `npm install restify`

    Questo comando installa Restify.

#### <a name="did-you-get-an-error"></a>È stato visualizzato un errore?
Quando si usa NPM in alcuni sistemi operativi, potrebbe essere visualizzato il messaggio di errore **Error: EPERM, chmod '/usr/local/bin/..'** e un suggerimento che si tenta di account hello in esecuzione come amministratore. In questo caso, è possibile utilizzare hello sudo comando toorun NPM a un livello di privilegio superiore.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>È stato visualizzato un errore relativo a DTrace?
Durante l'installazione di Restify, potrebbe essere visualizzato un errore simile al seguente:

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

output di Hello di questo comando dovrebbe essere simile toohello seguente output:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Passaggio 6: Installare Passport.js nell'API Web
[Passport](http://passportjs.org/) è il middleware di autenticazione per Node.js. Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o Restify applicazione web. Una gamma completa di strategie supporta l'autenticazione con nome utente e password, Facebook, Twitter e altro ancora.

È stata sviluppata una strategia per Azure Active Directory. Si installa il modulo e quindi aggiunta strategia di Azure Active Directory hello plug-in.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** directory.

2. passport.js tooinstall, immettere hello comando seguente:

    `npm install passport`

    output di Hello del comando hello dovrebbe essere simile toohello seguenti:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Passaggio 7: Aggiungere AD di Azure di Passport tooyour web API
Questo punto verranno aggiunte strategia OAuth hello utilizzando `passport-azure-ad`, una suite di strategie che si connettono tooPassport Azure Active Directory. In questo esempio di API REST tale strategia viene usata per i token di connessione.

> [!NOTE]
> Anche se OAuth2 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, i più diffusi sono solo alcuni. I token di connessione sono token di hello più comunemente usato per la protezione di endpoint. Si tratta di tipo hello maggiormente emesso del token in OAuth2. Molte implementazioni presuppongono che i token di connessione sono hello unico tipo di token rilasciati.
>
>

Dalla riga di comando hello, modificare le directory toohello **azuread** directory.

Comando che segue hello di tipo hello tooinstall Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

output di Hello del comando hello dovrebbe essere simile toohello seguente output:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Passaggio 8: Aggiungere MongoDB moduli tooyour web API
MongoDB viene usato come archivio dati. Per questo motivo, è necessario tooinstall hello ampiamente utilizzato nei modelli di plug-in chiamati Mongoose toomanage e schemi. È anche necessario driver di database hello tooinstall per MongoDB (denominato anche MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Passaggio 9: Installare moduli aggiuntivi
È quindi possibile installare hello rimanenti moduli necessari.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

    `cd azuread`

2. Immettere hello seguenti comandi tooinstall questi moduli nel **node_modules** directory:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Passaggio 10: Creare un file server.js con le dipendenze
file server.js Hello fornisce la maggior parte delle funzionalità di hello per l'API del server web. Aggiungere la maggior parte dei file di toothis il nostro codice. Ai fini della produzione, è consigliabile eseguire il refactoring funzionalità hello in file più piccoli, ad esempio route distinte e controller. In questa dimostrazione si usa server.js per questa funzionalità.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

    `cd azuread`

2. Creare un `server.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Salvare il file hello. Tooit sarà restituiamo a breve.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Passaggio 11: Creare un toostore di file di configurazione delle impostazioni di Azure AD
Questo file di codice passa i parametri di configurazione hello dal tooPassport.js del portale di Azure Active Directory. Questi valori di configurazione è stato creato quando è stato aggiunto portale toohello API web di hello nella prima parte di hello della procedura dettagliata hello. Viene descritto il tooput in valori hello di questi parametri dopo aver copiato il codice hello.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

    `cd azuread`

2. Creare un `config.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Salvare il file hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Passaggio 12: Aggiunta di file di configurazione valori tooyour server.js
È necessario tooread questi valori dal file config hello creato attraverso l'applicazione. toodo, aggiungiamo file hello. config come una risorsa necessaria nell'applicazione. Quindi impostiamo hello globale toomatch hello variabili nel documento config.js hello.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

    `cd azuread`

2. Aprire il `server.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:

    ```Javascript
    var config = require('./config');
    ```
3. Quindi aggiungere una nuova sezione troppo`server.js` con hello seguente codice:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Salvare il file hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Passaggio 13: Aggiunta di hello MongoDB modello e le informazioni tramite Mongoose
Ora tutti questa preparazione in corso toostart estinzione come questi tre file vengono combinati in un servizio API REST.

Questa procedura dettagliata, utilizziamo MongoDB toostore l'attività come descritto nel passaggio 4.

In hello `config.js` file che abbiamo creato nel passaggio 11, viene chiamato dal database `tasklist`, perché questo è ciò che è stato inserito alla fine di hello del nostro **mogoose_auth_local** URL di connessione. Non è necessario toocreate questo database in anticipo in MongoDB. Al contrario, MongoDB crea questo per noi in hello prima esecuzione dell'applicazione server (supponendo che il database hello non esiste già).

Ora che è stato indicato server hello quale database MongoDB desideriamo toouse, abbiamo bisogno di toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.

### <a name="discussion-of-hello-model"></a>Descrizione del modello di hello
Questo modello di schema è semplice ed è possibile espanderlo in base alle esigenze.

NOME: il nome di hello della persona hello toohello attività assegnata. Valore **stringa**.

: Hello attività stessa. Valore **stringa**.

: Hello Data attività hello viene scadenza. Valore **datetime**.

COMPLETATA: Se l'attività hello è completata o non. Valore **booleano**.

### <a name="creating-hello-schema-in-hello-code"></a>Creazione di schema hello in codice hello
1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

    `cd azuread`

2. Aprire il `server.js` file in un editor qualsiasi e quindi aggiungere le seguenti informazioni di sotto la voce di configurazione hello hello:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
Come si può vedere dal codice hello, abbiamo creato prima il nostro schema. Quindi si crea un oggetto modello utilizziamo toostore i dati in tutto hello codice quando si definisce il nostro **route**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Passaggio 14: Aggiungere le route per il server API REST delle attività
Ora che è disponibile un toowork del modello di database con, aggiungere route hello è in corso utilizzare per i server API REST.

### <a name="about-routes-in-restify"></a>Informazioni sulle route in Restify
Le route funzionano in hello Restify stesso modo che in hello Express dello stack. Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello. Le route si definiscono di solito in un file separato. A questo scopo, la route è inserito nel file server.js hello. È consigliabile inserirle in un file a parte per usarle in fase di produzione.

Di seguito è riportato un modello tipico per una route Restify:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Si tratta hello modello al livello più elementare. Restify ed Express offrono funzionalità molto più avanzate, ad esempio la definizione di tipi di applicazione e l'esecuzione di un routing complesso tra endpoint diversi. Ai fini di questa procedura dettagliata, vengono usate route semplici.

### <a name="add-default-routes-tooour-server"></a>Aggiungere server tooour di route predefinita
È ora aggiungere hello route CRUD di base di creazione, recupero, aggiornamento ed eliminare.

1. Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente:

    `cd azuread`

2. Aprire hello `server.js` file in un editor qualsiasi e quindi aggiungere le seguenti informazioni di sotto di voci del database precedente hello apportate hello:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Aggiungere la gestione degli errori nelle API
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Passaggio 15: Creare il server
Ora che il database è stato definito e le route sono state aggiunte, Hello ultima operazione toodo aggiungere istanza hello del server che gestisce delle chiamate.

Restify (e Express) è possibile eseguire una grande quantità di personalizzazione per un server API REST, ma verrà nuovamente il programma di installazione di toouse hello più semplice a questo scopo.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Passaggio 16: Aggiungere server di toohello route hello (senza autenticazione per il momento)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Passaggio 17: Eseguire server hello (prima dell'aggiunta del supporto di OAuth)
Testare il server prima di aggiungere l'autenticazione.

tootest modo più semplice Hello del server è tramite curl in una riga di comando. Prima di procedere è dobbiamo un'utilità che consente di elaborare tooparse output in formato JSON.

1. Installare hello strumento JSON (hello tutti i seguenti esempi di questo strumento) seguenti:

    `$npm install -g jsontool`

    Vengono installati lo strumento JSON hello a livello globale. Ora che è stato portato a termine che, di seguito riprodurre con server hello:

2. Assicurarsi prima di tutto che l'istanza di MongoDB sia in esecuzione:

    `$sudo mongod`

3. Quindi, modificare la directory toohello e avviare per:

    `$ cd azuread``$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. Ora è possibile aggiungere un'attività in questo modo:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

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
    È anche possibile elencare le attività di Brandon in questo modo:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Se tutto funziona, siamo tooadd pronto OAuth toohello API REST del server.

Ora si dispone di un'API REST con MongoDB.

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Passaggio 18: Aggiunta di server API REST di autenticazione tooour
Ora che l'API REST è in esecuzione è possibile iniziare a usarla con Azure AD.

Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Utilizzare hello OIDCBearerStrategy inclusa passport-azure Active Directory
Nei passaggi precedenti è stato creato un tipico server REST TODO senza alcun tipo di autenticazione. Questa operazione è stata eseguita nel modo indicato di seguito.

1. Innanzitutto, è necessario che si desidera toouse Passport tooindicate. Inserire il codice subito dopo la configurazione dell'altro server:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Quando si scrivono le API, è consigliabile collegare sempre toosomething dati hello univoco da token hello hello utente non può effettuare lo spoofing. Quando il server archivia elementi TODO, li archivia in base all'ID di oggetto hello dell'utente hello nel token hello (chiamati tramite token.oid), che è stato inserito nel campo "proprietario" hello. In questo modo, solo l'utente può accedere ai relativi elementi TODO. Non è non presenti rischi in hello API di "proprietario", un utente esterno può richiedere hello TODOs di altri utenti, anche se vengono autenticati.                    

2. Avanti utilizziamo strategia connessione hello fornita con `passport-azure-ad`. Esaminare il codice hello per il momento e spiega rest hello a breve. Inserire il codice seguente dopo quanto incollato in precedenza:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via) seguite dagli scrittori della strategia. Esaminando la strategia di hello, vedere che vengono passati una funzione che ha un token e un fatto come parametri hello. strategia di Hello proviene toous nuovamente dopo che esegue il proprio lavoro. Dopo questo caso, vengono archiviati utente hello e token hello stash in modo non dobbiamo tooask per tale nuovamente.

> [!IMPORTANT]
> il codice precedente di Hello in tutti gli utenti che si verificano tooauthenticate tooour server. Questa operazione è nota come registrazione automatica. Nei server di produzione è preferibile non consentire l'accesso a chiunque senza prima prevedere un processo di registrazione. Si tratta in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere toofill informazioni aggiuntive. Se questo non è un programma della riga di comando, è possibile estrarre posta elettronica hello dall'oggetto token hello è restituito e quindi richiesto hello utente toofill informazioni aggiuntive. Poiché si tratta di un server di prova, è sufficiente aggiungerli database in memoria toohello.
>
>

### <a name="protect-some-endpoints"></a>Proteggere alcuni endpoint
Proteggere gli endpoint specificando hello `passport.authenticate()` chiamata con protocollo hello che si desidera toouse.

il codice server effettuare ulteriori qualcosa di interessante, toomake Modifica route hello.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Passaggio 19: Eseguire nuovamente l'applicazione server e assicurarsi che rifiuti l'utente
Consente di usare `curl` nuovamente toosee se OAuth2 protection è ora disponibile su questo endpoint. Eseguire il test prima di eseguire qualsiasi SDK client in questo endpoint. Hello intestazioni che vengono restituite devono essere sufficiente tootell ci se verrà percorso corretto hello verso il basso.

1. Assicurarsi prima di tutto che l'istanza di MongoDB sia in esecuzione:

    `$sudo mongod`

2. Quindi, modificare la directory toohello e avviare per.

      `$ cd azuread``$ node server.js`

3. Provare un'operazione POST di base.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 è risposta hello che si sta cercando di seguito. Questa risposta indica che il livello di Passport hello sta cercando tooredirect toohello autorizzato endpoint, che è esattamente quello desiderato.

## <a name="next-steps"></a>Passaggi successivi
Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth2. Sarà necessario toogo tramite una procedura dettagliata di aggiuntiva.

Dopo avere appreso come tooimplement un'API REST tramite Restify e OAuth2. È inoltre più che sufficiente tookeep codice lo sviluppo del servizio e di apprendimento come toobuild in questo esempio.

Se si è interessati in passaggi successivi hello in consentirti di ADAL, ecco alcuni client ADAL supportati, è consigliabile che continuare a lavorare con.

Clonare computer dello sviluppatore tooyour verso il basso e configurare come descritto nella procedura dettagliata hello.

[ADAL per iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
