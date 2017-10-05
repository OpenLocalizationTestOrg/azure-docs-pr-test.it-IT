---
title: "Caricare i dati in Azure SQL Data Warehouse – Data factory | Documentazione Microsoft"
description: Questa esercitazione carica i dati in Azure SQL Data Warehouse tramite Data factory di Azure e usa un database SQL Server come origine dati.
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
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="c7459-103">Caricare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c7459-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="c7459-104">È possibile usare Azure Data Factory per caricare dati in Azure SQL Data Warehouse da uno qualsiasi degli [archivi dati di origine supportati](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c7459-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c7459-105">Ad esempio, i dati possono essere caricati da un database SQL di Azure o da un database Oracle in SQL Data Warehouse tramite Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c7459-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="c7459-106">L'esercitazione contenuta in questo articolo mostra come caricare dati da un database di SQL Server locale in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c7459-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="c7459-107">**Tempo stimato**: per completare questa esercitazione sono necessari circa 10-15 minuti una volta soddisfatti i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="c7459-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7459-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7459-108">Prerequisites</span></span>

- <span data-ttu-id="c7459-109">È necessario un **database di SQL Server** con tabelle contenenti i dati da copiare in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c7459-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="c7459-110">È necessario un **SQL Data Warehouse** online.</span><span class="sxs-lookup"><span data-stu-id="c7459-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="c7459-111">Se non si dispone di un data warehouse, vedere l'articolo relativo alla [creazione di un'istanza di Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="c7459-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="c7459-112">È necessario un **account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c7459-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="c7459-113">Se non si dispone di un account di archiviazione, vedere l'articolo relativo alla [creazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c7459-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="c7459-114">Per le migliori prestazioni, posizionare l'account di archiviazione e il data warehouse nella stessa area si Azure.</span><span class="sxs-lookup"><span data-stu-id="c7459-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="c7459-115">Configurare una data factory</span><span class="sxs-lookup"><span data-stu-id="c7459-115">Configure a data factory</span></span>
1. <span data-ttu-id="c7459-116">Accedere al [Portale di Azure][].</span><span class="sxs-lookup"><span data-stu-id="c7459-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="c7459-117">Individuare il data warehouse e fare clic per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="c7459-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="c7459-118">Nel pannello principale fare clic su **Carica dati** > **Data factory di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c7459-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Avviare la procedura guidata di caricamento dei dati](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="c7459-120">Se non si dispone di una data factory nella sottoscrizione di Azure, verrà visualizzata una finestra di dialogo **Nuova data factory** in una scheda separata del browser.</span><span class="sxs-lookup"><span data-stu-id="c7459-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="c7459-121">Inserire le informazioni richieste e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c7459-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="c7459-122">Dopo aver creato la data factory, la finestra di dialogo **Nuova data factory** verrà chiusa e sarà visualizzata la finestra di dialogo **Select Data Factory** (Seleziona data factory).</span><span class="sxs-lookup"><span data-stu-id="c7459-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="c7459-123">Se si dispone già di una o più data factory nella sottoscrizione di Azure, verrà visualizzata la finestra di dialogo **Select Data Factory** (Seleziona data factory).</span><span class="sxs-lookup"><span data-stu-id="c7459-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="c7459-124">In questa finestra di dialogo è possibile selezionare una data factory esistente o fare clic su **Create new data factory** (Crea nuova data factory) per crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="c7459-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Configurare una data factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="c7459-126">Nella finestra di dialogo **Select Data Factory** (Seleziona data factory) l'opzione **Carica dati** è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c7459-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="c7459-127">Fare clic su **Avanti** per avviare la creazione di un'attività di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="c7459-128">Configurare le proprietà della data factory</span><span class="sxs-lookup"><span data-stu-id="c7459-128">Configure the data factory properties</span></span>
<span data-ttu-id="c7459-129">Dopo avere creato una data factory, il passaggio successivo consiste nel configurare la pianificazione di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="c7459-130">Per **Nome attività** immettere **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="c7459-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="c7459-131">Selezionare l'opzione **Esegui una volta** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Configurare il bilanciamento del carico](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="c7459-133">Configurare l'archivio dati e il gateway di origine</span><span class="sxs-lookup"><span data-stu-id="c7459-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="c7459-134">Ora indicare alla data factory il database SQL Server locale da cui si desidera caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="c7459-135">Scegliere **SQL Server** dal catalogo dell'archivio dati di origine supportato e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![Scegliere l'origine SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="c7459-137">Verrà visualizzata la finestra di dialogo **Specify the on-premises SQL Server database** (Specificare il database SQL Server locale).</span><span class="sxs-lookup"><span data-stu-id="c7459-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="c7459-138">Il primo campo **Nome connessione** viene compilato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7459-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="c7459-139">Il secondo campo richiede il nome del **gateway**.</span><span class="sxs-lookup"><span data-stu-id="c7459-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="c7459-140">Se si usa una data factory esistente che dispone già di un gateway, è possibile riusarlo selezionandolo dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c7459-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="c7459-141">Fare clic sul collegamento **Crea gateway** per creare un gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="c7459-142">Se l'archivio dati di origine è locale o in una macchina virtuale IaaS di Azure, è necessario un gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="c7459-143">Un gateway ha una relazione 1-1 con una data factory.</span><span class="sxs-lookup"><span data-stu-id="c7459-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="c7459-144">Non può essere usato da un'altra data factory, ma può essere usato da più attività di caricamento dei dati nella stessa data factory.</span><span class="sxs-lookup"><span data-stu-id="c7459-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="c7459-145">Un gateway consente di connettersi a più archivi di dati durante l'esecuzione di attività di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="c7459-146">Per informazioni dettagliate sul gateway, vedere l'articolo [Gateway di gestione dati](../data-factory/data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c7459-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="c7459-147">Verrà visualizzata la finestra di dialogo **Crea gateway**.</span><span class="sxs-lookup"><span data-stu-id="c7459-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="c7459-148">Come nome immettere **GatewayForDWLoading** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c7459-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="c7459-149">Verrà visualizzata la finestra di dialogo **Configure Gateway** (Configura gateway).</span><span class="sxs-lookup"><span data-stu-id="c7459-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="c7459-150">Fare clic su **Launch express setup on this computer** (Avvia installazione rapida sul computer) per scaricare, installare e registrare automaticamente il gateway di gestione dati nel computer corrente.</span><span class="sxs-lookup"><span data-stu-id="c7459-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="c7459-151">Lo stato di avanzamento viene visualizzato in una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="c7459-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="c7459-152">Se il computer non riesce a connettersi all'archivio dati, è possibile [scaricare e installare il gateway](https://www.microsoft.com/download/details.aspx?id=39717) manualmente in un computer in grado di connettersi all'archivio dati e quindi usare la chiave per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c7459-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="c7459-153">L'installazione rapida funziona in modo nativo con Microsoft Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c7459-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="c7459-154">Se si usa Google Chrome, installare innanzitutto l'estensione ClickOnce dal web store Chrome.</span><span class="sxs-lookup"><span data-stu-id="c7459-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="c7459-156">Attendere il completamento dell'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="c7459-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="c7459-157">Una volta che il gateway è stato registrato correttamente ed è online, la finestra popup viene chiusa e il nuovo gateway viene visualizzato nel campo del gateway.</span><span class="sxs-lookup"><span data-stu-id="c7459-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="c7459-158">Quindi compilare come segue i restanti campi obbligatori e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="c7459-159">**Nome del server**: nome del server SQL locale.</span><span class="sxs-lookup"><span data-stu-id="c7459-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="c7459-160">**Nome del database**: database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7459-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="c7459-161">**Crittografia delle credenziali**: usare il valore predefinito dal web browser.</span><span class="sxs-lookup"><span data-stu-id="c7459-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="c7459-162">**Tipo di autenticazione**: scegliere il tipo di autenticazione in uso.</span><span class="sxs-lookup"><span data-stu-id="c7459-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="c7459-163">**Nome utente** e **Password**: immettere il nome utente e la password per un utente che dispone dell'autorizzazione per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="c7459-165">Il passaggio successivo consiste nello scegliere le tabelle da cui copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="c7459-166">È possibile filtrare le tabelle usando parole chiave.</span><span class="sxs-lookup"><span data-stu-id="c7459-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="c7459-167">Ed è possibile visualizzare in anteprima lo schema dei dati e della tabella nel riquadro inferiore.</span><span class="sxs-lookup"><span data-stu-id="c7459-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="c7459-168">Dopo aver completato la selezione, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-168">After you finish your selection, click **Next**.</span></span>

    ![Selezionare le tabelle](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="c7459-170">Configurare la destinazione, ovvero SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c7459-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="c7459-171">Ora informare Data Factory sulle informazioni di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c7459-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="c7459-172">Le informazioni di connessione di SQL Data Warehouse sono inserite automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7459-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="c7459-173">Immettere il nome utente e la password</span><span class="sxs-lookup"><span data-stu-id="c7459-173">Enter the password for the user name.</span></span> <span data-ttu-id="c7459-174">e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-174">and click **Next**.</span></span>

    ![Configurare la destinazione](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="c7459-176">Viene visualizzato un mapping intelligente delle tabelle che associa le tabelle di origine a quelle di destinazione in base ai nomi di tabella.</span><span class="sxs-lookup"><span data-stu-id="c7459-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="c7459-177">Se la tabella non esiste nella destinazione, per impostazione predefinita Azure Data Factory ne crea una con lo stesso nome; si applica a SQL Server o al database SQL di Azure come origine.</span><span class="sxs-lookup"><span data-stu-id="c7459-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="c7459-178">È possibile anche eseguire il mapping a una tabella esistente.</span><span class="sxs-lookup"><span data-stu-id="c7459-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="c7459-179">Controllare le associazioni e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-179">Review and click **Next**.</span></span>

    ![Eseguire il mapping delle tabelle](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="c7459-181">Esaminare il mapping dello schema e cercare eventuali messaggi di errore o di avviso.</span><span class="sxs-lookup"><span data-stu-id="c7459-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="c7459-182">Il mapping intelligente è basato sui nomi delle colonne.</span><span class="sxs-lookup"><span data-stu-id="c7459-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="c7459-183">Se è presente una conversione di tipo di dati non supportata tra la colonna di origine e di destinazione, viene visualizzato un messaggio di errore insieme della tabella corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c7459-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="c7459-184">Se si sceglie di consentire a Data Factory di creare automaticamente le tabelle, può essere applicata un'adeguata conversione del tipo di dati se è necessario per risolvere eventuali incompatibilità tra gli archivi di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c7459-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Eseguire il mapping dello schema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="c7459-186">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="c7459-187">Configurare le impostazioni delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c7459-187">Configure the performance settings</span></span>
<span data-ttu-id="c7459-188">Nelle configurazioni relative alle prestazioni configurare un account di archiviazione usato per la gestione temporanea dei dati prima di caricarli con efficacia in SQL Data Warehouse usando [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="c7459-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="c7459-189">Al termine della copia, i dati provvisori nell'archiviazione verranno eliminati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7459-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="c7459-190">Selezionare un account di archiviazione di Azure esistente e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c7459-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurare il BLOB di gestione temporanea](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="c7459-192">Esaminare le informazioni di riepilogo e distribuire la pipeline</span><span class="sxs-lookup"><span data-stu-id="c7459-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="c7459-193">Esaminare la configurazione e fare clic sul pulsante **Fine** per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7459-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Distribuire la data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="c7459-195">Monitorare lo stato di avanzamento del caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="c7459-195">Monitor data loading progress</span></span>

<span data-ttu-id="c7459-196">È possibile visualizzare l'avanzamento e i risultati della distribuzione nella pagina **Distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="c7459-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="c7459-197">Una volta terminata la distribuzione, fare clic sul collegamento **Click here to monitor copy pipeline** (Fare clic qui per monitorare la pipeline di copia) per monitorare l'avanzamento del caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7459-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![Monitorare la pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="c7459-199">La pipeline di caricamento dati **DWLoadData-fromSQLServer** appena creata viene selezionata automaticamente da **Esplora risorse** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c7459-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![Visualizzare la pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="c7459-201">Fare clic nella pipeline nel pannello centrale per vedere lo stato dettagliato per ogni tabella associata a un'attività.</span><span class="sxs-lookup"><span data-stu-id="c7459-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![Visualizzare l'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="c7459-203">Fare clic su un'attività per visualizzare i dettagli di caricamento dei dati nel riquadro di destra, tra cui la dimensione dei dati, le righe, la velocità effettiva e così via.</span><span class="sxs-lookup"><span data-stu-id="c7459-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![Visualizzare i dettagli dell'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="c7459-205">Per avviare questa visualizzazione di monitoraggio in seguito, accedere al proprio SQL Data Warehouse, fare clic su **Carica dati > Data factory di Azure**, selezionare la data factory e scegliere **Monitor existing loading tasks** (Monitora attività di caricamento esistenti).</span><span class="sxs-lookup"><span data-stu-id="c7459-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7459-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7459-206">Next steps</span></span>

<span data-ttu-id="c7459-207">Per eseguire la migrazione del database in SQL Data Warehouse, vedere [Eseguire la migrazione della soluzione in SQL Data Warehouse](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="c7459-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="c7459-208">Per altre informazioni su Azure Data Factory e le funzionalità di spostamento dei dati, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7459-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="c7459-209">Introduzione al servizio Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c7459-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="c7459-210">Spostare dati con l'attività di copia</span><span class="sxs-lookup"><span data-stu-id="c7459-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="c7459-211">Spostare dati da e verso Azure SQL Data Warehouse con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c7459-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="c7459-212">Per esplorare i dati in SQL Data Warehouse, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7459-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="c7459-213">Connettersi a SQL Data Warehouse con Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="c7459-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="c7459-214">[Visualizzare i dati con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="c7459-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Portale di Azure]: https://portal.azure.com
