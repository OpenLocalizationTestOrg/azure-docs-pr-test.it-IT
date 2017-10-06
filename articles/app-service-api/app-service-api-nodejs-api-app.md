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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="e07c9-103">Compilare un'API RESTful Node.js e distribuirlo tooan API app in Azure</span><span class="sxs-lookup"><span data-stu-id="e07c9-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="e07c9-104">Questa Guida introduttiva viene illustrato come toocreate un'API REST, scritto con Node.js [Express](http://expressjs.com/), usando un [Swagger](http://swagger.io/) definizione e la distribuzione come un [app per le API](app-service-api-apps-why-best-platform.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c9-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="e07c9-105">È possibile creare app hello utilizzando gli strumenti da riga di comando, configurare le risorse con hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e distribuire app hello tramite Git.</span><span class="sxs-lookup"><span data-stu-id="e07c9-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="e07c9-106">Al termine, si avrà un'API REST di esempio in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c9-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e07c9-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e07c9-107">Prerequisites</span></span>

* [<span data-ttu-id="e07c9-108">Git</span><span class="sxs-lookup"><span data-stu-id="e07c9-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="e07c9-109">Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="e07c9-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e07c9-110">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e07c9-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e07c9-111">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="e07c9-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e07c9-112">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e07c9-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="e07c9-113">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="e07c9-113">Prepare your environment</span></span>

1. <span data-ttu-id="e07c9-114">In una finestra terminale, eseguire hello successivo comando tooclone hello esempio tooyour locale.</span><span class="sxs-lookup"><span data-stu-id="e07c9-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="e07c9-115">Spostarsi nella directory toohello che contiene il codice di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e07c9-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="e07c9-116">Installare [Swaggerize](https://www.npmjs.com/package/swaggerize-express) nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e07c9-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="e07c9-117">Swaggerize è uno strumento che genera codice Node.js per l'API REST da una definizione Swagger.</span><span class="sxs-lookup"><span data-stu-id="e07c9-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="e07c9-118">Generare codice Node.js</span><span class="sxs-lookup"><span data-stu-id="e07c9-118">Generate Node.js code</span></span> 

<span data-ttu-id="e07c9-119">In questa sezione dell'esercitazione hello modella un'API lo sviluppo del flusso di lavoro in cui creare i metadati Swagger prima e utilizzare tale tooscaffold (generazione automatica) codice lato server per hello API.</span><span class="sxs-lookup"><span data-stu-id="e07c9-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="e07c9-120">Cambiare directory toohello *avviare* cartella, quindi eseguire `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="e07c9-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="e07c9-121">Swaggerize crea un progetto di Node.js per l'API dalla definizione Swagger hello in *api.json*.</span><span class="sxs-lookup"><span data-stu-id="e07c9-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="e07c9-122">Quando Swaggerize chiede un nome di progetto, usare *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="e07c9-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="e07c9-123">Personalizzare il codice del progetto hello</span><span class="sxs-lookup"><span data-stu-id="e07c9-123">Customize hello project code</span></span>

1. <span data-ttu-id="e07c9-124">Hello copia *lib* hello nella cartella *ContactList* cartella creata da `yo swaggerize`, quindi spostarsi in *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="e07c9-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="e07c9-125">Installare hello `jsonpath` e `swaggerize-ui` moduli NPM.</span><span class="sxs-lookup"><span data-stu-id="e07c9-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="e07c9-126">Sostituire il codice hello in hello *handlers/contacts.js* con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="e07c9-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="e07c9-127">Questo codice Usa i dati JSON hello archiviati in *lib/contacts.json* servita dal *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="e07c9-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="e07c9-128">nuovo Hello *contacts.js* codice restituisce tutti i contatti nel repository di hello come un payload JSON.</span><span class="sxs-lookup"><span data-stu-id="e07c9-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="e07c9-129">Sostituire il codice hello in hello **handlers/contacts/{id}.js** file con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="e07c9-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="e07c9-130">Questo codice consente di utilizzare un percorso tooreturn variabile solo hello contatto con un ID specificato.</span><span class="sxs-lookup"><span data-stu-id="e07c9-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="e07c9-131">Sostituire il codice hello in **server.js** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="e07c9-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="e07c9-132">Questo codice rende toolet alcune piccole modifiche funziona con il servizio App di Azure ed espone un'interfaccia web interattive per l'API.</span><span class="sxs-lookup"><span data-stu-id="e07c9-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="e07c9-133">Hello test API in locale</span><span class="sxs-lookup"><span data-stu-id="e07c9-133">Test hello API locally</span></span>

1. <span data-ttu-id="e07c9-134">Avvio app Node.js hello</span><span class="sxs-lookup"><span data-stu-id="e07c9-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="e07c9-135">Sfoglia toohttp://localhost:8000 / contatta hello tooview JSON per l'intero elenco di contatti hello.</span><span class="sxs-lookup"><span data-stu-id="e07c9-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="e07c9-136">Sfoglia toohttp://localhost:8000 contatti/2 tooview hello contatto con un `id` di due.</span><span class="sxs-lookup"><span data-stu-id="e07c9-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="e07c9-137">Tramite l'interfaccia web di Swagger hello in http://localhost:8000/servicemodelsamples/Service/docs API hello del test.</span><span class="sxs-lookup"><span data-stu-id="e07c9-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interfaccia Web di Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="e07c9-139"><a id="createapiapp"></a> Creare un'app per le API</span><span class="sxs-lookup"><span data-stu-id="e07c9-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="e07c9-140">In questa sezione utilizzare hello Azure CLI 2.0 toocreate hello risorse toohost hello API nel servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c9-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="e07c9-141">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="e07c9-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="e07c9-142">Se si dispone di più sottoscrizioni di Azure, modifica hello predefinito sottoscrizione toohello desiderato uno.</span><span class="sxs-lookup"><span data-stu-id="e07c9-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="e07c9-143">Distribuire l'API di hello con Git</span><span class="sxs-lookup"><span data-stu-id="e07c9-143">Deploy hello API with Git</span></span>

<span data-ttu-id="e07c9-144">Distribuire app per le API toohello codice mediante il push dei commit dal tooAzure di repository Git locale del servizio App.</span><span class="sxs-lookup"><span data-stu-id="e07c9-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="e07c9-145">Inizializzare un nuovo repository in hello *ContactList* directory.</span><span class="sxs-lookup"><span data-stu-id="e07c9-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="e07c9-146">Escludere hello *node_modules* directory creato da npm in precedenza nell'esercitazione di hello da Git.</span><span class="sxs-lookup"><span data-stu-id="e07c9-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="e07c9-147">Creare un nuovo `.gitignore` file nella directory corrente hello e aggiungere hello dopo il testo in una nuova riga in un punto qualsiasi nel file hello.</span><span class="sxs-lookup"><span data-stu-id="e07c9-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="e07c9-148">Conferma hello `node_modules` cartella verrà ignorata con `git status`.</span><span class="sxs-lookup"><span data-stu-id="e07c9-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="e07c9-149">Eseguire il commit hello modifiche toohello repository.</span><span class="sxs-lookup"><span data-stu-id="e07c9-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="e07c9-150">Hello test API in Azure</span><span class="sxs-lookup"><span data-stu-id="e07c9-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="e07c9-151">Aprire un browser toohttp://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="e07c9-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="e07c9-152">Vedrai hello che stesso JSON restituito come se apportate in precedenza nell'esercitazione hello richiesta hello in locale.</span><span class="sxs-lookup"><span data-stu-id="e07c9-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="e07c9-153">In un browser, visitare toohello `http://app_name.azurewebsites.net/docs` tootry endpoint out hello Swagger dell'interfaccia utente in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c9-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Interfaccia utente di Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="e07c9-155">È ora possibile distribuire gli aggiornamenti toohello esempio API tooAzure eseguendo il push dei commit toohello Azure Git repository.</span><span class="sxs-lookup"><span data-stu-id="e07c9-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="e07c9-156">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="e07c9-156">Clean up</span></span>

<span data-ttu-id="e07c9-157">tooclean le risorse di hello creato in questa Guida rapida, eseguire il comando CLI di Azure seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e07c9-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="e07c9-158">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="e07c9-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="e07c9-159">Usare app per le API da client JavaScript con CORS</span><span class="sxs-lookup"><span data-stu-id="e07c9-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

