---
title: Guida introduttiva di aaaNode.js | Documenti Microsoft
description: Informazioni su come toocreate Node.js una semplice applicazione web e distribuirla come servizio cloud di Azure tooan.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="f66b0-103">Compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="f66b0-104">Questa esercitazione viene illustrato come toocreate Node.js una semplice applicazione in esecuzione in un servizio Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="f66b0-105">Servizi cloud sono blocchi predefiniti di hello delle applicazioni cloud scalabili in Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="f66b0-106">Consentono la separazione di hello e la gestione indipendente e scalabilità orizzontale di componenti front-end e back-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="f66b0-107">Servizi cloud offre una potente macchina virtuale dedicata per ospitare ogni ruolo in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="f66b0-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="f66b0-108">Per ulteriori informazioni sui servizi Cloud e le modalità di confronto tooAzure siti Web e macchine virtuali, vedere [confronto siti Web di Azure, servizi Cloud e macchine virtuali].</span><span class="sxs-lookup"><span data-stu-id="f66b0-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="f66b0-109">Ricerca toobuild un semplice sito Web?</span><span class="sxs-lookup"><span data-stu-id="f66b0-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="f66b0-110">Se lo scenario prevede un semplice sito Web front-end, è possibile [usare un'app Web leggera].</span><span class="sxs-lookup"><span data-stu-id="f66b0-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="f66b0-111">Come si espande l'app web e i requisiti cambiano, è possibile aggiornare facilmente tooa servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="f66b0-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="f66b0-112">Questa esercitazione consente di creare una semplice applicazione Web ospitata in un ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="f66b0-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="f66b0-113">Verrà usare tootest emulatore di calcolo hello l'applicazione localmente, quindi distribuirlo utilizzando gli strumenti da riga di comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f66b0-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="f66b0-114">un'applicazione Hello è una semplice applicazione "hello world":</span><span class="sxs-lookup"><span data-stu-id="f66b0-114">hello application is a simple "hello world" application:</span></span>

![Un web browser visualizzazione pagina web di Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="f66b0-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f66b0-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="f66b0-117">Questa esercitazione usa Azure PowerShell, che richiede Windows.</span><span class="sxs-lookup"><span data-stu-id="f66b0-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="f66b0-118">Installare e configurare [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="f66b0-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="f66b0-119">Scaricare e installare hello [Azure SDK per .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="f66b0-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="f66b0-120">In hello installare il programma di installazione, selezionare:</span><span class="sxs-lookup"><span data-stu-id="f66b0-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="f66b0-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="f66b0-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="f66b0-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="f66b0-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="f66b0-123">Creare un progetto di Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="f66b0-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="f66b0-124">Eseguire hello seguenti attività toocreate un nuovo progetto di servizio Cloud di Azure, insieme a base scaffolding Node.js:</span><span class="sxs-lookup"><span data-stu-id="f66b0-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="f66b0-125">Eseguire **Windows PowerShell** come amministratore, da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f66b0-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="f66b0-126">[La connessione PowerShell] tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="f66b0-127">Immettere hello progetto di hello toocreate toocreate cmdlet PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="f66b0-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![risultato di Hello del comando helloworld hello New-AzureService][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="f66b0-129">Hello **New AzureServiceProject** cmdlet genera una struttura di base per la pubblicazione di un tooa applicazione Node.js servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="f66b0-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="f66b0-130">Contiene i file di configurazione necessari per la pubblicazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="f66b0-131">cmdlet di Hello cambia anche directory toohello di directory di lavoro per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="f66b0-132">cmdlet di Hello crea hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="f66b0-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="f66b0-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef** sono file specifici di Azure, necessari per la pubblicazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="f66b0-134">Per altre informazioni, vedere [Creazione di un servizio ospitato per Azure].</span><span class="sxs-lookup"><span data-stu-id="f66b0-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="f66b0-135">**Deploymentsettings**: archivia le impostazioni locali utilizzate da hello i cmdlet di distribuzione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f66b0-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="f66b0-136">Immettere hello successivo comando tooadd un nuovo ruolo web:</span><span class="sxs-lookup"><span data-stu-id="f66b0-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![output di Hello del comando Add-AzureNodeWebRole hello][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="f66b0-138">Hello **Add-AzureNodeWebRole** cmdlet crea un'applicazione Node.js di base.</span><span class="sxs-lookup"><span data-stu-id="f66b0-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="f66b0-139">Viene inoltre modificata hello **con estensione csfg** e **csdef** tooadd voci di configurazione per il nuovo ruolo di hello dei file.</span><span class="sxs-lookup"><span data-stu-id="f66b0-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f66b0-140">Se non si specifica un nome di ruolo, viene usato un nome predefinito.</span><span class="sxs-lookup"><span data-stu-id="f66b0-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="f66b0-141">È possibile fornire un nome come primo parametro del cmdlet hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="f66b0-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="f66b0-142">app Node.js Hello è definito nel file hello **server.js**, che si trova nella directory di hello per ruolo web hello (**WebRole1** per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="f66b0-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="f66b0-143">Ecco il codice hello:</span><span class="sxs-lookup"><span data-stu-id="f66b0-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="f66b0-144">Questo codice è essenzialmente hello stesso hello "Hello World" di esempio in hello [nodejs.org] sito Web, ad eccezione del fatto che utilizza il numero di porta hello assegnato dall'ambiente cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="f66b0-145">Distribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f66b0-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="f66b0-146">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f66b0-147">È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) o [iscriversi per un account gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="f66b0-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="f66b0-148">Scaricare hello Azure impostazioni di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="f66b0-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="f66b0-149">toodeploy tooAzure l'applicazione, è necessario prima scaricare hello pubblicazione le impostazioni per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="f66b0-150">Eseguire hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="f66b0-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="f66b0-151">Verrà utilizzato il browser toonavigate toohello pagina di download delle impostazioni di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="f66b0-152">Potrebbe essere richiesta toolog con un Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f66b0-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="f66b0-153">In questo caso, utilizzare account hello associati alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="f66b0-154">Percorso file di hello scaricato profilo tooa consentono di accedere facilmente di salvataggio.</span><span class="sxs-lookup"><span data-stu-id="f66b0-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="f66b0-155">Eseguire riportata di seguito cmdlet tooimport hello scaricato profilo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="f66b0-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="f66b0-156">Dopo l'importazione di hello le impostazioni di pubblicazione, provare a eliminare hello scaricato il file con estensione publishsettings, perché contiene informazioni che possono consentire a un utente tooaccess l'account.</span><span class="sxs-lookup"><span data-stu-id="f66b0-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="f66b0-157">Pubblicare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f66b0-157">Publish hello application</span></span>
<span data-ttu-id="f66b0-158">toopublish, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f66b0-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="f66b0-159">**-ServiceName** specifica hello nome per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="f66b0-160">Deve essere un nome univoco, in caso contrario hello pubblicare processo avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f66b0-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="f66b0-161">Hello **Get-Date** comando puntine su una stringa di data/ora che è necessario rendere univoca con nome hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="f66b0-162">**-Location** specifica datacenter hello che verrà ospitata in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="f66b0-163">un elenco dei centri dati disponibili, utilizzare hello toosee **Get AzureLocation** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f66b0-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="f66b0-164">**-Avviare** apre una finestra del browser e passa il servizio ospitato toohello dopo la distribuzione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f66b0-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="f66b0-165">Dopo la pubblicazione riesce, verrà visualizzato di seguito toohello simile risposta:</span><span class="sxs-lookup"><span data-stu-id="f66b0-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![output di Hello di hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="f66b0-167">Può richiedere alcuni minuti per toodeploy applicazione hello e diventano disponibile durante la pubblicazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="f66b0-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="f66b0-168">Una volta completata la distribuzione di hello, una finestra del browser verrà aperto e passare servizio cloud toohello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Una finestra del browser pagina hello hello world; URL di Hello indica pagina hello è ospitato in Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="f66b0-170">L'applicazione è in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="f66b0-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="f66b0-171">Hello **pubblica AzureServiceProject** cmdlet esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f66b0-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="f66b0-172">Crea un pacchetto toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f66b0-172">Creates a package toodeploy.</span></span> <span data-ttu-id="f66b0-173">pacchetto di Hello contiene tutti i file hello nella cartella dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="f66b0-174">Crea un nuovo **account di archiviazione** nel caso non ne esista uno.</span><span class="sxs-lookup"><span data-stu-id="f66b0-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="f66b0-175">Hello account di archiviazione di Azure è pacchetto dell'applicazione hello toostore utilizzato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="f66b0-176">È possibile eliminare l'account di archiviazione di hello in modo sicuro al termine dell'operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f66b0-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="f66b0-177">Crea un nuovo **servizio cloud** nel caso in cui non ne esista già uno.</span><span class="sxs-lookup"><span data-stu-id="f66b0-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="f66b0-178">Oggetto **servizio cloud** hello contenitore in cui è ospitata l'applicazione quando è tooAzure distribuito.</span><span class="sxs-lookup"><span data-stu-id="f66b0-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="f66b0-179">Per altre informazioni, vedere [Creazione di un servizio ospitato per Azure].</span><span class="sxs-lookup"><span data-stu-id="f66b0-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="f66b0-180">Pubblica tooAzure pacchetto di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="f66b0-181">Arrestare ed eliminare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="f66b0-181">Stopping and deleting your application</span></span>
<span data-ttu-id="f66b0-182">Dopo aver distribuito l'applicazione, è opportuno toodisable in modo è possibile evitare i costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f66b0-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="f66b0-183">Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria.</span><span class="sxs-lookup"><span data-stu-id="f66b0-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="f66b0-184">Ora del server viene utilizzata una volta distribuita l'applicazione, anche se le istanze di hello non sono in esecuzione e sono in stato arrestato hello.</span><span class="sxs-lookup"><span data-stu-id="f66b0-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="f66b0-185">Nella finestra di Windows PowerShell hello, arrestare la distribuzione del servizio hello creata nella sezione precedente di hello con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f66b0-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="f66b0-186">L'arresto del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="f66b0-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="f66b0-187">Quando il servizio hello viene arrestato, viene visualizzato un messaggio che indica che è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="f66b0-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![stato di Hello del comando Stop-AzureService hello][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="f66b0-189">servizio di hello toodelete, hello chiamata seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f66b0-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="f66b0-190">Quando richiesto, immettere **Y** servizio hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="f66b0-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="f66b0-191">Eliminazione del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="f66b0-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="f66b0-192">Dopo aver eliminato il servizio hello viene visualizzato un messaggio che indica che il servizio di hello è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="f66b0-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![stato di Hello del comando Remove-AzureService hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="f66b0-194">Eliminazione del servizio di hello non comporta l'eliminazione account di archiviazione hello creato quando il servizio di hello inizialmente è stato pubblicato e si continuerà toobe fatturato per l'archiviazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="f66b0-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="f66b0-195">Se nessun altro elemento utilizza archiviazione hello, è opportuno toodelete è.</span><span class="sxs-lookup"><span data-stu-id="f66b0-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66b0-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f66b0-196">Next steps</span></span>
<span data-ttu-id="f66b0-197">Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js].</span><span class="sxs-lookup"><span data-stu-id="f66b0-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[confronto siti Web di Azure, servizi Cloud e macchine virtuali]: ../app-service-web/choose-web-site-cloud-service-vm.md
[usare un'app Web leggera]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK per .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[La connessione PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Creazione di un servizio ospitato per Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro per sviluppatori di Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
