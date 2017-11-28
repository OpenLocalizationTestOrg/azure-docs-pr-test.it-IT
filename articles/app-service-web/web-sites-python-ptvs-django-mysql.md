---
title: aaaDjango e MySQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web Django che archivia i dati in un'istanza di database MySQL e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="16190-103">Django e MySQL in Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16190-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="16190-104">In questa esercitazione si utilizzerà [Python Tools per Visual Studio](https://www.visualstudio.com/vs/python) toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling.</span><span class="sxs-lookup"><span data-stu-id="16190-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="16190-105">Si apprenderà come toouse ospitato un servizio MySQL in Azure e come tooconfigure hello web app toouse MySQL come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="16190-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="16190-106">Hello informazioni contenute in questa esercitazione sono disponibili anche in hello video seguente:</span><span class="sxs-lookup"><span data-stu-id="16190-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="16190-107">[PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: app Django con MySQL)</span><span class="sxs-lookup"><span data-stu-id="16190-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="16190-108">Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di archiviazione tabelle di Azure, MySQL e SQL Database.</span><span class="sxs-lookup"><span data-stu-id="16190-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="16190-109">Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="16190-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16190-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16190-110">Prerequisites</span></span>
* <span data-ttu-id="16190-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="16190-111">Visual Studio 2015</span></span>
* <span data-ttu-id="16190-112">[Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="16190-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="16190-113">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="16190-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="16190-114">[Python Tools 2.2 per Visual Studio esempi VSIX]</span><span class="sxs-lookup"><span data-stu-id="16190-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="16190-115">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="16190-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="16190-116">Django 1.9 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="16190-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="16190-117">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="16190-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="16190-118">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="16190-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="16190-119">Creare hello progetto</span><span class="sxs-lookup"><span data-stu-id="16190-119">Create hello Project</span></span>
<span data-ttu-id="16190-120">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="16190-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="16190-121">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="16190-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="16190-122">Si creerà un database locale usando sqlite,</span><span class="sxs-lookup"><span data-stu-id="16190-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="16190-123">Quindi viene eseguita un'applicazione hello in locale.</span><span class="sxs-lookup"><span data-stu-id="16190-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="16190-124">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="16190-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="16190-125">modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**.</span><span class="sxs-lookup"><span data-stu-id="16190-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="16190-126">Selezionare **progetto Web di polling Django** e fare clic su OK toocreate hello progetto.</span><span class="sxs-lookup"><span data-stu-id="16190-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="16190-128">Sarà richiesto tooinstall i pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="16190-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="16190-129">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="16190-129">Select **Install into a virtual environment**.</span></span>
   
    ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="16190-131">Selezionare **Python 2.7** o **Python 3.4** come interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="16190-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="16190-133">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="16190-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="16190-134">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="16190-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="16190-135">Questo verrà aprire una Console di gestione Django e creare un database sqlite nella cartella di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="16190-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="16190-136">Seguire hello richieste toocreate un utente.</span><span class="sxs-lookup"><span data-stu-id="16190-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="16190-137">Verificare che l'applicazione hello funzioni premendo `F5`.</span><span class="sxs-lookup"><span data-stu-id="16190-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="16190-138">Fare clic su **Accedi** hello barra di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="16190-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Barra di spostamento di Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="16190-140">Immettere le credenziali di hello per utente hello creato quando è possibile sincronizzare database hello.</span><span class="sxs-lookup"><span data-stu-id="16190-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Form di accesso](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="16190-142">Fare clic su **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="16190-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="16190-144">Fare clic su un sondaggio e votare.</span><span class="sxs-lookup"><span data-stu-id="16190-144">Click on a poll and vote.</span></span>
    
     ![Votazione nei poll di esempio](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="16190-146">Creare un database MySQL</span><span class="sxs-lookup"><span data-stu-id="16190-146">Create a MySQL Database</span></span>
<span data-ttu-id="16190-147">Per il database di hello, si creerà un database di hosting MySQL di ClearDB in Azure.</span><span class="sxs-lookup"><span data-stu-id="16190-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="16190-148">In alternativa, è possibile creare una propria macchina virtuale in esecuzione in Azure, quindi installare e amministrare MySQL manualmente.</span><span class="sxs-lookup"><span data-stu-id="16190-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="16190-149">Per creare un database con un piano gratuito, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="16190-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="16190-150">Accedi toohello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="16190-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="16190-151">Nella parte superiore del riquadro di spostamento hello hello, fare clic su **NEW**, quindi fare clic su **dati e archiviazione**, quindi fare clic su **MySQL Database**.</span><span class="sxs-lookup"><span data-stu-id="16190-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="16190-152">Configurare il nuovo database di MySQL hello creando un nuovo gruppo di risorse e selezionare hello percorso appropriato per tale.</span><span class="sxs-lookup"><span data-stu-id="16190-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="16190-153">Una volta creato il database di MySQL hello, fare clic su **proprietà** nel pannello database hello.</span><span class="sxs-lookup"><span data-stu-id="16190-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="16190-154">Utilizzare il valore hello copia pulsante tooput hello di **stringa di connessione** negli Appunti hello.</span><span class="sxs-lookup"><span data-stu-id="16190-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="16190-155">Configurare hello progetto</span><span class="sxs-lookup"><span data-stu-id="16190-155">Configure hello Project</span></span>
<span data-ttu-id="16190-156">In questa sezione, è possibile configurare i database web app toouse hello MySQL che appena creato.</span><span class="sxs-lookup"><span data-stu-id="16190-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="16190-157">Verrà installato anche database di MySQL toouse obbligatorio Python pacchetti aggiuntivi con Django.</span><span class="sxs-lookup"><span data-stu-id="16190-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="16190-158">Quindi, puoi eseguire app web hello in locale.</span><span class="sxs-lookup"><span data-stu-id="16190-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="16190-159">In Visual Studio, aprire **settings.py**, da hello *ProjectName* cartella.</span><span class="sxs-lookup"><span data-stu-id="16190-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="16190-160">Incollare temporaneamente la stringa di connessione hello nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="16190-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="16190-161">stringa di connessione Hello è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="16190-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="16190-162">Database predefinito di modifica hello **motore** toouse MySQL e set hello valori per **nome**, **utente**, **PASSWORD** e  **HOST** da hello **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="16190-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="16190-163">In Esplora soluzioni in **ambienti Python**, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="16190-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="16190-164">Installare il pacchetto di hello `mysqlclient` utilizzando **pip**.</span><span class="sxs-lookup"><span data-stu-id="16190-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="16190-166">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="16190-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="16190-167">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="16190-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="16190-168">Per creare tabelle hello di database MySQL hello creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="16190-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="16190-169">Seguire hello richieste toocreate un utente, che non dispone di utente hello toomatch nel database sqlite hello creato nella prima sezione di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="16190-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="16190-170">Eseguire un'applicazione hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="16190-170">Run hello application with `F5`.</span></span> <span data-ttu-id="16190-171">Esegue il polling creati con **creare sondaggi esempio** e hello i dati inviati dal voto verranno serializzati nel database di MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="16190-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="16190-172">Pubblicare hello web app tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="16190-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="16190-173">Hello Azure .NET SDK fornisce un modo semplice di toodeploy il tooAzure app web del servizio App.</span><span class="sxs-lookup"><span data-stu-id="16190-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="16190-174">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="16190-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="16190-176">Fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="16190-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="16190-177">Fare clic su **New** toocreate una nuova app web.</span><span class="sxs-lookup"><span data-stu-id="16190-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="16190-178">Compilare hello seguente i campi e fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="16190-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="16190-179">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="16190-179">**Web App name**</span></span>
   * <span data-ttu-id="16190-180">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="16190-180">**App Service plan**</span></span>
   * <span data-ttu-id="16190-181">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="16190-181">**Resource group**</span></span>
   * <span data-ttu-id="16190-182">**Area**</span><span class="sxs-lookup"><span data-stu-id="16190-182">**Region**</span></span>
   * <span data-ttu-id="16190-183">Lasciare **server di Database** impostare troppo**alcun database**</span><span class="sxs-lookup"><span data-stu-id="16190-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="16190-184">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="16190-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="16190-185">Web browser verrà aperto automaticamente toohello pubblicato web app.</span><span class="sxs-lookup"><span data-stu-id="16190-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="16190-186">Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **MySQL** database ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="16190-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Web browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="16190-188">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="16190-188">Congratulations!</span></span> <span data-ttu-id="16190-189">È stato pubblicato correttamente il tooAzure app web basate su MySQL.</span><span class="sxs-lookup"><span data-stu-id="16190-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16190-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16190-190">Next steps</span></span>
<span data-ttu-id="16190-191">Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, Django e MySQL.</span><span class="sxs-lookup"><span data-stu-id="16190-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="16190-192">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="16190-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="16190-193">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="16190-193">[Web Projects]</span></span>
  * <span data-ttu-id="16190-194">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="16190-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="16190-195">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="16190-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="16190-196">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="16190-196">[Django Documentation]</span></span>
* <span data-ttu-id="16190-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="16190-197">[MySQL]</span></span>

<span data-ttu-id="16190-198">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="16190-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[portale Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentazione di Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
