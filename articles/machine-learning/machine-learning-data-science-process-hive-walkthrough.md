---
title: dati aaaExplore un Hadoop del cluster e creare modelli in Azure Machine Learning | Documenti Microsoft
description: Utilizzando hello Team processo di analisi scientifica dei dati per uno scenario end-to-end che utilizza un HDInsight Hadoop toobuild del cluster e distribuire un modello usando un set di dati disponibili pubblicamente.
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="be7fe-103">Processo di analisi scientifica dei dati del Team di Hello in azione: cluster di utilizzare Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="be7fe-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="be7fe-104">In questa procedura dettagliata, si usa hello [Team Data Science processo (TDSP)](data-science-process-overview.md) in un scenario end-to-end utilizzando un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare e funzionalità engineer dati hello pubblicamente disponibile [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati e toodown campionare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="be7fe-105">Con Azure Machine Learning toohandle multiclasse e binarie classificazione e regressione delle attività di stima vengono compilati i modelli di dati hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="be7fe-106">Per una procedura dettagliata che illustra come toohandle cluster di un set di dati più grande (1 terabyte) per uno scenario simile utilizzando HDInsight Hadoop per l'elaborazione dati, vedere [processo di analisi scientifica dei dati di Team - i cluster Hadoop HDInsight di Azure utilizzando un set di dati di 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="be7fe-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="be7fe-107">È inoltre possibile toouse un hello tooaccomplish di IPython notebook attività procedura dettagliata di hello presentata tramite set di dati di hello 1 TB.</span><span class="sxs-lookup"><span data-stu-id="be7fe-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="be7fe-108">Gli utenti che sarebbero ad esempio tootry deve consultare questo approccio hello [procedura dettagliata Criteo utilizzando una connessione ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) argomento.</span><span class="sxs-lookup"><span data-stu-id="be7fe-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="be7fe-109"><a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York</span><span class="sxs-lookup"><span data-stu-id="be7fe-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="be7fe-110">dati di andata e ritorno Taxi NYC Hello è di circa 20GB di file compressi valori delimitati da virgole (CSV) (~ 48GB non compressi), che comprendono 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario.</span><span class="sxs-lookup"><span data-stu-id="be7fe-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="be7fe-111">Ogni record di andata e ritorno include il percorso di ritiro e deposito hello e l'ora, hack anonimi (driver) il numero di licenza e numero medallion (id univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="be7fe-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="be7fe-112">dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:</span><span class="sxs-lookup"><span data-stu-id="be7fe-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="be7fe-113">file CSV di Hello 'trip_data' contengono i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="be7fe-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="be7fe-114">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="be7fe-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="be7fe-115">file CSV di Hello 'trip_fare' contengono i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato.</span><span class="sxs-lookup"><span data-stu-id="be7fe-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="be7fe-116">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="be7fe-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="be7fe-117">viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da campi hello: medallion, le maggiori\_titolo e prelievo\_datetime.</span><span class="sxs-lookup"><span data-stu-id="be7fe-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="be7fe-118">tooget tutti di hello dettagli pertinenti tooa particolare di andata e ritorno, è sufficiente toojoin con tre chiavi: hello "medallion", "hack\_licenza" e "prelievo\_datetime".</span><span class="sxs-lookup"><span data-stu-id="be7fe-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="be7fe-119">Vengono descritte alcune ulteriori dettagli dei dati di hello quando è archiviarli in tabelle Hive a breve.</span><span class="sxs-lookup"><span data-stu-id="be7fe-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="be7fe-120"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="be7fe-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="be7fe-121">Quando per raggiungere i dati, determinare il tipo di hello di stime che si desidera toomake in base alle analisi consente di chiarire attività hello che sarà necessario tooinclude del processo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="be7fe-122">Ecco tre esempi di problemi di stima che si risolvono in questa procedura dettagliata il cui formulazione è basato su hello *suggerimento\_quantità*:</span><span class="sxs-lookup"><span data-stu-id="be7fe-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="be7fe-123">**Classificazione binaria**: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="be7fe-124">**Classificazione multiclasse**: intervallo di hello toopredict degli importi di suggerimento pagato viaggi hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="be7fe-125">Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:</span><span class="sxs-lookup"><span data-stu-id="be7fe-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="be7fe-126">**Attività di regressione**: quantità di hello toopredict del suggerimento hello a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="be7fe-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="be7fe-127"><a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi avanzata</span><span class="sxs-lookup"><span data-stu-id="be7fe-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-128">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-129">Per impostare un ambiente Azure per l'analisi avanzata basato su un cluster HDInsight è necessario seguire questa procedura composta da tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="be7fe-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="be7fe-130">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): l'account di archiviazione viene usato per archiviare i dati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="be7fe-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="be7fe-131">dati Hello utilizzati nei cluster di HDInsight si trovano anche qui.</span><span class="sxs-lookup"><span data-stu-id="be7fe-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="be7fe-132">[Personalizzare Azure HDInsight Hadoop cluster per hello avanzate processo Analitica e la tecnologia](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="be7fe-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="be7fe-133">questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="be7fe-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="be7fe-134">Esistono due importanti passaggi tooremember durante la personalizzazione del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be7fe-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="be7fe-135">Ricordare che account di archiviazione hello toolink creato nel passaggio 1 con il cluster HDInsight quando viene creata.</span><span class="sxs-lookup"><span data-stu-id="be7fe-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="be7fe-136">Questo account di archiviazione è tooaccess utilizzati i dati elaborati all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="be7fe-137">Dopo la creazione di cluster hello, abilitare nodo head di accesso remoto a toohello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="be7fe-138">Passare toohello **configurazione** scheda e fare clic su **Abilita modalità remota**.</span><span class="sxs-lookup"><span data-stu-id="be7fe-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="be7fe-139">Questo passaggio consente di specificare le credenziali utente hello usate per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="be7fe-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="be7fe-140">[Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md): area di lavoro questo Azure Machine Learning è modelli di apprendimento toobuild utilizzato.</span><span class="sxs-lookup"><span data-stu-id="be7fe-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="be7fe-141">Questa attività è stato risolto dopo aver completato un'esplorazione dei dati iniziali e verso il basso campionamento utilizzando cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="be7fe-142"><a name="getdata"></a>Ottenere dati hello da un'origine pubblica</span><span class="sxs-lookup"><span data-stu-id="be7fe-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-143">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-144">hello tooget [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati dal percorso pubblico, è possibile utilizzare uno dei metodi di hello descritto in [tooand spostare dati dall'archiviazione Blob di Azure](machine-learning-data-science-move-azure-blob.md) macchina di tooyour toocopy hello dati.</span><span class="sxs-lookup"><span data-stu-id="be7fe-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="be7fe-145">Di seguito viene descritto come usare AzCopy tootransfer hello file contenente i dati.</span><span class="sxs-lookup"><span data-stu-id="be7fe-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="be7fe-146">toodownload e installare AzCopy istruzioni hello in [introduzione hello utilità della riga di comando di AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="be7fe-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="be7fe-147">Da una finestra del prompt dei comandi eseguire hello comandi AzCopy seguente, sostituendo *< path_to_data_folder >* con la destinazione desiderata hello:</span><span class="sxs-lookup"><span data-stu-id="be7fe-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="be7fe-148">Al termine della copia di hello, un totale di file compressi 24 sono nella cartella dati hello scelto.</span><span class="sxs-lookup"><span data-stu-id="be7fe-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="be7fe-149">Decomprimere hello scaricato i file toohello stessa directory nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="be7fe-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="be7fe-150">Prendere nota della cartella hello in cui risiedono i file non compresso hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="be7fe-151">Questa cartella verrà hello cui tooas *< percorso\_a\_unzipped_data\_file\>*  è quello che segue.</span><span class="sxs-lookup"><span data-stu-id="be7fe-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="be7fe-152"><a name="upload"></a>Caricare contenitore del cluster Azure HDInsight Hadoop hello dati toohello predefinito</span><span class="sxs-lookup"><span data-stu-id="be7fe-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-153">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-154">In hello comandi AzCopy seguenti, sostituire hello seguenti parametri con valori reali hello specificata durante la creazione di un cluster Hadoop hello e decomprimere i file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="be7fe-155">***&#60; path_to_data_folder >*** hello directory (percorso) nel computer che contengono file di dati decompresso hello</span><span class="sxs-lookup"><span data-stu-id="be7fe-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="be7fe-156">***&#60; il nome di account di archiviazione del cluster Hadoop >*** hello account di archiviazione associato al cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="be7fe-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="be7fe-157">***&#60; contenitore predefinito del cluster Hadoop >*** contenitore predefinito hello utilizzato dal cluster.</span><span class="sxs-lookup"><span data-stu-id="be7fe-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="be7fe-158">Si noti che nome hello predefinito hello contenitore è in genere hello stesso nome come cluster hello stesso.</span><span class="sxs-lookup"><span data-stu-id="be7fe-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="be7fe-159">Ad esempio, se il cluster hello viene chiamato "abc123.azurehdinsight.net", contenitore predefinito hello è abc123.</span><span class="sxs-lookup"><span data-stu-id="be7fe-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="be7fe-160">***&#60; chiave dell'account di archiviazione >*** hello chiave hello account di archiviazione utilizzato dal cluster</span><span class="sxs-lookup"><span data-stu-id="be7fe-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="be7fe-161">Da un prompt dei comandi o da una finestra di Windows PowerShell nel computer, eseguire hello seguenti due comandi AzCopy.</span><span class="sxs-lookup"><span data-stu-id="be7fe-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="be7fe-162">Questo comando consente di caricare i dati di andata e ritorno hello troppo***nyctaxitripraw*** directory nel contenitore predefinito hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="be7fe-163">Questo comando consente di caricare dati tariffa hello troppo***nyctaxifareraw*** directory nel contenitore predefinito hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="be7fe-164">dati Hello devono ora nell'archiviazione Blob di Azure e pronto toobe utilizzati all'interno del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="be7fe-165"><a name="#download-hql-files"></a>Accedere al nodo head di hello del cluster Hadoop ed e la preparazione per l'analisi esplorativa dei dati</span><span class="sxs-lookup"><span data-stu-id="be7fe-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-166">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-167">nodo head di hello tooaccess del cluster di hello per analisi esplorative dei dati e verso il basso il campionamento dei dati di hello, attenersi alla procedura hello [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="be7fe-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="be7fe-168">In questa procedura dettagliata viene usato principalmente le query scritte [Hive](https://hive.apache.org/), un linguaggio di query simile a SQL, tooperform esplorazioni di raccogliere dati.</span><span class="sxs-lookup"><span data-stu-id="be7fe-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="be7fe-169">le query Hive Hello vengono archiviate nei file .hql.</span><span class="sxs-lookup"><span data-stu-id="be7fe-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="be7fe-170">È quindi verso il basso di esempio questa toobe dati utilizzato all'interno di Azure Machine Learning per la creazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="be7fe-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="be7fe-171">cluster di hello tooprepare per analisi esplorative dei dati, scaricare hello .hql contenenti script Hive appropriati hello da [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa directory (C:\temp) locale nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="be7fe-172">toodo, aprire hello **prompt dei comandi** dall'interno hello nodo head di hello hello cluster e il problema, i due comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="be7fe-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="be7fe-173">Questi due comandi verranno scaricati tutti i file .hql necessari in questa directory locale di questa procedura dettagliata toohello ***C:\temp &#92;*** nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="be7fe-174"><a name="#hive-db-tables"></a>Creare database e tabelle Hive partizionati in base al mese</span><span class="sxs-lookup"><span data-stu-id="be7fe-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-175">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-176">È ora sono tabelle Hive toocreate pronto per il set di dati taxi NYC.</span><span class="sxs-lookup"><span data-stu-id="be7fe-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="be7fe-177">Nel nodo head di hello del cluster Hadoop hello, aprire hello ***della riga di comando Hadoop*** hello desktop del nodo head hello e immettere una directory di Hive hello immettendo il comando hello</span><span class="sxs-lookup"><span data-stu-id="be7fe-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="be7fe-178">**Eseguire tutti i comandi di Hive in questa procedura dettagliata da hello sopra Hive bin / prompt dei comandi. In questo modo, eventuali problemi di percorso verranno risolti automaticamente. Vengono utilizzati termini hello "Hive prompt dei comandi", "bin Hive / prompt dei comandi" e "riga di comando Hadoop" in modo intercambiabile in questa procedura dettagliata.**</span><span class="sxs-lookup"><span data-stu-id="be7fe-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="be7fe-179">Hello Hive prompt dei comandi, digitare hello comando nella riga di comando di Hadoop di tabelle e il nodo head hello toosubmit di hello Hive query Hive toocreate database seguente:</span><span class="sxs-lookup"><span data-stu-id="be7fe-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="be7fe-180">Di seguito è contenuto hello di hello ***C:\temp\sample\_hive\_creare\_db\_e\_tables.hql*** file che crea il database Hive ***nyctaxidb *** e tabelle ***viaggi*** e ***tariffa***.</span><span class="sxs-lookup"><span data-stu-id="be7fe-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="be7fe-181">Questo script Hive crea due tabelle:</span><span class="sxs-lookup"><span data-stu-id="be7fe-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="be7fe-182">tabella "di andata e ritorno" Hello contiene i dettagli di andata e ritorno di ogni interscambio (Dettagli driver, tempo di prelievo, la distanza di andata e ritorno e l'ora)</span><span class="sxs-lookup"><span data-stu-id="be7fe-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="be7fe-183">Nella tabella "tariffa" Hello contiene dettagli tariffa (tariffa, suggerimento importo, pedaggio e supplementi).</span><span class="sxs-lookup"><span data-stu-id="be7fe-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="be7fe-184">Se per un'ulteriore assistenza con queste procedure o tooinvestigate quelli alternativi, vedere sezione hello [query Hive inviare direttamente da hello della riga di comando Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="be7fe-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="be7fe-185"><a name="#load-data"></a>Caricare le tabelle tooHive dati dalle partizioni</span><span class="sxs-lookup"><span data-stu-id="be7fe-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-186">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-187">Hello NYC taxi dispone di un partizionamento naturale per mese, utilizziamo tooenable tempi di elaborazione e query più rapidi.</span><span class="sxs-lookup"><span data-stu-id="be7fe-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="be7fe-188">Hello comandi di PowerShell riportati di seguito (emesso dalla directory di Hive hello utilizzando hello **della riga di comando Hadoop**) caricare dati toohello "viaggi" e "tariffa" Hive tabelle partizionate in base al mese.</span><span class="sxs-lookup"><span data-stu-id="be7fe-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="be7fe-189">Hello *esempio\_hive\_caricare\_dati\_da\_partitions.hql* file contiene i seguenti hello **caricare** comandi.</span><span class="sxs-lookup"><span data-stu-id="be7fe-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="be7fe-190">Si noti che un numero di query Hive che utilizziamo nel processo di esplorazione hello implica la ricerca di in solo una singola partizione o in un paio di partizioni.</span><span class="sxs-lookup"><span data-stu-id="be7fe-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="be7fe-191">Ma è stato possibile eseguire queste query tra tutti i dati hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="be7fe-192"><a name="#show-db"></a>Visualizzare i database in un cluster HDInsight Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="be7fe-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="be7fe-193">database di hello tooshow creati in cluster HDInsight Hadoop all'interno di finestra della riga di comando Hadoop hello eseguire hello nella riga di comando di Hadoop di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="be7fe-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="be7fe-194"><a name="#show-tables"></a>Mostra tabelle Hive hello nel database nyctaxidb hello</span><span class="sxs-lookup"><span data-stu-id="be7fe-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="be7fe-195">tabelle di hello tooshow nel database nyctaxidb hello, eseguire hello nella riga di comando di Hadoop di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="be7fe-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="be7fe-196">È possibile verificare che le tabelle di hello sono partizionate eseguendo il comando hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be7fe-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="be7fe-197">Hello è previsto output è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be7fe-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="be7fe-198">Analogamente, è possibile assicurare che hello tariffa viene partizionata eseguendo il comando hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be7fe-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="be7fe-199">Hello è previsto output è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be7fe-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="be7fe-200"><a name="#explore-hive"></a>Esplorare i dati e progettare le funzionalità in Hive</span><span class="sxs-lookup"><span data-stu-id="be7fe-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-201">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-202">Hello l'esplorazione dei dati e le attività di progettazione per hello dati caricati in tabelle Hive hello possono essere effettuati utilizzando le query Hive di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="be7fe-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="be7fe-203">Di seguito sono riportati alcuni esempi delle attività che si affronteranno in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="be7fe-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="be7fe-204">Consente di visualizzare i record di 10 superiore hello in entrambe le tabelle.</span><span class="sxs-lookup"><span data-stu-id="be7fe-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="be7fe-205">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="be7fe-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="be7fe-206">Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="be7fe-207">Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.</span><span class="sxs-lookup"><span data-stu-id="be7fe-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="be7fe-208">Generare funzioni calcolando le distanze hello diretto di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="be7fe-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="be7fe-209">Esplorazione: Vista hello top 10 record di andata e ritorno tabella</span><span class="sxs-lookup"><span data-stu-id="be7fe-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-210">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-211">toosee quali dati hello sono simile, esamineremo 10 record da ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="be7fe-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="be7fe-212">Eseguire i seguenti due query separatamente dagli hello Hive prompt dei comandi nei record di hello della riga di comando Hadoop console tooinspect hello hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="be7fe-213">tooget hello primi 10 record nella tabella hello "viaggi" dal primo mese di hello:</span><span class="sxs-lookup"><span data-stu-id="be7fe-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="be7fe-214">tooget hello primi 10 record nella tabella hello "tariffa" dal primo mese di hello:</span><span class="sxs-lookup"><span data-stu-id="be7fe-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="be7fe-215">È spesso utile toosave hello record tooa file per la visualizzazione semplice.</span><span class="sxs-lookup"><span data-stu-id="be7fe-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="be7fe-216">Toohello una piccola modifica di sopra di query esegue questa operazione:</span><span class="sxs-lookup"><span data-stu-id="be7fe-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="be7fe-217">Esplorazione: Numero di hello visualizzazione di record in ogni 12 partizioni hello</span><span class="sxs-lookup"><span data-stu-id="be7fe-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-218">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-219">Di interesse è hello variazioni numero hello di trip durante l'anno di calendario hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="be7fe-220">Raggruppamento in base al mese consente toosee questa distribuzione di trip l'aspetto seguente.</span><span class="sxs-lookup"><span data-stu-id="be7fe-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="be7fe-221">Questa operazione produce output di hello:</span><span class="sxs-lookup"><span data-stu-id="be7fe-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="be7fe-222">In questo caso, hello prima colonna è mese hello e hello secondo numero hello di trip per il mese.</span><span class="sxs-lookup"><span data-stu-id="be7fe-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="be7fe-223">È anche possibile conteggio totale hello dei record di questo set di dati di andata e ritorno eseguendo hello comando al prompt dei comandi di hello Hive directory seguente.</span><span class="sxs-lookup"><span data-stu-id="be7fe-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="be7fe-224">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="be7fe-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="be7fe-225">Utilizzando i comandi toothose simili per set di dati di andata e ritorno hello, è possibile rilasciare le query Hive dal prompt di directory hello Hive per hello tariffa dati toovalidate hello numero di set di record.</span><span class="sxs-lookup"><span data-stu-id="be7fe-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="be7fe-226">Questa operazione produce output di hello:</span><span class="sxs-lookup"><span data-stu-id="be7fe-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="be7fe-227">Si noti che viene restituito hello esatta stesso numero di viaggi al mese per entrambi i set di dati.</span><span class="sxs-lookup"><span data-stu-id="be7fe-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="be7fe-228">Questo fornisce la convalida prima di hello che hello dati sono stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="be7fe-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="be7fe-229">Il conteggio hello il numero totale di record nel set di dati tariffa hello può essere eseguito tramite comando hello seguente dal prompt dei comandi di hello Hive directory:</span><span class="sxs-lookup"><span data-stu-id="be7fe-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="be7fe-230">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="be7fe-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="be7fe-231">numero totale di Hello di record in entrambe le tabelle è inoltre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="be7fe-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="be7fe-232">Ciò fornisce una convalida secondo tale hello dati sono stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="be7fe-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="be7fe-233">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="be7fe-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-234">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-235">In questo esempio identifica medallion hello (numeri taxi) con più di 100 trip all'interno di un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="be7fe-236">vantaggi di query Hello da hello partizionata accesso alla tabella poiché condizionato, dalla variabile partizione hello **mese**.</span><span class="sxs-lookup"><span data-stu-id="be7fe-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="be7fe-237">risultati della query Hello scritte tooa file locale queryoutput.tsv in `C:\temp` nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="be7fe-238">Di seguito è contenuto hello di *esempio\_hive\_viaggi\_conteggio\_da\_medallion.hql* file per l'ispezione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="be7fe-239">medallion Hello nel set di dati di hello NYC taxi identifica un file cab univoco.</span><span class="sxs-lookup"><span data-stu-id="be7fe-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="be7fe-240">È possibile identificare i taxi "occupati" chiedendo quali di essi hanno effettuato più di un determinato numero di corse in un intervallo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="be7fe-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="be7fe-241">esempio Hello identifica file CAB che ha effettuato più di cento viaggi in hello primi tre mesi, e Salva hello risultati tooa locale file di query C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="be7fe-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="be7fe-242">Di seguito è contenuto hello di *esempio\_hive\_viaggi\_conteggio\_da\_medallion.hql* file per l'ispezione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="be7fe-243">Da hello Hive prompt dei comandi, problema hello comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be7fe-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="be7fe-244">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="be7fe-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-245">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-246">Durante l'esplorazione di un set di dati, è spesso necessario numero hello tooexamine di co-occorrenze dei gruppi di valori.</span><span class="sxs-lookup"><span data-stu-id="be7fe-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="be7fe-247">In questa sezione viene fornito un esempio di come toodo per a quelle driver.</span><span class="sxs-lookup"><span data-stu-id="be7fe-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="be7fe-248">Hello *esempio\_hive\_viaggi\_conteggio\_da\_medallion\_license.hql* dati tariffa hello impostata su "medallion" e "hack_license" dei gruppi di file e restituisce i conteggi di ogni combinazione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="be7fe-249">Di seguito è riportato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="be7fe-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="be7fe-250">Questa query restituisce le combinazioni dei taxi e degli autisti, visualizzate in ordine decrescente in base al numero di corse.</span><span class="sxs-lookup"><span data-stu-id="be7fe-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="be7fe-251">Da hello Hive prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="be7fe-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="be7fe-252">risultati della query Hello vengono scritti i file locale tooa C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="be7fe-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="be7fe-253">Esplorazione: valutazione della qualità dei dati mediante il controllo del record di longitudine/latitudine non validi</span><span class="sxs-lookup"><span data-stu-id="be7fe-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-254">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-255">Degli obiettivi comune di analisi esplorativa dei dati è tooweed i record non valido.</span><span class="sxs-lookup"><span data-stu-id="be7fe-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="be7fe-256">Hello riportato in questa sezione determina se sia hello longitudine o latitudine campi contengono un valore molto di fuori di hello area NYC.</span><span class="sxs-lookup"><span data-stu-id="be7fe-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="be7fe-257">Poiché è probabile che i record contengono un valori di latitudine, longitudine errato, è necessario tooeliminate da tutti i dati che sono toobe utilizzati per la modellazione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="be7fe-258">Di seguito è contenuto hello di *esempio\_hive\_qualità\_assessment.hql* file per l'ispezione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="be7fe-259">Da hello Hive prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="be7fe-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="be7fe-260">Hello *-S* argomento incluso in questo comando Elimina l'immagine di schermata hello lo stato dei processi di MapReduce Hive hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="be7fe-261">Ciò è utile perché rende più leggibile di output della query Hive stampa schermata hello di hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="be7fe-262">Esplorazione: distribuzioni in classi binarie delle mance delle corse</span><span class="sxs-lookup"><span data-stu-id="be7fe-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-263">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-264">Per il problema di classificazione binaria hello descritto nella hello [esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sezione, è utile tooknow se è stato specificato un suggerimento o non.</span><span class="sxs-lookup"><span data-stu-id="be7fe-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="be7fe-265">Questa distribuzione delle mance è di tipo binario:</span><span class="sxs-lookup"><span data-stu-id="be7fe-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="be7fe-266">mancia offerta (classe 1, tip\_amount > $ 0)</span><span class="sxs-lookup"><span data-stu-id="be7fe-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="be7fe-267">nessuna mancia (classe 0, tip\_amount = $ 0).</span><span class="sxs-lookup"><span data-stu-id="be7fe-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="be7fe-268">Hello *esempio\_hive\_inclinato\_frequencies.hql* esegue questa operazione file riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="be7fe-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="be7fe-269">Da hello Hive prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="be7fe-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="be7fe-270">: Esplorazione Le distribuzioni di classe in base alle impostazioni hello multiclasse</span><span class="sxs-lookup"><span data-stu-id="be7fe-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-271">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-272">Problema di classificazione multiclasse hello descritte nella hello [esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sezione questo set di dati può anche essere applicato tooa di classificazione naturale in cui desideriamo quantità hello toopredict dei suggerimenti hello specificato.</span><span class="sxs-lookup"><span data-stu-id="be7fe-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="be7fe-273">È possibile usare gli intervalli di bin toodefine suggerimento nella query hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="be7fe-274">tooget hello distribuzioni di classe per hello diversi intervalli di suggerimento, utilizziamo hello *esempio\_hive\_suggerimento\_intervallo\_frequencies.hql* file.</span><span class="sxs-lookup"><span data-stu-id="be7fe-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="be7fe-275">Di seguito è riportato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="be7fe-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="be7fe-276">Eseguire hello comando seguente dalla riga di comando Hadoop console:</span><span class="sxs-lookup"><span data-stu-id="be7fe-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="be7fe-277">Esplorazione: calcolare la distanza diretta tra due posizioni di latitudine e longitudine</span><span class="sxs-lookup"><span data-stu-id="be7fe-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-278">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-279">Presenza di una misura della distanza diretto hello consente toofind out discrepanza hello tra i file e hello effettivo attivarsi distanza.</span><span class="sxs-lookup"><span data-stu-id="be7fe-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="be7fe-280">Questa funzionalità è motivare identificando che potrebbero essere minore di passeggeri tootip probabile se essi individuare tale driver hello è intenzionalmente usato li da strada molto più lunga.</span><span class="sxs-lookup"><span data-stu-id="be7fe-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="be7fe-281">confronto di hello toosee tra distanza effettiva di andata e ritorno e hello [distanza Haversine](http://en.wikipedia.org/wiki/Haversine_formula) tra i due punti di longitudine latitudine (distanza di hello "circle eccellente"), utilizziamo funzioni trigonometriche hello disponibili all'interno di Hive, in questo modo:</span><span class="sxs-lookup"><span data-stu-id="be7fe-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="be7fe-282">Nella query hello sopra, R è raggio hello hello terra in miglia e pi greco è tooradians convertito.</span><span class="sxs-lookup"><span data-stu-id="be7fe-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="be7fe-283">Si noti che i punti di longitudine latitudine hello sono i valori "filtrato" tooremove distanti da area NYC hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="be7fe-284">In questo caso, è scrivere la directory dei risultati tooa chiamato "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="be7fe-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="be7fe-285">Hello sequenza di comandi illustrata di seguito crea innanzitutto la directory di output e quindi esegue hello Hive.</span><span class="sxs-lookup"><span data-stu-id="be7fe-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="be7fe-286">Da hello Hive prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="be7fe-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="be7fe-287">Hello risultati della query vengono scritti i BLOB Azure too9 ***queryoutputdir/000000\_0*** troppo ***queryoutputdir/000008\_0*** sotto il contenitore predefinito hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="be7fe-288">dimensioni di hello toosee dei singoli BLOB hello, eseguiamo hello comando seguente dal prompt dei comandi di hello Hive directory:</span><span class="sxs-lookup"><span data-stu-id="be7fe-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="be7fe-289">contenuto di hello toosee di un determinato file, ad esempio 000000\_0, utilizziamo Hadoop `copyToLocal` comando, di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="be7fe-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="be7fe-290">In presenza di file di grandi dimensioni, l'operazione `copyToLocal` può essere molto lenta e non è quindi consigliabile.</span><span class="sxs-lookup"><span data-stu-id="be7fe-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="be7fe-291">Dei principali vantaggi di avere tali dati si trovano in un blob di Azure è che si può esplorare i dati di hello all'interno di Azure Machine Learning che usano hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="be7fe-292"><a name="#downsample"></a>Sottocampionare i dati e creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="be7fe-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="be7fe-293">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="be7fe-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="be7fe-294">Dopo la fase di analisi esplorativa dati hello, siamo ora in dati di hello esempio toodown pronto per la creazione di modelli in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="be7fe-295">In questa sezione viene illustrato come eseguire una query toodown dati esempio hello, che sono quindi accessibile dalla hello toouse un Hive [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="be7fe-296">Il campionamento dei dati hello verso il basso</span><span class="sxs-lookup"><span data-stu-id="be7fe-296">Down sampling hello data</span></span>
<span data-ttu-id="be7fe-297">Questa procedura si articola in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="be7fe-297">There are two steps in this procedure.</span></span> <span data-ttu-id="be7fe-298">Innanzitutto è aggiungere hello **nyctaxidb.trip** e **nyctaxidb.fare** tabelle in tre le chiavi presenti in tutti i record: "medallion", "hack\_licenza", e "prelievo\_datetime".</span><span class="sxs-lookup"><span data-stu-id="be7fe-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="be7fe-299">È quindi possibile generare un'etichetta di classificazione binaria **tipped** e un'etichetta di classificazione multiclasse **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="be7fe-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="be7fe-300">toobe toouse in grado di hello verso il basso dati campionati direttamente da hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, è necessario toostore risultati di hello di hello sopra la tabella query tooan interna Hive.</span><span class="sxs-lookup"><span data-stu-id="be7fe-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="be7fe-301">In seguito, si crea una tabella interna di Hive e popola il relativo contenuto con hello unita e verso il basso dati campionati.</span><span class="sxs-lookup"><span data-stu-id="be7fe-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="be7fe-302">query Hello applica funzioni standard di Hive direttamente il toogenerate hello ora del giorno, settimana dell'anno, giorno della settimana (1 sta per lunedì e 7 sta per domenica) da hello "prelievo\_datetime" campo e hello distanza diretta tra il prelievo di hello e dropoff percorsi.</span><span class="sxs-lookup"><span data-stu-id="be7fe-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="be7fe-303">Gli utenti possono fare riferimento troppo[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) per un elenco completo di tali funzioni.</span><span class="sxs-lookup"><span data-stu-id="be7fe-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="be7fe-304">Hello query quindi verso il basso di dati di campioni hello in modo che i risultati della query hello rientrino in hello Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="be7fe-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="be7fe-305">Solo circa l'1% del set di dati originale hello viene importato in hello Studio.</span><span class="sxs-lookup"><span data-stu-id="be7fe-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="be7fe-306">Di seguito sono contenuti hello di *esempio\_hive\_preparare\_per\_aml\_full.hql* in grado di preparare i dati per il modello di compilazione in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="be7fe-307">toorun questa query, dalla directory Hive hello richiesta:</span><span class="sxs-lookup"><span data-stu-id="be7fe-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="be7fe-308">Avere una tabella interna "nyctaxidb.nyctaxi_downsampled_dataset", che è possibile accedere tramite hello [l'importazione dei dati] [ import-data] modulo da Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="be7fe-309">Inoltre, sarà possibile usare questo set di dati per la creazione di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="be7fe-310">Usare il modulo di importazione dei dati hello in hello tooaccess Azure Machine Learning verso il basso dati campionati</span><span class="sxs-lookup"><span data-stu-id="be7fe-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="be7fe-311">Prerequisiti per eseguire una query Hive in hello [l'importazione dei dati] [ import-data] modulo di Azure Machine Learning, è necessario accedere tooan Azure Machine Learning area di lavoro e accedere alle credenziali toohello di hello cluster e il relativo account di archiviazione associato.</span><span class="sxs-lookup"><span data-stu-id="be7fe-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="be7fe-312">Alcuni dettagli su hello [l'importazione dei dati] [ import-data] modulo e hello tooinput parametri:</span><span class="sxs-lookup"><span data-stu-id="be7fe-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="be7fe-313">**URI del server HCatalog**: se il nome del cluster hello abc123, allora si tratta semplicemente: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="be7fe-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="be7fe-314">**Nome dell'account utente Hadoop** : nome utente hello scelto per il cluster hello (**non** nome utente di accesso remoto hello)</span><span class="sxs-lookup"><span data-stu-id="be7fe-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="be7fe-315">**Password dell'account utente Hadoop** : password hello scelta per il cluster hello (**non** password di accesso remoto hello)</span><span class="sxs-lookup"><span data-stu-id="be7fe-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="be7fe-316">**Percorso dei dati di output** : si è scelto toobe Azure.</span><span class="sxs-lookup"><span data-stu-id="be7fe-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="be7fe-317">**Nome dell'account di archiviazione Azure** : nome dell'account di archiviazione predefinito hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="be7fe-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="be7fe-318">**Nome del contenitore di Azure** : nome del contenitore predefinito hello per cluster hello è e viene in genere hello stesso come nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="be7fe-319">Per un cluster denominato "abc123", il nome del contenitore è semplicemente abc123.</span><span class="sxs-lookup"><span data-stu-id="be7fe-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be7fe-320">**Qualsiasi tabella a cui si desidera tooquery utilizzando hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning deve essere una tabella interna.**</span><span class="sxs-lookup"><span data-stu-id="be7fe-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="be7fe-321">Di seguito è riportato un suggerimento per determinare se una tabella T in un database D.db è una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="be7fe-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="be7fe-322">Da hello Hive prompt dei comandi, problema hello comando:</span><span class="sxs-lookup"><span data-stu-id="be7fe-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="be7fe-323">Se la tabella hello è una tabella interna e viene compilata, il relativo contenuto deve essere visualizzato qui.</span><span class="sxs-lookup"><span data-stu-id="be7fe-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="be7fe-324">Un altro modo toodetermine, se la tabella è una tabella interna è toouse hello Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="be7fe-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="be7fe-325">Utilizzare il nome del contenitore predefinito toohello toonavigate del cluster hello e quindi filtrare in base al nome di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="be7fe-326">Se la tabella hello e il relativo contenuto è presente, questo errore conferma che è una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="be7fe-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="be7fe-327">Ecco uno snapshot della query Hive hello e hello [l'importazione dei dati] [ import-data] modulo:</span><span class="sxs-lookup"><span data-stu-id="be7fe-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Query Hive per il modulo di importazione dei dati](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="be7fe-329">Si noti che poiché il nostro giù dati campionati risiedono nel contenitore predefinito hello, query Hive risultante hello da Azure Machine Learning è molto semplice ed è solo un "Seleziona * da nyctaxidb.nyctaxi\_sottocampionate\_dati".</span><span class="sxs-lookup"><span data-stu-id="be7fe-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="be7fe-330">set di dati Hello può ora essere usato come punto di partenza per la creazione di modelli di Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="be7fe-331"><a name="mlmodel"></a>Creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="be7fe-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="be7fe-332">Sono ora in grado di tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="be7fe-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="be7fe-333">dati Hello sono pronti per noi toouse nella risoluzione dei problemi di stima hello identificati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="be7fe-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="be7fe-334">**1. Classificazione binaria**: toopredict o meno un suggerimento è stato pagato per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="be7fe-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="be7fe-335">**Strumento di apprendimento usato:** regressione logistica a due classi</span><span class="sxs-lookup"><span data-stu-id="be7fe-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="be7fe-336">a.</span><span class="sxs-lookup"><span data-stu-id="be7fe-336">a.</span></span> <span data-ttu-id="be7fe-337">Per questo problema, l'etichetta (o classe) di destinazione è "tipped".</span><span class="sxs-lookup"><span data-stu-id="be7fe-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="be7fe-338">Il set di dati sottocampionati originale dispone di alcune colonne che indicano le perdite di destinazione per questo esperimento di classificazione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="be7fe-339">In particolare: suggerimento\_classe, suggerimento\_quantità e totale\_importo rivelare informazioni etichetta di destinazione hello che non è disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="be7fe-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="be7fe-340">È rimuovere queste colonne dalla considerazione utilizzando hello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="be7fe-341">snapshot Hello seguente mostra il nostro toopredict esperimento o meno un suggerimento è stato pagato per un determinato andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="be7fe-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="be7fe-343">b.</span><span class="sxs-lookup"><span data-stu-id="be7fe-343">b.</span></span> <span data-ttu-id="be7fe-344">Per questo esperimento, le distribuzioni dell'etichetta di destinazione sono approssimativamente 1:1.</span><span class="sxs-lookup"><span data-stu-id="be7fe-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="be7fe-345">snapshot Hello riportato di seguito mostra distribuzione hello etichette di classe suggerimento per il problema di classificazione binaria hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Distribuzione delle etichette della classe relativa alla mancia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="be7fe-347">Di conseguenza, si ottengono un AUC di 0.987 come illustrato nella figura che segue hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Valore AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="be7fe-349">**2. Classificazione multiclasse**: intervallo di hello toopredict degli importi di suggerimento pagato viaggi hello, utilizzate in precedenza hello classi definite.</span><span class="sxs-lookup"><span data-stu-id="be7fe-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="be7fe-350">**Strumento di apprendimento usato:** regressione logistica multiclasse</span><span class="sxs-lookup"><span data-stu-id="be7fe-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="be7fe-351">a.</span><span class="sxs-lookup"><span data-stu-id="be7fe-351">a.</span></span> <span data-ttu-id="be7fe-352">Per questo problema, l'etichetta (o classe) di destinazione è "tip\_class", che può assumere uno dei cinque valori (0, 1, 2, 3, 4).</span><span class="sxs-lookup"><span data-stu-id="be7fe-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="be7fe-353">Come nel caso di classificazione binaria hello, sono disponibili alcune colonne che sono le perdite di destinazione per questa sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="be7fe-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="be7fe-354">In particolare: inclinato, suggerimento\_importo totale\_importo rivelare informazioni etichetta di destinazione hello che non è disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="be7fe-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="be7fe-355">È rimuovere queste colonne con hello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="be7fe-356">Hello snapshot seguente viene illustrato il nostro toopredict esperimento collocazione un suggerimento è probabilmente toofall (classe 0: suggerimento = $0, la classe 1: suggerimento > $0 e suggerimento < = $5, classe 2: suggerimento > $5 e suggerimento < = $10, classe 3: suggerimento > 10 e suggerimento < = $20 Classe 4: suggerimento > $20)</span><span class="sxs-lookup"><span data-stu-id="be7fe-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="be7fe-358">Di seguito è illustrata la distribuzione della classe di test effettiva.</span><span class="sxs-lookup"><span data-stu-id="be7fe-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="be7fe-359">Vediamo che mentre la classe 0 e 1 di classe sono più comuni, hello altre classi sono rari.</span><span class="sxs-lookup"><span data-stu-id="be7fe-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Distribuzione della classe di test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="be7fe-361">b.</span><span class="sxs-lookup"><span data-stu-id="be7fe-361">b.</span></span> <span data-ttu-id="be7fe-362">Per questo esercizio, usato un toolook di una matrice di confusione l'accuratezza della stima.</span><span class="sxs-lookup"><span data-stu-id="be7fe-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="be7fe-363">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="be7fe-363">This is shown below.</span></span>

![Matrice di confusione](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="be7fe-365">Si noti che mentre le accuratezze la classe in classi prevalente hello è abbastanza efficace, modello hello non esegue un processo valido di "apprendimento" nelle classi rari hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="be7fe-366">**3. Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.</span><span class="sxs-lookup"><span data-stu-id="be7fe-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="be7fe-367">**Strumento di apprendimento usato:** albero delle decisioni con boosting</span><span class="sxs-lookup"><span data-stu-id="be7fe-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="be7fe-368">a.</span><span class="sxs-lookup"><span data-stu-id="be7fe-368">a.</span></span> <span data-ttu-id="be7fe-369">Per questo problema, l'etichetta (o classe) di destinazione è "tiptip\_amount".</span><span class="sxs-lookup"><span data-stu-id="be7fe-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="be7fe-370">In questo caso sono i problemi di destinazione: inclinato, suggerimento\_(classe), totale\_quantità, tutte queste variabili rivelare informazioni sulla quantità di suggerimento hello che non è in genere disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="be7fe-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="be7fe-371">È rimuovere queste colonne con hello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="be7fe-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="be7fe-372">Hello snapshot belows Mostra la quantità di hello toopredict esperimento di hello suggerimento fornito.</span><span class="sxs-lookup"><span data-stu-id="be7fe-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="be7fe-374">b.</span><span class="sxs-lookup"><span data-stu-id="be7fe-374">b.</span></span> <span data-ttu-id="be7fe-375">Per i problemi di regressione è misurare le accuratezze hello del nostro stima esaminando l'errore quadrato hello nelle stime hello, hello coefficiente di determinazione e hello come.</span><span class="sxs-lookup"><span data-stu-id="be7fe-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="be7fe-376">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="be7fe-376">We show these below.</span></span>

![Statistiche di stima](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="be7fe-378">È possibile notare che sulla hello coefficiente di determinazione 0.709, implicando 71% circa della varianza hello è spiegato dai nostri coefficienti di modello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be7fe-379">informazioni su Azure Machine Learning toolearn e come tooaccess e usarlo, vedere troppo[novità Machine Learning?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="be7fe-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="be7fe-380">Una risorsa molto utile per la riproduzione con una serie di esperimenti di Machine Learning in Azure Machine Learning è hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="be7fe-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="be7fe-381">Raccolta di Hello riguarda una gamma di esperimenti e viene fornita un'introduzione approfondita nell'intervallo di hello delle funzionalità di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="be7fe-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="be7fe-382">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="be7fe-382">License Information</span></span>
<span data-ttu-id="be7fe-383">In questa procedura dettagliata di esempio e i relativi script associati vengono condivisi da Microsoft con licenza MIT hello.</span><span class="sxs-lookup"><span data-stu-id="be7fe-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="be7fe-384">Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.</span><span class="sxs-lookup"><span data-stu-id="be7fe-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="be7fe-385">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="be7fe-385">References</span></span>
<span data-ttu-id="be7fe-386">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="be7fe-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="be7fe-387">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="be7fe-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="be7fe-388">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="be7fe-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
