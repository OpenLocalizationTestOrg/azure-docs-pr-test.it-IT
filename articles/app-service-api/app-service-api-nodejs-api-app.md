---
title: App per le API Node.js nel Servizio app di Azure | Microsoft Docs
description: Informazioni su come creare un'API RESTful Node.js e distribuirla in un'app per le API nel servizio app di Azure.
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
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="7c3de-103">Compilare un'API RESTful Node.js e distribuirla a un'app per le API in Azure</span><span class="sxs-lookup"><span data-stu-id="7c3de-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="7c3de-104">Questa guida introduttiva illustra come creare un'API REST, scritta con Node.js [Express](http://expressjs.com/), usando una definizione [Swagger](http://swagger.io/) e distribuirla in Azure come un'[app per le API](app-service-api-apps-why-best-platform.md).</span><span class="sxs-lookup"><span data-stu-id="7c3de-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="7c3de-105">Si creerà l'app usando gli strumenti da riga di comando, si configureranno le risorse con l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e si distribuirà l'app tramite Git.</span><span class="sxs-lookup"><span data-stu-id="7c3de-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="7c3de-106">Al termine, si avrà un'API REST di esempio in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c3de-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7c3de-107">Prerequisites</span></span>

* [<span data-ttu-id="7c3de-108">Git</span><span class="sxs-lookup"><span data-stu-id="7c3de-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="7c3de-109">Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="7c3de-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7c3de-110">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7c3de-111">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="7c3de-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="7c3de-112">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c3de-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="7c3de-113">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="7c3de-113">Prepare your environment</span></span>

1. <span data-ttu-id="7c3de-114">In una finestra del terminale eseguire il comando seguente per clonare il codice di esempio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="7c3de-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="7c3de-115">Passare alla directory contenente il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="7c3de-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="7c3de-116">Installare [Swaggerize](https://www.npmjs.com/package/swaggerize-express) nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="7c3de-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="7c3de-117">Swaggerize è uno strumento che genera codice Node.js per l'API REST da una definizione Swagger.</span><span class="sxs-lookup"><span data-stu-id="7c3de-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="7c3de-118">Generare codice Node.js</span><span class="sxs-lookup"><span data-stu-id="7c3de-118">Generate Node.js code</span></span> 

<span data-ttu-id="7c3de-119">In questa sezione dell'esercitazione viene modellato un flusso di lavoro di sviluppo di API che crea prima i metadati di Swagger e li usa per lo scaffolding (generazione automatica) del codice server per l'API.</span><span class="sxs-lookup"><span data-stu-id="7c3de-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="7c3de-120">Modificare la directory per impostarla sulla cartella di *avvio* e quindi eseguire `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="7c3de-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="7c3de-121">Swaggerize crea un progetto Node.js per l'API dalla definizione Swagger in *api.json*.</span><span class="sxs-lookup"><span data-stu-id="7c3de-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="7c3de-122">Quando Swaggerize chiede un nome di progetto, usare *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="7c3de-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="7c3de-123">Personalizzare il codice del progetto</span><span class="sxs-lookup"><span data-stu-id="7c3de-123">Customize the project code</span></span>

1. <span data-ttu-id="7c3de-124">Copiare la cartella *lib* nella cartella *ContactList* creata da `yo swaggerize` e quindi modificare la directory in *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="7c3de-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="7c3de-125">Installare i moduli NPM `jsonpath` e `swaggerize-ui`.</span><span class="sxs-lookup"><span data-stu-id="7c3de-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="7c3de-126">Sostituire il codice nel file *handlers/contacts.js* con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7c3de-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="7c3de-127">Questo codice usa i dati JSON archiviati nel file *lib/contacts.json* servito da *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="7c3de-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="7c3de-128">Il nuovo codice *contacts.js* restituisce tutti i contatti nel repository come un payload JSON.</span><span class="sxs-lookup"><span data-stu-id="7c3de-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="7c3de-129">Sostituire il codice nel file **handlers/contacts/{id}.js** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7c3de-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="7c3de-130">Questo codice consente di usare una variabile di percorso per restituire solo il contatto con un ID specifico.</span><span class="sxs-lookup"><span data-stu-id="7c3de-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="7c3de-131">Sostituire il codice nel file **server.js** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7c3de-131">Replace the code in **server.js** with the following code:</span></span>

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

    <span data-ttu-id="7c3de-132">Questo codice introduce alcune piccole modifiche che consentono di usarlo con il servizio app di Azure ed espone un'interfaccia Web interattiva per l'API.</span><span class="sxs-lookup"><span data-stu-id="7c3de-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="7c3de-133">Testare l'API in locale</span><span class="sxs-lookup"><span data-stu-id="7c3de-133">Test the API locally</span></span>

1. <span data-ttu-id="7c3de-134">Avviare l'app Node.js</span><span class="sxs-lookup"><span data-stu-id="7c3de-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="7c3de-135">Accedere a http://localhost:8000/contacts per visualizzare il codice JSON per l'intero elenco di contatti.</span><span class="sxs-lookup"><span data-stu-id="7c3de-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
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

3. <span data-ttu-id="7c3de-136">Accedere a http://localhost:8000/contacts/2 per visualizzare il contatto con un `id` su due.</span><span class="sxs-lookup"><span data-stu-id="7c3de-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="7c3de-137">Testare l'API usando l'interfaccia Web di Swagger all'indirizzo http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="7c3de-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interfaccia Web di Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="7c3de-139"><a id="createapiapp"></a> Creare un'app per le API</span><span class="sxs-lookup"><span data-stu-id="7c3de-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="7c3de-140">In questa sezione si usa l'interfaccia della riga di comando di Azure 2.0 per creare le risorse necessarie per ospitare l'API nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="7c3de-141">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="7c3de-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="7c3de-142">Se sono presenti più sottoscrizioni di Azure, cambiare la sottoscrizione predefinita specificando quella da usare.</span><span class="sxs-lookup"><span data-stu-id="7c3de-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="7c3de-143">Distribuire l'API con Git</span><span class="sxs-lookup"><span data-stu-id="7c3de-143">Deploy the API with Git</span></span>

<span data-ttu-id="7c3de-144">Distribuire il codice nell'app per le API effettuando il push dei commit dal repository Git locale al servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="7c3de-145">Inizializzare un nuovo repository nella directory *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="7c3de-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="7c3de-146">Escludere la directory *node_modules* creata da npm in un passaggio precedente dell'esercitazione in Git.</span><span class="sxs-lookup"><span data-stu-id="7c3de-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="7c3de-147">Creare un nuovo file `.gitignore` nella directory corrente e aggiungere il testo seguente in una nuova riga in un punto qualsiasi del file.</span><span class="sxs-lookup"><span data-stu-id="7c3de-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="7c3de-148">Confermare che la cartella `node_modules` venga ignorata con `git status`.</span><span class="sxs-lookup"><span data-stu-id="7c3de-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="7c3de-149">Eseguire il commit delle modifiche nel repository.</span><span class="sxs-lookup"><span data-stu-id="7c3de-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="7c3de-150">Testare l'API in Azure</span><span class="sxs-lookup"><span data-stu-id="7c3de-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="7c3de-151">Aprire una finestra del browser all'indirizzo http://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="7c3de-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="7c3de-152">Verrà visualizzato lo stesso codice JSON restituito quando è stata eseguita la richiesta in locale in un passaggio precedente dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7c3de-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

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

2. <span data-ttu-id="7c3de-153">In un browser accedere all'endpoint `http://app_name.azurewebsites.net/docs` per provare l'interfaccia utente di Swagger in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Interfaccia utente di Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="7c3de-155">È ora possibile distribuire gli aggiornamenti nell'API di esempio in Azure eseguendo il push dei commit nel repository Git di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3de-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="7c3de-156">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="7c3de-156">Clean up</span></span>

<span data-ttu-id="7c3de-157">Per eliminare tutte le risorse create nella presente guida introduttiva, eseguire questo comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="7c3de-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="7c3de-158">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="7c3de-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="7c3de-159">Usare app per le API da client JavaScript con CORS</span><span class="sxs-lookup"><span data-stu-id="7c3de-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

