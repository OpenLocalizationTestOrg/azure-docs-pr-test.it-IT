---
title: aaaBuild e distribuire un modello di machine learning utilizza SQL Server in una macchina virtuale di Azure | Microsoft documenti
description: Advanced Analytics Process and Technology in azione
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="93f74-103">Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Server</span><span class="sxs-lookup"><span data-stu-id="93f74-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="93f74-104">In questa esercitazione, si scoprirà processo hello della compilazione e distribuzione di un modello di machine learning utilizzando SQL Server e un set di dati disponibile pubblicamente, hello [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati.</span><span class="sxs-lookup"><span data-stu-id="93f74-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="93f74-105">procedura Hello segue un flusso di lavoro di analisi scientifica dei dati standard: inserimento esplorare i dati di hello, progettare learning toofacilitate funzionalità, quindi compilare e distribuire un modello.</span><span class="sxs-lookup"><span data-stu-id="93f74-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="93f74-106"><a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York</span><span class="sxs-lookup"><span data-stu-id="93f74-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="93f74-107">dati di andata e ritorno Taxi NYC Hello è di circa 20GB di file CSV compressi (~ 48GB non compressi), che comprendono 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario.</span><span class="sxs-lookup"><span data-stu-id="93f74-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="93f74-108">Ogni record di andata e ritorno include il percorso di ritiro e deposito hello e l'ora, hack anonimi (driver) il numero di licenza e numero medallion (id univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="93f74-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="93f74-109">dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:</span><span class="sxs-lookup"><span data-stu-id="93f74-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="93f74-110">Hello 'trip_data' CSV contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="93f74-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="93f74-111">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="93f74-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="93f74-112">Hello 'trip_fare' CSV contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato.</span><span class="sxs-lookup"><span data-stu-id="93f74-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="93f74-113">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="93f74-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="93f74-114">viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da campi hello: medallion, le maggiori\_titolo e prelievo\_datetime.</span><span class="sxs-lookup"><span data-stu-id="93f74-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="93f74-115"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="93f74-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="93f74-116">Si verranno formulare tre problemi di stima in base a hello *suggerimento\_quantità*, vale a dire:</span><span class="sxs-lookup"><span data-stu-id="93f74-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="93f74-117">Classificazione binaria: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="93f74-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="93f74-118">Classificazione multiclasse: intervallo di hello toopredict del suggerimento pagato viaggi hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="93f74-119">Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:</span><span class="sxs-lookup"><span data-stu-id="93f74-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="93f74-120">Attività di regressione: quantità di hello toopredict del suggerimento a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="93f74-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="93f74-121"><a name="setup"></a>Impostazione hello Azure data science ambiente per analitica avanzate</span><span class="sxs-lookup"><span data-stu-id="93f74-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="93f74-122">Come si può vedere dal hello [pianificazione dell'ambiente](machine-learning-data-science-plan-your-environment.md) Guida, sono disponibili diverse opzioni toowork con set di dati NYC Taxi trip hello in Azure:</span><span class="sxs-lookup"><span data-stu-id="93f74-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="93f74-123">Utilizzare i dati di hello in BLOB di Azure quindi modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93f74-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="93f74-124">Caricare i dati di hello in un database di SQL Server e il modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93f74-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="93f74-125">In questa esercitazione verrà illustrato l'importazione bulk parallela di hello tooa di dati SQL Server, l'esplorazione dei dati, la funzionalità di progettazione verso il basso campionamento utilizzando SQL Server Management Studio nonché utilizzando IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="93f74-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="93f74-126">Gli [script di esempio](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e i [blocchi di appunti IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) di esempio vengono condivisi in GitHub.</span><span class="sxs-lookup"><span data-stu-id="93f74-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="93f74-127">Un toowork notebook IPython di esempio con i dati di hello in BLOB di Azure è disponibile anche in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="93f74-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="93f74-128">tooset dell'ambiente di analisi scientifica dei dati di Azure:</span><span class="sxs-lookup"><span data-stu-id="93f74-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="93f74-129">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="93f74-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="93f74-130">Creare un'area di lavoro di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="93f74-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="93f74-131">[Eseguire il provisioning di una macchina virtuale Data Science](machine-learning-data-science-setup-sql-server-virtual-machine.md), che fornirà SQL Server e un server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="93f74-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="93f74-132">script di esempio Hello e IPython notebook saranno macchina virtuale di analisi scientifica dei dati scaricati tooyour durante il processo di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="93f74-133">Al termine del processo di script di post-installazione VM hello, esempi di hello sarà nella raccolta documenti di VM:</span><span class="sxs-lookup"><span data-stu-id="93f74-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="93f74-134">Script di esempio: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="93f74-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="93f74-135">Blocchi di appunti di esempio IPython: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="93f74-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="93f74-136">where `<user_name>` è il nome di accesso Windows della VM.</span><span class="sxs-lookup"><span data-stu-id="93f74-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="93f74-137">Si farà riferimento a cartelle di esempio toohello come **gli script di esempio** e **esempio IPython notebook**.</span><span class="sxs-lookup"><span data-stu-id="93f74-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="93f74-138">Basato su dimensioni del set di dati hello, percorso di origine dati e ambiente di destinazione selezionati di Azure hello, questo scenario è simile troppo[Scenario \#5: grandi set di dati in un file locale, SQL Server nella macchina virtuale di Azure di destinazione](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="93f74-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="93f74-139"><a name="getdata"></a>Ottenere hello dati dall'origine pubblico</span><span class="sxs-lookup"><span data-stu-id="93f74-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="93f74-140">hello tooget [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati dal percorso pubblico, è possibile utilizzare uno dei metodi di hello descritto in [tooand spostare dati dall'archiviazione Blob di Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello tooyour dati nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="93f74-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="93f74-141">dati hello toocopy utilizzando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="93f74-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="93f74-142">Log nella macchina virtuale tooyour (VM)</span><span class="sxs-lookup"><span data-stu-id="93f74-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="93f74-143">Creare una nuova directory nel disco di dati della macchina virtuale di hello (Nota: non utilizzare hello disco temporaneo che viene fornito con hello macchina virtuale come disco dati).</span><span class="sxs-lookup"><span data-stu-id="93f74-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="93f74-144">In una finestra del prompt dei comandi, eseguire hello Azcopy della riga di comando seguente, sostituendo < path_to_data_folder > con la cartella di dati creata in (2):</span><span class="sxs-lookup"><span data-stu-id="93f74-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="93f74-145">Al termine, hello AzCopy un totale di 24 compresso file CSV (12 per viaggi\_dati e 12 per viaggi\_tariffa) devono trovarsi nella cartella dati hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="93f74-146">Decomprimere i file scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="93f74-147">Prendere nota hello cartella in cui risiedono i file non compresso hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="93f74-148">Questa cartella verrà tooas cui hello < percorso\_a\_dati\_file\>.</span><span class="sxs-lookup"><span data-stu-id="93f74-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="93f74-149"><a name="dbload"></a>Importazione in blocco dei dati nel database SQL Server</span><span class="sxs-lookup"><span data-stu-id="93f74-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="93f74-150">Hello delle prestazioni di caricamento/trasferire grandi quantità di database SQL tooan di dati e le query successive possono essere migliorate tramite *viste e tabelle partizionate*.</span><span class="sxs-lookup"><span data-stu-id="93f74-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="93f74-151">In questa sezione verrà seguito hello istruzioni di [parallela Bulk dei dati utilizzando SQL partizione tabelle di importazione](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate un nuovo database e caricare hello i dati in tabelle partizionate in parallelo.</span><span class="sxs-lookup"><span data-stu-id="93f74-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="93f74-152">Mentre si è connessi tooyour macchina virtuale, avviare **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="93f74-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="93f74-153">Effettuare la connessione mediante Autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="93f74-153">Connect using Windows Authentication.</span></span>
   
    ![Connessione a SSMS][12]
3. <span data-ttu-id="93f74-155">Se non ancora aver modificato la modalità autenticazione di SQL Server hello e creato un nuovo utente di accesso SQL, aprire il file di script hello denominato **modificare\_auth.sql** in hello **gli script di esempio** cartella.</span><span class="sxs-lookup"><span data-stu-id="93f74-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="93f74-156">Modificare nome hello predefinito dell'utente e password.</span><span class="sxs-lookup"><span data-stu-id="93f74-156">Change hello  default user name and password.</span></span> <span data-ttu-id="93f74-157">Fare clic su **! Eseguire** nello script hello toorun di hello barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="93f74-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Esecuzione dello script][13]
4. <span data-ttu-id="93f74-159">Verificare e/o modificare hello predefinito del database e log cartelle tooensure che nuovi database verrà archiviati in un disco dati di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="93f74-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="93f74-160">immagine di macchina virtuale SQL Server Hello ottimizzata per caricamenti DataWarehouse è preconfigurata con dischi dati e di log.</span><span class="sxs-lookup"><span data-stu-id="93f74-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="93f74-161">Se la macchina virtuale non include un disco dati e nuovi dischi rigidi virtuali non sono aggiunti durante il processo di installazione VM hello, modificare le cartelle predefinite hello come segue:</span><span class="sxs-lookup"><span data-stu-id="93f74-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="93f74-162">Nome di SQL Server hello pulsante destro del mouse nel pannello e fare clic a sinistra hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="93f74-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Proprietà di SQL Server][14]
   * <span data-ttu-id="93f74-164">Selezionare **le impostazioni del Database** da hello **selezione pagina** elenco toohello sinistra.</span><span class="sxs-lookup"><span data-stu-id="93f74-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="93f74-165">Verificare e/o modificare hello **percorsi predefiniti Database** toohello **disco dati** percorsi di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="93f74-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="93f74-166">In cui si trova nuovi database se creato con le impostazioni percorso di hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="93f74-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Impostazioni predefinite del database SQL][15]  
5. <span data-ttu-id="93f74-168">toocreate un nuovo database e un set di filegroup toohold hello tabelle partizionate, aprire uno script di esempio hello **creare\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="93f74-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="93f74-169">Hello script crea un nuovo database denominato **TaxiNYC** e 12 filegroup nel percorso dati predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="93f74-170">In ogni gruppo sarà presente un mese di dati trip\_data e trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="93f74-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="93f74-171">Modificare il nome del database hello, se opportuno.</span><span class="sxs-lookup"><span data-stu-id="93f74-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="93f74-172">Fare clic su **! Eseguire** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="93f74-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="93f74-173">Successivamente, creare due tabelle delle partizioni, uno per viaggi hello\_dati e un altro per viaggi hello\_fare.</span><span class="sxs-lookup"><span data-stu-id="93f74-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="93f74-174">Aprire uno script di esempio hello **creare\_partizionata\_Table**, che sarà:</span><span class="sxs-lookup"><span data-stu-id="93f74-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="93f74-175">Creare un partizione funzione toosplit hello dati in base al mese.</span><span class="sxs-lookup"><span data-stu-id="93f74-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="93f74-176">Creare un toomap lo schema di partizione di filegroup diverso tooa dati di ogni mese.</span><span class="sxs-lookup"><span data-stu-id="93f74-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="93f74-177">Creare due schema di partizione di tabelle partizionate toohello mappato: **nyctaxi\_viaggi** conterrà viaggi hello\_dati e **nyctaxi\_tariffa** conterrà viaggi hello \_presentare i dati.</span><span class="sxs-lookup"><span data-stu-id="93f74-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="93f74-178">Fare clic su **! Eseguire** toorun hello script e creare le tabelle partizionata hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="93f74-179">In hello **gli script di esempio** cartella, sono disponibili due script di PowerShell di esempio forniti toodemonstrate importazioni bulk parallela tooSQL Server di tabelle di dati.</span><span class="sxs-lookup"><span data-stu-id="93f74-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="93f74-180">**bcp\_parallela\_generic.ps1** è una script generico tooparallel importazione bulk dei dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="93f74-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="93f74-181">Modificare questo script tooset hello input e destinazione le variabili come indicato nelle righe di commento hello nello script hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="93f74-182">**bcp\_parallela\_nyctaxi.ps1** è una versione preconfigurata di script generico hello e può essere utilizzato tootooload entrambe le tabelle per i dati NYC Taxi trip hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="93f74-183">Pulsante destro del mouse hello **bcp\_parallela\_nyctaxi.ps1** nome dello script e fare clic su **modifica** tooopen in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93f74-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="93f74-184">Hello revisione preimpostato variabili e modificare secondo nome del database selezionato tooyour, cartella di dati di input, cartella di destinazione del log e file di formato di esempio toohello percorsi **nyctaxi_trip.xml** e **nyctaxi\_ Fare.XML** (disponibile in hello **gli script di esempio** cartella).</span><span class="sxs-lookup"><span data-stu-id="93f74-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Importazione in blocco dei dati][16]
   
    <span data-ttu-id="93f74-186">È inoltre possibile selezionare la modalità di autenticazione hello, impostazione predefinita è autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="93f74-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="93f74-187">Fare clic sulla freccia verde hello toorun barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="93f74-188">script Hello avvierà 24 operazioni di importazione bulk in parallelo, 12 per ogni tabella partizionata.</span><span class="sxs-lookup"><span data-stu-id="93f74-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="93f74-189">Si può monitorare lo stato di importazione dati di hello aprendo una cartella dati predefinita di SQL Server hello come set precedente.</span><span class="sxs-lookup"><span data-stu-id="93f74-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="93f74-190">i report di script di PowerShell Hello hello iniziale e finale di volte.</span><span class="sxs-lookup"><span data-stu-id="93f74-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="93f74-191">Quando tutti completo importazioni in blocco, viene segnalato hello ora di fine.</span><span class="sxs-lookup"><span data-stu-id="93f74-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="93f74-192">Controllare hello destinazione log cartella tooverify importazioni bulk hello hanno avuto esito positivo, ad esempio, non segnalati errori nella cartella log della destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="93f74-193">Il database ora è pronto per l'esplorazione, la progettazione di funzionalità e altre operazioni che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="93f74-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="93f74-194">Poiché le tabelle di hello vengono partizionate in base toohello **prelievo\_datetime** campo, le query che includono **prelievo\_datetime** condizioni hello  **DOVE** clausola trarranno vantaggio rispetto allo schema di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="93f74-195">In **SQL Server Management Studio**, esplorare uno script di esempio fornito hello **esempio\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="93f74-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="93f74-196">toorun delle query di esempio hello, evidenziazione hello righe di query, quindi fare clic su **! Eseguire** nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="93f74-197">Hello dati NYC Taxi trip viene caricato in due tabelle separate.</span><span class="sxs-lookup"><span data-stu-id="93f74-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="93f74-198">operazioni di join tooimprove, è consigliabile tabelle hello tooindex.</span><span class="sxs-lookup"><span data-stu-id="93f74-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="93f74-199">script di esempio Hello **creare\_partizionata\_index.sql** crea indici partizionati nella chiave di join composti hello **medallion, le maggiori\_licenza e prelievo\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="93f74-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="93f74-200"><a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in SQL Server</span><span class="sxs-lookup"><span data-stu-id="93f74-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="93f74-201">In questa sezione, si eseguirà la generazione di funzionalità e l'esplorazione dei dati mediante l'esecuzione di query SQL direttamente in hello **SQL Server Management Studio** utilizzando il database di SQL Server hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93f74-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="93f74-202">Uno script di esempio denominato **esempio\_queries.sql** è disponibile in hello **gli script di esempio** cartella.</span><span class="sxs-lookup"><span data-stu-id="93f74-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="93f74-203">Modificare nome del database hello toochange script hello, se è diverso da predefinito hello: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="93f74-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="93f74-204">In questo esercizio, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="93f74-204">In this exercise, we will:</span></span>

* <span data-ttu-id="93f74-205">Connettersi troppo**SQL Server Management Studio** usando l'autenticazione di Windows o utilizzando l'autenticazione di SQL e hello Nome accesso SQL e una password.</span><span class="sxs-lookup"><span data-stu-id="93f74-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="93f74-206">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="93f74-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="93f74-207">Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="93f74-208">Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.</span><span class="sxs-lookup"><span data-stu-id="93f74-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="93f74-209">Generazione di funzionalità calcolo/confronto delle distanze delle corse.</span><span class="sxs-lookup"><span data-stu-id="93f74-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="93f74-210">Join di tabelle hello due ed estrarre un campione casuale che verrà utilizzato toobuild modelli.</span><span class="sxs-lookup"><span data-stu-id="93f74-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="93f74-211">Quando si è pronti tooproceed tooAzure Machine Learning, è possibile:</span><span class="sxs-lookup"><span data-stu-id="93f74-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="93f74-212">Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, o</span><span class="sxs-lookup"><span data-stu-id="93f74-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="93f74-213">Mantenere hello campionato e dati decodificati Prevedi toouse per la creazione di un nuovo database modello di tabella e utilizzano nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="93f74-214">In questa sezione si salverà hello query finale tooextract hello dati di esempio e.</span><span class="sxs-lookup"><span data-stu-id="93f74-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="93f74-215">secondo metodo Hello viene dimostrata in hello [l'esplorazione dei dati e funzionalità di progettazione in IPython Notebook](#ipnb) sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="93f74-216">Per una rapida verifica del numero di hello di righe e colonne in hello tabelle popolate in precedenza mediante l'importazione bulk parallela,</span><span class="sxs-lookup"><span data-stu-id="93f74-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="93f74-217">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="93f74-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="93f74-218">In questo esempio identifica medallion hello (numeri taxi) con più di 100 trip all'interno di un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="93f74-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="93f74-219">query Hello può costituire un vantaggio accesso alle tabelle partizionata hello poiché condizionato, dallo schema di partizione hello di **prelievo\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="93f74-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="93f74-220">Una query di set di dati completo hello renderà inoltre usare della tabella partizionata hello e/o l'analisi di indice.</span><span class="sxs-lookup"><span data-stu-id="93f74-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="93f74-221">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="93f74-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="93f74-222">Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate</span><span class="sxs-lookup"><span data-stu-id="93f74-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="93f74-223">In questo esempio consente di esaminare se i campi di longitudine e/o latitudine hello contenere un valore non valido (gradi in radianti devono essere compreso tra -90 e 90,) o (0, 0) le coordinate.</span><span class="sxs-lookup"><span data-stu-id="93f74-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="93f74-224">Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="93f74-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="93f74-225">In questo esempio trova il numero di hello di viaggi che sono stati inclinato e inclinato non in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo).</span><span class="sxs-lookup"><span data-stu-id="93f74-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="93f74-226">Questa distribuzione riflette hello binario etichetta distribuzione toobe utilizzato successivamente per la modellazione di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="93f74-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="93f74-227">Esplorazione: distribuzione della classe o dell'intervallo delle mance</span><span class="sxs-lookup"><span data-stu-id="93f74-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="93f74-228">Questo esempio calcola la distribuzione di hello degli intervalli di comandi in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo).</span><span class="sxs-lookup"><span data-stu-id="93f74-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="93f74-229">Si tratta di distribuzione hello di classi di etichetta hello che verrà usato successivamente per la modellazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="93f74-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="93f74-230">Esplorazione: calcolo e confronto della distanza delle corse</span><span class="sxs-lookup"><span data-stu-id="93f74-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="93f74-231">In questo esempio converte la longitudine di ritiro e deposito hello e geography tooSQL latitudine punta, distanza di andata e ritorno hello utilizzando SQL geography punti differenza calcola e restituisce un campione casuale di risultati hello per il confronto.</span><span class="sxs-lookup"><span data-stu-id="93f74-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="93f74-232">esempio Hello limita i risultati di hello toovalid coordinate solo tramite query valutazione della qualità dei dati hello descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93f74-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="93f74-233">Progettazione di funzionalità nelle query SQL</span><span class="sxs-lookup"><span data-stu-id="93f74-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="93f74-234">Hello etichetta generazione geography conversione esplorazione le query e possono essere anche usato toogenerate etichette o le funzionalità rimuovendo hello conteggio parte.</span><span class="sxs-lookup"><span data-stu-id="93f74-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="93f74-235">Vengono forniti esempi SQL engineering di funzionalità aggiuntive in hello [l'esplorazione dei dati e funzionalità di progettazione in IPython Notebook](#ipnb) sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="93f74-236">È più efficiente toorun hello funzionalità generazione query sul set di dati completo hello o un sottoinsieme di grandi dimensioni usando le query SQL eseguito direttamente sull'istanza di database di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="93f74-237">le query Hello possono essere eseguite **SQL Server Management Studio**, IPython Notebook o qualsiasi strumento/ambiente di sviluppo che può accedere a hello database locale o remota.</span><span class="sxs-lookup"><span data-stu-id="93f74-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="93f74-238">Preparazione dei dati per la creazione di modelli</span><span class="sxs-lookup"><span data-stu-id="93f74-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="93f74-239">hello join di query seguente di Hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa** tabelle, genera un'etichetta di classificazione binaria **inclinato**, etichetta di classificazione multiclasse **suggerimento\_classe**ed estrae un campione casuale di % 1 da hello aggiunti a un set di dati completo.</span><span class="sxs-lookup"><span data-stu-id="93f74-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="93f74-240">Questa query può essere copiata successivamente incollata direttamente in hello [Azure Machine Learning Studio](https://studio.azureml.net) [l'importazione dei dati] [ import-data] modulo per l'inserimento di dati direttamente dal database di SQL Server hello istanza di Azure.</span><span class="sxs-lookup"><span data-stu-id="93f74-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="93f74-241">query Hello esclude i record con errato (0, 0) le coordinate.</span><span class="sxs-lookup"><span data-stu-id="93f74-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="93f74-242"><a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="93f74-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="93f74-243">In questa sezione, si eseguirà l'esplorazione dei dati e la generazione di funzionalità mediante sia Python e query SQL sul database di SQL Server hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93f74-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="93f74-244">IPython notebook esempio denominato **machine-Learning-data-science-process-sql-story.ipynb** è disponibile in hello **esempio IPython notebook** cartella.</span><span class="sxs-lookup"><span data-stu-id="93f74-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="93f74-245">Tale blocco di appunti è disponibile anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="93f74-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="93f74-246">Hello sequenza consigliata quando si utilizzano dati di grandi dimensioni può essere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="93f74-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="93f74-247">Lettura in un piccolo esempio dei dati hello in un frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="93f74-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="93f74-248">Eseguire alcune visualizzazioni e delle esplorazioni utilizzando hello dati campionati.</span><span class="sxs-lookup"><span data-stu-id="93f74-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="93f74-249">Provare varie combinazioni di progettazione di funzionalità mediante hello dati campionati.</span><span class="sxs-lookup"><span data-stu-id="93f74-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="93f74-250">Per l'esplorazione dei dati più grande, la manipolazione dei dati e progettazione di funzionalità, utilizzare query di SQL Python tooissue direttamente nel database di SQL Server hello hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="93f74-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="93f74-251">Decidere toouse dimensioni di esempio hello per la compilazione del modello di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="93f74-252">Al termine tooproceed tooAzure Machine Learning, può:</span><span class="sxs-lookup"><span data-stu-id="93f74-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="93f74-253">Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="93f74-254">Questo metodo è illustrato in hello [compilazione dei modelli in Azure Machine Learning](#mlmodel) sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="93f74-255">Mantenere hello campionati e i dati decodificati Prevedi toouse per la creazione di una nuova tabella di database modello, quindi utilizzare nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="93f74-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="93f74-256">di seguito Hello sono pochi l'esplorazione dei dati, la visualizzazione dei dati e funzionalità di esempi di progettazione.</span><span class="sxs-lookup"><span data-stu-id="93f74-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="93f74-257">Per ulteriori esempi, vedere hello esempio SQL IPython notebook hello **esempio IPython notebook** cartella.</span><span class="sxs-lookup"><span data-stu-id="93f74-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="93f74-258">Inizializzazione delle credenziali di database</span><span class="sxs-lookup"><span data-stu-id="93f74-258">Initialize Database Credentials</span></span>
<span data-ttu-id="93f74-259">Inizializzare le impostazioni di connessione di database in hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="93f74-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="93f74-260">Creazione della connessione di database</span><span class="sxs-lookup"><span data-stu-id="93f74-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="93f74-261">Segnalazione del numero di righe e di colonne nella tabella nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="93f74-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="93f74-262">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="93f74-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="93f74-263">Numero di colonne totali = 14</span><span class="sxs-lookup"><span data-stu-id="93f74-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="93f74-264">Lettura in un campione di dati di dimensioni ridotte da hello Database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="93f74-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="93f74-265">Tabella di esempio hello tooread ora è 6.492000 secondi</span><span class="sxs-lookup"><span data-stu-id="93f74-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="93f74-266">Numero di righe e di colonne recuperate = (8.4952, 21)</span><span class="sxs-lookup"><span data-stu-id="93f74-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="93f74-267">Statistiche descrittive</span><span class="sxs-lookup"><span data-stu-id="93f74-267">Descriptive Statistics</span></span>
<span data-ttu-id="93f74-268">Sono ora dati campionato hello tooexplore pronto.</span><span class="sxs-lookup"><span data-stu-id="93f74-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="93f74-269">Iniziamo con esaminando le statistiche descrittive per hello **viaggi\_distanza** (o qualsiasi altro) campi:</span><span class="sxs-lookup"><span data-stu-id="93f74-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="93f74-270">Visualizzazione: esempio di box plot</span><span class="sxs-lookup"><span data-stu-id="93f74-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="93f74-271">Successivamente si esamina il grafico box plot di hello per hello viaggi distanza toovisualize hello quantili</span><span class="sxs-lookup"><span data-stu-id="93f74-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="93f74-273">Visualizzazione: esempio di tracciato di distribuzione</span><span class="sxs-lookup"><span data-stu-id="93f74-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="93f74-275">Visualizzazione: tracciati a barre e linee</span><span class="sxs-lookup"><span data-stu-id="93f74-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="93f74-276">In questo esempio è bin distanza di andata e ritorno hello in cinque bin e visualizzare i risultati di binning hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="93f74-277">È possibile tracciare hello sopra distribuzione bin in una barra o riga del tracciato come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="93f74-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="93f74-280">Visualizzazione: esempio di grafico a dispersione</span><span class="sxs-lookup"><span data-stu-id="93f74-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="93f74-281">Viene illustrata la dispersione tra **viaggi\_ora\_in\_sec** e **viaggi\_distanza** toosee nel caso di qualsiasi correlazione</span><span class="sxs-lookup"><span data-stu-id="93f74-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

<span data-ttu-id="93f74-283">Analogamente è possibile controllare la relazione hello tra **frequenza\_codice** e **viaggi\_distanza**.</span><span class="sxs-lookup"><span data-stu-id="93f74-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="93f74-285">Hello sub-campionamento dei dati in SQL</span><span class="sxs-lookup"><span data-stu-id="93f74-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="93f74-286">Durante la preparazione dei dati per il modello di compilazione in [Azure Machine Learning Studio](https://studio.azureml.net), è possibile decidere di su hello **toouse query SQL direttamente nel modulo di importazione dei dati hello** o permanenti hello progettata e campionati dati in una nuova tabella, è possibile utilizzare in hello [l'importazione dei dati] [ import-data] modulo con un semplice **selezionare * FROM < il\_nuova\_tabella\_nome >**.</span><span class="sxs-lookup"><span data-stu-id="93f74-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="93f74-287">In questa sezione che si creerà un nuovo hello toohold tabella campionata e decodificati dati.</span><span class="sxs-lookup"><span data-stu-id="93f74-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="93f74-288">Viene fornito un esempio di una query SQL diretta per la compilazione del modello in hello [l'esplorazione dei dati e funzionalità di progettazione in SQL Server](#dbexplore) sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="93f74-289">Creare una tabella di esempio e la popola con % 1 di hello unita in join tabelle.</span><span class="sxs-lookup"><span data-stu-id="93f74-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="93f74-290">Innanzitutto eliminare la tabella, se presente.</span><span class="sxs-lookup"><span data-stu-id="93f74-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="93f74-291">In questa sezione è join di tabelle di hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa**, estrarre un campione casuale di % 1 e rendere persistenti i dati campionato hello in un nuovo nome di tabella  **nyctaxi\_uno\_%**:</span><span class="sxs-lookup"><span data-stu-id="93f74-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="93f74-292">Esplorazione dei dati mediante query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="93f74-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="93f74-293">In questa sezione vengono analizzate le distribuzioni dei dati utilizzando i dati di % 1 campionate hello che viene mantenuti nella nuova tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93f74-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="93f74-294">Si noti che esplorazioni simile possono essere eseguite mediante tabelle originali di hello, utilizzando facoltativamente **TABLESAMPLE** tooa dato periodo di tempo utilizzando hello risultati dell'esplorazione di hello toolimit sample o limitando hello **prelievo \_datetime** partizioni, come illustrato nell'hello [l'esplorazione dei dati e funzionalità di progettazione in SQL Server](#dbexplore) sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="93f74-295">Esplorazione: distribuzione giornaliera delle corse</span><span class="sxs-lookup"><span data-stu-id="93f74-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="93f74-296">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="93f74-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="93f74-297">Generazione di funzionalità mediante query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="93f74-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="93f74-298">In questa sezione verranno generati nuove etichette e funzionalità direttamente tramite query SQL, operano su tabella di esempio di % 1 hello è creato nella sezione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="93f74-299">Generazione di etichette: generazione di etichette di classe</span><span class="sxs-lookup"><span data-stu-id="93f74-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="93f74-300">Nell'esempio seguente di hello, si genera due set di etichette toouse per la modellazione:</span><span class="sxs-lookup"><span data-stu-id="93f74-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="93f74-301">Etichette di classe binaria **tipped** (che forniscono una stima sull'elargizione di una mancia)</span><span class="sxs-lookup"><span data-stu-id="93f74-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="93f74-302">Etichette multiclasse **suggerimento\_classe** (stima bin suggerimento hello o intervallo)</span><span class="sxs-lookup"><span data-stu-id="93f74-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="93f74-303">Progettazione di funzionalità: funzionalità di conteggio per le colonne relative alle categorie</span><span class="sxs-lookup"><span data-stu-id="93f74-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="93f74-304">In questo esempio trasforma un campo categorico in un campo numerico sostituendo ogni categoria con conteggio hello dei casi nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="93f74-305">Progettazione di funzionalità: funzionalità di collocazione per le colonne numeriche</span><span class="sxs-lookup"><span data-stu-id="93f74-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="93f74-306">In questo esempio, un campo numerico continuo viene trasformato in intervalli di categorie predefiniti, vale a dire che il campo numerico verrà trasformato in un campo di categoria.</span><span class="sxs-lookup"><span data-stu-id="93f74-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="93f74-307">Progettazione di funzionalità: funzionalità di estrazione della posizione dalla longitudine/latitudine decimale</span><span class="sxs-lookup"><span data-stu-id="93f74-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="93f74-308">In questo esempio suddivide rappresentazione decimale di hello di un campo di latitudine e/o longitudine in più campi area livelli di granularità diversi, ad esempio, paese, città, città, blocco e così via. Si noti che il nuovo hello geo-i campi non sono mappati a percorsi tooactual.</span><span class="sxs-lookup"><span data-stu-id="93f74-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="93f74-309">Per informazioni sul mapping delle località con codice geografico, vedere [Servizi REST di Bing Mappe](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="93f74-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="93f74-310">Verificare il modulo di finale hello della tabella trasformato hello</span><span class="sxs-lookup"><span data-stu-id="93f74-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="93f74-311">Sono ora pronti tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="93f74-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="93f74-312">dati Hello sono pronti per uno qualsiasi dei problemi di stima hello identificati in precedenza, vale a dire:</span><span class="sxs-lookup"><span data-stu-id="93f74-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="93f74-313">Classificazione binaria: toopredict o meno un suggerimento è stato pagato per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="93f74-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="93f74-314">Classificazione multiclasse: intervallo di hello toopredict del suggerimento a pagamento, in base a toohello classi definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93f74-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="93f74-315">Attività di regressione: quantità di hello toopredict del suggerimento a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="93f74-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="93f74-316"><a name="mlmodel"></a>Compilazione di modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93f74-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="93f74-317">toobegin hello modellazione esercizio log nell'area di lavoro tooyour Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="93f74-318">Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="93f74-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="93f74-319">tooget avviato con Azure Machine Learning, vedere [che cos'è Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="93f74-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="93f74-320">Accedi troppo[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="93f74-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="93f74-321">pagina iniziale di Studio Hello un'ampia gamma di informazioni, video, esercitazioni, collegamenti toohello riferimento moduli e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="93f74-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="93f74-322">Per ulteriori informazioni su Azure Machine Learning, consultare hello [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="93f74-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="93f74-323">Un esperimento di training tipica è costituita da hello segue:</span><span class="sxs-lookup"><span data-stu-id="93f74-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="93f74-324">Creazione di un esperimento **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="93f74-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="93f74-325">Ottenere dati di hello tooAzure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="93f74-326">Pre-elaborazione, trasformare e modificare i dati di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="93f74-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="93f74-327">Generazione di funzionalità, se necessario.</span><span class="sxs-lookup"><span data-stu-id="93f74-327">Generate features as needed.</span></span>
5. <span data-ttu-id="93f74-328">Suddividere i dati di hello in set di dati di training e la convalida o il test (o set di dati separati per ogni).</span><span class="sxs-lookup"><span data-stu-id="93f74-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="93f74-329">Selezionare uno o più algoritmi di machine learning a seconda di hello toosolve problema di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="93f74-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="93f74-330">Ad esempio, classificazione binaria, classificazione multiclasse, regressione.</span><span class="sxs-lookup"><span data-stu-id="93f74-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="93f74-331">Eseguire il training di uno o più modelli utilizzando hello training set.</span><span class="sxs-lookup"><span data-stu-id="93f74-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="93f74-332">Assegnare un punteggio hello convalida set di dati utilizzando modelli con training hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="93f74-333">Valutare hello modelli toocompute hello le metriche pertinenti per l'apprendimento problema hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="93f74-334">Ottimizzare i modelli di hello e selezionare hello migliore modello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="93f74-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="93f74-335">In questo esercizio, abbiamo già esplorato e decodificati dati hello in SQL Server e deciso tooingest dimensioni di esempio hello in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="93f74-336">toobuild uno o più modelli di stima hello che si è deciso di:</span><span class="sxs-lookup"><span data-stu-id="93f74-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="93f74-337">Ottenere dati di hello tooAzure Machine Learning usando hello [l'importazione dei dati] [ import-data] modulo, disponibile in hello **dati di Input e Output** sezione.</span><span class="sxs-lookup"><span data-stu-id="93f74-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="93f74-338">Per ulteriori informazioni, vedere hello [l'importazione dei dati] [ import-data] pagina di riferimento modulo.</span><span class="sxs-lookup"><span data-stu-id="93f74-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Dati di importazione di Azure Machine Learning][17]
2. <span data-ttu-id="93f74-340">Selezionare **Database SQL di Azure** come hello **origine dati** in hello **proprietà** pannello.</span><span class="sxs-lookup"><span data-stu-id="93f74-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="93f74-341">Immettere nome DNS del database hello in hello **nome server Database** campo.</span><span class="sxs-lookup"><span data-stu-id="93f74-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="93f74-342">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="93f74-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="93f74-343">Immettere hello **nome del Database** nel campo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="93f74-344">Immettere hello **nome utente di SQL** in hello * * aqccount nome utente e password hello in hello **password dell'account utente Server**.</span><span class="sxs-lookup"><span data-stu-id="93f74-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="93f74-345">Selezione dell'opzione **Accetta qualsiasi certificato server** .</span><span class="sxs-lookup"><span data-stu-id="93f74-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="93f74-346">In hello **query Database** Modifica area di testo, incollare query hello estrae hello necessario campi (incluse eventuali campi calcolati, ad esempio etichette hello) del database e verso il basso esempi di dimensioni del campione hello dati toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="93f74-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="93f74-347">Un esempio di lettura dei dati direttamente dal database di SQL Server hello un esperimento di classificazione binaria è in figura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="93f74-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="93f74-348">È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.</span><span class="sxs-lookup"><span data-stu-id="93f74-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formazione di Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="93f74-350">In hello modellazione estrazione dei dati e il campionamento di esempi di query forniti nelle sezioni precedenti, **tutte le etichette per gli esercizi di modellazione hello tre sono inclusi nella query hello**.</span><span class="sxs-lookup"><span data-stu-id="93f74-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="93f74-351">Un passaggio importante (obbligatorio) in ogni hello esercizi sulla modellazione è troppo**escludere** hello etichette non necessari per hello altri due problemi e qualsiasi altro **destinazione perdite**.</span><span class="sxs-lookup"><span data-stu-id="93f74-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="93f74-352">Per ad esempio, quando si utilizza una classificazione binaria, utilizzare hello etichetta **inclinato** ed escludere i campi di hello **suggerimento\_classe**, **suggerimento\_quantità**, e **totale\_quantità**.</span><span class="sxs-lookup"><span data-stu-id="93f74-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="93f74-353">Hello quest'ultimo vengono pagate perdite di destinazione, perché implicano suggerimento hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="93f74-354">colonne non necessarie tooexclude e/o perdite di destinazione, è possibile utilizzare hello [selezionare le colonne nel set di dati] [ select-columns] modulo o hello [Modifica metadati] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="93f74-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="93f74-355">Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="93f74-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="93f74-356"><a name="mldeploy"></a>Distribuzione di modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93f74-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="93f74-357">Quando il modello è pronto, è possibile distribuirlo facilmente come servizio web direttamente da esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="93f74-358">Per ulteriori informazioni sulla distribuzione di servizi Web Azure Machine Learning, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="93f74-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="93f74-359">toodeploy un nuovo servizio web, è necessario:</span><span class="sxs-lookup"><span data-stu-id="93f74-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="93f74-360">Creare un esperimento di assegnazione di punteggio.</span><span class="sxs-lookup"><span data-stu-id="93f74-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="93f74-361">Distribuire il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-361">Deploy hello web service.</span></span>

<span data-ttu-id="93f74-362">un punteggio sperimentare da toocreate un **completato** esperimento di training, fare clic su **CREATE SCORING EXPERIMENT** nella barra delle azioni inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Valutazione di Azure][18]

<span data-ttu-id="93f74-364">Azure Machine Learning tenterà toocreate un esperimento di assegnazione dei punteggi in base ai componenti di hello dell'esperimento di training hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="93f74-365">In particolare, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="93f74-365">In particular, it will:</span></span>

1. <span data-ttu-id="93f74-366">Salva modello con training hello e rimuovere i moduli di training modello di hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="93f74-367">Identificare una logica **porta di input** toorepresent hello previsto schema dati di input.</span><span class="sxs-lookup"><span data-stu-id="93f74-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="93f74-368">Identificare una logica **porta di output** toorepresent dello schema output di hello web previsto del servizio.</span><span class="sxs-lookup"><span data-stu-id="93f74-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="93f74-369">Quando viene creato l'assegnazione dei punteggi esperimento hello, esaminarla e modificare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="93f74-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="93f74-370">Un esempio tipico di regolazione sia set di dati tooreplace hello input e/o query con uno che esclude i campi di etichetta, poiché questi non saranno disponibili quando viene chiamato servizio hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="93f74-371">È anche una dimensione di hello tooreduce buona norma di hello alcuni record, dello schema di input sufficiente hello tooindicate tooa set di dati e/o query di input.</span><span class="sxs-lookup"><span data-stu-id="93f74-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="93f74-372">Per la porta di output di hello, è comune tooexclude campi di tutti gli input e includere solo hello **Scored Labels** e **calcolato il punteggio della probabilità** in hello output utilizzando hello [selezionare le colonne nel set di dati ] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="93f74-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="93f74-373">Un punteggio esperimento di esempio è in figura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="93f74-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="93f74-374">Al termine toodeploy, fare clic su hello **servizio WEB di pubblicare** pulsante nella barra delle azioni inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Pubblicazione di Azure Machine Learning][11]

<span data-ttu-id="93f74-376">toorecap, in questa esercitazione, questa procedura dettagliata è stato creato un ambiente di analisi scientifica dei dati di Azure, ha collaborato con un dataset pubblici di grandi dimensioni tutte modo hello da toomodel di acquisizione di dati di training e la distribuzione di un servizio web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93f74-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="93f74-377">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="93f74-377">License Information</span></span>
<span data-ttu-id="93f74-378">In questa procedura dettagliata di esempio e il relativo tipo di accompagnamento notebook(s) IPython e script sono condivisi da Microsoft con licenza MIT hello.</span><span class="sxs-lookup"><span data-stu-id="93f74-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="93f74-379">Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.</span><span class="sxs-lookup"><span data-stu-id="93f74-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="93f74-380">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="93f74-380">References</span></span>
<span data-ttu-id="93f74-381">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="93f74-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="93f74-382">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="93f74-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="93f74-383">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="93f74-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
