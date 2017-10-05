---
title: Come usare l'SDK del server back-end Node.js per App per dispositivi mobili | Documentazione Microsoft
description: Informazioni su come usare l'SDK del server back-end di Node.js per App per dispositivi mobili del servizio app di Azure.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="c7785-103">Come usare Node.js SDK per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="c7785-104">Questo articolo fornisce informazioni dettagliate ed esempi sull'uso di un back-end Node.js nelle app per dispositivi mobili del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="c7785-105"><a name="Introduction"></a>Introduzione</span><span class="sxs-lookup"><span data-stu-id="c7785-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="c7785-106">App per dispositivi mobili del servizio app di Azure consente di aggiungere un'API Web di accesso ai dati ottimizzata per dispositivi mobili a un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="c7785-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="c7785-107">Azure App Service Mobile Apps SDK viene fornito per le applicazioni Web Node.js e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7785-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="c7785-108">L'SDK consente le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7785-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="c7785-109">Operazioni su tabella (read, insert, update, delete) per l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="c7785-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="c7785-110">Operazioni sulle API personalizzate</span><span class="sxs-lookup"><span data-stu-id="c7785-110">Custom API operations</span></span>

<span data-ttu-id="c7785-111">Entrambe le operazioni permettono l'autenticazione in tutti i provider di identità consentiti dal servizio app di Azure, inclusi i provider di identità basati su social network, ad esempio Facebook, Twitter, Google e Microsoft nonché Azure Active Directory per l'identità aziendale.</span><span class="sxs-lookup"><span data-stu-id="c7785-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="c7785-112">Esempi per ogni caso d'uso sono disponibili nella [directory degli esempi in GitHub].</span><span class="sxs-lookup"><span data-stu-id="c7785-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="c7785-113">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="c7785-113">Supported Platforms</span></span>
<span data-ttu-id="c7785-114">Node SDK per App per dispositivi mobili di Azure supporta la versione LTS corrente di Node e le versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c7785-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="c7785-115">Al momento della stesura di questo testo, la versione LTS più recente di è Node v4.5.0.</span><span class="sxs-lookup"><span data-stu-id="c7785-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="c7785-116">Altre versioni di Node potrebbero funzionare, ma non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="c7785-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="c7785-117">Node SDK per App per dispositivi mobili di Azure supporta due driver di database, il driver node-mssql supporta SQL Azure e le istanze locali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7785-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="c7785-118">Il driver sqlite3 supporta i database SQLite solo su un'unica istanza.</span><span class="sxs-lookup"><span data-stu-id="c7785-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="c7785-119"><a name="howto-cmdline-basicapp"></a>Creare un back-end Node.js di base usando la riga di comando</span><span class="sxs-lookup"><span data-stu-id="c7785-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="c7785-120">Ogni back-end Node.js per le app per dispositivi mobili del servizio app di Azure viene avviato come applicazione ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="c7785-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="c7785-121">ExpressJS è il framework dei servizi Web più diffuso disponibile per Node.js.</span><span class="sxs-lookup"><span data-stu-id="c7785-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="c7785-122">È possibile creare un'applicazione [Express] di base seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c7785-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="c7785-123">Creare una directory per il progetto in una finestra di comando o di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7785-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="c7785-124">Eseguire npm init per inizializzare la struttura del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="c7785-125">Il comando npm init pone una serie di domande per inizializzare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="c7785-126">Vedere l'output di esempio:</span><span class="sxs-lookup"><span data-stu-id="c7785-126">See the example output:</span></span>

    ![L'output di init npm][0]
3. <span data-ttu-id="c7785-128">Installare le librerie express e azure-mobile-apps dal repository npm.</span><span class="sxs-lookup"><span data-stu-id="c7785-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="c7785-129">Creare un file app.js per implementare il server per dispositivi mobili di base.</span><span class="sxs-lookup"><span data-stu-id="c7785-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="c7785-130">Questa applicazione crea un'API Web ottimizzata per dispositivi mobili con un endpoint singolo,`/tables/TodoItem`, che consente l'accesso non autenticato a un archivio dati SQL sottostante usando uno schema dinamico.</span><span class="sxs-lookup"><span data-stu-id="c7785-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="c7785-131">È adatta per l'avvio rapido delle librerie client seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7785-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="c7785-132">[Avvio rapido di client Android]</span><span class="sxs-lookup"><span data-stu-id="c7785-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="c7785-133">[Avvio rapido di client Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="c7785-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="c7785-134">[Avvio rapido di client iOS]</span><span class="sxs-lookup"><span data-stu-id="c7785-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="c7785-135">[Avvio rapido di client Windows Store]</span><span class="sxs-lookup"><span data-stu-id="c7785-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="c7785-136">[Avvio rapido di client Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="c7785-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="c7785-137">[Avvio rapido di client Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="c7785-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="c7785-138">[Avvio rapido di client Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="c7785-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="c7785-139">Il codice per questa applicazione di base è disponibile nell' [esempio basicapp in GitHub].</span><span class="sxs-lookup"><span data-stu-id="c7785-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="c7785-140"><a name="howto-vs2015-basicapp"></a>Procedura: Creare un back-end Node.js con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c7785-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="c7785-141">Visual Studio 2015 richiede un'estensione per lo sviluppo di applicazioni Node.js all'interno dell'IDE.</span><span class="sxs-lookup"><span data-stu-id="c7785-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="c7785-142">Per iniziare, installare gli [Strumenti Node.js 1.1 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c7785-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="c7785-143">Dopo aver installato gli Strumenti Node.js per Visual Studio, creare un'applicazione Express 4.x:</span><span class="sxs-lookup"><span data-stu-id="c7785-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="c7785-144">Aprire la finestra di dialogo **Nuovo progetto** (da **File** > **Nuovo** > **Progetto...**).</span><span class="sxs-lookup"><span data-stu-id="c7785-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="c7785-145">Espandere **Modelli** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="c7785-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="c7785-146">Selezionare **Basic Azure Node.js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="c7785-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="c7785-147">Immettere il nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-147">Fill in the project name.</span></span>  <span data-ttu-id="c7785-148">Fare clic su *OK*.</span><span class="sxs-lookup"><span data-stu-id="c7785-148">Click *OK*.</span></span>

    ![Nuovo progetto di Visual Studio 2015][1]
5. <span data-ttu-id="c7785-150">Fare clic sul nodo **npm** e selezionare **Install New npm packages...**.</span><span class="sxs-lookup"><span data-stu-id="c7785-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="c7785-151">Al momento della creazione della prima applicazione Node.js potrebbe essere necessario aggiornare il catalogo npm.</span><span class="sxs-lookup"><span data-stu-id="c7785-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="c7785-152">Fare clic su **Refresh** (Aggiorna), se necessario.</span><span class="sxs-lookup"><span data-stu-id="c7785-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="c7785-153">Immettere *azure-mobile-apps* nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c7785-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="c7785-154">Fare clic sul pacchetto **azure-mobile-apps 2.0.0**, quindi fare clic su **Install Package**.</span><span class="sxs-lookup"><span data-stu-id="c7785-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Installare nuovi pacchetti npm][2]
8. <span data-ttu-id="c7785-156">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="c7785-156">Click **Close**.</span></span>
9. <span data-ttu-id="c7785-157">Aprire il file *app.js* per aggiungere il supporto per l'SDK per App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="c7785-158">Nella riga 6 nella parte inferiore delle istruzioni require della libreria aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="c7785-159">Circa alla riga 27 dopo le altre istruzioni app.use aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="c7785-160">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="c7785-160">Save the file.</span></span>
10. <span data-ttu-id="c7785-161">Eseguire l'applicazione in locale, ovvero l'API viene eseguita in http://localhost:3000, o pubblicarla in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="c7785-162"><a name="create-node-backend-portal"></a>Procedura: Creare un back-end Node.js usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="c7785-163">È possibile creare un back-end dell'app per dispositivi mobili direttamente nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="c7785-164">È possibile seguire i passaggi seguenti o creare un client e un nuovo server seguendo l'esercitazione [Creare un'app per dispositivi mobili](app-service-mobile-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c7785-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="c7785-165">L'esercitazione contiene una versione semplificata di queste istruzioni e dimostra i progetti del concetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="c7785-166">Nel pannello *Attività iniziali*, in **Creare un'API di tabella** scegliere **Node.js** come **Linguaggio back-end**.</span><span class="sxs-lookup"><span data-stu-id="c7785-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="c7785-167">Selezionare la casella per "**Sono consapevole che questa operazione comporterà la sovrascrittura di tutti i contenuti del sito.**" e fare clic su **Crea tabella TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="c7785-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="c7785-168"><a name="download-quickstart"></a>Procedura: Scaricare il progetto di codice di avvio rapido del back-end Node.js tramite Git</span><span class="sxs-lookup"><span data-stu-id="c7785-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="c7785-169">Quando si crea un back-end dell'app per dispositivi mobili Node.js usando il pannello **Avvio rapido** del portale, viene creato e distribuito nel sito un progetto Node.js.</span><span class="sxs-lookup"><span data-stu-id="c7785-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="c7785-170">È possibile aggiungere tabelle e API e modificare i file di codice per il back-end Node.js nel portale.</span><span class="sxs-lookup"><span data-stu-id="c7785-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="c7785-171">Si possono anche usare vari strumenti di distribuzione per scaricare il progetto back-end, per poter aggiungere o modificare tabelle e API, quindi ripubblicare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="c7785-172">Per altre informazioni, vedere la [Guida alla distribuzione del servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="c7785-173">La procedura seguente usa un repository Git per scaricare il codice del progetto di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="c7785-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="c7785-174">Se non è già stato fatto, installare Git.</span><span class="sxs-lookup"><span data-stu-id="c7785-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="c7785-175">I passaggi necessari per installare Git variano a seconda del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c7785-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="c7785-176">Vedere la sezione [Installazione di Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) per indicazioni specifiche del sistema operativo relative a distribuzioni e installazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="c7785-177">Seguire i passaggi in [Abilitare il repository dell'app del servizio app](../app-service-web/app-service-deploy-local-git.md#Step3) per abilitare il repository Git per il sito di back-end, prendendo nota del nome utente e della password della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c7785-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="c7785-178">Nel pannello di back-end dell'app per dispositivi mobili annotare l'impostazione **URL clone Git** .</span><span class="sxs-lookup"><span data-stu-id="c7785-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="c7785-179">Eseguire il comando `git clone` usando l'URL clone Git e immettendo la password quando richiesto, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="c7785-180">Passare alla directory locale, che nell'esempio precedente è /todolist e osservare che sono stati scaricati i file di progetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="c7785-181">Individuare il file `todoitem.json` nella directory `/tables`.</span><span class="sxs-lookup"><span data-stu-id="c7785-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="c7785-182">Questo file definisce le autorizzazioni sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="c7785-183">Individuare il file `todoitem.js` nella stessa directory, che definisce gli script di operazioni CRUD per la tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="c7785-184">Dopo che sono state apportate modifiche ai file di progetto, eseguire i comandi seguenti per aggiungere, eseguire il commit delle modifiche e quindi caricare nel sito:</span><span class="sxs-lookup"><span data-stu-id="c7785-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="c7785-185">Quando si aggiungono nuovi file al progetto, è necessario prima di tutto eseguire il comando `git add .`.</span><span class="sxs-lookup"><span data-stu-id="c7785-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="c7785-186">Il sito viene ripubblicato ogni volta che viene effettuato il push di un nuovo set di commit al sito.</span><span class="sxs-lookup"><span data-stu-id="c7785-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="c7785-187"><a name="howto-publish-to-azure"></a>Procedura: Pubblicare il back-end Node.js in Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="c7785-188">Microsoft Azure offre numerosi meccanismi per la pubblicazione del back-end Node.js per le app per dispositivi mobili del servizio app di Azure,</span><span class="sxs-lookup"><span data-stu-id="c7785-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="c7785-189">tra cui l'uso di strumenti di distribuzione integrati in Visual Studio, strumenti da riga di comando e opzioni di distribuzione continua basate sul controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="c7785-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="c7785-190">Per altre informazioni su questo argomento, vedere la [Guida alla distribuzione del servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="c7785-191">Il servizio app di Azure include suggerimenti specifici per l'applicazione Node.js che è consigliabile esaminare prima della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="c7785-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="c7785-192">Come [specificare la versione di Node.js]</span><span class="sxs-lookup"><span data-stu-id="c7785-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="c7785-193">Come [usare i moduli di Node]</span><span class="sxs-lookup"><span data-stu-id="c7785-193">How to [use Node modules]</span></span>

### <span data-ttu-id="c7785-194"><a name="howto-enable-homepage"></a>Procedura: Abilitare una home page dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c7785-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="c7785-195">Molte applicazioni sono una combinazione di app Web e per dispositivi mobili e il framework ExpressJS consente di combinare i due aspetti.</span><span class="sxs-lookup"><span data-stu-id="c7785-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="c7785-196">In alcuni casi, tuttavia, è consigliabile implementare solo un'interfaccia per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c7785-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="c7785-197">È utile fornire una pagina di destinazione per garantire il servizio app sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c7785-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="c7785-198">È possibile fornire la propria home page o abilitarne una temporanea.</span><span class="sxs-lookup"><span data-stu-id="c7785-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="c7785-199">Per abilitare una home page temporanea, usare quanto segue per creare un'istanza di App per dispositivi mobili di Azure:</span><span class="sxs-lookup"><span data-stu-id="c7785-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="c7785-200">È possibile aggiungere questa impostazione al file `azureMobile.js` se si vuole che questa opzione sia disponibile solo quando si sviluppa in locale.</span><span class="sxs-lookup"><span data-stu-id="c7785-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="c7785-201"><a name="TableOperations"></a>Operazioni su tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="c7785-202">Node.js Server SDK (azure-mobile-apps) offre diversi meccanismi per esporre le tabelle dati archiviate nel database SQL di Azure come API Web.</span><span class="sxs-lookup"><span data-stu-id="c7785-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="c7785-203">Sono disponibili cinque operazioni.</span><span class="sxs-lookup"><span data-stu-id="c7785-203">Five operations are provided.</span></span>

| <span data-ttu-id="c7785-204">Operazione</span><span class="sxs-lookup"><span data-stu-id="c7785-204">Operation</span></span> | <span data-ttu-id="c7785-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7785-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7785-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="c7785-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="c7785-207">Ottiene tutti i record nella tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-207">Get all records in the table</span></span> |
| <span data-ttu-id="c7785-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="c7785-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="c7785-209">Ottiene un record specifico nella tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="c7785-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="c7785-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="c7785-211">Creare un record nella tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-211">Create a record in the table</span></span> |
| <span data-ttu-id="c7785-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="c7785-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="c7785-213">Aggiornare un record nella tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-213">Update a record in the table</span></span> |
| <span data-ttu-id="c7785-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="c7785-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="c7785-215">Elimina un record dalla tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-215">Delete a record in the table</span></span> |

<span data-ttu-id="c7785-216">Questa API Web supporta [OData] ed estende lo schema della tabella per supportare la [sincronizzazione dati offline].</span><span class="sxs-lookup"><span data-stu-id="c7785-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="c7785-217"><a name="howto-dynamicschema"></a>Procedura: Definire le tabelle con uno schema dinamico</span><span class="sxs-lookup"><span data-stu-id="c7785-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="c7785-218">Perché sia possibile usare una tabella, è necessario prima definirla.</span><span class="sxs-lookup"><span data-stu-id="c7785-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="c7785-219">Le tabelle possono essere definite con uno schema statico (dove lo sviluppatore definisce le colonne all'interno dello schema) o in modo dinamico (dove l'SDK controlla lo schema in base alle richieste in ingresso).</span><span class="sxs-lookup"><span data-stu-id="c7785-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="c7785-220">Lo sviluppatore può anche controllare alcuni aspetti specifici dell'API Web aggiungendo codice JavaScript alla definizione.</span><span class="sxs-lookup"><span data-stu-id="c7785-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="c7785-221">Come procedura consigliata, è necessario definire ogni tabella in un file JavaScript nella directory delle tabelle, quindi usare il metodo tables.import() per importare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="c7785-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="c7785-222">Estendendo l'app di base, il file app.js viene regolato:</span><span class="sxs-lookup"><span data-stu-id="c7785-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="c7785-223">Definire la tabella in ./tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="c7785-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="c7785-224">Per impostazione predefinita, le tabelle usano lo schema dinamico.</span><span class="sxs-lookup"><span data-stu-id="c7785-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="c7785-225">Per disattivare lo schema dinamico a livello globale, impostare su false l'impostazione dell'app **MS_DynamicSchema** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="c7785-226">Per un esempio completo, vedere l' [esempio todo in GitHub].</span><span class="sxs-lookup"><span data-stu-id="c7785-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="c7785-227"><a name="howto-staticschema"></a>Procedura: Definire le tabelle con uno schema statico</span><span class="sxs-lookup"><span data-stu-id="c7785-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="c7785-228">È possibile definire in modo esplicito le colonne da esporre con l'API Web.</span><span class="sxs-lookup"><span data-stu-id="c7785-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="c7785-229">Node.js SDK (azure-mobile-apps) aggiunge automaticamente tutte le altre colonne necessarie per la sincronizzazione dati offline all'elenco specificato.</span><span class="sxs-lookup"><span data-stu-id="c7785-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="c7785-230">Ad esempio, le applicazioni client di avvio rapido richiedono una tabella con due colonne: text (una stringa) e complete (un valore booleano).</span><span class="sxs-lookup"><span data-stu-id="c7785-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="c7785-231">Questa tabella può essere specificata nel file JavaScript di definizione della tabella, presente nella directory delle tabelle, nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="c7785-232">Se si definiscono le tabelle in modo statico, è necessario chiamare il metodo tables.initialize() per creare lo schema del database all'avvio.</span><span class="sxs-lookup"><span data-stu-id="c7785-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="c7785-233">Il metodo tables.initialize() restituisce un oggetto [Promise] in modo che il servizio Web non gestisca le richieste prima dell'inizializzazione del database.</span><span class="sxs-lookup"><span data-stu-id="c7785-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="c7785-234"><a name="howto-sqlexpress-setup"></a>Procedura: Usare SQL Express come archivio dati di sviluppo nel computer locale</span><span class="sxs-lookup"><span data-stu-id="c7785-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="c7785-235">Node SDK per le app per dispositivi mobili di Azure offre tre opzioni predefinite per la gestione dei dati:</span><span class="sxs-lookup"><span data-stu-id="c7785-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="c7785-236">Usare il driver **memory** per fornire un archivio di esempio non persistente</span><span class="sxs-lookup"><span data-stu-id="c7785-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="c7785-237">Usare il driver **mssql** per fornire un archivio dati di SQL Express per lo sviluppo</span><span class="sxs-lookup"><span data-stu-id="c7785-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="c7785-238">Usare il driver **mssql** per fornire un archivio dati del database SQL di Azure per la produzione</span><span class="sxs-lookup"><span data-stu-id="c7785-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="c7785-239">Node.js SDK per le app per dispositivi mobili di Azure usa il [pacchetto mssql per Node.js] per stabilire e usare una connessione a SQL Express e al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="c7785-240">Per questo pacchetto è necessario abilitare le connessioni TCP nell'istanza di SQL Express.</span><span class="sxs-lookup"><span data-stu-id="c7785-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="c7785-241">Il driver memory non fornisce un set completo di funzionalità per i test.</span><span class="sxs-lookup"><span data-stu-id="c7785-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="c7785-242">Per testare il back-end in locale, è consigliabile usare un archivio dati di SQL Express con il driver mssql.</span><span class="sxs-lookup"><span data-stu-id="c7785-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="c7785-243">Scaricare e installare [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="c7785-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="c7785-244">Assicurarsi di installare l'edizione SQL Server 2014 Express with Tools.</span><span class="sxs-lookup"><span data-stu-id="c7785-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="c7785-245">A meno che non sia richiesto in modo esplicito il supporto a 64 bit, l'esecuzione della versione a 32 bit richiede una quantità di memoria inferiore.</span><span class="sxs-lookup"><span data-stu-id="c7785-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="c7785-246">Eseguire Gestione configurazione SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="c7785-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="c7785-247">Espandere il nodo **Configurazione di rete SQL Server** nel menu ad albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c7785-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="c7785-248">Fare clic su **Protocolli per SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="c7785-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="c7785-249">Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="c7785-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="c7785-250">Fare clic su **OK** nella finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="c7785-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="c7785-251">Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c7785-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="c7785-252">Fare clic sulla scheda **Indirizzi IP** .</span><span class="sxs-lookup"><span data-stu-id="c7785-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="c7785-253">Trovare il nodo **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="c7785-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="c7785-254">Nel campo **Porta TCP** immettere **1433**.</span><span class="sxs-lookup"><span data-stu-id="c7785-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="c7785-255">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7785-255">Click **OK**.</span></span>  <span data-ttu-id="c7785-256">Fare clic su **OK** nella finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="c7785-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="c7785-257">Fare clic su **Servizi di SQL Server** nel menu ad albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c7785-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="c7785-258">Fare clic con il pulsante destro del mouse su **SQL Server (SQLEXPRESS)** e scegliere **Riavvia**</span><span class="sxs-lookup"><span data-stu-id="c7785-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="c7785-259">Chiudere Gestione configurazione SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="c7785-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="c7785-260">Eseguire SQL Server 2014 Management Studio e connettersi all'istanza locale di SQL Express</span><span class="sxs-lookup"><span data-stu-id="c7785-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="c7785-261">Fare clic con il pulsante destro del mouse sull'istanza in Esplora oggetti e scegliere **Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c7785-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="c7785-262">Selezionare la pagina **Sicurezza** .</span><span class="sxs-lookup"><span data-stu-id="c7785-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="c7785-263">Assicurarsi che l'opzione **Modalità di autenticazione di SQL Server e di Windows** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c7785-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="c7785-264">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="c7785-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="c7785-265">Espandere **Sicurezza** > **Account di accesso** .</span><span class="sxs-lookup"><span data-stu-id="c7785-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="c7785-266">Fare clic con il pulsante destro del mouse su **Account di accesso** e scegliere **Nuovo account di accesso**</span><span class="sxs-lookup"><span data-stu-id="c7785-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="c7785-267">Immettere un nome account di accesso.</span><span class="sxs-lookup"><span data-stu-id="c7785-267">Enter a Login name.</span></span>  <span data-ttu-id="c7785-268">Selezionare **Autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c7785-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="c7785-269">Immettere una password e quindi immetterla di nuovo in **Conferma password**.</span><span class="sxs-lookup"><span data-stu-id="c7785-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="c7785-270">La password deve soddisfare i requisiti di complessità di Windows.</span><span class="sxs-lookup"><span data-stu-id="c7785-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="c7785-271">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="c7785-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="c7785-272">Fare clic con il pulsante destro del mouse sul nuovo account di accesso e scegliere **Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c7785-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="c7785-273">Selezionare la pagina **Ruoli server** .</span><span class="sxs-lookup"><span data-stu-id="c7785-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="c7785-274">Selezionare la casella accanto al ruolo server **dbcreator** .</span><span class="sxs-lookup"><span data-stu-id="c7785-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="c7785-275">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="c7785-275">Click **OK**</span></span>
   13. <span data-ttu-id="c7785-276">Chiudere SQL Server 2015 Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c7785-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="c7785-277">Prendere nota del nome utente e della password selezionati.</span><span class="sxs-lookup"><span data-stu-id="c7785-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="c7785-278">Potrebbe essere necessario assegnare autorizzazioni o ruoli del server aggiuntivi a seconda dei requisiti di database specifici.</span><span class="sxs-lookup"><span data-stu-id="c7785-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="c7785-279">L'applicazione Node.js legge la variabile di ambiente **SQLCONNSTR_MS_TableConnectionString** per la stringa di connessione per il database.</span><span class="sxs-lookup"><span data-stu-id="c7785-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="c7785-280">Questa variabile può essere impostata all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="c7785-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="c7785-281">Ad esempio, è possibile usare PowerShell per impostare questa variabile di ambiente:</span><span class="sxs-lookup"><span data-stu-id="c7785-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="c7785-282">Accedere al database con una connessione TCP/IP e fornire un nome utente e una password per la connessione.</span><span class="sxs-lookup"><span data-stu-id="c7785-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="c7785-283"><a name="howto-config-localdev"></a>Procedura: Configurare il progetto per lo sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="c7785-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="c7785-284">App per dispositivi mobili di Azure legge un file JavaScript denominato *azureMobile.js* dal file system locale.</span><span class="sxs-lookup"><span data-stu-id="c7785-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="c7785-285">Non usare questo file per configurare Azure Mobile Apps SDK nell'ambiente di produzione. Usare invece Impostazioni app nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="c7785-286">Il file *azureMobile.js* deve esportare un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="c7785-287">Le impostazioni più comuni sono:</span><span class="sxs-lookup"><span data-stu-id="c7785-287">The most common settings are:</span></span>

* <span data-ttu-id="c7785-288">Impostazioni database</span><span class="sxs-lookup"><span data-stu-id="c7785-288">Database Settings</span></span>
* <span data-ttu-id="c7785-289">Impostazioni di registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="c7785-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="c7785-290">Impostazioni CORS alternative</span><span class="sxs-lookup"><span data-stu-id="c7785-290">Alternate CORS Settings</span></span>

<span data-ttu-id="c7785-291">Di seguito è riportato un file *azureMobile.js* di esempio che implementa le impostazioni del database seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7785-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="c7785-292">È consigliabile aggiungere *azureMobile.js* al file con estensione *.gitignore*, o altro file IGNORE di controllo del codice sorgente, per evitare che le password vengano archiviate nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c7785-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="c7785-293">Configurare sempre le impostazioni di produzione in Impostazioni app nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="c7785-294"><a name="howto-appsettings"></a>Procedura: Configurare le impostazioni dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="c7785-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="c7785-295">Quasi tutte le impostazioni nel file *azureMobile.js* hanno un'impostazione app equivalente nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="c7785-296">Usare l'elenco seguente per configurare l'app in Impostazioni app:</span><span class="sxs-lookup"><span data-stu-id="c7785-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="c7785-297">Impostazione app</span><span class="sxs-lookup"><span data-stu-id="c7785-297">App Setting</span></span> | <span data-ttu-id="c7785-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="c7785-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="c7785-299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7785-299">Description</span></span> | <span data-ttu-id="c7785-300">Valori validi</span><span class="sxs-lookup"><span data-stu-id="c7785-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c7785-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="c7785-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="c7785-302">name</span><span class="sxs-lookup"><span data-stu-id="c7785-302">name</span></span> |<span data-ttu-id="c7785-303">Nome dell'app</span><span class="sxs-lookup"><span data-stu-id="c7785-303">The name of the app</span></span> |<span data-ttu-id="c7785-304">string</span><span class="sxs-lookup"><span data-stu-id="c7785-304">string</span></span> |
| <span data-ttu-id="c7785-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="c7785-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="c7785-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="c7785-306">logging.level</span></span> |<span data-ttu-id="c7785-307">Livello log minimo di messaggi da registrare</span><span class="sxs-lookup"><span data-stu-id="c7785-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="c7785-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="c7785-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="c7785-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="c7785-309">**MS_DebugMode**</span></span> |<span data-ttu-id="c7785-310">debug</span><span class="sxs-lookup"><span data-stu-id="c7785-310">debug</span></span> |<span data-ttu-id="c7785-311">Abilitare o disabilitare la modalità di debug</span><span class="sxs-lookup"><span data-stu-id="c7785-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="c7785-312">true, false</span><span class="sxs-lookup"><span data-stu-id="c7785-312">true, false</span></span> |
| <span data-ttu-id="c7785-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="c7785-313">**MS_TableSchema**</span></span> |<span data-ttu-id="c7785-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="c7785-314">data.schema</span></span> |<span data-ttu-id="c7785-315">Nome dello schema predefinito per le tabelle SQL</span><span class="sxs-lookup"><span data-stu-id="c7785-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="c7785-316">string (valore predefinito: dbo)</span><span class="sxs-lookup"><span data-stu-id="c7785-316">string (default: dbo)</span></span> |
| <span data-ttu-id="c7785-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="c7785-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="c7785-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="c7785-318">data.dynamicSchema</span></span> |<span data-ttu-id="c7785-319">Abilitare o disabilitare la modalità di debug</span><span class="sxs-lookup"><span data-stu-id="c7785-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="c7785-320">true, false</span><span class="sxs-lookup"><span data-stu-id="c7785-320">true, false</span></span> |
| <span data-ttu-id="c7785-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="c7785-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="c7785-322">version (impostata su undefined)</span><span class="sxs-lookup"><span data-stu-id="c7785-322">version (set to undefined)</span></span> |<span data-ttu-id="c7785-323">Disabilita l'intestazione X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="c7785-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="c7785-324">true, false</span><span class="sxs-lookup"><span data-stu-id="c7785-324">true, false</span></span> |
| <span data-ttu-id="c7785-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="c7785-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="c7785-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="c7785-326">skipversioncheck</span></span> |<span data-ttu-id="c7785-327">Disabilita il controllo della versione dell'API client</span><span class="sxs-lookup"><span data-stu-id="c7785-327">Disables the client API version check</span></span> |<span data-ttu-id="c7785-328">true, false</span><span class="sxs-lookup"><span data-stu-id="c7785-328">true, false</span></span> |

<span data-ttu-id="c7785-329">Per definire un'impostazione app:</span><span class="sxs-lookup"><span data-stu-id="c7785-329">To set an App Setting:</span></span>

1. <span data-ttu-id="c7785-330">Accedere al [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="c7785-331">Selezionare **Tutte le risorse** o **Servizi app** e quindi fare clic sul nome dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c7785-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="c7785-332">Per impostazione predefinita si apre il pannello Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c7785-332">The Settings blade opens by default.</span></span> <span data-ttu-id="c7785-333">In caso contrario fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c7785-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="c7785-334">Fare clic su **Impostazioni dell'applicazione** nel menu GENERALE.</span><span class="sxs-lookup"><span data-stu-id="c7785-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="c7785-335">Scorrere fino alla sezione Impostazioni app.</span><span class="sxs-lookup"><span data-stu-id="c7785-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="c7785-336">Se l'impostazione app esiste già, fare clic sul valore dell'impostazione dell'app per modificarlo.</span><span class="sxs-lookup"><span data-stu-id="c7785-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="c7785-337">Se l'impostazione app non esiste, immettere l'impostazione app nella casella Chiave e il valore nella casella Valore.</span><span class="sxs-lookup"><span data-stu-id="c7785-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="c7785-338">Al termine, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c7785-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="c7785-339">Per modificare la maggior parte delle impostazioni dell'app, è necessario riavviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c7785-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="c7785-340"><a name="howto-use-sqlazure"></a>Procedura: Usare il database SQL come archivio dati di produzione</span><span class="sxs-lookup"><span data-stu-id="c7785-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="c7785-341">L'uso del database SQL di Azure come archivio dati è identico in tutti i tipi di applicazione del Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="c7785-342">Se non è già stato fatto, seguire questa procedura per creare un back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c7785-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="c7785-343">Accedere al [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="c7785-344">Nella parte superiore sinistra della finestra, fare clic su di **+ nuovo** pulsante > **Web e dispositivi mobili** > **App Mobile**, quindi specificare un nome per il back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="c7785-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="c7785-345">Nella casella **Gruppo di risorse** immettere lo stesso nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="c7785-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="c7785-346">Viene selezionato il piano di servizio app predefinito.</span><span class="sxs-lookup"><span data-stu-id="c7785-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="c7785-347">Per modificare il piano di servizio app, fare clic su Piano di servizio app > **+ Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="c7785-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="c7785-348">Specificare un nome del nuovo piano del servizio app e selezionare un percorso appropriato.</span><span class="sxs-lookup"><span data-stu-id="c7785-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="c7785-349">Fare clic su Piano tariffario e selezionare un piano tariffario appropriato per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c7785-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="c7785-350">Selezionare **Visualizza tutto** per visualizzare altre opzioni sui prezzi, ad esempio **Gratuito** e **Condiviso**.</span><span class="sxs-lookup"><span data-stu-id="c7785-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="c7785-351">Dopo aver scelto il livello di prezzo, fare clic su **Seleziona** .</span><span class="sxs-lookup"><span data-stu-id="c7785-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="c7785-352">Nel pannello **Piano di servizio app** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7785-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="c7785-353">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c7785-353">Click **Create**.</span></span> <span data-ttu-id="c7785-354">L'operazione di provisioning di un back-end dell'app per dispositivi mobili può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c7785-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="c7785-355">Dopo avere eseguito il provisioning del back-end dell'app per dispositivi mobili, nel portale viene aperto il pannello **Impostazioni** relativo al back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c7785-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="c7785-356">Una volta creato il back-end dell'app per dispositivi mobili, è possibile scegliere se connettere un database SQL esistente o creare un nuovo database SQL.</span><span class="sxs-lookup"><span data-stu-id="c7785-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="c7785-357">In questa sezione viene creato un database SQL.</span><span class="sxs-lookup"><span data-stu-id="c7785-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="c7785-358">Se nella stessa posizione del back-end dell'app per dispositivi mobili è già presente un database, è possibile scegliere **Usare un database esistente** e quindi selezionare questo database.</span><span class="sxs-lookup"><span data-stu-id="c7785-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="c7785-359">Non è consigliabile usare un database in una posizione diversa, a causa di latenze più elevate.</span><span class="sxs-lookup"><span data-stu-id="c7785-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="c7785-360">Nel nuovo back-end dell'app per dispositivi mobili fare clic su **Impostazioni** > **App per dispositivi mobili** > **Dati** > **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c7785-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="c7785-361">Nel pannello **Aggiungi connessione dati** fare clic su **Database SQL - Configurare le impostazioni necessarie** > **Crea un nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="c7785-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="c7785-362">Immettere il nome del nuovo database nel campo **Nome** .</span><span class="sxs-lookup"><span data-stu-id="c7785-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="c7785-363">Fare clic su **Server**.</span><span class="sxs-lookup"><span data-stu-id="c7785-363">Click **Server**.</span></span>  <span data-ttu-id="c7785-364">Nel pannello **Nuovo server** immettere un nome di server univoco nel campo **Nome server** e specificare un **Account di accesso amministratore server** e una **Password** idonei.</span><span class="sxs-lookup"><span data-stu-id="c7785-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="c7785-365">Verificare che l'opzione **Consenti ai servizi di Azure di accedere al server** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c7785-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="c7785-366">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7785-366">Click **OK**.</span></span>

    ![Creare un database SQL di Azure][6]
4. <span data-ttu-id="c7785-368">Nel pannello **Nuovo database** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7785-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="c7785-369">Nel pannello **Aggiungi connessione dati** selezionare **Stringa di connessione** e immettere l'account di accesso e la password forniti al momento della creazione del database.</span><span class="sxs-lookup"><span data-stu-id="c7785-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="c7785-370">Se si usa un database esistente, fornire le credenziali di accesso per il database.</span><span class="sxs-lookup"><span data-stu-id="c7785-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="c7785-371">Dopo averli immessi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7785-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="c7785-372">Nel pannello **Aggiungi connessione dati** fare nuovamente clic su **OK** per creare il database.</span><span class="sxs-lookup"><span data-stu-id="c7785-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="c7785-373">La creazione del database può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c7785-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="c7785-374">Usare l'area **Notifiche** per monitorare l'avanzamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c7785-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="c7785-375">L'avanzamento non viene eseguito se il database non è stato distribuito correttamente.</span><span class="sxs-lookup"><span data-stu-id="c7785-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="c7785-376">Al termine della distribuzione viene creata una stringa di connessione per l'istanza di database SQL nelle impostazioni dell'app del back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="c7785-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="c7785-377">È possibile visualizzare l'impostazione dell'app in **Impostazioni** > **Impostazioni dell'applicazione** > **Stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="c7785-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="c7785-378"><a name="howto-tables-auth"></a>Procedura: Richiedere l'autenticazione per l'accesso alle tabelle</span><span class="sxs-lookup"><span data-stu-id="c7785-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="c7785-379">Per usare l'autenticazione del servizio app con l'endpoint delle tabelle, è necessario prima configurare l'autenticazione del servizio app nel [Portale di Azure] .</span><span class="sxs-lookup"><span data-stu-id="c7785-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="c7785-380">Per altre informazioni sulla configurazione dell'autenticazione in un Servizio app di Azure, vedere la Guida alla configurazione per il provider di identità che si intende usare:</span><span class="sxs-lookup"><span data-stu-id="c7785-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="c7785-381">[Come configurare l'autenticazione di Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="c7785-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="c7785-382">[Come configurare l'autenticazione di Facebook]</span><span class="sxs-lookup"><span data-stu-id="c7785-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="c7785-383">[Come configurare l'autenticazione di Google]</span><span class="sxs-lookup"><span data-stu-id="c7785-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="c7785-384">[Come configurare l'autenticazione di Microsoft]</span><span class="sxs-lookup"><span data-stu-id="c7785-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="c7785-385">[Come configurare l'autenticazione di Twitter]</span><span class="sxs-lookup"><span data-stu-id="c7785-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="c7785-386">Ogni tabella ha una proprietà di accesso che può essere usata per controllare l'accesso alla tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="c7785-387">L'esempio seguente mostra una tabella definita in modo statico in cui è richiesta l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="c7785-388">La proprietà di accesso può assumere uno dei tre valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7785-388">The access property can take one of three values</span></span>

* <span data-ttu-id="c7785-389">*anonymous* indica che all'applicazione client è consentito leggere i dati senza autenticazione</span><span class="sxs-lookup"><span data-stu-id="c7785-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="c7785-390">*authenticated* indica che l'applicazione client deve inviare un token di autenticazione valido con la richiesta</span><span class="sxs-lookup"><span data-stu-id="c7785-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="c7785-391">*disabled* indica che la tabella è attualmente disabilitata.</span><span class="sxs-lookup"><span data-stu-id="c7785-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="c7785-392">Se la proprietà di accesso non è definita, è consentito l'accesso non autenticato.</span><span class="sxs-lookup"><span data-stu-id="c7785-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="c7785-393"><a name="howto-tables-getidentity"></a>Procedura: Usare le attestazioni di autenticazione con le tabelle</span><span class="sxs-lookup"><span data-stu-id="c7785-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="c7785-394">È possibile impostare diverse attestazioni richieste quando viene impostata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="c7785-395">Queste attestazioni non sono in genere disponibili tramite l'oggetto `context.user` .</span><span class="sxs-lookup"><span data-stu-id="c7785-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="c7785-396">È possibile tuttavia recuperarle usando il metodo `context.user.getIdentity()` .</span><span class="sxs-lookup"><span data-stu-id="c7785-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="c7785-397">Il metodo `getIdentity()` restituisce una promessa che viene risolta in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="c7785-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="c7785-398">L'oggetto viene associato a una chiave tramite il metodo di autenticazione (facebook, google, twitter, microsoftaccount o aad).</span><span class="sxs-lookup"><span data-stu-id="c7785-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="c7785-399">Ad esempio, se si configura l'autenticazione dell'account Microsoft e si richiede l'attestazione degli indirizzi di posta elettronica, è possibile aggiungere l'indirizzo di posta elettronica nel record con il controller tabelle seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="c7785-400">Per visualizzare le attestazioni disponibili, usare un browser Web per visualizzare l'endpoint `/.auth/me` del sito.</span><span class="sxs-lookup"><span data-stu-id="c7785-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="c7785-401"><a name="howto-tables-disabled"></a>Procedura: Disabilitare l'accesso a specifiche operazioni su tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="c7785-402">Oltre che sulla tabella, la proprietà di accesso può essere usata per controllare singole operazioni.</span><span class="sxs-lookup"><span data-stu-id="c7785-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="c7785-403">Sono disponibili quattro operazioni:</span><span class="sxs-lookup"><span data-stu-id="c7785-403">There are four operations:</span></span>

* <span data-ttu-id="c7785-404">*read* è l'operazione RESTful GET nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="c7785-405">*insert* è l'operazione POST RESTful sulla tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="c7785-406">*update* è l'operazione PATCH RESTful sulla tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="c7785-407">*delete* è l'operazione RESTful DELETE nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="c7785-408">Si supponga, ad esempio, di voler fornire una tabella non autenticata di sola lettura:</span><span class="sxs-lookup"><span data-stu-id="c7785-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="c7785-409"><a name="howto-tables-query"></a>Procedura: Modificare la query usata con le operazioni su tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="c7785-410">Un requisito comune per le operazioni su tabella è consentire una visualizzazione con restrizioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7785-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="c7785-411">Ad esempio, è possibile fornire una tabella contrassegnata con l'ID dell'utente autenticato in modo sia possibile solo leggere o aggiornare i propri record.</span><span class="sxs-lookup"><span data-stu-id="c7785-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="c7785-412">La definizione di tabella riportata di seguito fornisce questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="c7785-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="c7785-413">Le operazioni che in genere eseguono una query avranno una proprietà query modificabile con una clausola where.</span><span class="sxs-lookup"><span data-stu-id="c7785-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="c7785-414">La proprietà query è un oggetto [QueryJS] usato per convertire una query OData in qualcosa che il back-end dei dati possa elaborare.</span><span class="sxs-lookup"><span data-stu-id="c7785-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="c7785-415">Per i casi di semplice uguaglianza, come quello riportato in precedenza, è possibile usare una mappa.</span><span class="sxs-lookup"><span data-stu-id="c7785-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="c7785-416">È anche possibile aggiungere clausole SQL specifiche:</span><span class="sxs-lookup"><span data-stu-id="c7785-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="c7785-417"><a name="howto-tables-softdelete"></a>Procedura: Configurare l'eliminazione temporanea in una tabella</span><span class="sxs-lookup"><span data-stu-id="c7785-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="c7785-418">L'eliminazione temporanea non elimina effettivamente i record.</span><span class="sxs-lookup"><span data-stu-id="c7785-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="c7785-419">Al contrario, questi vengono contrassegnati come eliminati nel database impostando la colonna relativa all'eliminazione su true.</span><span class="sxs-lookup"><span data-stu-id="c7785-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="c7785-420">L'SDK di App per dispositivi mobili di Azure rimuove automaticamente dai risultati i record con eliminazione temporanea, a meno che l'SDK del client mobile non usi il metodo IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="c7785-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="c7785-421">Per configurare una tabella per l'eliminazione temporanea, impostare la proprietà `softDelete` nel file di definizione della tabella:</span><span class="sxs-lookup"><span data-stu-id="c7785-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="c7785-422">È necessario stabilire un meccanismo per l'eliminazione dei record, che sia da un'applicazione client, con un processo Web, tramite Funzioni di Azure o un'API personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c7785-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="c7785-423"><a name="howto-tables-seeding"></a>Procedura: Eseguire il seeding dei dati nel database</span><span class="sxs-lookup"><span data-stu-id="c7785-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="c7785-424">Quando si crea una nuova applicazione, è consigliabile eseguire il seeding dei dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="c7785-425">Questa operazione può essere eseguita all'interno del file JavaScript di definizione della tabella, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c7785-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="c7785-426">Il seeding dei dati viene eseguito solo quando la tabella viene creata dall'SDK di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7785-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="c7785-427">Se la tabella esiste già all'interno del database, non verranno inseriti dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="c7785-428">Se lo schema dinamico è abilitato, lo schema viene dedotto dai dati di seeding.</span><span class="sxs-lookup"><span data-stu-id="c7785-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="c7785-429">È consigliabile chiamare in modo esplicito il metodo `tables.initialize()` per creare la tabella all'avvio dell'esecuzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="c7785-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="c7785-430"><a name="Swagger"></a>Procedura: Abilitare il supporto di Swagger</span><span class="sxs-lookup"><span data-stu-id="c7785-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="c7785-431">Le app per dispositivi mobili del servizio app di Azure sono fornite con il supporto di [Swagger] incorporato.</span><span class="sxs-lookup"><span data-stu-id="c7785-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="c7785-432">Per abilitare il supporto di Swagger, installare prima di tutto swagger-ui come una dipendenza:</span><span class="sxs-lookup"><span data-stu-id="c7785-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="c7785-433">Una volta installato, è possibile abilitare il supporto di Swagger nel costruttore di app per dispositivi mobili di Azure:</span><span class="sxs-lookup"><span data-stu-id="c7785-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="c7785-434">È consigliabile abilitare il supporto di Swagger solo nelle edizioni di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="c7785-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="c7785-435">È possibile farlo usando l'impostazione dell'app `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="c7785-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="c7785-436">L'endpoint swagger sarà posizionato in http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="c7785-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="c7785-437">È possibile accedere all'interfaccia utente di Swagger tramite l'endpoint `/swagger/ui` .</span><span class="sxs-lookup"><span data-stu-id="c7785-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="c7785-438">Se si sceglie di richiedere l'autenticazione a livello dell'intera applicazione., Swagger genera un errore.</span><span class="sxs-lookup"><span data-stu-id="c7785-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="c7785-439">Per ottenere risultati ottimali, scegliere di consentire le richieste non autenticate tramite le impostazioni di autenticazione/autorizzazione del Servizio app di Azure e quindi controllare l'autenticazione con la proprietà `table.access` .</span><span class="sxs-lookup"><span data-stu-id="c7785-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="c7785-440">È anche possibile aggiungere l'opzione Swagger al file `azureMobile.js` se si vuole supportare Swagger solo quando si sviluppa in locale.</span><span class="sxs-lookup"><span data-stu-id="c7785-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="c7785-441"><a name="push">Notifiche push</span><span class="sxs-lookup"><span data-stu-id="c7785-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="c7785-442">App per dispositivi mobili si integra con Hub di notifica di Azure per consentire l'invio di notifiche push mirate a milioni di dispositivi basati sulle piattaforme principali.</span><span class="sxs-lookup"><span data-stu-id="c7785-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="c7785-443">Con Hub di notifica è possibile inviare notifiche push a dispositivi iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="c7785-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="c7785-444">Per altre informazioni su tutte le operazioni disponibili con Hub di notifica, vedere [Panoramica dell'Hub di notifica di Azure](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7785-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="c7785-445"></a><a name="send-push"></a>Procedura: Inviare notifiche push</span><span class="sxs-lookup"><span data-stu-id="c7785-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="c7785-446">Il codice seguente illustra come usare l'oggetto push per inviare una notifica push di trasmissione ai dispositivi iOS registrati:</span><span class="sxs-lookup"><span data-stu-id="c7785-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="c7785-447">Creando una registrazione push con modello dal client, è possibile inviare un messaggio di push con modello ai dispositivi basati su tutte le piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="c7785-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="c7785-448">Il codice seguente illustra come inviare una notifica con modello:</span><span class="sxs-lookup"><span data-stu-id="c7785-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="c7785-449"><a name="push-user"></a>Procedura: Inviare notifiche push agli utenti autenticati tramite tag</span><span class="sxs-lookup"><span data-stu-id="c7785-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="c7785-450">Se un utente autenticato esegue la registrazione per le notifiche push, viene automaticamente aggiunto un tag con l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="c7785-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="c7785-451">Tramite questo tag, è possibile inviare notifiche push a tutti i dispositivi registrati da un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="c7785-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="c7785-452">Il codice seguente ottiene il SID dell'utente che esegue la richiesta e invia un modello di notifica push a ogni registrazione del dispositivo per tale utente:</span><span class="sxs-lookup"><span data-stu-id="c7785-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="c7785-453">Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="c7785-454"><a name="CustomAPI"></a> API personalizzate</span><span class="sxs-lookup"><span data-stu-id="c7785-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="c7785-455"><a name="howto-customapi-basic"></a>Procedura: Definire un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="c7785-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="c7785-456">Oltre all'API di accesso ai dati attraverso l'endpoint /tables, App per dispositivi mobili di Azure può fornire la copertura per le API personalizzate.</span><span class="sxs-lookup"><span data-stu-id="c7785-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="c7785-457">Le API personalizzate sono definite in modo analogo alle definizioni di tabella e possono accedere alle stesse funzionalità, inclusa l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="c7785-458">Per usare l'autenticazione del servizio app con un'API personalizzata, è necessario prima configurare l'autenticazione del servizio app nel [Portale di Azure] .</span><span class="sxs-lookup"><span data-stu-id="c7785-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="c7785-459">Per altre informazioni sulla configurazione dell'autenticazione in un Servizio app di Azure, vedere la Guida alla configurazione per il provider di identità che si intende usare:</span><span class="sxs-lookup"><span data-stu-id="c7785-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="c7785-460">[Come configurare l'autenticazione di Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="c7785-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="c7785-461">[Come configurare l'autenticazione di Facebook]</span><span class="sxs-lookup"><span data-stu-id="c7785-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="c7785-462">[Come configurare l'autenticazione di Google]</span><span class="sxs-lookup"><span data-stu-id="c7785-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="c7785-463">[Come configurare l'autenticazione di Microsoft]</span><span class="sxs-lookup"><span data-stu-id="c7785-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="c7785-464">[Come configurare l'autenticazione di Twitter]</span><span class="sxs-lookup"><span data-stu-id="c7785-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="c7785-465">Le API personalizzate vengono definite in modo molto simile alle API di tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="c7785-466">Creare una directory **api** .</span><span class="sxs-lookup"><span data-stu-id="c7785-466">Create an **api** directory</span></span>
2. <span data-ttu-id="c7785-467">Creare un file JavaScript di definizione dell'API nella directory **api** .</span><span class="sxs-lookup"><span data-stu-id="c7785-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="c7785-468">Usare il metodo di importazione per importare la directory **api** .</span><span class="sxs-lookup"><span data-stu-id="c7785-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="c7785-469">Di seguito è riportata la definizione dell'API prototipo basata sull'esempio di app di base usato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7785-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="c7785-470">Si prenda ad esempio un'API che restituisce la data del server usando il metodo *Date.now()* .</span><span class="sxs-lookup"><span data-stu-id="c7785-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="c7785-471">Il file api/date.js è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c7785-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="c7785-472">Ogni parametro è uno dei verbi RESTful standard: GET, POST, PATCH o DELETE.</span><span class="sxs-lookup"><span data-stu-id="c7785-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="c7785-473">Il metodo è una funzione [ExpressJS Middleware] standard che invia l'output richiesto.</span><span class="sxs-lookup"><span data-stu-id="c7785-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="c7785-474"><a name="howto-customapi-auth"></a>Procedura: Richiedere l'autenticazione per l'accesso a un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="c7785-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="c7785-475">L'SDK di App per dispositivi mobili di Azure implementa l'autenticazione nello stesso modo sia per l'endpoint delle tabelle che per le API personalizzate.</span><span class="sxs-lookup"><span data-stu-id="c7785-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="c7785-476">Per aggiungere l'autenticazione all'API sviluppata nella sezione precedente, aggiungere una proprietà **access** :</span><span class="sxs-lookup"><span data-stu-id="c7785-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="c7785-477">È anche possibile specificare l'autenticazione su operazioni specifiche:</span><span class="sxs-lookup"><span data-stu-id="c7785-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="c7785-478">Lo stesso token usato per l'endpoint delle tabelle deve essere usato per le API personalizzate che richiedono l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="c7785-479"><a name="howto-customapi-auth"></a>Procedura: Gestire il caricamento di file di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="c7785-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="c7785-480">L'SDK delle app per dispositivi mobili di Azure usa il [middleware body-parser](https://github.com/expressjs/body-parser) per accettare e decodificare il contenuto del corpo nell'elemento inviato.</span><span class="sxs-lookup"><span data-stu-id="c7785-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="c7785-481">È possibile preconfigurare il body-parser per accettare caricamenti di file più grandi:</span><span class="sxs-lookup"><span data-stu-id="c7785-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="c7785-482">Il file ha una codifica in base 64 prima della trasmissione,</span><span class="sxs-lookup"><span data-stu-id="c7785-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="c7785-483">che aumenterà le dimensioni del caricamento effettivo e di cui è quindi necessario tenere conto.</span><span class="sxs-lookup"><span data-stu-id="c7785-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="c7785-484"><a name="howto-customapi-sql"></a>Procedura: Eseguire istruzioni SQL personalizzate</span><span class="sxs-lookup"><span data-stu-id="c7785-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="c7785-485">Con Azure Mobile App SDK è possibile accedere all'intero contesto tramite l'oggetto request, consentendo di eseguire facilmente istruzioni SQL con parametri sul provider di dati definito:</span><span class="sxs-lookup"><span data-stu-id="c7785-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="c7785-486"><a name="Debugging"></a>Debug, tabelle semplici e API semplici</span><span class="sxs-lookup"><span data-stu-id="c7785-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="c7785-487"><a name="howto-diagnostic-logs"></a>Procedura: Eseguire il debug e diagnosticare e risolvere i problemi di App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="c7785-488">Il Servizio app di Azure offre diverse tecniche di debug e risoluzione dei problemi per le applicazioni Node.js.</span><span class="sxs-lookup"><span data-stu-id="c7785-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="c7785-489">Per iniziare la risoluzione dei problemi del back-end Node.js Mobile, consultare i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="c7785-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="c7785-490">[Monitoraggio di un servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="c7785-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="c7785-491">[Abilitazione della registrazione diagnostica nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="c7785-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="c7785-492">[Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c7785-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="c7785-493">Le applicazioni Node.js hanno accesso a un'ampia gamma di strumenti per i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c7785-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="c7785-494">Al suo interno l'SDK di Node.js per App per dispositivi mobili di Azure usa [Winston] per la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c7785-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="c7785-495">La registrazione viene abilitata automaticamente abilitando la modalità di debug o impostando su true l'impostazione dell'app **MS_DebugMode** nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="c7785-496">I log generati vengono visualizzati tra i log di diagnostica del [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c7785-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="c7785-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procedura: Usare tabelle semplici nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="c7785-498">L'impostazione Easy Tables nel portale consente di creare e usare tabelle direttamente nel portale.</span><span class="sxs-lookup"><span data-stu-id="c7785-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="c7785-499">Consente anche di modificare le operazioni di tabella usando l'editor del servizio app.</span><span class="sxs-lookup"><span data-stu-id="c7785-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="c7785-500">Quando si fa clic su **Tabelle semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare una tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="c7785-501">È anche possibile visualizzare i dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-501">You can also see data in the table.</span></span>

![Utilizzare Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="c7785-503">I comandi seguenti sono disponibili sulla barra dei comandi di una tabella:</span><span class="sxs-lookup"><span data-stu-id="c7785-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="c7785-504">**Modifica autorizzazioni** : è possibile modificare l'autorizzazione per le operazioni di lettura, inserimento, aggiornamento ed eliminazione di operazioni sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="c7785-505">Le opzioni consentono di eseguire l'accesso anonimo, richiedere l'autenticazione o disabilitare qualunque tipo di accesso all'operazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="c7785-506">**Modifica script** : il file di script per la tabella viene aperto nell'editor del servizio app.</span><span class="sxs-lookup"><span data-stu-id="c7785-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="c7785-507">**Gestisci schema** : è possibile aggiungere o eliminare le colonne o modificare l'indice di tabella.</span><span class="sxs-lookup"><span data-stu-id="c7785-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="c7785-508">**Cancella tabella** : tronca una tabella esistente eliminando tutte le righe di dati ma lasciando lo schema invariato.</span><span class="sxs-lookup"><span data-stu-id="c7785-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="c7785-509">**Elimina righe** : è possibile eliminare singole righe di dati.</span><span class="sxs-lookup"><span data-stu-id="c7785-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="c7785-510">**Visualizzare log di streaming** : consente di connettersi al servizio di log in streaming del sito.</span><span class="sxs-lookup"><span data-stu-id="c7785-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="c7785-511"><a name="work-easy-apis"></a>Procedura: Usare Easy APIs nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c7785-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="c7785-512">L'impostazione Easy APIs nel portale consentono di creare e usare API personalizzate direttamente nel portale.</span><span class="sxs-lookup"><span data-stu-id="c7785-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="c7785-513">È possibile modificare gli script dell'API usando l'editor del servizio app.</span><span class="sxs-lookup"><span data-stu-id="c7785-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="c7785-514">Quando si fa clic su **API semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare un endpoint API personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c7785-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Utilizzare Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="c7785-516">Nel portale è possibile modificare le autorizzazioni di accesso per una determinata azione HTTP, modificare il file di script dell'API nell'editor del servizio app o visualizzare i log in streaming.</span><span class="sxs-lookup"><span data-stu-id="c7785-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="c7785-517"><a name="online-editor"></a>Procedura: Modificare il codice nell'editor del servizio app</span><span class="sxs-lookup"><span data-stu-id="c7785-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="c7785-518">Il portale di Azure consente di modificare i file di script del back-end Node.js nell'editor del servizio app senza dover scaricare il progetto nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="c7785-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="c7785-519">Per modificare i file di script nell'editor online:</span><span class="sxs-lookup"><span data-stu-id="c7785-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="c7785-520">Nel pannello del back-end dell'app per dispositivi mobili fare clic su **Tutte le impostazioni** > **Easy tables** o **Easy APIs**, fare clic su una tabella o un'API e quindi su **Modifica script**.</span><span class="sxs-lookup"><span data-stu-id="c7785-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="c7785-521">Il file di script viene aperto nell'editor del servizio app.</span><span class="sxs-lookup"><span data-stu-id="c7785-521">The script file is opened in the App Service Editor.</span></span>

    ![Editor del servizio app](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="c7785-523">Apportare le modifiche al file di codice nell'editor online.</span><span class="sxs-lookup"><span data-stu-id="c7785-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="c7785-524">Le modifiche vengono salvate automaticamente durante la digitazione.</span><span class="sxs-lookup"><span data-stu-id="c7785-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="c7785-525">[Avvio rapido di client Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="c7785-526">[Avvio rapido di client Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="c7785-527">[Avvio rapido di client iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="c7785-528">[Avvio rapido di client Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="c7785-529">[Avvio rapido di client Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="c7785-530">[Avvio rapido di client Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="c7785-531">[Avvio rapido di client Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c7785-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="c7785-532">[sincronizzazione dati offline]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="c7785-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="c7785-533">[Come configurare l'autenticazione di Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c7785-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="c7785-534">[Come configurare l'autenticazione di Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c7785-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="c7785-535">[Come configurare l'autenticazione di Google]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c7785-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="c7785-536">[Come configurare l'autenticazione di Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c7785-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="c7785-537">[Come configurare l'autenticazione di Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c7785-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="c7785-538">[Guida alla distribuzione del servizio app di Azure]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="c7785-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="c7785-539">[Monitoraggio di un servizio app di Azure]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="c7785-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="c7785-540">[Abilitazione della registrazione diagnostica nel servizio app di Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="c7785-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="c7785-541">[Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="c7785-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="c7785-542">[specificare la versione di Node.js]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="c7785-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="c7785-543">[usare i moduli di Node]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="c7785-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="c7785-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="c7785-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="c7785-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="c7785-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="c7785-546">[Portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="c7785-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="c7785-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="c7785-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="c7785-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="c7785-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="c7785-549">[esempio basicapp in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="c7785-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="c7785-550">[esempio todo in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="c7785-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="c7785-551">[directory degli esempi in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="c7785-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="c7785-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="c7785-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="c7785-553">[Strumenti Node.js 1.1 per Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="c7785-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="c7785-554">[pacchetto mssql per Node.js]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="c7785-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="c7785-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="c7785-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="c7785-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="c7785-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="c7785-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="c7785-557">[Winston]: https://github.com/winstonjs/winston</span></span>
