---
title: aaaFlask e l'archiviazione tabelle di Azure in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web pallone che archivia i dati nell'archiviazione tabelle di Azure e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="72c60-103">Flask e archiviazione tabelle di Azure con Python Tools 2.2 per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72c60-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="72c60-104">In questa esercitazione si userà [Python Tools per Visual Studio] toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling.</span><span class="sxs-lookup"><span data-stu-id="72c60-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="72c60-105">Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="72c60-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="72c60-106">app web viene eseguito il polling di Hello definisce un'astrazione per il relativo repository, pertanto è possibile passare facilmente tra diversi tipi di repository (In memoria, archiviazione tabelle di Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="72c60-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="72c60-107">Si apprenderà come account di toocreate una risorsa di archiviazione di Azure, come tooconfigure hello web app toouse archiviazione tabelle di Azure e come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="72c60-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="72c60-108">Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di MongoDB, archiviazione tabelle di Azure, MySQL e SQL Database.</span><span class="sxs-lookup"><span data-stu-id="72c60-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="72c60-109">Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="72c60-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72c60-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72c60-110">Prerequisites</span></span>
* <span data-ttu-id="72c60-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="72c60-111">Visual Studio 2015</span></span>
* <span data-ttu-id="72c60-112">[Python Tools 2.2 per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="72c60-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="72c60-113">[Python Tools 2.2 per Visual Studio esempi VSIX]</span><span class="sxs-lookup"><span data-stu-id="72c60-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="72c60-114">[Strumenti di Azure SDK per Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="72c60-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="72c60-115">[Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]</span><span class="sxs-lookup"><span data-stu-id="72c60-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="72c60-116">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="72c60-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="72c60-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="72c60-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="72c60-118">Creare hello progetto</span><span class="sxs-lookup"><span data-stu-id="72c60-118">Create hello Project</span></span>
<span data-ttu-id="72c60-119">In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="72c60-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="72c60-120">Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="72c60-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="72c60-121">Viene quindi eseguito localmente utilizzando i repository di hello predefinito in memoria un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="72c60-122">In Visual Studio selezionare **File**, **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="72c60-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="72c60-123">modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**.</span><span class="sxs-lookup"><span data-stu-id="72c60-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="72c60-124">Selezionare **progetto Web di polling pallone** e fare clic su OK toocreate hello progetto.</span><span class="sxs-lookup"><span data-stu-id="72c60-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="72c60-126">Sarà richiesto tooinstall i pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="72c60-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="72c60-127">Selezionare **Installa in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="72c60-127">Select **Install into a virtual environment**.</span></span>
   
     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="72c60-129">Selezionare **Python 2.7** o **Python 3.4** come interprete base hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="72c60-131">Verificare che l'applicazione hello funzioni premendo `F5`.</span><span class="sxs-lookup"><span data-stu-id="72c60-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="72c60-132">Per impostazione predefinita, un'applicazione hello utilizza un archivio in memoria che non richiede alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="72c60-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="72c60-133">Tutti i dati viene persa quando hello del server web.</span><span class="sxs-lookup"><span data-stu-id="72c60-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="72c60-134">Fare clic su **Crea sondaggio di esempio**, quindi fare clic su un sondaggio e su un voto.</span><span class="sxs-lookup"><span data-stu-id="72c60-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="72c60-136">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="72c60-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="72c60-137">le operazioni di archiviazione toouse, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="72c60-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="72c60-138">Per creare un account di archiviazione, attenersi alla procedura riportata di seguito</span><span class="sxs-lookup"><span data-stu-id="72c60-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="72c60-139">Accedere al hello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="72c60-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="72c60-140">Fare clic su hello **New** sull'icona nella parte superiore di hello a sinistra della hello portale, quindi fare clic su **dati e archiviazione** > **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="72c60-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="72c60-141">Fare clic su **crea**, quindi assegnare un nome univoco di account di archiviazione hello e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) relativo.</span><span class="sxs-lookup"><span data-stu-id="72c60-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Quick Create](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="72c60-143">Quando è stato creato l'account di archiviazione hello, hello **notifiche** pulsante farà lampeggiare una verde **esito positivo** ed è aperto il pannello dell'account di archiviazione hello gruppo tooshow appartiene toohello nuova risorsa creato.</span><span class="sxs-lookup"><span data-stu-id="72c60-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="72c60-144">Fare clic su hello **chiavi di accesso** parte nel pannello hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72c60-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="72c60-145">Prendere nota del nome dell'account hello e key1 hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-145">Take note of hello account name and hello key1.</span></span>
   
      ![Chiavi](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="72c60-147">È necessario questo tooconfigure informazioni nella sezione successiva hello del progetto.</span><span class="sxs-lookup"><span data-stu-id="72c60-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="72c60-148">Configurare hello progetto</span><span class="sxs-lookup"><span data-stu-id="72c60-148">Configure hello Project</span></span>
<span data-ttu-id="72c60-149">In questa sezione, è possibile configurare l'account di archiviazione applicazione toouse hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="72c60-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="72c60-150">Si noterà come le impostazioni di connessione tooobtain hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72c60-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="72c60-151">Quindi verrà eseguito in locale un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="72c60-152">In Visual Studio fare clic con il pulsante destro del mouse sul nodo del progetto in Esplora soluzioni e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="72c60-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="72c60-153">Fare clic su hello **Debug** scheda.</span><span class="sxs-lookup"><span data-stu-id="72c60-153">Click on hello **Debug** tab.</span></span>
   
     ![Impostazioni di debug del progetto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="72c60-155">Impostare i valori hello delle variabili di ambiente richieste da un'applicazione hello in **comando Server Debug**, **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="72c60-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="72c60-156">Questo verrà impostato le variabili di ambiente hello quando si **Avvia debug**.</span><span class="sxs-lookup"><span data-stu-id="72c60-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="72c60-157">Se si desidera hello variabili toobe imposta quando si **Avvia senza eseguire debug**, hello set stessi valori in **esecuzione del comando Server** anche.</span><span class="sxs-lookup"><span data-stu-id="72c60-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="72c60-158">In alternativa, è possibile definire variabili di ambiente utilizzando il pannello di controllo di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="72c60-159">Si tratta di un'opzione migliore se si desidera archiviare le credenziali nel codice sorgente tooavoid o file di progetto.</span><span class="sxs-lookup"><span data-stu-id="72c60-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="72c60-160">Si noti che è necessario per nuovo ambiente valori toobe toohello disponibile un'applicazione hello toorestart Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72c60-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="72c60-161">codice Hello che implementa il repository di archiviazione tabelle di Azure hello è **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="72c60-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="72c60-162">Vedere hello [documentazione] per ulteriori informazioni su come toouse del servizio tabelle da Python.</span><span class="sxs-lookup"><span data-stu-id="72c60-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="72c60-163">Eseguire un'applicazione hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="72c60-163">Run hello application with `F5`.</span></span> <span data-ttu-id="72c60-164">Esegue il polling creati con **creare sondaggi esempio** e dati hello inviati dai voti verranno serializzati nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="72c60-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="72c60-165">Ambiente virtuale di Python 2.7 Hello può causare un'interruzione di eccezioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72c60-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="72c60-166">Premere `F5` toocontinue durante il caricamento di progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="72c60-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="72c60-167">Sfoglia toohello **su** tooverify pagina che hello applicazione utilizza hello **archiviazione tabelle di Azure** repository.</span><span class="sxs-lookup"><span data-stu-id="72c60-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="72c60-169">Esplorare hello archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="72c60-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="72c60-170">È facile tooview e modificare le tabelle di archiviazione con Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72c60-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="72c60-171">In questa sezione si userà contenuto hello tooview di Esplora Server delle tabelle di applicazione hello viene eseguito il polling.</span><span class="sxs-lookup"><span data-stu-id="72c60-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="72c60-172">Questo richiede toobe strumenti di Microsoft Azure installato, che sono disponibili come parte di hello [Azure SDK per .NET].</span><span class="sxs-lookup"><span data-stu-id="72c60-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="72c60-173">Aprire **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="72c60-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="72c60-174">Espandere **Account di archiviazione**, l'account di archiviazione di riferimento e quindi **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="72c60-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="72c60-176">Fare doppio clic su hello **sondaggi** o **scelte** contenuto hello tooview della tabella hello in una finestra del documento, nonché aggiungere, rimuovere o modificare entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="72c60-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Risultati della query relativa alla tabella](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="72c60-178">Pubblicare hello web app tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="72c60-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="72c60-179">Hello Azure .NET SDK fornisce un modo semplice di toodeploy il tooAzure app web del servizio App.</span><span class="sxs-lookup"><span data-stu-id="72c60-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="72c60-180">In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="72c60-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="72c60-182">Fare clic su **App Web di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="72c60-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="72c60-183">Fare clic su **New** toocreate una nuova app web.</span><span class="sxs-lookup"><span data-stu-id="72c60-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="72c60-184">Compilare hello seguente i campi e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="72c60-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="72c60-185">**Nome dell'app Web**</span><span class="sxs-lookup"><span data-stu-id="72c60-185">**Web App name**</span></span>
   * <span data-ttu-id="72c60-186">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="72c60-186">**App Service plan**</span></span>
   * <span data-ttu-id="72c60-187">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="72c60-187">**Resource group**</span></span>
   * <span data-ttu-id="72c60-188">**Area**</span><span class="sxs-lookup"><span data-stu-id="72c60-188">**Region**</span></span>
   * <span data-ttu-id="72c60-189">Lasciare **server di Database** impostare troppo**alcun database**</span><span class="sxs-lookup"><span data-stu-id="72c60-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="72c60-190">Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="72c60-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="72c60-191">Web browser verrà aperto automaticamente toohello pubblicato web app.</span><span class="sxs-lookup"><span data-stu-id="72c60-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="72c60-192">Se si seleziona toohello sulla pagina, si noterà che usa hello **In memoria** repository, non hello **archiviazione tabelle di Azure** repository.</span><span class="sxs-lookup"><span data-stu-id="72c60-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="72c60-193">Ciò accade perché le variabili di ambiente hello non sono impostate nell'istanza di hello App Web nel servizio App di Azure, pertanto utilizza valori predefiniti di hello specificati **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="72c60-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="72c60-194">Configurare l'istanza di hello App Web</span><span class="sxs-lookup"><span data-stu-id="72c60-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="72c60-195">In questa sezione, è possibile configurare le variabili di ambiente per istanza di hello App Web.</span><span class="sxs-lookup"><span data-stu-id="72c60-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="72c60-196">In [portale Azure](https://portal.azure.com), aprire il pannello dell'app web hello facendo **Sfoglia** > **servizi App** > nome dell'app web.</span><span class="sxs-lookup"><span data-stu-id="72c60-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="72c60-197">Nel pannello dell'app Web fare clic su **Tutte le impostazioni** e quindi su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="72c60-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="72c60-198">Scorrere verso il basso toohello **impostazioni App** sezione e impostare i valori hello **REPOSITORY\_nome**, **archiviazione\_nome** e  **ARCHIVIAZIONE\_chiave** come descritto in hello **progetto hello configura** sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="72c60-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Impostazioni app](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="72c60-200">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="72c60-200">Click on **Save**.</span></span> <span data-ttu-id="72c60-201">Dopo aver ricevuto le notifiche di hello che sono state applicate le modifiche di hello, fare clic su **Sfoglia** dal pannello principale di hello Web app.</span><span class="sxs-lookup"><span data-stu-id="72c60-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="72c60-202">Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **archiviazione tabelle di Azure** repository.</span><span class="sxs-lookup"><span data-stu-id="72c60-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="72c60-203">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="72c60-203">Congratulations!</span></span>
   
     ![Web browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="72c60-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72c60-205">Next steps</span></span>
<span data-ttu-id="72c60-206">Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, pallone e archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="72c60-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="72c60-207">[Documentazione di Python Tools per Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="72c60-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="72c60-208">[Progetti Web]</span><span class="sxs-lookup"><span data-stu-id="72c60-208">[Web Projects]</span></span>
  * <span data-ttu-id="72c60-209">[Progetti servizio cloud]</span><span class="sxs-lookup"><span data-stu-id="72c60-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="72c60-210">[Debug remoto in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="72c60-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="72c60-211">[Documentazione di Flask]</span><span class="sxs-lookup"><span data-stu-id="72c60-211">[Flask Documentation]</span></span>
* <span data-ttu-id="72c60-212">[Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="72c60-212">[Azure Storage]</span></span>
* <span data-ttu-id="72c60-213">[Azure SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="72c60-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="72c60-214">[Come tooUse hello del servizio di archiviazione di tabelle da Python]</span><span class="sxs-lookup"><span data-stu-id="72c60-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="72c60-215">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="72c60-215">What's changed</span></span>
* <span data-ttu-id="72c60-216">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="72c60-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentazione]:../cosmos-db/table-storage-how-to-use-python.md
[Come tooUse hello del servizio di archiviazione di tabelle da Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK per .NET]: http://azure.microsoft.com/downloads/
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Documentazione di Flask]: http://flask.pocoo.org/
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Archiviazione di Azure]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK per Python]: https://github.com/Azure/azure-sdk-for-python
