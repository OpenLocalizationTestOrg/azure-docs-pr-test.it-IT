---
title: aaaDeploy un tooAzure di app web del servizio App Sails.js | Documenti Microsoft
description: Informazioni su come toodeploy un'applicazione Node.js servizio App di Azure. Questa esercitazione viene illustrato come un Sails.js toodeploy app web.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Distribuire un tooAzure di app web Sails.js servizio App
In questa esercitazione illustra come toodeploy un tooAzure app Sails.js servizio App. Nel processo di hello, è possibile raccogliere alcune informazioni generali su come tooconfigure il toorun app Node.js nel servizio App.

Questa esercitazione illustra alcune operazioni utili, ad esempio:

* Configurare l'esecuzione di un'app Sails.js nel servizio app.
* Distribuire un servizio di tooApp app dalla riga di comando hello.
* Stdout e stderr di lettura log tootroubleshoot eventuali problemi di distribuzione.
* Archiviare le variabili di ambiente al di fuori del controllo del codice sorgente.
* Accedere alle variabili di ambiente di Azure dall'app.
* Connettersi a database tooa (MongoDB).

Avere una conoscenza pratica di Sails.js. In questa esercitazione non è previsto toohelp i problemi correlati toorunning Sail.js in generale.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="prerequisites"></a>Prerequisiti
* [Node.JS](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2)
* Un account Microsoft Azure. Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure. Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Passaggio 1: Creare e configurare un'app Sails.js in locale
Innanzitutto, creare rapidamente un'app Sails.js predefinita nell'ambiente di sviluppo attenendosi alla procedura seguente:

1. Terminal della riga di comando di hello aperto di propria scelta e `CD` tooa directory di lavoro.
2. Creare un'app Sails.js ed eseguirla:

        sails new <app_name>
        cd <app_name>
        sails lift

    Verificare che è possibile passare una home page predefinita toohello in http://localhost:1377.

1. Abilitare quindi la registrazione per Azure. Nella directory radice, creare un file denominato `iisnode.yml` e aggiungere hello due righe seguenti:

        loggingEnabled: true
        logDirectory: iisnode

    La registrazione è ora abilitata per hello [iisnode](https://github.com/tjanczuk/iisnode) che Azure App Service utilizza App Node.js toorun server. 
    Per ulteriori informazioni sul funzionamento, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).

2. A questo punto, configurare le variabili di ambiente Azure toouse di hello Sails.js app. Aprire config/env/production.js tooconfigure nell'ambiente di produzione e impostare `port` e `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    La documentazione di queste impostazioni di configurazione è disponibile nella [Documentazione di Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Successivamente, impostare come hardcoded hello Node.js versione toouse. Nel file package. JSON, aggiungere hello seguenti `engines` proprietà tooset hello Node.js versione tooone che si desidera.

        "engines": {
            "node": "6.9.1"
        },

5. Inizializzare infine un repository Git ed eseguire il commit dei file. In hello radice dell'applicazione (in cui è package. JSON), eseguire hello Git comandi seguenti:

        git init
        git add .
        git commit -m "<your commit message>"

Il codice è pronto toobe distribuito. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Passaggio 2: Creare un'app Azure e distribuire Sails.js

Successivamente, creare hello risorsa del servizio App in Azure e distribuire il tooit app Sails.js.

1. Accedi tooAzure nel modo seguente:

        az login

    Seguire l'account di accesso di hello toocontinue prompt hello in un browser con un account Microsoft con la sottoscrizione di Azure.

3. Utente di distribuzione hello per servizio App. Si distribuirà il codice usando queste credenziali in un secondo momento.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con un nome. Per questa esercitazione Node.js, non è necessario tooknow che cos'è.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee i possibili valori da utilizzare per `<location>`, utilizzare hello `az appservice list-locations` comando CLI.

3. Creare un [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" con un nome. Per questa esercitazione su Node.js, è sufficiente sapere che non sono previsti costi per le app Web in questo piano.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Creare una nuova app Web con un nome univoco in `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Passaggio 3: Configurare e distribuire l'app Sails.js

1. Configurare la distribuzione Git locale per la nuova app web con hello comando seguente:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Si otterrà un output JSON come questo, che è stato configurato il repository Git remoto hello:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Aggiungere URL hello in hello JSON come un Git remoto per il repository locale (chiamato `azure` per motivi di semplicità).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Distribuire il toohello codice di esempio `azure` Git remoto. Quando richiesto, utilizzare le credenziali di distribuzione hello configurati in precedenza.

        git push azure master

7. Infine, ma è sufficiente avviare l'app di Azure in tempo reale nel browser hello:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Dovrebbe essere hello stessa Sails.js home page.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Risoluzione dei problemi di distribuzione
Se l'applicazione Sails.js non riesce per qualche motivo nel servizio App, trovare il log di stderr hello toohelp risoluzione dei problemi.
Per ulteriori informazioni, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).
Se l'applicazione hello sono stati avviati, devono visualizzare i log di stdout hello è familiare messaggio:

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

È possibile controllare la granularità dei log di stdout hello in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.

## <a name="connect-tooa-database-in-azure"></a>La connessione a database tooa in Azure
tooconnect tooa database in Azure, creare database hello di propria scelta in Azure, ad esempio Database SQL di Azure, MySQL, MongoDB, Cache di Azure (Redis), e così via e utilizzare hello corrispondente [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Hello passaggi in questa sezione viene illustrato come tooMongoDB tooconnect utilizzando un [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, che può supportare le connessioni client di MongoDB.

1. [Creare un account Cosmos DB con supporto del protocollo per MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Creare una raccolta e un database Cosmos DB](../documentdb/documentdb-create-collection.md). nome Hello dell'insieme di hello non è rilevante, ma è necessario il nome di hello del database di hello quando ci si connette da Sails.js.
3. [Trovare hello informazioni di connessione per il database DB Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Dal terminale della riga di comando, installare l'adapter di MongoDB hello:

        npm install sails-mongo --save

3. Aprire config/connections.js e aggiungere hello elenco toohello oggetto di connessione seguente:

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > Hello `ssl: true` opzione è importante perché [DB Cosmos richiede](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Per ogni variabile di ambiente (`process.env.*`), è necessario tooset nel servizio App. toodo, questa fase hello seguenti comandi dal terminale. Utilizzare le informazioni di connessione hello per le DB Cosmos.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    L'inserimento delle proprie impostazioni nelle impostazioni dell'app Azure mantiene i dati sensibili al di fuori del controllo del codice sorgente (Git). Passaggio successivo si configurerà lo sviluppo delle stesse informazioni di connessione di hello toouse di ambiente.
5. Aprire config/local.js e aggiungere hello segue l'oggetto di connessioni:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Questa configurazione sostituisce le impostazioni di hello nel file config/connections.js per ambiente locale hello. Questo file con estensione gitignore predefinito hello nel progetto viene escluso in modo non verranno archiviato in Git. A questo punto, si è in grado di tooconnect tooyour DB Cosmos (MongoDB) database dall'app web di Azure e nell'ambiente di sviluppo locale.
6. Aprire config/env/production.js tooconfigure nell'ambiente di produzione e aggiungere il seguente hello `models` oggetto:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Aprire config/env/development.js tooconfigure l'ambiente di sviluppo e aggiungere il seguente hello `models` oggetto:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`Consente di utilizzare toocreate funzionalità di migrazione del database e aggiornare facilmente le raccolte di database o tabelle. Tuttavia, `migrate: 'safe'` viene utilizzato per l'ambiente di Azure (produzione) perché Sails.js non è possibile toouse `migrate: 'alter'` in un ambiente di produzione (vedere [Sails.js documentazione](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Da hello terminal, [generare](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) un Sails.js [cianografia API](http://sailsjs.org/documentation/concepts/blueprints) come è in genere, quindi eseguito `sails lift` per creare database hello con Sails.js migrazione del database. ad esempio:

         sails generate api mywidget
         sails lift

    Hello `mywidget` modello generato da questo comando è vuoto, ma è possibile usarlo tooshow che si disponga della connettività di database.
    Quando si esegue `sails lift`, Crea raccolte mancante hello e modelli di tabelle per hello utilizzate dall'applicazione.
9. API di accesso hello progetto appena creato nel browser hello. ad esempio:

        http://localhost:1337/mywidget/create

    Hello API deve restituire tooyou indietro di hello creato voce nella finestra del browser hello, che significa che la raccolta è stata creata correttamente.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. A questo punto, push tooAzure le modifiche e passare tooyour app toomake verificarne che il corretto funzionamento.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Accesso API progetto iniziale di hello dell'app web di Azure. ad esempio:

         http://<appname>.azurewebsites.net/mywidget/create

     Se hello API restituisce un'altra nuova voce, quindi l'app web di Azure con cui sta comunicando tooyour DB Cosmos (MongoDB) database.

## <a name="more-resources"></a>Altre risorse
* [Introduzione alle app Web Node.js nel servizio app di Azure](app-service-web-get-started-nodejs.md)
* [Utilizzo di moduli Node.js con le applicazioni Azure](../nodejs-use-node-modules-azure-apps.md)
