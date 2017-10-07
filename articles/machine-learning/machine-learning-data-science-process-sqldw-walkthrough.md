---
title: 'Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse | Documenti Microsoft'
description: Advanced Analytics Process and Technology in azione
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="e1ca4-103">Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="e1ca4-104">In questa esercitazione si illustrano la compilazione e distribuzione di un modello di machine learning usando SQL Data Warehouse (SQL Data Warehouse) per un set di dati disponibile pubblicamente, hello [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="e1ca4-105">modello di classificazione binaria Hello costruito stima o meno un suggerimento viene pagato per un di andata e ritorno e modelli per la classificazione multiclasse e regressione vengono anche illustrati in che consentono di stimare distribuzione hello per quantità suggerimento hello a pagamento.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="e1ca4-106">procedura Hello segue hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="e1ca4-107">Viene illustrato come toosetup un ambiente di analisi scientifica dei dati, come tooload hello dati nel data Warehouse di SQL e come usare data Warehouse SQL o un IPython Notebook tooexplore hello dati e tecnico funzionalità toomodel.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="e1ca4-108">È quindi possibile visualizzare come toobuild e distribuire un modello con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="e1ca4-109"><a name="dataset"></a>set di dati NYC Taxi trip Hello</span><span class="sxs-lookup"><span data-stu-id="e1ca4-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="e1ca4-110">dati di andata e ritorno Taxi NYC Hello è costituita da circa 20GB di file CSV compressi (~ 48GB non compressi), registrazione 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="e1ca4-111">Ogni record di andata e ritorno include percorsi di ritiro e deposito hello e volte, resi anonimi hack numero di patente) (e hello numero medallion (id univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e1ca4-112">dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="e1ca4-113">Hello **trip_data.csv** file contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata di andata e ritorno e lunghezza di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e1ca4-114">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="e1ca4-115">Hello **trip_fare.csv** file contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="e1ca4-116">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e1ca4-117">Hello **chiave univoca** utilizzato viaggi toojoin\_dati e andata e ritorno\_tariffa è composta da hello e tre i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="e1ca4-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="e1ca4-118">medallion,</span></span>
* <span data-ttu-id="e1ca4-119">hack\_license e</span><span class="sxs-lookup"><span data-stu-id="e1ca4-119">hack\_license and</span></span>
* <span data-ttu-id="e1ca4-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-120">pickup\_datetime.</span></span>

## <span data-ttu-id="e1ca4-121"><a name="mltasks"></a>Risolvere tre tipi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="e1ca4-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="e1ca4-122">Abbiamo formulare tre problemi di stima in base a hello *suggerimento\_quantità* tooillustrate tre tipi di modellazione di attività:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="e1ca4-123">**Classificazione binaria**: toopredict o meno un suggerimento è stato pagato un andata e ritorno, vale a dire un *suggerimento\_quantità* che è maggiore di $0 è un esempio positivo, mentre un *suggerimento\_quantità* $ 0 è riportato un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="e1ca4-124">**Classificazione multiclasse**: intervallo di hello toopredict del suggerimento pagato viaggi hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="e1ca4-125">Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="e1ca4-126">**Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="e1ca4-127"><a name="setup"></a>Configurare un ambiente di analisi scientifica dei dati di Azure hello per analitica avanzate</span><span class="sxs-lookup"><span data-stu-id="e1ca4-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="e1ca4-128">tooset dell'ambiente di analisi scientifica dei dati di Azure, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="e1ca4-129">**Creare l'account di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="e1ca4-130">Quando si esegue il provisioning manualmente l'archiviazione blob di Azure, scegliere una posizione geografica per l'archiviazione blob di Azure in ingresso o in più vicino possibile troppo**centro-meridionali**, ovvero in cui è archiviato i dati NYC Taxi hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="e1ca4-131">verranno copiati i dati Hello utilizzando lo strumento AzCopy dalla tooa di contenitore di hello blob pubblici archiviazione nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="e1ca4-132">Hello più vicino di archiviazione blob di Azure è tooSouth Central US, hello più veloce (passaggio 4) questa attività verrà completata.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="e1ca4-133">toocreate account manualmente l'archiviazione di Azure, hello seguire i passaggi descritti in [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e1ca4-134">Essere note toomake che sui valori hello per le seguenti credenziali di account di archiviazione saranno necessari più avanti in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="e1ca4-135">**Storage Account Name**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="e1ca4-136">**Chiave dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="e1ca4-137">**Nome del contenitore** (che si desidera hello toobe di dati archiviati in hello archiviazione blob di Azure)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="e1ca4-138">**Effettuare il provisioning dell'istanza di Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="e1ca4-139">Seguire la documentazione di hello in [creare un Data Warehouse SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision un'istanza di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="e1ca4-140">Verificare che sia possibile effettuare le notazioni su hello seguendo le credenziali di SQL Data Warehouse che verranno usate nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="e1ca4-141">**Nome server**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="e1ca4-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="e1ca4-142">**Nome SQLDW (database)**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="e1ca4-143">**Nome utente**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-143">**Username**</span></span>
* <span data-ttu-id="e1ca4-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-144">**Password**</span></span>

<span data-ttu-id="e1ca4-145">**Installare Visual Studio e SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="e1ca4-146">Per istruzioni, vedere [Installare Visual Studio 2015 e SSDT per SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="e1ca4-147">**Connettere tooyour data Warehouse di SQL Azure con Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="e1ca4-148">Per istruzioni, vedere i passaggi 1 e 2 in [connettersi tooAzure SQL Data Warehouse con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-149">Esecuzione hello seguente query SQL sul database hello è stato creato in SQL Data Warehouse (connessione argomento, anziché hello query fornito nel passaggio 3 di hello) troppo**creare una chiave master**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="e1ca4-150">**Creare un'area di lavoro di Azure Machine Learning nella sottoscrizione di Azure.**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="e1ca4-151">Per istruzioni, vedere [Creare un'area di lavoro di Machine Learning di Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="e1ca4-152"><a name="getdata"></a>Caricare i dati di hello in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="e1ca4-153">Aprire una console dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="e1ca4-154">Eseguire il seguente hello comandi PowerShell toodownload hello SQL file script di esempio che si condividono con l'utente in GitHub tooa locale nella directory specificata con il parametro hello *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="e1ca4-155">È possibile modificare il valore di hello del parametro *- DestDir* tooany directory locale.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="e1ca4-156">Se *- DestDir* non esiste, verrà creata da hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-157">Potrebbe essere troppo**Esegui come amministratore** quando si esegue lo script di PowerShell seguente, se hello il *DestDir* directory deve tooit toocreate o toowrite con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="e1ca4-158">Dopo la corretta esecuzione, la directory di lavoro corrente cambia troppo*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="e1ca4-159">Dovrebbe essere possibile toosee schermo come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="e1ca4-160">Nel *- DestDir*, eseguire lo script di PowerShell in modalità amministratore seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="e1ca4-161">Quando uno script di PowerShell hello viene eseguito per hello prima volta, viene chiesto informazioni hello tooinput del data Warehouse SQL Azure e l'account di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="e1ca4-162">Al termine di questo script di PowerShell in esecuzione per hello prima volta, le credenziali di hello input si verrà sia stato scritto il file di configurazione tooa SQLDW.conf nella directory di lavoro presenti hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="e1ca4-163">Hello future di questo file di script di PowerShell ha hello opzione tooread necessari tutti i parametri da questo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="e1ca4-164">Se è necessario toochange alcuni parametri, è possibile scegliere tooinput parametri hello nella schermata di hello al prompt dei comandi per l'eliminazione di questo file di configurazione e l'immissione di valori dei parametri hello come richiesto o valori di parametro hello toochange modificando hello SQLDW.conf file nel *- DestDir* directory.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-165">In ordine tooavoid schema nome in conflitto con quelli già esistenti del data Warehouse SQL Azure, durante la lettura dei parametri direttamente dal file SQLDW.conf hello, un numero casuale di 3 cifre viene aggiunto il nome di schema toohello dal file SQLDW.conf hello come nome dello schema predefinito di hello per ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="e1ca4-166">script di PowerShell Hello può richiedere un nome di schema: è possibile specificare il nome di hello a discrezione di utente.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="e1ca4-167">Questo **script di PowerShell** file completa hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="e1ca4-168">**Esegue il download e l'installazione di AzCopy**, se non è già installato</span><span class="sxs-lookup"><span data-stu-id="e1ca4-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="e1ca4-169">**Copia di account di archiviazione blob privato tooyour dati** dal blob pubblici di hello con AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1ca4-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="e1ca4-170">**Carica dati tramite Polybase (eseguendo LoadDataToSQLDW.sql) tooyour Azure SQL DW** dall'account di archiviazione blob privato con hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="e1ca4-171">Creare uno schema</span><span class="sxs-lookup"><span data-stu-id="e1ca4-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="e1ca4-172">Creare una credenziale con ambito di database</span><span class="sxs-lookup"><span data-stu-id="e1ca4-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="e1ca4-173">Creare un'origine dati esterna per un BLOB di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e1ca4-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="e1ca4-174">Creare un formato di file esterno da un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="e1ca4-175">Dati non compressi e campi sono separati dal carattere barra verticale hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="e1ca4-176">Creare tabelle esterne relative a tariffe e corse per il set di dati relativo alle corse dei taxi di New York nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="e1ca4-177">Caricare i dati da tabelle esterne in tooSQL di archiviazione blob di Azure Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="e1ca4-178">Creare una tabella di dati di esempio (NYCTaxi_Sample) e inserire dati tooit dalla selezione delle query SQL sulle tabelle di andata e ritorno e tariffa hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="e1ca4-179">(Alcuni passaggi di questa procedura dettagliata è necessario toouse questa tabella di esempio.)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="e1ca4-180">posizione geografica di Hello degli account di archiviazione influisce sui tempi di caricamento.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-181">A seconda della posizione geografica di hello dell'account di archiviazione blob privato, hello processo di copia dei dati da un account di archiviazione privato tooyour blob pubblico può saranno necessari circa 15 minuti o anche più e hello processo di caricamento dei dati dall'account di archiviazione Azure SQL DW tooyour può richiedere 20 minuti o più.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="e1ca4-182">Sarà necessario toodecide cosa fare se si dispone di origine e i file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-183">Se toobe di file con estensione csv hello copiati dall'account di archiviazione blob privato tooyour archiviazione blob pubblici hello già esiste nell'account di archiviazione blob privato, AzCopy verrà chiesto se si desidera toooverwrite li.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="e1ca4-184">Se non si desidera toooverwrite così input  **n**  quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="e1ca4-185">Se si desidera toooverwrite **tutti** di essi, di input **un** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="e1ca4-186">È anche possibile immettere **y** toooverwrite CSV file singolarmente.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Grafico n. 21][21]

<span data-ttu-id="e1ca4-188">È possibile usare i propri dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-188">You can use your own data.</span></span> <span data-ttu-id="e1ca4-189">Se i dati sono nel computer locale in un'applicazione reale, è comunque possibile usare AzCopy tooupload locale dati tooyour privata di archiviazione blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="e1ca4-190">È necessario solo hello toochange **origine** posizione, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy comando hello PowerShell script toohello locale della directory del file che contiene i dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="e1ca4-191">Se i dati sono già nell'archiviazione blob di Azure privato dell'applicazione di uno scenario reale, è possibile ignorare hello AzCopy passaggio hello script di PowerShell e caricare direttamente hello dati tooAzure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="e1ca4-192">Questo richiederà ulteriori la modifica di hello script tootailor toohello formato dei dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="e1ca4-193">Questo script di Powershell anche inserisce informazioni di Azure SQL DW in hello dati l'esplorazione dei file di esempio SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py hello in modo che questi tre file siano pronti toobe provato immediatamente al termine dell'esecuzione hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="e1ca4-194">Al termine dell'esecuzione, verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="e1ca4-195"><a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e1ca4-196">In questa sezione vengono effettuate l'esplorazione dei dati e la generazione di funzionalità eseguendo query SQL direttamente su Azure SQL DW usando **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="e1ca4-197">Tutte le query SQL utilizzate in questa sezione sono disponibili nello script di esempio hello denominato *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="e1ca4-198">Questo file è già stato scaricato tooyour directory locale dallo script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="e1ca4-199">È anche possibile recuperarlo da [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql),</span><span class="sxs-lookup"><span data-stu-id="e1ca4-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="e1ca4-200">Ma il file hello in GitHub non dispone di informazioni di Azure SQL DW hello collegate.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="e1ca4-201">Connettersi con Visual Studio con il nome di accesso SQL DW hello e una password di Azure SQL DW tooyour e aprire hello **Esplora oggetti di SQL** tooconfirm hello database e le tabelle sono state importate.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="e1ca4-202">Recuperare hello *SQLDW_Explorations.sql* file.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ca4-203">tooopen un editor di query Parallel Data Warehouse (PDW), utilizzare hello **nuova Query** comando mentre è selezionato il PDW in hello **Esplora oggetti di SQL**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="e1ca4-204">editor di query SQL standard Hello non è supportato da PDW.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="e1ca4-205">Di seguito sono di tipo hello di dati eseguite attività di generazione di esplorazione e funzionalità in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="e1ca4-206">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="e1ca4-207">Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="e1ca4-208">Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="e1ca4-209">Generazione di funzionalità calcolo/confronto delle distanze delle corse.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="e1ca4-210">Join di tabelle hello due ed estrarre un campione casuale che verrà utilizzato toobuild modelli.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="e1ca4-211">Verifica dell'importazione dei dati</span><span class="sxs-lookup"><span data-stu-id="e1ca4-211">Data import verification</span></span>
<span data-ttu-id="e1ca4-212">Queste query offrono una rapida verifica del numero di hello di righe e colonne in tabelle compilate in precedenza mediante bulk parallela del Polybase importano, hello</span><span class="sxs-lookup"><span data-stu-id="e1ca4-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="e1ca4-213">**Output:** si dovrebbero ottenere 173.179.759 righe e 14 colonne.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="e1ca4-214">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e1ca4-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="e1ca4-215">Questo esempio di query identifica medallions hello (numeri taxi) completata più di 100 trip all'interno di un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="e1ca4-216">query Hello può costituire un vantaggio accesso alle tabelle partizionata hello poiché condizionato, dallo schema di partizione hello di **prelievo\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="e1ca4-217">Una query di set di dati completo hello renderà inoltre usare della tabella partizionata hello e/o l'analisi di indice.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="e1ca4-218">**Output:** query hello deve restituire una tabella con righe specificando medallions hello 13,369 (taxi) e numero di andata e ritorno completata da essi in 2013 hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="e1ca4-219">Hello ultima colonna contiene il conteggio di hello del numero di hello di viaggi completata.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="e1ca4-220">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="e1ca4-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="e1ca4-221">In questo esempio identifica medallions hello (numeri taxi) e hack_license numeri (driver) che è stata completata più di 100 trip all'interno di un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="e1ca4-222">**Output:** query hello devono restituire una tabella con 13,369 righe specificando hello 13,369 Auto/driver ID completate più di 100 trip nel 2013.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="e1ca4-223">Hello ultima colonna contiene il conteggio di hello del numero di hello di viaggi completata.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="e1ca4-224">Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate</span><span class="sxs-lookup"><span data-stu-id="e1ca4-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="e1ca4-225">In questo esempio consente di esaminare se i campi di longitudine e/o latitudine hello contenere un valore non valido (gradi in radianti devono essere compreso tra -90 e 90,) o (0, 0) le coordinate.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="e1ca4-226">**Output:** query hello restituisce 837,467 trip contenenti campi non validi di longitudine e/o latitudine.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="e1ca4-227">Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="e1ca4-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="e1ca4-228">In questo esempio trova il numero di hello di viaggi che sono stati inclinato rispetto al numero di hello che non sono stati inclinato in un periodo di tempo specificato (o in hello set di dati completo se per l'anno completo hello come è configurato in questo caso).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="e1ca4-229">Questa distribuzione riflette hello binario etichetta distribuzione toobe utilizzato successivamente per la modellazione di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="e1ca4-230">**Output:** hello query deve seguente hello restituito suggerimento le frequenze per anno hello inclinato 2013: 90,447,622 e 82,264,709 inclinato non.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="e1ca4-231">Esplorazione: distribuzione della classe o dell'intervallo delle mance</span><span class="sxs-lookup"><span data-stu-id="e1ca4-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="e1ca4-232">Questo esempio calcola la distribuzione di hello degli intervalli di comandi in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="e1ca4-233">Si tratta di distribuzione hello di classi di etichetta hello che verrà usato successivamente per la modellazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="e1ca4-234">**Output:**</span><span class="sxs-lookup"><span data-stu-id="e1ca4-234">**Output:**</span></span>

| <span data-ttu-id="e1ca4-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="e1ca4-235">tip_class</span></span> | <span data-ttu-id="e1ca4-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="e1ca4-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="e1ca4-237">1</span><span class="sxs-lookup"><span data-stu-id="e1ca4-237">1</span></span> |<span data-ttu-id="e1ca4-238">82230915</span><span class="sxs-lookup"><span data-stu-id="e1ca4-238">82230915</span></span> |
| <span data-ttu-id="e1ca4-239">2</span><span class="sxs-lookup"><span data-stu-id="e1ca4-239">2</span></span> |<span data-ttu-id="e1ca4-240">6198803</span><span class="sxs-lookup"><span data-stu-id="e1ca4-240">6198803</span></span> |
| <span data-ttu-id="e1ca4-241">3</span><span class="sxs-lookup"><span data-stu-id="e1ca4-241">3</span></span> |<span data-ttu-id="e1ca4-242">1932223</span><span class="sxs-lookup"><span data-stu-id="e1ca4-242">1932223</span></span> |
| <span data-ttu-id="e1ca4-243">0</span><span class="sxs-lookup"><span data-stu-id="e1ca4-243">0</span></span> |<span data-ttu-id="e1ca4-244">82264625</span><span class="sxs-lookup"><span data-stu-id="e1ca4-244">82264625</span></span> |
| <span data-ttu-id="e1ca4-245">4</span><span class="sxs-lookup"><span data-stu-id="e1ca4-245">4</span></span> |<span data-ttu-id="e1ca4-246">85765</span><span class="sxs-lookup"><span data-stu-id="e1ca4-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="e1ca4-247">Esplorazione: calcolo e confronto della distanza delle corse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="e1ca4-248">In questo esempio converte la longitudine di ritiro e deposito hello e geography tooSQL latitudine punta, distanza di andata e ritorno hello utilizzando SQL geography punti differenza calcola e restituisce un campione casuale di risultati hello per il confronto.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="e1ca4-249">esempio Hello limita i risultati di hello toovalid coordinate solo tramite query valutazione della qualità dei dati hello descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="e1ca4-250">Progettazione di funzionalità con le funzioni SQL</span><span class="sxs-lookup"><span data-stu-id="e1ca4-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="e1ca4-251">Le funzioni SQL a volte possono essere una valida opzione per progettare funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="e1ca4-252">In questa procedura dettagliata, è stato definito una SQL funzione toocalculate hello distanza diretta tra i percorsi di ritiro e dropoff hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="e1ca4-253">È possibile eseguire script SQL in seguito hello **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="e1ca4-254">Di seguito è riportato uno script SQL hello che definisce la funzione di distanza hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="e1ca4-255">Ecco un esempio toocall questa funzionalità toogenerate funzione nella query SQL:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="e1ca4-256">**Output:** questa query genera una tabella (con 2,803,538 righe) con Latitude prelievo e dropoff e longitudine e hello corrispondente diretti chilometri.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="e1ca4-257">Di seguito sono risultati hello per primi 3 righe:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="e1ca4-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="e1ca4-258">pickup_latitude</span></span> | <span data-ttu-id="e1ca4-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="e1ca4-259">pickup_longitude</span></span> | <span data-ttu-id="e1ca4-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="e1ca4-260">dropoff_latitude</span></span> | <span data-ttu-id="e1ca4-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="e1ca4-261">dropoff_longitude</span></span> | <span data-ttu-id="e1ca4-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="e1ca4-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e1ca4-263">1</span><span class="sxs-lookup"><span data-stu-id="e1ca4-263">1</span></span> |<span data-ttu-id="e1ca4-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="e1ca4-264">40.731804</span></span> |<span data-ttu-id="e1ca4-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="e1ca4-265">-74.001083</span></span> |<span data-ttu-id="e1ca4-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="e1ca4-266">40.736622</span></span> |<span data-ttu-id="e1ca4-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="e1ca4-267">-73.988953</span></span> |<span data-ttu-id="e1ca4-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="e1ca4-268">.7169601222</span></span> |
| <span data-ttu-id="e1ca4-269">2</span><span class="sxs-lookup"><span data-stu-id="e1ca4-269">2</span></span> |<span data-ttu-id="e1ca4-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="e1ca4-270">40.715794</span></span> |<span data-ttu-id="e1ca4-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="e1ca4-271">-74,010635</span></span> |<span data-ttu-id="e1ca4-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="e1ca4-272">40.725338</span></span> |<span data-ttu-id="e1ca4-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="e1ca4-273">-74.00399</span></span> |<span data-ttu-id="e1ca4-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="e1ca4-274">.7448343721</span></span> |
| <span data-ttu-id="e1ca4-275">3</span><span class="sxs-lookup"><span data-stu-id="e1ca4-275">3</span></span> |<span data-ttu-id="e1ca4-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="e1ca4-276">40.761456</span></span> |<span data-ttu-id="e1ca4-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="e1ca4-277">-73.999886</span></span> |<span data-ttu-id="e1ca4-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="e1ca4-278">40.766544</span></span> |<span data-ttu-id="e1ca4-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="e1ca4-279">-73.988228</span></span> |<span data-ttu-id="e1ca4-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="e1ca4-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="e1ca4-281">Preparazione dei dati per la creazione del modello</span><span class="sxs-lookup"><span data-stu-id="e1ca4-281">Prepare data for model building</span></span>
<span data-ttu-id="e1ca4-282">hello join di query seguente di Hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa** tabelle, genera un'etichetta di classificazione binaria **inclinato**, etichetta di classificazione multiclasse **suggerimento\_classe**ed estrae un esempio di hello completo aggiunti a un set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="e1ca4-283">campionamento Hello avviene mediante il recupero di un subset di trip hello in base al tempo di prelievo.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="e1ca4-284">Questa query può essere copiata successivamente incollata direttamente in hello [Azure Machine Learning Studio](https://studio.azureml.net) [l'importazione dei dati] [ import-data] modulo per l'inserimento di dati direttamente dall'istanza di database SQL di hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="e1ca4-285">query Hello esclude i record con errato (0, 0) le coordinate.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="e1ca4-286">Quando si è pronti tooproceed tooAzure Machine Learning, è possibile:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="e1ca4-287">Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, o</span><span class="sxs-lookup"><span data-stu-id="e1ca4-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="e1ca4-288">Mantenere hello campionato e dati decodificati Prevedi toouse per modello di compilazione in un nuovo data Warehouse di SQL tabella e usare nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="e1ca4-289">Hello script di PowerShell nel passaggio precedente ha eseguito questa operazione per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="e1ca4-290">È possibile leggere direttamente dalla tabella nel modulo di importazione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="e1ca4-291"><a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e1ca4-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="e1ca4-292">In questa sezione, si eseguirà l'esplorazione dei dati e la generazione di funzionalità mediante entrambi Python e query SQL su SQL DW hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="e1ca4-293">IPython notebook esempio denominato **SQLDW_Explorations.ipynb** e un file di script Python **SQLDW_Explorations_Scripts.py** sono stati scaricati tooyour directory locale.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="e1ca4-294">Sono disponibili anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="e1ca4-295">Questi due file sono identici negli script di Python.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="e1ca4-296">file di script Python Hello viene fornito tooyou nel caso in cui non è un server di IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="e1ca4-297">Questi due file di Python di esempio sono stati progettati in **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="e1ca4-298">le informazioni di Azure SQL DW: esempio hello IPython Notebook Hello e hello Python macchina locale scaricato tooyour file di script è stato collegato dallo script di PowerShell hello in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="e1ca4-299">Possono essere eseguiti senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-299">They are executable without any modification.</span></span>

<span data-ttu-id="e1ca4-300">Se un'area di lavoro di Azure ml è già stato configurato, è possibile caricare l'esempio hello del servizio di Azure ml IPython Notebook toohello IPython Notebook direttamente e avviarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="e1ca4-301">Di seguito sono hello passaggi tooupload tooAzureML servizio IPython Notebook:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="e1ca4-302">Nell'area di lavoro Azure ml tooyour di log, fare clic su "Studio" nella parte superiore di hello e fare clic su "Notebook" sul lato sinistro di hello della pagina web hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Grafico n. 22][22]
2. <span data-ttu-id="e1ca4-304">Fare clic su "Nuovo" nell'angolo inferiore sinistro hello della pagina web hello e selezionare "Python 2".</span><span class="sxs-lookup"><span data-stu-id="e1ca4-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="e1ca4-305">Fornire un notebook toohello nome, quindi fare clic su hello segno di spunta toocreate hello vuoto nuovo IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Grafico n. 23][23]
3. <span data-ttu-id="e1ca4-307">Fare clic sul simbolo "Jupyter" hello nell'angolo superiore sinistro di hello di hello nuovo IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Grafico n. 24][24]
4. <span data-ttu-id="e1ca4-309">Trascinare e rilasciare hello esempio IPython Notebook toohello **albero** pagina dei servizi di Azure ml IPython Notebook, fare clic su **caricare**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="e1ca4-310">Quindi, l'esempio hello IPython Notebook sarà toohello caricato il servizio di Azure ml IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Grafico n. 25][25]

<span data-ttu-id="e1ca4-312">In hello toorun ordine esempio IPython Notebook o file di script Python hello, hello pacchetti Python seguenti sono necessari.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="e1ca4-313">Se si utilizza il servizio di Azure ml IPython Notebook hello, questi pacchetti sono stati già installati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="e1ca4-314">pandas</span><span class="sxs-lookup"><span data-stu-id="e1ca4-314">pandas</span></span>
    - <span data-ttu-id="e1ca4-315">numpy</span><span class="sxs-lookup"><span data-stu-id="e1ca4-315">numpy</span></span>
    - <span data-ttu-id="e1ca4-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="e1ca4-316">matplotlib</span></span>
    - <span data-ttu-id="e1ca4-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="e1ca4-317">pyodbc</span></span>
    - <span data-ttu-id="e1ca4-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="e1ca4-318">PyTables</span></span>

<span data-ttu-id="e1ca4-319">Hello sequenza consigliata durante la compilazione di soluzioni di analisi avanzate in Azure ml con dati di grandi dimensioni può essere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="e1ca4-320">Lettura in un piccolo esempio dei dati hello in un frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="e1ca4-321">Eseguire alcune visualizzazioni e delle esplorazioni utilizzando hello dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="e1ca4-322">Provare varie combinazioni di progettazione di funzionalità mediante hello dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="e1ca4-323">Per l'esplorazione dei dati più grande, la modifica dei dati e progettazione di funzionalità, utilizzare Python tooissue query SQL direttamente hello SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="e1ca4-324">Decidere per l'esempio hello dimensioni toobe adatto per la compilazione del modello di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="e1ca4-325">Hello seguito sono riportati alcuni l'esplorazione dei dati, visualizzazione dei dati ed esempi di progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="e1ca4-326">Sono disponibili ulteriori analisi di dati: esempio hello IPython Notebook e file di script Python di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="e1ca4-327">Inizializzare le credenziali di database</span><span class="sxs-lookup"><span data-stu-id="e1ca4-327">Initialize database credentials</span></span>
<span data-ttu-id="e1ca4-328">Inizializzare le impostazioni di connessione di database in hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="e1ca4-329">Creare la connessione al database</span><span class="sxs-lookup"><span data-stu-id="e1ca4-329">Create database connection</span></span>
<span data-ttu-id="e1ca4-330">Di seguito è stringa di connessione hello crea hello connessione toohello database.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="e1ca4-331">Segnalare il numero di righe e di colonne nella tabella <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="e1ca4-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="e1ca4-332">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="e1ca4-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="e1ca4-333">Numero di colonne totali = 14</span><span class="sxs-lookup"><span data-stu-id="e1ca4-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="e1ca4-334">Segnalare il numero di righe e di colonne nella tabella <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="e1ca4-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="e1ca4-335">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="e1ca4-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="e1ca4-336">Numero di colonne totali = 11</span><span class="sxs-lookup"><span data-stu-id="e1ca4-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="e1ca4-337">Lettura in un campione di dati di dimensioni ridotte da hello Database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="e1ca4-338">Tabella di esempio hello tooread ora è 14.096495 secondi.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="e1ca4-339">Numero di righe e di colonne recuperate = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="e1ca4-340">Statistiche descrittive</span><span class="sxs-lookup"><span data-stu-id="e1ca4-340">Descriptive statistics</span></span>
<span data-ttu-id="e1ca4-341">A questo punto è dati campionato hello tooexplore pronto.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="e1ca4-342">Iniziamo con esaminano alcune statistiche descrittive per hello **viaggi\_distanza** (o qualsiasi altro campo scelto toospecify).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="e1ca4-343">Visualizzazione: esempio di box plot</span><span class="sxs-lookup"><span data-stu-id="e1ca4-343">Visualization: Box plot example</span></span>
<span data-ttu-id="e1ca4-344">Successivamente vengono analizzati grafico box plot di hello per hello viaggi distanza toovisualize hello quantili.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="e1ca4-346">Visualizzazione: esempio di tracciato di distribuzione</span><span class="sxs-lookup"><span data-stu-id="e1ca4-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="e1ca4-347">Grafici che visualizzano distribuzione hello e un istogramma per hello campionate distanze di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="e1ca4-349">Visualizzazione: tracciati a barre e linee</span><span class="sxs-lookup"><span data-stu-id="e1ca4-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="e1ca4-350">In questo esempio è bin distanza di andata e ritorno hello in cinque bin e visualizzare i risultati di binning hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="e1ca4-351">È possibile tracciare hello sopra distribuzione bin in una barra o riga del tracciato con:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

<span data-ttu-id="e1ca4-353">e</span><span class="sxs-lookup"><span data-stu-id="e1ca4-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="e1ca4-355">Visualizzazione: esempi di grafico a dispersione</span><span class="sxs-lookup"><span data-stu-id="e1ca4-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="e1ca4-356">Viene illustrata la dispersione tra **viaggi\_ora\_in\_sec** e **viaggi\_distanza** toosee nel caso di qualsiasi correlazione</span><span class="sxs-lookup"><span data-stu-id="e1ca4-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

<span data-ttu-id="e1ca4-358">Analogamente è possibile controllare la relazione hello tra **frequenza\_codice** e **viaggi\_distanza**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="e1ca4-360">Esplorazione nei dati campionati usando query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e1ca4-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="e1ca4-361">In questa sezione vengono analizzate le distribuzioni dei dati utilizzando i dati campionato hello che viene mantenuti nella nuova tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="e1ca4-362">Si noti che esplorazioni simile possono essere eseguite mediante tabelle originali hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="e1ca4-363">Esplorazione: Numero di righe e colonne in hello campionate tabella</span><span class="sxs-lookup"><span data-stu-id="e1ca4-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="e1ca4-364">Esplorazione: distribuzione delle corse per cui è stata lasciata una mancia e di quelle per cui non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="e1ca4-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="e1ca4-365">Esplorazione: distribuzione della classe delle mance</span><span class="sxs-lookup"><span data-stu-id="e1ca4-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="e1ca4-366">Esplorazione: Tracciare distribuzione suggerimento hello dalla classe</span><span class="sxs-lookup"><span data-stu-id="e1ca4-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Grafico n. 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="e1ca4-368">Esplorazione: distribuzione giornaliera delle corse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="e1ca4-369">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e1ca4-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="e1ca4-370">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="e1ca4-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="e1ca4-371">Esplorazione: distribuzione degli orari delle corse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="e1ca4-372">Esplorazione: distribuzione delle distanze delle corse</span><span class="sxs-lookup"><span data-stu-id="e1ca4-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="e1ca4-373">Esplorazione: distribuzione dei tipi di pagamento</span><span class="sxs-lookup"><span data-stu-id="e1ca4-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="e1ca4-374">Verificare il modulo di finale hello della tabella trasformato hello</span><span class="sxs-lookup"><span data-stu-id="e1ca4-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="e1ca4-375"><a name="mlmodel"></a>Creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e1ca4-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="e1ca4-376">Sono ora pronti tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="e1ca4-377">dati Hello sono pronto toobe utilizzata in uno qualsiasi dei problemi di stima hello identificati in precedenza, vale a dire:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="e1ca4-378">**Classificazione binaria**: toopredict o meno un suggerimento è stato pagato per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="e1ca4-379">**Classificazione multiclasse**: intervallo di hello toopredict del suggerimento a pagamento, in base a toohello classi definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="e1ca4-380">**Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="e1ca4-381">toobegin hello esercizio di modellazione, accedi tooyour **Azure Machine Learning** dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="e1ca4-382">Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure ML](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="e1ca4-383">tooget avviato con Azure Machine Learning, vedere [che cos'è Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="e1ca4-384">Accedi troppo[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="e1ca4-385">pagina iniziale di Studio Hello un'ampia gamma di informazioni, video, esercitazioni, collegamenti toohello riferimento moduli e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="e1ca4-386">Per ulteriori informazioni su Azure Machine Learning, consultare hello [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="e1ca4-387">Un esperimento di training tipica è costituita da hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="e1ca4-388">Creazione di un esperimento **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="e1ca4-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="e1ca4-389">Ottenere dati di hello in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="e1ca4-390">Pre-elaborazione, trasformare e modificare i dati di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="e1ca4-391">Generazione di funzionalità, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-391">Generate features as needed.</span></span>
5. <span data-ttu-id="e1ca4-392">Suddividere i dati di hello in set di dati di training e la convalida o il test (o set di dati separati per ogni).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="e1ca4-393">Selezionare uno o più algoritmi di machine learning a seconda di hello toosolve problema di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="e1ca4-394">Ad esempio, classificazione binaria, classificazione multiclasse, regressione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="e1ca4-395">Eseguire il training di uno o più modelli utilizzando hello training set.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="e1ca4-396">Assegnare un punteggio hello convalida set di dati utilizzando modelli con training hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="e1ca4-397">Valutare hello modelli toocompute hello le metriche pertinenti per l'apprendimento problema hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="e1ca4-398">Ottimizzare i modelli di hello e selezionare hello migliore modello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="e1ca4-399">In questo esercizio, abbiamo già esplorato e decodificati dati hello in SQL Data Warehouse e deciso tooingest dimensioni di esempio hello in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="e1ca4-400">Ecco hello procedure toobuild uno o più modelli di previsione hello:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="e1ca4-401">Ottenere dati hello in Azure ML utilizzando hello [l'importazione dei dati] [ import-data] modulo, disponibile in hello **dati di Input e Output** sezione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="e1ca4-402">Per ulteriori informazioni, vedere hello [l'importazione dei dati] [ import-data] pagina di riferimento modulo.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Import Data di Azure ML][17]
2. <span data-ttu-id="e1ca4-404">Selezionare **Database SQL di Azure** come hello **origine dati** in hello **proprietà** pannello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="e1ca4-405">Immettere nome DNS del database hello in hello **nome server Database** campo.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="e1ca4-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="e1ca4-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="e1ca4-407">Immettere hello **nome del Database** nel campo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="e1ca4-408">Immettere hello *nome utente di SQL* in hello **nome dell'account utente Server**, hello e *password* in hello **password dell'account utente Server**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="e1ca4-409">Controllare hello **accettare qualsiasi certificato server** opzione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="e1ca4-410">In hello **query Database** Modifica area di testo, incollare query hello estrae hello necessario campi (incluse eventuali campi calcolati, ad esempio etichette hello) del database e verso il basso esempi di dimensioni del campione hello dati toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="e1ca4-411">Un esempio di un esperimento di classificazione binaria, la lettura dei dati direttamente dal database di SQL Data Warehouse hello è nella figura che segue hello (ricordare tooreplace hello nomi nyctaxi_trip e nyctaxi_fare dallo schema hello utilizzato nel nome e hello nomi di tabella il procedura dettagliata).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="e1ca4-412">È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formazione su Azure ML][10]

> [!IMPORTANT]
> <span data-ttu-id="e1ca4-414">In hello modellazione estrazione dei dati e il campionamento di esempi di query forniti nelle sezioni precedenti, **tutte le etichette per gli esercizi di modellazione hello tre sono inclusi nella query hello**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="e1ca4-415">Un passaggio importante (obbligatorio) in ogni hello esercizi sulla modellazione è troppo**escludere** hello etichette non necessari per hello altri due problemi e qualsiasi altro **destinazione perdite**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="e1ca4-416">Ad esempio, quando si utilizza una classificazione binaria, utilizzare l'etichetta hello **inclinato** ed escludere i campi di hello **suggerimento\_classe**, **suggerimento\_quantità**, e **totale\_quantità**.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="e1ca4-417">Hello quest'ultimo vengono pagate perdite di destinazione, perché implicano suggerimento hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="e1ca4-418">tooexclude eventuali colonne non necessarie o perdite di destinazione, è possibile utilizzare hello [selezionare le colonne nel set di dati] [ select-columns] modulo o hello [Modifica metadati] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="e1ca4-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="e1ca4-419">Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="e1ca4-420"><a name="mldeploy"></a>Distribuire modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e1ca4-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="e1ca4-421">Quando il modello è pronto, è possibile distribuirlo facilmente come servizio web direttamente da esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="e1ca4-422">Per ulteriori informazioni sulla distribuzione di servizi Web Azure ML, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca4-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="e1ca4-423">toodeploy un nuovo servizio web, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="e1ca4-424">Creare un esperimento di assegnazione di punteggio.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="e1ca4-425">Distribuire il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-425">Deploy hello web service.</span></span>

<span data-ttu-id="e1ca4-426">un punteggio sperimentare da toocreate un **completato** esperimento di training, fare clic su **CREATE SCORING EXPERIMENT** nella barra delle azioni inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Valutazione di Azure][18]

<span data-ttu-id="e1ca4-428">Azure Machine Learning tenterà toocreate un esperimento di assegnazione dei punteggi in base ai componenti di hello dell'esperimento di training hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="e1ca4-429">In particolare, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e1ca4-429">In particular, it will:</span></span>

1. <span data-ttu-id="e1ca4-430">Salva modello con training hello e rimuovere i moduli di training modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="e1ca4-431">Identificare una logica **porta di input** toorepresent hello previsto schema dati di input.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="e1ca4-432">Identificare una logica **porta di output** toorepresent dello schema output di hello web previsto del servizio.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="e1ca4-433">Quando viene creato l'assegnazione dei punteggi esperimento hello, esaminarla e adattare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="e1ca4-434">Un esempio tipico di regolazione sia set di dati tooreplace hello input e/o query con uno che esclude i campi di etichetta, poiché questi non saranno disponibili quando viene chiamato servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="e1ca4-435">È anche una dimensione di hello tooreduce buona norma di hello alcuni record, dello schema di input sufficiente hello tooindicate tooa set di dati e/o query di input.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="e1ca4-436">Per la porta di output di hello, è comune tooexclude campi di tutti gli input e includere solo hello **Scored Labels** e **calcolato il punteggio della probabilità** in hello output utilizzando hello [selezionare le colonne nel set di dati ] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e1ca4-437">Un esempio esperimento di assegnazione dei punteggi viene fornito nella figura hello seguente.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="e1ca4-438">Al termine toodeploy, fare clic su hello **servizio WEB di pubblicare** pulsante nella barra delle azioni inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Pubblicazione di Azure ML][11]

## <a name="summary"></a><span data-ttu-id="e1ca4-440">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e1ca4-440">Summary</span></span>
<span data-ttu-id="e1ca4-441">toorecap cosa che abbiamo realizzato in questa esercitazione di questa procedura dettagliata, è stato creato un ambiente di analisi scientifica dei dati di Azure, ha collaborato con un ampio set di dati pubblici, portarlo tramite hello processo di analisi scientifica dei dati Team, tutte le modalità di hello dal training toomodel acquisizione di dati, quindi toohello distribuzione di un servizio web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="e1ca4-442">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="e1ca4-442">License information</span></span>
<span data-ttu-id="e1ca4-443">In questa procedura dettagliata di esempio e il relativo tipo di accompagnamento notebook(s) IPython e script sono condivisi da Microsoft con licenza MIT hello.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="e1ca4-444">Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.</span><span class="sxs-lookup"><span data-stu-id="e1ca4-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="e1ca4-445">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="e1ca4-445">References</span></span>
<span data-ttu-id="e1ca4-446">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="e1ca4-447">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="e1ca4-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="e1ca4-448">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="e1ca4-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
