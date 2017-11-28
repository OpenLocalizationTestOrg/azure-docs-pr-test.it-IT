---
title: toowork aaaHow con i server back-end di hello Node.js SDK per App per dispositivi mobili | Documenti Microsoft
description: Informazioni su come toowork con hello server back-end di Node.js SDK per App Mobile di servizio App di Azure.
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="3c607-103">Come toouse hello Azure Mobile App Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="3c607-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="3c607-104">In questo articolo fornisce informazioni dettagliate ed esempi che mostrano come toowork con un back-end di Node.js in Azure App Service App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="3c607-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="3c607-105"><a name="Introduction"></a>Introduzione</span><span class="sxs-lookup"><span data-stu-id="3c607-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="3c607-106">App per dispositivi mobili Azure App Service fornisce hello funzionalità tooadd ottimizzato mobile l'accesso ai dati dell'applicazione web di tooa API Web.</span><span class="sxs-lookup"><span data-stu-id="3c607-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="3c607-107">Hello Azure App Service Mobile App SDK è disponibile per applicazioni web ASP.NET e Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c607-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="3c607-108">Hello SDK fornisce hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="3c607-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="3c607-109">Operazioni su tabella (read, insert, update, delete) per l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="3c607-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="3c607-110">Operazioni sulle API personalizzate</span><span class="sxs-lookup"><span data-stu-id="3c607-110">Custom API operations</span></span>

<span data-ttu-id="3c607-111">Entrambe le operazioni permettono l'autenticazione in tutti i provider di identità consentiti dal servizio app di Azure, inclusi i provider di identità basati su social network, ad esempio Facebook, Twitter, Google e Microsoft nonché Azure Active Directory per l'identità aziendale.</span><span class="sxs-lookup"><span data-stu-id="3c607-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="3c607-112">È possibile trovare esempi per ogni caso d'usano in hello [directory esempi su GitHub].</span><span class="sxs-lookup"><span data-stu-id="3c607-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="3c607-113">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="3c607-113">Supported Platforms</span></span>
<span data-ttu-id="3c607-114">Hello Azure Mobile App nodo SDK supporta hello che LTS corrente di rilascio del nodo e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3c607-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="3c607-115">A partire dalla scrittura, hello LTS più recente è v4.5.0 di nodo.</span><span class="sxs-lookup"><span data-stu-id="3c607-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="3c607-116">Altre versioni di Node potrebbero funzionare, ma non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="3c607-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="3c607-117">Hello SDK nodo App Mobile di Azure supporta due driver di database - hello nodo mssql driver supporta SQL Azure e le istanze di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="3c607-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="3c607-118">driver sqlite3 Hello supporta database SQLite in una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="3c607-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="3c607-119"><a name="howto-cmdline-basicapp"></a>Procedura: creare un back-end di base Node.js tramite hello riga di comando</span><span class="sxs-lookup"><span data-stu-id="3c607-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="3c607-120">Ogni back-end Node.js per le app per dispositivi mobili del servizio app di Azure viene avviato come applicazione ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="3c607-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="3c607-121">ExpressJS è hello più popolari framework del servizio web disponibile per Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c607-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="3c607-122">È possibile creare un'applicazione [Express] di base seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c607-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="3c607-123">Creare una directory per il progetto in una finestra di comando o di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c607-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="3c607-124">Eseguire la struttura del pacchetto npm init tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="3c607-125">comando di Hello npm init chiede un insieme di progetti di hello tooinitialize domande.</span><span class="sxs-lookup"><span data-stu-id="3c607-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="3c607-126">Vedere l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-126">See hello example output:</span></span>

    ![output di Hello npm init][0]
3. <span data-ttu-id="3c607-128">Installare le librerie di express e App mobili di azure hello dal repository npm hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="3c607-129">Creare un app.js file tooimplement hello mobili server di base.</span><span class="sxs-lookup"><span data-stu-id="3c607-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="3c607-130">Questa applicazione crea un WebAPI ottimizzata con un singolo endpoint (`/tables/TodoItem`) che fornisce l'accesso non autenticato tooan sottostante l'archivio dati SQL tramite uno schema dinamico.</span><span class="sxs-lookup"><span data-stu-id="3c607-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="3c607-131">È adatta per l'avvio rapido delle librerie client seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c607-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="3c607-132">[Avvio rapido di client Android]</span><span class="sxs-lookup"><span data-stu-id="3c607-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="3c607-133">[Avvio rapido di client Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="3c607-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="3c607-134">[Avvio rapido di client iOS]</span><span class="sxs-lookup"><span data-stu-id="3c607-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="3c607-135">[Avvio rapido di client Windows Store]</span><span class="sxs-lookup"><span data-stu-id="3c607-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="3c607-136">[Avvio rapido di client Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="3c607-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="3c607-137">[Avvio rapido di client Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="3c607-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="3c607-138">[Avvio rapido di client Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="3c607-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="3c607-139">È possibile trovare codice hello per questa applicazione di base hello [esempio basicapp in GitHub].</span><span class="sxs-lookup"><span data-stu-id="3c607-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="3c607-140"><a name="howto-vs2015-basicapp"></a>Procedura: Creare un back-end Node.js con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3c607-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="3c607-141">Visual Studio 2015 richiede delle applicazioni Node.js toodevelop estensione all'interno di hello IDE.</span><span class="sxs-lookup"><span data-stu-id="3c607-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="3c607-142">toostart, installare hello [Node.js Tools 1.1 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3c607-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="3c607-143">Una volta installati hello Node.js Tools per Visual Studio, creare un'applicazione di 4. x Express:</span><span class="sxs-lookup"><span data-stu-id="3c607-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="3c607-144">Aprire hello **nuovo progetto** finestra di dialogo (da **File** > **New** > **progetto...** ).</span><span class="sxs-lookup"><span data-stu-id="3c607-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="3c607-145">Espandere **Modelli** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="3c607-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="3c607-146">Seleziona hello **base Azure Node.js Express 4 applicazione**.</span><span class="sxs-lookup"><span data-stu-id="3c607-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="3c607-147">Inserire il nome di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-147">Fill in hello project name.</span></span>  <span data-ttu-id="3c607-148">Fare clic su *OK*.</span><span class="sxs-lookup"><span data-stu-id="3c607-148">Click *OK*.</span></span>

    ![Nuovo progetto di Visual Studio 2015][1]
5. <span data-ttu-id="3c607-150">Pulsante destro del mouse hello **npm** nodo e selezionare **installare nuovi pacchetti npm...** .</span><span class="sxs-lookup"><span data-stu-id="3c607-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="3c607-151">Potrebbe essere necessario catalogo di npm toorefresh hello nella creazione di un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c607-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="3c607-152">Fare clic su **Refresh** (Aggiorna), se necessario.</span><span class="sxs-lookup"><span data-stu-id="3c607-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="3c607-153">Immettere *App mobili di azure* nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="3c607-154">Fare clic su hello **-App mobili di azure-2.0.0** del pacchetto, quindi fare clic su **Installa pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="3c607-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Installare nuovi pacchetti npm][2]
8. <span data-ttu-id="3c607-156">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="3c607-156">Click **Close**.</span></span>
9. <span data-ttu-id="3c607-157">Aprire hello *app.js* tooadd supporto per applicazioni mobili di Azure SDK hello file.</span><span class="sxs-lookup"><span data-stu-id="3c607-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="3c607-158">Nella parte inferiore di riga 6 at hello della libreria hello richiedono istruzioni, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="3c607-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="3c607-159">Circa riga 27 dopo hello altre istruzioni app.use, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="3c607-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="3c607-160">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-160">Save hello file.</span></span>
10. <span data-ttu-id="3c607-161">Eseguire un'applicazione hello in locale (Buongiorno API viene pubblicato su http://localhost:3000) oppure pubblicare tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3c607-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="3c607-162"><a name="create-node-backend-portal"></a>Procedura: creare un back-end di Node.js tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c607-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="3c607-163">È possibile creare un diritto di back-end delle App per dispositivi mobili in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="3c607-164">Eseguire hello seguenti passaggi oppure creare un client e server insieme seguente hello [creare un'app per dispositivi mobili](app-service-mobile-ios-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="3c607-165">esercitazione Hello contiene una versione semplificata di queste istruzioni ed è ottimale per la prova dei progetti concetto.</span><span class="sxs-lookup"><span data-stu-id="3c607-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="3c607-166">In hello *iniziare* pannello, in **creare una tabella API**, scegliere **Node.js** come il **language back-end**.</span><span class="sxs-lookup"><span data-stu-id="3c607-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="3c607-167">Casella hello per "**sono consapevole che verranno sovrascritti tutti i contenuti del sito.**", quindi fare clic su **tabella TodoItem creare**.</span><span class="sxs-lookup"><span data-stu-id="3c607-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="3c607-168"><a name="download-quickstart"></a>Procedura: Download hello Node.js back-end delle Guide rapide progetto di codice tramite Git</span><span class="sxs-lookup"><span data-stu-id="3c607-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="3c607-169">Quando si crea un back-end dell'App Mobile Node.js tramite il portale di hello **introduttiva** pannello creato un progetto di Node.js per l'utente e del sito tooyour distribuito.</span><span class="sxs-lookup"><span data-stu-id="3c607-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="3c607-170">È possibile aggiungere tabelle e le API e modificare i file di codice back-end Node.js hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="3c607-171">È anche possibile utilizzare vari strumenti toodownload hello back-end progetto di distribuzione di in modo che è possibile aggiungere o modificare tabelle e le API, quindi pubblicare di nuovo il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="3c607-172">Per altre informazioni, vedere la [Guida alla distribuzione del servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="3c607-173">Hello procedura seguente usa un codice del progetto Git repository toodownload hello Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="3c607-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="3c607-174">Se non è già stato fatto, installare Git.</span><span class="sxs-lookup"><span data-stu-id="3c607-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="3c607-175">Hello passaggi necessari tooinstall Git variano tra i sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="3c607-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="3c607-176">Vedere la sezione [Installazione di Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) per indicazioni specifiche del sistema operativo relative a distribuzioni e installazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="3c607-177">Seguire i passaggi di hello in [Enable hello repository di applicazione di servizio App](../app-service-web/app-service-deploy-local-git.md#Step3) repository Git di hello tooenable per il sito di back-end, prendendo nota di hello distribuzione username e password.</span><span class="sxs-lookup"><span data-stu-id="3c607-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="3c607-178">Nel Pannello di hello per il back-end dell'App Mobile, prendere nota di hello **URL clone Git** impostazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="3c607-179">Eseguire hello `git clone` comando utilizzando l'URL del clone Git hello, immettere la password quando richiesto, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3c607-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="3c607-180">Si noti che i file di progetto e esplorazione toolocal directory, ovvero nel precedente esempio hello /todolist, sono stati scaricati.</span><span class="sxs-lookup"><span data-stu-id="3c607-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="3c607-181">Individuare hello `todoitem.json` file hello `/tables` directory.</span><span class="sxs-lookup"><span data-stu-id="3c607-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="3c607-182">Questo file definisce le autorizzazioni sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="3c607-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="3c607-183">Anche trovare hello `todoitem.js` file hello stessa directory, che definisce l'operazione CRUD di script per tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="3c607-184">Dopo avere apportato modifiche tooproject file, eseguire hello comandi tooadd, eseguire il commit, quindi caricare il sito toohello le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c607-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="3c607-185">Quando si aggiungono nuovi file di progetto toohello, è necessario innanzitutto hello tooexecute `git add .` comando.</span><span class="sxs-lookup"><span data-stu-id="3c607-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="3c607-186">sito Hello viene ripubblicata senza modifiche ogni volta che un nuovo set di operazioni di commit viene inserito il sito toohello.</span><span class="sxs-lookup"><span data-stu-id="3c607-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="3c607-187"><a name="howto-publish-to-azure"></a>Procedura: pubblicare il tooAzure back-end di Node.js</span><span class="sxs-lookup"><span data-stu-id="3c607-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="3c607-188">Microsoft Azure offre numerosi meccanismi per la pubblicazione di Azure App Service Mobile App Node.js back-end per hello servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c607-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="3c607-189">tra cui l'uso di strumenti di distribuzione integrati in Visual Studio, strumenti da riga di comando e opzioni di distribuzione continua basate sul controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="3c607-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="3c607-190">Per altre informazioni su questo argomento, vedere la [Guida alla distribuzione del servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="3c607-191">Il servizio app di Azure include suggerimenti specifici per l'applicazione Node.js che è consigliabile esaminare prima della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="3c607-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="3c607-192">Come troppo[specificare hello nodo versione]</span><span class="sxs-lookup"><span data-stu-id="3c607-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="3c607-193">Come troppo[utilizzare i moduli del nodo]</span><span class="sxs-lookup"><span data-stu-id="3c607-193">How too[use Node modules]</span></span>

### <span data-ttu-id="3c607-194"><a name="howto-enable-homepage"></a>Procedura: Abilitare una home page dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3c607-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="3c607-195">Molte applicazioni sono una combinazione di web e App per dispositivi mobili e framework ExpressJS hello consente toocombine due facet.</span><span class="sxs-lookup"><span data-stu-id="3c607-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="3c607-196">In alcuni casi, tuttavia, è preferibile tooonly implementare un'interfaccia per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="3c607-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="3c607-197">È utile tooprovide che un servizio app di hello tooensure di pagina di destinazione sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3c607-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="3c607-198">È possibile fornire la propria home page o abilitarne una temporanea.</span><span class="sxs-lookup"><span data-stu-id="3c607-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="3c607-199">tooenable una home page temporanea, utilizzare hello seguente tooinstantiate App mobili di Azure:</span><span class="sxs-lookup"><span data-stu-id="3c607-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="3c607-200">Se si desidera questa opzione è disponibile solo quando si sviluppa in locale, è possibile aggiungere questa impostazione tooyour `azureMobile.js` file.</span><span class="sxs-lookup"><span data-stu-id="3c607-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="3c607-201"><a name="TableOperations"></a>Operazioni su tabella</span><span class="sxs-lookup"><span data-stu-id="3c607-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="3c607-202">Hello Server Node.js di App mobili di azure SDK fornisce meccanismi tooexpose dati archiviate nel Database di SQL Azure come un WebAPI tabelle.</span><span class="sxs-lookup"><span data-stu-id="3c607-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="3c607-203">Sono disponibili cinque operazioni.</span><span class="sxs-lookup"><span data-stu-id="3c607-203">Five operations are provided.</span></span>

| <span data-ttu-id="3c607-204">Operazione</span><span class="sxs-lookup"><span data-stu-id="3c607-204">Operation</span></span> | <span data-ttu-id="3c607-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c607-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c607-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="3c607-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="3c607-207">Ottenere tutti i record nella tabella di hello</span><span class="sxs-lookup"><span data-stu-id="3c607-207">Get all records in hello table</span></span> |
| <span data-ttu-id="3c607-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="3c607-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="3c607-209">Ottenere un record specifico nella tabella di hello</span><span class="sxs-lookup"><span data-stu-id="3c607-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="3c607-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="3c607-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="3c607-211">Creare un record nella tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-211">Create a record in hello table</span></span> |
| <span data-ttu-id="3c607-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="3c607-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="3c607-213">Aggiornare un record nella tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-213">Update a record in hello table</span></span> |
| <span data-ttu-id="3c607-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="3c607-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="3c607-215">Eliminare un record nella tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-215">Delete a record in hello table</span></span> |

<span data-ttu-id="3c607-216">Supporta questa WebAPI [OData] ed estende hello tabella dello schema toosupport [sincronizzazione dati offline].</span><span class="sxs-lookup"><span data-stu-id="3c607-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="3c607-217"><a name="howto-dynamicschema"></a>Procedura: Definire le tabelle con uno schema dinamico</span><span class="sxs-lookup"><span data-stu-id="3c607-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="3c607-218">Perché sia possibile usare una tabella, è necessario prima definirla.</span><span class="sxs-lookup"><span data-stu-id="3c607-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="3c607-219">Le tabelle possono essere definite con uno schema statico (dove developer hello definisce colonne hello all'interno dello schema hello) o in modo dinamico (dove hello SDK controlli schema hello in base alle richieste in ingresso).</span><span class="sxs-lookup"><span data-stu-id="3c607-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="3c607-220">Inoltre, sviluppatore hello è possibile controllare aspetti specifici di hello WebAPI aggiungendo definizione toohello del codice Javascript.</span><span class="sxs-lookup"><span data-stu-id="3c607-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="3c607-221">Come procedura consigliata, è necessario definire ogni tabella in un file Javascript nella directory di tabelle hello, quindi utilizzare le tabelle di hello tables.import() tooimport metodo.</span><span class="sxs-lookup"><span data-stu-id="3c607-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="3c607-222">Estensione basic-app hello, sarebbe possibile regolare file app.js hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="3c607-223">Definire la tabella hello. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="3c607-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="3c607-224">Per impostazione predefinita, le tabelle usano lo schema dinamico.</span><span class="sxs-lookup"><span data-stu-id="3c607-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="3c607-225">tooturn disattivare lo schema dinamico impostato a livello globale, hello impostazione App **MS_DynamicSchema** toofalse all'interno di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c607-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="3c607-226">È possibile trovare un esempio completo in hello [esempio todo in GitHub].</span><span class="sxs-lookup"><span data-stu-id="3c607-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="3c607-227"><a name="howto-staticschema"></a>Procedura: Definire le tabelle con uno schema statico</span><span class="sxs-lookup"><span data-stu-id="3c607-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="3c607-228">È possibile definire in modo esplicito hello colonne tooexpose tramite hello WebAPI.</span><span class="sxs-lookup"><span data-stu-id="3c607-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="3c607-229">Hello che App mobili di azure Node.js SDK aggiunge automaticamente eventuali colonne aggiuntive, necessarie per dati non in linea sincronizzazione toohello elenco fornito.</span><span class="sxs-lookup"><span data-stu-id="3c607-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="3c607-230">Ad esempio, le applicazioni client di avvio rapido richiedono una tabella con due colonne: text (una stringa) e complete (un valore booleano).</span><span class="sxs-lookup"><span data-stu-id="3c607-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="3c607-231">tabella Hello può essere definita in hello tabella JavaScript file di definizione (che si trova nella directory di tabelle hello) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c607-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="3c607-232">Se si definiscono le tabelle in modo statico, è necessario chiamare anche lo schema del database hello toocreate metodo tables.initialize() hello all'avvio.</span><span class="sxs-lookup"><span data-stu-id="3c607-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="3c607-233">metodo tables.initialize() Hello restituisce un [promessa] in modo che servizio web hello non soddisfare le richieste prima database hello da inizializzare.</span><span class="sxs-lookup"><span data-stu-id="3c607-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="3c607-234"><a name="howto-sqlexpress-setup"></a>Procedura: Usare SQL Express come archivio dati di sviluppo nel computer locale</span><span class="sxs-lookup"><span data-stu-id="3c607-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="3c607-235">Hello App mobili di Azure hello AzureMobile App nodo SDK sono disponibili tre opzioni per la gestione di dati predefinito hello: SDK fornisce tre opzioni per la gestione di dati predefinito hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="3c607-236">Hello utilizzare **memoria** archivio di esempio tooprovide un non-persistent driver</span><span class="sxs-lookup"><span data-stu-id="3c607-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="3c607-237">Hello utilizzare **mssql** tooprovide driver un archivio di dati SQL Express per lo sviluppo</span><span class="sxs-lookup"><span data-stu-id="3c607-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="3c607-238">Hello utilizzare **mssql** tooprovide driver un archivio dati di Database SQL di Azure per la produzione</span><span class="sxs-lookup"><span data-stu-id="3c607-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="3c607-239">Hello Azure Mobile App Node.js SDK Usa hello [pacchetto Node.js mssql] tooestablish e utilizzare una connessione tooboth SQL Express e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="3c607-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="3c607-240">Per questo pacchetto è necessario abilitare le connessioni TCP nell'istanza di SQL Express.</span><span class="sxs-lookup"><span data-stu-id="3c607-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="3c607-241">driver di memoria Hello non fornisce un set completo di funzionalità per il test.</span><span class="sxs-lookup"><span data-stu-id="3c607-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="3c607-242">Se si desidera tootest back-end in locale, è consigliabile utilizzare hello di un archivio dati di SQL Express e hello driver mssql.</span><span class="sxs-lookup"><span data-stu-id="3c607-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="3c607-243">Scaricare e installare [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="3c607-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="3c607-244">Assicurarsi di che installare SQL Server 2014 Express hello con versione degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="3c607-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="3c607-245">A meno che non è necessaria in modo esplicito il supporto a 64 bit, la versione a 32 bit hello utilizza minore quantità di memoria durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3c607-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="3c607-246">Eseguire Gestione configurazione SQL Server 2014 hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="3c607-247">Espandere hello **configurazione di rete SQL Server** nodo nel menu di hello albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3c607-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="3c607-248">Fare clic su **Protocolli per SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="3c607-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="3c607-249">Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="3c607-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="3c607-250">Fare clic su **OK** nella finestra di dialogo popup hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="3c607-251">Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="3c607-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="3c607-252">Fare clic su hello **gli indirizzi IP** scheda.</span><span class="sxs-lookup"><span data-stu-id="3c607-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="3c607-253">Trovare hello **IPAll** nodo.</span><span class="sxs-lookup"><span data-stu-id="3c607-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="3c607-254">In hello **la porta TCP** immettere **1433**.</span><span class="sxs-lookup"><span data-stu-id="3c607-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="3c607-255">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c607-255">Click **OK**.</span></span>  <span data-ttu-id="3c607-256">Fare clic su **OK** nella finestra di dialogo popup hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="3c607-257">Fare clic su **servizi di SQL Server** nel menu di hello albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3c607-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="3c607-258">Fare clic con il pulsante destro del mouse su **SQL Server (SQLEXPRESS)** e scegliere **Riavvia**</span><span class="sxs-lookup"><span data-stu-id="3c607-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="3c607-259">Chiudere Gestione configurazione SQL Server 2014 hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="3c607-260">Eseguire hello SQL Server 2014 Management Studio e connettersi tooyour istanza locale di SQL Express</span><span class="sxs-lookup"><span data-stu-id="3c607-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="3c607-261">L'istanza in Esplora oggetti hello e scegliere **proprietà**</span><span class="sxs-lookup"><span data-stu-id="3c607-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="3c607-262">Seleziona hello **sicurezza** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c607-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="3c607-263">Assicurarsi di hello **modalità di autenticazione di Windows e SQL Server** è selezionata</span><span class="sxs-lookup"><span data-stu-id="3c607-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="3c607-264">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="3c607-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="3c607-265">Espandere **sicurezza** > **gli account di accesso** in hello Esplora oggetti</span><span class="sxs-lookup"><span data-stu-id="3c607-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="3c607-266">Fare clic con il pulsante destro del mouse su **Account di accesso** e scegliere **Nuovo account di accesso**</span><span class="sxs-lookup"><span data-stu-id="3c607-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="3c607-267">Immettere un nome account di accesso.</span><span class="sxs-lookup"><span data-stu-id="3c607-267">Enter a Login name.</span></span>  <span data-ttu-id="3c607-268">Selezionare **Autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3c607-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="3c607-269">Immettere una Password, quindi immettere hello stessa password in **Conferma password**.</span><span class="sxs-lookup"><span data-stu-id="3c607-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="3c607-270">password di Hello deve soddisfare i requisiti di complessità di Windows.</span><span class="sxs-lookup"><span data-stu-id="3c607-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="3c607-271">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="3c607-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="3c607-272">Fare clic con il pulsante destro del mouse sul nuovo account di accesso e scegliere **Proprietà**</span><span class="sxs-lookup"><span data-stu-id="3c607-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="3c607-273">Seleziona hello **i ruoli del Server** pagina</span><span class="sxs-lookup"><span data-stu-id="3c607-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="3c607-274">Controllare hello casella Avanti toohello **dbcreator** ruolo del server</span><span class="sxs-lookup"><span data-stu-id="3c607-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="3c607-275">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="3c607-275">Click **OK**</span></span>
   13. <span data-ttu-id="3c607-276">Chiudere hello SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="3c607-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="3c607-277">Assicurarsi di hello record username e password che è stata selezionata.</span><span class="sxs-lookup"><span data-stu-id="3c607-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="3c607-278">A seconda dei requisiti di database specifico, potrebbe essere necessario tooassign altri ruoli del server o autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="3c607-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="3c607-279">applicazione Node.js Hello legge hello **SQLCONNSTR_MS_TableConnectionString** variabile di ambiente per la stringa di connessione hello per questo database.</span><span class="sxs-lookup"><span data-stu-id="3c607-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="3c607-280">Questa variabile può essere impostata all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3c607-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="3c607-281">Ad esempio, è possibile utilizzare PowerShell tooset questa variabile di ambiente:</span><span class="sxs-lookup"><span data-stu-id="3c607-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="3c607-282">Accedere a database hello tramite una connessione TCP/IP e fornire un nome utente e una password per la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="3c607-283"><a name="howto-config-localdev"></a>Procedura: Configurare il progetto per lo sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="3c607-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="3c607-284">App per dispositivi mobili Azure legge un file JavaScript denominato *azureMobile.js* dal file System locale hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="3c607-285">Non utilizzare hello di tooconfigure questo file app Mobile di Azure SDK nell'ambiente di produzione: utilizzare le impostazioni dell'App all'interno di hello [portale di Azure] invece.</span><span class="sxs-lookup"><span data-stu-id="3c607-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="3c607-286">Hello *azureMobile.js* file necessario esportare un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="3c607-287">impostazioni di Hello più comuni sono:</span><span class="sxs-lookup"><span data-stu-id="3c607-287">hello most common settings are:</span></span>

* <span data-ttu-id="3c607-288">Impostazioni database</span><span class="sxs-lookup"><span data-stu-id="3c607-288">Database Settings</span></span>
* <span data-ttu-id="3c607-289">Impostazioni di registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="3c607-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="3c607-290">Impostazioni CORS alternative</span><span class="sxs-lookup"><span data-stu-id="3c607-290">Alternate CORS Settings</span></span>

<span data-ttu-id="3c607-291">Un esempio *azureMobile.js* file implementa hello indicato di seguito le impostazioni del database precedente:</span><span class="sxs-lookup"><span data-stu-id="3c607-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

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

<span data-ttu-id="3c607-292">È consigliabile aggiungere *azureMobile.js* tooyour *con estensione gitignore* file (o altri ignorare i file di controllo del codice sorgente) tooprevent le password vengano archiviate nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="3c607-293">Configurare sempre le impostazioni di produzione nelle impostazioni dell'App all'interno di hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="3c607-294"><a name="howto-appsettings"></a>Procedura: Configurare le impostazioni dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="3c607-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="3c607-295">La maggior parte delle impostazioni in hello *azureMobile.js* file dispone di un'impostazione di App equivalente in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="3c607-296">Uso dell'app di hello seguente elenco tooconfigure nelle impostazioni dell'App:</span><span class="sxs-lookup"><span data-stu-id="3c607-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="3c607-297">Impostazione app</span><span class="sxs-lookup"><span data-stu-id="3c607-297">App Setting</span></span> | <span data-ttu-id="3c607-298">*azureMobile.js*</span><span class="sxs-lookup"><span data-stu-id="3c607-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="3c607-299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c607-299">Description</span></span> | <span data-ttu-id="3c607-300">Valori validi</span><span class="sxs-lookup"><span data-stu-id="3c607-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3c607-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="3c607-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="3c607-302">name</span><span class="sxs-lookup"><span data-stu-id="3c607-302">name</span></span> |<span data-ttu-id="3c607-303">nome Hello dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="3c607-303">hello name of hello app</span></span> |<span data-ttu-id="3c607-304">string</span><span class="sxs-lookup"><span data-stu-id="3c607-304">string</span></span> |
| <span data-ttu-id="3c607-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="3c607-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="3c607-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="3c607-306">logging.level</span></span> |<span data-ttu-id="3c607-307">Livello di log minimo di messaggi toolog</span><span class="sxs-lookup"><span data-stu-id="3c607-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="3c607-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="3c607-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="3c607-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="3c607-309">**MS_DebugMode**</span></span> |<span data-ttu-id="3c607-310">debug</span><span class="sxs-lookup"><span data-stu-id="3c607-310">debug</span></span> |<span data-ttu-id="3c607-311">Abilitare o disabilitare la modalità di debug</span><span class="sxs-lookup"><span data-stu-id="3c607-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="3c607-312">true, false</span><span class="sxs-lookup"><span data-stu-id="3c607-312">true, false</span></span> |
| <span data-ttu-id="3c607-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="3c607-313">**MS_TableSchema**</span></span> |<span data-ttu-id="3c607-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="3c607-314">data.schema</span></span> |<span data-ttu-id="3c607-315">Nome dello schema predefinito per le tabelle SQL</span><span class="sxs-lookup"><span data-stu-id="3c607-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="3c607-316">string (valore predefinito: dbo)</span><span class="sxs-lookup"><span data-stu-id="3c607-316">string (default: dbo)</span></span> |
| <span data-ttu-id="3c607-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="3c607-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="3c607-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="3c607-318">data.dynamicSchema</span></span> |<span data-ttu-id="3c607-319">Abilitare o disabilitare la modalità di debug</span><span class="sxs-lookup"><span data-stu-id="3c607-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="3c607-320">true, false</span><span class="sxs-lookup"><span data-stu-id="3c607-320">true, false</span></span> |
| <span data-ttu-id="3c607-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="3c607-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="3c607-322">versione (set tooundefined)</span><span class="sxs-lookup"><span data-stu-id="3c607-322">version (set tooundefined)</span></span> |<span data-ttu-id="3c607-323">Disabilita l'intestazione X-ZUMO-Server-versione di hello</span><span class="sxs-lookup"><span data-stu-id="3c607-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="3c607-324">true, false</span><span class="sxs-lookup"><span data-stu-id="3c607-324">true, false</span></span> |
| <span data-ttu-id="3c607-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="3c607-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="3c607-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="3c607-326">skipversioncheck</span></span> |<span data-ttu-id="3c607-327">Disabilita il controllo della versione API client hello</span><span class="sxs-lookup"><span data-stu-id="3c607-327">Disables hello client API version check</span></span> |<span data-ttu-id="3c607-328">true, false</span><span class="sxs-lookup"><span data-stu-id="3c607-328">true, false</span></span> |

<span data-ttu-id="3c607-329">tooset un'impostazione di App:</span><span class="sxs-lookup"><span data-stu-id="3c607-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="3c607-330">Accedi toohello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="3c607-331">Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="3c607-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="3c607-332">pannello impostazioni Hello viene aperto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="3c607-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="3c607-333">In caso contrario fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="3c607-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="3c607-334">Fare clic su **le impostazioni dell'applicazione** nel menu Generale hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="3c607-335">Scorrere toohello sezione App impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3c607-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="3c607-336">Se l'app impostazione già esiste, fare clic su hello valore hello app impostazione tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="3c607-337">Se l'impostazione dell'app non esiste, immettere hello impostazione dell'App nella casella chiave hello e valore hello nella casella valore hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="3c607-338">Al termine, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3c607-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="3c607-339">Per modificare la maggior parte delle impostazioni dell'app, è necessario riavviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="3c607-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="3c607-340"><a name="howto-use-sqlazure"></a>Procedura: Usare il database SQL come archivio dati di produzione</span><span class="sxs-lookup"><span data-stu-id="3c607-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="3c607-341">L'uso del database SQL di Azure come archivio dati è identico in tutti i tipi di applicazione del Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c607-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="3c607-342">Se non è già stato fatto, seguire questi toocreate passaggi un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="3c607-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="3c607-343">Accedi toohello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="3c607-344">Hello in alto a sinistra della finestra hello, fare clic su hello **+ nuovo** pulsante > **Web e dispositivi mobili** > **App Mobile**, quindi specificare un nome per il back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="3c607-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="3c607-345">In hello **gruppo di risorse** immettere hello stesso nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="3c607-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="3c607-346">piano di servizio App predefinito Hello è selezionato.</span><span class="sxs-lookup"><span data-stu-id="3c607-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="3c607-347">Se si desidera toochange piano di servizio App, è possibile farlo facendo clic sul piano di servizio App hello > **+ Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3c607-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="3c607-348">Specificare un nome del piano di servizio App nuovo hello e selezionare un percorso appropriato.</span><span class="sxs-lookup"><span data-stu-id="3c607-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="3c607-349">Selezionare un piano tariffario appropriato per il servizio hello tariffario hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="3c607-350">Selezionare **visualizzare tutti** tooview più prezzi opzioni, ad esempio **libero** e **Shared**.</span><span class="sxs-lookup"><span data-stu-id="3c607-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="3c607-351">Dopo aver selezionato il livello di prezzo, fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3c607-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="3c607-352">In hello **piano di servizio App** pannello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c607-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="3c607-353">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3c607-353">Click **Create**.</span></span> <span data-ttu-id="3c607-354">L'operazione di provisioning di un back-end dell'app per dispositivi mobili può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="3c607-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="3c607-355">Una volta che viene eseguito il provisioning di back-end App Mobile hello, hello viene visualizzato il portale di hello **impostazioni** pannello back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="3c607-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="3c607-356">Dopo la creazione di back-end di hello App per dispositivi mobili, è possibile scegliere tooeither connettere un SQL database tooyour App Mobile back-end esistente o creare un nuovo database SQL.</span><span class="sxs-lookup"><span data-stu-id="3c607-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="3c607-357">In questa sezione viene creato un database SQL.</span><span class="sxs-lookup"><span data-stu-id="3c607-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="3c607-358">Se si dispone già di un database in hello stessa posizione di back-end di hello app per dispositivi mobili, è invece possibile scegliere **utilizza un database esistente** e quindi selezionare il database.</span><span class="sxs-lookup"><span data-stu-id="3c607-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="3c607-359">non è consigliabile utilizzare Hello di un database in una posizione diversa latenze più elevate.</span><span class="sxs-lookup"><span data-stu-id="3c607-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="3c607-360">In hello nuovo back-end App Mobile, fare clic su **impostazioni** > **App Mobile** > **dati** > **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3c607-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="3c607-361">In hello **aggiungere una connessione dati** pannello, fare clic su **Database di SQL - configurare le impostazioni necessarie** > **creare un nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="3c607-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="3c607-362">Immettere il nome di hello del nuovo database hello in hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="3c607-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="3c607-363">Fare clic su **Server**.</span><span class="sxs-lookup"><span data-stu-id="3c607-363">Click **Server**.</span></span>  <span data-ttu-id="3c607-364">In hello **nuovo server** pannello, immettere un nome server univoci in hello **nome Server** campo e forniscono un adatto **account di accesso amministratore Server** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="3c607-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="3c607-365">Verificare **server tooaccess di servizi di azure Consenti** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="3c607-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="3c607-366">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c607-366">Click **OK**.</span></span>

    ![Creare un database SQL di Azure][6]
4. <span data-ttu-id="3c607-368">In hello **nuovo database** pannello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c607-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="3c607-369">In hello **aggiungere una connessione dati** pannello seleziona **stringa di connessione**, immettere l'account di accesso hello e la password fornita durante la creazione di database hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="3c607-370">Se si utilizza un database esistente, fornire le credenziali di account di accesso hello per quel database.</span><span class="sxs-lookup"><span data-stu-id="3c607-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="3c607-371">Dopo averli immessi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c607-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="3c607-372">In hello **aggiungere una connessione dati** pannello fare nuovamente clic **OK** database hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c607-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="3c607-373">Creazione del database hello può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="3c607-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="3c607-374">Hello utilizzare **notifiche** area toomonitor hello lo stato di avanzamento della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="3c607-375">Avanza fino a quando il database di hello è stato distribuito correttamente.</span><span class="sxs-lookup"><span data-stu-id="3c607-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="3c607-376">Dopo aver distribuito correttamente, viene creata una stringa di connessione per istanza di Database SQL di hello nel back-end le impostazioni dell'App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="3c607-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="3c607-377">È possibile visualizzare questa impostazione di app in hello **impostazioni** > **le impostazioni dell'applicazione** > **le stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="3c607-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="3c607-378"><a name="howto-tables-auth"></a>Procedura: richiedere l'autenticazione per accesso tootables</span><span class="sxs-lookup"><span data-stu-id="3c607-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="3c607-379">Se si desidera toouse l'autenticazione del servizio App con endpoint tabelle hello, è necessario configurare l'autenticazione del servizio App in hello [portale di Azure] prima.</span><span class="sxs-lookup"><span data-stu-id="3c607-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="3c607-380">Per ulteriori informazioni sulla configurazione dell'autenticazione in un servizio App di Azure, esaminare hello Guida alla configurazione per il provider di identità hello intendi toouse:</span><span class="sxs-lookup"><span data-stu-id="3c607-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="3c607-381">[Modalità autenticazione di Azure Active Directory tooconfigure]</span><span class="sxs-lookup"><span data-stu-id="3c607-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="3c607-382">[Come tooconfigure l'autenticazione di Facebook]</span><span class="sxs-lookup"><span data-stu-id="3c607-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="3c607-383">[Come tooconfigure l'autenticazione di Google]</span><span class="sxs-lookup"><span data-stu-id="3c607-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="3c607-384">[Come tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="3c607-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="3c607-385">[Come tooconfigure autenticazione Twitter]</span><span class="sxs-lookup"><span data-stu-id="3c607-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="3c607-386">Ogni tabella dispone di una proprietà di accesso che può essere utilizzato toocontrol accesso toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="3c607-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="3c607-387">Hello seguente esempio mostra una tabella in modo statico definita necessaria autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="3c607-388">proprietà di accesso Hello può assumere uno dei tre valori</span><span class="sxs-lookup"><span data-stu-id="3c607-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="3c607-389">*anonimo* indica che un'applicazione client hello è consentita tooread dati senza autenticazione</span><span class="sxs-lookup"><span data-stu-id="3c607-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="3c607-390">*autenticazione* indica che un'applicazione hello client deve inviare un token di autenticazione valido con richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="3c607-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="3c607-391">*disabled* indica che la tabella è attualmente disabilitata.</span><span class="sxs-lookup"><span data-stu-id="3c607-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="3c607-392">Se la proprietà di accesso hello è definita, è consentito l'accesso non autenticato.</span><span class="sxs-lookup"><span data-stu-id="3c607-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="3c607-393"><a name="howto-tables-getidentity"></a>Procedura: Usare le attestazioni di autenticazione con le tabelle</span><span class="sxs-lookup"><span data-stu-id="3c607-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="3c607-394">È possibile impostare diverse attestazioni richieste quando viene impostata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="3c607-395">Queste attestazioni non sono in genere disponibili tramite hello `context.user` oggetto.</span><span class="sxs-lookup"><span data-stu-id="3c607-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="3c607-396">Tuttavia, possono essere recuperate utilizzando hello `context.user.getIdentity()` metodo.</span><span class="sxs-lookup"><span data-stu-id="3c607-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="3c607-397">Hello `getIdentity()` metodo restituisce una promessa che risolve l'oggetto tooan.</span><span class="sxs-lookup"><span data-stu-id="3c607-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="3c607-398">oggetto Hello è codificato dal metodo di autenticazione (facebook, google, twitter, microsoftaccount o aad).</span><span class="sxs-lookup"><span data-stu-id="3c607-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="3c607-399">Ad esempio, se si configura l'autenticazione di Account Microsoft e l'attestazione basata su indirizzi di posta elettronica hello richiesta, è possibile aggiungere record toohello indirizzo di posta elettronica hello con hello controller nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="3c607-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="3c607-400">toosee le attestazioni sono disponibili, utilizzare un hello tooview di web browser `/.auth/me` endpoint del sito.</span><span class="sxs-lookup"><span data-stu-id="3c607-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="3c607-401"><a name="howto-tables-disabled"></a>Procedura: operazioni di tabella toospecific Disabilita accesso</span><span class="sxs-lookup"><span data-stu-id="3c607-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="3c607-402">In aggiunta tooappearing tabella hello, proprietà di accesso hello può essere utilizzato toocontrol singole operazioni.</span><span class="sxs-lookup"><span data-stu-id="3c607-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="3c607-403">Sono disponibili quattro operazioni:</span><span class="sxs-lookup"><span data-stu-id="3c607-403">There are four operations:</span></span>

* <span data-ttu-id="3c607-404">*lettura* hello ottenere RESTful operazione sulla tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="3c607-405">*Inserisci* hello POST RESTful operazione sulla tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="3c607-406">*aggiornare* hello PATCH RESTful operazione sulla tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="3c607-407">*eliminare* hello eliminare RESTful operazione sulla tabella hello</span><span class="sxs-lookup"><span data-stu-id="3c607-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="3c607-408">Ad esempio, è preferibile tooprovide una tabella non autenticata di sola lettura:</span><span class="sxs-lookup"><span data-stu-id="3c607-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="3c607-409"><a name="howto-tables-query"></a>Procedura: modificare query hello utilizzato con operazioni di tabella</span><span class="sxs-lookup"><span data-stu-id="3c607-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="3c607-410">Un requisito comune per le operazioni di tabella è una vista limitata di dati hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="3c607-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="3c607-411">Ad esempio, è possibile fornire una tabella che è contrassegnata con hello autenticato ID utente in modo che è possibile leggere o aggiornare i propri record.</span><span class="sxs-lookup"><span data-stu-id="3c607-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="3c607-412">Hello definizione della tabella seguente fornisce questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="3c607-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="3c607-413">Le operazioni che in genere eseguono una query avranno una proprietà query modificabile con una clausola where.</span><span class="sxs-lookup"><span data-stu-id="3c607-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="3c607-414">proprietà query Hello è un [QueryJS] oggetto che è in grado di elaborare tooconvert usato un toosomething di query OData che hello dati di back-end.</span><span class="sxs-lookup"><span data-stu-id="3c607-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="3c607-415">Per i casi di uguaglianza semplici (ad esempio hello uno precedente), è possibile utilizzare una mappa.</span><span class="sxs-lookup"><span data-stu-id="3c607-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="3c607-416">È anche possibile aggiungere clausole SQL specifiche:</span><span class="sxs-lookup"><span data-stu-id="3c607-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="3c607-417"><a name="howto-tables-softdelete"></a>Procedura: Configurare l'eliminazione temporanea in una tabella</span><span class="sxs-lookup"><span data-stu-id="3c607-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="3c607-418">L'eliminazione temporanea non elimina effettivamente i record.</span><span class="sxs-lookup"><span data-stu-id="3c607-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="3c607-419">Invece contrassegna come eliminati nel database di hello impostando tootrue colonna hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="3c607-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="3c607-420">a meno che non hello Mobile Client SDK utilizza IncludeDeleted(), Hello App Mobile di Azure SDK rimuove automaticamente record eliminato dai risultati.</span><span class="sxs-lookup"><span data-stu-id="3c607-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="3c607-421">eliminare una tabella per soft, tooconfigure impostare hello `softDelete` proprietà nel file di definizione di tabella hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="3c607-422">È necessario stabilire un meccanismo per l'eliminazione dei record, che sia da un'applicazione client, con un processo Web, tramite Funzioni di Azure o un'API personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3c607-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="3c607-423"><a name="howto-tables-seeding"></a>Procedura: Eseguire il seeding dei dati nel database</span><span class="sxs-lookup"><span data-stu-id="3c607-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="3c607-424">Quando si crea una nuova applicazione, è preferibile tooseed una tabella con dati.</span><span class="sxs-lookup"><span data-stu-id="3c607-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="3c607-425">Questa operazione può essere eseguita nel file di JavaScript definizione tabella hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c607-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="3c607-426">Il seeding dei dati viene eseguito solo quando la tabella hello viene creata da hello App Mobile di Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="3c607-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="3c607-427">Se la tabella hello esiste già nel database di hello, nessun dato viene inserito nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="3c607-428">Se lo schema dinamico è abilitato, lo schema viene dedotto dal dati hello seeding.</span><span class="sxs-lookup"><span data-stu-id="3c607-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="3c607-429">Si consiglia di chiamare in modo esplicito hello `tables.initialize()` tabella quando il servizio hello viene avviata l'esecuzione del metodo toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="3c607-430"><a name="Swagger"></a>Procedura: Abilitare il supporto di Swagger</span><span class="sxs-lookup"><span data-stu-id="3c607-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="3c607-431">Le app per dispositivi mobili del servizio app di Azure sono fornite con il supporto di [Swagger] incorporato.</span><span class="sxs-lookup"><span data-stu-id="3c607-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="3c607-432">tooenable supporto Swagger, installare innanzitutto swagger hello dell'interfaccia utente come dipendenza:</span><span class="sxs-lookup"><span data-stu-id="3c607-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="3c607-433">Una volta installato, è possibile abilitare il supporto di Swagger nel costruttore di hello App mobili di Azure:</span><span class="sxs-lookup"><span data-stu-id="3c607-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="3c607-434">È probabilmente solo desidera tooenable Swagger supporto nelle edizioni di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="3c607-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="3c607-435">È possibile farlo usando l'impostazione dell'app `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="3c607-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="3c607-436">Hello swagger endpoint si trova in http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="3c607-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="3c607-437">È possibile accedere hello Swagger dell'interfaccia utente tramite hello `/swagger/ui` endpoint.</span><span class="sxs-lookup"><span data-stu-id="3c607-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="3c607-438">Se si sceglie l'autenticazione toorequire dall'intera applicazione, Swagger genera un errore.</span><span class="sxs-lookup"><span data-stu-id="3c607-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="3c607-439">Per ottenere risultati ottimali, scegliere le richieste autenticate tooallow tramite in hello Azure l'autenticazione del servizio App / impostazioni di autorizzazione, quindi controllare l'autenticazione utilizzando hello `table.access` proprietà.</span><span class="sxs-lookup"><span data-stu-id="3c607-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="3c607-440">È inoltre possibile aggiungere hello Swagger opzione tooyour `azureMobile.js` file se si desidera solo Swagger supporto durante lo sviluppo in locale.</span><span class="sxs-lookup"><span data-stu-id="3c607-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="3c607-441"><a name="push">Notifiche push</span><span class="sxs-lookup"><span data-stu-id="3c607-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="3c607-442">App per dispositivi mobili si integra con gli hub di notifica di Azure tooenable è toomillions di notifiche push toosend destinata dei dispositivi tra tutte le principali piattaforme.</span><span class="sxs-lookup"><span data-stu-id="3c607-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="3c607-443">Tramite gli hub di notifica, è possibile inviare push tooiOS notifiche, i dispositivi Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="3c607-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="3c607-444">toolearn più sulle operazioni che è possibile eseguire con gli hub di notifica, vedere [Panoramica di hub di notifica](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c607-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="3c607-445"></a><a name="send-push"></a>Procedura: Inviare notifiche push</span><span class="sxs-lookup"><span data-stu-id="3c607-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="3c607-446">Hello di codice seguente mostra i dispositivi iOS tooregistered notifica push toouse hello push oggetto toosend una trasmissione:</span><span class="sxs-lookup"><span data-stu-id="3c607-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="3c607-447">Per creare una registrazione di modello push client hello, è possibile inviare invece un toodevices di messaggio modello push su tutte le piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="3c607-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="3c607-448">Hello seguente codice mostra come toosend una notifica modello:</span><span class="sxs-lookup"><span data-stu-id="3c607-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="3c607-449"><a name="push-user"></a>Procedura: tooan di notifiche push trasmissione autenticato l'utente con il tag</span><span class="sxs-lookup"><span data-stu-id="3c607-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="3c607-450">Quando un utente autenticato registrati per le notifiche push, un tag di ID utente viene aggiunto automaticamente toohello registrazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="3c607-451">Tramite questo tag, è possibile inviare push dispositivi tooall notifiche registrati da un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="3c607-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="3c607-452">Hello codice seguente ottiene hello SID dell'utente che effettua la richiesta hello e invia una registrazione di modello push notifica tooevery dispositivo per tale utente:</span><span class="sxs-lookup"><span data-stu-id="3c607-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="3c607-453">Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="3c607-454"><a name="CustomAPI"></a> API personalizzate</span><span class="sxs-lookup"><span data-stu-id="3c607-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="3c607-455"><a name="howto-customapi-basic"></a>Procedura: Definire un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="3c607-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="3c607-456">Inoltre toohello di accesso ai dati API tramite l'endpoint /tables hello, App mobili di Azure può fornire una copertura di API personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3c607-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="3c607-457">Le API personalizzate sono definite in un simile definizioni di tabella toohello modo e possono accedere a tutti hello stessa funzionalità, tra cui l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="3c607-458">Se si desidera toouse l'autenticazione del servizio App con un'API personalizzata, è necessario configurare l'autenticazione del servizio App in hello [portale di Azure] prima.</span><span class="sxs-lookup"><span data-stu-id="3c607-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="3c607-459">Per ulteriori informazioni sulla configurazione dell'autenticazione in un servizio App di Azure, esaminare hello Guida alla configurazione per il provider di identità hello intendi toouse:</span><span class="sxs-lookup"><span data-stu-id="3c607-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="3c607-460">[Modalità autenticazione di Azure Active Directory tooconfigure]</span><span class="sxs-lookup"><span data-stu-id="3c607-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="3c607-461">[Come tooconfigure l'autenticazione di Facebook]</span><span class="sxs-lookup"><span data-stu-id="3c607-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="3c607-462">[Come tooconfigure l'autenticazione di Google]</span><span class="sxs-lookup"><span data-stu-id="3c607-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="3c607-463">[Come tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="3c607-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="3c607-464">[Come tooconfigure autenticazione Twitter]</span><span class="sxs-lookup"><span data-stu-id="3c607-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="3c607-465">Le API personalizzate vengono definite in gran parte hello come hello tabelle API.</span><span class="sxs-lookup"><span data-stu-id="3c607-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="3c607-466">Creare una directory **api** .</span><span class="sxs-lookup"><span data-stu-id="3c607-466">Create an **api** directory</span></span>
2. <span data-ttu-id="3c607-467">Creare un file JavaScript definizione dell'API in hello **api** directory.</span><span class="sxs-lookup"><span data-stu-id="3c607-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="3c607-468">Utilizzare prova importazione metodo tooimport prova **api** directory.</span><span class="sxs-lookup"><span data-stu-id="3c607-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="3c607-469">Ecco di definizione dell'api prototipo hello in base a esempio di app basic hello che è utilizzate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3c607-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="3c607-470">Esaminiamo un esempio di API che restituisce Data server hello utilizzando hello *Date.now()* metodo.</span><span class="sxs-lookup"><span data-stu-id="3c607-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="3c607-471">Di seguito è riportato il file di api/date.js hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="3c607-472">Ogni parametro è uno dei hello RESTful verbi standard - GET, POST, PATCH o DELETE.</span><span class="sxs-lookup"><span data-stu-id="3c607-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="3c607-473">metodo Hello è uno standard [ExpressJS Middleware] funzione che invia l'output di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="3c607-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="3c607-474"><a name="howto-customapi-auth"></a>Procedura: richiedere l'autenticazione per l'API di accesso tooa personalizzata</span><span class="sxs-lookup"><span data-stu-id="3c607-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="3c607-475">Implementa l'autenticazione in hello Azure Mobile App SDK allo stesso modo per endpoint di hello tabelle e le API personalizzate.</span><span class="sxs-lookup"><span data-stu-id="3c607-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="3c607-476">Per aggiungere l'autenticazione toohello API sviluppato nella sezione precedente di hello, aggiungere un **accesso** proprietà:</span><span class="sxs-lookup"><span data-stu-id="3c607-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="3c607-477">È anche possibile specificare l'autenticazione su operazioni specifiche:</span><span class="sxs-lookup"><span data-stu-id="3c607-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="3c607-478">Hello stesso token utilizzato per l'endpoint di tabelle hello deve essere usato per le API personalizzate che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="3c607-479"><a name="howto-customapi-auth"></a>Procedura: Gestire il caricamento di file di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="3c607-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="3c607-480">Azure Mobile App SDK Usa hello [corpo parser middleware](https://github.com/expressjs/body-parser) tooaccept e decodificare il contenuto del corpo nell'elemento inviato.</span><span class="sxs-lookup"><span data-stu-id="3c607-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="3c607-481">È possibile preconfigurare caricamenti di file più grandi di corpo parser tooaccept:</span><span class="sxs-lookup"><span data-stu-id="3c607-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="3c607-482">file Hello è codificati prima della trasmissione in base 64.</span><span class="sxs-lookup"><span data-stu-id="3c607-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="3c607-483">Ciò aumenta la dimensione di hello del caricamento effettivo hello e pertanto hello dimensioni, che è necessario tener conto.</span><span class="sxs-lookup"><span data-stu-id="3c607-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="3c607-484"><a name="howto-customapi-sql"></a>Procedura: Eseguire istruzioni SQL personalizzate</span><span class="sxs-lookup"><span data-stu-id="3c607-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="3c607-485">Hello App Mobile di Azure SDK consente l'accesso toohello intero contesto tramite l'oggetto richiesta hello, consentendo tooexecute i provider di dati definito toohello istruzioni SQL con parametri facilmente:</span><span class="sxs-lookup"><span data-stu-id="3c607-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="3c607-486"><a name="Debugging"></a>Debug, tabelle semplici e API semplici</span><span class="sxs-lookup"><span data-stu-id="3c607-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="3c607-487"><a name="howto-diagnostic-logs"></a>Procedura: Eseguire il debug e diagnosticare e risolvere i problemi di App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="3c607-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="3c607-488">Hello Azure App Service fornisce diverse debug e risoluzione dei problemi di tecniche per applicazioni Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c607-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="3c607-489">Fare riferimento toohello tooget articoli avviato nel back-end Node.js Mobile di risoluzione dei problemi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c607-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="3c607-490">[Monitoraggio di un servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="3c607-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="3c607-491">[Abilitazione della registrazione diagnostica nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="3c607-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="3c607-492">[Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3c607-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="3c607-493">Le applicazioni Node.js hanno accesso tooa ampia gamma di strumenti di log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3c607-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="3c607-494">Internamente, hello Azure Mobile App Node.js SDK Usa [Winston] per la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3c607-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="3c607-495">La registrazione è abilitata automaticamente attivare la modalità di debug o dall'impostazione hello **MS_DebugMode** tootrue impostazione app in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="3c607-496">Log generati vengono visualizzati nel log di diagnostica di hello in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="3c607-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="3c607-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procedura: utilizzare tabelle semplice in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c607-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="3c607-498">Tabelle di facile nel portale di hello consentono di creare e utilizzare direttamente le tabelle nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="3c607-499">È anche possibile modificare le operazioni di tabella utilizzando l'Editor di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="3c607-500">Quando si fa clic su **Tabelle semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare una tabella.</span><span class="sxs-lookup"><span data-stu-id="3c607-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="3c607-501">È inoltre possibile visualizzare dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-501">You can also see data in hello table.</span></span>

![Utilizzare Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="3c607-503">Hello comandi riportati di seguito sono disponibili sulla barra dei comandi di hello per una tabella:</span><span class="sxs-lookup"><span data-stu-id="3c607-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="3c607-504">**Modificare le autorizzazioni** : hello l'autorizzazione per la lettura di modifica, inserire, aggiornare ed eliminare operazioni sulla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="3c607-505">Le opzioni sono tooallow l'accesso anonimo, l'autenticazione toorequire o toodisable tutte toohello operazione di accesso.</span><span class="sxs-lookup"><span data-stu-id="3c607-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="3c607-506">**Modificare lo script** -hello script per tabella hello viene aperto nell'Editor di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="3c607-507">**Gestire schema** : aggiungere o eliminare le colonne o modificare l'indice di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="3c607-508">**Cancella tabella** -tronca una tabella esistente, eliminare tutte le righe di dati ma lasciando schema hello invariata.</span><span class="sxs-lookup"><span data-stu-id="3c607-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="3c607-509">**Elimina righe** : è possibile eliminare singole righe di dati.</span><span class="sxs-lookup"><span data-stu-id="3c607-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="3c607-510">**Visualizza i log di streaming** -consente di connettersi toohello streaming il servizio di registrazione per il sito.</span><span class="sxs-lookup"><span data-stu-id="3c607-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="3c607-511"><a name="work-easy-apis"></a>Procedura: utilizzare le API semplice in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c607-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="3c607-512">API semplice nel portale di hello consentono di creare e utilizzare con diritto di API personalizzata nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="3c607-513">È possibile modificare gli script di API utilizzando l'Editor di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="3c607-514">Quando si fa clic su **API semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare un endpoint API personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3c607-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Utilizzare Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="3c607-516">Nel portale di hello, si può modificare le autorizzazioni di accesso hello per una determinata azione HTTP, file di script nell'Editor di servizio App di hello API, visualizzare o modificare i log di streaming hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="3c607-517"><a name="online-editor"></a>Procedura: modificare il codice nell'Editor di servizio App hello</span><span class="sxs-lookup"><span data-stu-id="3c607-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="3c607-518">Hello portale di Azure consente di modificare i file di script di back-end di Node. js in hello Editor di servizio App senza dover scaricare computer locale di hello progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="3c607-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="3c607-519">file di script tooedit nell'editor online hello:</span><span class="sxs-lookup"><span data-stu-id="3c607-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="3c607-520">Nel pannello del back-end dell'app per dispositivi mobili fare clic su **Tutte le impostazioni** > **Easy tables** o **Easy APIs**, fare clic su una tabella o un'API e quindi su **Modifica script**.</span><span class="sxs-lookup"><span data-stu-id="3c607-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="3c607-521">file di script Hello viene aperto in hello Editor di servizio App.</span><span class="sxs-lookup"><span data-stu-id="3c607-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Editor del servizio app](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="3c607-523">Verificare il file del codice toohello le modifiche apportate nell'editor online hello.</span><span class="sxs-lookup"><span data-stu-id="3c607-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="3c607-524">Le modifiche vengono salvate automaticamente durante la digitazione.</span><span class="sxs-lookup"><span data-stu-id="3c607-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Avvio rapido di client Android]: app-service-mobile-android-get-started.md
[Avvio rapido di client Apache Cordova]: app-service-mobile-cordova-get-started.md
[Avvio rapido di client iOS]: app-service-mobile-ios-get-started.md
[Avvio rapido di client Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Avvio rapido di client Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Avvio rapido di client Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Avvio rapido di client Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[sincronizzazione dati offline]: app-service-mobile-offline-data-sync.md
[Modalità autenticazione di Azure Active Directory tooconfigure]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Come tooconfigure l'autenticazione di Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Come tooconfigure l'autenticazione di Google]: app-service-mobile-how-to-configure-google-authentication.md
[Come tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Come tooconfigure autenticazione Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guida alla distribuzione del servizio app di Azure]: ../app-service-web/web-sites-deploy.md
[Monitoraggio di un servizio app di Azure]: ../app-service-web/web-sites-monitor.md
[Abilitazione della registrazione diagnostica nel servizio app di Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[specificare hello nodo versione]: ../nodejs-specify-node-version-azure-apps.md
[utilizzare i moduli del nodo]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portale di Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promessa]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[esempio basicapp in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[esempio todo in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directory esempi su GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 per Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[pacchetto Node.js mssql]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
