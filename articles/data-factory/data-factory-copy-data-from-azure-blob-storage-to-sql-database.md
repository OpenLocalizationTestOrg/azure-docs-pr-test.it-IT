---
title: Copiare dati da un'archiviazione BLOB al database SQL - Azure| Documentazione Microsoft
description: "Questa esercitazione illustra come usare l'attività di copia in una pipeline di Azure Data Factory per copiare i dati da un archivio BLOB a un database SQL."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="31c62-104">Esercitazione: Copiare dati da un archivio BLOB al database SQL usando Data Factory</span><span class="sxs-lookup"><span data-stu-id="31c62-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31c62-105">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31c62-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="31c62-106">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="31c62-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="31c62-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31c62-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="31c62-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31c62-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="31c62-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31c62-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="31c62-110">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31c62-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="31c62-111">API REST</span><span class="sxs-lookup"><span data-stu-id="31c62-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="31c62-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="31c62-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="31c62-113">In questa esercitazione si crea una data factory con una pipeline per copiare i dati dall'archivio BLOB al database SQL.</span><span class="sxs-lookup"><span data-stu-id="31c62-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="31c62-114">L'attività di copia esegue lo spostamento dei dati in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="31c62-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="31c62-115">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="31c62-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="31c62-116">Per informazioni dettagliate sull'attività di copia, vedere [Attività di spostamento dei dati](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="31c62-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="31c62-117">Per una panoramica dettagliata del servizio Data factory, vedere l'articolo [Introduzione al servizio Azure Data Factory](data-factory-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="31c62-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="31c62-118">Prerequisiti per l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="31c62-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="31c62-119">Prima di iniziare questa esercitazione, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="31c62-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="31c62-120">**Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="31c62-120">**Azure subscription**.</span></span>  <span data-ttu-id="31c62-121">Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="31c62-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="31c62-122">Per informazioni dettagliate, vedere l'articolo [Versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) .</span><span class="sxs-lookup"><span data-stu-id="31c62-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="31c62-123">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="31c62-123">**Azure Storage Account**.</span></span> <span data-ttu-id="31c62-124">In questa esercitazione l'archivio BLOB viene usato come archivio dati di **origine** .</span><span class="sxs-lookup"><span data-stu-id="31c62-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="31c62-125">Se non si ha un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) per informazioni su come crearne uno.</span><span class="sxs-lookup"><span data-stu-id="31c62-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="31c62-126">**Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="31c62-126">**Azure SQL Database**.</span></span> <span data-ttu-id="31c62-127">In questa esercitazione viene usato un database SQL di Azure come archivio dati di **destinazione** .</span><span class="sxs-lookup"><span data-stu-id="31c62-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="31c62-128">Se non è disponibile un database SQL di Azure da usare nell'esercitazione, vedere [Come creare e configurare un database SQL di Azure](../sql-database/sql-database-get-started.md) per crearne uno.</span><span class="sxs-lookup"><span data-stu-id="31c62-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="31c62-129">**SQL Server 2012/2014 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="31c62-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="31c62-130">Per creare un database di esempio e per visualizzare i dati risultanti in tale database, viene usato SQL Server Management Studio o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31c62-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="31c62-131">Raccogliere il nome dell'account e la chiave dell'archivio BLOB</span><span class="sxs-lookup"><span data-stu-id="31c62-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="31c62-132">Per eseguire questa esercitazione, sono necessari il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31c62-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="31c62-133">Prendere nota del **nome** e della **chiave** per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31c62-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="31c62-134">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="31c62-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="31c62-135">Fare clic su **Altri servizi** nel menu a sinistra e selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="31c62-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Sfoglia - Account di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="31c62-137">Nel pannello **Account di archiviazione** selezionare l'**account di archiviazione di Azure** da usare in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="31c62-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="31c62-138">Selezionare **Chiavi di accesso** in **IMPOSTAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="31c62-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="31c62-139">Fare clic sul pulsante **copia** (immagine) accanto alla casella di testo **Nome account di archiviazione** e salvarlo/incollarlo, ad esempio, in un file di testo.</span><span class="sxs-lookup"><span data-stu-id="31c62-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="31c62-140">Ripetere il passaggio precedente per copiare o annotare la chiave denominata **key1**.</span><span class="sxs-lookup"><span data-stu-id="31c62-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Chiave di accesso alle risorse di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="31c62-142">Fare clic su **X**per chiudere tutti i pannelli.</span><span class="sxs-lookup"><span data-stu-id="31c62-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="31c62-143">Raccogliere i nomi del server, del database e dell'utente per il database SQL</span><span class="sxs-lookup"><span data-stu-id="31c62-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="31c62-144">Per eseguire questa esercitazione, sono necessari i nomi del server, del database e dell'utente di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="31c62-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="31c62-145">Annotare i nomi di **server**, **database** e **utente** per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="31c62-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="31c62-146">Nel **portale di Azure** fare clic su **Altri servizi** a sinistra e selezionare **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="31c62-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="31c62-147">Nel pannello **Database SQL** selezionare il **database** da usare nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="31c62-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="31c62-148">Annotare il **nome database**.</span><span class="sxs-lookup"><span data-stu-id="31c62-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="31c62-149">Nel pannello **Database SQL**, fare clic su **Proprietà** in **IMPOSTAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="31c62-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="31c62-150">Annotare i valori per **NOME SERVER** e **ACCOUNT DI ACCESSO AMMINISTRATORE SERVER**.</span><span class="sxs-lookup"><span data-stu-id="31c62-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="31c62-151">Fare clic su **X**per chiudere tutti i pannelli.</span><span class="sxs-lookup"><span data-stu-id="31c62-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="31c62-152">Consentire ai servizi di Azure di accedere a SQL Server</span><span class="sxs-lookup"><span data-stu-id="31c62-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="31c62-153">Assicurarsi che l'impostazione **Consenti l'accesso a Servizi di Azure** sia **ATTIVA** per il server di Azure SQL, in modo che il servizio Data Factory possa accedere al server di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="31c62-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="31c62-154">Per verificare e attivare l'impostazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="31c62-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="31c62-155">Fare clic sull'hub **Altri servizi** a sinistra e selezionare **Server SQL**.</span><span class="sxs-lookup"><span data-stu-id="31c62-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="31c62-156">Selezionare il server e fare clic su **Firewall** in **IMPOSTAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="31c62-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="31c62-157">Nel pannello **Impostazioni del firewall** fare clic su **ATTIVA** per **Consenti l'accesso a Servizi Azure**.</span><span class="sxs-lookup"><span data-stu-id="31c62-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="31c62-158">Fare clic su **X**per chiudere tutti i pannelli.</span><span class="sxs-lookup"><span data-stu-id="31c62-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="31c62-159">Preparare l'archivio BLOB e il database SQL</span><span class="sxs-lookup"><span data-stu-id="31c62-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="31c62-160">Preparare ora l'archivio BLOB di Azure e il database SQL Azure per l'esercitazione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="31c62-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="31c62-161">Avviare il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="31c62-161">Launch Notepad.</span></span> <span data-ttu-id="31c62-162">Copiare il testo seguente e salvarlo come file **emp.txt** nella cartella **C:\ADFGetStarted** nel disco rigido.</span><span class="sxs-lookup"><span data-stu-id="31c62-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="31c62-163">Usare strumenti come [Azure Storage Explorer](http://storageexplorer.com/) per creare il contenitore **adftutorial** e per caricare il file **emp.txt** nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="31c62-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="31c62-166">Usare il seguente script SQL per creare la tabella **emp** nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="31c62-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="31c62-167">**Se nel computer è installato SQL Server 2012/2014**, seguire le istruzioni fornite in [Gestione del database SQL di Azure con SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) per connettersi al server SQL di Azure ed eseguire lo script SQL.</span><span class="sxs-lookup"><span data-stu-id="31c62-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="31c62-168">Per configurare il firewall per un server SQL di Azure, questo articolo usa il [portale di Azure classico](http://manage.windowsazure.com), non il [nuovo portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31c62-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="31c62-169">Se il client non è autorizzato ad accedere al server di Azure SQL, è necessario configurare il firewall per il server di Azure SQL in modo da consentire l'accesso dal computer (indirizzo IP).</span><span class="sxs-lookup"><span data-stu-id="31c62-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="31c62-170">Per informazioni sulla procedura per configurare il firewall per il server Azure SQL, vedere [questo articolo](../sql-database/sql-database-configure-firewall-settings.md) .</span><span class="sxs-lookup"><span data-stu-id="31c62-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="31c62-171">Creare un'istanza di Data factory</span><span class="sxs-lookup"><span data-stu-id="31c62-171">Create a data factory</span></span>
<span data-ttu-id="31c62-172">I passaggi relativi ai prerequisiti sono stati completati.</span><span class="sxs-lookup"><span data-stu-id="31c62-172">You have completed the prerequisites.</span></span> <span data-ttu-id="31c62-173">È possibile creare un data factory usando uno dei seguenti metodi.</span><span class="sxs-lookup"><span data-stu-id="31c62-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="31c62-174">Per eseguire l'esercitazione, fare clic su una delle opzioni nell'elenco a discesa in alto oppure sui collegamenti indicati qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="31c62-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="31c62-175">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="31c62-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="31c62-176">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31c62-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="31c62-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31c62-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="31c62-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31c62-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="31c62-179">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31c62-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="31c62-180">API REST</span><span class="sxs-lookup"><span data-stu-id="31c62-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="31c62-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="31c62-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="31c62-182">La pipeline di dati in questa esercitazione copia i dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="31c62-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="31c62-183">Non trasforma i dati di input per produrre dati di output.</span><span class="sxs-lookup"><span data-stu-id="31c62-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="31c62-184">Per un'esercitazione su come trasformare i dati usando Azure Data Factory, vedere [Esercitazione: Creare la prima pipeline per elaborare i dati usando il cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="31c62-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="31c62-185">È possibile concatenare due attività, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input di altre attività.</span><span class="sxs-lookup"><span data-stu-id="31c62-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="31c62-186">Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="31c62-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
