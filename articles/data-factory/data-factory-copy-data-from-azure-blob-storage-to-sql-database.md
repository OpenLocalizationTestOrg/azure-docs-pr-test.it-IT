---
title: dati aaaCopy tooSQL Database - archiviazione Blob Azure | Documenti Microsoft
description: "Questa esercitazione viene illustrato come attività di copia in una Data Factory di Azure toouse pipeline toocopy dati dal database tooSQL di archiviazione Blob."
keywords: blob sql, archivio blob, copia di dati
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="96652-104">Esercitazione: Copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory</span><span class="sxs-lookup"><span data-stu-id="96652-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96652-105">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="96652-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="96652-106">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="96652-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="96652-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="96652-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="96652-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96652-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="96652-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96652-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="96652-110">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96652-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="96652-111">API REST</span><span class="sxs-lookup"><span data-stu-id="96652-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="96652-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="96652-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="96652-113">In questa esercitazione, si crea una data factory con una pipeline toocopy dati dal database tooSQL di archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="96652-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="96652-114">Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="96652-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="96652-115">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="96652-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="96652-116">Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="96652-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="96652-117">Per una panoramica dettagliata di hello servizio Data Factory, vedere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="96652-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="96652-118">Prerequisiti per l'esercitazione hello</span><span class="sxs-lookup"><span data-stu-id="96652-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="96652-119">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="96652-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="96652-120">**Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="96652-120">**Azure subscription**.</span></span>  <span data-ttu-id="96652-121">Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="96652-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="96652-122">Vedere hello [versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="96652-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="96652-123">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="96652-123">**Azure Storage Account**.</span></span> <span data-ttu-id="96652-124">Usare l'archiviazione di blob hello come un **origine** archivio dati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="96652-125">Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="96652-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="96652-126">**Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="96652-126">**Azure SQL Database**.</span></span> <span data-ttu-id="96652-127">In questa esercitazione viene usato un database SQL di Azure come archivio dati di **destinazione** .</span><span class="sxs-lookup"><span data-stu-id="96652-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="96652-128">Se non si dispone di un database SQL di Azure che è possibile utilizzare nell'esercitazione di hello, vedere [come toocreate e configurare un Database di SQL Azure](../sql-database/sql-database-get-started.md) toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="96652-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="96652-129">**SQL Server 2012/2014 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="96652-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="96652-130">Si utilizza SQL Server Management Studio o Visual Studio toocreate un database di esempio e dati del risultato hello tooview nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="96652-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="96652-131">Raccogliere il nome dell'account e la chiave dell'archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="96652-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="96652-132">È necessario hello account chiave nome e un account di archiviazione Azure toodo questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="96652-133">Prendere nota del **nome** e della **chiave** per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="96652-134">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96652-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96652-135">Fare clic su **più servizi** su hello dal menu a sinistra **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="96652-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Sfoglia - Account di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="96652-137">In hello **gli account di archiviazione** blade, seleziona hello **account di archiviazione Azure** che si desidera toouse in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="96652-138">Selezionare **Chiavi di accesso** in **IMPOSTAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="96652-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="96652-139">Fare clic su **copia** (immagine) accanto troppo**nome account di archiviazione** testo casella e Salva e incollarlo in un punto (ad esempio: in un file di testo).</span><span class="sxs-lookup"><span data-stu-id="96652-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="96652-140">Ripetere toocopy passaggio precedente hello o annotare hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="96652-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Chiave di accesso alle risorse di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="96652-142">Chiudere tutti i pannelli hello facendo **X**.</span><span class="sxs-lookup"><span data-stu-id="96652-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="96652-143">Raccogliere i nomi del server, del database e dell'utente per il database SQL</span><span class="sxs-lookup"><span data-stu-id="96652-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="96652-144">È necessario nomi hello del server SQL Azure, database e toodo utente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="96652-145">Annotare i nomi di **server**, **database** e **utente** per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="96652-146">In hello **portale di Azure**, fare clic su **più servizi** su hello a sinistra e seleziona **database SQL**.</span><span class="sxs-lookup"><span data-stu-id="96652-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="96652-147">In hello **pannello database SQL**selezionare hello **database** che si desidera toouse in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="96652-148">Annotare hello **nome del database**.</span><span class="sxs-lookup"><span data-stu-id="96652-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="96652-149">In hello **database SQL** pannello, fare clic su **proprietà** in **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="96652-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="96652-150">Annotare i valori hello per **nome SERVER** e **account di accesso amministratore SERVER**.</span><span class="sxs-lookup"><span data-stu-id="96652-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="96652-151">Chiudere tutti i pannelli hello facendo **X**.</span><span class="sxs-lookup"><span data-stu-id="96652-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="96652-152">Consentire a servizi di Azure tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="96652-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="96652-153">Verificare che **Consenti l'accesso ai servizi tooAzure** impostazione disattivata **ON** per il server SQL Azure in modo che il servizio Data Factory di hello può accedere al server di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="96652-154">tooverify e attivare questa impostazione, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="96652-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="96652-155">Fare clic su **più servizi** hub hello sinistra e fare clic su **istanze di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="96652-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="96652-156">Selezionare il server e fare clic su **Firewall** in **IMPOSTAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="96652-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="96652-157">In hello **le impostazioni del Firewall** pannello, fare clic su **ON** per **Consenti l'accesso ai servizi tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="96652-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="96652-158">Chiudere tutti i pannelli hello facendo **X**.</span><span class="sxs-lookup"><span data-stu-id="96652-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="96652-159">Preparare l'archivio BLOB e il database SQL</span><span class="sxs-lookup"><span data-stu-id="96652-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="96652-160">A questo punto, preparare l'archiviazione blob di Azure e il database SQL di Azure per l'esercitazione hello eseguendo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96652-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="96652-161">Avviare il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="96652-161">Launch Notepad.</span></span> <span data-ttu-id="96652-162">Copiare hello segue testo e salvarlo come **emp.txt** troppo**C:\ADFGetStarted** cartella sul disco rigido.</span><span class="sxs-lookup"><span data-stu-id="96652-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="96652-163">Utilizzare strumenti come [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** hello contenitore e tooupload **emp.txt** contenitore toohello file.</span><span class="sxs-lookup"><span data-stu-id="96652-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Azure Storage Explorer](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="96652-166">Hello utilizzare hello toocreate di script SQL seguente **emp** tabella nel Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="96652-167">**Se è installato nel computer SQL Server 2012/2014:** seguire le istruzioni da [la gestione di Database SQL Azure utilizzando SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server ed eseguire hello script SQL.</span><span class="sxs-lookup"><span data-stu-id="96652-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="96652-168">Questo articolo Usa hello [portale di Azure classico](http://manage.windowsazure.com), non hello [nuovo portale di Azure](https://portal.azure.com), tooconfigure firewall per un server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="96652-169">Se il client non è consentito server SQL di Azure di hello tooaccess, è necessario tooconfigure firewall per l'accesso di SQL Azure server tooallow dal computer (indirizzo IP).</span><span class="sxs-lookup"><span data-stu-id="96652-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="96652-170">Vedere [questo articolo](../sql-database/sql-database-configure-firewall-settings.md) per firewall hello tooconfigure di passaggi per il server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="96652-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="96652-171">Creare un'istanza di Data factory</span><span class="sxs-lookup"><span data-stu-id="96652-171">Create a data factory</span></span>
<span data-ttu-id="96652-172">Siano stati soddisfatti i prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="96652-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="96652-173">È possibile creare una data factory utilizzando uno dei seguenti modi hello.</span><span class="sxs-lookup"><span data-stu-id="96652-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="96652-174">Fare clic su una delle opzioni di hello nell'elenco a discesa hello nella parte superiore di hello o hello segue collegamenti tooperform hello esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96652-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="96652-175">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="96652-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="96652-176">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="96652-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="96652-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96652-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="96652-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96652-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="96652-179">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96652-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="96652-180">API REST</span><span class="sxs-lookup"><span data-stu-id="96652-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="96652-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="96652-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="96652-182">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="96652-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="96652-183">Non Trasforma dati di output tooproduce dati di input.</span><span class="sxs-lookup"><span data-stu-id="96652-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="96652-184">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare i primi dati tootransform pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="96652-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="96652-185">È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="96652-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="96652-186">Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="96652-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
