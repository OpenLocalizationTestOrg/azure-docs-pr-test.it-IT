---
title: App Web Python con Bottle in Azure
description: Un'esercitazione introduttiva all'esecuzione di un'app Web di Python in App Web del servizio app di Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="36eca-103">Creazione di app Web con Bottle in Azure</span><span class="sxs-lookup"><span data-stu-id="36eca-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="36eca-104">Questa esercitazione illustra le operazioni iniziali per l'esecuzione di Python in App Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="36eca-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="36eca-105">Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!</span><span class="sxs-lookup"><span data-stu-id="36eca-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="36eca-106">Se la crescita dell'applicazione lo richiede, è possibile passare all'hosting a pagamento e avvalersi dell'integrazione con tutti gli altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="36eca-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="36eca-107">Si creerà un'app Web usando il framework Web di Bottle. Vedere le versioni alternative di questa esercitazione per [Django](web-sites-python-create-deploy-django-app.md) e [Flask](web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="36eca-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="36eca-108">Verrà creato il sito Web dalla raccolta di Azure, sarà configurata la distribuzione Git e si procederà alla clonazione locale del repository.</span><span class="sxs-lookup"><span data-stu-id="36eca-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="36eca-109">Quindi si eseguirà l'applicazione localmente e si apporteranno le modifiche, che verranno sottoposte al commit e al push in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="36eca-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="36eca-110">Nell'esercitazione viene illustrato come eseguire queste operazioni da Windows o Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="36eca-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="36eca-111">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="36eca-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="36eca-112">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="36eca-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="36eca-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="36eca-113">Prerequisites</span></span>
* <span data-ttu-id="36eca-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="36eca-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="36eca-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="36eca-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="36eca-116">setuptools, pip, virtualenv (solo Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="36eca-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="36eca-117">Git</span><span class="sxs-lookup"><span data-stu-id="36eca-117">Git</span></span>
* <span data-ttu-id="36eca-118">[Python Tools 2.2 per Visual Studio][Python Tools 2.2 per Visual Studio] (PTVS) - Nota: è facoltativo</span><span class="sxs-lookup"><span data-stu-id="36eca-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="36eca-119">**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.</span><span class="sxs-lookup"><span data-stu-id="36eca-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="36eca-120">Windows</span><span class="sxs-lookup"><span data-stu-id="36eca-120">Windows</span></span>
<span data-ttu-id="36eca-121">Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="36eca-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="36eca-122">In tal modo viene installata la versione a 32 bit di Python, setuptools, pip, virtualenv e così via (Python a 32 bit è la versione installata sui computer host di Azure).</span><span class="sxs-lookup"><span data-stu-id="36eca-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="36eca-123">In alternativa, è possibile ottenere Python da [python.org].</span><span class="sxs-lookup"><span data-stu-id="36eca-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="36eca-124">Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].</span><span class="sxs-lookup"><span data-stu-id="36eca-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="36eca-125">Se si utilizza Visual Studio, è possibile utilizzare il supporto Git integrato.</span><span class="sxs-lookup"><span data-stu-id="36eca-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="36eca-126">È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="36eca-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="36eca-127">Si tratta di un'operazione facoltativa, ma se si dispone di [Visual Studio], inclusa la versione gratuita di Visual Studio Community 2013 o Visual Studio Express 2013 per il Web, si otterrà anche l'IDE Python.</span><span class="sxs-lookup"><span data-stu-id="36eca-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="36eca-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="36eca-128">Mac/Linux</span></span>
<span data-ttu-id="36eca-129">È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="36eca-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="36eca-130">Creazione di un'app Web nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="36eca-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="36eca-131">Il primo passaggio per la creazione di un'app consiste nella creazione dell'app Web tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36eca-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="36eca-132">Accedere al portale di Azure e scegliere il **nuovo** pulsante nell'angolo inferiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="36eca-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="36eca-133">Nella casella di ricerca digitare "python".</span><span class="sxs-lookup"><span data-stu-id="36eca-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="36eca-134">Nei risultati della ricerca selezionare **Bottle** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="36eca-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="36eca-135">Configurare la nuova app Bottle, ad esempio creando un nuovo piano di servizio app e un nuovo gruppo di risorse correlato.</span><span class="sxs-lookup"><span data-stu-id="36eca-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="36eca-136">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="36eca-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="36eca-137">Configurare la pubblicazione Git per l'app Web appena creata seguendo le istruzioni disponibili in [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="36eca-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="36eca-138">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="36eca-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="36eca-139">Contenuti del repository Git</span><span class="sxs-lookup"><span data-stu-id="36eca-139">Git repository contents</span></span>
<span data-ttu-id="36eca-140">Di seguito viene fornita una panoramica dei file contenuti nel repository Git iniziale, che saranno clonati nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="36eca-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="36eca-141">Fonti principali per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36eca-141">Main sources for the application.</span></span> <span data-ttu-id="36eca-142">È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.</span><span class="sxs-lookup"><span data-stu-id="36eca-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="36eca-143">Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="36eca-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="36eca-144">Supporto del server di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="36eca-144">Local development server support.</span></span> <span data-ttu-id="36eca-145">Consente di eseguire l'applicazione localmente.</span><span class="sxs-lookup"><span data-stu-id="36eca-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="36eca-146">File di progetto da utilizzare con [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="36eca-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="36eca-147">Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.</span><span class="sxs-lookup"><span data-stu-id="36eca-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="36eca-148">Pacchetti esterni necessari da parte di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="36eca-148">External packages needed by this application.</span></span> <span data-ttu-id="36eca-149">Lo script di distribuzione eseguirà l'installazione di pip dei pacchetti elencati in questo file.</span><span class="sxs-lookup"><span data-stu-id="36eca-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="36eca-150">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="36eca-150">IIS configuration files.</span></span> <span data-ttu-id="36eca-151">Lo script di distribuzione utilizzerà il file appropriato web.x.y.config e lo copierà come web.config.</span><span class="sxs-lookup"><span data-stu-id="36eca-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="36eca-152">File facoltativi - Personalizzazione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="36eca-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="36eca-153">File facoltativi - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="36eca-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="36eca-154">Altri file sul server</span><span class="sxs-lookup"><span data-stu-id="36eca-154">Additional files on server</span></span>
<span data-ttu-id="36eca-155">Alcuni file sono presenti sul server ma non vengono aggiunti al repository Git.</span><span class="sxs-lookup"><span data-stu-id="36eca-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="36eca-156">Si tratta di file creati dallo script di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="36eca-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="36eca-157">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="36eca-157">IIS configuration file.</span></span> <span data-ttu-id="36eca-158">Creato da web.x.y.config per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="36eca-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="36eca-159">Ambiente virtuale Python.</span><span class="sxs-lookup"><span data-stu-id="36eca-159">Python virtual environment.</span></span> <span data-ttu-id="36eca-160">Creato durante la distribuzione se sul sito non esiste già un ambiente virtuale compatibile.</span><span class="sxs-lookup"><span data-stu-id="36eca-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="36eca-161">I pacchetti elencati in requirements.txt vengono installati con pip. Tuttavia, se i pacchetti sono installati, l'installazione di pip non verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="36eca-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="36eca-162">Nelle tre sezioni successive viene descritto come procedere con lo sviluppo dei siti Web in tre ambienti diversi:</span><span class="sxs-lookup"><span data-stu-id="36eca-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="36eca-163">Windows, con Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36eca-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="36eca-164">Windows, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="36eca-164">Windows, with command line</span></span>
* <span data-ttu-id="36eca-165">Mac/Linux, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="36eca-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="36eca-166">Sviluppo di app Web - Windows - Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36eca-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="36eca-167">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="36eca-167">Clone the repository</span></span>
<span data-ttu-id="36eca-168">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="36eca-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="36eca-169">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="36eca-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="36eca-170">Aprire il file della soluzione (.sln) incluso nella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="36eca-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="36eca-171">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="36eca-171">Create virtual environment</span></span>
<span data-ttu-id="36eca-172">A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="36eca-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="36eca-173">Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).</span><span class="sxs-lookup"><span data-stu-id="36eca-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="36eca-174">Assicurarsi che il nome dell'ambiente sia `env`.</span><span class="sxs-lookup"><span data-stu-id="36eca-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="36eca-175">Selezionare l'interprete di base.</span><span class="sxs-lookup"><span data-stu-id="36eca-175">Select the base interpreter.</span></span> <span data-ttu-id="36eca-176">Assicurarsi di utilizzare la stessa versione di Python è selezionata per l'applicazione web (in runtime.txt o **le impostazioni dell'applicazione** blade dell'applicazione web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="36eca-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="36eca-177">Assicurarsi che l'opzione per scaricare e installare i pacchetti sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="36eca-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="36eca-178">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="36eca-178">Click **Create**.</span></span> <span data-ttu-id="36eca-179">In tal modo verrà creato l'ambiente virtuale e verranno installate le dipendenze elencate in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="36eca-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="36eca-180">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="36eca-180">Run using development server</span></span>
<span data-ttu-id="36eca-181">Premere F5 per avviare il debug. Il Web browser si aprirà automaticamente sulla pagina in esecuzione locale.</span><span class="sxs-lookup"><span data-stu-id="36eca-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="36eca-182">È possibile impostare punti di interruzione nelle origini, utilizzare le finestre Espressioni di controllo e così via. Per altre informazioni sulle varie funzionalità, vedere la [documentazione di Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="36eca-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="36eca-183">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="36eca-183">Make changes</span></span>
<span data-ttu-id="36eca-184">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="36eca-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="36eca-185">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="36eca-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="36eca-186">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="36eca-186">Install more packages</span></span>
<span data-ttu-id="36eca-187">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="36eca-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="36eca-188">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="36eca-188">You can install additional packages using pip.</span></span> <span data-ttu-id="36eca-189">Per installare un pacchetto, fare clic con il pulsante destro del mouse e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="36eca-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="36eca-190">Ad esempio, per installare Azure SDK per Python, che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, immettere `azure`:</span><span class="sxs-lookup"><span data-stu-id="36eca-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="36eca-191">Fare clic con il pulsante destro del mouse sull'ambiente virtuale e selezionare **Genera requirements.txt** per aggiornare requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="36eca-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="36eca-192">Quindi, eseguire il commit delle modifiche a requirements.txt al repository Git.</span><span class="sxs-lookup"><span data-stu-id="36eca-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="36eca-193">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="36eca-193">Deploy to Azure</span></span>
<span data-ttu-id="36eca-194">Per attivare una distribuzione, fare clic su **Sincronizza** o su **Push**.</span><span class="sxs-lookup"><span data-stu-id="36eca-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="36eca-195">La sincronizzazione esegue sia il push che il pull.</span><span class="sxs-lookup"><span data-stu-id="36eca-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="36eca-196">La prima distribuzione richiederà un po' di tempo, in quanto verrà creato un ambiente virtuale, si installeranno i pacchetti e così via.</span><span class="sxs-lookup"><span data-stu-id="36eca-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="36eca-197">In Visual Studio non viene visualizzato l'avanzamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="36eca-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="36eca-198">Se si desidera rivedere l'output, vedere la sezione in [Risoluzione dei problemi- Distribuzione](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="36eca-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="36eca-199">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="36eca-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="36eca-200">Sviluppo di app Web - Windows - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="36eca-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="36eca-201">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="36eca-201">Clone the repository</span></span>
<span data-ttu-id="36eca-202">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure e aggiungere il repository di Azure come remoto.</span><span class="sxs-lookup"><span data-stu-id="36eca-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="36eca-203">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="36eca-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="36eca-204">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="36eca-204">Create virtual environment</span></span>
<span data-ttu-id="36eca-205">Verrà creato un nuovo ambiente virtuale per lo sviluppo (non aggiungerlo al repository).</span><span class="sxs-lookup"><span data-stu-id="36eca-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="36eca-206">Non è possibile cambiare la posizione degli ambienti virtuali in Python, pertanto, ciascuno sviluppatore che lavora all'applicazione ne creerà una locale.</span><span class="sxs-lookup"><span data-stu-id="36eca-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="36eca-207">Assicurarsi di utilizzare la stessa versione di Python selezionata per l'app web (in runtime.txt o nel pannello delle impostazioni dell'applicazione per l’app web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="36eca-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="36eca-208">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="36eca-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="36eca-209">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="36eca-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="36eca-210">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36eca-210">Install any external packages required by your application.</span></span> <span data-ttu-id="36eca-211">È possibile utilizzare il file requirements.txt nella radice del repository per installare i pacchetti nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="36eca-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="36eca-212">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="36eca-212">Run using development server</span></span>
<span data-ttu-id="36eca-213">È possibile avviare l'applicazione in un server di sviluppo con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="36eca-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="36eca-214">Sulla console verranno visualizzati l'URL e la porta su cui è in ascolto il server:</span><span class="sxs-lookup"><span data-stu-id="36eca-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="36eca-215">Quindi, aprire il Web browser su tale URL.</span><span class="sxs-lookup"><span data-stu-id="36eca-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="36eca-216">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="36eca-216">Make changes</span></span>
<span data-ttu-id="36eca-217">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="36eca-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="36eca-218">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="36eca-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="36eca-219">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="36eca-219">Install more packages</span></span>
<span data-ttu-id="36eca-220">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="36eca-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="36eca-221">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="36eca-221">You can install additional packages using pip.</span></span> <span data-ttu-id="36eca-222">Ad esempio, per installare Azure SDK per Python,che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="36eca-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="36eca-223">Assicurarsi di aggiornare requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="36eca-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="36eca-224">Eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="36eca-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="36eca-225">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="36eca-225">Deploy to Azure</span></span>
<span data-ttu-id="36eca-226">Per attivare una distribuzione, eseguire il push delle modifiche in Azure:</span><span class="sxs-lookup"><span data-stu-id="36eca-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="36eca-227">Verrà visualizzato l'output dello script di distribuzione, inclusa la creazione dell'ambiente virtuale, l'installazione di pacchetti, la creazione di web.config.</span><span class="sxs-lookup"><span data-stu-id="36eca-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="36eca-228">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="36eca-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="36eca-229">Sviluppo del sito Web - Mac/Linux - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="36eca-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="36eca-230">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="36eca-230">Clone the repository</span></span>
<span data-ttu-id="36eca-231">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure e aggiungere il repository di Azure come remoto.</span><span class="sxs-lookup"><span data-stu-id="36eca-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="36eca-232">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="36eca-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="36eca-233">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="36eca-233">Create virtual environment</span></span>
<span data-ttu-id="36eca-234">Verrà creato un nuovo ambiente virtuale per lo sviluppo (non aggiungerlo al repository).</span><span class="sxs-lookup"><span data-stu-id="36eca-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="36eca-235">Non è possibile cambiare la posizione degli ambienti virtuali in Python, pertanto, ciascuno sviluppatore che lavora all'applicazione ne creerà una locale.</span><span class="sxs-lookup"><span data-stu-id="36eca-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="36eca-236">Assicurarsi di utilizzare la stessa versione di Python è selezionata per l'applicazione web (in runtime.txt o blade le impostazioni dell'applicazione dell'applicazione web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="36eca-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="36eca-237">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="36eca-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="36eca-238">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="36eca-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="36eca-239">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="36eca-239">or pyvenv env</span></span>

<span data-ttu-id="36eca-240">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36eca-240">Install any external packages required by your application.</span></span> <span data-ttu-id="36eca-241">È possibile utilizzare il file requirements.txt nella radice del repository per installare i pacchetti nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="36eca-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="36eca-242">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="36eca-242">Run using development server</span></span>
<span data-ttu-id="36eca-243">È possibile avviare l'applicazione in un server di sviluppo con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="36eca-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="36eca-244">Sulla console verranno visualizzati l'URL e la porta su cui è in ascolto il server:</span><span class="sxs-lookup"><span data-stu-id="36eca-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="36eca-245">Quindi, aprire il Web browser su tale URL.</span><span class="sxs-lookup"><span data-stu-id="36eca-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="36eca-246">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="36eca-246">Make changes</span></span>
<span data-ttu-id="36eca-247">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="36eca-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="36eca-248">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="36eca-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="36eca-249">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="36eca-249">Install more packages</span></span>
<span data-ttu-id="36eca-250">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="36eca-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="36eca-251">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="36eca-251">You can install additional packages using pip.</span></span> <span data-ttu-id="36eca-252">Ad esempio, per installare Azure SDK per Python,che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="36eca-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="36eca-253">Assicurarsi di aggiornare requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="36eca-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="36eca-254">Eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="36eca-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="36eca-255">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="36eca-255">Deploy to Azure</span></span>
<span data-ttu-id="36eca-256">Per attivare una distribuzione, eseguire il push delle modifiche in Azure:</span><span class="sxs-lookup"><span data-stu-id="36eca-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="36eca-257">Verrà visualizzato l'output dello script di distribuzione, inclusa la creazione dell'ambiente virtuale, l'installazione di pacchetti, la creazione di web.config.</span><span class="sxs-lookup"><span data-stu-id="36eca-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="36eca-258">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="36eca-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="36eca-259">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="36eca-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="36eca-260">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="36eca-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="36eca-261">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36eca-261">Next Steps</span></span>
<span data-ttu-id="36eca-262">Visitare i seguenti collegamenti per altre informazioni su Bottle e Python Tools per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="36eca-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="36eca-263">[Documentazione di Bottle]</span><span class="sxs-lookup"><span data-stu-id="36eca-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="36eca-264">[documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="36eca-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="36eca-265">Per informazioni sull'uso di Archiviazione tabelle di Azure e MongoDB:</span><span class="sxs-lookup"><span data-stu-id="36eca-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="36eca-266">[Bottle e MongoDB in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="36eca-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="36eca-267">[Bottle e archiviazione tabelle di Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="36eca-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="36eca-268">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="36eca-268">What's changed</span></span>
* <span data-ttu-id="36eca-269">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="36eca-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="36eca-270">[Bottle e MongoDB in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="36eca-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="36eca-271">[Bottle e archiviazione tabelle di Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="36eca-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="36eca-272">[Azure SDK per Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="36eca-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="36eca-273">[Azure SDK per Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="36eca-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="36eca-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="36eca-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="36eca-275">[Git per Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="36eca-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="36eca-276">[GitHub per Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="36eca-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="36eca-277">[Python Tools per Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="36eca-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="36eca-278">[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="36eca-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="36eca-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="36eca-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="36eca-280">[documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="36eca-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="36eca-281">[Documentazione di Bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="36eca-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

