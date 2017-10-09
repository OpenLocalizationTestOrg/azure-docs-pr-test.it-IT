---
title: aaaConnect un tooAzure di app di MongoDB DB Cosmos utilizzando Node.js | Documenti Microsoft
description: Informazioni su come tooconnect un tooAzure di app Node.js MongoDB Cosmos DB esistente
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="23757-103">Azure Cosmos DB: Eseguire la migrazione di un'app Web MongoDB Node.js esistente</span><span class="sxs-lookup"><span data-stu-id="23757-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="23757-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23757-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="23757-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="23757-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="23757-106">Questa Guida introduttiva illustra come toouse esistente [MongoDB](mongodb-introduction.md) app scritte in Node.js e connetterla tooyour DB Cosmos Azure database, che supporta le connessioni client di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="23757-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="23757-107">In altre parole, l'applicazione di Node.js riconosce solo che viene stabilita la connessione database tooa utilizzando APIs MongoDB.</span><span class="sxs-lookup"><span data-stu-id="23757-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="23757-108">È trasparente toohello applicazione hello dati viene archiviato nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23757-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="23757-109">Al termine, si avrà un'applicazione MEAN (MongoDB, Express, AngularJS e Node.js) in esecuzione in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="23757-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="23757-111">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="23757-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="23757-112">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="23757-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="23757-113">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23757-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="23757-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="23757-114">Prerequisites</span></span> 
<span data-ttu-id="23757-115">Inoltre tooAzure CLI, è necessario [Node.js](https://nodejs.org/) e [Git](http://www.git-scm.com/downloads) installato localmente toorun `npm` e `git` comandi.</span><span class="sxs-lookup"><span data-stu-id="23757-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="23757-116">È necessario saper usare Node.js.</span><span class="sxs-lookup"><span data-stu-id="23757-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="23757-117">Questa Guida rapida non è previsto toohelp si con lo sviluppo di applicazioni Node.js in generale.</span><span class="sxs-lookup"><span data-stu-id="23757-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="23757-118">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="23757-118">Clone hello sample application</span></span>

<span data-ttu-id="23757-119">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="23757-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="23757-120">Eseguire hello repository di esempio hello tooclone i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="23757-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="23757-121">Il repository di esempio contiene predefinito hello [MEAN.js](http://meanjs.org/) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23757-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="23757-122">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="23757-122">Run hello application</span></span>

<span data-ttu-id="23757-123">Installare i pacchetti hello necessarie e avviare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23757-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="23757-124">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="23757-124">Log in tooAzure</span></span>

<span data-ttu-id="23757-125">Se si utilizza un installato CLI di Azure, accedere tooyour sottoscrizione di Azure con hello [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="23757-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="23757-126">È possibile ignorare questo passaggio se si usa hello Shell di Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="23757-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="23757-127">Aggiungere il modulo di Azure Cosmos DB hello</span><span class="sxs-lookup"><span data-stu-id="23757-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="23757-128">Se si utilizza un installato CLI di Azure, verificare toosee se hello `cosmosdb` componente è già installato eseguendo hello `az` comando.</span><span class="sxs-lookup"><span data-stu-id="23757-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="23757-129">Se `cosmosdb` è hello elenco di comandi di base, procedere toohello del comando successivo.</span><span class="sxs-lookup"><span data-stu-id="23757-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="23757-130">È possibile ignorare questo passaggio se si usa hello Shell di Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="23757-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="23757-131">Se `cosmosdb` non è in elenco di comandi di base di hello, reinstallare [CLI di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23757-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="23757-132">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="23757-132">Create a resource group</span></span>

<span data-ttu-id="23757-133">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="23757-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="23757-134">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="23757-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="23757-135">Hello seguente viene creato un gruppo di risorse nell'area Europa occidentale hello.</span><span class="sxs-lookup"><span data-stu-id="23757-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="23757-136">Scegliere un nome univoco per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="23757-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="23757-137">Se si utilizza una Shell di Cloud di Azure, fare clic su **Provalo**, seguire hello istruzioni visualizzate toologin, quindi copiare il comando di hello nel prompt dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="23757-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="23757-138">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="23757-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="23757-139">Creare un account Azure Cosmos DB con hello [cosmosdb az creare](/cli/azure/cosmosdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="23757-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="23757-140">In hello seguente comando, sostituire il proprio nome di account Azure Cosmos DB univoco in cui si vedere hello `<cosmosdb-name>` segnaposto.</span><span class="sxs-lookup"><span data-stu-id="23757-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="23757-141">Questo nome univoco da utilizzare come parte dell'endpoint Azure Cosmos DB (`https://<cosmosdb-name>.documents.azure.com/`), in modo che nome hello deve toobe univoco in tutti gli account di Azure Cosmos DB in Azure.</span><span class="sxs-lookup"><span data-stu-id="23757-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="23757-142">Hello `--kind MongoDB` parametro consente le connessioni client di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="23757-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="23757-143">Quando viene creato l'account di Azure Cosmos DB hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="23757-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="23757-144">In questo esempio utilizza JSON come formato di output di hello CLI di Azure, hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="23757-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="23757-145">toouse output di un altro formato, vedere [Output formati per i comandi CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23757-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="23757-146">Connettere il database dell'applicazione toohello di Node.js</span><span class="sxs-lookup"><span data-stu-id="23757-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="23757-147">In questo passaggio è connettersi MEAN.js esempio database dell'applicazione tooan DB Cosmos Azure che appena creato, utilizzando una stringa di connessione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="23757-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="23757-148">Configurare la stringa di connessione hello nell'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="23757-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="23757-149">Nel repository di MEAN.js aprire `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="23757-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="23757-150">Sostituire il contenuto di hello del file con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="23757-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="23757-151">Assicurarsi di tooalso sostituire hello due `<cosmosdb-name>` segnaposto con il nome dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="23757-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="23757-152">Recuperare la chiave hello</span><span class="sxs-lookup"><span data-stu-id="23757-152">Retrieve hello key</span></span>

<span data-ttu-id="23757-153">Nel database di Azure Cosmos DB tooan tooconnect ordine, è necessario chiave hello del database.</span><span class="sxs-lookup"><span data-stu-id="23757-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="23757-154">Hello utilizzare [az cosmosdb elenco chiavi](/cli/azure/cosmosdb#list-keys) chiave primaria di comando tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="23757-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="23757-155">Hello CLI di Azure genera informazioni toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="23757-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="23757-156">Copiare il valore di hello di `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="23757-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="23757-157">Incollare questo hello `<primary_master_key>` in `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="23757-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="23757-158">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="23757-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="23757-159">Eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23757-159">Run hello application again.</span></span>

<span data-ttu-id="23757-160">Eseguire di nuovo `npm start`.</span><span class="sxs-lookup"><span data-stu-id="23757-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="23757-161">Un messaggio di console dovrebbero ora essere che tale ambiente di sviluppo hello sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="23757-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="23757-162">Passare troppo`http://localhost:3000` in un browser.</span><span class="sxs-lookup"><span data-stu-id="23757-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="23757-163">Fare clic su **iscrizione** in toocreate menu e riprovare superiore hello due fittizio gli utenti.</span><span class="sxs-lookup"><span data-stu-id="23757-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="23757-164">applicazione di esempio MEAN.js Hello archivia i dati utente nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="23757-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="23757-165">Se hanno esito positivo e MEAN.js accede automaticamente a hello creato utente, quindi la connessione di database di Azure Cosmos funziona.</span><span class="sxs-lookup"><span data-stu-id="23757-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js si connette correttamente tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="23757-167">Visualizzare i dati in Esplora dati</span><span class="sxs-lookup"><span data-stu-id="23757-167">View data in Data Explorer</span></span>

<span data-ttu-id="23757-168">Dati archiviati da un database di Azure Cosmos sono tooview disponibili, query e esecuzione della logica di business nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23757-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="23757-169">tooview, eseguire una query e utilizzare i dati utente hello creati nel passaggio precedente hello, account di accesso toohello [portale di Azure](https://portal.azure.com) nel web browser.</span><span class="sxs-lookup"><span data-stu-id="23757-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="23757-170">Nella casella di ricerca superiore hello, digitare Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="23757-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="23757-171">Quando il pannello dell'account Cosmos DB si apre, selezionare l'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="23757-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="23757-172">Nel riquadro di spostamento sinistro di hello, fare clic su Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="23757-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="23757-173">Espandere la raccolta nel riquadro raccolte hello e quindi è possibile visualizzare documenti hello nella raccolta di hello, eseguire query sui dati, hello e anche creare ed eseguire le stored procedure, trigger e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="23757-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Esplora dati in hello portale di Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="23757-175">Distribuire hello Node.js applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="23757-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="23757-176">In questo passaggio, si distribuisce il tooAzure applicazione connessa MongoDB Node.js DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23757-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="23757-177">Si è notato che file di configurazione hello che è stato modificato in precedenza è per l'ambiente di sviluppo hello (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="23757-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="23757-178">Quando si distribuisce il tooApp di applicazione del servizio, verrà eseguito in ambiente di produzione hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="23757-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="23757-179">A questo punto, è necessario toomake hello stesso modifica il file di configurazione corrispondente di toohello.</span><span class="sxs-lookup"><span data-stu-id="23757-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="23757-180">Nel repository di MEAN.js aprire `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="23757-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="23757-181">In hello `db` oggetto, sostituire il valore di hello di `uri` come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="23757-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="23757-182">Impossibile verificare segnaposto tooreplace hello come prima.</span><span class="sxs-lookup"><span data-stu-id="23757-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="23757-183">Hello `ssl=true` opzione è importante perché [DB Cosmos Azure richiede SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="23757-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="23757-184">In hello terminal, eseguire il commit di tutte le modifiche in Git.</span><span class="sxs-lookup"><span data-stu-id="23757-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="23757-185">È possibile copiare entrambi toorun comandi insieme.</span><span class="sxs-lookup"><span data-stu-id="23757-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="23757-186">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="23757-186">Clean up resources</span></span>

<span data-ttu-id="23757-187">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="23757-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="23757-188">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="23757-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="23757-189">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="23757-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23757-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23757-190">Next steps</span></span>

<span data-ttu-id="23757-191">In questa Guida rapida, si è appreso come un database di Azure Cosmos toocreate account e creare un insieme di MongoDB mediante Esplora dati hello.</span><span class="sxs-lookup"><span data-stu-id="23757-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="23757-192">È ora possibile eseguire la migrazione il tooAzure dati MongoDB DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23757-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="23757-193">Importare i dati di MongoDB in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="23757-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
