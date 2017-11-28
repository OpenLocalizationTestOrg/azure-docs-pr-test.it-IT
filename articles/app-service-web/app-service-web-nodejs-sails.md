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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="82d99-104">Distribuire un tooAzure di app web Sails.js servizio App</span><span class="sxs-lookup"><span data-stu-id="82d99-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="82d99-105">In questa esercitazione illustra come toodeploy un tooAzure app Sails.js servizio App.</span><span class="sxs-lookup"><span data-stu-id="82d99-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="82d99-106">Nel processo di hello, è possibile raccogliere alcune informazioni generali su come tooconfigure il toorun app Node.js nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="82d99-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="82d99-107">Questa esercitazione illustra alcune operazioni utili, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="82d99-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="82d99-108">Configurare l'esecuzione di un'app Sails.js nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="82d99-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="82d99-109">Distribuire un servizio di tooApp app dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="82d99-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="82d99-110">Stdout e stderr di lettura log tootroubleshoot eventuali problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="82d99-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="82d99-111">Archiviare le variabili di ambiente al di fuori del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="82d99-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="82d99-112">Accedere alle variabili di ambiente di Azure dall'app.</span><span class="sxs-lookup"><span data-stu-id="82d99-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="82d99-113">Connettersi a database tooa (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="82d99-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="82d99-114">Avere una conoscenza pratica di Sails.js.</span><span class="sxs-lookup"><span data-stu-id="82d99-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="82d99-115">In questa esercitazione non è previsto toohelp i problemi correlati toorunning Sail.js in generale.</span><span class="sxs-lookup"><span data-stu-id="82d99-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="82d99-116">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="82d99-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="82d99-117">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="82d99-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="82d99-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="82d99-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="82d99-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="82d99-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82d99-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="82d99-120">Prerequisites</span></span>
* [<span data-ttu-id="82d99-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="82d99-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="82d99-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="82d99-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="82d99-123">Git</span><span class="sxs-lookup"><span data-stu-id="82d99-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="82d99-124">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="82d99-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="82d99-125">Un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82d99-125">A Microsoft Azure account.</span></span> <span data-ttu-id="82d99-126">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="82d99-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="82d99-127">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="82d99-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="82d99-128">Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.</span><span class="sxs-lookup"><span data-stu-id="82d99-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="82d99-129">Passaggio 1: Creare e configurare un'app Sails.js in locale</span><span class="sxs-lookup"><span data-stu-id="82d99-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="82d99-130">Innanzitutto, creare rapidamente un'app Sails.js predefinita nell'ambiente di sviluppo attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="82d99-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="82d99-131">Terminal della riga di comando di hello aperto di propria scelta e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="82d99-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="82d99-132">Creare un'app Sails.js ed eseguirla:</span><span class="sxs-lookup"><span data-stu-id="82d99-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="82d99-133">Verificare che è possibile passare una home page predefinita toohello in http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="82d99-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="82d99-134">Abilitare quindi la registrazione per Azure.</span><span class="sxs-lookup"><span data-stu-id="82d99-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="82d99-135">Nella directory radice, creare un file denominato `iisnode.yml` e aggiungere hello due righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="82d99-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="82d99-136">La registrazione è ora abilitata per hello [iisnode](https://github.com/tjanczuk/iisnode) che Azure App Service utilizza App Node.js toorun server.</span><span class="sxs-lookup"><span data-stu-id="82d99-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="82d99-137">Per ulteriori informazioni sul funzionamento, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="82d99-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="82d99-138">A questo punto, configurare le variabili di ambiente Azure toouse di hello Sails.js app.</span><span class="sxs-lookup"><span data-stu-id="82d99-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="82d99-139">Aprire config/env/production.js tooconfigure nell'ambiente di produzione e impostare `port` e `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="82d99-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="82d99-140">La documentazione di queste impostazioni di configurazione è disponibile nella [Documentazione di Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="82d99-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="82d99-141">Successivamente, impostare come hardcoded hello Node.js versione toouse.</span><span class="sxs-lookup"><span data-stu-id="82d99-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="82d99-142">Nel file package. JSON, aggiungere hello seguenti `engines` proprietà tooset hello Node.js versione tooone che si desidera.</span><span class="sxs-lookup"><span data-stu-id="82d99-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="82d99-143">Inizializzare infine un repository Git ed eseguire il commit dei file.</span><span class="sxs-lookup"><span data-stu-id="82d99-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="82d99-144">In hello radice dell'applicazione (in cui è package. JSON), eseguire hello Git comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="82d99-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="82d99-145">Il codice è pronto toobe distribuito.</span><span class="sxs-lookup"><span data-stu-id="82d99-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="82d99-146">Passaggio 2: Creare un'app Azure e distribuire Sails.js</span><span class="sxs-lookup"><span data-stu-id="82d99-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="82d99-147">Successivamente, creare hello risorsa del servizio App in Azure e distribuire il tooit app Sails.js.</span><span class="sxs-lookup"><span data-stu-id="82d99-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="82d99-148">Accedi tooAzure nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="82d99-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="82d99-149">Seguire l'account di accesso di hello toocontinue prompt hello in un browser con un account Microsoft con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="82d99-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="82d99-150">Utente di distribuzione hello per servizio App.</span><span class="sxs-lookup"><span data-stu-id="82d99-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="82d99-151">Si distribuirà il codice usando queste credenziali in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="82d99-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="82d99-152">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con un nome.</span><span class="sxs-lookup"><span data-stu-id="82d99-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="82d99-153">Per questa esercitazione Node.js, non è necessario tooknow che cos'è.</span><span class="sxs-lookup"><span data-stu-id="82d99-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="82d99-154">toosee i possibili valori da utilizzare per `<location>`, utilizzare hello `az appservice list-locations` comando CLI.</span><span class="sxs-lookup"><span data-stu-id="82d99-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="82d99-155">Creare un [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" con un nome.</span><span class="sxs-lookup"><span data-stu-id="82d99-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="82d99-156">Per questa esercitazione su Node.js, è sufficiente sapere che non sono previsti costi per le app Web in questo piano.</span><span class="sxs-lookup"><span data-stu-id="82d99-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="82d99-157">Creare una nuova app Web con un nome univoco in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="82d99-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="82d99-158">Passaggio 3: Configurare e distribuire l'app Sails.js</span><span class="sxs-lookup"><span data-stu-id="82d99-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="82d99-159">Configurare la distribuzione Git locale per la nuova app web con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82d99-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="82d99-160">Si otterrà un output JSON come questo, che è stato configurato il repository Git remoto hello:</span><span class="sxs-lookup"><span data-stu-id="82d99-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="82d99-161">Aggiungere URL hello in hello JSON come un Git remoto per il repository locale (chiamato `azure` per motivi di semplicità).</span><span class="sxs-lookup"><span data-stu-id="82d99-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="82d99-162">Distribuire il toohello codice di esempio `azure` Git remoto.</span><span class="sxs-lookup"><span data-stu-id="82d99-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="82d99-163">Quando richiesto, utilizzare le credenziali di distribuzione hello configurati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82d99-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="82d99-164">Infine, ma è sufficiente avviare l'app di Azure in tempo reale nel browser hello:</span><span class="sxs-lookup"><span data-stu-id="82d99-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="82d99-165">Dovrebbe essere hello stessa Sails.js home page.</span><span class="sxs-lookup"><span data-stu-id="82d99-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="82d99-166">Risoluzione dei problemi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="82d99-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="82d99-167">Se l'applicazione Sails.js non riesce per qualche motivo nel servizio App, trovare il log di stderr hello toohelp risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="82d99-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="82d99-168">Per ulteriori informazioni, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="82d99-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="82d99-169">Se l'applicazione hello sono stati avviati, devono visualizzare i log di stdout hello è familiare messaggio:</span><span class="sxs-lookup"><span data-stu-id="82d99-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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

<span data-ttu-id="82d99-170">È possibile controllare la granularità dei log di stdout hello in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span><span class="sxs-lookup"><span data-stu-id="82d99-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="82d99-171">La connessione a database tooa in Azure</span><span class="sxs-lookup"><span data-stu-id="82d99-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="82d99-172">tooconnect tooa database in Azure, creare database hello di propria scelta in Azure, ad esempio Database SQL di Azure, MySQL, MongoDB, Cache di Azure (Redis), e così via e utilizzare hello corrispondente [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="82d99-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="82d99-173">Hello passaggi in questa sezione viene illustrato come tooMongoDB tooconnect utilizzando un [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, che può supportare le connessioni client di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="82d99-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="82d99-174">[Creare un account Cosmos DB con supporto del protocollo per MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="82d99-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="82d99-175">[Creare una raccolta e un database Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="82d99-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="82d99-176">nome Hello dell'insieme di hello non è rilevante, ma è necessario il nome di hello del database di hello quando ci si connette da Sails.js.</span><span class="sxs-lookup"><span data-stu-id="82d99-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="82d99-177">[Trovare hello informazioni di connessione per il database DB Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="82d99-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="82d99-178">Dal terminale della riga di comando, installare l'adapter di MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="82d99-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="82d99-179">Aprire config/connections.js e aggiungere hello elenco toohello oggetto di connessione seguente:</span><span class="sxs-lookup"><span data-stu-id="82d99-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="82d99-180">Hello `ssl: true` opzione è importante perché [DB Cosmos richiede](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="82d99-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="82d99-181">Per ogni variabile di ambiente (`process.env.*`), è necessario tooset nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="82d99-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="82d99-182">toodo, questa fase hello seguenti comandi dal terminale.</span><span class="sxs-lookup"><span data-stu-id="82d99-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="82d99-183">Utilizzare le informazioni di connessione hello per le DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="82d99-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="82d99-184">L'inserimento delle proprie impostazioni nelle impostazioni dell'app Azure mantiene i dati sensibili al di fuori del controllo del codice sorgente (Git).</span><span class="sxs-lookup"><span data-stu-id="82d99-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="82d99-185">Passaggio successivo si configurerà lo sviluppo delle stesse informazioni di connessione di hello toouse di ambiente.</span><span class="sxs-lookup"><span data-stu-id="82d99-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="82d99-186">Aprire config/local.js e aggiungere hello segue l'oggetto di connessioni:</span><span class="sxs-lookup"><span data-stu-id="82d99-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="82d99-187">Questa configurazione sostituisce le impostazioni di hello nel file config/connections.js per ambiente locale hello.</span><span class="sxs-lookup"><span data-stu-id="82d99-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="82d99-188">Questo file con estensione gitignore predefinito hello nel progetto viene escluso in modo non verranno archiviato in Git.</span><span class="sxs-lookup"><span data-stu-id="82d99-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="82d99-189">A questo punto, si è in grado di tooconnect tooyour DB Cosmos (MongoDB) database dall'app web di Azure e nell'ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="82d99-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="82d99-190">Aprire config/env/production.js tooconfigure nell'ambiente di produzione e aggiungere il seguente hello `models` oggetto:</span><span class="sxs-lookup"><span data-stu-id="82d99-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="82d99-191">Aprire config/env/development.js tooconfigure l'ambiente di sviluppo e aggiungere il seguente hello `models` oggetto:</span><span class="sxs-lookup"><span data-stu-id="82d99-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="82d99-192">`migrate: 'alter'`Consente di utilizzare toocreate funzionalità di migrazione del database e aggiornare facilmente le raccolte di database o tabelle.</span><span class="sxs-lookup"><span data-stu-id="82d99-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="82d99-193">Tuttavia, `migrate: 'safe'` viene utilizzato per l'ambiente di Azure (produzione) perché Sails.js non è possibile toouse `migrate: 'alter'` in un ambiente di produzione (vedere [Sails.js documentazione](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="82d99-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="82d99-194">Da hello terminal, [generare](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) un Sails.js [cianografia API](http://sailsjs.org/documentation/concepts/blueprints) come è in genere, quindi eseguito `sails lift` per creare database hello con Sails.js migrazione del database.</span><span class="sxs-lookup"><span data-stu-id="82d99-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="82d99-195">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="82d99-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="82d99-196">Hello `mywidget` modello generato da questo comando è vuoto, ma è possibile usarlo tooshow che si disponga della connettività di database.</span><span class="sxs-lookup"><span data-stu-id="82d99-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="82d99-197">Quando si esegue `sails lift`, Crea raccolte mancante hello e modelli di tabelle per hello utilizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="82d99-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="82d99-198">API di accesso hello progetto appena creato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="82d99-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="82d99-199">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="82d99-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="82d99-200">Hello API deve restituire tooyou indietro di hello creato voce nella finestra del browser hello, che significa che la raccolta è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="82d99-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="82d99-201">A questo punto, push tooAzure le modifiche e passare tooyour app toomake verificarne che il corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="82d99-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="82d99-202">Accesso API progetto iniziale di hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="82d99-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="82d99-203">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="82d99-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="82d99-204">Se hello API restituisce un'altra nuova voce, quindi l'app web di Azure con cui sta comunicando tooyour DB Cosmos (MongoDB) database.</span><span class="sxs-lookup"><span data-stu-id="82d99-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="82d99-205">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="82d99-205">More resources</span></span>
* [<span data-ttu-id="82d99-206">Introduzione alle app Web Node.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="82d99-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="82d99-207">Utilizzo di moduli Node.js con le applicazioni Azure</span><span class="sxs-lookup"><span data-stu-id="82d99-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
