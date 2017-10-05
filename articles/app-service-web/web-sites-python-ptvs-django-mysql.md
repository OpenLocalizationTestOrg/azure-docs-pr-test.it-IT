---
title: Django e MySQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come usare Python Tools per Visual Studio per creare un'app Web Django che archivia i dati in un'istanza di database MySQL e per distribuirla in App Web del servizio app di Azure.
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
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="79a10-103">Django e MySQL in Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79a10-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="79a10-104">In questa esercitazione si userà [Python Tools per Visual Studio](https://www.visualstudio.com/vs/python) al fine di creare una semplice app Web per sondaggi con uno dei modelli di esempio PTVS.</span><span class="sxs-lookup"><span data-stu-id="79a10-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="79a10-105">Si apprenderà come usare un servizio MySQL ospitato in Azure, come configurare l'app Web per l'uso di MySQL e come pubblicare l'app Web in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="79a10-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="79a10-106">Le informazioni contenute in questa esercitazione sono disponibili anche nel video seguente:</span><span class="sxs-lookup"><span data-stu-id="79a10-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="79a10-107">[PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: app Django con MySQL)</span><span class="sxs-lookup"><span data-stu-id="79a10-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="79a10-108">Vedere il [Centro per sviluppatori Python] per altri articoli che trattano lo sviluppo di app Web del servizio app di Azure con PTVS usando i framework Web di Bottle, Flask e Django con i servizi di archiviazione tabelle di Azure, MySQL e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="79a10-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="79a10-109">Sebbene questo articolo sia incentrato sul servizio app, i passaggi sono simili a quelli previsti per lo sviluppo dei [servizi cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="79a10-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79a10-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79a10-110">Prerequisites</span></span>
* <span data-ttu-id="79a10-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="79a10-111">Visual Studio 2015</span></span>
* <span data-ttu-id="79a10-112">[Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="79a10-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="79a10-113">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="79a10-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="79a10-114">[VSIX degli esempi di Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="79a10-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="79a10-115">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="79a10-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="79a10-116">Django 1.9 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="79a10-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="79a10-117">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="79a10-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="79a10-118">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="79a10-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="79a10-119">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="79a10-119">Create the Project</span></span>
<span data-ttu-id="79a10-120">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="79a10-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="79a10-121">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="79a10-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="79a10-122">Si creerà un database locale usando sqlite,</span><span class="sxs-lookup"><span data-stu-id="79a10-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="79a10-123">quindi verrà eseguita l'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="79a10-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="79a10-124">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="79a10-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="79a10-125">I modelli di progetto di [VSIX degli esempi di Python Tools 2.2 per Visual Studio] sono disponibili in **Python**, **Esempi**.</span><span class="sxs-lookup"><span data-stu-id="79a10-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="79a10-126">Selezionare **Polls Django Web Project** e fare clic su OK per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="79a10-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="79a10-128">Verrà richiesto di installare pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="79a10-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="79a10-129">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="79a10-129">Select **Install into a virtual environment**.</span></span>
   
    ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="79a10-131">Selezionare **Python 2.7** o **Python 3.4** come interprete di base.</span><span class="sxs-lookup"><span data-stu-id="79a10-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="79a10-133">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto, scegliere **Python** e quindi selezionare**Django Migrate** (Migrazione Django).</span><span class="sxs-lookup"><span data-stu-id="79a10-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="79a10-134">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="79a10-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="79a10-135">Verrà aperta una console di gestione Django e verrà creato un database sqlite database nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="79a10-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="79a10-136">Seguire le istruzioni visualizzate per creare un utente.</span><span class="sxs-lookup"><span data-stu-id="79a10-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="79a10-137">Verificare che l'applicazione funzioni premendo `F5`.</span><span class="sxs-lookup"><span data-stu-id="79a10-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="79a10-138">Fare clic su **Log in** sulla barra di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="79a10-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Barra di spostamento di Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="79a10-140">Immettere le credenziali per l'utente creato al momento della sincronizzazione del database.</span><span class="sxs-lookup"><span data-stu-id="79a10-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Form di accesso](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="79a10-142">Fare clic su **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="79a10-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="79a10-144">Fare clic su un sondaggio e votare.</span><span class="sxs-lookup"><span data-stu-id="79a10-144">Click on a poll and vote.</span></span>
    
     ![Votazione nei poll di esempio](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="79a10-146">Creare un database MySQL</span><span class="sxs-lookup"><span data-stu-id="79a10-146">Create a MySQL Database</span></span>
<span data-ttu-id="79a10-147">Per il database verrà creato un database ospitato MySQL di ClearDB in Azure.</span><span class="sxs-lookup"><span data-stu-id="79a10-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="79a10-148">In alternativa, è possibile creare una propria macchina virtuale in esecuzione in Azure, quindi installare e amministrare MySQL manualmente.</span><span class="sxs-lookup"><span data-stu-id="79a10-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="79a10-149">Per creare un database con un piano gratuito, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="79a10-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="79a10-150">Accedere al [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="79a10-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="79a10-151">Nella parte superiore del riquadro di spostamento fare clic su **NUOVO**, quindi su **Dati e archiviazione** e infine su **Database MySQL**.</span><span class="sxs-lookup"><span data-stu-id="79a10-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="79a10-152">Configurare il nuovo database MySQL creando un nuovo gruppo di risorse e selezionare il percorso appropriato.</span><span class="sxs-lookup"><span data-stu-id="79a10-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="79a10-153">Dopo aver creato il database MySQL, fare clic su **Proprietà** nel pannello del database.</span><span class="sxs-lookup"><span data-stu-id="79a10-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="79a10-154">Usare il pulsante Copia per inserire il valore della **STRINGA DI CONNESSIONE** negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="79a10-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="79a10-155">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="79a10-155">Configure the Project</span></span>
<span data-ttu-id="79a10-156">In questa sezione verrà configurata l'app Web per usare il database MySQL appena creato.</span><span class="sxs-lookup"><span data-stu-id="79a10-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="79a10-157">Verranno anche installati i pacchetti Python aggiuntivi necessari per usare i database MySQL con Django,</span><span class="sxs-lookup"><span data-stu-id="79a10-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="79a10-158">quindi l'app Web verrà eseguita in locale.</span><span class="sxs-lookup"><span data-stu-id="79a10-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="79a10-159">In Visual Studio aprire **settings.py**dalla cartella *NomeProgetto* .</span><span class="sxs-lookup"><span data-stu-id="79a10-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="79a10-160">Incollare temporaneamente la stringa di connessione nell'editor.</span><span class="sxs-lookup"><span data-stu-id="79a10-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="79a10-161">La stringa di connessione è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="79a10-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="79a10-162">Modificare il database predefinito **ENGINE** in modo che usi MySQL e impostare i valori relativi a **NAME**, **USER**, **PASSWORD** e **HOST** da **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="79a10-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="79a10-163">In Esplora soluzioni, under **Python Environments**, fare clic con il pulsante destro del mouse sull'ambiente virtuale e selezionare **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="79a10-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="79a10-164">Installare il pacchetto `mysqlclient` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="79a10-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="79a10-166">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto, scegliere **Python** e quindi selezionare**Django Migrate** (Migrazione Django).</span><span class="sxs-lookup"><span data-stu-id="79a10-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="79a10-167">Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).</span><span class="sxs-lookup"><span data-stu-id="79a10-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="79a10-168">Verranno in tal modo create le tabelle per il database MySQL creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="79a10-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="79a10-169">Seguire le istruzioni per creare un utente, che non deve necessariamente corrispondere all'utente nel database sqlite creato nella prima sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="79a10-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="79a10-170">Eseguire l'applicazione con `F5`.</span><span class="sxs-lookup"><span data-stu-id="79a10-170">Run the application with `F5`.</span></span> <span data-ttu-id="79a10-171">I sondaggi creati con **Create Sample Polls** e i dati inviati mediante voto verranno serializzati nel database MySQL.</span><span class="sxs-lookup"><span data-stu-id="79a10-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="79a10-172">Pubblicare l'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="79a10-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="79a10-173">L'SDK .NET di Azure offre un modo semplice di distribuire l'app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="79a10-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="79a10-174">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo di progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="79a10-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="79a10-176">Fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="79a10-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="79a10-177">Fare clic su **Nuovo** per creare una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="79a10-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="79a10-178">Compilare i campi seguenti, quindi fare clic su **Crea**:</span><span class="sxs-lookup"><span data-stu-id="79a10-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="79a10-179">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="79a10-179">**Web App name**</span></span>
   * <span data-ttu-id="79a10-180">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="79a10-180">**App Service plan**</span></span>
   * <span data-ttu-id="79a10-181">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="79a10-181">**Resource group**</span></span>
   * <span data-ttu-id="79a10-182">**Area**</span><span class="sxs-lookup"><span data-stu-id="79a10-182">**Region**</span></span>
   * <span data-ttu-id="79a10-183">Lasciare **Server database** impostato su **Nessun database**.</span><span class="sxs-lookup"><span data-stu-id="79a10-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="79a10-184">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="79a10-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="79a10-185">L'app Web pubblicata verrà aperto automaticamente nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="79a10-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="79a10-186">L'app Web dovrebbe funzionare come previsto, usando il database **MySQL** ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="79a10-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Web browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="79a10-188">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="79a10-188">Congratulations!</span></span> <span data-ttu-id="79a10-189">La pubblicazione in Azure dell'app Web basata su MySQL è stata completata.</span><span class="sxs-lookup"><span data-stu-id="79a10-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79a10-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79a10-190">Next steps</span></span>
<span data-ttu-id="79a10-191">Usare i collegamenti seguenti per altre informazioni su Python Tools per Visual Studio, Django e MySQL.</span><span class="sxs-lookup"><span data-stu-id="79a10-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="79a10-192">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="79a10-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="79a10-193">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="79a10-193">[Web Projects]</span></span>
  * <span data-ttu-id="79a10-194">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="79a10-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="79a10-195">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="79a10-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="79a10-196">[Documentazione di Django]</span><span class="sxs-lookup"><span data-stu-id="79a10-196">[Django Documentation]</span></span>
* <span data-ttu-id="79a10-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="79a10-197">[MySQL]</span></span>

<span data-ttu-id="79a10-198">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="79a10-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centro per sviluppatori Python]: /develop/python/
[servizi cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portale di Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX degli esempi di Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
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
