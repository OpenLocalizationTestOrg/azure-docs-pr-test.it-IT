---
title: app aaaNode.js API nel servizio App di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'API RESTful Node.js e distribuzione di app tooan API nel servizio App di Azure.
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Compilare un'API RESTful Node.js e distribuirlo tooan API app in Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Questa Guida introduttiva viene illustrato come toocreate un'API REST, scritto con Node.js [Express](http://expressjs.com/), usando un [Swagger](http://swagger.io/) definizione e la distribuzione come un [app per le API](app-service-api-apps-why-best-platform.md) in Azure. È possibile creare app hello utilizzando gli strumenti da riga di comando, configurare le risorse con hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e distribuire app hello tramite Git.  Al termine, si avrà un'API REST di esempio in esecuzione in Azure.

## <a name="prerequisites"></a>Prerequisiti

* [Git](https://git-scm.com/)
* [Node.js e NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Preparare l'ambiente

1. In una finestra terminale, eseguire hello successivo comando tooclone hello esempio tooyour locale.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Spostarsi nella directory toohello che contiene il codice di esempio hello.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Installare [Swaggerize](https://www.npmjs.com/package/swaggerize-express) nel computer locale. Swaggerize è uno strumento che genera codice Node.js per l'API REST da una definizione Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Generare codice Node.js 

In questa sezione dell'esercitazione hello modella un'API lo sviluppo del flusso di lavoro in cui creare i metadati Swagger prima e utilizzare tale tooscaffold (generazione automatica) codice lato server per hello API. 

Cambiare directory toohello *avviare* cartella, quindi eseguire `yo swaggerize`. Swaggerize crea un progetto di Node.js per l'API dalla definizione Swagger hello in *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Quando Swaggerize chiede un nome di progetto, usare *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Personalizzare il codice del progetto hello

1. Hello copia *lib* hello nella cartella *ContactList* cartella creata da `yo swaggerize`, quindi spostarsi in *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Installare hello `jsonpath` e `swaggerize-ui` moduli NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Sostituire il codice hello in hello *handlers/contacts.js* con hello seguente codice: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Questo codice Usa i dati JSON hello archiviati in *lib/contacts.json* servita dal *lib/contactRepository.js*. nuovo Hello *contacts.js* codice restituisce tutti i contatti nel repository di hello come un payload JSON. 

4. Sostituire il codice hello in hello **handlers/contacts/{id}.js** file con hello seguente codice:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Questo codice consente di utilizzare un percorso tooreturn variabile solo hello contatto con un ID specificato.

5. Sostituire il codice hello in **server.js** con hello seguente codice:

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    Questo codice rende toolet alcune piccole modifiche funziona con il servizio App di Azure ed espone un'interfaccia web interattive per l'API.

### <a name="test-hello-api-locally"></a>Hello test API in locale

1. Avvio app Node.js hello
    ```bash
    npm start
    ```
    
2. Sfoglia toohttp://localhost:8000 / contatta hello tooview JSON per l'intero elenco di contatti hello.
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. Sfoglia toohttp://localhost:8000 contatti/2 tooview hello contatto con un `id` di due.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. Tramite l'interfaccia web di Swagger hello in http://localhost:8000/servicemodelsamples/Service/docs API hello del test.
   
    ![Interfaccia Web di Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Creare un'app per le API

In questa sezione utilizzare hello Azure CLI 2.0 toocreate hello risorse toohost hello API nel servizio App di Azure. 

1.  Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.

    ```azurecli-interactive
    az login
    ```

2. Se si dispone di più sottoscrizioni di Azure, modifica hello predefinito sottoscrizione toohello desiderato uno.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Distribuire l'API di hello con Git

Distribuire app per le API toohello codice mediante il push dei commit dal tooAzure di repository Git locale del servizio App.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Inizializzare un nuovo repository in hello *ContactList* directory. 

    ```bash
    git init .
    ```

3. Escludere hello *node_modules* directory creato da npm in precedenza nell'esercitazione di hello da Git. Creare un nuovo `.gitignore` file nella directory corrente hello e aggiungere hello dopo il testo in una nuova riga in un punto qualsiasi nel file hello.

    ```
    node_modules/
    ```
    Conferma hello `node_modules` cartella verrà ignorata con `git status`.

4. Eseguire il commit hello modifiche toohello repository.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Hello test API in Azure

1. Aprire un browser toohttp://app_name.azurewebsites.net/contacts. Vedrai hello che stesso JSON restituito come se apportate in precedenza nell'esercitazione hello richiesta hello in locale.

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. In un browser, visitare toohello `http://app_name.azurewebsites.net/docs` tootry endpoint out hello Swagger dell'interfaccia utente in esecuzione in Azure.

    ![Interfaccia utente di Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    È ora possibile distribuire gli aggiornamenti toohello esempio API tooAzure eseguendo il push dei commit toohello Azure Git repository.

## <a name="clean-up"></a>Eseguire la pulizia

tooclean le risorse di hello creato in questa Guida rapida, eseguire il comando CLI di Azure seguente hello:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Passaggio successivo 
> [!div class="nextstepaction"]
> [Usare app per le API da client JavaScript con CORS](app-service-api-cors-consume-javascript.md)

