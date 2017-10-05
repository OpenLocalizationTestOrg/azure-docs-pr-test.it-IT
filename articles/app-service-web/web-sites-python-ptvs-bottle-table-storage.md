---
title: Bottle e archiviazione tabelle di Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come usare Python Tools per Visual Studio per creare un'applicazione Bottle che archivia i dati nel servizio di archiviazione tabelle di Azure e distribuisce l'app Web in App Web del servizio app di Azure.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e1df7-103">Bottle e archiviazione tabelle di Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1df7-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="e1df7-104">In questa esercitazione si userà [Python Tools per Visual Studio] al fine di creare una semplice app Web per sondaggi con uno dei modelli di esempio PTVS.</span><span class="sxs-lookup"><span data-stu-id="e1df7-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="e1df7-105">Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="e1df7-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="e1df7-106">L'app Web per sondaggi definisce un'astrazione per il proprio repository; in questo modo, è possibile passare facilmente tra diversi tipi di repository (in memoria, archiviazione tabelle di Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e1df7-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="e1df7-107">Si apprenderà come creare un account di archiviazione di Azure, come configurare l'app Web per l'uso dell'archiviazione tabelle di Azure e come pubblicare l'app Web in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e1df7-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e1df7-108">Vedere il [Centro per sviluppatori Python] per consultare altri articoli che trattano lo sviluppo di app Web del servizio app di Azure con PTVS usando i framework Web di Bottle, Flask e Django con i servizi di MongoDB, archiviazione tabelle di Azure, MySQL e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="e1df7-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="e1df7-109">Sebbene questo articolo sia incentrato sul servizio app, i passaggi sono simili a quelli previsti per lo sviluppo dei [servizi cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="e1df7-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1df7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e1df7-110">Prerequisites</span></span>
* <span data-ttu-id="e1df7-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e1df7-111">Visual Studio 2015</span></span>
* <span data-ttu-id="e1df7-112">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e1df7-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e1df7-113">[VSIX degli esempi di Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e1df7-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e1df7-114">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="e1df7-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e1df7-115">[Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="e1df7-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e1df7-116">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="e1df7-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e1df7-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="e1df7-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="e1df7-118">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="e1df7-118">Create the Project</span></span>
<span data-ttu-id="e1df7-119">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="e1df7-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e1df7-120">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="e1df7-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e1df7-121">L'applicazione verrà quindi eseguita in locale tramite il repository in memoria predefinito.</span><span class="sxs-lookup"><span data-stu-id="e1df7-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="e1df7-122">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e1df7-123">I modelli di progetto di [VSIX degli esempi di Python Tools 2.2 per Visual Studio] sono disponibili in **Python**, **Esempi**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e1df7-124">Selezionare **Progetto Web di sondaggi Bottle** e fare clic su OK per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="e1df7-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="e1df7-126">Verrà richiesto di installare pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="e1df7-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="e1df7-127">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-127">Select **Install into a virtual environment**.</span></span>
   
     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="e1df7-129">Selezionare **Python 2.7** o **Python 3.4** come interprete di base.</span><span class="sxs-lookup"><span data-stu-id="e1df7-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e1df7-131">Verificare che l'applicazione funzioni premendo `F5`.</span><span class="sxs-lookup"><span data-stu-id="e1df7-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="e1df7-132">Per impostazione predefinita, l'applicazione usa un repository in memoria che non richiede alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="e1df7-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="e1df7-133">Tutti i dati vengono persi quando il server Web viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="e1df7-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="e1df7-134">Fare clic su **Crea sondaggio di esempio**, quindi fare clic su un sondaggio e su un voto.</span><span class="sxs-lookup"><span data-stu-id="e1df7-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e1df7-136">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e1df7-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="e1df7-137">Per effettuare operazioni di archiviazione, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1df7-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="e1df7-138">Per creare un account di archiviazione, attenersi alla procedura riportata di seguito</span><span class="sxs-lookup"><span data-stu-id="e1df7-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="e1df7-139">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e1df7-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e1df7-140">Fare clic sull'icona **Nuovo** nella parte inferiore sinistra del portale, quindi fare clic su **Dati e archiviazione** >  **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="e1df7-141">Fare clic sul pulsante **Crea** quindi assegnare un nome univoco all'account di archiviazione e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) correlato.</span><span class="sxs-lookup"><span data-stu-id="e1df7-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Quick Create](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="e1df7-143">Quando l'account di archiviazione viene creato, nel pulsante **Notifiche** lampeggia in verde il testo **OPERAZIONE RIUSCITA** e il pannello dell'account di archiviazione si apre per visualizzare che appartiene al nuovo gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="e1df7-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="e1df7-144">Fare clic sulla sezione **Chiavi di accesso** del pannello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e1df7-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="e1df7-145">Prendere nota del nome dell'account e della chiave denominata key1.</span><span class="sxs-lookup"><span data-stu-id="e1df7-145">Take note of the account name and key1.</span></span>
   
      ![Chiavi](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="e1df7-147">Queste informazioni sono necessarie per configurare il progetto nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="e1df7-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="e1df7-148">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="e1df7-148">Configure the Project</span></span>
<span data-ttu-id="e1df7-149">In questa sezione verrà configurata l'applicazione per usare l'account di archiviazione appena creato.</span><span class="sxs-lookup"><span data-stu-id="e1df7-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="e1df7-150">quindi verrà eseguita l'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="e1df7-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="e1df7-151">In Visual Studio fare clic con il pulsante destro del mouse sul nodo del progetto in Esplora soluzioni e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="e1df7-152">Fare clic sulla scheda **Debug** .</span><span class="sxs-lookup"><span data-stu-id="e1df7-152">Click on the **Debug** tab.</span></span>
   
     ![Impostazioni di debug del progetto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="e1df7-154">Impostare i valori delle variabili di ambiente richieste dall'applicazione in **Debug Server Command**, **Environment**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="e1df7-155">In questo modo verranno impostate le variabili di ambiente quando si sceglie **Avvia debug**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="e1df7-156">Se si vuole che le variabili vengano impostate quando si **avvia senza eseguire il debug**, impostare gli stessi valori anche in **Run Server Command**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="e1df7-157">In alternativa, è possibile definire variabili di ambiente usando il Pannello di controllo di Windows.</span><span class="sxs-lookup"><span data-stu-id="e1df7-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="e1df7-158">Si tratta di un'opzione migliore se si vuole evitare di archiviare le credenziali nel codice sorgente/nel file del progetto.</span><span class="sxs-lookup"><span data-stu-id="e1df7-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="e1df7-159">Si noti che è necessario riavviare Visual Studio affinché i nuovi valori di ambiente siano disponibili per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1df7-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="e1df7-160">Il codice che implementa il repository di archiviazione tabelle di Azure si trova in **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="e1df7-161">Per altre informazioni su come usare il servizio tabelle da Python, vedere la [documentazione] .</span><span class="sxs-lookup"><span data-stu-id="e1df7-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="e1df7-162">Eseguire l'applicazione con `F5`.</span><span class="sxs-lookup"><span data-stu-id="e1df7-162">Run the application with `F5`.</span></span> <span data-ttu-id="e1df7-163">I sondaggi creati con **Create Sample Polls** e i dati inviati mediante voto verranno serializzati nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1df7-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1df7-164">L'ambiente virtuale Python 2.7 può causare un'interruzione di eccezioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1df7-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="e1df7-165">Premere `F5` per continuare il caricamento del progetto web.</span><span class="sxs-lookup"><span data-stu-id="e1df7-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="e1df7-166">Passare alla pagina **About** per verificare che l'applicazione usi il repository di **archiviazione tabelle di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="e1df7-168">Esplorare l'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="e1df7-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="e1df7-169">È facile visualizzare e modificare le tabelle di archiviazione tramite Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1df7-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="e1df7-170">In questa sezione si userà Esplora server per visualizzare il contenuto delle tabelle dell'applicazione di sondaggio.</span><span class="sxs-lookup"><span data-stu-id="e1df7-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="e1df7-171">A tale scopo, è necessario che siano installati gli strumenti di Microsoft Azure, disponibili come parte di [Azure SDK per .NET].</span><span class="sxs-lookup"><span data-stu-id="e1df7-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="e1df7-172">Aprire **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="e1df7-173">Espandere **Account di archiviazione**, l'account di archiviazione di riferimento e quindi **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="e1df7-175">Fare doppio clic su **sondaggi** o **opzioni** per visualizzarne i contenuti in una finestra di documento, nonché aggiungere/rimuovere/modificare entità.</span><span class="sxs-lookup"><span data-stu-id="e1df7-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Risultati della query relativa alla tabella](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="e1df7-177">Pubblicare l'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e1df7-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="e1df7-178">L'SDK .NET di Azure offre un modo semplice di distribuire l'app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1df7-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="e1df7-179">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo di progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e1df7-181">Fare clic su **App Web di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="e1df7-182">Fare clic su **Nuovo** per creare una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="e1df7-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="e1df7-183">Compilare i campi seguenti, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="e1df7-184">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="e1df7-184">**Web App name**</span></span>
   * <span data-ttu-id="e1df7-185">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="e1df7-185">**App Service plan**</span></span>
   * <span data-ttu-id="e1df7-186">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="e1df7-186">**Resource group**</span></span>
   * <span data-ttu-id="e1df7-187">**Area**</span><span class="sxs-lookup"><span data-stu-id="e1df7-187">**Region**</span></span>
   * <span data-ttu-id="e1df7-188">Lasciare **Server database** impostato su **Nessun database**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="e1df7-189">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e1df7-190">L'app Web pubblicata verrà aperto automaticamente nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="e1df7-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="e1df7-191">Se si passa alla pagina relativa alle informazioni, si noterà che viene usato il repository **in memoria**, non il repository di **archiviazione tabelle di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e1df7-192">Ciò avviene perché le variabili di ambiente non sono impostate per l'istanza app Web in Azure App Service; pertanto vengono usati i valori predefiniti specificati in **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="e1df7-193">Configurare l'istanza di app Web</span><span class="sxs-lookup"><span data-stu-id="e1df7-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="e1df7-194">In questa sezione verranno configurate le variabili dell'istanza di App Web.</span><span class="sxs-lookup"><span data-stu-id="e1df7-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="e1df7-195">Nel [portale di Azure] aprire il pannello dell'app Web facendo clic su **Sfoglia** > **Servizi app** > nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="e1df7-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="e1df7-196">Nel pannello dell'app Web fare clic su **Tutte le impostazioni** e quindi su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="e1df7-197">Scorrere verso il basso fino alla sezione **Impostazioni app** e impostare i valori per **REPOSITORY\_NAME**, **STORAGE\_NAME** e **STORAGE\_KEY**, come descritto nella sezione precedente **Configurare il progetto**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Impostazioni app](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="e1df7-199">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1df7-199">Click on **Save**.</span></span> <span data-ttu-id="e1df7-200">Dopo aver ricevuto le notifiche relative all'applicazione delle modifiche, fare clic su **Sfoglia** dal pannello principale dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="e1df7-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="e1df7-201">L'app Web dovrebbe funzionare come previsto, usando il repository di **archiviazione tabelle di Azure** .</span><span class="sxs-lookup"><span data-stu-id="e1df7-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e1df7-202">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="e1df7-202">Congratulations!</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="e1df7-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1df7-204">Next steps</span></span>
<span data-ttu-id="e1df7-205">Usare i collegamenti seguenti per altre informazioni su Python Tools per Visual Studio, Bottle e archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1df7-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="e1df7-206">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e1df7-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e1df7-207">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="e1df7-207">[Web Projects]</span></span>
  * <span data-ttu-id="e1df7-208">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="e1df7-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e1df7-209">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e1df7-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e1df7-210">[Documentazione di Bottle]</span><span class="sxs-lookup"><span data-stu-id="e1df7-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="e1df7-211">[Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="e1df7-211">[Azure Storage]</span></span>
* <span data-ttu-id="e1df7-212">[Azure SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="e1df7-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="e1df7-213">[Come usare il servizio di archiviazione tabelle di Python]</span><span class="sxs-lookup"><span data-stu-id="e1df7-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e1df7-214">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="e1df7-214">What's changed</span></span>
* <span data-ttu-id="e1df7-215">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e1df7-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro per sviluppatori Python]: /develop/python/
[servizi cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentazione]:../cosmos-db/table-storage-how-to-use-python.md
[Come usare il servizio di archiviazione tabelle di Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[portale di Azure]: https://portal.azure.com
[Azure SDK per .NET]: http://azure.microsoft.com/downloads/
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[VSIX degli esempi di Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Documentazione di Bottle]: http://bottlepy.org/docs/dev/index.html
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Archiviazione di Azure]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK per Python]: https://github.com/Azure/azure-sdk-for-python
