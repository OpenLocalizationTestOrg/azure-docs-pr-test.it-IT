---
title: Creazione di app Web con Django
description: "Un'esercitazione introduttiva è in esecuzione un'applicazione web di Python in Azure applicazione servizio Web App."
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
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="c6a31-103">Creazione di app Web con Django</span><span class="sxs-lookup"><span data-stu-id="c6a31-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="c6a31-104">In questa esercitazione vengono illustrate le operazioni iniziali per l'esecuzione di Python nelle [app Web di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c6a31-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c6a31-105">Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!</span><span class="sxs-lookup"><span data-stu-id="c6a31-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c6a31-106">Se la crescita dell'applicazione lo richiede, è possibile passare all'hosting a pagamento e avvalersi dell'integrazione con tutti gli altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a31-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="c6a31-107">Verrà creata un'applicazione usando il framework Web di Django (vedere le versioni alternative di questa esercitazione per [Flask](web-sites-python-create-deploy-flask-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="c6a31-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="c6a31-108">Verrà creato il sito Web dalla raccolta di Azure, sarà configurata la distribuzione Git e si procederà alla clonazione locale del repository.</span><span class="sxs-lookup"><span data-stu-id="c6a31-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="c6a31-109">Quindi verrà eseguita l'applicazione localmente, si apporteranno le modifiche, e queste verranno successivamente sottoposte al commit e al push in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a31-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="c6a31-110">Nell'esercitazione viene illustrato come eseguire queste operazioni da Windows o Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="c6a31-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c6a31-111">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="c6a31-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c6a31-112">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="c6a31-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c6a31-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6a31-113">Prerequisites</span></span>
* <span data-ttu-id="c6a31-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="c6a31-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c6a31-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="c6a31-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c6a31-116">setuptools, pip, virtualenv (solo Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="c6a31-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c6a31-117">Git</span><span class="sxs-lookup"><span data-stu-id="c6a31-117">Git</span></span>
* <span data-ttu-id="c6a31-118">[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) - Nota: non è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c6a31-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c6a31-119">**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.</span><span class="sxs-lookup"><span data-stu-id="c6a31-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c6a31-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c6a31-120">Windows</span></span>
<span data-ttu-id="c6a31-121">Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="c6a31-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c6a31-122">In tal modo viene installata la versione a 32 bit di Python, setuptools, pip, virtualenv e così via (Python a 32 bit è la versione installata sui computer host di Azure).</span><span class="sxs-lookup"><span data-stu-id="c6a31-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="c6a31-123">In alternativa, è possibile ottenere Python da [python.org].</span><span class="sxs-lookup"><span data-stu-id="c6a31-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c6a31-124">Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].</span><span class="sxs-lookup"><span data-stu-id="c6a31-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c6a31-125">Se si utilizza Visual Studio, è possibile utilizzare il supporto Git integrato.</span><span class="sxs-lookup"><span data-stu-id="c6a31-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="c6a31-126">È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6a31-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c6a31-127">Si tratta di un'operazione facoltativa, ma se si dispone di [Visual Studio], inclusa la versione gratuita di Visual Studio Community 2013 o Visual Studio Express 2013 per il Web, si otterrà anche l'IDE Python.</span><span class="sxs-lookup"><span data-stu-id="c6a31-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c6a31-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c6a31-128">Mac/Linux</span></span>
<span data-ttu-id="c6a31-129">È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="c6a31-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="c6a31-130">Creazione delle app Web sul portale</span><span class="sxs-lookup"><span data-stu-id="c6a31-130">Web App Creation on Portal</span></span>
<span data-ttu-id="c6a31-131">Il primo passaggio per la creazione di un'app consiste nella creazione dell'app Web tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6a31-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c6a31-132">Accedere al portale di Azure e scegliere il **nuovo** pulsante nell'angolo inferiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="c6a31-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="c6a31-133">Nella casella di ricerca digitare "python".</span><span class="sxs-lookup"><span data-stu-id="c6a31-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="c6a31-134">Nei risultati della ricerca selezionare **Django** (pubblicata da PTVS), quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="c6a31-135">Configurare la nuova applicazione Django, come la creazione di un nuovo piano di servizio dell'applicazione e un nuovo gruppo di risorse per esso.</span><span class="sxs-lookup"><span data-stu-id="c6a31-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c6a31-136">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c6a31-137">Configurare la pubblicazione Git per l'app Web appena creata seguendo le istruzioni disponibili in [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6a31-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c6a31-138">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="c6a31-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c6a31-139">Contenuti del repository Git</span><span class="sxs-lookup"><span data-stu-id="c6a31-139">Git repository contents</span></span>
<span data-ttu-id="c6a31-140">Di seguito viene fornita una panoramica dei file contenuti nel repository Git iniziale, che saranno clonati nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="c6a31-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

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

<span data-ttu-id="c6a31-141">Fonti principali per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-141">Main sources for the application.</span></span> <span data-ttu-id="c6a31-142">È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.</span><span class="sxs-lookup"><span data-stu-id="c6a31-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="c6a31-143">Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="c6a31-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="c6a31-144">Gestione locale e supporto serve di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="c6a31-144">Local management and development server support.</span></span> <span data-ttu-id="c6a31-145">Da utilizzare per eseguire l'applicazione localmente, sincronizzare il database e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a31-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="c6a31-146">Database predefinito.</span><span class="sxs-lookup"><span data-stu-id="c6a31-146">Default database.</span></span> <span data-ttu-id="c6a31-147">Include le tabelle necessarie per l'applicazione da eseguire, ma non contiene utenti (sincronizzare il database per creare un utente).</span><span class="sxs-lookup"><span data-stu-id="c6a31-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="c6a31-148">File di progetto da utilizzare con [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6a31-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c6a31-149">Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.</span><span class="sxs-lookup"><span data-stu-id="c6a31-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c6a31-150">Pacchetti esterni necessari da parte di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-150">External packages needed by this application.</span></span> <span data-ttu-id="c6a31-151">Lo script di distribuzione eseguirà l'installazione di pip dei pacchetti elencati in questo file.</span><span class="sxs-lookup"><span data-stu-id="c6a31-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c6a31-152">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="c6a31-152">IIS configuration files.</span></span> <span data-ttu-id="c6a31-153">Lo script di distribuzione utilizzerà il file appropriato web.x.y.config e lo copierà come web.config.</span><span class="sxs-lookup"><span data-stu-id="c6a31-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c6a31-154">File facoltativi - Personalizzazione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="c6a31-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c6a31-155">File facoltativi - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="c6a31-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c6a31-156">Altri file sul server</span><span class="sxs-lookup"><span data-stu-id="c6a31-156">Additional files on server</span></span>
<span data-ttu-id="c6a31-157">Alcuni file sono presenti sul server ma non vengono aggiunti al repository Git.</span><span class="sxs-lookup"><span data-stu-id="c6a31-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="c6a31-158">Si tratta di file creati dallo script di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="c6a31-159">File di configurazione IIS.</span><span class="sxs-lookup"><span data-stu-id="c6a31-159">IIS configuration file.</span></span> <span data-ttu-id="c6a31-160">Creato da web.x.y.config per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c6a31-161">Ambiente virtuale Python.</span><span class="sxs-lookup"><span data-stu-id="c6a31-161">Python virtual environment.</span></span> <span data-ttu-id="c6a31-162">Creato durante la distribuzione se sul sito non esiste già un ambiente virtuale compatibile.</span><span class="sxs-lookup"><span data-stu-id="c6a31-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="c6a31-163">I pacchetti elencati in requirements.txt vengono installati con pip. Tuttavia, se i pacchetti sono installati, l'installazione di pip non verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="c6a31-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="c6a31-164">Nelle tre sezioni successive viene descritto come procedere con lo sviluppo dei siti Web in tre ambienti diversi:</span><span class="sxs-lookup"><span data-stu-id="c6a31-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="c6a31-165">Windows, con Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6a31-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c6a31-166">Windows, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="c6a31-166">Windows, with command line</span></span>
* <span data-ttu-id="c6a31-167">Mac/Linux, con la riga di comando</span><span class="sxs-lookup"><span data-stu-id="c6a31-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c6a31-168">Sviluppo di siti Web - Windows - Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6a31-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c6a31-169">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="c6a31-169">Clone the repository</span></span>
<span data-ttu-id="c6a31-170">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a31-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="c6a31-171">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6a31-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c6a31-172">Aprire il file della soluzione (.sln) incluso nella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="c6a31-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c6a31-173">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a31-173">Create virtual environment</span></span>
<span data-ttu-id="c6a31-174">A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c6a31-175">Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).</span><span class="sxs-lookup"><span data-stu-id="c6a31-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c6a31-176">Assicurarsi che il nome dell'ambiente sia `env`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="c6a31-177">Selezionare l'interprete di base.</span><span class="sxs-lookup"><span data-stu-id="c6a31-177">Select the base interpreter.</span></span> <span data-ttu-id="c6a31-178">Assicurarsi di utilizzare la stessa versione di Python è selezionata per l'applicazione web (in runtime.txt o **le impostazioni dell'applicazione** blade dell'applicazione web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="c6a31-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="c6a31-179">Assicurarsi che l'opzione per scaricare e installare i pacchetti sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c6a31-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c6a31-180">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-180">Click **Create**.</span></span> <span data-ttu-id="c6a31-181">In tal modo verrà creato l'ambiente virtuale e verranno installate le dipendenze elencate in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c6a31-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="c6a31-182">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="c6a31-182">Create a superuser</span></span>
<span data-ttu-id="c6a31-183">Il database incluso con l'applicazione non dispone di un superuser definito.</span><span class="sxs-lookup"><span data-stu-id="c6a31-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c6a31-184">Per utilizzare la funzionalità di accesso nell'applicazione o l'interfaccia di amministrazione Django (se si decide di abilitarla), sarà necessario creare un superuser.</span><span class="sxs-lookup"><span data-stu-id="c6a31-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c6a31-185">Eseguire questo comando dalla riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="c6a31-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c6a31-186">Seguire i prompt per impostare il nome utente, la password e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a31-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6a31-187">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c6a31-187">Run using development server</span></span>
<span data-ttu-id="c6a31-188">Premere F5 per avviare il debug. Il Web browser si aprirà automaticamente sulla pagina in esecuzione locale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="c6a31-189">È possibile impostare punti di interruzione nelle origini, utilizzare le finestre Espressioni di controllo e così via. Per altre informazioni sulle varie funzionalità, vedere la [documentazione di Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6a31-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c6a31-190">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="c6a31-190">Make changes</span></span>
<span data-ttu-id="c6a31-191">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="c6a31-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c6a31-192">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="c6a31-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="c6a31-193">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="c6a31-193">Install more packages</span></span>
<span data-ttu-id="c6a31-194">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="c6a31-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6a31-195">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="c6a31-195">You can install additional packages using pip.</span></span> <span data-ttu-id="c6a31-196">Per installare un pacchetto, fare clic con il pulsante destro del mouse e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c6a31-197">Ad esempio, per installare Azure SDK per Python, che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, immettere `azure`:</span><span class="sxs-lookup"><span data-stu-id="c6a31-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c6a31-198">Fare clic con il pulsante destro del mouse sull'ambiente virtuale e selezionare **Genera requirements.txt** per aggiornare requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c6a31-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="c6a31-199">Quindi, eseguire il commit delle modifiche a requirements.txt al repository Git.</span><span class="sxs-lookup"><span data-stu-id="c6a31-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="c6a31-200">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="c6a31-200">Deploy to Azure</span></span>
<span data-ttu-id="c6a31-201">Per attivare una distribuzione, fare clic su **Sincronizza** o su **Push**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c6a31-202">La sincronizzazione esegue sia il push che il pull.</span><span class="sxs-lookup"><span data-stu-id="c6a31-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="c6a31-203">La prima distribuzione richiederà un po' di tempo, in quanto verrà creato un ambiente virtuale, si installeranno i pacchetti e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a31-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c6a31-204">In Visual Studio non viene visualizzato l'avanzamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="c6a31-205">Se si desidera rivedere l'output, vedere la sezione in [Risoluzione dei problemi- Distribuzione](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="c6a31-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c6a31-206">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c6a31-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c6a31-207">Sviluppo di siti Web - Windows - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="c6a31-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c6a31-208">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="c6a31-208">Clone the repository</span></span>
<span data-ttu-id="c6a31-209">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure e aggiungere il repository di Azure come remoto.</span><span class="sxs-lookup"><span data-stu-id="c6a31-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c6a31-210">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6a31-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c6a31-211">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a31-211">Create virtual environment</span></span>
<span data-ttu-id="c6a31-212">Verrà creato un nuovo ambiente virtuale per lo sviluppo (non aggiungerlo al repository).</span><span class="sxs-lookup"><span data-stu-id="c6a31-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c6a31-213">Non è possibile cambiare la posizione degli ambienti virtuali in Python, pertanto, ciascuno sviluppatore che lavora all'applicazione ne creerà una locale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c6a31-214">Assicurarsi di utilizzare la stessa versione di Python è selezionata per l'applicazione web (in runtime.txt o blade le impostazioni dell'applicazione dell'applicazione web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="c6a31-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c6a31-215">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c6a31-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c6a31-216">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c6a31-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c6a31-217">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-217">Install any external packages required by your application.</span></span> <span data-ttu-id="c6a31-218">È possibile utilizzare il file requirements.txt nella radice del repository per installare i pacchetti nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="c6a31-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c6a31-219">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="c6a31-219">Create a superuser</span></span>
<span data-ttu-id="c6a31-220">Il database incluso con l'applicazione non dispone di un superuser definito.</span><span class="sxs-lookup"><span data-stu-id="c6a31-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c6a31-221">Per utilizzare la funzionalità di accesso nell'applicazione o l'interfaccia di amministrazione Django (se si decide di abilitarla), sarà necessario creare un superuser.</span><span class="sxs-lookup"><span data-stu-id="c6a31-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c6a31-222">Eseguire questo comando dalla riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="c6a31-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c6a31-223">Seguire i prompt per impostare il nome utente, la password e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a31-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6a31-224">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c6a31-224">Run using development server</span></span>
<span data-ttu-id="c6a31-225">È possibile avviare l'applicazione in un server di sviluppo con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="c6a31-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="c6a31-226">Sulla console verranno visualizzati l'URL e la porta su cui è in ascolto il server:</span><span class="sxs-lookup"><span data-stu-id="c6a31-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="c6a31-227">Quindi, aprire il Web browser su tale URL.</span><span class="sxs-lookup"><span data-stu-id="c6a31-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c6a31-228">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="c6a31-228">Make changes</span></span>
<span data-ttu-id="c6a31-229">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="c6a31-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c6a31-230">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="c6a31-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c6a31-231">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="c6a31-231">Install more packages</span></span>
<span data-ttu-id="c6a31-232">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="c6a31-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6a31-233">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="c6a31-233">You can install additional packages using pip.</span></span> <span data-ttu-id="c6a31-234">Ad esempio, per installare Azure SDK per Python,che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="c6a31-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c6a31-235">Assicurarsi di aggiornare requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c6a31-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c6a31-236">Eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="c6a31-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c6a31-237">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="c6a31-237">Deploy to Azure</span></span>
<span data-ttu-id="c6a31-238">Per attivare una distribuzione, eseguire il push delle modifiche in Azure:</span><span class="sxs-lookup"><span data-stu-id="c6a31-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c6a31-239">Verrà visualizzato l'output dello script di distribuzione, inclusa la creazione dell'ambiente virtuale, l'installazione di pacchetti, la creazione di web.config.</span><span class="sxs-lookup"><span data-stu-id="c6a31-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c6a31-240">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c6a31-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c6a31-241">Sviluppo del sito Web - Mac/Linux - Riga di comando</span><span class="sxs-lookup"><span data-stu-id="c6a31-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c6a31-242">Clonare il repository</span><span class="sxs-lookup"><span data-stu-id="c6a31-242">Clone the repository</span></span>
<span data-ttu-id="c6a31-243">Innanzitutto, clonare il repository utilizzando l'URL fornito sul portale di Azure e aggiungere il repository di Azure come remoto.</span><span class="sxs-lookup"><span data-stu-id="c6a31-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c6a31-244">Per altre informazioni, vedere [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6a31-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c6a31-245">Creare l'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a31-245">Create virtual environment</span></span>
<span data-ttu-id="c6a31-246">Verrà creato un nuovo ambiente virtuale per lo sviluppo (non aggiungerlo al repository).</span><span class="sxs-lookup"><span data-stu-id="c6a31-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c6a31-247">Non è possibile cambiare la posizione degli ambienti virtuali in Python, pertanto, ciascuno sviluppatore che lavora all'applicazione ne creerà una locale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c6a31-248">Assicurarsi di utilizzare la stessa versione di Python è selezionata per l'applicazione web (in runtime.txt o blade le impostazioni dell'applicazione dell'applicazione web nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="c6a31-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c6a31-249">Per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c6a31-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c6a31-250">Per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c6a31-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="c6a31-251">oppure</span><span class="sxs-lookup"><span data-stu-id="c6a31-251">or</span></span>

    pyvenv env

<span data-ttu-id="c6a31-252">Installare tutti i pacchetti esterni richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-252">Install any external packages required by your application.</span></span> <span data-ttu-id="c6a31-253">È possibile utilizzare il file requirements.txt nella radice del repository per installare i pacchetti nell'ambiente virtuale:</span><span class="sxs-lookup"><span data-stu-id="c6a31-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c6a31-254">Creare un superuser</span><span class="sxs-lookup"><span data-stu-id="c6a31-254">Create a superuser</span></span>
<span data-ttu-id="c6a31-255">Il database incluso con l'applicazione non dispone di un superuser definito.</span><span class="sxs-lookup"><span data-stu-id="c6a31-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c6a31-256">Per utilizzare la funzionalità di accesso nell'applicazione o l'interfaccia di amministrazione Django (se si decide di abilitarla), sarà necessario creare un superuser.</span><span class="sxs-lookup"><span data-stu-id="c6a31-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c6a31-257">Eseguire questo comando dalla riga di comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="c6a31-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="c6a31-258">Seguire i prompt per impostare il nome utente, la password e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a31-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6a31-259">Eseguire mediante il server di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c6a31-259">Run using development server</span></span>
<span data-ttu-id="c6a31-260">È possibile avviare l'applicazione in un server di sviluppo con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="c6a31-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="c6a31-261">Sulla console verranno visualizzati l'URL e la porta su cui è in ascolto il server:</span><span class="sxs-lookup"><span data-stu-id="c6a31-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="c6a31-262">Quindi, aprire il Web browser su tale URL.</span><span class="sxs-lookup"><span data-stu-id="c6a31-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c6a31-263">Apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="c6a31-263">Make changes</span></span>
<span data-ttu-id="c6a31-264">È possibile sperimentare apportando modifiche alle origini applicazioni e/o ai modelli.</span><span class="sxs-lookup"><span data-stu-id="c6a31-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c6a31-265">Dopo aver testato le modifiche, eseguirne il commit al repository Git:</span><span class="sxs-lookup"><span data-stu-id="c6a31-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c6a31-266">Installare altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="c6a31-266">Install more packages</span></span>
<span data-ttu-id="c6a31-267">È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.</span><span class="sxs-lookup"><span data-stu-id="c6a31-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6a31-268">È possibile installare altri pacchetti utilizzando pip.</span><span class="sxs-lookup"><span data-stu-id="c6a31-268">You can install additional packages using pip.</span></span> <span data-ttu-id="c6a31-269">Ad esempio, per installare Azure SDK per Python,che fornisce l'accesso all'archivio Azure, al bus di servizio e ad altri servizi Azure, digitare:</span><span class="sxs-lookup"><span data-stu-id="c6a31-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c6a31-270">Assicurarsi di aggiornare requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c6a31-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c6a31-271">Eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="c6a31-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c6a31-272">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="c6a31-272">Deploy to Azure</span></span>
<span data-ttu-id="c6a31-273">Per attivare una distribuzione, eseguire il push delle modifiche in Azure:</span><span class="sxs-lookup"><span data-stu-id="c6a31-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c6a31-274">Verrà visualizzato l'output dello script di distribuzione, inclusa la creazione dell'ambiente virtuale, l'installazione di pacchetti, la creazione di web.config.</span><span class="sxs-lookup"><span data-stu-id="c6a31-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c6a31-275">Passare all'URL di Azure per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c6a31-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c6a31-276">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="c6a31-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c6a31-277">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a31-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="c6a31-278">Risoluzione dei problemi - File statici</span><span class="sxs-lookup"><span data-stu-id="c6a31-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="c6a31-279">Django dispone del concetto della raccolta dei file statici.</span><span class="sxs-lookup"><span data-stu-id="c6a31-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="c6a31-280">Tutti i file statici vengono copiati dal percorso originale in una sola cartella.</span><span class="sxs-lookup"><span data-stu-id="c6a31-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="c6a31-281">Per questa applicazione, i file statici vengono copiati in `/static`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="c6a31-282">Tale operazione viene eseguita perché i file statici possono provenire da Django diversi.</span><span class="sxs-lookup"><span data-stu-id="c6a31-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="c6a31-283">Ad esempio, i file statici delle interfacce di amministrazione di Django si trovano in una sottocartella di una libreria Django nell'ambiente virtuale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="c6a31-284">I file statici definiti da questa applicazione si trovano in `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="c6a31-285">Quando si usano più framework Django, i file statici saranno ubicati in più punti.</span><span class="sxs-lookup"><span data-stu-id="c6a31-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="c6a31-286">Quando si esegue l'applicazione in modalità debug, l'applicazione utilizza i file statici dalla posizione originale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="c6a31-287">Quando si esegue l'applicazione in modalità di rilascio, i file statici **non** vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="c6a31-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="c6a31-288">L'utilizzo dei file è responsabilità del server Web.</span><span class="sxs-lookup"><span data-stu-id="c6a31-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="c6a31-289">Per questa applicazione, IIS utilizzerà i file statici da `/static`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="c6a31-290">La raccolta dei file statici viene eseguita automaticamente come parte dello script di distribuzione, eliminando i file raccolti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c6a31-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="c6a31-291">Ciò significa che la raccolta si verifica ogni volta che si esegue la distribuzione, rallentando leggermente la distribuzione, ma garantendo che i file obsoleti non siano disponibili, evitando un potenziale problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c6a31-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="c6a31-292">Per ignorare la raccolta dei file statici per l'applicazione Django:</span><span class="sxs-lookup"><span data-stu-id="c6a31-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="c6a31-293">Sarà quindi necessario eseguire manualmente la raccolta nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="c6a31-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="c6a31-294">Quindi rimuovere la cartella `\static` da `.gitignore` e aggiungerla al repository Git.</span><span class="sxs-lookup"><span data-stu-id="c6a31-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="c6a31-295">Risoluzione dei problemi - Impostazioni</span><span class="sxs-lookup"><span data-stu-id="c6a31-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="c6a31-296">In `DjangoWebProject/settings.py`è possibile modificare diverse impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c6a31-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="c6a31-297">La modalità di debug è abilitata per la comodità dello sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="c6a31-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="c6a31-298">Un simpatico effetto secondario di questa situazione sta nel fatto che sarà possibile vedere immagini e altro contenuto statico durante l'esecuzione locale, senza dover raccogliere i file statici.</span><span class="sxs-lookup"><span data-stu-id="c6a31-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="c6a31-299">Per disabilitare la modalità di debug:</span><span class="sxs-lookup"><span data-stu-id="c6a31-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="c6a31-300">Quando il debug è disabilitato, il valore per `ALLOWED_HOSTS` deve essere aggiornato in modo da includere il nome host di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a31-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="c6a31-301">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a31-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="c6a31-302">o per abilitare qualsiasi host:</span><span class="sxs-lookup"><span data-stu-id="c6a31-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="c6a31-303">In pratica, è possibile decidere di svolgere operazioni più complesse per gestire il cambio tra la modalità di debug e di rilascio e l'acquisizione del nome host.</span><span class="sxs-lookup"><span data-stu-id="c6a31-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="c6a31-304">È possibile impostare variabili di ambiente mediante la pagina **CONFIGURA** del portale di Azure, nella sezione di **impostazioni delle app**.</span><span class="sxs-lookup"><span data-stu-id="c6a31-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="c6a31-305">Ciò può essere utile per impostare i valori che è possibile non si desideri visualizzare nelle origini (stringhe di connessione, password e così via), o che si desidera impostare in modo diverso tra Azure e il computer locale.</span><span class="sxs-lookup"><span data-stu-id="c6a31-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="c6a31-306">In `settings.py`, è possibile eseguire una query delle variabili di ambiente tramite `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="c6a31-307">Utilizzo di un database</span><span class="sxs-lookup"><span data-stu-id="c6a31-307">Using a Database</span></span>
<span data-ttu-id="c6a31-308">Il database incluso con l'applicazione è un database sqlite.</span><span class="sxs-lookup"><span data-stu-id="c6a31-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="c6a31-309">Si tratta di un comodo e utile database predefinito da utilizzare per lo sviluppo, in quanto richiede una configurazione minima.</span><span class="sxs-lookup"><span data-stu-id="c6a31-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="c6a31-310">Il database è archiviato nel file db.sqlite3 nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="c6a31-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="c6a31-311">Azure fornisce servizi di database semplici da utilizzare da un'applicazione Django.</span><span class="sxs-lookup"><span data-stu-id="c6a31-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="c6a31-312">Nelle esercitazioni per l'uso di [Database SQL] e [MySQL] da un'applicazione Django vengono mostrati i passaggi necessari per creare il servizio di database, modificare le impostazioni del database in `DjangoWebProject/settings.py`e le librerie richieste per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="c6a31-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="c6a31-313">È ovvio che se si preferisce gestire server di database personalizzati, è possibile farlo utilizzando macchine virtuali Windows o Linux in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a31-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="c6a31-314">Interfaccia di amministrazione di Django</span><span class="sxs-lookup"><span data-stu-id="c6a31-314">Django Admin Interface</span></span>
<span data-ttu-id="c6a31-315">Una volta avviata la creazione dei modelli, è possibile decidere di popolare il database con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="c6a31-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="c6a31-316">Un modo semplice per aggiungere e modificare il contenuto in maniera interattiva, consiste nell'utilizzare l'interfaccia di amministrazione di Django.</span><span class="sxs-lookup"><span data-stu-id="c6a31-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="c6a31-317">Il codice per l'interfaccia di amministrazione è commentato nelle origini applicazioni, ma è contrassegnato in modo chiaro, così da poter essere abilitato facilmente (cercare).</span><span class="sxs-lookup"><span data-stu-id="c6a31-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="c6a31-318">Una volta abilitato, sincronizzare il database, eseguire l'applicazione e navigare fino a `/admin`.</span><span class="sxs-lookup"><span data-stu-id="c6a31-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6a31-319">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6a31-319">Next Steps</span></span>
<span data-ttu-id="c6a31-320">Per ulteriori informazioni su Django e Python Tools per Visual Studio, seguire i collegamenti forniti di seguito:</span><span class="sxs-lookup"><span data-stu-id="c6a31-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="c6a31-321">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="c6a31-321">[Django Documentation]</span></span>
* <span data-ttu-id="c6a31-322">[documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c6a31-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c6a31-323">Per informazioni sull'utilizzo di Database SQL e MySQL:</span><span class="sxs-lookup"><span data-stu-id="c6a31-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="c6a31-324">[Django e MySQL in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c6a31-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c6a31-325">[Django e database SQL in Azure con Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c6a31-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="c6a31-326">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c6a31-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c6a31-327">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="c6a31-327">What's changed</span></span>
* <span data-ttu-id="c6a31-328">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c6a31-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
[documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Documentazione di Django]: https://www.djangoproject.com/
