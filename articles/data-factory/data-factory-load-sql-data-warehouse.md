---
title: aaaLoad terabyte di dati in SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="d7a8a-103">Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7a8a-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="d7a8a-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) è un database basato su cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati relazionali e non relazionali.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="d7a8a-105">Basato sull'architettura di elaborazione parallela massiva (MPP, Massively Parallel Processing), SQL Data Warehouse è ottimizzato per i carichi di lavoro dei data warehouse dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="d7a8a-106">Offre l'elasticità con hello flessibilità tooscale di archiviazione del cloud e di calcolo in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="d7a8a-107">L'uso di Azure SQL Data Warehouse è ora più semplice dell'uso di **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="d7a8a-108">Data Factory di Azure è un servizio di integrazione di dati basato su cloud completamente gestito, che può essere utilizzato toopopulate un SQL Data Warehouse con dati hello dal sistema esistente e risparmiare tempo prezioso durante la valutazione di SQL Data Warehouse e la compilazione del analitica soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="d7a8a-109">Ecco i vantaggi principali di hello di caricare dati in Azure SQL Data Warehouse utilizzando Data Factory di Azure:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="d7a8a-110">**Facile tooset backup**: 5-intuitivo guidata non necessari di scripting.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="d7a8a-111">**Supporto completo per archivi dati**: supporto integrato per una vasta gamma di archivi dati locali e basati su cloud.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="d7a8a-112">**Protetti e conformi**: i dati vengono trasferiti tramite HTTPS ExpressRoute e presenza servizio globale garantisce i dati non oltrepassa mai confini geografici hello</span><span class="sxs-lookup"><span data-stu-id="d7a8a-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="d7a8a-113">**Prestazioni ineguagliabile tramite PolyBase** – utilizzando Polybase è più efficiente modo toomove dati hello in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d7a8a-114">Utilizza hello funzionalità blob di gestione temporanea, è possibile ottenere la velocità di carico elevato da tutti i tipi di archivi dati oltre all'archiviazione Blob di Azure che hello Polybase supporta per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="d7a8a-115">In questo articolo illustra come toouse Data Factory Copia guidata tooload 1 TB dati dall'archiviazione Blob di Azure in Azure SQL Data Warehouse in meno di 15 minuti, a una velocità effettiva superiore a 1,2 GBps.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="d7a8a-116">In questo articolo vengono fornite istruzioni dettagliate per lo spostamento dei dati tramite Copia guidata hello in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="d7a8a-117">Per informazioni generali sulle funzionalità di Data Factory di spostamento dei dati da e verso Azure SQL Data Warehouse, vedere [spostare tooand dati da Azure SQL Data Warehouse usando Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="d7a8a-118">È anche possibile creare pipeline usando il portale di Azure, Visual Studio, PowerShell e così via. Vedere [esercitazione: copiare i dati da tooAzure Blob di Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per un'esercitazione rapida con istruzioni dettagliate per l'utilizzo di attività di copia hello in Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="d7a8a-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d7a8a-119">Prerequisites</span></span>
* <span data-ttu-id="d7a8a-120">Archivio BLOB di Azure: questo esperimento usa l'archivio BLOB di Azure (GRS) per l'archiviazione di set di dati di test TPC-H.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="d7a8a-121">Se non si dispone di un account di archiviazione di Azure, ottenere informazioni [come un account di archiviazione toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d7a8a-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="d7a8a-122">[TPC-H](http://www.tpc.org/tpch/) dati: verrà toouse TPC-H come set di dati testing hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="d7a8a-123">toodo, è necessario toouse `dbgen` dal toolkit TPC-H, che consente di generare set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="d7a8a-124">Si può scaricare il codice sorgente per `dbgen` da [strumenti TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilarlo oppure download hello compilato binario da [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="d7a8a-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="d7a8a-125">Toogenerate file flat di 1 TB per i comandi di esecuzione dbgen.exe con seguenti hello `lineitem` tabella distribuito tra i 10 file:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="d7a8a-126">…</span><span class="sxs-lookup"><span data-stu-id="d7a8a-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="d7a8a-127">Ora hello copia generati tooAzure file Blob.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="d7a8a-128">Fare riferimento troppo[spostare tooand dati da un file system locale usando Azure Data Factory](data-factory-onprem-file-system-connector.md) come toodo che tramite Copia file ADF.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="d7a8a-129">Azure SQL Data Warehouse: in questo esperimento i dati vengono caricati nell'istanza di Azure SQL Data Warehouse creata con 6000 DWU (Data Warehouse Units)</span><span class="sxs-lookup"><span data-stu-id="d7a8a-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="d7a8a-130">Fare riferimento troppo[creare un Data Warehouse di SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) per istruzioni dettagliate su come toocreate SQL di un Data Warehouse del database.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="d7a8a-131">tooget hello carico possibile ottenere prestazioni ottimali in SQL Data Warehouse tramite Polybase, si sceglie di numero massimo di Data Warehouse unità (Dwu) consentito nell'impostazione delle prestazioni di hello, che è 6.000 Dwu.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d7a8a-132">Durante il caricamento dal Blob di Azure, prestazioni di caricamento dati di hello sono direttamente proporzionale toohello numero Dwu configurare nei hello SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="d7a8a-133">Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 1.000 DWU richiede 87 minuti (alla velocità effettiva di circa 200 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 2.000 DWU richiede 46 minuti (alla velocità effettiva di circa 380 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 6.000 DWU richiede 14 minuti (alla velocità effettiva di circa 1,2 GBps)</span><span class="sxs-lookup"><span data-stu-id="d7a8a-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="d7a8a-134">toocreate un SQL Data Warehouse con 6.000 Dwu, scorrimento hello prestazioni tutti hello modo toohello destra:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Dispositivo di scorrimento delle prestazioni](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="d7a8a-136">Se un database esistente non è configurato con 6000 DWU, è possibile aumentarne la capacità tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="d7a8a-137">Esplorare database toohello nel portale di Azure ed è disponibile un **scala** pulsante hello **Panoramica** pannello mostrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Pulsante Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="d7a8a-139">Fare clic su hello **scala** seguente di hello tooopen pulsante pannello, spostare il valore massimo toohello del dispositivo di scorrimento hello e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Finestra di dialogo Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="d7a8a-141">In questo esperimento i dati vengono caricati in Azure SQL Data Warehouse mediante la classe di risorse `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="d7a8a-142">esigenze di copia tooachieve migliori prestazioni possibili, toobe eseguita tramite un utente di SQL Data Warehouse appartenente troppo`xlargerc` classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="d7a8a-143">Informazioni su come toodo che seguendo [un esempio di classe di risorse utente di modificare](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d7a8a-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="d7a8a-144">Creazione dello schema di tabella di destinazione nel database di Azure SQL Data Warehouse, eseguendo l'istruzione DDL hello:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

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
<span data-ttu-id="d7a8a-145">Con passaggi preliminari hello completati, è ora sono attività di copia hello tooconfigure pronto utilizzando Copia guidata hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="d7a8a-146">Avviare la Copia guidata</span><span class="sxs-lookup"><span data-stu-id="d7a8a-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="d7a8a-147">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7a8a-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d7a8a-148">Fare clic su **+ nuovo** dall'angolo superiore sinistro di hello, fare clic su **Intelligence + analitica**, fare clic su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="d7a8a-149">In hello **nuova data factory** pannello:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="d7a8a-150">Immettere **LoadIntoSQLDWDataFactory** per hello **nome**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="d7a8a-151">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d7a8a-152">Se viene visualizzato l'errore hello: **"LoadIntoSQLDWDataFactory" nome della Data factory non è disponibile**, modificare il nome di hello di hello data factory (ad esempio, yournameLoadIntoSQLDWDataFactory) e provare a creare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="d7a8a-153">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="d7a8a-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="d7a8a-154">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="d7a8a-155">Per il gruppo di risorse, effettuare una delle hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="d7a8a-156">Selezionare **utilizzare esistente** tooselect un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="d7a8a-157">Selezionare **Crea nuovo** tooenter un nome per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="d7a8a-158">Selezionare un **percorso** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="d7a8a-159">Selezionare **toodashboard Pin** casella di controllo nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="d7a8a-160">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-160">Click **Create**.</span></span>
4. <span data-ttu-id="d7a8a-161">Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Home page di Data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="d7a8a-163">Nella home page di hello Data Factory, fare clic su hello **copiare dati** riquadro toolaunch **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d7a8a-164">Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", disabilitare o deselezionare **bloccare i cookie di terze parti e i dati del sito** (oppure) mantenere abilitato e creare un'eccezione per **login.microsoftonline.com**e quindi provare ad avviare la procedura guidata hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="d7a8a-165">Passaggio 1: Configurare una pianificazione di caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="d7a8a-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="d7a8a-166">primo passaggio Hello è dati hello tooconfigure durante il caricamento di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="d7a8a-167">In hello **proprietà** pagina:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="d7a8a-168">Immettere **CopyFromBlobToAzureSqlDataWarehouse** per **Nome attività**</span><span class="sxs-lookup"><span data-stu-id="d7a8a-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="d7a8a-169">Selezionare l'opzione **Esegui una volta**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="d7a8a-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-170">Click **Next**.</span></span>  

    ![Copia guidata: pagina delle proprietà](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="d7a8a-172">Passaggio 2: Configurare l'origine</span><span class="sxs-lookup"><span data-stu-id="d7a8a-172">Step 2: Configure source</span></span>
<span data-ttu-id="d7a8a-173">Questa sezione è illustrato hello origine hello tooconfigure di passaggi: Blob di Azure contenente hello 1 TB TPC-file voce H.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="d7a8a-174">Seleziona hello **archiviazione Blob di Azure** come dati hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Copia guidata: selezionare la pagina di origine](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="d7a8a-176">Immettere informazioni di connessione hello per hello account di archiviazione Blob di Azure, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Copia guidata: informazioni sulla connessione di origine](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="d7a8a-178">Scegliere hello **cartella** riga hello TPC-H contenente i file di elemento e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Copia guidata: selezionare la cartella di input](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="d7a8a-180">Fare clic su **Avanti**, impostazioni di formato di file hello vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="d7a8a-181">Verificare che il delimitatore di colonna sia toomake ' | 'anziché una virgola predefinito hello','.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="d7a8a-182">Fare clic su **Avanti** dopo avere visualizzata in anteprima i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-182">Click **Next** after you have previewed hello data.</span></span>

    ![Copia guidata: impostazioni di formattazione file](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="d7a8a-184">Passaggio 3: Configurare la destinazione</span><span class="sxs-lookup"><span data-stu-id="d7a8a-184">Step 3: Configure destination</span></span>
<span data-ttu-id="d7a8a-185">In questa sezione viene illustrato come tooconfigure hello destinazione: `lineitem` tabella nel database di hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="d7a8a-186">Scegliere **Azure SQL Data Warehouse** come destinazione di hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Copia guidata: selezionare l'archivio dati di destinazione](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="d7a8a-188">Inserire informazioni di connessione hello per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="d7a8a-189">Assicurarsi di specificare l'utente hello che è un membro del ruolo hello `xlargerc` (vedere hello **prerequisiti** sezione per informazioni dettagliate), fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Copia guidata: informazioni sulla connessione di destinazione](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="d7a8a-191">Scegliere la tabella di destinazione hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-191">Choose hello destination table and click **Next**.</span></span>

    ![Copia guidata: pagina del mapping della tabella](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="d7a8a-193">Nella pagina Mapping dello schema, lasciare deselezionata l'opzione "Apply column mapping" (Applica mapping di colonne) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="d7a8a-194">Passaggio 4: Impostazioni relative alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d7a8a-194">Step 4: Performance settings</span></span>

<span data-ttu-id="d7a8a-195">L'opzione **Allow polybase** (Consenti Polybase) è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="d7a8a-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-196">Click **Next**.</span></span>

![Copia guidata: pagina del mapping dello schema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="d7a8a-198">Passaggio 5: Distribuire e monitorare i risultati del caricamento</span><span class="sxs-lookup"><span data-stu-id="d7a8a-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="d7a8a-199">Fare clic su **fine** toodeploy pulsante.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-199">Click **Finish** button toodeploy.</span></span>

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="d7a8a-201">Una volta completata la distribuzione di hello, fare clic su `Click here toomonitor copy pipeline` copia hello toomonitor avanzamento dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="d7a8a-202">Pipeline copia selezionare hello è stato creato in hello **attività Windows** elenco.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="d7a8a-204">È possibile visualizzare i dettagli di esecuzione in hello copia di hello **attività finestra Esplora** nel riquadro di destra hello, compresi hello volume di dati letti dall'origine e scritti nella destinazione, la durata e velocità effettiva Media di hello per hello eseguire.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="d7a8a-205">Come si può vedere dal hello seguente cattura di schermata e la copia di 1 TB da archiviazione Blob di Azure in SQL Data Warehouse ha impiegato 14 minuti, in modo efficace una velocità effettiva di GBps 1.22!</span><span class="sxs-lookup"><span data-stu-id="d7a8a-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Copia guidata: finestra di dialogo operazione completata](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="d7a8a-207">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="d7a8a-207">Best practices</span></span>
<span data-ttu-id="d7a8a-208">Di seguito sono elencate alcune procedure consigliate per l'esecuzione del database di Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d7a8a-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="d7a8a-209">Usare una classe di risorse di dimensioni maggiori durante il caricamento in un INDICE COLUMNSTORE CLUSTER.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="d7a8a-210">Per join più efficienti, è consigliabile usare la distribuzione hash da una colonna di selezione anziché la distribuzione round robin predefinita.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="d7a8a-211">Per una maggiore velocità di carico, è consigliabile usare un heap per i dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="d7a8a-212">Creare statistiche al termine del caricamento di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d7a8a-213">Per informazioni dettagliate, vedere [Procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d7a8a-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7a8a-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7a8a-214">Next steps</span></span>
* <span data-ttu-id="d7a8a-215">[Data Factory Copia guidata](data-factory-copy-wizard.md) -questo articolo fornisce informazioni dettagliate sulla copia guidata hello.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="d7a8a-216">[Copiare l'attività manuale sulle prestazioni e ottimizzazione](data-factory-copy-activity-performance.md) -questo articolo sono contenute le misurazioni delle prestazioni di riferimento hello e Guida all'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="d7a8a-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
