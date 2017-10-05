---
title: Compilare e distribuire un modello di Machine Learning utilizzando SQL Server in una macchina virtuale di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 6c5361c7e47209c8eb4d5630b44b3dcfeedeaf01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="e695b-103">Processo di analisi scientifica dei dati per i team in azione: uso di SQL Server</span><span class="sxs-lookup"><span data-stu-id="e695b-103">The Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="e695b-104">Questa esercitazione illustra la procedura dettagliata di costruzione e distribuzione di un modello di Machine Learning usando SQL Server e un set di dati disponibili pubblicamente: il set di dati [Corse dei taxi di New York](http://www.andresmh.com/nyctaxitrips/) .</span><span class="sxs-lookup"><span data-stu-id="e695b-104">In this tutorial, you walk through the process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="e695b-105">La procedura segue un flusso di lavoro di analisi scientifica dei dati standard: acquisizione ed esplorazione dei dati, funzionalità ingegneristiche per facilitare l'apprendimento e quindi compilazione e distribuzione di un modello.</span><span class="sxs-lookup"><span data-stu-id="e695b-105">The procedure follows a standard data science workflow: ingest and explore the data, engineer features to facilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="e695b-106"><a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York</span><span class="sxs-lookup"><span data-stu-id="e695b-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="e695b-107">I dati relativi alle corse dei taxi a NYC hanno dimensioni di circa 20 GB sotto forma di file CSV compressi(circa 48 GB senza compressione), e includono oltre 173 milioni di corse singole nonché le tariffe pagate per ciascuna corsa.</span><span class="sxs-lookup"><span data-stu-id="e695b-107">The NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="e695b-108">Il record di ogni corsa include la località di partenza e di arrivo, il numero di patente anonimo (del tassista) e il numero di licenza (ID univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="e695b-108">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e695b-109">I dati sono relativi a tutte le corse per l'anno 2013 e vengono forniti nei due set di dati seguenti per ciascun mese:</span><span class="sxs-lookup"><span data-stu-id="e695b-109">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="e695b-110">Il file CSV 'trip_data' contiene i dettagli delle corse, ad esempio il numero dei passeggeri, i punti partenza e arrivo, la durata e la lunghezza della corsa.</span><span class="sxs-lookup"><span data-stu-id="e695b-110">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e695b-111">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e695b-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="e695b-112">Il file CSV 'trip_fare' contiene i dettagli della tariffa pagata per ciascuna corsa, ad esempio tipo di pagamento, importo, soprattassa e tasse, mance e pedaggi e l'importo totale pagato.</span><span class="sxs-lookup"><span data-stu-id="e695b-112">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="e695b-113">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e695b-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e695b-114">La chiave univoca che consente di unire trip\_data e trip\_fare è composta dai campi: medallion, hack\_licence e pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e695b-114">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="e695b-115"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="e695b-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="e695b-116">Verranno formulati tre problemi di stima, basati su *tip\_amount*, vale a dire:</span><span class="sxs-lookup"><span data-stu-id="e695b-116">We will formulate three prediction problems based on the *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="e695b-117">Classificazione binaria: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="e695b-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="e695b-118">Classificazione multiclasse: consente di prevedere l'intervallo di mance lasciato per la corsa.</span><span class="sxs-lookup"><span data-stu-id="e695b-118">Multiclass classification: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="e695b-119">Il valore *tip\_amount* viene suddiviso in cinque bin o classi:</span><span class="sxs-lookup"><span data-stu-id="e695b-119">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="e695b-120">Attività di regressione: consente di prevedere l'importo della mancia lasciata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="e695b-120">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="e695b-121"><a name="setup"></a>Configurazione dell'ambiente di analisi scientifica dei dati Azure per l’analitica avanzata</span><span class="sxs-lookup"><span data-stu-id="e695b-121"><a name="setup"></a>Setting Up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="e695b-122">Come è possibile vedere nella guida di [pianificazione dell'ambiente](machine-learning-data-science-plan-your-environment.md) , sono disponibili diverse opzioni per utilizzare il set di dati Corse dei taxi di NYC in Azure:</span><span class="sxs-lookup"><span data-stu-id="e695b-122">As you can see from the [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options to work with the NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="e695b-123">Utilizzare i dati nei BLOB di Azure, quindi creare un modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e695b-123">Work with the data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="e695b-124">Caricare i dati in un database SQL Server, quindi creare un modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e695b-124">Load the data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="e695b-125">In questa esercitazione verrà illustrato come eseguire l'importazione in blocco in parallelo dei dati in SQL Server, l'esplorazione dei dati, la progettazione delle funzionalità e il sottocampionamento tramite SQL Server Management Studio e mediante IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e695b-125">In this tutorial we will demonstrate parallel bulk import of the data to a SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="e695b-126">Gli [script di esempio](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e i [blocchi di appunti IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) di esempio vengono condivisi in GitHub.</span><span class="sxs-lookup"><span data-stu-id="e695b-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="e695b-127">È inoltre disponibile nello stesso percorso un blocco di appunti IPython di esempio per gestire i dati nei blob.</span><span class="sxs-lookup"><span data-stu-id="e695b-127">A sample IPython notebook to work with the data in Azure blobs is also available in the same location.</span></span>

<span data-ttu-id="e695b-128">Per configurare l'ambiente di analisi scientifica dei dati di Azure:</span><span class="sxs-lookup"><span data-stu-id="e695b-128">To set up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="e695b-129">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e695b-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="e695b-130">Creare un'area di lavoro di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="e695b-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="e695b-131">[Eseguire il provisioning di una macchina virtuale Data Science](machine-learning-data-science-setup-sql-server-virtual-machine.md), che fornirà SQL Server e un server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e695b-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e695b-132">Gli script e i blocchi di appunti IPython di esempio verranno scaricati nella macchina virtuale Data Science durante il processo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e695b-132">The sample scripts and IPython notebooks will be downloaded to your Data Science virtual machine during the setup process.</span></span> <span data-ttu-id="e695b-133">Una volta completato lo script di post installazione della VM, gli esempi saranno disponibili nella libreria dei documenti della VM:</span><span class="sxs-lookup"><span data-stu-id="e695b-133">When the VM post-installation script completes, the samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="e695b-134">Script di esempio: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="e695b-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="e695b-135">Blocchi di appunti di esempio IPython: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="e695b-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="e695b-136">where `<user_name>` è il nome di accesso Windows della VM.</span><span class="sxs-lookup"><span data-stu-id="e695b-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="e695b-137">Le cartelle di esempio saranno denominate **Script di esempio** e **Blocchi di appunti IPython di esempio**.</span><span class="sxs-lookup"><span data-stu-id="e695b-137">We will refer to the sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="e695b-138">In base alle dimensioni del set di dati, al percorso dell'origine dati e all'ambiente di destinazione Azure selezionato, questo scenario è simile allo [Scenario \#n.5: Set di dati di grandi dimensioni in file locali, con destinazione SQL Server nella macchina virtuale di Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="e695b-138">Based on the dataset size, data source location, and the selected Azure target environment, this scenario is similar to [Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="e695b-139"><a name="getdata"></a>Acquisizione dei dati da un'origine pubblica</span><span class="sxs-lookup"><span data-stu-id="e695b-139"><a name="getdata"></a>Get the Data from Public Source</span></span>
<span data-ttu-id="e695b-140">Per visualizzare il set di dati [Corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/) dal relativo percorso pubblico, è possibile usare uno qualsiasi dei metodi descritti in [Spostamento dei dati da e verso l'archivio BLOB di Azure](machine-learning-data-science-move-azure-blob.md) e copiare i dati nella nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e695b-140">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your new virtual machine.</span></span>

<span data-ttu-id="e695b-141">Per copiare i dati usando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e695b-141">To copy the data using AzCopy:</span></span>

1. <span data-ttu-id="e695b-142">Accedere alla macchina virtuale (VM)</span><span class="sxs-lookup"><span data-stu-id="e695b-142">Log in to your virtual machine (VM)</span></span>
2. <span data-ttu-id="e695b-143">Creare una nuova directory nel disco dati della macchina virtuale (nota: non utilizzare come disco dati il disco temporaneo fornito con la macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="e695b-143">Create a new directory in the VM's data disk (Note: Do not use the Temporary Disk which comes with the VM as a Data Disk).</span></span>
3. <span data-ttu-id="e695b-144">In una finestra di prompt dei comandi, eseguire la seguente riga di comando Azcopy, sostituendo <path_to_data_folder> con la cartella dei dati creata al passaggio (2):</span><span class="sxs-lookup"><span data-stu-id="e695b-144">In a Command Prompt window, run the following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="e695b-145">Al termine dell'esecuzione di AzCopy, nella cartella dovrebbero essere presenti 24 file CSV compressi (12 per trip\_data e 12 per trip\_fare).</span><span class="sxs-lookup"><span data-stu-id="e695b-145">When the AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in the data folder.</span></span>
4. <span data-ttu-id="e695b-146">Decomprimere i file scaricati.</span><span class="sxs-lookup"><span data-stu-id="e695b-146">Unzip the downloaded files.</span></span> <span data-ttu-id="e695b-147">Prendere nota della cartella in cui si trovano i dati non compressi.</span><span class="sxs-lookup"><span data-stu-id="e695b-147">Note the folder where the uncompressed files reside.</span></span> <span data-ttu-id="e695b-148">Il riferimento di questa cartella sarà <percorso\_a\_file\_dati\>.</span><span class="sxs-lookup"><span data-stu-id="e695b-148">This folder will be referred to as the <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="e695b-149"><a name="dbload"></a>Importazione in blocco dei dati nel database SQL Server</span><span class="sxs-lookup"><span data-stu-id="e695b-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="e695b-150">È possibile migliorare le prestazioni relative al caricamento/trasferimento di grandi quantità di dati in un database SQL e le successive query usando *Tabelle e viste partizionate*.</span><span class="sxs-lookup"><span data-stu-id="e695b-150">The performance of loading/transferring large amounts of data to an SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="e695b-151">In questa sezione, verranno seguite le istruzioni fornite in [Importazione in blocco dei dati in parallelo tramite le tabelle delle partizioni di SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) per creare un nuovo database e caricare i dati nelle tabelle partizionate in parallelo.</span><span class="sxs-lookup"><span data-stu-id="e695b-151">In this section, we will follow the instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) to create a new database and load the data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="e695b-152">Dopo aver effettuato l'accesso alla VM, avviare **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="e695b-152">While logged in to your VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="e695b-153">Effettuare la connessione mediante Autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="e695b-153">Connect using Windows Authentication.</span></span>
   
    ![Connessione a SSMS][12]
3. <span data-ttu-id="e695b-155">Se non è stata ancora modificata la modalità di autenticazione di SQL Server e non è stato creato un nuovo utente di accesso SQL, aprire il file di script denominato **change\_auth.sql** nella cartella **Script di esempio**.</span><span class="sxs-lookup"><span data-stu-id="e695b-155">If you have not yet changed the SQL Server authentication mode and created a new SQL login user, open the script file named **change\_auth.sql** in the **Sample Scripts** folder.</span></span> <span data-ttu-id="e695b-156">Modificare il nome utente e la password predefiniti.</span><span class="sxs-lookup"><span data-stu-id="e695b-156">Change the  default user name and password.</span></span> <span data-ttu-id="e695b-157">Fare clic su **!Esegui** nella barra degli strumenti per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="e695b-157">Click **!Execute** in the toolbar to run the script.</span></span>
   
    ![Esecuzione dello script][13]
4. <span data-ttu-id="e695b-159">Verificare e/o modificare le cartelle di database e log predefinite di SQL Server per essere certi che i database appena creati saranno archiviati nel disco dati.</span><span class="sxs-lookup"><span data-stu-id="e695b-159">Verify and/or change the SQL Server default database and log folders to ensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="e695b-160">L'immagine della VM SQL Server che viene ottimizzata per i carichi data warehouse viene preconfigurata con i dischi dati e di registro.</span><span class="sxs-lookup"><span data-stu-id="e695b-160">The SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="e695b-161">Se nella VM in uso non è incluso un disco dati e durante il processo di configurazione della VM sono stati aggiunti dei nuovi dischi virtuali, modificare le cartelle predefinite nel modo indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e695b-161">If your VM did not include a Data Disk and you added new virtual hard disks during the VM setup process, change the default folders as follows:</span></span>
   
   * <span data-ttu-id="e695b-162">Fare clic con il pulsante destro del mouse sul nome dell'SQL Server nel pannello a sinistra e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="e695b-162">Right-click the SQL Server name in the left panel and click **Properties**.</span></span>
     
       ![Proprietà di SQL Server][14]
   * <span data-ttu-id="e695b-164">Selezionare **Impostazioni database** dall'elenco **Seleziona pagina** sulla sinistra.</span><span class="sxs-lookup"><span data-stu-id="e695b-164">Select **Database Settings** from the **Select a page** list to the left.</span></span>
   * <span data-ttu-id="e695b-165">Verificare e/o modificare **Percorsi predefiniti database** nei percorsi **Disco dati** di preferenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-165">Verify and/or change the **Database default locations** to the **Data Disk** locations of your choice.</span></span> <span data-ttu-id="e695b-166">È questa la posizione in cui si trovano i nuovi database se vengono creati con le impostazioni di percorso predefinite.</span><span class="sxs-lookup"><span data-stu-id="e695b-166">This is where new databases reside if created with the default location settings.</span></span>
     
       ![Impostazioni predefinite del database SQL][15]  
5. <span data-ttu-id="e695b-168">Per creare un nuovo database e un set di filegroup in cui conservare le tabelle partizionate, aprire lo script di esempio **create\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="e695b-168">To create a new database and a set of filegroups to hold the partitioned tables, open the sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="e695b-169">Mediante questo script verranno creati un nuovo database denominato **TaxiNYC** e 12 filegroup nel percorso dei dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="e695b-169">The script will create a new database named **TaxiNYC** and 12 filegroups in the default data location.</span></span> <span data-ttu-id="e695b-170">In ogni gruppo sarà presente un mese di dati trip\_data e trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="e695b-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="e695b-171">Se lo si desidera, modificare il nome del database.</span><span class="sxs-lookup"><span data-stu-id="e695b-171">Modify the database name, if desired.</span></span> <span data-ttu-id="e695b-172">Fare clic su **!Esegui** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="e695b-172">Click **!Execute** to run the script.</span></span>
6. <span data-ttu-id="e695b-173">Successivamente, creare due tabelle delle partizioni, una per trip\_data e l'altra per trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="e695b-173">Next, create two partition tables, one for the trip\_data and another for the trip\_fare.</span></span> <span data-ttu-id="e695b-174">Aprire lo script di esempio **create\_partitioned\_table.sql**, in modo da eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-174">Open the sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="e695b-175">Creare una funzione di partizione per suddividere i dati per mese.</span><span class="sxs-lookup"><span data-stu-id="e695b-175">Create a partition function to split the data by month.</span></span>
   * <span data-ttu-id="e695b-176">Creare uno schema di partizione per eseguire il mapping dei dati di ciascun mese a un filegroup diverso.</span><span class="sxs-lookup"><span data-stu-id="e695b-176">Create a partition scheme to map each month's data to a different filegroup.</span></span>
   * <span data-ttu-id="e695b-177">Creare due tabelle partizionate di cui è stato eseguito il mapping allo schema di partizione: **nyctaxi\_trip** conterrà i dati trip\_data e **nyctaxi\_fare** conterrà i dati trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="e695b-177">Create two partitioned tables mapped to the partition scheme: **nyctaxi\_trip** will hold the trip\_data and **nyctaxi\_fare** will hold the trip\_fare data.</span></span>
     
     <span data-ttu-id="e695b-178">Fare clic su **!Esegui** per eseguire lo script e creare le tabelle partizionate.</span><span class="sxs-lookup"><span data-stu-id="e695b-178">Click **!Execute** to run the script and create the partitioned tables.</span></span>
7. <span data-ttu-id="e695b-179">Nella cartella **Script di esempio** , sono presenti due script PowerShell di esempio, forniti per illustrare le importazioni in blocco in parallelo dei dati nelle tabelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e695b-179">In the **Sample Scripts** folder, there are two sample PowerShell scripts provided to demonstrate parallel bulk imports of data to SQL Server tables.</span></span>
   
   * <span data-ttu-id="e695b-180">**bcp\_parallel\_generic.ps1** è uno script generico per l'importazione in blocco in parallelo dei dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="e695b-180">**bcp\_parallel\_generic.ps1** is a generic script to parallel bulk import data into a table.</span></span> <span data-ttu-id="e695b-181">Modificare lo script per impostare le variabili di input e di destinazione come indicato nelle righe di commento dello script.</span><span class="sxs-lookup"><span data-stu-id="e695b-181">Modify this script to set the input and target variables as indicated in the comment lines in the script.</span></span>
   * <span data-ttu-id="e695b-182">**bcp\_parallel\_nyctaxi.ps1** è una versione preconfigurata dello script generico e può essere usata per caricare entrambe le tabelle per i dati Corse dei taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="e695b-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of the generic script and can be used to to load both tables for the NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="e695b-183">Fare clic con il pulsante destro del mouse sul nome dello script **bcp\_parallel\_nyctaxi.ps1** e fare clic su **Modifica** per aprirlo in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e695b-183">Right-click the **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** to open it in PowerShell.</span></span> <span data-ttu-id="e695b-184">Esaminare le variabili preimpostate e modificarle in base al nome di database selezionato, alla cartella dei dati di input, alla cartella del log di destinazione e ai percorsi dei file di formato di esempio **nyctaxi_trip.xml** e **nyctaxi\_fare.xml** (forniti nella cartella **Script di esempio**).</span><span class="sxs-lookup"><span data-stu-id="e695b-184">Review the preset variables and modify according to your selected database name, input data folder, target log folder, and paths to the  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in the **Sample Scripts** folder).</span></span>
   
    ![Importazione in blocco dei dati][16]
   
    <span data-ttu-id="e695b-186">È inoltre possibile selezionare la modalità di autenticazione. La modalità predefinita è Autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="e695b-186">You may also select the authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="e695b-187">Fare clic sulla freccia verde nella barra degli strumenti per eseguire.</span><span class="sxs-lookup"><span data-stu-id="e695b-187">Click the green arrow in the toolbar to run.</span></span> <span data-ttu-id="e695b-188">Mediante lo script verranno avviate 24 operazioni in blocco in parallelo, 12 per ogni tabella partizionata.</span><span class="sxs-lookup"><span data-stu-id="e695b-188">The script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="e695b-189">È possibile controllare lo stato dell'importazione dei dati aprendo la cartella dei dati predefinita di SQL Server come impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-189">You may monitor the data import progress by opening the SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="e695b-190">Nello script PowerShell vengono segnalate l'ora di inizio e l'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="e695b-190">The PowerShell script reports the starting and ending times.</span></span> <span data-ttu-id="e695b-191">Al completamento di tutte le importazioni in blocco, viene indicata l'ora finale.</span><span class="sxs-lookup"><span data-stu-id="e695b-191">When all bulk imports complete, the ending time is reported.</span></span> <span data-ttu-id="e695b-192">Verificare nella cartella del log di destinazione che le importazioni in blocco siano state completate correttamente, vale a dire che non siano stati segnalati errori nella cartella del log di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e695b-192">Check the target log folder to verify that the bulk imports were successful, i.e., no errors reported in the target log folder.</span></span>
10. <span data-ttu-id="e695b-193">Il database ora è pronto per l'esplorazione, la progettazione di funzionalità e altre operazioni che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="e695b-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="e695b-194">Poiché le tabelle sono partizionate in base al campo **pickup\_datetime**, le query che includono le condizioni **pickup\_datetime** nella clausola **WHERE** si avvarranno dello schema di partizione.</span><span class="sxs-lookup"><span data-stu-id="e695b-194">Since the tables are partitioned according to the **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in the **WHERE** clause will benefit from the partition scheme.</span></span>
11. <span data-ttu-id="e695b-195">In **SQL Server Management Studio** esplorare lo script di esempio fornito **sample\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="e695b-195">In **SQL Server Management Studio**, explore the provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="e695b-196">Per eseguire una qualsiasi query di esempio, evidenziare le righe della query, quindi fare clic su **!Esegui** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="e695b-196">To run any of the sample queries, highlight the query lines then click **!Execute** in the toolbar.</span></span>
12. <span data-ttu-id="e695b-197">I dati di Corse dei taxi di NYC vengono caricati in due tabelle distinte.</span><span class="sxs-lookup"><span data-stu-id="e695b-197">The NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="e695b-198">Per migliorare le operazioni di unione, è consigliabile indicizzare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="e695b-198">To improve join operations, it is highly recommended to index the tables.</span></span> <span data-ttu-id="e695b-199">Lo script di esempio **create\_partitioned\_index.sql** consente di creare indici partizionati sulla chiave di join composita **medallion, hack\_license, and pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="e695b-199">The sample script **create\_partitioned\_index.sql** creates partitioned indexes on the composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="e695b-200"><a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in SQL Server</span><span class="sxs-lookup"><span data-stu-id="e695b-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="e695b-201">In questa sezione, verranno eseguite l'esplorazione dei dati e la generazione di funzionalità mediante l'esecuzione di query SQL direttamente in **SQL Server Management Studio** tramite un database SQL Server creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in the **SQL Server Management Studio** using the SQL Server database created earlier.</span></span> <span data-ttu-id="e695b-202">Uno script di esempio denominato **sample\_queries.sql** viene fornito nella cartella **Script di esempio**.</span><span class="sxs-lookup"><span data-stu-id="e695b-202">A sample script named **sample\_queries.sql** is provided in the **Sample Scripts** folder.</span></span> <span data-ttu-id="e695b-203">Modificare lo script per cambiare il nome del database, se è diverso da quello predefinito: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="e695b-203">Modify the script to change the database name, if it is different from the default: **TaxiNYC**.</span></span>

<span data-ttu-id="e695b-204">In questo esercizio, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-204">In this exercise, we will:</span></span>

* <span data-ttu-id="e695b-205">Connessione a **SQL Server Management Studio** tramite Autenticazione di Windows o mediante Autenticazione SQL e il nome di accesso e la password SQL.</span><span class="sxs-lookup"><span data-stu-id="e695b-205">Connect to **SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and the SQL login name and password.</span></span>
* <span data-ttu-id="e695b-206">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="e695b-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="e695b-207">Indagine sulla qualità dei dati dei campi di longitudine e latitudine.</span><span class="sxs-lookup"><span data-stu-id="e695b-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="e695b-208">Generazione di etichette di classificazione binaria e multiclasse basata su **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="e695b-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="e695b-209">Generazione di funzionalità calcolo/confronto delle distanze delle corse.</span><span class="sxs-lookup"><span data-stu-id="e695b-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="e695b-210">Unione di due tabelle ed estrazione di un campione casuale che verrà utilizzato per la creazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="e695b-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

<span data-ttu-id="e695b-211">Una volta pronti a proseguire con Azure Machine Learning, è possibile effettuare una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-211">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="e695b-212">Salvare la query SQL finale per estrarre e campionare i dati e copiare e incollare la query direttamente in un modulo [Import Data][import-data] (Importa dati) in Azure Machine Learning, oppure</span><span class="sxs-lookup"><span data-stu-id="e695b-212">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="e695b-213">Salvare in modo definitivo i dati campionati e compilati che si prevede di usare per la creazione di modelli in una nuova tabella di database e usare la nuova tabella nel modulo [Import Data][import-data] (Importa dati) in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-213">Persist the sampled and engineered data you plan to use for model building in a new database table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="e695b-214">In questa sezione verrà salvata la query finale per estrarre e campionare i dati.</span><span class="sxs-lookup"><span data-stu-id="e695b-214">In this section we will save the final query to extract and sample the data.</span></span> <span data-ttu-id="e695b-215">Il secondo metodo viene illustrato nella sezione [Esplorazione dei dati e progettazione di funzionalità in IPython Notebook](#ipnb) .</span><span class="sxs-lookup"><span data-stu-id="e695b-215">The second method is demonstrated in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="e695b-216">Per una verifica rapida del numero di righe e di colonne nelle tabelle popolate in precedenza tramite l'importazione in blocco in parallelo,</span><span class="sxs-lookup"><span data-stu-id="e695b-216">For a quick verification of the number of rows and columns in the tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="e695b-217">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e695b-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="e695b-218">In questo esempio viene identificata la licenza (numero del taxi) che ha eseguito più di 100 corse in un determinato periodo.</span><span class="sxs-lookup"><span data-stu-id="e695b-218">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="e695b-219">Per la query verrà usata la tabella partizionata poiché è condizionata dallo schema di partizione di **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="e695b-219">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="e695b-220">Per la query del set di dati completo verrà inoltre utilizzata la tabella partizionata e/o l'analisi dell'indice.</span><span class="sxs-lookup"><span data-stu-id="e695b-220">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="e695b-221">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="e695b-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="e695b-222">Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate</span><span class="sxs-lookup"><span data-stu-id="e695b-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="e695b-223">In questo esempio viene esaminato se uno dei campi relativi alla longitudine o alla latitudine contiene un valore non valido (i gradi radianti devono essere compresi tra -90 e 90) o presenta le coordinate (0, 0).</span><span class="sxs-lookup"><span data-stu-id="e695b-223">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="e695b-224">Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="e695b-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="e695b-225">In questo esempio viene individuato il numero di corse per le quali è stata lasciata una mancia e il numero di corse per le quali non è stata lasciata una mancia in un determinato periodo (o nel set di dati completo, in caso di un anno intero).</span><span class="sxs-lookup"><span data-stu-id="e695b-225">This example finds the number of trips that were tipped vs. not tipped in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="e695b-226">Questa distribuzione riflette la distribuzione delle etichette binarie che dovranno essere utilizzate in seguito per la creazione di modelli di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="e695b-226">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="e695b-227">Esplorazione: distribuzione della classe o dell'intervallo delle mance</span><span class="sxs-lookup"><span data-stu-id="e695b-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="e695b-228">In questo esempio viene calcolata la distribuzione degli intervalli delle mance in un determinato periodo (o nel set di dati completo, in caso di un anno intero).</span><span class="sxs-lookup"><span data-stu-id="e695b-228">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="e695b-229">Si tratta della distribuzione delle classi di etichette che verranno utilizzate in seguito per la creazione di modelli di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="e695b-229">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

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

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="e695b-230">Esplorazione: calcolo e confronto della distanza delle corse</span><span class="sxs-lookup"><span data-stu-id="e695b-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="e695b-231">In questo esempio, la longitudine e la latitudine del prelievo e dello scarico vengono convertite in punti geografici SQL, viene calcolata la distanza della corsa mediante la differenza dei punti geografici di SQL e viene restituito un campione casuale dei risultati per il confronto.</span><span class="sxs-lookup"><span data-stu-id="e695b-231">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="e695b-232">Nell'esempio i risultati vengono limitati unicamente alle coordinate valide tramite la query per la valutazione della qualità dei dati illustrata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-232">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

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

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="e695b-233">Progettazione di funzionalità nelle query SQL</span><span class="sxs-lookup"><span data-stu-id="e695b-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="e695b-234">Le query di esplorazione per la generazione delle etichette e la conversione geografica possono inoltre essere utilizzate per generare etichette/funzionalità se si rimuove la parte relativa al conteggio.</span><span class="sxs-lookup"><span data-stu-id="e695b-234">The label generation and geography conversion exploration queries can also be used to generate labels/features by removing the counting part.</span></span> <span data-ttu-id="e695b-235">Ulteriori esempi SQL di progettazione di funzionalità vengono forniti nella sezione [Esplorazione dei dati e progettazione di funzionalità in IPython Notebook](#ipnb) .</span><span class="sxs-lookup"><span data-stu-id="e695b-235">Additional feature engineering SQL examples are provided in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="e695b-236">È più efficiente eseguire le query di generazione di funzionalità sull'intero set di dati o su un subset di grandi dimensioni tramite query SQL che si eseguono direttamente sull'istanza di database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e695b-236">It is more efficient to run the feature generation queries on the full dataset or a large subset of it using SQL queries which run directly on the SQL Server database instance.</span></span> <span data-ttu-id="e695b-237">Le query possono essere eseguite in **SQL Server Management Studio**, IPython Notebook o in qualsiasi strumento o ambiente di sviluppo in grado di accedere al database localmente o in remoto.</span><span class="sxs-lookup"><span data-stu-id="e695b-237">The queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access the database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="e695b-238">Preparazione dei dati per la creazione di modelli</span><span class="sxs-lookup"><span data-stu-id="e695b-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="e695b-239">Le query riportate di seguito consentono di unire le tabelle **nyctaxi\_trip** e **nyctaxi\_fare**, generare un'etichetta di classificazione binaria **tipped**, un'etichetta di classificazione multiclasse **tip\_class** e di estrarre un campione casuale dell'1% dall'intero set di dati unito.</span><span class="sxs-lookup"><span data-stu-id="e695b-239">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from the full joined dataset.</span></span> <span data-ttu-id="e695b-240">La query può essere copiata e incollata direttamente nel modulo [Import Data][import-data] (Importa dati) di [Azure Machine Learning Studio](https://studio.azureml.net) per l'inserimento diretto dei dati dall'istanza del database SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="e695b-240">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL Server database instance in Azure.</span></span> <span data-ttu-id="e695b-241">La query esclude i record con le coordinate errate (0, 0).</span><span class="sxs-lookup"><span data-stu-id="e695b-241">The query excludes records with incorrect (0, 0) coordinates.</span></span>

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


## <span data-ttu-id="e695b-242"><a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e695b-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="e695b-243">In questa sezione, verranno eseguite l'esplorazione dei dati e la generazione di funzionalità mediante l'esecuzione di query Pyton e SQL tramite un database SQL Server creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL Server database created earlier.</span></span> <span data-ttu-id="e695b-244">Un blocco di appunti IPython di esempio denominato **machine-Learning-data-science-process-sql-story.ipynb** viene fornito nella cartella **Blocchi di appunti di esempio IPython**.</span><span class="sxs-lookup"><span data-stu-id="e695b-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in the **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="e695b-245">Tale blocco di appunti è disponibile anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="e695b-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="e695b-246">La sequenza consigliata quando si utilizzano i Big Data è la seguente:</span><span class="sxs-lookup"><span data-stu-id="e695b-246">The recommended sequence when working with big data is the following:</span></span>

* <span data-ttu-id="e695b-247">Leggere un piccolo campione di dati in un frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="e695b-247">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="e695b-248">Eseguire alcune visualizzazioni ed esplorazioni tramite i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e695b-248">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="e695b-249">Sperimentare la progettazione di funzionalità utilizzando i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e695b-249">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="e695b-250">Per operazioni più estese di esplorazione dei dati, manipolazione dei dati e progettazione di funzionalità, utilizzare Python per inviare query SQL direttamente al database SQL Server nella VM Azure.</span><span class="sxs-lookup"><span data-stu-id="e695b-250">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL Server database in the Azure VM.</span></span>
* <span data-ttu-id="e695b-251">Decidere la dimensione del campione da utilizzare per la creazione di modelli Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-251">Decide the sample size to use for Azure Machine Learning model building.</span></span>

<span data-ttu-id="e695b-252">Una volta pronti a proseguire con Azure Machine Learning, è possibile effettuare una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-252">When ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="e695b-253">Salvare la query SQL finale per estrarre e campionare i dati e copiare e incollare la query direttamente in un modulo [Import Data][import-data] (Importa dati) in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-253">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="e695b-254">Questo metodo è illustrato nella sezione [Creazione di modelli in Azure Machine Learning](#mlmodel) .</span><span class="sxs-lookup"><span data-stu-id="e695b-254">This method is demonstrated in the [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="e695b-255">Salvare in modo definitivo i dati campionati e compilati che si prevede di usare per la creazione di modelli in una nuova tabella di database, quindi usare la nuova tabella nel modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="e695b-255">Persist the sampled and engineered data you plan to use for model building in a new database table, then use the new table in the [Import Data][import-data] module.</span></span>

<span data-ttu-id="e695b-256">Di seguito vengono forniti alcuni esempi di esplorazione dei dati, visualizzazione dei dati e progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e695b-256">The following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="e695b-257">Per ulteriori esempi, vedere il blocco di appunti di esempio SQL IPython nella cartella **Blocchi di appunti IPython di esempio** .</span><span class="sxs-lookup"><span data-stu-id="e695b-257">For more examples, see the sample SQL IPython notebook in the **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="e695b-258">Inizializzazione delle credenziali di database</span><span class="sxs-lookup"><span data-stu-id="e695b-258">Initialize Database Credentials</span></span>
<span data-ttu-id="e695b-259">Inizializzare le impostazioni di connessione del database nelle seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="e695b-259">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="e695b-260">Creazione della connessione di database</span><span class="sxs-lookup"><span data-stu-id="e695b-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="e695b-261">Segnalazione del numero di righe e di colonne nella tabella nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="e695b-261">Report number of rows and columns in table nyctaxi_trip</span></span>
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

* <span data-ttu-id="e695b-262">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="e695b-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="e695b-263">Numero di colonne totali = 14</span><span class="sxs-lookup"><span data-stu-id="e695b-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a><span data-ttu-id="e695b-264">Effettuazione della lettura di un piccolo campione di dati dal database SQL Server</span><span class="sxs-lookup"><span data-stu-id="e695b-264">Read-in a small data sample from the SQL Server Database</span></span>
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
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="e695b-265">Il tempo per la lettura della tabella di esempio è di 6,492000 secondi</span><span class="sxs-lookup"><span data-stu-id="e695b-265">Time to read the sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="e695b-266">Numero di righe e di colonne recuperate = (8.4952, 21)</span><span class="sxs-lookup"><span data-stu-id="e695b-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="e695b-267">Statistiche descrittive</span><span class="sxs-lookup"><span data-stu-id="e695b-267">Descriptive Statistics</span></span>
<span data-ttu-id="e695b-268">Ora è possibile esplorare i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e695b-268">Now are ready to explore the sampled data.</span></span> <span data-ttu-id="e695b-269">Si inizia dalle statistiche descrittive per i campi **trip\_distance** (o qualsiasi altro):</span><span class="sxs-lookup"><span data-stu-id="e695b-269">We start with looking at descriptive statistics for the **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="e695b-270">Visualizzazione: esempio di box plot</span><span class="sxs-lookup"><span data-stu-id="e695b-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="e695b-271">Successivamente si consulterà il box plot per la distanza delle corse, per visualizzare le quantità</span><span class="sxs-lookup"><span data-stu-id="e695b-271">Next we look at the box plot for the trip distance to visualize the quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="e695b-273">Visualizzazione: esempio di tracciato di distribuzione</span><span class="sxs-lookup"><span data-stu-id="e695b-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="e695b-275">Visualizzazione: tracciati a barre e linee</span><span class="sxs-lookup"><span data-stu-id="e695b-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="e695b-276">In questo esempio, la distanza delle corse viene suddivisa in cinque contenitori e vengono visualizzati i risultati di questa suddivisione.</span><span class="sxs-lookup"><span data-stu-id="e695b-276">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="e695b-277">La distribuzione precedente può essere rappresentata in un tracciato a barre o linee come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="e695b-277">We can plot the above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="e695b-280">Visualizzazione: esempio di grafico a dispersione</span><span class="sxs-lookup"><span data-stu-id="e695b-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="e695b-281">Viene eseguito un grafico a dispersione tra **trip\_time\_in\_secs** e **trip\_distance** per verificare se esiste una correlazione.</span><span class="sxs-lookup"><span data-stu-id="e695b-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

<span data-ttu-id="e695b-283">Allo stesso modo, è possibile verificare la relazione tra **rate\_code** e **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="e695b-283">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="sub-sampling-the-data-in-sql"></a><span data-ttu-id="e695b-285">Sottocampionamento dei dati in SQL</span><span class="sxs-lookup"><span data-stu-id="e695b-285">Sub-Sampling the Data in SQL</span></span>
<span data-ttu-id="e695b-286">Quando si preparano i dati per la creazione di modelli in [Azure Machine Learning Studio](https://studio.azureml.net), è possibile decidere la **query SQL da usare direttamente nel modulo Importa dati** o salvare in modo definitivo i dati compilati e campionati in una nuova tabella e poi usarla nel modulo [Importa dati][import-data] con un semplice **SELECT * FROM <nome\_della\_nuova\_tabella>**.</span><span class="sxs-lookup"><span data-stu-id="e695b-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on the **SQL query to use directly in the Import Data module** or persist the engineered and sampled data in a new table, which you could use in the [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="e695b-287">In questa sezione verrà creata una nuova tabella per contenere i dati campionati e compilati.</span><span class="sxs-lookup"><span data-stu-id="e695b-287">In this section we will create a new table to hold the sampled and engineered data.</span></span> <span data-ttu-id="e695b-288">Un esempio di query SQL diretta per la creazione di modelli viene fornita nella sezione [Esplorazione dei dati e progettazione di funzionalità in SQL Server](#dbexplore) .</span><span class="sxs-lookup"><span data-stu-id="e695b-288">An example of a direct SQL query for model building is provided in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="e695b-289">Creazione di una tabella di esempio e popolamento con l'1% delle tabelle unite.</span><span class="sxs-lookup"><span data-stu-id="e695b-289">Create a Sample Table and Populate with 1% of the Joined Tables.</span></span> <span data-ttu-id="e695b-290">Innanzitutto eliminare la tabella, se presente.</span><span class="sxs-lookup"><span data-stu-id="e695b-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="e695b-291">In questa sezione, saranno unite le tabelle **nyctaxi\_trip** e **nyctaxi\_fare**, verrà estratto un campione casuale dell'1% e i dati campionati verranno salvati definitivamente in una nuova tabella denominata **nyctaxi\_one\_percent**:</span><span class="sxs-lookup"><span data-stu-id="e695b-291">In this section, we join the tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist the sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="e695b-292">Esplorazione dei dati mediante query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e695b-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="e695b-293">In questa sezione, verranno esplorate le distribuzioni di dati tramite l'1% dei dati campionati salvati in modo definitivo nella nuova tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-293">In this section, we explore data distributions using the 1% sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="e695b-294">Si noti che esplorazioni simili possono essere eseguite usando le tabelle originali, avvalendosi, se lo si desidera, di **TABLESAMPLE** per limitare l'esempio di esplorazione o limitando i risultati a un determinato periodo tramite le partizioni **pickup\_datetime**, come illustrato nella sezione [Esplorazione dei dati e progettazione di funzionalità in SQL Server](#dbexplore).</span><span class="sxs-lookup"><span data-stu-id="e695b-294">Note that similar explorations can be performed using the original tables, optionally using **TABLESAMPLE** to limit the exploration sample or by limiting the results to a given time period using the **pickup\_datetime** partitions, as illustrated in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="e695b-295">Esplorazione: distribuzione giornaliera delle corse</span><span class="sxs-lookup"><span data-stu-id="e695b-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="e695b-296">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e695b-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="e695b-297">Generazione di funzionalità mediante query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e695b-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="e695b-298">In questa sezione verranno generate nuove etichette e funzionalità direttamente mediante query SQL, effettuando operazioni nella tabella di esempio dell'1% creata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e695b-298">In this section we will generate new labels and features directly using SQL queries, operating on the 1% sample table we created in the previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="e695b-299">Generazione di etichette: generazione di etichette di classe</span><span class="sxs-lookup"><span data-stu-id="e695b-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="e695b-300">Nell'esempio seguente, verranno generati due set di etichette da utilizzare per la creazione dei modelli:</span><span class="sxs-lookup"><span data-stu-id="e695b-300">In the following example, we generate two sets of labels to use for modeling:</span></span>

1. <span data-ttu-id="e695b-301">Etichette di classe binaria **tipped** (che forniscono una stima sull'elargizione di una mancia)</span><span class="sxs-lookup"><span data-stu-id="e695b-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="e695b-302">Etichette multiclasse **tip\_class** (che forniscono una stima sul contenitore delle mance o sull'intervallo di queste)</span><span class="sxs-lookup"><span data-stu-id="e695b-302">Multiclass Labels **tip\_class** (predicting the tip bin or range)</span></span>
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="e695b-303">Progettazione di funzionalità: funzionalità di conteggio per le colonne relative alle categorie</span><span class="sxs-lookup"><span data-stu-id="e695b-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="e695b-304">In questo esempio un campo di categoria viene trasformato in un campo numerico mediante la sostituzione di ciascuna categoria con il conteggio delle relative occorrenze nei dati.</span><span class="sxs-lookup"><span data-stu-id="e695b-304">This example transforms a categorical field into a numeric field by replacing each category with the count of its occurrences in the data.</span></span>

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="e695b-305">Progettazione di funzionalità: funzionalità di collocazione per le colonne numeriche</span><span class="sxs-lookup"><span data-stu-id="e695b-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="e695b-306">In questo esempio, un campo numerico continuo viene trasformato in intervalli di categorie predefiniti, vale a dire che il campo numerico verrà trasformato in un campo di categoria.</span><span class="sxs-lookup"><span data-stu-id="e695b-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="e695b-307">Progettazione di funzionalità: funzionalità di estrazione della posizione dalla longitudine/latitudine decimale</span><span class="sxs-lookup"><span data-stu-id="e695b-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="e695b-308">In questo esempio, la rappresentazione decimale di un campo di latitudine o longitudine viene suddivisa in più campi area di diversa granularità, ad esempio, paese, città, paese, quartiere e così via.  Si noti che non viene eseguito il mapping dei nuovi campi geografici alle località effettive.</span><span class="sxs-lookup"><span data-stu-id="e695b-308">This example breaks down the decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that the new geo-fields are not mapped to actual locations.</span></span> <span data-ttu-id="e695b-309">Per informazioni sul mapping delle località con codice geografico, vedere [Servizi REST di Bing Mappe](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="e695b-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

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

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="e695b-310">Verificare l'aspetto finale della tabella con funzionalità</span><span class="sxs-lookup"><span data-stu-id="e695b-310">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="e695b-311">A questo punto è possibile procedere con la creazione e la distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e695b-311">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="e695b-312">I dati sono pronti per eventuali problemi di stima identificati in precedenza, in modo specifico:</span><span class="sxs-lookup"><span data-stu-id="e695b-312">The data is ready for any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="e695b-313">Classificazione binaria: consente di prevedere se per la corsa è stata lasciata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="e695b-313">Binary classification: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="e695b-314">Classificazione multiclasse: consente di prevedere l'intervallo di mance pagato, in base alle classi definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e695b-314">Multiclass classification: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="e695b-315">Attività di regressione: consente di prevedere l'importo della mancia lasciata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="e695b-315">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="e695b-316"><a name="mlmodel"></a>Compilazione di modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e695b-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="e695b-317">Per iniziare l'esercizio relativo alla creazione di modelli, accedere all'area di lavoro Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-317">To begin the modeling exercise, log in to your Azure Machine Learning workspace.</span></span> <span data-ttu-id="e695b-318">Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e695b-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="e695b-319">Per iniziare a utilizzare Azure Machine Learning, vedere [Informazioni su Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="e695b-319">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="e695b-320">Effettuare l'accesso ad [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e695b-320">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="e695b-321">Nella pagina iniziale vengono fornite moltissime informazioni, video, esercitazioni, collegamenti al Riferimento ai moduli e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="e695b-321">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="e695b-322">Per ulteriori informazioni su Azure Machine Learning, consultare il [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="e695b-322">Fore more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="e695b-323">Un tipico esperimento training consiste nelle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-323">A typical training experiment consists of the following:</span></span>

1. <span data-ttu-id="e695b-324">Creazione di un esperimento **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="e695b-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="e695b-325">Ottenere i dati in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-325">Get the data to Azure Machine Learning.</span></span>
3. <span data-ttu-id="e695b-326">Pre-elaborazione, trasformazione e manipolazione dei dati secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="e695b-326">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="e695b-327">Generazione di funzionalità, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e695b-327">Generate features as needed.</span></span>
5. <span data-ttu-id="e695b-328">Suddivisione dei dati in set di dati di training, convalida o test(o creazione di set di dati distinti per ciascuna tipologia).</span><span class="sxs-lookup"><span data-stu-id="e695b-328">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="e695b-329">Selezione di uno o più algoritmi Machine Learning, a seconda del problema di apprendimento da risolvere.</span><span class="sxs-lookup"><span data-stu-id="e695b-329">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="e695b-330">Ad esempio, classificazione binaria, classificazione multiclasse, regressione.</span><span class="sxs-lookup"><span data-stu-id="e695b-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="e695b-331">Training di uno o più modelli tramite il set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="e695b-331">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="e695b-332">Calcolo del punteggio del set di dati di convalida mediante i modelli sottoposti a training.</span><span class="sxs-lookup"><span data-stu-id="e695b-332">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="e695b-333">Valutazione dei modelli per calcolare la metrica rilevante per il problema di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="e695b-333">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="e695b-334">Ottimizzazione dei modelli e selezione del modello migliore per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e695b-334">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="e695b-335">In questo esercizio, i dati sono già stati esplorati e compilati in SQL Server, ed è stata decisa la dimensione del campione da inserire in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-335">In this exercise, we have already explored and engineered the data in SQL Server, and decided on the sample size to ingest in Azure Machine Learning.</span></span> <span data-ttu-id="e695b-336">Per creare uno o più modelli di stima è stato deciso di effettuare le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-336">To build one or more of the prediction models we decided:</span></span>

1. <span data-ttu-id="e695b-337">Inserire i dati in Azure Machine Learning tramite il modulo [Import Data][import-data] (Importa dati), disponibile nella sezione **Data Input and Output** (Input e output dei dati).</span><span class="sxs-lookup"><span data-stu-id="e695b-337">Get the data to Azure Machine Learning using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="e695b-338">Per altre informazioni, vedere la pagina di riferimento sul modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="e695b-338">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Dati di importazione di Azure Machine Learning][17]
2. <span data-ttu-id="e695b-340">Selezione del **Database SQL Azure** come **Origine dati** nel pannello **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="e695b-340">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="e695b-341">Immissione del nome DNS del database nel campo **Nome server database** .</span><span class="sxs-lookup"><span data-stu-id="e695b-341">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="e695b-342">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="e695b-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="e695b-343">Immissione del **Nome database** nel campo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e695b-343">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="e695b-344">Immissione del **Nome utente SQL** in **Nome account utente server e della password in **Password account utente server**.</span><span class="sxs-lookup"><span data-stu-id="e695b-344">Enter the **SQL user name** in the **Server user aqccount name, and the password in the **Server user account password**.</span></span>
6. <span data-ttu-id="e695b-345">Selezione dell'opzione **Accetta qualsiasi certificato server** .</span><span class="sxs-lookup"><span data-stu-id="e695b-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="e695b-346">Nell'area di testo di modifica **Query database** , incollare la query che consente di estrarre i campi di database necessari (inclusi i campi calcolati come le etichette) e sottocampionare i dati nella dimensione campione desiderata.</span><span class="sxs-lookup"><span data-stu-id="e695b-346">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="e695b-347">Nella figura seguente viene fornito un esempio di un esperimento di classificazione binaria in cui si esegue la lettura dei dati direttamente dal database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e695b-347">An example of a binary classification experiment reading data directly from the SQL Server database is in the figure below.</span></span> <span data-ttu-id="e695b-348">È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.</span><span class="sxs-lookup"><span data-stu-id="e695b-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formazione di Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="e695b-350">Negli esempi di estrazione dei dati di modellazione e di query di campionamento forniti nelle sezioni precedenti, **tutte le etichette per i tre esercizi sulla creazione dei modelli sono incluse nella query**.</span><span class="sxs-lookup"><span data-stu-id="e695b-350">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="e695b-351">Un passaggio importante (richiesto) in ciascun esercizio sulla modellazione consiste nell'**escludere** le etichette non necessarie per gli altri due problemi ed eventuali **perdite di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="e695b-351">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="e695b-352">Ad esempio, con la classificazione binaria, usare l'etichetta **tipped** ed escludere i campi **tip\_class**, **tip\_amount** e **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="e695b-352">For e.g., when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="e695b-353">Questi ultimi sono perdite di destinazione in quanto implicano la mancia pagata.</span><span class="sxs-lookup"><span data-stu-id="e695b-353">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="e695b-354">Per escludere le colonne non necessarie e/o le perdite di destinazione, è possibile usare il modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) o [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="e695b-354">To exclude unnecessary columns and/or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="e695b-355">Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="e695b-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="e695b-356"><a name="mldeploy"></a>Distribuzione di modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e695b-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="e695b-357">Quando il modello è pronto, è possibile distribuirlo in modo semplice come servizio Web direttamente dall'esperimento.</span><span class="sxs-lookup"><span data-stu-id="e695b-357">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="e695b-358">Per ulteriori informazioni sulla distribuzione di servizi Web Azure Machine Learning, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e695b-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="e695b-359">Per distribuire un nuovo servizio Web, è necessario effettuare le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-359">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="e695b-360">Creare un esperimento di assegnazione di punteggio.</span><span class="sxs-lookup"><span data-stu-id="e695b-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="e695b-361">Distribuire il servizio web.</span><span class="sxs-lookup"><span data-stu-id="e695b-361">Deploy the web service.</span></span>

<span data-ttu-id="e695b-362">Per creare un esperimento di assegnazione dei punteggi da un esperimento di training **completato**, fare clic su **CREATE SCORING EXPERIMENT** (CREA ESPERIMENTO DI ASSEGNAZIONE PUNTEGGI) nella barra delle azioni inferiore.</span><span class="sxs-lookup"><span data-stu-id="e695b-362">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Valutazione di Azure][18]

<span data-ttu-id="e695b-364">Azure Machine Learning tenterà di creare un esperimento di assegnazione di punteggio basato sui componenti dell'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="e695b-364">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="e695b-365">In particolare, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e695b-365">In particular, it will:</span></span>

1. <span data-ttu-id="e695b-366">Salvataggio del modello sottoposto a training e rimozione dei moduli di training del modello.</span><span class="sxs-lookup"><span data-stu-id="e695b-366">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="e695b-367">Identificazione di una **porta di input** logica per rappresentare lo schema di dati di input previsto.</span><span class="sxs-lookup"><span data-stu-id="e695b-367">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="e695b-368">Identificazione di una **porta di output** logica per rappresentare lo schema di output del servizio Web previsto.</span><span class="sxs-lookup"><span data-stu-id="e695b-368">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="e695b-369">Una volta creato l'esperimento di assegnazione del punteggio, esaminarlo e regolarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e695b-369">When the scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="e695b-370">Una regolazione tipica consiste nel sostituire il set di dati di input e/o la query con uno che escluda i campi etichetta, in quanto questi non saranno disponibili quando si chiama il servizio.</span><span class="sxs-lookup"><span data-stu-id="e695b-370">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="e695b-371">È inoltre buona norma ridurre la dimensione del set di dati di input e/o della query a pochi record, sufficienti a indicare lo schema di input.</span><span class="sxs-lookup"><span data-stu-id="e695b-371">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="e695b-372">Per la porta di output, di solito vengono esclusi tutti i campi di input e inclusi soltanto **Scored Labels** (Etichette con punteggio) e **Scored Probabilities** (Probabilità con punteggio) nell'output, tramite il modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="e695b-372">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e695b-373">Nella figura seguente viene fornito un esperimento di assegnazione di punteggio di esempio.</span><span class="sxs-lookup"><span data-stu-id="e695b-373">A sample scoring experiment is in the figure below.</span></span> <span data-ttu-id="e695b-374">Quando si è pronti per la distribuzione, fare clic sul pulsante **PUBBLICA SERVIZIO WEB** nella barra delle azioni inferiore.</span><span class="sxs-lookup"><span data-stu-id="e695b-374">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Pubblicazione di Azure Machine Learning][11]

<span data-ttu-id="e695b-376">Ricapitolando, in questa esercitazione dettagliata è stato creato un ambiente di analisi scientifica dei dati Azure, è stato utilizzato un set di dati pubblico di grandi dimensioni dall'acquisizione dei dati al training del modello e alla distribuzione di un servizio Web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e695b-376">To recap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all the way from data acquisition to model training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="e695b-377">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="e695b-377">License Information</span></span>
<span data-ttu-id="e695b-378">Questa procedura dettagliata di esempio e gli script e i blocchi di appunti IPython che la accompagnano sono condivisi da Microsoft nella licenza MIT.</span><span class="sxs-lookup"><span data-stu-id="e695b-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="e695b-379">Selezionare il file LICENSE.txt nella directory del codice di esempio in GitHub per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="e695b-379">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="e695b-380">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="e695b-380">References</span></span>
<span data-ttu-id="e695b-381">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="e695b-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="e695b-382">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="e695b-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="e695b-383">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="e695b-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
