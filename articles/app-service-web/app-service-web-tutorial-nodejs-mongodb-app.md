---
title: aaaBuild un'app web Node. js e MongoDB in Azure | Documenti Microsoft
description: Informazioni su come tooget un'app Node.js Usa Azure, con connessione tooa Cosmos DB database con una stringa di connessione di MongoDB.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="1b545-103">Creare un'app Web Node.js e MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="1b545-104">Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="1b545-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1b545-105">Questa esercitazione viene illustrato come un Node.js toocreate web app in Azure e connetterla database MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="1b545-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="1b545-106">Al termine, si avrà un'applicazione MEAN (MongoDB, Express, AngularJS e Node.js) in esecuzione nel [servizio app di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b545-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="1b545-107">Per semplicità, l'applicazione di esempio hello utilizza hello [framework web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="1b545-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="1b545-109">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1b545-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b545-110">Creare un database MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="1b545-111">Connettersi a un tooMongoDB app Node.js</span><span class="sxs-lookup"><span data-stu-id="1b545-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="1b545-112">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b545-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1b545-113">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1b545-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="1b545-114">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="1b545-115">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b545-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1b545-116">Prerequisites</span></span>

<span data-ttu-id="1b545-117">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1b545-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="1b545-118">Installare Git</span><span class="sxs-lookup"><span data-stu-id="1b545-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="1b545-119">Installare Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="1b545-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="1b545-120">[Installare Gulp.js](http://gulpjs.com/), richiesto da [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started)</span><span class="sxs-lookup"><span data-stu-id="1b545-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="1b545-121">Installare ed eseguire MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="1b545-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1b545-122">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1b545-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1b545-123">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1b545-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1b545-124">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1b545-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="1b545-125">Testare il MongoDB locale</span><span class="sxs-lookup"><span data-stu-id="1b545-125">Test local MongoDB</span></span>

<span data-ttu-id="1b545-126">Finestra terminal aprire hello e `cd` toohello `bin` directory di installazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b545-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="1b545-127">In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="1b545-128">Eseguire `mongo` nell'istanza hello tooconnect terminal tooyour locale MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="1b545-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="1b545-129">Se la connessione ha esito positivo significa che il database MongoDB è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1b545-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="1b545-130">In caso contrario, assicurarsi che sia stato avviato il database MongoDB locale seguendo i passaggi di hello in [installare MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="1b545-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="1b545-131">Spesso, MongoDB è installato, ma è comunque necessario toostart eseguendo `mongod`.</span><span class="sxs-lookup"><span data-stu-id="1b545-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="1b545-132">Al termine di test del database MongoDB, digitare `Ctrl+C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="1b545-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="1b545-133">Creare l'app Node.js locale</span><span class="sxs-lookup"><span data-stu-id="1b545-133">Create local Node.js app</span></span>

<span data-ttu-id="1b545-134">In questo passaggio, impostare il progetto Node.js locale di hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="1b545-135">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="1b545-135">Clone hello sample application</span></span>

<span data-ttu-id="1b545-136">Nella finestra terminal hello `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1b545-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="1b545-137">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="1b545-138">Il repository di esempio contiene una copia di hello [MEAN.js repository](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="1b545-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="1b545-139">È toorun modificate nel servizio App (per ulteriori informazioni, vedere repository MEAN.js hello [file README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="1b545-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="1b545-140">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1b545-140">Run hello application</span></span>

<span data-ttu-id="1b545-141">Eseguire hello i pacchetti hello necessario tooinstall i comandi seguenti e avviare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="1b545-142">Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="1b545-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="1b545-143">Passare toohttp://localhost:3000 in un browser.</span><span class="sxs-lookup"><span data-stu-id="1b545-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="1b545-144">Fare clic su **iscrizione** in hello menu superiore e creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="1b545-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="1b545-145">applicazione di esempio MEAN.js Hello archivia i dati utente nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="1b545-146">Se hanno esito positivo alla creazione di un utente ed eseguire l'accesso, l'app sta scrivendo database MongoDB locale di dati toohello.</span><span class="sxs-lookup"><span data-stu-id="1b545-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js si connette correttamente tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="1b545-148">Selezionare **amministrazione > Gestisci articoli** tooadd alcuni articoli.</span><span class="sxs-lookup"><span data-stu-id="1b545-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="1b545-149">toostop Node.js in qualsiasi momento, premere `Ctrl+C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="1b545-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="1b545-150">Creare MongoDB di produzione</span><span class="sxs-lookup"><span data-stu-id="1b545-150">Create production MongoDB</span></span>

<span data-ttu-id="1b545-151">In questo passaggio si crea un database MongoDB in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="1b545-152">Quando l'applicazione viene distribuita tooAzure, Usa questo database cloud.</span><span class="sxs-lookup"><span data-stu-id="1b545-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="1b545-153">Per MongoDB, questa esercitazione usa [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="1b545-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="1b545-154">COSMOS DB supporta le connessioni client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b545-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="1b545-155">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b545-155">Log in tooAzure</span></span>

<span data-ttu-id="1b545-156">Si userà hello Azure CLI 2.0 toocreate hello risorse necessarie toohost l'app in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="1b545-157">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="1b545-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="1b545-158">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="1b545-158">Create a resource group</span></span>

<span data-ttu-id="1b545-159">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="1b545-160">Hello seguente viene creato un gruppo di risorse nell'area Europa occidentale hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="1b545-161">Hello utilizzare [az appservice elenco posizioni](/cli/azure/appservice#list-locations) posizioni disponibili toolist di comando CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="1b545-162">Creare un account Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1b545-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="1b545-163">Creare un account DB Cosmos con hello [cosmosdb az creare](/cli/azure/cosmosdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="1b545-164">In hello seguente comando, sostituire un nome univoco di DB Cosmos per hello  *\<cosmosdb_name >* segnaposto.</span><span class="sxs-lookup"><span data-stu-id="1b545-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="1b545-165">Questo nome viene utilizzato come parte di hello dell'endpoint Cosmos DB hello `https://<cosmosdb_name>.documents.azure.com/`, in modo che nome hello deve toobe univoco in tutti gli account DB Cosmos in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="1b545-166">nome Hello deve contenere solo lettere minuscole, numeri e caratteri di trattino (-) hello e deve essere compresa tra 3 e 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="1b545-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="1b545-167">Hello *-MongoDB kind* parametro consente le connessioni client di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b545-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="1b545-168">Quando viene creato l'account Cosmos DB hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="1b545-169">Connettere l'app tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="1b545-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="1b545-170">In questo passaggio è connettersi MEAN.js esempio database dell'applicazione toohello Cosmos DB che appena creato, utilizzando una stringa di connessione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b545-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="1b545-171">Recuperare una chiave del database hello</span><span class="sxs-lookup"><span data-stu-id="1b545-171">Retrieve hello database key</span></span>

<span data-ttu-id="1b545-172">tooconnect toohello DB Cosmos database, è necessario chiave hello del database.</span><span class="sxs-lookup"><span data-stu-id="1b545-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="1b545-173">Hello utilizzare [az cosmosdb elenco chiavi](/cli/azure/cosmosdb#list-keys) chiave primaria di comando tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="1b545-174">Hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiare il valore di hello di `primaryMasterKey`. <span data-ttu-id="1b545-176">È necessario queste informazioni nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="1b545-177">Configurare la stringa di connessione hello nell'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="1b545-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="1b545-178">Nell'archivio MEAN.js aprire _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="1b545-179">In hello `db` oggetto, aggiornare il valore di hello di `uri`:</span><span class="sxs-lookup"><span data-stu-id="1b545-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="1b545-180">Sostituire hello due  *\<cosmosdb_name >* segnaposto con il nome del database DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1b545-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="1b545-181">Sostituire hello  *\<primary_master_key >* segnaposto con chiave hello copiato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="1b545-182">Hello codice seguente viene illustrato hello `db` oggetto:</span><span class="sxs-lookup"><span data-stu-id="1b545-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="1b545-183">Hello `ssl=true` opzione è necessaria perché [DB Cosmos richiede SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="1b545-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="1b545-184">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1b545-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="1b545-185">Testare l'applicazione hello in modalità di produzione</span><span class="sxs-lookup"><span data-stu-id="1b545-185">Test hello application in production mode</span></span> 

<span data-ttu-id="1b545-186">Eseguire i seguenti script toominify e bundle di comando per l'ambiente di produzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="1b545-187">Questo processo genera file hello necessari dall'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="1b545-188">Esecuzione hello seguente stringa di comando toouse hello connessione configurata in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="1b545-189">`NODE_ENV=production`Imposta variabile di ambiente hello indicante toorun Node.js in ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="1b545-190">`node server.js`Avvia hello server Node.js con `server.js` nella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="1b545-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="1b545-191">Questo è il modo in cui l'applicazione Node.js viene caricata in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="1b545-192">Quando viene caricata l'applicazione hello, controllare toomake assicurarsi che sia in esecuzione nell'ambiente di produzione hello:</span><span class="sxs-lookup"><span data-stu-id="1b545-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="1b545-193">Passare toohttp://localhost:8443 in un browser.</span><span class="sxs-lookup"><span data-stu-id="1b545-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="1b545-194">Fare clic su **iscrizione** in hello menu superiore e creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="1b545-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="1b545-195">Se si crea un utente ha esito positivo e l'accesso, l'app sta scrivendo database DB Cosmos toohello di dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="1b545-196">In hello terminal, arrestare Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="1b545-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="1b545-197">Distribuire app tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b545-197">Deploy app tooAzure</span></span>

<span data-ttu-id="1b545-198">In questo passaggio, si distribuisce il tooAzure applicazione connessa MongoDB Node.js servizio App.</span><span class="sxs-lookup"><span data-stu-id="1b545-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="1b545-199">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="1b545-199">Create an App Service plan</span></span>

<span data-ttu-id="1b545-200">Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="1b545-201">esempio Hello crea un piano di servizio App denominato _myAppServicePlan_ utilizzando hello **libero** tariffario:</span><span class="sxs-lookup"><span data-stu-id="1b545-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="1b545-202">Quando viene creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="1b545-203">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="1b545-203">Create a web app</span></span>

<span data-ttu-id="1b545-204">Creare un'app web in hello `myAppServicePlan` il piano di servizio App con hello [az webapp creare](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="1b545-205">Consente di app web Hello è un tipo di hosting spazio toodeploy il codice e fornisce un URL per l'utente tooview hello applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="1b545-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="1b545-206">Utilizzare toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="1b545-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="1b545-207">In hello seguente comando, sostituire hello  *\<nome_app >* segnaposto con un nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="1b545-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="1b545-208">Questo nome viene utilizzato come parte di hello dell'URL predefinito hello per app web hello Nome hello deve toobe univoco tra tutte le App in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1b545-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="1b545-209">Quando hello web app è stata creata, hello Azure CLI indica toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="1b545-210">Configurare una variabile di ambiente</span><span class="sxs-lookup"><span data-stu-id="1b545-210">Configure an environment variable</span></span>

<span data-ttu-id="1b545-211">Nelle sezioni precedenti di hello dell'esercitazione, è hardcoded hello stringa di connessione database in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="1b545-212">In conformità a livello di protezione ottimale, si desidera tookeep dati sensibili fuori il repository Git.</span><span class="sxs-lookup"><span data-stu-id="1b545-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="1b545-213">Per l'app in esecuzione in Azure, si userà invece una variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="1b545-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="1b545-214">Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings aggiornare](/cli/azure/webapp/config/appsettings#update) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="1b545-215">Hello seguente esempio mostra come configurare un `MONGODB_URI` impostazione dell'app nell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="1b545-216">Sostituire hello  *\<nome_app >*,  *\<cosmosdb_name >*, e  *\<primary_master_key >* segnaposto.</span><span class="sxs-lookup"><span data-stu-id="1b545-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="1b545-217">Nel codice Node.js si accede all'impostazione dell'app con `process.env.MONGODB_URI`, esattamente come si accede a una variabile di ambiente qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="1b545-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="1b545-218">A questo punto, è possibile annullare too_config/env/production.js_ le modifiche con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="1b545-219">Aprire di nuovo _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="1b545-220">App MEAN.js predefinito hello è già configurato toouse hello `MONGODB_URI` variabile di ambiente che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1b545-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="1b545-221">Configurare la distribuzione con l'istanza Git locale</span><span class="sxs-lookup"><span data-stu-id="1b545-221">Configure local git deployment</span></span> 

<span data-ttu-id="1b545-222">Hello utilizzare [az webapp distribuzione utente set](/cli/azure/webapp/deployment/user#set) comando toocreate le credenziali per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b545-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="1b545-223">È possibile distribuire l'applicazione tooAzure servizio App, in vari modi, tra cui FTP, Git locale, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="1b545-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="1b545-224">Per FTP e Git locale, è necessario toohave un utente di distribuzione è configurata su hello server tooauthenticate la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b545-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="1b545-225">L'utente di distribuzione è a livello di account ed è diverso dall'account della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="1b545-226">È necessario solo tooconfigure questo utente di distribuzione una volta.</span><span class="sxs-lookup"><span data-stu-id="1b545-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="1b545-227">In hello seguente comando, sostituire  *\<nome utente >* e  *\<password >* con un nuovo nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="1b545-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="1b545-228">nome utente Hello deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="1b545-228">hello user name must be unique.</span></span> <span data-ttu-id="1b545-229">Hello password deve essere composta da almeno otto caratteri, con due simboli di hello seguenti tre elementi: lettere, numeri e simboli.</span><span class="sxs-lookup"><span data-stu-id="1b545-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="1b545-230">Se viene visualizzato un ` 'Conflict'. Details: 409` errore, nome utente hello di modifica.</span><span class="sxs-lookup"><span data-stu-id="1b545-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="1b545-231">Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.</span><span class="sxs-lookup"><span data-stu-id="1b545-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="1b545-232">Nome del record hello utente e password da utilizzare nei passaggi successivi quando si distribuisce l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="1b545-233">Hello utilizzare [az webapp distribuzione origine configurazione-locale-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure locale Git accesso toohello app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="1b545-234">Quando l'utente di distribuzione hello è configurato, hello CLI di Azure Mostra hello URL di distribuzione per l'app web di Azure in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="1b545-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="1b545-235">Copiare hello output da terminal hello, perché verrà usato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="1b545-236">Eseguire il push tooAzure da Git</span><span class="sxs-lookup"><span data-stu-id="1b545-236">Push tooAzure from Git</span></span>

<span data-ttu-id="1b545-237">Aggiungere un repository Git locale tooyour remoto di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="1b545-238">Push toohello Azure toodeploy remoto dell'applicazione di Node.js.</span><span class="sxs-lookup"><span data-stu-id="1b545-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="1b545-239">Verrà richiesto di password hello fornito in precedenza come parte della creazione di hello dell'utente di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="1b545-240">Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.</span><span class="sxs-lookup"><span data-stu-id="1b545-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="1b545-241">È possibile notare che viene eseguito il processo di distribuzione hello [Gulp](http://gulpjs.com/) dopo `npm install`.</span><span class="sxs-lookup"><span data-stu-id="1b545-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="1b545-242">Servizio App Gulp o Grunt attività non viene eseguito durante la distribuzione, pertanto questo repository di esempio ha due altri file nel relativo tooenable directory radice:</span><span class="sxs-lookup"><span data-stu-id="1b545-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="1b545-243">_.Deployment_ -toorun di servizio App di questo file indica `bash deploy.sh` come script di distribuzione personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="1b545-244">_Deploy.sh_ -hello script di distribuzione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1b545-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="1b545-245">Se si esamina il file hello, si noterà che l'esecuzione `gulp prod` dopo `npm install` e `bower install`.</span><span class="sxs-lookup"><span data-stu-id="1b545-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="1b545-246">È possibile utilizzare questo approccio tooadd qualsiasi tooyour passaggio distribuzione basati su Git.</span><span class="sxs-lookup"><span data-stu-id="1b545-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="1b545-247">Se si riavvia l'app Web di Azure in qualsiasi momento, il servizio app non esegue di nuovo queste attività di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b545-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="1b545-248">Sfoglia toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="1b545-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="1b545-249">Esplorare app web toohello distribuito tramite il browser.</span><span class="sxs-lookup"><span data-stu-id="1b545-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="1b545-250">Fare clic su **iscrizione** in hello menu superiore e creare un utente fittizio.</span><span class="sxs-lookup"><span data-stu-id="1b545-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="1b545-251">Se hanno esito positivo e l'applicazione hello accede automaticamente database MongoDB (DB Cosmos) di connettività toohello toohello creazione utente, quindi l'app MEAN.js in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="1b545-253">Selezionare **amministrazione > Gestisci articoli** tooadd alcuni articoli.</span><span class="sxs-lookup"><span data-stu-id="1b545-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="1b545-254">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="1b545-254">**Congratulations!**</span></span> <span data-ttu-id="1b545-255">L'app Node.js basata su dati è in esecuzione nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="1b545-256">Aggiornare il modello di dati e ridistribuire</span><span class="sxs-lookup"><span data-stu-id="1b545-256">Update data model and redeploy</span></span>

<span data-ttu-id="1b545-257">In questo passaggio si modifica hello `article` modello di dati e pubblicare il tooAzure di modifica.</span><span class="sxs-lookup"><span data-stu-id="1b545-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="1b545-258">Aggiornare il modello di dati hello</span><span class="sxs-lookup"><span data-stu-id="1b545-258">Update hello data model</span></span>

<span data-ttu-id="1b545-259">Aprire _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="1b545-260">In `ArticleSchema` aggiungere un tipo `String` denominato `comment`.</span><span class="sxs-lookup"><span data-stu-id="1b545-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="1b545-261">Al termine, il codice dello schema dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a><span data-ttu-id="1b545-262">Aggiornare il codice di articoli hello</span><span class="sxs-lookup"><span data-stu-id="1b545-262">Update hello articles code</span></span>

<span data-ttu-id="1b545-263">Aggiornare il resto di hello del `articles` codice toouse `comment`.</span><span class="sxs-lookup"><span data-stu-id="1b545-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="1b545-264">Esistono cinque file, è necessario toomodify: controller server hello e visualizzazioni client hello quattro.</span><span class="sxs-lookup"><span data-stu-id="1b545-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="1b545-265">Aprire _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="1b545-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="1b545-266">In hello `update` , aggiungere un'assegnazione di `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="1b545-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="1b545-267">Hello codice seguente viene illustrato hello completato `update` funzione:</span><span class="sxs-lookup"><span data-stu-id="1b545-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="1b545-268">Aprire _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="1b545-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="1b545-269">Sopra la chiusura di hello `</section>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:</span><span class="sxs-lookup"><span data-stu-id="1b545-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="1b545-270">Aprire _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="1b545-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="1b545-271">Sopra la chiusura di hello `</a>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:</span><span class="sxs-lookup"><span data-stu-id="1b545-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="1b545-272">Aprire _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="1b545-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="1b545-273">Inside hello `<div class="list-group">` elemento e sopra la chiusura di hello `</a>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:</span><span class="sxs-lookup"><span data-stu-id="1b545-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="1b545-274">Aprire _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="1b545-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="1b545-275">Trovare hello `<div class="form-group">` elemento che contiene il pulsante di invio hello, che ha un aspetto simile:</span><span class="sxs-lookup"><span data-stu-id="1b545-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="1b545-276">Appena sopra il tag, aggiungere un altro `<div class="form-group">` elemento che consente agli utenti di modificare hello `comment` campo.</span><span class="sxs-lookup"><span data-stu-id="1b545-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="1b545-277">Il nuovo elemento dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1b545-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="1b545-278">Testare le modifiche in locale</span><span class="sxs-lookup"><span data-stu-id="1b545-278">Test your changes locally</span></span>

<span data-ttu-id="1b545-279">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1b545-279">Save all your changes.</span></span>

<span data-ttu-id="1b545-280">Testare di nuovo le modifiche in modalità di produzione.</span><span class="sxs-lookup"><span data-stu-id="1b545-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="1b545-281">Tenere presente che il _config/env/production.js_ è stato ripristinato e hello `MONGODB_URI` variabile di ambiente viene impostata solo nell'app web di Azure e non nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="1b545-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="1b545-282">Se si esamina il file di configurazione di hello, si trova tale hello configurazione production per impostazione predefinita toouse un database locale di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b545-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="1b545-283">Ciò garantisce che non si modifichino i dati di produzione quando si testano modifiche al codice in locale.</span><span class="sxs-lookup"><span data-stu-id="1b545-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="1b545-284">Passare troppo`http://localhost:8443` in un browser e assicurarsi di avere effettuato.</span><span class="sxs-lookup"><span data-stu-id="1b545-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="1b545-285">Selezionare **amministrazione > Gestisci articoli**, quindi aggiungere un articolo selezionando hello  **+**  pulsante.</span><span class="sxs-lookup"><span data-stu-id="1b545-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="1b545-286">Hello vedere nuova `Comment` textbox ora.</span><span class="sxs-lookup"><span data-stu-id="1b545-286">You see hello new `Comment` textbox now.</span></span>

![Commento aggiunto campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="1b545-288">In hello terminal, arrestare Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="1b545-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="1b545-289">Pubblicare le modifiche tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b545-289">Publish changes tooAzure</span></span>

<span data-ttu-id="1b545-290">Eseguire il commit delle modifiche in Git, quindi eseguire il push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="1b545-291">Una volta hello `git push` è completata, passare tooyour Azure web app e provare la nuova funzionalità di hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Le modifiche apportate al modello e il database pubblicato tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="1b545-293">Eventuali articoli aggiunti in precedenza sono ancora visibili.</span><span class="sxs-lookup"><span data-stu-id="1b545-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="1b545-294">I dati esistenti in Cosmos DB non vengono persi.</span><span class="sxs-lookup"><span data-stu-id="1b545-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="1b545-295">Inoltre, lo schema di dati toohello gli aggiornamenti e lascia intatti i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="1b545-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="1b545-296">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="1b545-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="1b545-297">Durante l'esecuzione dell'applicazione di Node.js in Azure App Service, è possibile ottenere hello console registri reindirizzato tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="1b545-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="1b545-298">In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b545-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="1b545-299">log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="1b545-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="1b545-300">Una volta avviato il flusso di log, aggiornare l'app web di Azure in hello browser tooget traffico web.</span><span class="sxs-lookup"><span data-stu-id="1b545-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="1b545-301">È ora possibile visualizzare i registri di console reindirizzato tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="1b545-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="1b545-302">Arrestare il flusso dei log in qualsiasi momento digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="1b545-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="1b545-303">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-303">Manage your Azure web app</span></span>

<span data-ttu-id="1b545-304">Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1b545-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="1b545-305">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b545-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="1b545-307">Per impostazione predefinita, il portale di hello Mostra dell'app web **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="1b545-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="1b545-308">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="1b545-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="1b545-309">In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="1b545-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="1b545-310">schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello.</span><span class="sxs-lookup"><span data-stu-id="1b545-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="1b545-312">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b545-312">Next steps</span></span>

<span data-ttu-id="1b545-313">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1b545-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b545-314">Creare un database MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="1b545-315">Connettersi a un tooMongoDB app Node.js</span><span class="sxs-lookup"><span data-stu-id="1b545-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="1b545-316">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b545-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1b545-317">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1b545-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="1b545-318">Registri di flusso di Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="1b545-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="1b545-319">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b545-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="1b545-320">Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="1b545-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="1b545-321">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="1b545-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
