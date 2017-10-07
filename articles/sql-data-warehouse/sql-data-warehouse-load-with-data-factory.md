---
title: "dati di aaaLoad in Azure SQL Data Warehouse – Data Factory | Documenti Microsoft"
description: In questa esercitazione carica i dati in Azure SQL Data Warehouse utilizzando Data Factory di Azure e Usa un database di SQL Server come origine dati hello.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="1ff0d-103">Caricare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1ff0d-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="1ff0d-104">È possibile utilizzare dati tooload Data Factory di Azure in Azure SQL Data Warehouse da qualsiasi hello [archivi dati di origine supportata](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1ff0d-105">Ad esempio, i dati possono essere caricati da un database SQL di Azure o da un database Oracle in SQL Data Warehouse tramite Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="1ff0d-106">Esercitazione in questo articolo illustra come dati tooload da un Server SQL locale del database in un data warehouse SQL.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="1ff0d-107">**Tempo stimato**: in questa esercitazione richiede circa 10-15 minuti toocomplete una volta soddisfatti i prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ff0d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1ff0d-108">Prerequisites</span></span>

- <span data-ttu-id="1ff0d-109">È necessario un **database di SQL Server** con le tabelle che contengono dati hello toobe copiate toohello data warehouse di SQL.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="1ff0d-110">È necessario un **SQL Data Warehouse** online.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="1ff0d-111">Se si dispone già di un data warehouse, informazioni su come troppo[creare un Data Warehouse di SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="1ff0d-112">È necessario un **account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="1ff0d-113">Se si dispone già di un account di archiviazione, informazioni su come troppo[creare un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1ff0d-114">Per prestazioni ottimali, individuare l'account di archiviazione hello e hello data warehouse in hello stessa regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="1ff0d-115">Configurare una data factory</span><span class="sxs-lookup"><span data-stu-id="1ff0d-115">Configure a data factory</span></span>
1. <span data-ttu-id="1ff0d-116">Accedi toohello [portale di Azure][].</span><span class="sxs-lookup"><span data-stu-id="1ff0d-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="1ff0d-117">Individuare il data warehouse e fare clic su tooopen è.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="1ff0d-118">Nel pannello principale hello, fare clic su **Carica dati** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Avviare la procedura guidata di caricamento dei dati](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="1ff0d-120">Se si ha una data factory nella sottoscrizione di Azure, viene visualizzato un **nuova Data Factory** la finestra di dialogo in una scheda separata del browser hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="1ff0d-121">Compilare hello informazioni richieste e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="1ff0d-122">Dopo la creazione di data factory di hello hello **nuova Data Factory** chiude la finestra di dialogo e viene visualizzato hello **selezionare Data Factory** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="1ff0d-123">Se si dispone di uno o più factory di dati già presenti nella sottoscrizione di Azure hello, vedrai hello **selezionare Data Factory** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="1ff0d-124">Nella finestra di dialogo, è possibile selezionare una data factory esistente o fare clic su **Crea nuova data factory** toocreate uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Configurare una data factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="1ff0d-126">In hello **selezionare Data Factory** della finestra di dialogo hello **caricare dati** opzione è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="1ff0d-127">Fare clic su **Avanti** toostart la creazione di un'attività di caricamento di dati.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="1ff0d-128">Configurare le proprietà di hello data factory</span><span class="sxs-lookup"><span data-stu-id="1ff0d-128">Configure hello data factory properties</span></span>
<span data-ttu-id="1ff0d-129">Dopo avere creato una data factory, hello sarà dati hello tooconfigure durante il caricamento di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="1ff0d-130">Per **Nome attività** immettere **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="1ff0d-131">Utilizzare hello predefinito **Esegui una volta** opzione, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configurare il bilanciamento del carico](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="1ff0d-133">Configurare l'archivio dati di origine hello e gateway</span><span class="sxs-lookup"><span data-stu-id="1ff0d-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="1ff0d-134">Ora informare Data Factory di database di SQL Server on-premise hello da cui si desidera dati tooload.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="1ff0d-135">Scegliere **SQL Server** dai dati di origine supportato di hello archiviare catalogo e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Scegliere l'origine SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="1ff0d-137">Oggetto **database di SQL Server on-premise hello specificare** viene visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="1ff0d-138">prima di Hello **nome connessione** campo viene automaticamente compilato.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="1ff0d-139">secondo campo Hello chiede nome hello di hello **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="1ff0d-140">Se si utilizza una data factory esistente che dispone già di un gateway, è possibile riutilizzare gateway hello selezionandolo dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="1ff0d-141">Fare clic su hello **crea Gateway** collegamento toocreate un Gateway di gestione di dati.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="1ff0d-142">Se l'archivio dati di origine hello è locale o in una macchina virtuale IaaS di Azure, è necessario un Gateway di gestione di dati.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="1ff0d-143">Un gateway ha una relazione 1-1 con una data factory.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="1ff0d-144">Non può essere utilizzato da un altro data factory, ma può essere utilizzato da più attività con hello di caricamento di dati stessa data factory.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="1ff0d-145">Un gateway può essere utilizzato tooconnect toomultiple gli archivi dati durante l'esecuzione di attività di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="1ff0d-146">Per informazioni dettagliate sul gateway hello, vedere [Gateway di gestione dati](../data-factory/data-factory-data-management-gateway.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="1ff0d-147">Verrà visualizzata la finestra di dialogo **Crea gateway**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="1ff0d-148">Come nome immettere **GatewayForDWLoading** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="1ff0d-149">Verrà visualizzata la finestra di dialogo **Configure Gateway** (Configura gateway).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="1ff0d-150">Fare clic su **avviare l'installazione rapida in questo computer** tooautomatically scaricare, installare e registrare il Gateway di gestione di dati sul computer corrente.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="1ff0d-151">stato di Hello è visualizzato in una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="1ff0d-152">Se la macchina hello non può connettersi archivio dati toohello, è possibile eseguire manualmente [scaricare e installare il gateway hello](https://www.microsoft.com/download/details.aspx?id=39717) in un computer che può connettersi a dati toohello archiviare e quindi utilizzare tooregister chiave hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="1ff0d-153">l'installazione rapida Hello funziona in modo nativo con Microsoft Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="1ff0d-154">Se si utilizza Google Chrome, installare innanzitutto estensione ClickOnce hello dall'archivio web Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="1ff0d-156">Attendere toocomplete il programma di installazione di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="1ff0d-157">Una volta gateway hello viene registrata correttamente e sia in linea, chiude la finestra popup di hello e nuovo gateway hello viene visualizzato nel campo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="1ff0d-158">Quindi, compilare il resto di hello richiesto campi come indicato di seguito, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="1ff0d-159">**Nome del server**: nome di hello SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="1ff0d-160">**Nome del database**: database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="1ff0d-161">**Crittografia delle credenziali**: hello predefinito "dal web browser".</span><span class="sxs-lookup"><span data-stu-id="1ff0d-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="1ff0d-162">**Tipo di autenticazione**: scegliere il tipo di hello di autenticazione si sta usando.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="1ff0d-163">**Nome utente** e **password**: immettere il nome di utente hello e una password per un utente che dispone di dati di autorizzazione toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="1ff0d-165">passaggio successivo Hello è tabelle hello toochoose da cui toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="1ff0d-166">È possibile filtrare le tabelle di hello utilizzando le parole chiave.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="1ff0d-167">Ed è possibile visualizzare l'anteprima dello schema di dati e tabella hello nel pannello inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="1ff0d-168">Dopo aver completato la selezione, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-168">After you finish your selection, click **Next**.</span></span>

    ![Selezionare le tabelle](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="1ff0d-170">Configurare destinazione hello, il Data Warehouse SQL</span><span class="sxs-lookup"><span data-stu-id="1ff0d-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="1ff0d-171">Ora informare Data Factory di informazioni sulla destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="1ff0d-172">Le informazioni di connessione di SQL Data Warehouse sono inserite automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="1ff0d-173">Immettere la password di hello per nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="1ff0d-174">e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-174">and click **Next**.</span></span>

    ![Configurare la destinazione](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="1ff0d-176">Viene visualizzato un mapping di tabella intelligente che esegue il mapping di tabelle di origine toodestination in base ai nomi di tabella.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="1ff0d-177">Se la tabella hello non esiste nella destinazione hello, per impostazione predefinita ADF verrà creato uno con hello stesso nome (si applica tooSQL Server o Database SQL di Azure come origine).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="1ff0d-178">È anche possibile scegliere toomap tooan esistente nella tabella.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="1ff0d-179">Controllare le associazioni e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-179">Review and click **Next**.</span></span>

    ![Eseguire il mapping delle tabelle](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="1ff0d-181">Esaminare il mapping dello schema hello e cercare i messaggi di errore o avviso.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="1ff0d-182">Il mapping intelligente è basato sui nomi delle colonne.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="1ff0d-183">Se è presente una conversione di tipo di dati non supportati tra colonne di origine e destinazione hello, viene visualizzato un messaggio di errore insieme tabella corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="1ff0d-184">Se si sceglie automaticamente Data Factory toolet creare tabelle hello, conversione di tipi di dati appropriati può verificarsi se necessario incompatibilità hello toofix tra gli archivi di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Eseguire il mapping dello schema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="1ff0d-186">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="1ff0d-187">Configurare le impostazioni delle prestazioni di hello</span><span class="sxs-lookup"><span data-stu-id="1ff0d-187">Configure hello performance settings</span></span>
<span data-ttu-id="1ff0d-188">Nelle configurazioni di prestazioni hello, configurare un account di archiviazione di Azure utilizzato per la gestione temporanea di dati hello prima viene caricato in SQL Data Warehouse rendere più efficiente utilizzando [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="1ff0d-189">Dopo l'operazione di copia hello, dati provvisorio hello nel servizio di archiviazione verranno eseguiti automaticamente la pulizia.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="1ff0d-190">Selezionare un account di archiviazione di Azure esistente e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurare il BLOB di gestione temporanea](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="1ff0d-192">Esaminare le informazioni di riepilogo e distribuire la pipeline hello</span><span class="sxs-lookup"><span data-stu-id="1ff0d-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="1ff0d-193">Rivedere la configurazione di hello e fare clic su **fine** pipeline hello toodeploy di pulsante.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Distribuire la data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="1ff0d-195">Monitorare lo stato di avanzamento del caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="1ff0d-195">Monitor data loading progress</span></span>

<span data-ttu-id="1ff0d-196">È possibile visualizzare l'avanzamento della distribuzione hello e i risultati in hello **distribuzione** pagina.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="1ff0d-197">Una volta hello distribuzione viene eseguita, fare clic su collegamento hello **fare clic qui pipeline copia toomonitor** dati toomonitor avanzamento del caricamento.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Monitorare la pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="1ff0d-199">Hello appena creato **DWLoadData fromSQLServer** pipeline per il caricamento dei dati viene automaticamente selezionato da sinistra hello **Esplora inventario risorse**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Visualizzare la pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="1ff0d-201">Fare clic su nella pipeline hello centro hello hello toosee pannello stato dettagliato per ogni tabella in cui viene eseguito il mapping tooan attività.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Visualizzare l'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="1ff0d-203">Scegliere ulteriormente in un'attività e visualizzare dati hello il caricamento dei dettagli nel riquadro di destra hello tra dimensioni dei dati, le righe, velocità effettiva e così via.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Visualizzare i dettagli dell'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="1ff0d-205">Fare clic su questo monitoraggio visualizzazione versioni successive, visitare tooyour SQL Data Warehouse, toolaunch **Load Data > Data Factory di Azure**, selezionare l'ambiente di produzione e scegliere **monitorare esistente durante il caricamento di attività**.</span><span class="sxs-lookup"><span data-stu-id="1ff0d-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ff0d-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ff0d-206">Next steps</span></span>

<span data-ttu-id="1ff0d-207">vedere il tooSQL database Data Warehouse, toomigrate [Cenni preliminari sulla migrazione](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="1ff0d-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="1ff0d-208">toolearn ulteriori informazioni su Azure Data Factory e le funzionalità di spostamento dei dati, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="1ff0d-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="1ff0d-209">Introduzione tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1ff0d-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="1ff0d-210">Spostare dati con l'attività di copia</span><span class="sxs-lookup"><span data-stu-id="1ff0d-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="1ff0d-211">Spostare dati tooand da usando Azure Data Factory di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1ff0d-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="1ff0d-212">vedere i dati in SQL Data Warehouse, tooexplore hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="1ff0d-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="1ff0d-213">Connettersi tooSQL Data Warehouse con Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="1ff0d-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="1ff0d-214">[Visualizzare i dati con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="1ff0d-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portale di Azure]: https://portal.azure.com
