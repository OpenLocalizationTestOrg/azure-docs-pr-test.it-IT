---
title: Distribuire un'app Web Sails.js nel servizio app di Azure | Documentazione Microsoft
description: Informazioni su come distribuire un'applicazione Node.js nel servizio app di Azure. Questa esercitazione illustra come distribuire un'app Web Sails.js.
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="6d0f6-104">Distribuire un'app Web Sails.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="6d0f6-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="6d0f6-105">Questa esercitazione illustra come distribuire un'app Sails.js nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="6d0f6-106">Durante il processo vengono offerte informazioni generali sulla configurazione dell'app Node.js da eseguire nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="6d0f6-107">Questa esercitazione illustra alcune operazioni utili, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="6d0f6-108">Configurare l'esecuzione di un'app Sails.js nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="6d0f6-109">Distribuire un'app nel servizio app dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="6d0f6-110">Leggere i log stderr e stdout per risolvere eventuali problemi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="6d0f6-111">Archiviare le variabili di ambiente al di fuori del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="6d0f6-112">Accedere alle variabili di ambiente di Azure dall'app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="6d0f6-113">Connettersi a un database (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="6d0f6-114">Avere una conoscenza pratica di Sails.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="6d0f6-115">Questa esercitazione non fornisce informazioni sulla risoluzione dei problemi generali di esecuzione di Sail.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6d0f6-116">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="6d0f6-116">CLI versions to complete the task</span></span>

<span data-ttu-id="6d0f6-117">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6d0f6-118">[Interfaccia della riga di comando di Azure 1.0](app-service-web-nodejs-sails-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classici e di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="6d0f6-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="6d0f6-119">[Interfaccia della riga di comando di Azure 2.0](app-service-web-nodejs-sails.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="6d0f6-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d0f6-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6d0f6-120">Prerequisites</span></span>
* [<span data-ttu-id="6d0f6-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6d0f6-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="6d0f6-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="6d0f6-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="6d0f6-123">Git</span><span class="sxs-lookup"><span data-stu-id="6d0f6-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="6d0f6-124">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6d0f6-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="6d0f6-125">Un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-125">A Microsoft Azure account.</span></span> <span data-ttu-id="6d0f6-126">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="6d0f6-127">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="6d0f6-128">Creare un'app iniziale e provarla per un'ora, senza impegno e senza dover usare la carta di credito.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="6d0f6-129">Passaggio 1: Creare e configurare un'app Sails.js in locale</span><span class="sxs-lookup"><span data-stu-id="6d0f6-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="6d0f6-130">Innanzitutto, creare rapidamente un'app Sails.js predefinita nell'ambiente di sviluppo attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="6d0f6-131">Aprire il terminale della riga di comando desiderato ed eseguire `CD` in una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="6d0f6-132">Creare un'app Sails.js ed eseguirla:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="6d0f6-133">Assicurarsi che sia possibile passare alla home page predefinita in http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="6d0f6-134">Abilitare quindi la registrazione per Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="6d0f6-135">Nella directory radice creare un file denominato `iisnode.yml` e aggiungere le due righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="6d0f6-136">La registrazione è ora abilitata per il server [iisnode](https://github.com/tjanczuk/iisnode) usato dal Servizio app di Azure per eseguire le app Node.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="6d0f6-137">Per altre informazioni sul funzionamento, vedere [Come eseguire il debug di un'app Web Node.js nel servizio app di Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="6d0f6-138">Configurare quindi l'app Sails.js per usare le variabili di ambiente di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="6d0f6-139">Aprire config/env/production.js per configurare l'ambiente di produzione e impostare `port` e `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="6d0f6-140">La documentazione di queste impostazioni di configurazione è disponibile nella [Documentazione di Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="6d0f6-141">Impostare quindi come hardcoded la versione di Node.js che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="6d0f6-142">In package.json aggiungere la proprietà `engines` seguente per impostare la versione di Node.js desiderata.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="6d0f6-143">Inizializzare infine un repository Git ed eseguire il commit dei file.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="6d0f6-144">Nella radice dell'applicazione (in cui si trova package.json) eseguire i comandi Git seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="6d0f6-145">Il codice è pronto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="6d0f6-146">Passaggio 2: Creare un'app Azure e distribuire Sails.js</span><span class="sxs-lookup"><span data-stu-id="6d0f6-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="6d0f6-147">Creare ora la risorsa del servizio app in Azure e distribuirvi l'app Sails.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="6d0f6-148">accedere ad Azure in questo modo:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="6d0f6-149">Seguire le istruzioni per continuare l'accesso in un browser usando un account con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="6d0f6-150">Impostare l'utente di distribuzione per il servizio app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="6d0f6-151">Si distribuirà il codice usando queste credenziali in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="6d0f6-152">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con un nome.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="6d0f6-153">Per questa esercitazione su Node.js, non è strettamente necessario conoscerne tutte le caratteristiche e funzioni.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="6d0f6-154">Per visualizzare i possibili valori utilizzabili per `<location>`, usare il comando `az appservice list-locations` nell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="6d0f6-155">Creare un [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" con un nome.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="6d0f6-156">Per questa esercitazione su Node.js, è sufficiente sapere che non sono previsti costi per le app Web in questo piano.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="6d0f6-157">Creare una nuova app Web con un nome univoco in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="6d0f6-158">Passaggio 3: Configurare e distribuire l'app Sails.js</span><span class="sxs-lookup"><span data-stu-id="6d0f6-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="6d0f6-159">Configurare la distribuzione Git locale per la nuova app Web con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="6d0f6-160">Si otterrà un output JSON come questo, a indicare la configurazione del repository Git remoto:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="6d0f6-161">Aggiungere l'URL in JSON come Git remoto per il repository locale (chiamato `azure` per motivi di semplicità).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="6d0f6-162">Distribuire il codice di esempio per l'elemento Git remoto `azure`.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="6d0f6-163">Quando richiesto, usare le credenziali di distribuzione configurate prima.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="6d0f6-164">Infine, avviare l'app Azure attiva nel browser:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="6d0f6-165">Verrà visualizzata la stessa home page di Sails.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="6d0f6-166">Risoluzione dei problemi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="6d0f6-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="6d0f6-167">Se l'applicazione Sails.js per qualche motivo non viene avviata nel servizio app, cercare i log stderr per risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="6d0f6-168">Per altre informazioni, vedere [Come eseguire il debug di un'app Web Node.js nel servizio app di Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="6d0f6-169">Se l'app è stata avviata correttamente, il log stdout visualizzerà il messaggio:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="6d0f6-170">È possibile controllare la granularità dei log stdout nel file [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) .</span><span class="sxs-lookup"><span data-stu-id="6d0f6-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="6d0f6-171">Connettersi a un database in Azure</span><span class="sxs-lookup"><span data-stu-id="6d0f6-171">Connect to a database in Azure</span></span>
<span data-ttu-id="6d0f6-172">Per connettersi a un database in Azure, creare il database desiderato in Azure, ad esempio un database SQL di Azure, MySQL, MongoDB, Cache (Redis) di Azure e così via e usare l' [adattatore dell'archivio dati](https://github.com/balderdashy/sails#compatibility) corrispondente per stabilire la connessione.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="6d0f6-173">I passaggi di questa sezione illustrano come connettersi a MongoDB usando un database [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md), che può supportare le connessioni client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="6d0f6-174">[Creare un account Cosmos DB con supporto del protocollo per MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="6d0f6-175">[Creare una raccolta e un database Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="6d0f6-176">Il nome della raccolta non è importante, ma il nome del database è necessario quando ci si connette da Sails.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="6d0f6-177">[Trovare le informazioni di connessione per il database Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="6d0f6-178">Dal terminale della riga di comando installare l'adattatore di MongoDB:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="6d0f6-179">Aprire config/connections.js e aggiungere l'oggetto connessione seguente all'elenco:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="6d0f6-180">L'opzione `ssl: true` è importante perché [è necessaria per Cosmos DB](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="6d0f6-181">Per ogni variabile di ambiente (`process.env.*`), è necessario eseguirne l'impostazione nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="6d0f6-182">A tale scopo, eseguire i comandi seguenti dal terminale.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="6d0f6-183">Usare le informazioni di connessione per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="6d0f6-184">L'inserimento delle proprie impostazioni nelle impostazioni dell'app Azure mantiene i dati sensibili al di fuori del controllo del codice sorgente (Git).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="6d0f6-185">Si configurerà quindi l'ambiente di sviluppo per l'uso delle stesse informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="6d0f6-186">Aprire config/local.js e aggiungere l'oggetto connessione seguente:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="6d0f6-187">Questa configurazione sostituisce le impostazioni presenti nel file config/connections.js per l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="6d0f6-188">Questo file è escluso dal file con estensione gitignore predefinito del progetto, quindi non verrà archiviato in Git.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="6d0f6-189">A questo punto, è possibile connettersi al database Cosmos DB (MongoDB) dall'app Web di Azure e dall'ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="6d0f6-190">Aprire config/env/production.js per configurare l'ambiente di produzione e aggiungere l'oggetto `models` seguente:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="6d0f6-191">Aprire config/env/development.js per configurare l'ambiente di sviluppo e aggiungere l'oggetto `models` seguente:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="6d0f6-192">`migrate: 'alter'` consente di usare le funzionalità di migrazione di database per creare e aggiornare facilmente le raccolte o le tabelle di database.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="6d0f6-193">Per l'ambiente di produzione di Azure si usa tuttavia `migrate: 'safe'`, perché Sails.js non consente di usare `migrate: 'alter'` in un ambiente di produzione. Vedere la [documentazione di Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="6d0f6-194">Dal terminale eseguire [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) per generare un'[API di progetto](http://sailsjs.org/documentation/concepts/blueprints) (blueprint) Sails.js come di consueto, quindi eseguire `sails lift` per creare il database con la migrazione del database Sails.js.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="6d0f6-195">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="6d0f6-196">Il modello `mywidget` generato da questo comando è vuoto, ma è possibile usarlo per mostrare che la connettività del database è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="6d0f6-197">Quando si esegue `sails lift`, vengono create le raccolte e le tabelle mancanti per i modelli usati dall'app.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="6d0f6-198">Accedere all'API di progetto (blueprint) creata nel browser.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="6d0f6-199">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="6d0f6-200">L'API deve restituire all'utente la voce creata nella finestra del browser, per indicare che la raccolta è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="6d0f6-201">Effettuare quindi il push delle modifiche in Azure e passare all'app per verificare che funzioni ancora correttamente.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="6d0f6-202">Accedere all'API di progetto dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0f6-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="6d0f6-203">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d0f6-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="6d0f6-204">Se l'API restituisce un'altra voce nuova, l'app Web di Azure sta comunicando con il database Cosmos DB (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="6d0f6-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="6d0f6-205">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="6d0f6-205">More resources</span></span>
* [<span data-ttu-id="6d0f6-206">Introduzione alle app Web Node.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="6d0f6-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="6d0f6-207">Utilizzo di moduli Node.js con le applicazioni Azure</span><span class="sxs-lookup"><span data-stu-id="6d0f6-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
