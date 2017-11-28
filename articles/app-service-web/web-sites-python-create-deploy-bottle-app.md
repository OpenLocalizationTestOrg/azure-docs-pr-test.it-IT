---
title: App web aaaPython con Bottle in Azure
description: Un'esercitazione che illustra toorunning un'app web Python nelle App Web di servizio App di Azure.
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
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="dc4a5-103">Creazione di app Web con Bottle in Azure</span><span class="sxs-lookup"><span data-stu-id="dc4a5-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="dc4a5-104">In questa esercitazione viene descritto come tooget avviato Python nelle App Web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="dc4a5-105">Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!</span><span class="sxs-lookup"><span data-stu-id="dc4a5-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="dc4a5-106">Aumento delle dimensioni dell'app, è possibile passare toopaid hosting ed è inoltre possibile integrare con tutte hello altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="dc4a5-107">Si creerà un'app web utilizzando un framework web Bottle hello (vedere le versioni di questa esercitazione per [Django](web-sites-python-create-deploy-django-app.md) e [pallone](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="dc4a5-108">Si crea app web hello da hello Azure Marketplace, configurare la distribuzione Git e clonare il repository hello in locale.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="dc4a5-109">È quindi possibile verrà eseguito localmente l'app web hello, apportare modifiche, eseguire il commit e inviarli troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="dc4a5-110">Hello esercitazione viene illustrato come toodo da Windows o Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="dc4a5-111">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="dc4a5-112">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="dc4a5-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dc4a5-113">Prerequisites</span></span>
* <span data-ttu-id="dc4a5-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="dc4a5-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="dc4a5-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="dc4a5-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="dc4a5-116">setuptools, pip, virtualenv (solo Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="dc4a5-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="dc4a5-117">Git</span><span class="sxs-lookup"><span data-stu-id="dc4a5-117">Git</span></span>
* <span data-ttu-id="dc4a5-118">[Python Tools 2.2 per Visual Studio][Python Tools 2.2 per Visual Studio] (PTVS) - Nota: è facoltativo</span><span class="sxs-lookup"><span data-stu-id="dc4a5-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="dc4a5-119">**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="dc4a5-120">Windows</span><span class="sxs-lookup"><span data-stu-id="dc4a5-120">Windows</span></span>
<span data-ttu-id="dc4a5-121">Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="dc4a5-122">Versione a 32 bit hello di Python, setuptools, pip, virtualenv e così via (32 bit Python è ciò che viene installato nei computer host di Azure hello) vengono installati.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="dc4a5-123">In alternativa, è possibile ottenere Python da [python.org].</span><span class="sxs-lookup"><span data-stu-id="dc4a5-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="dc4a5-124">Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].</span><span class="sxs-lookup"><span data-stu-id="dc4a5-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="dc4a5-125">Se si utilizza Visual Studio, è possibile utilizzare il supporto di Git hello integrato.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="dc4a5-126">È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="dc4a5-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="dc4a5-127">Questa operazione è facoltativa, ma se dispone di [Visual Studio], tra cui hello liberare Visual Studio Community 2013 o Visual Studio Express 2013 per Web, quindi si riceverà un ottimo dell'IDE Python.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="dc4a5-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="dc4a5-128">Mac/Linux</span></span>
<span data-ttu-id="dc4a5-129">È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="dc4a5-130">Creazione di app Web nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="dc4a5-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="dc4a5-131">primo passaggio nella creazione dell'applicazione Hello è toocreate hello web app tramite hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="dc4a5-132">Accedere al portale di Azure hello e fare clic su hello **NEW** pulsante nell'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="dc4a5-133">Nella casella di ricerca hello, digitare "python".</span><span class="sxs-lookup"><span data-stu-id="dc4a5-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="dc4a5-134">Nei risultati della ricerca hello, selezionare **Bottle**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="dc4a5-135">Configurare hello nuova Bottle app, ad esempio la creazione di un nuovo piano di servizio App e un nuovo gruppo di risorse per tale.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="dc4a5-136">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="dc4a5-137">Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="dc4a5-138">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="dc4a5-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="dc4a5-139">Contenuti del repository Git</span><span class="sxs-lookup"><span data-stu-id="dc4a5-139">Git repository contents</span></span>
<span data-ttu-id="dc4a5-140">Di seguito è riportata una panoramica dei file hello che si trova nell'archivio Git iniziale hello, che è possibile clonare nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="dc4a5-141">Origini principali per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-141">Main sources for hello application.</span></span> <span data-ttu-id="dc4a5-142">È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="dc4a5-143">Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="dc4a5-144">Supporto del server di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-144">Local development server support.</span></span> <span data-ttu-id="dc4a5-145">Utilizzare questa applicazione hello toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="dc4a5-146">File di progetto da utilizzare con [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="dc4a5-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="dc4a5-147">Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="dc4a5-148">Pacchetti esterni necessari da parte di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-148">External packages needed by this application.</span></span> <span data-ttu-id="dc4a5-149">script di distribuzione Hello verrà pip pacchetti hello installazione elencati in questo file.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="dc4a5-150">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-150">IIS configuration files.</span></span> <span data-ttu-id="dc4a5-151">script di distribuzione Hello verrà utilizzata web.x.y.config appropriato hello e copiarlo come Web. config.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="dc4a5-152">File facoltativi - Personalizzazione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="dc4a5-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="dc4a5-153">File facoltativi - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="dc4a5-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="dc4a5-154">Altri file sul server</span><span class="sxs-lookup"><span data-stu-id="dc4a5-154">Additional files on server</span></span>
<span data-ttu-id="dc4a5-155">Alcuni file esistano nel server di hello ma non vengono aggiunti i repository git toohello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="dc4a5-156">Vengono creati tramite script di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="dc4a5-157">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-157">IIS configuration file.</span></span> <span data-ttu-id="dc4a5-158">Creato da web.x.y.config per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="dc4a5-159">Ambiente virtuale Python.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-159">Python virtual environment.</span></span> <span data-ttu-id="dc4a5-160">Se un ambiente virtuale compatibile non esiste già nell'applicazione web hello, creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="dc4a5-161">I pacchetti elencati in requirements.txt sono pip installato, ma pip ignorerà l'installazione se sono già installati i pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="dc4a5-162">Hello accanto 3 sezioni descrivono come tooproceed con hello web lo sviluppo di app in ambienti diversi 3:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="dc4a5-163">Windows, con Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc4a5-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="dc4a5-164">Windows, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="dc4a5-164">Windows, with command line</span></span>
* <span data-ttu-id="dc4a5-165">Mac/Linux, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="dc4a5-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="dc4a5-166">Sviluppo di app Web - Windows - Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc4a5-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="dc4a5-167">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="dc4a5-167">Clone hello repository</span></span>
<span data-ttu-id="dc4a5-168">In primo luogo, clonare il repository hello utilizzando url hello fornito nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="dc4a5-169">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="dc4a5-170">Aprire il file di soluzione hello (con estensione sln) che è incluso nella directory radice del repository hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="dc4a5-171">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="dc4a5-171">Create virtual environment</span></span>
<span data-ttu-id="dc4a5-172">A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="dc4a5-173">Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="dc4a5-174">Assicurarsi che il nome di hello dell'ambiente hello `env`.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="dc4a5-175">Selezionare l'interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-175">Select hello base interpreter.</span></span> <span data-ttu-id="dc4a5-176">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="dc4a5-177">Verificare che sia selezionata hello opzione toodownload e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="dc4a5-178">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-178">Click **Create**.</span></span> <span data-ttu-id="dc4a5-179">Questo verrà crea ambiente virtuale hello e installare le dipendenze elencate in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="dc4a5-180">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="dc4a5-180">Run using development server</span></span>
<span data-ttu-id="dc4a5-181">Premere F5 toostart debug e il browser verrà aperto automaticamente pagina toohello in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="dc4a5-182">È possibile impostare i punti di interruzione in origini hello, utilizzare le finestre Espressioni di controllo hello e così via. Vedere hello [Python Tools per la documentazione di Visual Studio] per ulteriori informazioni su hello varie funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="dc4a5-183">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="dc4a5-183">Make changes</span></span>
<span data-ttu-id="dc4a5-184">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="dc4a5-185">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="dc4a5-186">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc4a5-186">Install more packages</span></span>
<span data-ttu-id="dc4a5-187">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="dc4a5-188">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-188">You can install additional packages using pip.</span></span> <span data-ttu-id="dc4a5-189">tooinstall un pacchetto, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="dc4a5-190">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi di Azure, immettere `azure`:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="dc4a5-191">Fare clic sull'ambiente virtuale hello e selezionare **generare requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="dc4a5-192">Quindi, eseguire il commit del repository Git di hello modifiche toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="dc4a5-193">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="dc4a5-193">Deploy tooAzure</span></span>
<span data-ttu-id="dc4a5-194">tootrigger una distribuzione, fare clic su **sincronizzazione** o **Push**.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="dc4a5-195">La sincronizzazione esegue sia il push che il pull.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="dc4a5-196">prima distribuzione Hello richiederà del tempo, come verrà creato un ambiente virtuale, pacchetti di installazione e così via.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="dc4a5-197">Visual Studio non viene visualizzato lo stato di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="dc4a5-198">Se si desidera l'output di hello tooreview, vedere la sezione hello [Troubleshooting - distribuzione](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="dc4a5-199">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="dc4a5-200">Sviluppo di app Web - Windows - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="dc4a5-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="dc4a5-201">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="dc4a5-201">Clone hello repository</span></span>
<span data-ttu-id="dc4a5-202">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="dc4a5-203">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="dc4a5-204">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="dc4a5-204">Create virtual environment</span></span>
<span data-ttu-id="dc4a5-205">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="dc4a5-206">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="dc4a5-207">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione per l'app web nel portale di Azure hello runtime.txt o hello)</span><span class="sxs-lookup"><span data-stu-id="dc4a5-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="dc4a5-208">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="dc4a5-209">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="dc4a5-210">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-210">Install any external packages required by your application.</span></span> <span data-ttu-id="dc4a5-211">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="dc4a5-212">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="dc4a5-212">Run using development server</span></span>
<span data-ttu-id="dc4a5-213">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="dc4a5-214">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="dc4a5-215">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="dc4a5-216">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="dc4a5-216">Make changes</span></span>
<span data-ttu-id="dc4a5-217">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="dc4a5-218">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="dc4a5-219">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc4a5-219">Install more packages</span></span>
<span data-ttu-id="dc4a5-220">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="dc4a5-221">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-221">You can install additional packages using pip.</span></span> <span data-ttu-id="dc4a5-222">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="dc4a5-223">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="dc4a5-224">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="dc4a5-225">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="dc4a5-225">Deploy tooAzure</span></span>
<span data-ttu-id="dc4a5-226">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="dc4a5-227">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="dc4a5-228">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="dc4a5-229">Sviluppo del sito Web - Mac/Linux - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="dc4a5-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="dc4a5-230">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="dc4a5-230">Clone hello repository</span></span>
<span data-ttu-id="dc4a5-231">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="dc4a5-232">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="dc4a5-233">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="dc4a5-233">Create virtual environment</span></span>
<span data-ttu-id="dc4a5-234">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="dc4a5-235">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="dc4a5-236">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione runtime.txt o hello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="dc4a5-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="dc4a5-237">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="dc4a5-238">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="dc4a5-239">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="dc4a5-239">or pyvenv env</span></span>

<span data-ttu-id="dc4a5-240">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-240">Install any external packages required by your application.</span></span> <span data-ttu-id="dc4a5-241">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="dc4a5-242">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="dc4a5-242">Run using development server</span></span>
<span data-ttu-id="dc4a5-243">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="dc4a5-244">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="dc4a5-245">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="dc4a5-246">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="dc4a5-246">Make changes</span></span>
<span data-ttu-id="dc4a5-247">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="dc4a5-248">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="dc4a5-249">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc4a5-249">Install more packages</span></span>
<span data-ttu-id="dc4a5-250">L'applicazione può avere altre dipendenze oltre Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="dc4a5-251">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-251">You can install additional packages using pip.</span></span> <span data-ttu-id="dc4a5-252">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="dc4a5-253">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="dc4a5-254">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="dc4a5-255">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="dc4a5-255">Deploy tooAzure</span></span>
<span data-ttu-id="dc4a5-256">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="dc4a5-257">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="dc4a5-258">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="dc4a5-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="dc4a5-259">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc4a5-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="dc4a5-260">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="dc4a5-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="dc4a5-261">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc4a5-261">Next Steps</span></span>
<span data-ttu-id="dc4a5-262">Seguire questi toolearn collegamenti ulteriori sui Bottle e gli strumenti Python per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="dc4a5-263">[Documentazione di Bottle]</span><span class="sxs-lookup"><span data-stu-id="dc4a5-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="dc4a5-264">[Python Tools per la documentazione di Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="dc4a5-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="dc4a5-265">Per informazioni sull'uso di Archiviazione tabelle di Azure e MongoDB:</span><span class="sxs-lookup"><span data-stu-id="dc4a5-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="dc4a5-266">[Bottle e MongoDB in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="dc4a5-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="dc4a5-267">[Bottle e archiviazione tabelle di Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="dc4a5-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="dc4a5-268">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="dc4a5-268">What's changed</span></span>
* <span data-ttu-id="dc4a5-269">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="dc4a5-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle e MongoDB in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle e archiviazione tabelle di Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK per Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK per Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git per Windows]: http://msysgit.github.io/
[GitHub per Windows]: https://windows.github.com/
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools per la documentazione di Visual Studio]: http://aka.ms/ptvsdocs 
[Documentazione di Bottle]: http://bottlepy.org/docs/dev/index.html

