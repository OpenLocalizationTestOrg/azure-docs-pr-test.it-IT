---
title: App web aaaCreating con Django in Azure
description: Un'esercitazione che illustra toorunning un'app web Python nelle App Web di servizio App di Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="974a8-103">Creazione di app Web con Django</span><span class="sxs-lookup"><span data-stu-id="974a8-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="974a8-104">Questa esercitazione viene descritto come tooget ha avviato l'esecuzione Python [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="974a8-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="974a8-105">Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!</span><span class="sxs-lookup"><span data-stu-id="974a8-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="974a8-106">Aumento delle dimensioni dell'app, è possibile passare toopaid hosting ed è inoltre possibile integrare con tutte hello altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="974a8-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="974a8-107">Si creerà un'applicazione tramite un framework web Django hello (vedere le versioni di questa esercitazione per [pallone](web-sites-python-create-deploy-flask-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="974a8-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="974a8-108">Si crea app web hello da hello Azure Marketplace, configurare la distribuzione Git e clonare il repository hello in locale.</span><span class="sxs-lookup"><span data-stu-id="974a8-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="974a8-109">Quindi verrà eseguito in locale un'applicazione hello, apportare modifiche, eseguire il commit e inviarli tooAzure.</span><span class="sxs-lookup"><span data-stu-id="974a8-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="974a8-110">Hello esercitazione viene illustrato come toodo da Windows o Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="974a8-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="974a8-111">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="974a8-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="974a8-112">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="974a8-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="974a8-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="974a8-113">Prerequisites</span></span>
* <span data-ttu-id="974a8-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="974a8-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="974a8-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="974a8-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="974a8-116">setuptools, pip, virtualenv (solo Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="974a8-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="974a8-117">Git</span><span class="sxs-lookup"><span data-stu-id="974a8-117">Git</span></span>
* <span data-ttu-id="974a8-118">[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) - Nota: non è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="974a8-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="974a8-119">**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.</span><span class="sxs-lookup"><span data-stu-id="974a8-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="974a8-120">Windows</span><span class="sxs-lookup"><span data-stu-id="974a8-120">Windows</span></span>
<span data-ttu-id="974a8-121">Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="974a8-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="974a8-122">Versione a 32 bit hello di Python, setuptools, pip, virtualenv e così via (32 bit Python è ciò che viene installato nei computer host di Azure hello) vengono installati.</span><span class="sxs-lookup"><span data-stu-id="974a8-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="974a8-123">In alternativa, è possibile ottenere Python da [python.org].</span><span class="sxs-lookup"><span data-stu-id="974a8-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="974a8-124">Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].</span><span class="sxs-lookup"><span data-stu-id="974a8-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="974a8-125">Se si utilizza Visual Studio, è possibile utilizzare il supporto di Git hello integrato.</span><span class="sxs-lookup"><span data-stu-id="974a8-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="974a8-126">È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="974a8-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="974a8-127">Questa operazione è facoltativa, ma se dispone di [Visual Studio], tra cui hello liberare Visual Studio Community 2013 o Visual Studio Express 2013 per Web, quindi si riceverà un ottimo dell'IDE Python.</span><span class="sxs-lookup"><span data-stu-id="974a8-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="974a8-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="974a8-128">Mac/Linux</span></span>
<span data-ttu-id="974a8-129">È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="974a8-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="974a8-130">Creazione delle app Web sul portale</span><span class="sxs-lookup"><span data-stu-id="974a8-130">Web App Creation on Portal</span></span>
<span data-ttu-id="974a8-131">primo passaggio nella creazione dell'applicazione Hello è toocreate hello web app tramite hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="974a8-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="974a8-132">Accedere al portale di Azure hello e fare clic su hello **NEW** pulsante nell'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="974a8-133">Nella casella di ricerca hello, digitare "python".</span><span class="sxs-lookup"><span data-stu-id="974a8-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="974a8-134">Nei risultati della ricerca hello, selezionare **Django** (pubblicato da PTVS), quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="974a8-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="974a8-135">Configurare hello nuova Django app, ad esempio la creazione di un nuovo piano di servizio App e un nuovo gruppo di risorse per tale.</span><span class="sxs-lookup"><span data-stu-id="974a8-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="974a8-136">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="974a8-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="974a8-137">Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="974a8-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="974a8-138">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="974a8-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="974a8-139">Contenuti del repository Git</span><span class="sxs-lookup"><span data-stu-id="974a8-139">Git repository contents</span></span>
<span data-ttu-id="974a8-140">Di seguito è riportata una panoramica dei file hello che si trova nell'archivio Git iniziale hello, che è possibile clonare nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="974a8-141">Origini principali per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-141">Main sources for hello application.</span></span> <span data-ttu-id="974a8-142">È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.</span><span class="sxs-lookup"><span data-stu-id="974a8-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="974a8-143">Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="974a8-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="974a8-144">Gestione locale e supporto serve di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="974a8-144">Local management and development server support.</span></span> <span data-ttu-id="974a8-145">Utilizzare questa applicazione hello toorun localmente, la sincronizzazione database hello e così via.</span><span class="sxs-lookup"><span data-stu-id="974a8-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="974a8-146">Database predefinito.</span><span class="sxs-lookup"><span data-stu-id="974a8-146">Default database.</span></span> <span data-ttu-id="974a8-147">Include le tabelle necessarie hello per toorun applicazione hello, ma non contiene tutti gli utenti (sincronizzazione hello database toocreate un utente).</span><span class="sxs-lookup"><span data-stu-id="974a8-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="974a8-148">File di progetto da utilizzare con [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="974a8-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="974a8-149">Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.</span><span class="sxs-lookup"><span data-stu-id="974a8-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="974a8-150">Pacchetti esterni necessari da parte di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="974a8-150">External packages needed by this application.</span></span> <span data-ttu-id="974a8-151">script di distribuzione Hello verrà pip pacchetti hello installazione elencati in questo file.</span><span class="sxs-lookup"><span data-stu-id="974a8-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="974a8-152">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="974a8-152">IIS configuration files.</span></span> <span data-ttu-id="974a8-153">script di distribuzione Hello verrà utilizzata web.x.y.config appropriato hello e copiarlo come Web. config.</span><span class="sxs-lookup"><span data-stu-id="974a8-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="974a8-154">File facoltativi - Personalizzazione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="974a8-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="974a8-155">File facoltativi - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="974a8-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="974a8-156">Altri file sul server</span><span class="sxs-lookup"><span data-stu-id="974a8-156">Additional files on server</span></span>
<span data-ttu-id="974a8-157">Alcuni file esistano nel server di hello ma non vengono aggiunti i repository git toohello.</span><span class="sxs-lookup"><span data-stu-id="974a8-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="974a8-158">Vengono creati tramite script di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="974a8-159">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="974a8-159">IIS configuration file.</span></span> <span data-ttu-id="974a8-160">Creato da web.x.y.config per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="974a8-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="974a8-161">Ambiente virtuale Python.</span><span class="sxs-lookup"><span data-stu-id="974a8-161">Python virtual environment.</span></span> <span data-ttu-id="974a8-162">Se un ambiente virtuale compatibile non esiste già nell'applicazione web hello, creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="974a8-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="974a8-163">I pacchetti elencati in requirements.txt sono pip installato, ma pip ignorerà l'installazione se sono già installati i pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="974a8-164">Hello accanto 3 sezioni descrivono come tooproceed con hello web lo sviluppo di app in ambienti diversi 3:</span><span class="sxs-lookup"><span data-stu-id="974a8-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="974a8-165">Windows, con Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974a8-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="974a8-166">Windows, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="974a8-166">Windows, with command line</span></span>
* <span data-ttu-id="974a8-167">Mac/Linux, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="974a8-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="974a8-168">Sviluppo di siti Web - Windows - Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="974a8-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="974a8-169">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="974a8-169">Clone hello repository</span></span>
<span data-ttu-id="974a8-170">In primo luogo, clonare il repository hello utilizzando URL hello fornito nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="974a8-171">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="974a8-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="974a8-172">Aprire il file di soluzione hello (con estensione sln) che è incluso nella directory radice del repository hello hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="974a8-173">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="974a8-173">Create virtual environment</span></span>
<span data-ttu-id="974a8-174">A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="974a8-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="974a8-175">Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).</span><span class="sxs-lookup"><span data-stu-id="974a8-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="974a8-176">Assicurarsi che il nome di hello dell'ambiente hello `env`.</span><span class="sxs-lookup"><span data-stu-id="974a8-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="974a8-177">Selezionare l'interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-177">Select hello base interpreter.</span></span> <span data-ttu-id="974a8-178">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="974a8-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="974a8-179">Verificare che sia selezionata hello opzione toodownload e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="974a8-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="974a8-180">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="974a8-180">Click **Create**.</span></span> <span data-ttu-id="974a8-181">Questo verrà crea ambiente virtuale hello e installare le dipendenze elencate in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="974a8-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="974a8-182">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="974a8-182">Create a superuser</span></span>
<span data-ttu-id="974a8-183">database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito.</span><span class="sxs-lookup"><span data-stu-id="974a8-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="974a8-184">Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="974a8-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="974a8-185">Eseguire questo dalla hello della riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="974a8-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="974a8-186">Seguire il nome utente hello di hello prompt tooset, password e così via.</span><span class="sxs-lookup"><span data-stu-id="974a8-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="974a8-187">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="974a8-187">Run using development server</span></span>
<span data-ttu-id="974a8-188">Premere F5 toostart debug e il browser verrà aperto automaticamente pagina toohello in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="974a8-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="974a8-189">È possibile impostare i punti di interruzione in origini hello, utilizzare le finestre Espressioni di controllo hello e così via. Vedere hello [Python Tools per la documentazione di Visual Studio] per ulteriori informazioni su hello varie funzionalità.</span><span class="sxs-lookup"><span data-stu-id="974a8-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="974a8-190">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="974a8-190">Make changes</span></span>
<span data-ttu-id="974a8-191">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="974a8-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="974a8-192">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="974a8-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="974a8-193">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="974a8-193">Install more packages</span></span>
<span data-ttu-id="974a8-194">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="974a8-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="974a8-195">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="974a8-195">You can install additional packages using pip.</span></span> <span data-ttu-id="974a8-196">tooinstall un pacchetto, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="974a8-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="974a8-197">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi di Azure, immettere `azure`:</span><span class="sxs-lookup"><span data-stu-id="974a8-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="974a8-198">Fare clic sull'ambiente virtuale hello e selezionare **generare requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="974a8-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="974a8-199">Quindi, eseguire il commit del repository Git di hello modifiche toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="974a8-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="974a8-200">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="974a8-200">Deploy tooAzure</span></span>
<span data-ttu-id="974a8-201">tootrigger una distribuzione, fare clic su **sincronizzazione** o **Push**.</span><span class="sxs-lookup"><span data-stu-id="974a8-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="974a8-202">La sincronizzazione esegue sia il push che il pull.</span><span class="sxs-lookup"><span data-stu-id="974a8-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="974a8-203">prima distribuzione Hello richiederà del tempo, come verrà creato un ambiente virtuale, pacchetti di installazione e così via.</span><span class="sxs-lookup"><span data-stu-id="974a8-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="974a8-204">Visual Studio non viene visualizzato lo stato di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="974a8-205">Se si desidera l'output di hello tooreview, vedere la sezione hello [Troubleshooting - distribuzione](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="974a8-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="974a8-206">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="974a8-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="974a8-207">Sviluppo di siti Web - Windows - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="974a8-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="974a8-208">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="974a8-208">Clone hello repository</span></span>
<span data-ttu-id="974a8-209">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="974a8-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="974a8-210">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="974a8-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="974a8-211">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="974a8-211">Create virtual environment</span></span>
<span data-ttu-id="974a8-212">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="974a8-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="974a8-213">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="974a8-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="974a8-214">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione runtime.txt o hello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="974a8-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="974a8-215">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="974a8-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="974a8-216">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="974a8-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="974a8-217">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="974a8-217">Install any external packages required by your application.</span></span> <span data-ttu-id="974a8-218">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="974a8-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="974a8-219">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="974a8-219">Create a superuser</span></span>
<span data-ttu-id="974a8-220">database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito.</span><span class="sxs-lookup"><span data-stu-id="974a8-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="974a8-221">Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="974a8-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="974a8-222">Eseguire questo dalla hello della riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="974a8-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="974a8-223">Seguire il nome utente hello di hello prompt tooset, password e così via.</span><span class="sxs-lookup"><span data-stu-id="974a8-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="974a8-224">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="974a8-224">Run using development server</span></span>
<span data-ttu-id="974a8-225">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="974a8-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="974a8-226">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="974a8-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="974a8-227">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="974a8-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="974a8-228">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="974a8-228">Make changes</span></span>
<span data-ttu-id="974a8-229">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="974a8-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="974a8-230">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="974a8-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="974a8-231">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="974a8-231">Install more packages</span></span>
<span data-ttu-id="974a8-232">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="974a8-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="974a8-233">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="974a8-233">You can install additional packages using pip.</span></span> <span data-ttu-id="974a8-234">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="974a8-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="974a8-235">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="974a8-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="974a8-236">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="974a8-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="974a8-237">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="974a8-237">Deploy tooAzure</span></span>
<span data-ttu-id="974a8-238">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="974a8-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="974a8-239">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="974a8-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="974a8-240">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="974a8-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="974a8-241">Sviluppo del sito Web - Mac/Linux - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="974a8-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="974a8-242">Repository di hello clone</span><span class="sxs-lookup"><span data-stu-id="974a8-242">Clone hello repository</span></span>
<span data-ttu-id="974a8-243">In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota.</span><span class="sxs-lookup"><span data-stu-id="974a8-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="974a8-244">Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="974a8-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="974a8-245">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="974a8-245">Create virtual environment</span></span>
<span data-ttu-id="974a8-246">Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).</span><span class="sxs-lookup"><span data-stu-id="974a8-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="974a8-247">Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.</span><span class="sxs-lookup"><span data-stu-id="974a8-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="974a8-248">Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione runtime.txt o hello dell'app web nel portale di Azure hello).</span><span class="sxs-lookup"><span data-stu-id="974a8-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="974a8-249">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="974a8-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="974a8-250">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="974a8-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="974a8-251">oppure</span><span class="sxs-lookup"><span data-stu-id="974a8-251">or</span></span>

    pyvenv env

<span data-ttu-id="974a8-252">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="974a8-252">Install any external packages required by your application.</span></span> <span data-ttu-id="974a8-253">È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="974a8-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="974a8-254">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="974a8-254">Create a superuser</span></span>
<span data-ttu-id="974a8-255">database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito.</span><span class="sxs-lookup"><span data-stu-id="974a8-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="974a8-256">Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="974a8-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="974a8-257">Eseguire questo dalla hello della riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="974a8-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="974a8-258">Seguire il nome utente hello di hello prompt tooset, password e così via.</span><span class="sxs-lookup"><span data-stu-id="974a8-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="974a8-259">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="974a8-259">Run using development server</span></span>
<span data-ttu-id="974a8-260">È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="974a8-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="974a8-261">console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:</span><span class="sxs-lookup"><span data-stu-id="974a8-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="974a8-262">Quindi, aprire l'URL di web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="974a8-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="974a8-263">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="974a8-263">Make changes</span></span>
<span data-ttu-id="974a8-264">Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.</span><span class="sxs-lookup"><span data-stu-id="974a8-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="974a8-265">Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:</span><span class="sxs-lookup"><span data-stu-id="974a8-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="974a8-266">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="974a8-266">Install more packages</span></span>
<span data-ttu-id="974a8-267">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="974a8-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="974a8-268">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="974a8-268">You can install additional packages using pip.</span></span> <span data-ttu-id="974a8-269">Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="974a8-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="974a8-270">Verificare che tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="974a8-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="974a8-271">Eseguire il commit delle modifiche hello:</span><span class="sxs-lookup"><span data-stu-id="974a8-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="974a8-272">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="974a8-272">Deploy tooAzure</span></span>
<span data-ttu-id="974a8-273">una distribuzione tootrigger, hello push modifica tooAzure:</span><span class="sxs-lookup"><span data-stu-id="974a8-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="974a8-274">Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.</span><span class="sxs-lookup"><span data-stu-id="974a8-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="974a8-275">Sfoglia toohello URL Azure tooview le modifiche.</span><span class="sxs-lookup"><span data-stu-id="974a8-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="974a8-276">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="974a8-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="974a8-277">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="974a8-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="974a8-278">Risoluzione dei problemi - File statici</span><span class="sxs-lookup"><span data-stu-id="974a8-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="974a8-279">Django esiste il concetto di hello di raccolta dei file statici.</span><span class="sxs-lookup"><span data-stu-id="974a8-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="974a8-280">Questo accetta tutti i file statici hello dal percorso originale e li copia tooa unica cartella.</span><span class="sxs-lookup"><span data-stu-id="974a8-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="974a8-281">Per questa applicazione, vengono copiati troppo`/static`.</span><span class="sxs-lookup"><span data-stu-id="974a8-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="974a8-282">Tale operazione viene eseguita perché i file statici possono provenire da Django diversi.</span><span class="sxs-lookup"><span data-stu-id="974a8-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="974a8-283">Ad esempio, i file statici hello dalle interfacce di amministrazione di hello Django si trovano in una sottocartella della libreria Django nell'ambiente virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="974a8-284">I file statici definiti da questa applicazione si trovano in `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="974a8-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="974a8-285">Quando si usano più framework Django, i file statici saranno ubicati in più punti.</span><span class="sxs-lookup"><span data-stu-id="974a8-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="974a8-286">Quando si esegue un'applicazione hello in modalità di debug, un'applicazione hello fornisce i file statici hello nei percorsi originali.</span><span class="sxs-lookup"><span data-stu-id="974a8-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="974a8-287">Quando si esegue un'applicazione hello in modalità di rilascio, applicazione di hello esegue **non** utilizzati file statici hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="974a8-288">È responsabilità di hello di hello tooserve hello dei file server web.</span><span class="sxs-lookup"><span data-stu-id="974a8-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="974a8-289">Per questa applicazione, IIS servirà hello file statici `/static`.</span><span class="sxs-lookup"><span data-stu-id="974a8-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="974a8-290">raccolta di Hello dei file statici viene eseguita automaticamente come file di parte dello script di distribuzione hello, cancellazione raccolti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="974a8-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="974a8-291">Ciò significa hello raccolta viene eseguita in tutte le distribuzioni, rallentando di distribuzione, ma garantisce che i file obsoleti non saranno disponibili, evitare un potenziale problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="974a8-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="974a8-292">Se si desidera tooskip raccolta dei file statici per l'applicazione Django:</span><span class="sxs-lookup"><span data-stu-id="974a8-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="974a8-293">Sarà necessaria insieme hello toodo manualmente nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="974a8-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="974a8-294">Quindi rimuovere hello `\static` cartella `.gitignore` e aggiungerlo repository Git toohello.</span><span class="sxs-lookup"><span data-stu-id="974a8-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="974a8-295">Risoluzione dei problemi - Impostazioni</span><span class="sxs-lookup"><span data-stu-id="974a8-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="974a8-296">Varie impostazioni per un'applicazione hello possono essere modificate in `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="974a8-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="974a8-297">La modalità di debug è abilitata per la comodità dello sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="974a8-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="974a8-298">Uno degli effetti collaterali nice di che è che sarà in grado di toosee immagini e altri contenuti statici durante l'esecuzione in locale, senza che sia file statici toocollect.</span><span class="sxs-lookup"><span data-stu-id="974a8-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="974a8-299">modalità di debug toodisable:</span><span class="sxs-lookup"><span data-stu-id="974a8-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="974a8-300">Quando il debug è disabilitato, hello valore per `ALLOWED_HOSTS` toobe esigenze aggiornato nome host di Azure di tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="974a8-301">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="974a8-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="974a8-302">tooenable o qualsiasi:</span><span class="sxs-lookup"><span data-stu-id="974a8-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="974a8-303">In pratica, è opportuno toodo qualcosa toodeal più complesse con il passaggio tra debug e rilascio modalità e ottenere il nome host hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="974a8-304">È possibile impostare le variabili di ambiente tramite il portale di Azure hello **configura** pagina hello **impostazioni app** sezione.</span><span class="sxs-lookup"><span data-stu-id="974a8-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="974a8-305">Questo può essere utile per impostare i valori non è possibile tooappear nelle origini hello (le stringhe di connessione, le password e così via) o che si desidera tooset in modo diverso tra Azure e nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="974a8-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="974a8-306">In `settings.py`, è possibile eseguire una query utilizzando le variabili di ambiente hello `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="974a8-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="974a8-307">Utilizzo di un database</span><span class="sxs-lookup"><span data-stu-id="974a8-307">Using a Database</span></span>
<span data-ttu-id="974a8-308">database Hello è incluso in un'applicazione hello è un database sqlite.</span><span class="sxs-lookup"><span data-stu-id="974a8-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="974a8-309">Si tratta di un toouse database predefinito semplice e utile per lo sviluppo, poiché non richiede quasi alcuna installazione.</span><span class="sxs-lookup"><span data-stu-id="974a8-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="974a8-310">database di Hello è archiviato nel file db.sqlite3 hello nella cartella di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="974a8-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="974a8-311">Azure offre servizi di database che sono di facile toouse da un'applicazione Django.</span><span class="sxs-lookup"><span data-stu-id="974a8-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="974a8-312">Esercitazioni per l'utilizzo di [Database SQL] e [MySQL] da un'applicazione Django Mostra passaggi hello servizio di database hello toocreate necessario, modificare le impostazioni di database hello in `DjangoWebProject/settings.py`, hello e le librerie necessarie tooinstall.</span><span class="sxs-lookup"><span data-stu-id="974a8-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="974a8-313">Naturalmente, se si preferiscono toomanage i server di database, è possibile eseguire utilizzando Windows o Linux macchine virtuali in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="974a8-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="974a8-314">Interfaccia di amministrazione di Django</span><span class="sxs-lookup"><span data-stu-id="974a8-314">Django Admin Interface</span></span>
<span data-ttu-id="974a8-315">Una volta avviata la creazione dei modelli, è opportuno database hello toopopulate con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="974a8-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="974a8-316">Un modo semplice toodo aggiungere e modificare in modo interattivo il contenuto è l'interfaccia di amministrazione di toouse hello Django.</span><span class="sxs-lookup"><span data-stu-id="974a8-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="974a8-317">commento di codice Hello per interfaccia di amministrazione di hello in origini dell'applicazione hello, ma è contrassegnato chiaramente in modo è possibile abilitare facilmente il (ricerca di 'admin').</span><span class="sxs-lookup"><span data-stu-id="974a8-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="974a8-318">Dopo averlo abilitato, sincronizzare database hello, eseguire un'applicazione hello e passare troppo`/admin`.</span><span class="sxs-lookup"><span data-stu-id="974a8-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="974a8-319">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="974a8-319">Next Steps</span></span>
<span data-ttu-id="974a8-320">Seguire questi toolearn collegamenti ulteriori sui Django e gli strumenti Python per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="974a8-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="974a8-321">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="974a8-321">[Django Documentation]</span></span>
* <span data-ttu-id="974a8-322">[Python Tools per la documentazione di Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="974a8-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="974a8-323">Per informazioni sull'utilizzo di Database SQL e MySQL:</span><span class="sxs-lookup"><span data-stu-id="974a8-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="974a8-324">[Django e MySQL in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="974a8-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="974a8-325">[Django e database SQL in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="974a8-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="974a8-326">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="974a8-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="974a8-327">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="974a8-327">What's changed</span></span>
* <span data-ttu-id="974a8-328">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="974a8-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django e MySQL in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django e database SQL in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-django-sql.md
[Database SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Documentazione di Django]: https://www.djangoproject.com/
