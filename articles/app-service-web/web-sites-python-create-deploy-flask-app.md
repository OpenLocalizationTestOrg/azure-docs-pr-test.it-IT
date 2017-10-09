---
title: App web aaaCreating con pallone in Azure
description: Un'esercitazione che illustra toorunning un'app web Python in Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="00abc-103">Creazione di app Web con Flask in Azure</span><span class="sxs-lookup"><span data-stu-id="00abc-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="00abc-104">In questa esercitazione descrive la modalità di avvio in esecuzione Python in tooget [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="00abc-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="00abc-105">Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!</span><span class="sxs-lookup"><span data-stu-id="00abc-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="00abc-106">Aumento delle dimensioni dell'app, è possibile passare toopaid hosting ed è inoltre possibile integrare con tutte hello altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="00abc-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="00abc-107">Si creerà un'applicazione tramite un framework web pallone hello (vedere le versioni di questa esercitazione per [Django](web-sites-python-create-deploy-django-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="00abc-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="00abc-108">Si crea sito Web di hello dalla raccolta di Azure hello, configurare la distribuzione Git e clonare il repository hello in locale.</span><span class="sxs-lookup"><span data-stu-id="00abc-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="00abc-109">Quindi verrà eseguito in locale un'applicazione hello, apportare modifiche, eseguire il commit e inviarli tooAzure.</span><span class="sxs-lookup"><span data-stu-id="00abc-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="00abc-110">Hello esercitazione viene illustrato come toodo da Windows o Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="00abc-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="00abc-111">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="00abc-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="00abc-112">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="00abc-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="00abc-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00abc-113">Prerequisites</span></span>
* <span data-ttu-id="00abc-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="00abc-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="00abc-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="00abc-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="00abc-116">setuptools, pip, virtualenv (solo Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="00abc-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="00abc-117">Git</span><span class="sxs-lookup"><span data-stu-id="00abc-117">Git</span></span>
* <span data-ttu-id="00abc-118">[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) - Nota: non è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="00abc-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="00abc-119">**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.</span><span class="sxs-lookup"><span data-stu-id="00abc-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="00abc-120">Windows</span><span class="sxs-lookup"><span data-stu-id="00abc-120">Windows</span></span>
<span data-ttu-id="00abc-121">Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="00abc-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="00abc-122">Versione a 32 bit hello di Python, setuptools, pip, virtualenv e così via (32 bit Python è ciò che viene installato nei computer host di Azure hello) vengono installati.</span><span class="sxs-lookup"><span data-stu-id="00abc-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="00abc-123">In alternativa, è possibile ottenere Python da [python.org].</span><span class="sxs-lookup"><span data-stu-id="00abc-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="00abc-124">Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].</span><span class="sxs-lookup"><span data-stu-id="00abc-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="00abc-125">Se si utilizza Visual Studio, è possibile utilizzare il supporto di Git hello integrato.</span><span class="sxs-lookup"><span data-stu-id="00abc-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="00abc-126">È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="00abc-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="00abc-127">Questa operazione è facoltativa, ma se dispone di [Visual Studio], tra cui hello liberare Visual Studio Community 2013 o Visual Studio Express 2013 per Web, quindi si riceverà un ottimo dell'IDE Python.</span><span class="sxs-lookup"><span data-stu-id="00abc-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="00abc-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="00abc-128">Mac/Linux</span></span>
<span data-ttu-id="00abc-129">È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="00abc-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="00abc-130">Creare app Web nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="00abc-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="00abc-131">primo passaggio nella creazione dell'applicazione Hello è toocreate hello web app tramite hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00abc-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="00abc-132">Accedere al portale di Azure hello e fare clic su hello **NEW** pulsante nell'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="00abc-133">Fare clic su **Web e dispositivi mobili**.</span><span class="sxs-lookup"><span data-stu-id="00abc-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="00abc-134">Nella casella di ricerca hello, digitare "python".</span><span class="sxs-lookup"><span data-stu-id="00abc-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="00abc-135">Nei risultati della ricerca hello, selezionare **pallone**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="00abc-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="00abc-136">Configurare hello nuova pallone app, ad esempio la creazione di un nuovo piano di servizio App e un nuovo gruppo di risorse per tale.</span><span class="sxs-lookup"><span data-stu-id="00abc-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="00abc-137">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="00abc-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="00abc-138">Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="00abc-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="00abc-139">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="00abc-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="00abc-140">Contenuti del repository Git</span><span class="sxs-lookup"><span data-stu-id="00abc-140">Git repository contents</span></span>
<span data-ttu-id="00abc-141">Di seguito è riportata una panoramica dei file hello che si trova nell'archivio Git iniziale hello, che è possibile clonare nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="00abc-142">Origini principali per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-142">Main sources for hello application.</span></span>  <span data-ttu-id="00abc-143">È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.</span><span class="sxs-lookup"><span data-stu-id="00abc-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="00abc-144">Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="00abc-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="00abc-145">Supporto del server di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="00abc-145">Local development server support.</span></span> <span data-ttu-id="00abc-146">Utilizzare questa applicazione hello toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="00abc-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="00abc-147">File di progetto da utilizzare con [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="00abc-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="00abc-148">Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.</span><span class="sxs-lookup"><span data-stu-id="00abc-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="00abc-149">Pacchetti esterni necessari da parte di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="00abc-149">External packages needed by this application.</span></span> <span data-ttu-id="00abc-150">script di distribuzione Hello verrà pip pacchetti hello installazione elencati in questo file.</span><span class="sxs-lookup"><span data-stu-id="00abc-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="00abc-151">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="00abc-151">IIS configuration files.</span></span>  <span data-ttu-id="00abc-152">script di distribuzione Hello verrà utilizzata web.x.y.config appropriato hello e copiarlo come Web. config.</span><span class="sxs-lookup"><span data-stu-id="00abc-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="00abc-153">File facoltativi - Personalizzazione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="00abc-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="00abc-154">File facoltativi - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="00abc-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="00abc-155">Altri file sul server</span><span class="sxs-lookup"><span data-stu-id="00abc-155">Additional files on server</span></span>
<span data-ttu-id="00abc-156">Alcuni file esistano nel server di hello ma non vengono aggiunti i repository git toohello.</span><span class="sxs-lookup"><span data-stu-id="00abc-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="00abc-157">Vengono creati tramite script di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="00abc-158">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="00abc-158">IIS configuration file.</span></span>  <span data-ttu-id="00abc-159">Creato da web.x.y.config per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="00abc-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="00abc-160">Ambiente virtuale Python.</span><span class="sxs-lookup"><span data-stu-id="00abc-160">Python virtual environment.</span></span>  <span data-ttu-id="00abc-161">Se un ambiente virtuale compatibile non esiste già nell'applicazione hello, creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="00abc-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="00abc-162">I pacchetti elencati in requirements.txt sono pip installato, ma pip ignorerà l'installazione se sono già installati i pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="00abc-163">Hello accanto 3 sezioni descrivono come tooproceed con hello web lo sviluppo di app in ambienti diversi 3:</span><span class="sxs-lookup"><span data-stu-id="00abc-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="00abc-164">Windows, con Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00abc-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="00abc-165">Windows, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="00abc-165">Windows, with command line</span></span>
* <span data-ttu-id="00abc-166">Mac/Linux, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="00abc-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="00abc-167">Sviluppo di siti Web - Windows - Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00abc-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="00abc-168">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="00abc-168">Clone hello repository</span></span>
<span data-ttu-id="00abc-169">In primo luogo, clonare il repository hello utilizzando URL hello fornito nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="00abc-170">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="00abc-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="00abc-171">Aprire il file di soluzione hello (con estensione sln) che è incluso nella directory radice del repository hello hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="00abc-172">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="00abc-172">Create virtual environment</span></span>
<span data-ttu-id="00abc-173">A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="00abc-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="00abc-174">Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).</span><span class="sxs-lookup"><span data-stu-id="00abc-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="00abc-175">Assicurarsi che il nome di hello dell'ambiente hello `env`.</span><span class="sxs-lookup"><span data-stu-id="00abc-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="00abc-176">Selezionare l'interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-176">Select hello base interpreter.</span></span>  <span data-ttu-id="00abc-177">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="00abc-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="00abc-178">Verificare che sia selezionata hello opzione toodownload e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="00abc-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="00abc-179">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="00abc-179">Click **Create**.</span></span>  <span data-ttu-id="00abc-180">Questo verrà crea ambiente virtuale hello e installare le dipendenze elencate in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="00abc-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="00abc-181">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="00abc-181">Run using development server</span></span>
<span data-ttu-id="00abc-182">Premere F5 toostart debug e il browser verrà aperto automaticamente pagina toohello in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="00abc-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="00abc-183">È possibile impostare i punti di interruzione in origini hello, utilizzare le finestre Espressioni di controllo hello e così via.  Vedere hello [Python Tools per la documentazione di Visual Studio] per ulteriori informazioni su hello varie funzionalità.</span><span class="sxs-lookup"><span data-stu-id="00abc-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="00abc-184">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="00abc-184">Make changes</span></span>
<span data-ttu-id="00abc-185">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="00abc-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="00abc-186">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="00abc-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="00abc-187">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="00abc-187">Install more packages</span></span>
<span data-ttu-id="00abc-188">L'applicazione potrebbe avere dipendenze oltre Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="00abc-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="00abc-189">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="00abc-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="00abc-190">tooinstall un pacchetto, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="00abc-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="00abc-191">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi di Azure, immettere `azure`:</span><span class="sxs-lookup"><span data-stu-id="00abc-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="00abc-192">Fare clic sull'ambiente virtuale hello e selezionare **generare requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="00abc-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="00abc-193">Quindi, eseguire il commit del repository Git di hello modifiche toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="00abc-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="00abc-194">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="00abc-194">Deploy tooAzure</span></span>
<span data-ttu-id="00abc-195">tootrigger una distribuzione, fare clic su **sincronizzazione** o **Push**.</span><span class="sxs-lookup"><span data-stu-id="00abc-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="00abc-196">La sincronizzazione esegue sia il push che il pull.</span><span class="sxs-lookup"><span data-stu-id="00abc-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="00abc-197">prima distribuzione Hello richiederà del tempo, come verrà creato un ambiente virtuale, pacchetti di installazione e così via.</span><span class="sxs-lookup"><span data-stu-id="00abc-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="00abc-198">Visual Studio non viene visualizzato lo stato di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="00abc-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="00abc-199">Se si desidera l'output di hello tooreview, vedere la sezione hello [Troubleshooting - distribuzione](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="00abc-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="00abc-200">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="00abc-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="00abc-201">Sviluppo di siti Web - Windows - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="00abc-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="00abc-202">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="00abc-202">Clone hello repository</span></span>
<span data-ttu-id="00abc-203">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="00abc-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="00abc-204">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="00abc-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="00abc-205">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="00abc-205">Create virtual environment</span></span>
<span data-ttu-id="00abc-206">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="00abc-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="00abc-207">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="00abc-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="00abc-208">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="00abc-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="00abc-209">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="00abc-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="00abc-210">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="00abc-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="00abc-211">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="00abc-211">Install any external packages required by your application.</span></span> <span data-ttu-id="00abc-212">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="00abc-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="00abc-213">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="00abc-213">Run using development server</span></span>
<span data-ttu-id="00abc-214">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="00abc-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="00abc-215">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="00abc-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="00abc-216">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="00abc-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="00abc-217">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="00abc-217">Make changes</span></span>
<span data-ttu-id="00abc-218">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="00abc-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="00abc-219">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="00abc-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="00abc-220">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="00abc-220">Install more packages</span></span>
<span data-ttu-id="00abc-221">L'applicazione potrebbe avere dipendenze oltre Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="00abc-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="00abc-222">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="00abc-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="00abc-223">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="00abc-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="00abc-224">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="00abc-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="00abc-225">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="00abc-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="00abc-226">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="00abc-226">Deploy tooAzure</span></span>
<span data-ttu-id="00abc-227">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="00abc-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="00abc-228">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="00abc-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="00abc-229">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="00abc-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="00abc-230">Sviluppo del sito Web - Mac/Linux - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="00abc-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="00abc-231">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="00abc-231">Clone hello repository</span></span>
<span data-ttu-id="00abc-232">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="00abc-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="00abc-233">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="00abc-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="00abc-234">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="00abc-234">Create virtual environment</span></span>
<span data-ttu-id="00abc-235">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="00abc-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="00abc-236">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="00abc-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="00abc-237">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="00abc-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="00abc-238">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="00abc-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="00abc-239">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="00abc-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="00abc-240">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="00abc-240">or pyvenv env</span></span>

<span data-ttu-id="00abc-241">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="00abc-241">Install any external packages required by your application.</span></span> <span data-ttu-id="00abc-242">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="00abc-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="00abc-243">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="00abc-243">Run using development server</span></span>
<span data-ttu-id="00abc-244">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="00abc-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="00abc-245">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="00abc-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="00abc-246">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="00abc-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="00abc-247">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="00abc-247">Make changes</span></span>
<span data-ttu-id="00abc-248">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="00abc-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="00abc-249">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="00abc-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="00abc-250">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="00abc-250">Install more packages</span></span>
<span data-ttu-id="00abc-251">L'applicazione potrebbe avere dipendenze oltre Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="00abc-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="00abc-252">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="00abc-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="00abc-253">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="00abc-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="00abc-254">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="00abc-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="00abc-255">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="00abc-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="00abc-256">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="00abc-256">Deploy tooAzure</span></span>
<span data-ttu-id="00abc-257">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="00abc-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="00abc-258">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="00abc-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="00abc-259">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="00abc-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="00abc-260">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="00abc-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="00abc-261">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="00abc-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="00abc-262">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00abc-262">Next Steps</span></span>
<span data-ttu-id="00abc-263">Seguire questi toolearn collegamenti ulteriori sui pallone e gli strumenti Python per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="00abc-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="00abc-264">[Documentazione di Flask]</span><span class="sxs-lookup"><span data-stu-id="00abc-264">[Flask Documentation]</span></span>
* <span data-ttu-id="00abc-265">[Python Tools per la documentazione di Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="00abc-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="00abc-266">Per informazioni sull'uso di Archiviazione tabelle di Azure e MongoDB:</span><span class="sxs-lookup"><span data-stu-id="00abc-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="00abc-267">[Flask e MongoDB in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="00abc-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="00abc-268">[Flask e archiviazione tabelle di Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="00abc-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="00abc-269">Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="00abc-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="00abc-270">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="00abc-270">What's changed</span></span>
* <span data-ttu-id="00abc-271">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="00abc-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask e MongoDB in Azure con Python Tools per Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask e archiviazione tabelle di Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Documentazione di Flask]: http://flask.pocoo.org/ 

