---
title: aaaDjango e Database SQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web Django che archivia i dati in un'istanza del database SQL e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="d4692-103">Django e database SQL in Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4692-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="d4692-104">In questa esercitazione si userà [Python Tools per Visual Studio] toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling.</span><span class="sxs-lookup"><span data-stu-id="d4692-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="d4692-105">Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="d4692-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="d4692-106">Si apprenderà come toouse un database SQL ospitato in Azure, come tooconfigure hello web app toouse un database SQL e come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d4692-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="d4692-107">Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di archiviazione tabelle di Azure, MySQL e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="d4692-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="d4692-108">Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="d4692-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4692-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4692-109">Prerequisites</span></span>
* <span data-ttu-id="d4692-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d4692-110">Visual Studio 2015</span></span>
* <span data-ttu-id="d4692-111">[Python 2.7 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="d4692-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="d4692-112">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d4692-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="d4692-113">[Python Tools 2.2 per Visual Studio esempi VSIX]</span><span class="sxs-lookup"><span data-stu-id="d4692-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="d4692-114">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="d4692-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="d4692-115">Django 1.9 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="d4692-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d4692-116">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="d4692-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d4692-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="d4692-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="d4692-118">Creare hello progetto</span><span class="sxs-lookup"><span data-stu-id="d4692-118">Create hello Project</span></span>
<span data-ttu-id="d4692-119">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="d4692-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="d4692-120">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="d4692-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="d4692-121">Si creerà un database locale usando sqlite,</span><span class="sxs-lookup"><span data-stu-id="d4692-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="d4692-122">Quindi viene eseguito localmente hello web app.</span><span class="sxs-lookup"><span data-stu-id="d4692-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="d4692-123">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="d4692-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="d4692-124">modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**.</span><span class="sxs-lookup"><span data-stu-id="d4692-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="d4692-125">Selezionare **progetto Web di polling Django** e fare clic su OK toocreate hello progetto.</span><span class="sxs-lookup"><span data-stu-id="d4692-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="d4692-127">Sarà richiesto tooinstall i pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="d4692-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="d4692-128">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="d4692-128">Select **Install into a virtual environment**.</span></span>

     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="d4692-130">Selezionare **Python 2.7** come interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="d4692-132">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="d4692-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="d4692-133">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="d4692-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="d4692-134">Questo verrà aprire una Console di gestione Django e creare un database sqlite nella cartella di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="d4692-135">Seguire hello richieste toocreate un utente.</span><span class="sxs-lookup"><span data-stu-id="d4692-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="d4692-136">Verificare che l'applicazione hello funzioni premendo <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="d4692-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="d4692-137">Fare clic su **Accedi** hello barra di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="d4692-139">Immettere le credenziali di hello per utente hello creato quando è possibile sincronizzare database hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="d4692-141">Fare clic su **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="d4692-141">Click **Create Sample Polls**.</span></span>

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="d4692-143">Fare clic su un sondaggio e votare.</span><span class="sxs-lookup"><span data-stu-id="d4692-143">Click on a poll and vote.</span></span>

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="d4692-145">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="d4692-145">Create a SQL Database</span></span>
<span data-ttu-id="d4692-146">Per il database di hello, si creerà un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4692-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="d4692-147">Per creare un database, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="d4692-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="d4692-148">Accedere al hello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="d4692-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="d4692-149">Nella parte inferiore di hello del riquadro di spostamento hello, fare clic su **NEW**.</span><span class="sxs-lookup"><span data-stu-id="d4692-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="d4692-150">Fare clic su **Dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="d4692-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="d4692-151">Configurare hello Nuovo Database SQL tramite la creazione di un nuovo gruppo di risorse e selezionare hello posizione appropriata per tale.</span><span class="sxs-lookup"><span data-stu-id="d4692-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="d4692-152">Una volta creato hello Database SQL, fare clic su **aperta in Visual Studio** nel pannello database hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="d4692-153">Fare clic su **Configura firewall**.</span><span class="sxs-lookup"><span data-stu-id="d4692-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="d4692-154">In hello **le impostazioni del Firewall** pannello, aggiungere una regola firewall con **IP iniziale** e **IP finale** impostare l'indirizzo IP pubblico toohello del computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d4692-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="d4692-155">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d4692-155">Click **Save**.</span></span>

   <span data-ttu-id="d4692-156">In questo modo i server di database di connessioni toohello dal computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d4692-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="d4692-157">Nel pannello database hello, fare clic su **proprietà**, quindi fare clic su **Mostra le stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="d4692-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="d4692-158">Utilizzare il valore hello copia pulsante tooput hello di **ADO.NET** negli Appunti hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="d4692-159">Configurare hello progetto</span><span class="sxs-lookup"><span data-stu-id="d4692-159">Configure hello Project</span></span>
<span data-ttu-id="d4692-160">In questa sezione, è possibile configurare il database SQL di hello di web app toouse che appena creato.</span><span class="sxs-lookup"><span data-stu-id="d4692-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="d4692-161">È inoltre verrà installato il database SQL toouse obbligatorio Python pacchetti aggiuntivi con Django.</span><span class="sxs-lookup"><span data-stu-id="d4692-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="d4692-162">Quindi viene eseguito localmente hello web app.</span><span class="sxs-lookup"><span data-stu-id="d4692-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="d4692-163">In Visual Studio, aprire **settings.py**, da hello *ProjectName* cartella.</span><span class="sxs-lookup"><span data-stu-id="d4692-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="d4692-164">Incollare temporaneamente la stringa di connessione hello nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="d4692-165">stringa di connessione Hello è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="d4692-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="d4692-166">Modifica definizione hello `DATABASES` valori hello toouse precedenti.</span><span class="sxs-lookup"><span data-stu-id="d4692-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="d4692-167">In Esplora soluzioni in **ambienti Python**, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.</span><span class="sxs-lookup"><span data-stu-id="d4692-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="d4692-168">Installare il pacchetto di hello `pyodbc` utilizzando **pip**.</span><span class="sxs-lookup"><span data-stu-id="d4692-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="d4692-170">Installare il pacchetto di hello `django-pyodbc-azure` utilizzando **pip**.</span><span class="sxs-lookup"><span data-stu-id="d4692-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="d4692-172">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="d4692-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="d4692-173">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="d4692-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="d4692-174">Per creare tabelle hello per il database SQL hello creati nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="d4692-175">Seguire hello richieste toocreate un utente, che non dispone di utente hello toomatch nel database sqlite hello creato nella prima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="d4692-176">Eseguire un'applicazione hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="d4692-176">Run hello application with `F5`.</span></span> <span data-ttu-id="d4692-177">Esegue il polling creati con **creare sondaggi esempio** e hello i dati inviati dal voto verranno serializzati nel database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="d4692-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="d4692-178">Pubblicare hello web app tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="d4692-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="d4692-179">Hello Azure .NET SDK fornisce toodeploy un modo semplice il tooAzure di app web App del servizio Web App web.</span><span class="sxs-lookup"><span data-stu-id="d4692-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="d4692-180">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d4692-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="d4692-182">Fare clic su **App Web di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4692-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="d4692-183">Fare clic su **New** toocreate una nuova app web.</span><span class="sxs-lookup"><span data-stu-id="d4692-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="d4692-184">Compilare hello seguente i campi e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="d4692-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="d4692-185">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="d4692-185">**Web App name**</span></span>
   * <span data-ttu-id="d4692-186">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="d4692-186">**App Service plan**</span></span>
   * <span data-ttu-id="d4692-187">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="d4692-187">**Resource group**</span></span>
   * <span data-ttu-id="d4692-188">**Area**</span><span class="sxs-lookup"><span data-stu-id="d4692-188">**Region**</span></span>
   * <span data-ttu-id="d4692-189">Lasciare **server di Database** impostare troppo**alcun database**</span><span class="sxs-lookup"><span data-stu-id="d4692-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="d4692-190">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d4692-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="d4692-191">Web browser verrà aperto automaticamente toohello pubblicato web app.</span><span class="sxs-lookup"><span data-stu-id="d4692-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="d4692-192">Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **SQL** database ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="d4692-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="d4692-193">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="d4692-193">Congratulations!</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="d4692-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4692-195">Next steps</span></span>
<span data-ttu-id="d4692-196">Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, Django e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="d4692-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="d4692-197">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d4692-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="d4692-198">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="d4692-198">[Web Projects]</span></span>
  * <span data-ttu-id="d4692-199">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="d4692-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="d4692-200">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="d4692-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="d4692-201">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="d4692-201">[Django Documentation]</span></span>
* <span data-ttu-id="d4692-202">[Database SQL]</span><span class="sxs-lookup"><span data-stu-id="d4692-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d4692-203">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="d4692-203">What's changed</span></span>
* <span data-ttu-id="d4692-204">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d4692-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[portale Azure]: https://portal.azure.com
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentazione di Django]: https://www.djangoproject.com/
[Database SQL]: /documentation/services/sql-database/
