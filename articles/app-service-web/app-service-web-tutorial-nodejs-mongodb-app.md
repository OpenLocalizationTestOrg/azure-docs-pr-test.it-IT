---
title: Creare un'app Web Node.js e MongoDB in Azure | Microsoft Docs
description: Informazioni su come usare un'app Node.js in Azure, con connessione a un database Cosmos DB tramite una stringa di connessione MongoDB.
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
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="f4f3f-103">Creare un'app Web Node.js e MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="f4f3f-104">Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f4f3f-105">Questa esercitazione illustra come creare un'app Web Node.js in Azure e connetterla a un database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="f4f3f-106">Al termine, si avrà un'applicazione MEAN (MongoDB, Express, AngularJS e Node.js) in esecuzione nel [servizio app di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="f4f3f-107">Per semplicità, l'applicazione di esempio usa il [framework Web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="f4f3f-109">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4f3f-110">Creare un database MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="f4f3f-111">Connettere un'app Node.js a MongoDB</span><span class="sxs-lookup"><span data-stu-id="f4f3f-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="f4f3f-112">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f4f3f-113">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="f4f3f-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f4f3f-114">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f4f3f-115">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4f3f-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f4f3f-116">Prerequisites</span></span>

<span data-ttu-id="f4f3f-117">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="f4f3f-118">Installare Git</span><span class="sxs-lookup"><span data-stu-id="f4f3f-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="f4f3f-119">Installare Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="f4f3f-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="f4f3f-120">[Installare Gulp.js](http://gulpjs.com/), richiesto da [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started)</span><span class="sxs-lookup"><span data-stu-id="f4f3f-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="f4f3f-121">Installare ed eseguire MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="f4f3f-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f4f3f-122">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f4f3f-123">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="f4f3f-124">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="f4f3f-125">Testare il MongoDB locale</span><span class="sxs-lookup"><span data-stu-id="f4f3f-125">Test local MongoDB</span></span>

<span data-ttu-id="f4f3f-126">Aprire la finestra del terminale e usare il comando `cd` per passare alla directory `bin` dell'installazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="f4f3f-127">È possibile usare questa finestra del terminale per eseguire tutti i comandi presenti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="f4f3f-128">Eseguire `mongo` nel terminale per connettersi al server MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="f4f3f-129">Se la connessione ha esito positivo significa che il database MongoDB è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="f4f3f-130">In caso contrario, assicurarsi che il database MongoDB locale venga avviato seguendo la procedura descritta in [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) (Installare MongoDB Community Edition).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="f4f3f-131">Spesso, anche se MongoDB è stato installato, è necessario avviare il servizio eseguendo `mongod`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="f4f3f-132">Dopo avere testato il database MongoDB, digitare `Ctrl+C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="f4f3f-133">Creare l'app Node.js locale</span><span class="sxs-lookup"><span data-stu-id="f4f3f-133">Create local Node.js app</span></span>

<span data-ttu-id="f4f3f-134">In questo passaggio si imposta il progetto Node.js locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="f4f3f-135">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="f4f3f-135">Clone the sample application</span></span>

<span data-ttu-id="f4f3f-136">Nella finestra del terminale usare il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="f4f3f-137">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="f4f3f-138">Questo repository contiene una copia del [repository MEAN.js](https://github.com/meanjs/mean),</span><span class="sxs-lookup"><span data-stu-id="f4f3f-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="f4f3f-139">che è stato modificato per poter essere eseguito nel servizio app. Per altre informazioni, vedere il [file LEGGIMI](https://github.com/Azure-Samples/meanjs/blob/master/README.md) del repository MEAN.js.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="f4f3f-140">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="f4f3f-140">Run the application</span></span>

<span data-ttu-id="f4f3f-141">Eseguire i comandi seguenti per installare i pacchetti necessari e avviare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="f4f3f-142">Al termine del caricamento dell'app viene visualizzato un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-142">When the app is fully loaded, you see something similar to the following message:</span></span>

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

<span data-ttu-id="f4f3f-143">Passare a http://localhost:3000 in un browser.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="f4f3f-144">Fare clic su **Iscriviti** nel menu in alto e creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="f4f3f-145">L'applicazione di esempio MEAN.js archivia i dati utente nel database.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="f4f3f-146">Dopo aver creato un utente e aver eseguito l'accesso, l'app scriverà i dati nel database MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js si connette correttamente a MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="f4f3f-148">Selezionare **Admin > Manage Articles** (Amministrazione > Gestione articoli) per aggiungere articoli.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="f4f3f-149">Per arrestare Node.js in qualsiasi momento, premere `Ctrl+C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="f4f3f-150">Creare MongoDB di produzione</span><span class="sxs-lookup"><span data-stu-id="f4f3f-150">Create production MongoDB</span></span>

<span data-ttu-id="f4f3f-151">In questo passaggio si crea un database MongoDB in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="f4f3f-152">Quando viene distribuita in Azure, l'app usa questo database basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="f4f3f-153">Per MongoDB, questa esercitazione usa [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="f4f3f-154">COSMOS DB supporta le connessioni client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f4f3f-155">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-155">Log in to Azure</span></span>

<span data-ttu-id="f4f3f-156">Usare l'interfaccia della riga di comando di Azure 2.0 per creare le risorse necessarie per ospitare l'app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="f4f3f-157">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="f4f3f-158">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f4f3f-158">Create a resource group</span></span>

<span data-ttu-id="f4f3f-159">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="f4f3f-160">L'esempio seguente crea un gruppo di risorse nell'area Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="f4f3f-161">Usare il comando dell'interfaccia della riga di comando di Azure [az appservice list-locations](/cli/azure/appservice#list-locations) per visualizzare un elenco dei percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="f4f3f-162">Creare un account Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f4f3f-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="f4f3f-163">Creare un account Cosmos DB con il comando [az cosmosdb create](/cli/azure/cosmosdb#create).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="f4f3f-164">Nel comando seguente sostituire il segnaposto *\<cosmosdb_name>* con un nome Cosmos DB univoco.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="f4f3f-165">Poiché questo nome è incluso nell'endpoint Cosmos DB, `https://<cosmosdb_name>.documents.azure.com/`, è necessario che sia univoco in tutti gli account Cosmos DB in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="f4f3f-166">Il nome deve contenere solo lettere minuscole, numeri e il carattere (-) e deve avere una lunghezza compresa tra 3 e 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="f4f3f-167">Il parametro *--kind MongoDB* abilita le connessioni client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="f4f3f-168">Dopo la creazione dell'account Cosmos DB, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="f4f3f-169">Connettere l'app a MongoDB di produzione</span><span class="sxs-lookup"><span data-stu-id="f4f3f-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="f4f3f-170">In questo passaggio si usa una stringa di connessione MongoDB per connettere l'applicazione di esempio MEAN.js al database Cosmos DB appena creato.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="f4f3f-171">Recuperare la chiave del database</span><span class="sxs-lookup"><span data-stu-id="f4f3f-171">Retrieve the database key</span></span>

<span data-ttu-id="f4f3f-172">Per connettersi al database Cosmos DB, è necessario disporre della chiave database.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="f4f3f-173">Usare il comando [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) per recuperare la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="f4f3f-174">L'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiare il valore di `primaryMasterKey`. <span data-ttu-id="f4f3f-176">Queste informazioni saranno necessarie durante il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="f4f3f-177">Configurare la stringa di connessione nell'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="f4f3f-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="f4f3f-178">Nell'archivio MEAN.js aprire _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="f4f3f-179">Nell'oggetto `db` aggiornare il valore di `uri`:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="f4f3f-180">Sostituire i due segnaposto *\<cosmosdb_name>* con il nome del database Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="f4f3f-181">Sostituire il segnaposto *\<primary_master_key>* con la chiave copiata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="f4f3f-182">Il codice seguente mostra l'oggetto `db`:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="f4f3f-183">L'opzione `ssl=true` è obbligatoria poiché [Cosmos DB richiede l'SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="f4f3f-184">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="f4f3f-185">Testare l'applicazione nella modalità di produzione</span><span class="sxs-lookup"><span data-stu-id="f4f3f-185">Test the application in production mode</span></span> 

<span data-ttu-id="f4f3f-186">Eseguire il comando seguente per minimizzare e aggregare gli script per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="f4f3f-187">Questo processo genera i file necessari per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="f4f3f-188">Eseguire il comando seguente per usare la stringa di connessione configurata in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="f4f3f-189">`NODE_ENV=production` imposta la variabile di ambiente che richiede a Node.js l'esecuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="f4f3f-190">`node server.js` avvia il server Node.js con `server.js` nella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="f4f3f-191">Questo è il modo in cui l'applicazione Node.js viene caricata in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="f4f3f-192">Dopo aver caricato l'app, verificare che sia in esecuzione nell'ambiente di produzione:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="f4f3f-193">Passare a http://localhost:8443 in un browser.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="f4f3f-194">Fare clic su **Iscriviti** nel menu in alto e creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="f4f3f-195">Dopo aver creato un utente e aver eseguito l'accesso, l'app scriverà i dati nel database Cosmos DB in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="f4f3f-196">Nel terminale arrestare Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="f4f3f-197">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-197">Deploy app to Azure</span></span>

<span data-ttu-id="f4f3f-198">In questo passaggio si distribuisce l'applicazione Node.js connessa a MongoDB nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="f4f3f-199">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="f4f3f-199">Create an App Service plan</span></span>

<span data-ttu-id="f4f3f-200">Creare un piano di servizio app con il comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="f4f3f-201">L'esempio seguente crea un piano di servizio app denominato _myAppServicePlan_ usando il piano tariffario **GRATUITO**:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="f4f3f-202">Al termine della creazione del piano di servizio app, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="f4f3f-203">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="f4f3f-203">Create a web app</span></span>

<span data-ttu-id="f4f3f-204">Creare un'app Web nel piano di servizio app `myAppServicePlan` con il comando [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="f4f3f-205">L'app Web fornisce uno spazio host per distribuire il codice e un URL in cui visualizzare l'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="f4f3f-206">Usarlo per creare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-206">Use  to create the web app.</span></span> 

<span data-ttu-id="f4f3f-207">Nel comando seguente sostituire il segnaposto *\<app_name>* con un nome di app univoco.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="f4f3f-208">Poiché questo nome è incluso nell'URL predefinito dell'app Web, è necessario che sia univoco in tutte le app del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="f4f3f-209">Al termine della creazione dell'app Web, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="f4f3f-210">Configurare una variabile di ambiente</span><span class="sxs-lookup"><span data-stu-id="f4f3f-210">Configure an environment variable</span></span>

<span data-ttu-id="f4f3f-211">In una fase precedente dell'esercitazione è stata impostata come hardcoded la stringa di connessione al database in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="f4f3f-212">In linea con la procedura consigliata per la sicurezza, si intende mantenere i dati sensibili all'esterno del repository Git.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="f4f3f-213">Per l'app in esecuzione in Azure, si userà invece una variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="f4f3f-214">Nel servizio app le variabili di ambiente vengono impostate come _impostazioni dell'app_ usando il comando [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="f4f3f-215">L'esempio seguente configura l'impostazione dell'app `MONGODB_URI` nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="f4f3f-216">Sostituire i segnaposto *\<app_name>*, *\<cosmosdb_name>* e *\<primary_master_key>*.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="f4f3f-217">Nel codice Node.js si accede all'impostazione dell'app con `process.env.MONGODB_URI`, esattamente come si accede a una variabile di ambiente qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="f4f3f-218">Annullare a questo punto le modifiche a _config/env/production.js_ usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="f4f3f-219">Aprire di nuovo _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="f4f3f-220">Si noti che l'app MEAN.js predefinita è già configurata per l'uso della variabile di ambiente `MONGODB_URI` creata.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="f4f3f-221">Configurare la distribuzione con l'istanza Git locale</span><span class="sxs-lookup"><span data-stu-id="f4f3f-221">Configure local git deployment</span></span> 

<span data-ttu-id="f4f3f-222">Usare il comando [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) per creare le credenziali per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="f4f3f-223">È possibile distribuire l'applicazione nel Servizio app di Azure attraverso varie soluzioni, tra cui FTP, istanza Git locale, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="f4f3f-224">Per la distribuzione con FTP e l'istanza Git locale, è necessario che nel server sia configurato un utente della distribuzione per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="f4f3f-225">L'utente di distribuzione è a livello di account ed è diverso dall'account della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="f4f3f-226">L'utente della distribuzione deve essere configurato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="f4f3f-227">Nel comando seguente sostituire *\<user-name>* e *\<password>* con un nuovo nome utente e una nuova password.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="f4f3f-228">Il nome utente deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-228">The user name must be unique.</span></span> <span data-ttu-id="f4f3f-229">La password deve essere composta da almeno otto caratteri, con due dei tre elementi seguenti: lettere, numeri e simboli.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="f4f3f-230">Se viene visualizzato un errore ` 'Conflict'. Details: 409`, modificare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="f4f3f-231">Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="f4f3f-232">Registrare nome utente e password da usare nei passaggi successivi durante la distribuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="f4f3f-233">Usare il comando [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) per configurare l'accesso Git locale all'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="f4f3f-234">Dopo che l'utente della distribuzione è stato configurato, l'interfaccia della riga di comando di Azure visualizza l'URL della distribuzione per l'app Web di Azure nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="f4f3f-235">Copiare l'output dal terminale che verrà usato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="f4f3f-236">Effettuare il push in Azure da Git</span><span class="sxs-lookup"><span data-stu-id="f4f3f-236">Push to Azure from Git</span></span>

<span data-ttu-id="f4f3f-237">Aggiungere un'istanza remota di Azure al repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="f4f3f-238">Effettuare il push all'istanza remota di Azure per distribuire l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="f4f3f-239">Verrà richiesta la password specificata in precedenza nel corso della creazione dell'utente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="f4f3f-240">Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="f4f3f-241">Il processo di distribuzione esegue [Gulp](http://gulpjs.com/) dopo `npm install`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="f4f3f-242">Il servizio app non esegue attività Gulp o Grunt durante la distribuzione, pertanto questo repository di esempio include due file aggiuntivi nella directory radice per abilitarlo:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="f4f3f-243">_.deployment_: questo file indica al servizio app di eseguire `bash deploy.sh` come script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="f4f3f-244">_deploy.sh_: script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="f4f3f-245">Se si esamina il file, si noterà che esegue `gulp prod` dopo `npm install` e `bower install`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="f4f3f-246">È possibile usare questo approccio per aggiungere uno o più passaggi alla distribuzione basata su Git.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="f4f3f-247">Se si riavvia l'app Web di Azure in qualsiasi momento, il servizio app non esegue di nuovo queste attività di automazione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="f4f3f-248">Passare all'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="f4f3f-249">Passare all'app Web distribuita usando il Web browser.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="f4f3f-250">Fare clic su **Registrati** nel menu in alto e creare un utente fittizio.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="f4f3f-251">Se l'operazione ha esito positivo e l'app accede automaticamente all'utente creato, l'app MEAN.js in Azure sarà connessa al database MongoDB, ovvero Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="f4f3f-253">Selezionare **Admin > Manage Articles** (Amministrazione > Gestione articoli) per aggiungere articoli.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="f4f3f-254">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="f4f3f-254">**Congratulations!**</span></span> <span data-ttu-id="f4f3f-255">L'app Node.js basata su dati è in esecuzione nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="f4f3f-256">Aggiornare il modello di dati e ridistribuire</span><span class="sxs-lookup"><span data-stu-id="f4f3f-256">Update data model and redeploy</span></span>

<span data-ttu-id="f4f3f-257">In questo passaggio viene modificato il modello di dati `article` e viene pubblicata la modifica in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="f4f3f-258">Aggiornare il modello di dati</span><span class="sxs-lookup"><span data-stu-id="f4f3f-258">Update the data model</span></span>

<span data-ttu-id="f4f3f-259">Aprire _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="f4f3f-260">In `ArticleSchema` aggiungere un tipo `String` denominato `comment`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="f4f3f-261">Al termine, il codice dello schema dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-the-articles-code"></a><span data-ttu-id="f4f3f-262">Aggiornare il codice di articoli</span><span class="sxs-lookup"><span data-stu-id="f4f3f-262">Update the articles code</span></span>

<span data-ttu-id="f4f3f-263">Aggiornare la parte rimanente del codice `articles` per usare `comment`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="f4f3f-264">È necessario modificare cinque file: il controller server e le quattro visualizzazioni client.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="f4f3f-265">Aprire _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="f4f3f-266">Nella funzione `update` aggiungere un'assegnazione per `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="f4f3f-267">Il codice seguente mostra la funzione `update` completata:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="f4f3f-268">Aprire _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="f4f3f-269">Appena sopra il tag di chiusura `</section>` aggiungere la riga seguente per visualizzare `comment` insieme al resto dei dati dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="f4f3f-270">Aprire _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="f4f3f-271">Appena sopra il tag di chiusura `</a>` aggiungere la riga seguente per visualizzare `comment` insieme al resto dei dati dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="f4f3f-272">Aprire _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="f4f3f-273">Nell'elemento `<div class="list-group">` sopra il tag di chiusura `</a>` aggiungere la riga seguente per visualizzare `comment` con la parte rimanente dei dati dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="f4f3f-274">Aprire _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="f4f3f-275">Trovare l'elemento `<div class="form-group">` che contiene un pulsante di invio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="f4f3f-276">Sopra il tag aggiungere un altro elemento `<div class="form-group">` che consente agli utenti di modificare il campo `comment`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="f4f3f-277">Il nuovo elemento dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="f4f3f-278">Testare le modifiche in locale</span><span class="sxs-lookup"><span data-stu-id="f4f3f-278">Test your changes locally</span></span>

<span data-ttu-id="f4f3f-279">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-279">Save all your changes.</span></span>

<span data-ttu-id="f4f3f-280">Testare di nuovo le modifiche in modalità di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="f4f3f-281">Tenere presente che _config/env/production.js_ è stato ripristinato e che la variabile di ambiente `MONGODB_URI` è impostata solo nell'app Web di Azure e non nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="f4f3f-282">Se si esamina il file di configurazione, si noterà che la configurazione di produzione usa per impostazione predefinita un database MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="f4f3f-283">Ciò garantisce che non si modifichino i dati di produzione quando si testano modifiche al codice in locale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="f4f3f-284">Andare a `http://localhost:8443` in un browser e assicurarsi di avere eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="f4f3f-285">Selezionare **Admin > Manage Articles** (Admin > Gestione articoli), quindi aggiungere un articolo selezionando il pulsante **+**.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="f4f3f-286">La nuova casella di testo `Comment` è ora visibile.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-286">You see the new `Comment` textbox now.</span></span>

![Campo di commento aggiunto ad Articles (Articoli)](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="f4f3f-288">Nel terminale arrestare Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="f4f3f-289">Pubblicare le modifiche in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-289">Publish changes to Azure</span></span>

<span data-ttu-id="f4f3f-290">Eseguire il commit delle modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="f4f3f-291">Dopo aver completato `git push`, passare all'app Web di Azure e provare la nuova funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Modifiche al modello e al database pubblicate in Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="f4f3f-293">Eventuali articoli aggiunti in precedenza sono ancora visibili.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="f4f3f-294">I dati esistenti in Cosmos DB non vengono persi.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="f4f3f-295">Gli aggiornamenti allo schema di dati inoltre lasciano intatti i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="f4f3f-296">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="f4f3f-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="f4f3f-297">Mentre l'applicazione Node.js è in esecuzione nel servizio app di Azure, è possibile fare in modo che i log di console siano inviati tramite pipe al terminale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="f4f3f-298">Ciò consente di ottenere gli stessi messaggi di diagnostica per il debug degli errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="f4f3f-299">Per avviare lo streaming dei log, usare il comando [az webapp log tail](/cli/azure/webapp/log#tail).</span><span class="sxs-lookup"><span data-stu-id="f4f3f-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="f4f3f-300">Dopo avere avviato lo streaming del log, aggiornare l'app Web di Azure nel browser per ottenere traffico Web.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="f4f3f-301">I log di console vengono inviati tramite pipe al terminale.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="f4f3f-302">Arrestare il flusso dei log in qualsiasi momento digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="f4f3f-303">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-303">Manage your Azure web app</span></span>

<span data-ttu-id="f4f3f-304">Accedere al [portale di Azure](https://portal.azure.com) per visualizzare l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="f4f3f-305">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="f4f3f-307">Per impostazione predefinita, il portale visualizza la pagina **Panoramica** dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="f4f3f-308">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="f4f3f-309">In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="f4f3f-310">Le schede sul lato sinistro della pagina mostrano le diverse pagine di configurazione che è possibile aprire.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="f4f3f-312">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4f3f-312">Next steps</span></span>

<span data-ttu-id="f4f3f-313">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="f4f3f-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4f3f-314">Creare un database MongoDB in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="f4f3f-315">Connettere un'app Node.js a MongoDB</span><span class="sxs-lookup"><span data-stu-id="f4f3f-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="f4f3f-316">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f4f3f-317">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="f4f3f-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f4f3f-318">Eseguire lo streaming dei log da Azure al terminale</span><span class="sxs-lookup"><span data-stu-id="f4f3f-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="f4f3f-319">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="f4f3f-320">Passare all'esercitazione successiva per apprendere come eseguire il mapping di un nome DNS personalizzato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="f4f3f-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="f4f3f-321">Eseguire il mapping di un nome DNS personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f4f3f-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
