---
title: "aaaSQL attività Server Stored Procedure"
description: "Informazioni su come è possibile utilizzare l'attività di SQL Server Stored Procedure di hello tooinvoke una stored procedure in un Database SQL di Azure o Azure SQL Data Warehouse da una pipeline di Data Factory."
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
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="003a1-103">Attività di stored procedure di SQL Server</span><span class="sxs-lookup"><span data-stu-id="003a1-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="003a1-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="003a1-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="003a1-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="003a1-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="003a1-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="003a1-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="003a1-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="003a1-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="003a1-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="003a1-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="003a1-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="003a1-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="003a1-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="003a1-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="003a1-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="003a1-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="003a1-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="003a1-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="003a1-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="003a1-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="003a1-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="003a1-114">Overview</span></span>
<span data-ttu-id="003a1-115">Utilizzare le attività di trasformazione di dati in una Data Factory [pipeline](data-factory-create-pipelines.md) tootransform ed elaborare i dati non elaborati in stime e approfondimenti.</span><span class="sxs-lookup"><span data-stu-id="003a1-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="003a1-116">Hello attività Stored Procedure è una delle attività di trasformazione hello che supporta Data Factory.</span><span class="sxs-lookup"><span data-stu-id="003a1-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="003a1-117">In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="003a1-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="003a1-118">È possibile utilizzare una stored procedure in uno dei seguenti dati hello archivia nella propria azienda o in una macchina virtuale di Azure (VM) di hello attività Stored Procedure tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="003a1-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="003a1-119">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="003a1-119">Azure SQL Database</span></span>
- <span data-ttu-id="003a1-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="003a1-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="003a1-121">Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="003a1-121">SQL Server Database.</span></span>  <span data-ttu-id="003a1-122">Se si utilizza SQL Server, installare il Gateway di gestione di dati in hello che stesso computer che ospita hello database o in un computer separato che dispone di database di access toohello.</span><span class="sxs-lookup"><span data-stu-id="003a1-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="003a1-123">Gateway di gestione dati è un componente che connette in modo sicuro e gestito origini dati presenti in locale o in macchine virtuali di Azure ai servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="003a1-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="003a1-124">Per informazioni dettagliate, vedere [Data Management Gateway](data-factory-data-management-gateway.md) (Gateway di gestione dati).</span><span class="sxs-lookup"><span data-stu-id="003a1-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="003a1-125">Quando si copiano dati in Database SQL di Azure o SQL Server, è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure utilizzando hello **sqlWriterStoredProcedureName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="003a1-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="003a1-126">Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="003a1-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="003a1-127">Per ulteriori informazioni sulla proprietà hello, vedere i seguenti articoli connettore: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="003a1-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="003a1-128">Non è possibile richiamare una stored procedure durante la copia dei dati in un Azure SQL Data Warehouse tramite un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="003a1-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="003a1-129">Tuttavia, è possibile utilizzare hello stored procedure attività tooinvoke una stored procedure in un Data Warehouse di SQL.</span><span class="sxs-lookup"><span data-stu-id="003a1-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="003a1-130">Quando si copiano dati da Database SQL di Azure o Azure SQL Data Warehouse e SQL Server, è possibile configurare **SqlSource** in tooinvoke attività copia dei dati di tooread una stored procedure dal database di origine hello utilizzando hello  **sqlReaderStoredProcedureName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="003a1-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="003a1-131">Per ulteriori informazioni, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="003a1-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="003a1-132">seguendo questa procedura dettagliata Usa Hello hello attività Stored Procedure in un tooinvoke pipeline una stored procedure in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="003a1-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="003a1-133">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="003a1-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="003a1-134">Tabella di esempio e stored procedure</span><span class="sxs-lookup"><span data-stu-id="003a1-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="003a1-135">Creare i seguenti hello **tabella** nel Database di SQL Azure con SQL Server Management Studio o qualsiasi altro strumento si ha familiarità con.</span><span class="sxs-lookup"><span data-stu-id="003a1-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="003a1-136">colonna datetimestamp Hello è hello data e l'ora in cui viene generato il corrispondente ID di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

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
    <span data-ttu-id="003a1-137">ID è univoco hello identificato e hello datetimestamp hello data e l'ora in cui viene generato il corrispondente ID di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Dati di esempio](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="003a1-139">In questo esempio, hello archiviato consiste in un Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="003a1-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="003a1-140">Se hello stored procedure si trova in un Database di SQL Server e in Azure SQL Data Warehouse, l'approccio di hello è simile.</span><span class="sxs-lookup"><span data-stu-id="003a1-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="003a1-141">Per un database SQL Server, è necessario installare un [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="003a1-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="003a1-142">Creare i seguenti hello **stored procedure di** che inserisce dati in toohello **tabella di esempio**.</span><span class="sxs-lookup"><span data-stu-id="003a1-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="003a1-143">**Nome** e **maiuscole e minuscole** di hello parametro (DateTime in questo esempio) deve corrispondere a quello del parametro specificato nella pipeline/attività hello JSON.</span><span class="sxs-lookup"><span data-stu-id="003a1-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="003a1-144">In hello definizione della stored procedure, assicurarsi che  **@**  viene utilizzato come prefisso per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="003a1-145">Creare un'istanza di Data factory</span><span class="sxs-lookup"><span data-stu-id="003a1-145">Create a data factory</span></span>
1. <span data-ttu-id="003a1-146">Accedi troppo[portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="003a1-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="003a1-147">Fare clic su **NEW** scegliere dal menu a sinistra, hello **Intelligence + Analitica**, fare clic su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="003a1-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="003a1-149">In hello **nuova data factory** pannello immettere **SProcDF** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="003a1-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="003a1-150">I nomi di Data factory di Azure sono **univoci**.</span><span class="sxs-lookup"><span data-stu-id="003a1-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="003a1-151">È necessario nome di hello tooprefix della hello data factory con il nome, la creazione corretta tooenable hello di factory di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="003a1-153">Selezionare la **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="003a1-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="003a1-154">Per **gruppo di risorse**, effettuare una delle hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="003a1-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="003a1-155">Fare clic su **Crea nuovo** e immettere un nome per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="003a1-156">Fare clic su **Usa esistente** e scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="003a1-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="003a1-157">Seleziona hello **percorso** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="003a1-158">Selezionare **toodashboard Pin** in modo da poter visualizzare data factory di hello dashboard hello successivo tentativo di accesso.</span><span class="sxs-lookup"><span data-stu-id="003a1-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="003a1-159">Fare clic su **crea** su hello **nuova data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="003a1-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="003a1-160">Vedrai data factory di hello viene creato nel hello **dashboard** di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="003a1-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="003a1-161">Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Home page di Data factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="003a1-163">Creare un servizio collegato SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="003a1-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="003a1-164">Dopo aver creato una data factory di hello, si crea un servizio collegato SQL Azure che si collega il database SQL di Azure, che contiene una tabella di tabella di esempio hello e sp_sample stored procedure, tooyour data factory di.</span><span class="sxs-lookup"><span data-stu-id="003a1-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="003a1-165">Fare clic su **autore e distribuire** su hello **Data Factory** pannello **SProcDF** toolaunch hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="003a1-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="003a1-166">Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="003a1-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="003a1-167">Dovrebbe essere hello script JSON per la creazione di un SQL di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="003a1-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Nuovo archivio dati](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="003a1-169">In hello script JSON, apportare hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="003a1-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="003a1-170">Sostituire `<servername>` con nome hello del server di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="003a1-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="003a1-171">Sostituire `<databasename>` con database hello in cui viene creato nella tabella hello e hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="003a1-172">Sostituire `<username@servername>` con account utente di hello con database di access toohello.</span><span class="sxs-lookup"><span data-stu-id="003a1-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="003a1-173">Sostituire `<password>` con password hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Nuovo archivio dati](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="003a1-175">toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="003a1-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="003a1-176">Assicurarsi di visualizzare hello AzureSqlLinkedService nella struttura ad albero hello visualizzare a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="003a1-178">Creare un set di dati di output</span><span class="sxs-lookup"><span data-stu-id="003a1-178">Create an output dataset</span></span>
<span data-ttu-id="003a1-179">È necessario specificare che un set di dati di output per un'attività di stored procedure anche se hello stored procedure non produce i dati.</span><span class="sxs-lookup"><span data-stu-id="003a1-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="003a1-180">Ciò avviene perché l'output di hello set di dati che l'unità di pianificazione di hello dell'attività hello (frequenza hello attività viene eseguita - oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="003a1-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="003a1-181">Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="003a1-182">Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="003a1-183">Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="003a1-184">È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="003a1-185">In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio** (un set di dati che fa riferimento a tabella tooa che non contiene effettivamente l'output di hello stored procedure).</span><span class="sxs-lookup"><span data-stu-id="003a1-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="003a1-186">Questo set di dati fittizio viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="003a1-187">Fare clic su **... Ulteriori** sulla barra degli strumenti hello, fare clic su **nuovo set di dati**, fare clic su **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="003a1-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="003a1-188">**Nuovo set di dati** sul comando hello barra e selezionare **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="003a1-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="003a1-190">Copiare e incollare lo script JSON nell'editor di JSON toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

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
3. <span data-ttu-id="003a1-191">toodeploy hello set di dati, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="003a1-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="003a1-192">Confermare la visualizzazione dei set di dati di hello in visualizzazione struttura ad albero di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![Visualizzazione albero con servizi collegati](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="003a1-194">Creare una pipeline con l'attività SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="003a1-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="003a1-195">Si crea ora una pipeline con un'attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="003a1-196">Si noti hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="003a1-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="003a1-197">Hello **tipo** impostata troppo**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="003a1-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="003a1-198">Hello **storedProcedureName** nel tipo di proprietà è impostata troppo**sp_sample** (nome di hello stored procedure).</span><span class="sxs-lookup"><span data-stu-id="003a1-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="003a1-199">Hello **storedProcedureParameters** sezione contiene un parametro denominato **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="003a1-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="003a1-200">Nome e le maiuscole e minuscole del parametro hello in JSON devono corrispondere nome hello e maiuscole e minuscole del parametro hello nella definizione di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="003a1-201">Se è necessario passare null per un parametro, utilizzare la sintassi di hello: `"param1": null` (tutti in lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="003a1-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="003a1-202">Fare clic su **... Ulteriori** hello barra dei comandi e fare clic su **nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="003a1-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="003a1-203">Copiare e incollare hello frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="003a1-203">Copy/paste hello following JSON snippet:</span></span>   

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
3. <span data-ttu-id="003a1-204">pipeline di hello toodeploy, fare clic su **Distribuisci** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="003a1-205">Pipeline hello monitoraggio</span><span class="sxs-lookup"><span data-stu-id="003a1-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="003a1-206">Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate il pannello Data Factory toohello e fare clic su **diagramma**.</span><span class="sxs-lookup"><span data-stu-id="003a1-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="003a1-208">In hello **vista diagramma**, si visualizza una panoramica delle pipeline hello e set di dati utilizzati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="003a1-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="003a1-210">In vista diagramma hello, fare doppio clic sul set di dati hello `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="003a1-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="003a1-211">Vedrai sezioni hello in stato pronto.</span><span class="sxs-lookup"><span data-stu-id="003a1-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="003a1-212">Non vi saranno cinque sezioni perché viene prodotta una sezione per ogni ora tra l'ora di inizio hello e l'ora di fine da hello JSON.</span><span class="sxs-lookup"><span data-stu-id="003a1-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="003a1-214">Quando una sezione è in **pronto** stato, eseguire una `select * from sampletable` query hello Azure SQL database tooverify che hello dati è stato inserito nella tabella toohello dalla procedura archiviata hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Dati di output](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="003a1-216">Vedere [pipeline hello monitoraggio](data-factory-monitor-manage-pipelines.md) per informazioni dettagliate sul monitoraggio delle pipeline di Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="003a1-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="003a1-217">Specificare un set di dati di input</span><span class="sxs-lookup"><span data-stu-id="003a1-217">Specify an input dataset</span></span>
<span data-ttu-id="003a1-218">In questa procedura dettagliata hello, attività stored procedure non dispone di qualsiasi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="003a1-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="003a1-219">Se si specifica un set di dati di input, hello attività stored procedure non viene eseguito fino a quando non è disponibile la porzione di hello del set di dati input (nello stato Ready).</span><span class="sxs-lookup"><span data-stu-id="003a1-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="003a1-220">set di dati Hello può essere un set di dati esterno (che non sia stato generato da un'altra attività hello stessa pipeline) o un set di dati interno è prodotto da un'attività padre (attività hello che viene eseguito prima di questa attività).</span><span class="sxs-lookup"><span data-stu-id="003a1-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="003a1-221">È possibile specificare più set di dati di input per l'attività di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="003a1-222">Se in tal caso, hello attività stored procedure viene eseguita solo quando sono disponibili tutte le sezioni di set di dati input hello (nello stato Ready).</span><span class="sxs-lookup"><span data-stu-id="003a1-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="003a1-223">set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro.</span><span class="sxs-lookup"><span data-stu-id="003a1-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="003a1-224">È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="003a1-225">Concatenamento con altre attività</span><span class="sxs-lookup"><span data-stu-id="003a1-225">Chaining with other activities</span></span>
<span data-ttu-id="003a1-226">Se si desidera toochain un'attività upstream con questa attività, specificare l'output di hello di attività upstream hello come input di questa attività.</span><span class="sxs-lookup"><span data-stu-id="003a1-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="003a1-227">Quando si esegue questa operazione, hello attività stored procedure non viene eseguito fino al completamento dell'attività upstream hello e set di dati di attività upstream hello output di hello è disponibile (in stato pronto).</span><span class="sxs-lookup"><span data-stu-id="003a1-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="003a1-228">È possibile specificare i set di dati di output di più attività upstream come set di dati di input dell'attività di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="003a1-229">Quando esegue questa operazione, hello attività stored procedure viene eseguita solo quando sono disponibili tutte le sezioni di set di dati input hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="003a1-230">In hello l'esempio seguente, l'output di hello di attività di copia hello è: OutputDataset, che è un input di hello attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="003a1-231">Pertanto, hello attività stored procedure non viene eseguito fino al completamento dell'attività di copia hello e sezione OutputDataset hello è disponibile (nello stato Ready).</span><span class="sxs-lookup"><span data-stu-id="003a1-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="003a1-232">Se si specificano più set di dati di input, hello attività stored procedure non viene eseguito fino a quando non sono disponibili tutte le sezioni di set di dati input hello (nello stato Ready).</span><span class="sxs-lookup"><span data-stu-id="003a1-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="003a1-233">set di dati di input Hello non può essere utilizzato direttamente come attività di parametri toohello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="003a1-234">Per altre informazioni sul concatenamento di attività, vedere [attività multiple in una pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="003a1-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
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

<span data-ttu-id="003a1-235">Analogamente, toolink store procedure attività hello con **attività downstream** (attività hello che eseguire dopo il completamento hello attività stored procedure), specificare set di dati di attività di hello stored procedure come output di hello un input dell'attività a valle hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="003a1-236">Quando si copiano dati in Database SQL di Azure o SQL Server, è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure utilizzando hello **sqlWriterStoredProcedureName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="003a1-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="003a1-237">Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="003a1-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="003a1-238">Per ulteriori informazioni sulla proprietà hello, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="003a1-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="003a1-239">Quando si copiano dati da Database SQL di Azure o Azure SQL Data Warehouse e SQL Server, è possibile configurare **SqlSource** in tooinvoke attività copia dei dati di tooread una stored procedure dal database di origine hello utilizzando hello  **sqlReaderStoredProcedureName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="003a1-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="003a1-240">Per ulteriori informazioni, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="003a1-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="003a1-241">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="003a1-241">JSON format</span></span>
<span data-ttu-id="003a1-242">Di seguito è riportato il formato JSON hello per la definizione di un'attività di Stored Procedure:</span><span class="sxs-lookup"><span data-stu-id="003a1-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="003a1-243">Hello nella tabella seguente vengono descritte queste proprietà JSON:</span><span class="sxs-lookup"><span data-stu-id="003a1-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="003a1-244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="003a1-244">Property</span></span> | <span data-ttu-id="003a1-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="003a1-245">Description</span></span> | <span data-ttu-id="003a1-246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="003a1-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="003a1-247">name</span><span class="sxs-lookup"><span data-stu-id="003a1-247">name</span></span> | <span data-ttu-id="003a1-248">Nome dell'attività hello</span><span class="sxs-lookup"><span data-stu-id="003a1-248">Name of hello activity</span></span> |<span data-ttu-id="003a1-249">Sì</span><span class="sxs-lookup"><span data-stu-id="003a1-249">Yes</span></span> |
| <span data-ttu-id="003a1-250">description</span><span class="sxs-lookup"><span data-stu-id="003a1-250">description</span></span> |<span data-ttu-id="003a1-251">Testo che descrive le attività di hello viene utilizzato per</span><span class="sxs-lookup"><span data-stu-id="003a1-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="003a1-252">No</span><span class="sxs-lookup"><span data-stu-id="003a1-252">No</span></span> |
| <span data-ttu-id="003a1-253">type</span><span class="sxs-lookup"><span data-stu-id="003a1-253">type</span></span> | <span data-ttu-id="003a1-254">Deve essere impostato su: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="003a1-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="003a1-255">Sì</span><span class="sxs-lookup"><span data-stu-id="003a1-255">Yes</span></span> |
| <span data-ttu-id="003a1-256">inputs</span><span class="sxs-lookup"><span data-stu-id="003a1-256">inputs</span></span> | <span data-ttu-id="003a1-257">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="003a1-257">Optional.</span></span> <span data-ttu-id="003a1-258">Se si specifica un set di dati di input, deve essere disponibile (in stato "Pronto") per hello stored procedure toorun di attività.</span><span class="sxs-lookup"><span data-stu-id="003a1-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="003a1-259">set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro.</span><span class="sxs-lookup"><span data-stu-id="003a1-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="003a1-260">È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="003a1-261">No</span><span class="sxs-lookup"><span data-stu-id="003a1-261">No</span></span> |
| <span data-ttu-id="003a1-262">outputs</span><span class="sxs-lookup"><span data-stu-id="003a1-262">outputs</span></span> | <span data-ttu-id="003a1-263">È necessario specificare un set di dati di output per un'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="003a1-264">Set di dati di output specifica hello **pianificazione** per hello attività stored procedure (ogni ora, settimanale, mensile, ecc.).</span><span class="sxs-lookup"><span data-stu-id="003a1-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="003a1-265">Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="003a1-266">Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="003a1-267">Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="003a1-268">È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="003a1-269">In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio**, che viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="003a1-270">Sì</span><span class="sxs-lookup"><span data-stu-id="003a1-270">Yes</span></span> |
| <span data-ttu-id="003a1-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="003a1-271">storedProcedureName</span></span> |<span data-ttu-id="003a1-272">Specificare il nome di hello di hello stored procedure in database SQL di Azure hello o un database Azure SQL Data Warehouse o SQL Server che è rappresentato dal servizio hello collegato che Usa tabella di output di hello.</span><span class="sxs-lookup"><span data-stu-id="003a1-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="003a1-273">Sì</span><span class="sxs-lookup"><span data-stu-id="003a1-273">Yes</span></span> |
| <span data-ttu-id="003a1-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="003a1-274">storedProcedureParameters</span></span> |<span data-ttu-id="003a1-275">Specificare i valori dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="003a1-276">Se è necessario toopass null per un parametro, utilizzare la sintassi di hello: "param1": null (lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="003a1-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="003a1-277">Vedere hello seguente toolearn esempio sull'utilizzo di questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="003a1-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="003a1-278">No</span><span class="sxs-lookup"><span data-stu-id="003a1-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="003a1-279">Passaggio di un valore statico</span><span class="sxs-lookup"><span data-stu-id="003a1-279">Passing a static value</span></span>
<span data-ttu-id="003a1-280">A questo punto, si prendano in considerazione l'aggiunta di un'altra colonna denominata 'Scenario' nella tabella hello contenente un valore statico denominato 'Documento di esempio'.</span><span class="sxs-lookup"><span data-stu-id="003a1-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Dati di esempio 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="003a1-282">**Tabella:**</span><span class="sxs-lookup"><span data-stu-id="003a1-282">**Table:**</span></span>

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

<span data-ttu-id="003a1-283">**Stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="003a1-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="003a1-284">A questo punto, passare hello **Scenario** valore di parametro e hello da hello attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="003a1-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="003a1-285">Hello **typeProperties** sezione nel precedente esempio aspetto hello seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="003a1-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

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

<span data-ttu-id="003a1-286">**Set di dati di Data factory:**</span><span class="sxs-lookup"><span data-stu-id="003a1-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="003a1-287">**Pipeline di Data factory**</span><span class="sxs-lookup"><span data-stu-id="003a1-287">**Data Factory pipeline**</span></span>

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