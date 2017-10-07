---
title: aaaUse Redgate tooload dati tooyour Azure del data warehouse | Documenti Microsoft
description: Informazioni su come Studio di piattaforma di toouse Redgate dati per scenari di data warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="a42fc-103">Caricare dati con Data Platform Studio di Redgate</span><span class="sxs-lookup"><span data-stu-id="a42fc-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a42fc-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="a42fc-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="a42fc-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="a42fc-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="a42fc-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="a42fc-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="a42fc-107">BCP</span><span class="sxs-lookup"><span data-stu-id="a42fc-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="a42fc-108">In questa esercitazione illustra come toouse [dati piattaforma Studio del Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) dati toomove (dp) da un tooAzure di SQL Server on-premise SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="a42fc-109">Dati piattaforma Studio applica correzioni più appropriato per la compatibilità di hello e ottimizzazioni, pertanto dispone di hello più rapidamente tooget modo Introduzione a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="a42fc-110">[Redgate](http://www.red-gate.com), partner Microsoft da lunga data, offre diversi strumenti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a42fc-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="a42fc-111">Questa funzionalità di Data Platform Studio è disponibile gratuitamente per uso sia commerciale che non commerciale.</span><span class="sxs-lookup"><span data-stu-id="a42fc-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="a42fc-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a42fc-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="a42fc-113">Creare o identificare le risorse</span><span class="sxs-lookup"><span data-stu-id="a42fc-113">Create or identify resources</span></span>
<span data-ttu-id="a42fc-114">Prima di iniziare questa esercitazione, è necessario toohave:</span><span class="sxs-lookup"><span data-stu-id="a42fc-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="a42fc-115">**Database di SQL Server locale**: hello dati che si desidera tooimport tooSQL Data Warehouse deve toocome da un Server SQL locale (versione 2008R2 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="a42fc-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="a42fc-116">Data Platform Studio non è in grado di importare direttamente dati da un database SQL di Azure o da file di testo.</span><span class="sxs-lookup"><span data-stu-id="a42fc-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="a42fc-117">**Account di archiviazione Azure**: Studio piattaforma dati prepara i dati hello nell'archiviazione Blob di Azure prima di caricarli in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="a42fc-118">account di archiviazione Hello devono usare modello di distribuzione di "gestione di risorse" hello (impostazione predefinita hello) anziché il modello di distribuzione "Classiche" hello.</span><span class="sxs-lookup"><span data-stu-id="a42fc-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="a42fc-119">Se non si dispone di un account di archiviazione, informazioni su come tooCreate un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="a42fc-120">**SQL Data Warehouse**: in questa esercitazione sposta dati hello da tooSQL di SQL Server on-premise Data Warehouse, pertanto è necessario toohave online a un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="a42fc-121">Se si dispone già di un data warehouse, informazioni su come tooCreate un Data Warehouse di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a42fc-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="a42fc-122">Le prestazioni sono migliori se l'account di archiviazione hello e hello data warehouse vengono creati in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="a42fc-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="a42fc-123">Passaggio 1: Accedi tooData Studio piattaforma con l'account di Azure</span><span class="sxs-lookup"><span data-stu-id="a42fc-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="a42fc-124">Aprire il web browser e passare toohello [Studio piattaforma dati](https://www.dataplatformstudio.com/) sito Web.</span><span class="sxs-lookup"><span data-stu-id="a42fc-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="a42fc-125">Accedi con hello stesso account di Azure che è usato toocreate hello storage account e del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="a42fc-126">Se l'indirizzo di posta elettronica è associato sia un lavoro account e un account Microsoft, che account hello toochoose con tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="a42fc-127">Se si tratta del primo utilizzo Studio piattaforma dati, sono frequenti toogrant hello applicazione autorizzazione toomanage le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a42fc-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="a42fc-128">Passaggio 2: Avviare Importazione guidata hello</span><span class="sxs-lookup"><span data-stu-id="a42fc-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="a42fc-129">Dalla schermata principale di hello dei punti di distribuzione, selezionare hello importazione tooAzure SQL Data Warehouse collegamento toostart hello importazione guidata.</span><span class="sxs-lookup"><span data-stu-id="a42fc-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="a42fc-130">Passaggio 3: Installare hello dati piattaforma Studio Gateway</span><span class="sxs-lookup"><span data-stu-id="a42fc-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="a42fc-131">database di SQL Server on-premise tooyour tooconnect, è necessario tooinstall hello Gateway dei punti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="a42fc-132">gateway Hello è un agente client che fornisce accesso tooyour ambiente locale, estrae i dati di hello e lo carica tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="a42fc-133">I dati non passano mai attraverso i server Redgate.</span><span class="sxs-lookup"><span data-stu-id="a42fc-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="a42fc-134">hello tooinstall Gateway:</span><span class="sxs-lookup"><span data-stu-id="a42fc-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="a42fc-135">Fare clic su hello **crea Gateway** collegamento</span><span class="sxs-lookup"><span data-stu-id="a42fc-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="a42fc-136">Scaricare e installare il Gateway di hello con hello programma di installazione fornito</span><span class="sxs-lookup"><span data-stu-id="a42fc-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="a42fc-137">Hello Gateway può essere installato in tutti i computer con database di SQL Server origine toohello accesso rete.</span><span class="sxs-lookup"><span data-stu-id="a42fc-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="a42fc-138">Accede a database di SQL Server hello utilizzando l'autenticazione di Windows hello credenziali dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="a42fc-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="a42fc-139">Una volta installato, hello tooConnected modifiche dello stato di Gateway ed è possibile fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="a42fc-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="a42fc-140">Passaggio 4: Identificare i database di origine hello</span><span class="sxs-lookup"><span data-stu-id="a42fc-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="a42fc-141">In hello *immettere nome Server* casella di testo, immettere il nome di hello del server di hello che ospita il database e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a42fc-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="a42fc-142">Quindi, dal menu a discesa hello, selezionare hello database tooimport dati.</span><span class="sxs-lookup"><span data-stu-id="a42fc-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="a42fc-143">DP controlla se i database selezionati di hello per le tabelle tooimport.</span><span class="sxs-lookup"><span data-stu-id="a42fc-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="a42fc-144">Per impostazione predefinita, dei punti di distribuzione consente di importare tutte le tabelle hello hello database.</span><span class="sxs-lookup"><span data-stu-id="a42fc-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="a42fc-145">È possibile selezionare o deselezionare le tabelle espandendo hello tutte le tabelle di collegamento.</span><span class="sxs-lookup"><span data-stu-id="a42fc-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="a42fc-146">Selezionare hello rollforward toomove di pulsante Avanti.</span><span class="sxs-lookup"><span data-stu-id="a42fc-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="a42fc-147">Passaggio 5: Scegliere una data di archiviazione account toostage hello</span><span class="sxs-lookup"><span data-stu-id="a42fc-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="a42fc-148">Dei punti di distribuzione richiede i dati hello toostage un percorso.</span><span class="sxs-lookup"><span data-stu-id="a42fc-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="a42fc-149">Scegliere un account di archiviazione esistente dalla sottoscrizione e selezionare **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="a42fc-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="a42fc-150">Crea un nuovo contenitore blob in hello scelto l'account di archiviazione e utilizzare una cartella distinta per ogni importazione dei punti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="a42fc-151">Passaggio 6: Selezionare un data warehouse</span><span class="sxs-lookup"><span data-stu-id="a42fc-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="a42fc-152">È quindi necessario selezionare un online [Azure SQL Data Warehouse](http://aka.ms/sqldw) dati hello tooimport nel database.</span><span class="sxs-lookup"><span data-stu-id="a42fc-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="a42fc-153">Dopo aver selezionato il database, è necessario tooenter hello credenziali tooconnect toohello del database e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a42fc-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="a42fc-154">DP unisce le tabelle di dati di origine hello in data warehouse di hello.</span><span class="sxs-lookup"><span data-stu-id="a42fc-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="a42fc-155">DP Avvisa se il nome di tabella hello richiede toooverwrite esistenti nelle tabelle hello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="a42fc-156">È possibile eliminare tutti gli oggetti esistenti nel data warehouse di hello tracciando Elimina tutti gli oggetti esistenti prima dell'importazione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="a42fc-157">Passaggio 7: Importare dati hello</span><span class="sxs-lookup"><span data-stu-id="a42fc-157">Step 7: Import hello data</span></span>
<span data-ttu-id="a42fc-158">DP conferma che si desidera dati hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="a42fc-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="a42fc-159">Fare clic su hello inizio pulsante toobegin hello dati importazione.</span><span class="sxs-lookup"><span data-stu-id="a42fc-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="a42fc-160">Dei punti di distribuzione consente di visualizzare una visualizzazione che mostra lo stato di avanzamento hello di estrazione e caricamento di dati hello dal hello locale di SQL Server e hello lo stato di avanzamento dell'importazione di hello in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a42fc-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="a42fc-161">Una volta completata l'importazione di hello, dei punti di distribuzione consente di visualizzare un riepilogo di importazione dei dati hello e un report delle modifiche di correzioni hello che sono state eseguite.</span><span class="sxs-lookup"><span data-stu-id="a42fc-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="a42fc-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a42fc-162">Next steps</span></span>
<span data-ttu-id="a42fc-163">tooexplore i dati all'interno di SQL Data Warehouse, avviare la visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="a42fc-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="a42fc-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)] (Eseguire query in Azure SQL Data Warehouse (Visual Studio))</span><span class="sxs-lookup"><span data-stu-id="a42fc-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="a42fc-165">[Visualizzare i dati con Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="a42fc-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="a42fc-166">altre informazioni sulle dati piattaforma Studio del Redgate toolearn:</span><span class="sxs-lookup"><span data-stu-id="a42fc-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="a42fc-167">Visitare la home page dei punti di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="a42fc-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="a42fc-168">Guardare una demo di DPS su Channel9</span><span class="sxs-lookup"><span data-stu-id="a42fc-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="a42fc-169">Per una panoramica di altri modi toomigrate e caricare i dati in SQL Data Warehouse vedere:</span><span class="sxs-lookup"><span data-stu-id="a42fc-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="a42fc-170">[Eseguire la migrazione del Data Warehouse di tooSQL soluzione][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="a42fc-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="a42fc-171">Caricare i dati in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a42fc-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="a42fc-172">Per ulteriori suggerimenti per lo sviluppo, vedere hello [Cenni preliminari sullo sviluppo di SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="a42fc-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
