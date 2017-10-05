---
title: "Attività di stored procedure di SQL Server"
description: "Informazioni sull'uso dell'attività di stored procedure di SQL Server da una pipeline di Data factory per richiamare una stored procedure in un database SQL di Azure o in Azure SQL Data Warehouse."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="71ad5-103">Attività di stored procedure di SQL Server</span><span class="sxs-lookup"><span data-stu-id="71ad5-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="71ad5-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="71ad5-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="71ad5-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="71ad5-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="71ad5-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="71ad5-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="71ad5-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="71ad5-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="71ad5-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="71ad5-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="71ad5-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71ad5-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="71ad5-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71ad5-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="71ad5-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="71ad5-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="71ad5-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="71ad5-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="71ad5-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="71ad5-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="71ad5-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="71ad5-114">Overview</span></span>
<span data-ttu-id="71ad5-115">Le attività di trasformazione dei dati in una [pipeline](data-factory-create-pipelines.md) di Data factory trasformano ed elaborano i dati non elaborati in stime e approfondimenti.</span><span class="sxs-lookup"><span data-stu-id="71ad5-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="71ad5-116">L'attività di stored procedure è una delle attività di trasformazione supportate da Data factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="71ad5-117">Questo articolo si basa sull'articolo relativo alle [attività di trasformazione dei dati](data-factory-data-transformation-activities.md) che presenta una panoramica generale della trasformazione dei dati e le attività di trasformazione supportate in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="71ad5-118">È possibile usare l'attività stored procedure per richiamare una stored procedure in uno dei seguenti archivi dati presenti in azienda o in una macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="71ad5-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="71ad5-119">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="71ad5-119">Azure SQL Database</span></span>
- <span data-ttu-id="71ad5-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="71ad5-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="71ad5-121">Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="71ad5-121">SQL Server Database.</span></span>  <span data-ttu-id="71ad5-122">Se si usa SQL Server, è necessario installare Gateway di gestione dati nello stesso computer che ospita il database o in un computer separato che ha accesso al database.</span><span class="sxs-lookup"><span data-stu-id="71ad5-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="71ad5-123">Gateway di gestione dati è un componente che connette in modo sicuro e gestito origini dati presenti in locale o in macchine virtuali di Azure ai servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="71ad5-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="71ad5-124">Per informazioni dettagliate, vedere [Data Management Gateway](data-factory-data-management-gateway.md) (Gateway di gestione dati).</span><span class="sxs-lookup"><span data-stu-id="71ad5-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71ad5-125">Quando si copiano dati in SQL Server o nel Database SQL di Azure, è possibile configurare **SqlSink** nell'attività di copia per richiamare una stored procedure tramite la proprietà **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="71ad5-126">Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="71ad5-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="71ad5-127">Per informazioni dettagliate sulla proprietà, vedere gli articoli connettore seguenti: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="71ad5-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="71ad5-128">Non è possibile richiamare una stored procedure durante la copia dei dati in un Azure SQL Data Warehouse tramite un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="71ad5-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="71ad5-129">Tuttavia, è possibile usare l'attività di stored procedure per richiamare una stored procedure in un SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="71ad5-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="71ad5-130">Quando si copiano dati in SQL Server, nel Database SQL di Azure o in Azure SQL Data Warehouse, è possibile configurare **SqlSink** nell'attività di copia per richiamare una stored procedure che consenta di leggere i dati dal database di origine tramite la proprietà **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="71ad5-131">Per altre informazioni, vedere gli articoli connettore seguenti: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="71ad5-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="71ad5-132">La procedura dettagliata seguente usa l'attività stored procedure in una pipeline per richiamare una stored procedure in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="71ad5-133">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="71ad5-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="71ad5-134">Tabella di esempio e stored procedure</span><span class="sxs-lookup"><span data-stu-id="71ad5-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="71ad5-135">Creare la seguente **tabella** nel database SQL di Azure usando SQL Server Management Studio o qualsiasi altro strumento conosciuto.</span><span class="sxs-lookup"><span data-stu-id="71ad5-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="71ad5-136">La colonna datetimestamp riporta la data e l'ora in cui viene generato l'ID corrispondente.</span><span class="sxs-lookup"><span data-stu-id="71ad5-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="71ad5-137">La colonna ID riporta l'identificatore univoco, mentre la colonna datetimestamp riporta la data e l'ora in cui viene generato l'ID corrispondente.</span><span class="sxs-lookup"><span data-stu-id="71ad5-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Dati di esempio](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="71ad5-139">In questo esempio, la stored procedure si trova in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="71ad5-140">L'approccio è simile indipendentemente dal fatto che la stored procedure si trovi in un database Azure SQL Data Warehouse o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="71ad5-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="71ad5-141">Per un database SQL Server, è necessario installare un [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="71ad5-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="71ad5-142">Creare la seguente **stored procedure** che inserisce dati in **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="71ad5-143">Il **nome** e la **combinazione di maiuscole e minuscole** per il parametro (DateTime in questo esempio) devono corrispondere a quelli del parametro specificato nel codice JSON per la pipeline/attività.</span><span class="sxs-lookup"><span data-stu-id="71ad5-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="71ad5-144">Nella definizione della stored procedure assicurarsi che **@** sia usato come prefisso per il parametro.</span><span class="sxs-lookup"><span data-stu-id="71ad5-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="71ad5-145">Creare un'istanza di Data factory</span><span class="sxs-lookup"><span data-stu-id="71ad5-145">Create a data factory</span></span>
1. <span data-ttu-id="71ad5-146">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="71ad5-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="71ad5-147">Fare clic su **NUOVO** nel menu a sinistra e quindi su **Intelligence e analisi** e **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="71ad5-149">Nel pannello **Nuova data factory** immettere **SProcDF** come nome.</span><span class="sxs-lookup"><span data-stu-id="71ad5-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="71ad5-150">I nomi di Data factory di Azure sono **univoci**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="71ad5-151">È necessario anteporre al nome della data factory il proprio nome, per consentire la corretta creazione della factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="71ad5-153">Selezionare la **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="71ad5-154">In **Gruppo di risorse** eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="71ad5-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="71ad5-155">Fare clic su **Crea nuovo** e immettere un nome per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="71ad5-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="71ad5-156">Fare clic su **Usa esistente** e scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="71ad5-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="71ad5-157">Selezionare la **località** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="71ad5-158">Selezionare **Aggiungi al dashboard** per visualizzare la data factory nel dashboard al successivo tentativo di accesso.</span><span class="sxs-lookup"><span data-stu-id="71ad5-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="71ad5-159">Fare clic su **Crea** nel pannello **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="71ad5-160">Nel **dashboard** del portale di Azure verrà visualizzata la data factory in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="71ad5-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="71ad5-161">Dopo la creazione della data factory, viene visualizzata la pagina corrispondente con elencato il contenuto della data factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Home page di Data factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="71ad5-163">Creare un servizio collegato SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="71ad5-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="71ad5-164">Dopo aver creato la data factory, si crea un servizio collegato SQL di Azure che collega alla data factory il database SQL di Azure, contenente la tabella sampletable e la stored procedure sp_sample.</span><span class="sxs-lookup"><span data-stu-id="71ad5-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="71ad5-165">Fare clic su **Creare e distribuire** nel pannello **Data Factory** per **SProcDF** per avviare l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="71ad5-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="71ad5-166">Fare clic su **Nuovo archivio dati** sul barra dei comandi e scegliere **Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="71ad5-167">Nell'editor verrà visualizzato lo script JSON per la creazione di un servizio collegato SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Nuovo archivio dati](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="71ad5-169">Nello script JSON apportare le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="71ad5-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="71ad5-170">Sostituire `<servername>` con il nome del server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="71ad5-171">Sostituire `<databasename>` con il database in cui sono state create la tabella e la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="71ad5-172">Sostituire `<username@servername>` con l'account utente che ha accesso al database.</span><span class="sxs-lookup"><span data-stu-id="71ad5-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="71ad5-173">Sostituire `<password>` con la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="71ad5-173">Replace `<password>` with the password for the user account.</span></span>

      ![Nuovo archivio dati](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="71ad5-175">Per distribuire il servizio collegato, fare clic su **Distribuisci** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="71ad5-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="71ad5-176">Assicurarsi che AzureSqlLinkedService sia visibile nella visualizzazione albero sulla sinistra.</span><span class="sxs-lookup"><span data-stu-id="71ad5-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="71ad5-178">Creare un set di dati di output</span><span class="sxs-lookup"><span data-stu-id="71ad5-178">Create an output dataset</span></span>
<span data-ttu-id="71ad5-179">È necessario specificare un set di dati di output per un'attività stored procedure, anche se questa non produce alcun dato.</span><span class="sxs-lookup"><span data-stu-id="71ad5-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="71ad5-180">È il set di dati di output, infatti, che determina la pianificazione dell'attività (la frequenza con cui l'attività viene eseguita: ogni ora, ogni settimana e così via).</span><span class="sxs-lookup"><span data-stu-id="71ad5-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="71ad5-181">Il set di dati di output deve usare un **servizio collegato** che faccia riferimento a un database SQL di Azure, a un Azure SQL Data Warehouse o a un database SQL Server in cui si vuole che venga eseguita la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="71ad5-182">Il set di dati di output può essere usato per passare il risultato della stored procedure per la successiva elaborazione da parte di un'altra attività, [concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline), nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="71ad5-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="71ad5-183">Data Factory non scrive tuttavia automaticamente l'output di una stored procedure in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="71ad5-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="71ad5-184">È la stored procedure a scrivere dati in una tabella SQL cui punta il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="71ad5-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="71ad5-185">In alcuni casi, il set di dati di output può essere un **set di dati fittizio** (un set di dati che punta a una tabella che in realtà non contiene alcun output della stored procedure).</span><span class="sxs-lookup"><span data-stu-id="71ad5-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="71ad5-186">Il set di dati fittizio viene usato solo per specificare la pianificazione di esecuzione dell'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="71ad5-187">Fare clic su **... Altro** sulla barra degli strumenti, fare clic su **Nuovo set di dati**, fare clic su **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="71ad5-188">**Nuovo set di dati** sulla barra dei comandi e selezionare **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="71ad5-190">Copiare e incollare il seguente script JSON nell'editor JSON.</span><span class="sxs-lookup"><span data-stu-id="71ad5-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="71ad5-191">Per distribuire il set di dati, fare clic su **Distribuisci** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="71ad5-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="71ad5-192">Assicurarsi che il set di dati sia visibile nella visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="71ad5-192">Confirm that you see the dataset in the tree view.</span></span>

    ![Visualizzazione albero con servizi collegati](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="71ad5-194">Creare una pipeline con l'attività SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="71ad5-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="71ad5-195">Si crea ora una pipeline con un'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="71ad5-196">Tenere presenti le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="71ad5-196">Notice the following properties:</span></span> 

- <span data-ttu-id="71ad5-197">La proprietà **type** deve essere impostata su **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="71ad5-198">Nelle proprietà type, **storedProcedureName** deve essere impostato su **sp_sample** (nome della stored procedure).</span><span class="sxs-lookup"><span data-stu-id="71ad5-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="71ad5-199">La sezione **storedProcedureParameters** contiene un parametro denominato **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="71ad5-200">Il nome e la combinazione di maiuscole e minuscole del parametro in JSON deve corrispondere al nome e alla combinazione di maiuscole e minuscole del parametro nella definizione della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="71ad5-201">Se è necessario passare null per un parametro, usare la sintassi `"param1": null` (tutte lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="71ad5-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="71ad5-202">Fare clic su **... Altro** sulla barra dei comandi e quindi su **Nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="71ad5-203">Copiare e incollare il frammento JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="71ad5-203">Copy/paste the following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="71ad5-204">Per distribuire la pipeline, fare clic su **Distribuisci** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="71ad5-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="71ad5-205">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="71ad5-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="71ad5-206">Fare clic su **X** per chiudere i pannelli dell'editor di Data Factory, tornare al pannello Data Factory e quindi fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="71ad5-208">In **Vista diagramma**saranno visualizzati una panoramica delle pipeline e i set di dati usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="71ad5-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="71ad5-210">Nella vista Diagramma fare doppio clic sul set di dati `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="71ad5-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="71ad5-211">Verranno visualizzate le sezioni con stato pronto.</span><span class="sxs-lookup"><span data-stu-id="71ad5-211">You see the slices in Ready state.</span></span> <span data-ttu-id="71ad5-212">Dovrebbero essere presenti cinque sezioni perché dal JSON viene generata una sezione ogni ora tra l'ora di inizio e l'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="71ad5-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="71ad5-214">Quando lo stato di una sezione è **Pronto**, eseguire una query `select * from sampletable` sul database SQL di Azure per verificare che la stored procedure abbia inserito i dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="71ad5-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Dati di output](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="71ad5-216">Vedere [Monitorare la pipeline](data-factory-monitor-manage-pipelines.md) per informazioni dettagliate sul monitoraggio delle pipeline di Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="71ad5-217">Specificare un set di dati di input</span><span class="sxs-lookup"><span data-stu-id="71ad5-217">Specify an input dataset</span></span>
<span data-ttu-id="71ad5-218">Nella procedura dettagliata, l'attività stored procedure non contiene alcun set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="71ad5-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="71ad5-219">Se si specifica un set di dati di input, l'attività stored procedure non viene eseguita fino a quando la porzione del set di dati input non è disponibile (in stato Ready).</span><span class="sxs-lookup"><span data-stu-id="71ad5-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="71ad5-220">Il set di dati può essere esterno (non generato da un'altra attività nella stessa pipeline) o interno, ovvero generato da un'attività upstream (l'attività eseguita prima dell'attività corrente).</span><span class="sxs-lookup"><span data-stu-id="71ad5-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="71ad5-221">Per l'attività stored procedure è possibile specificare più set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="71ad5-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="71ad5-222">In questo caso, l'attività stored procedure viene eseguita solo quando sono disponibili tutte le porzioni di set di dati di input (in stato Ready).</span><span class="sxs-lookup"><span data-stu-id="71ad5-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="71ad5-223">Il set di dati di input non può essere usato nella stored procedure come parametro.</span><span class="sxs-lookup"><span data-stu-id="71ad5-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="71ad5-224">Viene usato solo per verificare la dipendenza prima di iniziare l'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="71ad5-225">Concatenamento con altre attività</span><span class="sxs-lookup"><span data-stu-id="71ad5-225">Chaining with other activities</span></span>
<span data-ttu-id="71ad5-226">Se si vuole concatenare un'attività upstream con questa attività, specificare l'output dell'attività upstream come input di questa attività.</span><span class="sxs-lookup"><span data-stu-id="71ad5-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="71ad5-227">In questo caso, l'attività stored procedure non viene eseguita fino a quando non viene completata l'attività upstream e il set di dati di output dell'attività upstream non è disponibile (in stato Ready).</span><span class="sxs-lookup"><span data-stu-id="71ad5-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="71ad5-228">È possibile specificare i set di dati di output di più attività upstream come set di dati di input dell'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="71ad5-229">In questo caso, l'attività stored procedure viene eseguita solo quando sono disponibili tutte le porzioni di set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="71ad5-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="71ad5-230">Nell'esempio seguente, l'output dell'attività di copia è OutputDataset, ossia un input dell'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="71ad5-231">L'attività stored procedure, quindi, non viene eseguita fino a quando non viene completata l'attività di copia e la porzione OutputDataset non è disponibile (in stato Ready).</span><span class="sxs-lookup"><span data-stu-id="71ad5-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="71ad5-232">Se si specificano più set di dati di input, l'attività stored procedure non viene eseguita fino a quando non sono disponibili (in stato Ready) le varie porzioni del set di dati input.</span><span class="sxs-lookup"><span data-stu-id="71ad5-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="71ad5-233">Non è possibile usare i set di dati di input direttamente come parametri dell'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="71ad5-234">Per altre informazioni sul concatenamento di attività, vedere [attività multiple in una pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="71ad5-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="71ad5-235">Analogamente, per collegare l'attività stored procedure con **attività downstream** (le attività eseguite al termine dell'attività stored procedure), specificare il set di dati di output dell'attività stored procedure come input dell'attività downstream nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="71ad5-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71ad5-236">Quando si copiano dati in SQL Server o nel Database SQL di Azure, è possibile configurare **SqlSink** nell'attività di copia per richiamare una stored procedure tramite la proprietà **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="71ad5-237">Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="71ad5-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="71ad5-238">Per informazioni dettagliate sulla proprietà, vedere gli articoli connettore seguenti: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="71ad5-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="71ad5-239">Quando si copiano dati in SQL Server, nel Database SQL di Azure o in Azure SQL Data Warehouse, è possibile configurare **SqlSink** nell'attività di copia per richiamare una stored procedure che consenta di leggere i dati dal database di origine tramite la proprietà **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="71ad5-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="71ad5-240">Per altre informazioni, vedere gli articoli connettore seguenti: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="71ad5-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="71ad5-241">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="71ad5-241">JSON format</span></span>
<span data-ttu-id="71ad5-242">Di seguito è riportato il formato JSON per la definizione di un'attività di Stored Procedure:</span><span class="sxs-lookup"><span data-stu-id="71ad5-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="71ad5-243">La tabella seguente illustra queste proprietà JSON:</span><span class="sxs-lookup"><span data-stu-id="71ad5-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="71ad5-244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="71ad5-244">Property</span></span> | <span data-ttu-id="71ad5-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71ad5-245">Description</span></span> | <span data-ttu-id="71ad5-246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="71ad5-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71ad5-247">name</span><span class="sxs-lookup"><span data-stu-id="71ad5-247">name</span></span> | <span data-ttu-id="71ad5-248">Nome dell'attività</span><span class="sxs-lookup"><span data-stu-id="71ad5-248">Name of the activity</span></span> |<span data-ttu-id="71ad5-249">Sì</span><span class="sxs-lookup"><span data-stu-id="71ad5-249">Yes</span></span> |
| <span data-ttu-id="71ad5-250">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71ad5-250">description</span></span> |<span data-ttu-id="71ad5-251">Testo descrittivo per lo scopo dell'attività</span><span class="sxs-lookup"><span data-stu-id="71ad5-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="71ad5-252">No</span><span class="sxs-lookup"><span data-stu-id="71ad5-252">No</span></span> |
| <span data-ttu-id="71ad5-253">type</span><span class="sxs-lookup"><span data-stu-id="71ad5-253">type</span></span> | <span data-ttu-id="71ad5-254">Deve essere impostato su: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="71ad5-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="71ad5-255">Sì</span><span class="sxs-lookup"><span data-stu-id="71ad5-255">Yes</span></span> |
| <span data-ttu-id="71ad5-256">inputs</span><span class="sxs-lookup"><span data-stu-id="71ad5-256">inputs</span></span> | <span data-ttu-id="71ad5-257">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="71ad5-257">Optional.</span></span> <span data-ttu-id="71ad5-258">Se si specifica un set di dati di input, questo dovrà essere disponibile (in stato 'Ready') per l'esecuzione dell'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="71ad5-259">Il set di dati di input non può essere usato nella stored procedure come parametro.</span><span class="sxs-lookup"><span data-stu-id="71ad5-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="71ad5-260">Viene usato solo per verificare la dipendenza prima di iniziare l'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="71ad5-261">No</span><span class="sxs-lookup"><span data-stu-id="71ad5-261">No</span></span> |
| <span data-ttu-id="71ad5-262">outputs</span><span class="sxs-lookup"><span data-stu-id="71ad5-262">outputs</span></span> | <span data-ttu-id="71ad5-263">È necessario specificare un set di dati di output per un'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="71ad5-264">Il set di dati di output specifica la **pianificazione** per le attività della stored procedure (ogni ora, ogni settimana, ogni mese e così via).</span><span class="sxs-lookup"><span data-stu-id="71ad5-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="71ad5-265">Il set di dati di output deve usare un **servizio collegato** che faccia riferimento a un database SQL di Azure, a un Azure SQL Data Warehouse o a un database SQL Server in cui si vuole che venga eseguita la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="71ad5-266">Il set di dati di output può essere usato per passare il risultato della stored procedure per la successiva elaborazione da parte di un'altra attività, [concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline), nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="71ad5-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="71ad5-267">Data Factory non scrive tuttavia automaticamente l'output di una stored procedure in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="71ad5-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="71ad5-268">È la stored procedure a scrivere dati in una tabella SQL cui punta il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="71ad5-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="71ad5-269">In alcuni casi, il set di dati di output può essere un **set di dati fittizio**che viene usato solo per specificare la pianificazione per l'esecuzione dell'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="71ad5-270">Sì</span><span class="sxs-lookup"><span data-stu-id="71ad5-270">Yes</span></span> |
| <span data-ttu-id="71ad5-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="71ad5-271">storedProcedureName</span></span> |<span data-ttu-id="71ad5-272">Specificare il nome della stored procedure nel database SQL di Azure, nel database SQL Server o in Azure SQL Data Warehouse rappresentato dal servizio collegato usato dalla tabella di output.</span><span class="sxs-lookup"><span data-stu-id="71ad5-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="71ad5-273">Sì</span><span class="sxs-lookup"><span data-stu-id="71ad5-273">Yes</span></span> |
| <span data-ttu-id="71ad5-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="71ad5-274">storedProcedureParameters</span></span> |<span data-ttu-id="71ad5-275">Specificare i valori dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="71ad5-276">Se è necessario passare null per un parametro, usare la sintassi "param1": null (tutte lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="71ad5-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="71ad5-277">Vedere l'esempio seguente per informazioni sull'uso di questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="71ad5-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="71ad5-278">No</span><span class="sxs-lookup"><span data-stu-id="71ad5-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="71ad5-279">Passaggio di un valore statico</span><span class="sxs-lookup"><span data-stu-id="71ad5-279">Passing a static value</span></span>
<span data-ttu-id="71ad5-280">A questo punto, si consideri l'aggiunta di un'altra colonna denominata 'Scenario' nella tabella contenente un valore statico denominato 'Document sample'.</span><span class="sxs-lookup"><span data-stu-id="71ad5-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Dati di esempio 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="71ad5-282">**Tabella:**</span><span class="sxs-lookup"><span data-stu-id="71ad5-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="71ad5-283">**Stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="71ad5-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="71ad5-284">Passare ora il parametro di **Scenario** e il valore dall'attività di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="71ad5-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="71ad5-285">La sezione **typeProperties** nell'esempio precedente è simile al seguente frammento:</span><span class="sxs-lookup"><span data-stu-id="71ad5-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="71ad5-286">**Set di dati di Data factory:**</span><span class="sxs-lookup"><span data-stu-id="71ad5-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="71ad5-287">**Pipeline di Data factory**</span><span class="sxs-lookup"><span data-stu-id="71ad5-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```