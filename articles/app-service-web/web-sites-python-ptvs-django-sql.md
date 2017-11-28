---
title: Django e database SQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come usare Python Tools per Visual Studio per creare un'app Web Django che archivia i dati in un'istanza di database SQL e per distribuirla in App Web del servizio app di Azure.
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="b4bc4-103">Django e database SQL in Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4bc4-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="b4bc4-104">In questa esercitazione si userà [Python Tools per Visual Studio] al fine di creare una semplice app Web per sondaggi con uno dei modelli di esempio PTVS.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="b4bc4-105">Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="b4bc4-106">Si apprenderà come usare un database SQL ospitato in Azure, come configurare l'app Web per usare un database SQL e come pubblicare l'app Web in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b4bc4-107">Vedere il [Centro per sviluppatori Python] per altri articoli che trattano lo sviluppo di app Web del servizio app di Azure con PTVS usando i framework Web di Bottle, Flask e Django con i servizi di archiviazione tabelle di Azure, MySQL e database SQL.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="b4bc4-108">Sebbene questo articolo sia incentrato sul servizio app, i passaggi sono simili a quelli previsti per lo sviluppo dei [servizi cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="b4bc4-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4bc4-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4bc4-109">Prerequisites</span></span>
* <span data-ttu-id="b4bc4-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b4bc4-110">Visual Studio 2015</span></span>
* <span data-ttu-id="b4bc4-111">[Python 2.7 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="b4bc4-112">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="b4bc4-113">[VSIX degli esempi di Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="b4bc4-114">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="b4bc4-115">Django 1.9 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="b4bc4-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b4bc4-116">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b4bc4-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="b4bc4-118">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="b4bc4-118">Create the Project</span></span>
<span data-ttu-id="b4bc4-119">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="b4bc4-120">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="b4bc4-121">Si creerà un database locale usando sqlite,</span><span class="sxs-lookup"><span data-stu-id="b4bc4-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="b4bc4-122">Quindi, l'app Web verrà eseguita in locale.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="b4bc4-123">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="b4bc4-124">I modelli di progetto di [VSIX degli esempi di Python Tools 2.2 per Visual Studio] sono disponibili in **Python**, **Esempi**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="b4bc4-125">Selezionare **Polls Django Web Project** e fare clic su OK per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="b4bc4-127">Verrà richiesto di installare pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="b4bc4-128">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-128">Select **Install into a virtual environment**.</span></span>

     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="b4bc4-130">Selezionare **Python 2.7** come interprete di base.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="b4bc4-132">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto, scegliere **Python** e quindi selezionare**Django Migrate** (Migrazione Django).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b4bc4-133">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="b4bc4-134">Verrà aperta una console di gestione Django e verrà creato un database sqlite database nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="b4bc4-135">Seguire le istruzioni visualizzate per creare un utente.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="b4bc4-136">Verificare che l'applicazione funzioni premendo <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="b4bc4-137">Fare clic su **Log in** sulla barra di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="b4bc4-139">Immettere le credenziali per l'utente creato al momento della sincronizzazione del database.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="b4bc4-141">Fare clic su **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-141">Click **Create Sample Polls**.</span></span>

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="b4bc4-143">Fare clic su un sondaggio e votare.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-143">Click on a poll and vote.</span></span>

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="b4bc4-145">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="b4bc4-145">Create a SQL Database</span></span>
<span data-ttu-id="b4bc4-146">Per il database verrà creato un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="b4bc4-147">Per creare un database, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="b4bc4-148">Accedere al [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="b4bc4-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="b4bc4-149">Nella parte inferiore del pannello di navigazione fare clic su **NUOVO**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="b4bc4-150">Fare clic su **Dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="b4bc4-151">Configurare il nuovo database SQL creando un nuovo gruppo di risorse e selezionare il percorso appropriato.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="b4bc4-152">Dopo aver creato il database SQL, fare clic su **Apri in Visual Studio** nel pannello del database.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="b4bc4-153">Fare clic su **Configura firewall**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="b4bc4-154">Nel pannello **Impostazioni firewall** aggiungere una regola firewall con **IP INIZIALE** e **IP FINALE** impostati sull'indirizzo IP pubblico del computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="b4bc4-155">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-155">Click **Save**.</span></span>

   <span data-ttu-id="b4bc4-156">Questa impostazione permetterà le connessioni al server di database dal computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="b4bc4-157">Nel pannello del database fare clic su **Proprietà**, quindi su **Mostra stringhe di connessione database**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="b4bc4-158">Usare il pulsante Copia per inserire il valore di **ADO.NET** negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="b4bc4-159">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="b4bc4-159">Configure the Project</span></span>
<span data-ttu-id="b4bc4-160">In questa sezione l'app Web verrà configurata per usare il database SQL appena creato.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="b4bc4-161">e verranno installati i pacchetti Python aggiuntivi necessari per usare i database SQL con Django.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="b4bc4-162">Quindi, l'app Web verrà eseguita in locale.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="b4bc4-163">In Visual Studio aprire **settings.py**dalla cartella *NomeProgetto* .</span><span class="sxs-lookup"><span data-stu-id="b4bc4-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="b4bc4-164">Incollare temporaneamente la stringa di connessione nell'editor.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="b4bc4-165">La stringa di connessione è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="b4bc4-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="b4bc4-166">Modificare la definizione di `DATABASES` per usare i valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="b4bc4-167">In Esplora soluzioni, under **Python Environments**, fare clic con il pulsante destro del mouse sull'ambiente virtuale e selezionare **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="b4bc4-168">Installare il pacchetto `pyodbc` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="b4bc4-170">Installare il pacchetto `django-pyodbc-azure` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="b4bc4-172">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto, scegliere **Python** e quindi selezionare**Django Migrate** (Migrazione Django).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b4bc4-173">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="b4bc4-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="b4bc4-174">Verranno create le tabelle per il database SQL creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="b4bc4-175">Seguire le istruzioni per creare un utente, che non deve necessariamente corrispondere all'utente nel database sqlite creato nella prima sezione.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="b4bc4-176">Eseguire l'applicazione con `F5`.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-176">Run the application with `F5`.</span></span> <span data-ttu-id="b4bc4-177">I sondaggi creati con **Create Sample Polls** e i dati inviati mediante voto verranno serializzati nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="b4bc4-178">Pubblicare l'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b4bc4-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="b4bc4-179">L'SDK .NET di Azure offre un modo semplice di distribuire l'app Web in App Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="b4bc4-180">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo di progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="b4bc4-182">Fare clic su **App Web di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="b4bc4-183">Fare clic su **Nuovo** per creare una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="b4bc4-184">Compilare i campi seguenti, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="b4bc4-185">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="b4bc4-185">**Web App name**</span></span>
   * <span data-ttu-id="b4bc4-186">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="b4bc4-186">**App Service plan**</span></span>
   * <span data-ttu-id="b4bc4-187">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="b4bc4-187">**Resource group**</span></span>
   * <span data-ttu-id="b4bc4-188">**Area**</span><span class="sxs-lookup"><span data-stu-id="b4bc4-188">**Region**</span></span>
   * <span data-ttu-id="b4bc4-189">Lasciare **Server database** impostato su **Nessun database**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="b4bc4-190">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="b4bc4-191">L'app Web pubblicata verrà aperto automaticamente nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="b4bc4-192">L'app Web dovrebbe funzionare come previsto, usando il database **SQL** ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="b4bc4-193">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-193">Congratulations!</span></span>

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="b4bc4-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4bc4-195">Next steps</span></span>
<span data-ttu-id="b4bc4-196">Usare i collegamenti seguenti per altre informazioni su Python Tools per Visual Studio, Django e il database SQL.</span><span class="sxs-lookup"><span data-stu-id="b4bc4-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="b4bc4-197">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="b4bc4-198">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-198">[Web Projects]</span></span>
  * <span data-ttu-id="b4bc4-199">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="b4bc4-200">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="b4bc4-201">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-201">[Django Documentation]</span></span>
* <span data-ttu-id="b4bc4-202">[Database SQL]</span><span class="sxs-lookup"><span data-stu-id="b4bc4-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b4bc4-203">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="b4bc4-203">What's changed</span></span>
* <span data-ttu-id="b4bc4-204">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b4bc4-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="b4bc4-205">[Centro per sviluppatori Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="b4bc4-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="b4bc4-206">[servizi cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="b4bc4-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="b4bc4-207">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b4bc4-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="b4bc4-208">[Python Tools per Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="b4bc4-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="b4bc4-209">[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="b4bc4-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="b4bc4-210">[VSIX degli esempi di Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="b4bc4-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="b4bc4-211">[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="b4bc4-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="b4bc4-212">[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="b4bc4-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="b4bc4-213">[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="b4bc4-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="b4bc4-214">[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="b4bc4-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="b4bc4-215">[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="b4bc4-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="b4bc4-216">[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="b4bc4-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="b4bc4-217">[Documentazione di Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="b4bc4-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="b4bc4-218">[Database SQL]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="b4bc4-218">[SQL Database]: /documentation/services/sql-database/</span></span>
