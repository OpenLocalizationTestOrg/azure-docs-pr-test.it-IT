---
title: Caricare terabyte di dati in SQL Data Warehouse | Documentazione Microsoft
description: Illustra come caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="8677a-103">Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Data Factory</span><span class="sxs-lookup"><span data-stu-id="8677a-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="8677a-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) è un database basato su cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati relazionali e non relazionali.</span><span class="sxs-lookup"><span data-stu-id="8677a-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="8677a-105">Basato sull'architettura di elaborazione parallela massiva (MPP, Massively Parallel Processing), SQL Data Warehouse è ottimizzato per i carichi di lavoro dei data warehouse dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8677a-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="8677a-106">Offre l'elasticità del cloud con la flessibilità per ridimensionare la capacità di archiviazione e di calcolo in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="8677a-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="8677a-107">L'uso di Azure SQL Data Warehouse è ora più semplice dell'uso di **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="8677a-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="8677a-108">Azure Data Factory è un servizio di integrazione di dati basato su cloud completamente gestito, che può essere usato per popolare un'istanza di SQL Data Warehouse con i dati del sistema esistente e che consente di risparmiare tempo prezioso durante la valutazione di SQL Data Warehouse e la creazione di soluzioni di analisi.</span><span class="sxs-lookup"><span data-stu-id="8677a-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="8677a-109">Di seguito sono elencati i vantaggi principali del caricamento di dati in Azure SQL Data Warehouse mediante Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="8677a-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="8677a-110">**Semplicità di configurazione**: procedura guidata intuitiva in 5 passaggi, senza necessità di script.</span><span class="sxs-lookup"><span data-stu-id="8677a-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="8677a-111">**Supporto completo per archivi dati**: supporto integrato per una vasta gamma di archivi dati locali e basati su cloud.</span><span class="sxs-lookup"><span data-stu-id="8677a-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="8677a-112">**Sicurezza e conformità**: i dati vengono trasferiti tramite HTTPS o ExpressRoute e la presenza di un servizio globale garantisce che i dati non superino mai il confine geografico.</span><span class="sxs-lookup"><span data-stu-id="8677a-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="8677a-113">**Prestazioni ineguagliabili tramite Polybase**: Polybase rappresenta il modo più efficiente per spostare dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8677a-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8677a-114">Mediante la funzionalità di gestione temporanea dei BLOB è possibile ottenere velocità di carico elevate da tutti i tipi di archivi dati oltre all'archivio BLOB di Azure, supportato da Polybase per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8677a-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="8677a-115">Questo articolo illustra come usare la Copia guidata di Data Factory per caricare 1 TB di dati da Archiviazione BLOB di Azure ad Azure SQL Data Warehouse in meno di 15 minuti a una velocità effettiva di oltre 1,2 GBps.</span><span class="sxs-lookup"><span data-stu-id="8677a-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="8677a-116">Questo articolo include istruzioni dettagliate per spostare dati in Azure SQL Data Warehouse tramite la Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="8677a-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="8677a-117">Per informazioni generali sulle funzionalità di Data Factory per lo spostamento di dati da e verso Azure SQL Data Warehouse, vedere [Spostare dati da e verso Azure SQL Data Warehouse mediante Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8677a-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="8677a-118">È anche possibile creare pipeline usando il portale di Azure, Visual Studio, PowerShell e così via. Per una procedura con istruzioni dettagliate sull'uso dell'attività di copia in Azure Data Factory, vedere l'esercitazione [Copiare dati da un archivio BLOB al database SQL usando Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="8677a-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="8677a-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8677a-119">Prerequisites</span></span>
* <span data-ttu-id="8677a-120">Archivio BLOB di Azure: questo esperimento usa l'archivio BLOB di Azure (GRS) per l'archiviazione di set di dati di test TPC-H.</span><span class="sxs-lookup"><span data-stu-id="8677a-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="8677a-121">Se non si ha un account di archiviazione di Azure, vedere l'articolo relativo alla [creazione di un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8677a-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="8677a-122">Dati [TPC-H](http://www.tpc.org/tpch/): si userà TPC-H come set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="8677a-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="8677a-123">A tale scopo, è necessario usare `dbgen` dal toolkit TPC-H, che consente di generare il set di dati.</span><span class="sxs-lookup"><span data-stu-id="8677a-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="8677a-124">È possibile scaricare il codice sorgente per `dbgen` dagli [strumenti TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilarlo autonomamente oppure scaricare il file binario compilato da [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="8677a-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="8677a-125">Eseguire dbgen.exe con i comandi seguenti per generare un file flat da 1 TB per la tabella `lineitem` distribuito tra 10 file:</span><span class="sxs-lookup"><span data-stu-id="8677a-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="8677a-126">…</span><span class="sxs-lookup"><span data-stu-id="8677a-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="8677a-127">Copiare ora i file generati nel BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8677a-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="8677a-128">Per informazioni su come eseguire questa operazione usando ADF Copy, vedere [Spostare i dati da e nel file system locale usando Azure Data Factory](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8677a-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="8677a-129">Azure SQL Data Warehouse: in questo esperimento i dati vengono caricati nell'istanza di Azure SQL Data Warehouse creata con 6000 DWU (Data Warehouse Units)</span><span class="sxs-lookup"><span data-stu-id="8677a-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="8677a-130">Per informazioni su come creare un database di SQL Data Warehouse, vedere [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) (Creare un'istanza di Azure SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="8677a-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="8677a-131">Per ottenere le migliori prestazioni di caricamento possibili in SQL Data Warehouse usando Polybase, si è scelto il numero massimo di DWU consentito nell'impostazione delle prestazioni, ovvero 6000 DWU.</span><span class="sxs-lookup"><span data-stu-id="8677a-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8677a-132">Durante il caricamento dal BLOB di Azure, le prestazioni di caricamento dei dati sono direttamente proporzionali al numero di DWU configurate in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="8677a-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="8677a-133">Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 1.000 DWU richiede 87 minuti (alla velocità effettiva di circa 200 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 2.000 DWU richiede 46 minuti (alla velocità effettiva di circa 380 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 6.000 DWU richiede 14 minuti (alla velocità effettiva di circa 1,2 GBps)</span><span class="sxs-lookup"><span data-stu-id="8677a-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="8677a-134">Per creare un'istanza di SQL Data Warehouse con 6000 DWU, spostare il dispositivo di scorrimento delle prestazioni verso destra:</span><span class="sxs-lookup"><span data-stu-id="8677a-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Dispositivo di scorrimento delle prestazioni](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="8677a-136">Se un database esistente non è configurato con 6000 DWU, è possibile aumentarne la capacità tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8677a-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="8677a-137">Passare al database nel portale di Azure e individuare il pulsante **Ridimensiona** nel pannello **Panoramica** illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="8677a-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Pulsante Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="8677a-139">Fare clic sul pulsante **Ridimensiona** per aprire il pannello seguente, spostare il dispositivo di scorrimento fino al valore massimo e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8677a-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Finestra di dialogo Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="8677a-141">In questo esperimento i dati vengono caricati in Azure SQL Data Warehouse mediante la classe di risorse `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="8677a-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="8677a-142">Per ottenere la velocità effettiva migliore possibile, è necessario eseguire la copia tramite un utente di SQL Data Warehouse appartenente alla classe di risorse `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="8677a-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="8677a-143">Per eseguire questa operazione, seguire la procedura descritta in [Esempio di modifica della classe di risorse di un utente](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="8677a-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="8677a-144">Creare lo schema della tabella di destinazione nel database di Azure SQL Data Warehouse eseguendo l'istruzione DDL seguente:</span><span class="sxs-lookup"><span data-stu-id="8677a-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="8677a-145">Dopo aver completato i passaggi preliminari necessari, è ora possibile configurare l'attività di copia mediante la Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="8677a-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="8677a-146">Avviare la Copia guidata</span><span class="sxs-lookup"><span data-stu-id="8677a-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="8677a-147">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8677a-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8677a-148">Fare clic su **+ NUOVO** nell'angolo in alto a sinistra e quindi su **Intelligence e analisi** e su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="8677a-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="8677a-149">Nel pannello **Nuova data factory** :</span><span class="sxs-lookup"><span data-stu-id="8677a-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="8677a-150">Immettere **LoadIntoSQLDWDataFactory** come **nome**.</span><span class="sxs-lookup"><span data-stu-id="8677a-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="8677a-151">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8677a-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="8677a-152">Se viene visualizzato un errore simile a **Nome "LoadIntoSQLDWDataFactory" per la data factory non disponibile**, cambiare il nome della data factory (ad esempio, nomeutenteLoadIntoSQLDWDataFactory) e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="8677a-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="8677a-153">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="8677a-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="8677a-154">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="8677a-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="8677a-155">In Gruppo di risorse eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="8677a-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="8677a-156">Selezionare **Usa esistente** per scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="8677a-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="8677a-157">Selezionare **Crea nuovo** per immettere un nome per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8677a-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="8677a-158">Selezionare una **località** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="8677a-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="8677a-159">Selezionare la casella di controllo **Aggiungi al dashboard** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="8677a-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="8677a-160">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8677a-160">Click **Create**.</span></span>
4. <span data-ttu-id="8677a-161">Al termine della creazione verrà visualizzato il pannello **Data factory**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="8677a-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Home page di Data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="8677a-163">Nella home page di Data Factory fare clic sul riquadro **Copia dati** per avviare la **Copy Wizard** (Copia guidata).</span><span class="sxs-lookup"><span data-stu-id="8677a-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8677a-164">Se il Web browser è bloccato su "Concessione autorizzazioni in corso...", disabilitare/deselezionare l'impostazione **Block third party cookies and site data** (Blocca cookie e dati del sito di terze parti) oppure lasciarla abilitata e creare un'eccezione per **login.microsoftonline.com** e quindi provare di nuovo ad avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="8677a-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="8677a-165">Passaggio 1: Configurare una pianificazione di caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="8677a-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="8677a-166">Il primo passaggio consiste nel configurare la pianificazione di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="8677a-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="8677a-167">Nella pagina **Proprietà** :</span><span class="sxs-lookup"><span data-stu-id="8677a-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="8677a-168">Immettere **CopyFromBlobToAzureSqlDataWarehouse** per **Nome attività**</span><span class="sxs-lookup"><span data-stu-id="8677a-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="8677a-169">Selezionare l'opzione **Esegui una volta**.</span><span class="sxs-lookup"><span data-stu-id="8677a-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="8677a-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-170">Click **Next**.</span></span>  

    ![Copia guidata: pagina delle proprietà](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="8677a-172">Passaggio 2: Configurare l'origine</span><span class="sxs-lookup"><span data-stu-id="8677a-172">Step 2: Configure source</span></span>
<span data-ttu-id="8677a-173">Questa sezione illustra i passaggi per configurare l'origine: BLOB di Azure contenente i file delle voci TPC-H da 1 TB.</span><span class="sxs-lookup"><span data-stu-id="8677a-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="8677a-174">Selezionare **Archivio BLOB di Azure** come archivio dati e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Copia guidata: selezionare la pagina di origine](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="8677a-176">Immettere le informazioni di connessione per l'account di archiviazione BLOB di Azure e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Copia guidata: informazioni sulla connessione di origine](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="8677a-178">Scegliere la **cartella** contenente i file della voce TPC-H e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Copia guidata: selezionare la cartella di input](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="8677a-180">Facendo clic su **Avanti** le impostazioni del formato di file vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8677a-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="8677a-181">Verificare che il delimitatore di colonna sia "|" anziché la virgola predefinita ",".</span><span class="sxs-lookup"><span data-stu-id="8677a-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="8677a-182">Dopo aver visualizzato l'anteprima dei dati fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-182">Click **Next** after you have previewed the data.</span></span>

    ![Copia guidata: impostazioni di formattazione file](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="8677a-184">Passaggio 3: Configurare la destinazione</span><span class="sxs-lookup"><span data-stu-id="8677a-184">Step 3: Configure destination</span></span>
<span data-ttu-id="8677a-185">Questa sezione illustra come configurare la destinazione: tabella `lineitem` nel database di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8677a-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="8677a-186">Selezionare **Azure SQL Data Warehouse** come archivio di destinazione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Copia guidata: selezionare l'archivio dati di destinazione](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="8677a-188">Immettere le informazioni di connessione per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8677a-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="8677a-189">Assicurarsi di specificare l'utente membro del ruolo `xlargerc` (per informazioni dettagliate, vedere la sezione **Prerequisiti**), quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Copia guidata: informazioni sulla connessione di destinazione](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="8677a-191">Scegliere la tabella di destinazione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-191">Choose the destination table and click **Next**.</span></span>

    ![Copia guidata: pagina del mapping della tabella](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="8677a-193">Nella pagina Mapping dello schema, lasciare deselezionata l'opzione "Apply column mapping" (Applica mapping di colonne) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="8677a-194">Passaggio 4: Impostazioni relative alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="8677a-194">Step 4: Performance settings</span></span>

<span data-ttu-id="8677a-195">L'opzione **Allow polybase** (Consenti Polybase) è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8677a-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="8677a-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8677a-196">Click **Next**.</span></span>

![Copia guidata: pagina del mapping dello schema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="8677a-198">Passaggio 5: Distribuire e monitorare i risultati del caricamento</span><span class="sxs-lookup"><span data-stu-id="8677a-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="8677a-199">Fare clic sul pulsante **Fine** per eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8677a-199">Click **Finish** button to deploy.</span></span>

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="8677a-201">Al termine della distribuzione, fare clic su `Click here to monitor copy pipeline` per monitorare l'avanzamento dell'esecuzione della copia.</span><span class="sxs-lookup"><span data-stu-id="8677a-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="8677a-202">Scegliere la pipeline di copia creata nell'elenco **Activity Windows** (Finestre attività).</span><span class="sxs-lookup"><span data-stu-id="8677a-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="8677a-204">È possibile visualizzare i dettagli relativi all'esecuzione della copia in **Activity Window Explorer** (Esplora attività) nel riquadro di destra, inclusi il volume dei dati letti dall'origine e scritti nella destinazione, la durata e la velocità effettiva media dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8677a-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="8677a-205">Come si può notare dalla schermata seguente, la copia di 1 TB dall'archivio BLOB di Azure a SQL Data Warehouse ha richiesto 14 minuti, raggiungendo di fatto la velocità effettiva di 1,22 Gbps.</span><span class="sxs-lookup"><span data-stu-id="8677a-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Copia guidata: finestra di dialogo operazione completata](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="8677a-207">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="8677a-207">Best practices</span></span>
<span data-ttu-id="8677a-208">Di seguito sono elencate alcune procedure consigliate per l'esecuzione del database di Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="8677a-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="8677a-209">Usare una classe di risorse di dimensioni maggiori durante il caricamento in un INDICE COLUMNSTORE CLUSTER.</span><span class="sxs-lookup"><span data-stu-id="8677a-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="8677a-210">Per join più efficienti, è consigliabile usare la distribuzione hash da una colonna di selezione anziché la distribuzione round robin predefinita.</span><span class="sxs-lookup"><span data-stu-id="8677a-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="8677a-211">Per una maggiore velocità di carico, è consigliabile usare un heap per i dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="8677a-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="8677a-212">Creare statistiche al termine del caricamento di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8677a-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="8677a-213">Per informazioni dettagliate, vedere [Procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="8677a-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8677a-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8677a-214">Next steps</span></span>
* <span data-ttu-id="8677a-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) (Copia guidata di Data Factory): questo articolo include informazioni dettagliate sulla Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="8677a-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="8677a-216">[Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md): questo articolo include la guida all'ottimizzazione e alle misurazioni delle prestazioni di riferimento.</span><span class="sxs-lookup"><span data-stu-id="8677a-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
