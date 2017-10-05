---
title: Esplorare i dati in un cluster Hadoop e di creare modelli in Azure Machine Learning | Documentazione Microsoft
description: Uso del Processo di analisi scientifica dei dati per i team per uno scenario end-to-end in cui un cluster Hadoop di HDInsight viene usato per creare e distribuire un modello con un set di dati disponibile pubblicamente.
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
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="2e2cd-103">Processo di analisi scientifica dei dati per i team in azione: uso dei cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2cd-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="2e2cd-104">In questa procedura dettagliata si usa il [Processo di analisi scientifica dei dati per i team (TDSP)](data-science-process-overview.md) in uno scenario end-to-end usufruendo di un [cluster Hadoop di Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) per archiviare, esplorare e acquisire dati di progettazione del set di dati relativo alle [corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/) disponibile pubblicamente, nonché sottocampionarli.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="2e2cd-105">I modelli dei dati sono creati con Azure Machine Learning in modo da gestire la classificazione binaria e multiclasse e attività predittive di regressione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="2e2cd-106">Per una procedura dettagliata su come gestire un set di dati più grande (1 terabyte) in uno scenario simile in cui si usano i cluster Hadoop di HDInsight per l'elaborazione dei dati, vedere [Processo di analisi scientifica dei dati per i team: uso di cluster Hadoop di Azure HDInsight su un set di dati da 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="2e2cd-107">Per eseguire le attività presentate in questa procedura con un set di dati da 1 TB, è anche possibile usare IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="2e2cd-108">Se si vuole provare questo approccio, vedere l'argomento relativo alla [procedura dettagliata Criteo con una connessione Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="2e2cd-109"><a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York</span><span class="sxs-lookup"><span data-stu-id="2e2cd-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="2e2cd-110">I dati relativi alle corse dei taxi di NYC sono rappresentati come file csv compressi e di dimensione pari a 20 GB (48 GB non compressi); questi comprendono informazioni su oltre 173 milioni di corse singole e sulle tariffe pagate.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="2e2cd-111">Il record di ogni corsa include la località di partenza e di arrivo, il numero di patente anonimo (del tassista) e il numero di licenza (ID univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="2e2cd-112">I dati sono relativi a tutte le corse per l'anno 2013 e vengono forniti nei due set di dati seguenti per ciascun mese:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="2e2cd-113">I file con estensione csv "trip_data" contengono i dettagli delle corse, ad esempio il numero dei passeggeri, i punti di partenza e arrivo, la durata e la lunghezza della corsa.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="2e2cd-114">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="2e2cd-115">I file con estensione csv "trip_fare" contengono i dettagli della tariffa pagata per ciascuna corsa, ad esempio tipo di pagamento, importo, soprattassa e tasse, mance e pedaggi e l'importo totale pagato.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="2e2cd-116">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="2e2cd-117">La chiave univoca che consente di unire trip\_data e trip\_fare è composta dai campi: medallion, hack\_licence e pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="2e2cd-118">Per ottenere tutti i dettagli relativi a una corsa specifica, è sufficiente creare un join con tre chiavi: "medallion", "hack\_license" e "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="2e2cd-119">Altri dettagli relativi ai dati verranno forniti a breve, quando se ne eseguirà l'archiviazione nelle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="2e2cd-120"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="2e2cd-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="2e2cd-121">Prima di usare i dati, è opportuno stabilire il tipo di stima che si desidera ottenere dall'analisi, in modo da comprendere meglio le attività che devono essere incluse nel processo.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="2e2cd-122">Di seguito sono riportati tre esempi di problemi di previsione che verranno affrontati in questa procedura dettagliata e la cui formulazione si basa sul valore *tip\_amount*:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="2e2cd-123">**Classificazione binaria**: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="2e2cd-124">**Classificazione multiclasse**: consente di prevedere l'intervallo in cui si inserisce l'importo della mancia pagata per la corsa.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="2e2cd-125">Il valore *tip\_amount* viene suddiviso in cinque bin o classi:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="2e2cd-126">**Attività di regressione**: consente di prevedere l'importo della mancia pagata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="2e2cd-127"><a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi avanzata</span><span class="sxs-lookup"><span data-stu-id="2e2cd-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-128">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-129">Per impostare un ambiente Azure per l'analisi avanzata basato su un cluster HDInsight è necessario seguire questa procedura composta da tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="2e2cd-130">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): l'account di archiviazione viene usato per archiviare i dati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="2e2cd-131">Anche i dati usati nei cluster HDInsight vengono archiviati in questa posizione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="2e2cd-132">[Personalizzare i cluster Hadoop di Azure HDInsight per Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="2e2cd-133">questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="2e2cd-134">Quando si personalizza un cluster HDInsight, è importante non dimenticare due passaggi importanti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="2e2cd-135">Collegare l'account di archiviazione creato nel passaggio 1 al cluster HDInsight al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="2e2cd-136">Questo account di archiviazione, infatti, viene usato per accedere ai dati elaborati all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="2e2cd-137">Dopo aver creato il cluster, abilitare l'accesso remoto al relativo nodo head.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="2e2cd-138">Passare alla scheda **Configurazione** e fare clic su **Abilita modalità remota**.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="2e2cd-139">Questo passaggio consente di specificare le credenziali utente da usare per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="2e2cd-140">[Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md): questa area di lavoro di Azure Machine Learning viene usata per creare modelli di apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="2e2cd-141">Questa attività viene eseguita dopo aver completato un'analisi iniziale dei dati e aver eseguito un'operazione di sottocampionamento con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="2e2cd-142"><a name="getdata"></a>Acquisire i dati da un'origine pubblica</span><span class="sxs-lookup"><span data-stu-id="2e2cd-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-143">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-144">Per acquisire il set di dati [Corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/) dal relativo percorso pubblico, è possibile usare uno dei metodi descritti in [Spostamento dei dati da e verso l'archiviazione BLOB di Azure](machine-learning-data-science-move-azure-blob.md) e copiare i dati nel nuovo computer.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="2e2cd-145">Si descrive ora come usare AzCopy per trasferire i file contenenti i dati.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="2e2cd-146">Per scaricare e installare AzCopy, seguire le istruzioni fornite in [Introduzione all'utilità della riga di comando AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="2e2cd-147">Da una finestra del prompt dei comandi, eseguire i seguenti comandi AzCopy sostituendo *<path_to_data_folder>* con la destinazione desiderata:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="2e2cd-148">Al termine dell'operazione di copia, nella cartella dati scelta sarà presente un totale di 24 file compressi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="2e2cd-149">Decomprimere i file scaricati nella stessa directory del computer locale.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="2e2cd-150">Prendere nota della cartella in cui si trovano i dati non compressi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="2e2cd-151">Si farà riferimento a questa cartella come *<path\_to\_unzipped_data\_files\>* che segue.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="2e2cd-152"><a name="upload"></a>Caricare i dati nel contenitore predefinito del cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2cd-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-153">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-154">Nei seguenti comandi AzCopy, sostituire i parametri seguenti con i valori effettivi specificati durante la creazione del cluster Hadoop e decomprimere i file di dati.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="2e2cd-155">***&#60;path_to_data_folder>***: la directory (insieme al percorso) sul computer contenente i file di dati non compressi</span><span class="sxs-lookup"><span data-stu-id="2e2cd-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="2e2cd-156">***&#60;storage account name of Hadoop cluster>***: l'account di archiviazione associato al cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2cd-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="2e2cd-157">***&#60;default container of Hadoop cluster>***: il contenitore predefinito usato dal cluster</span><span class="sxs-lookup"><span data-stu-id="2e2cd-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="2e2cd-158">Il nome del contenitore predefinito corrisponde in genere al nome del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="2e2cd-159">Ad esempio, se il nome del cluster è "abc123.azurehdinsight.net", quello del contenitore predefinito sarà abc123.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="2e2cd-160">***&#60;storage account key>***: la chiave dell'account di archiviazione usato dal cluster</span><span class="sxs-lookup"><span data-stu-id="2e2cd-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="2e2cd-161">Da un prompt dei comandi o una finestra di Windows PowerShell nel computer, eseguire i due comandi AzCopy seguenti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="2e2cd-162">Questo comando consente di caricare i dati delle corse nella directory ***nyctaxitripraw*** all'interno del contenitore predefinito del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="2e2cd-163">Questo comando consente di caricare i dati delle tariffe nella directory ***nyctaxifareraw*** all'interno del contenitore predefinito del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="2e2cd-164">I dati si trovano ora nell'archiviazione BLOB di Azure e sono pronti per essere usati all'interno del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="2e2cd-165"><a name="#download-hql-files"></a>Accedere al nodo head del cluster Hadoop e preparare l'analisi esplorativa dei dati</span><span class="sxs-lookup"><span data-stu-id="2e2cd-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-166">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-167">Per accedere al nodo head del cluster per l'analisi esplorativa e il sottocampionamento dei dati, seguire la procedura descritta in [Accedere al nodo head del cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="2e2cd-168">In questa procedura dettagliata si useranno essenzialmente query scritte in [Hive](https://hive.apache.org/), un linguaggio di query di tipo SQL per l'esecuzione di analisi preliminari dei dati.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="2e2cd-169">Le query Hive vengono archiviate in file con estensione hql.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="2e2cd-170">Si effettuerà quindi il sottocampionamento dei dati da usare in Azure Machine Learning per la creazione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="2e2cd-171">Per preparare il cluster per l'analisi esplorativa dei dati, i file con estensione .hql con i relativi script Hive vengono scaricati da [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) in una directory locale (C:\temp) del nodo head.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="2e2cd-172">A questo scopo, aprire il **prompt dei comandi** dal nodo head del cluster ed eseguire i due comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="2e2cd-173">Questi due comandi consentiranno di scaricare tutti i file con estensione .hql necessari in questa procedura nella directory locale ***C:\temp&#92;*** del nodo head.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="2e2cd-174"><a name="#hive-db-tables"></a>Creare database e tabelle Hive partizionati in base al mese</span><span class="sxs-lookup"><span data-stu-id="2e2cd-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-175">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-176">È ora possibile creare tabelle Hive per il set di dati sui taxi di New York.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="2e2cd-177">Nel nodo head del cluster Hadoop, aprire la ***riga di comando di Hadoop*** sul desktop del nodo head e specificare la directory Hive immettendo il comando</span><span class="sxs-lookup"><span data-stu-id="2e2cd-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="2e2cd-178">**Eseguire tutti i comandi di Hive in questa procedura dettagliata dal prompt della directory bin/ Hive sopra indicato. In questo modo, eventuali problemi di percorso verranno risolti automaticamente. I termini "prompt della directory Hive", "prompt della directory/del bin Hive" e "riga di comando di Hadoop" verranno usati in modo intercambiabile in questo documento.**</span><span class="sxs-lookup"><span data-stu-id="2e2cd-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="2e2cd-179">Dal prompt della directory Hive, immettere il comando seguente nella riga di comando di Hadoop del nodo head per inviare query Hive per la creazione di database e tabelle Hive:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="2e2cd-180">Di seguito è riportato il contenuto del file ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql***, che consente di creare il database Hive ***nyctaxidb*** e le tabelle ***trip*** e ***fare***.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="2e2cd-181">Questo script Hive crea due tabelle:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="2e2cd-182">la tabella "trip" che contiene i dettagli relativi alle corse (informazioni sull'autista, ora di prelievo, distanza e tempo della corsa) e</span><span class="sxs-lookup"><span data-stu-id="2e2cd-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="2e2cd-183">la tabella "fare" che contiene dettagli relativi alle tariffe (importo della tariffa, importo della mancia, pedaggio ed eventuali supplementi).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="2e2cd-184">Per ricevere maggiore assistenza per lo svolgimento di queste procedure o per conoscere procedure alternative, vedere la sezione [Inviare query Hive direttamente dalla riga di comando di Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="2e2cd-185"><a name="#load-data"></a>Caricare i dati nelle tabelle Hive in base alle partizioni</span><span class="sxs-lookup"><span data-stu-id="2e2cd-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-186">In genere, questa attività viene svolta da un **amministratore** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-187">Il set di dati sui taxi di New York presenta un partizionamento naturale per mese, utile per velocizzare i tempi di elaborazione e ridurre la durata delle query.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="2e2cd-188">I comandi di PowerShell seguenti (specificati dalla directory Hive tramite la **riga di comando di Hadoop**) caricano i dati nelle tabelle Hive "trip" e "fare" partizionate per mese.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="2e2cd-189">Il file *sample\_hive\_load\_data\_by\_partitions.hql* contiene i comandi **LOAD** seguenti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="2e2cd-190">Alcune query Hive a cui si ricorrerà più avanti nel corso del processo di esplorazione prevedono l'uso di un'unica o al massimo due partizioni.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="2e2cd-191">Queste query, tuttavia, possono essere eseguite sull'intero set di dati.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="2e2cd-192"><a name="#show-db"></a>Visualizzare i database nel cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2cd-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="2e2cd-193">Per visualizzare i database creati nel cluster Hadoop di HDInsight nella finestra della riga di comando di Hadoop, eseguire il comando seguente nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="2e2cd-194"><a name="#show-tables"></a>Visualizzare le tabelle Hive nel database nyctaxidb</span><span class="sxs-lookup"><span data-stu-id="2e2cd-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="2e2cd-195">Per visualizzare le tabelle nel database nyctaxidb, eseguire il seguente comando nella riga di comando di Hadoop:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="2e2cd-196">È possibile verificare che le tabelle siano partizionate eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="2e2cd-197">Di seguito è riportato l'output previsto:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="2e2cd-198">Analogamente, è possibile verificare che la tabella "fare" sia partizionata eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="2e2cd-199">Di seguito è riportato l'output previsto:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-199">The expected output is shown below:</span></span>

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

## <span data-ttu-id="2e2cd-200"><a name="#explore-hive"></a>Esplorare i dati e progettare le funzionalità in Hive</span><span class="sxs-lookup"><span data-stu-id="2e2cd-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-201">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-202">Le attività di esplorazione dei dati e di progettazione delle funzionalità relative ai dati caricati nelle tabelle Hive possono essere eseguite usando le query Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="2e2cd-203">Di seguito sono riportati alcuni esempi delle attività che si affronteranno in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="2e2cd-204">Visualizzazione dei i 10 record principali in entrambe le tabelle.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="2e2cd-205">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="2e2cd-206">Indagine sulla qualità dei dati dei campi di longitudine e latitudine.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="2e2cd-207">Generazione di etichette di classificazione binaria e multiclasse basata su **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="2e2cd-208">Creazione di funzionalità calcolando le distanze dirette delle corse.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="2e2cd-209">Esplorazione: visualizzare i 10 record principali nella tabella delle corse</span><span class="sxs-lookup"><span data-stu-id="2e2cd-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-210">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-211">Per visualizzare la natura dei dati, verranno esaminati 10 record di ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="2e2cd-212">Eseguire separatamente le due query seguenti dal prompt della directory Hive nella console della riga di comando di Hadoop per analizzare i record.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="2e2cd-213">Per ottenere i primi 10 record della tabella "trip" dal primo mese:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="2e2cd-214">Per ottenere i primi 10 record della tabella "fare" dal primo mese:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="2e2cd-215">Per una maggiore comodità di visualizzazione, è spesso utile salvare i record in un file.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="2e2cd-216">Una piccola modifica alla query precedente esegue questa operazione:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="2e2cd-217">Esplorazione: visualizzare il numero di record in ognuna delle 12 partizioni</span><span class="sxs-lookup"><span data-stu-id="2e2cd-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-218">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-219">È interessante osservare come il numero delle corse subisca sensibili variazioni nel corso dell'anno.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="2e2cd-220">Il raggruppamento in base al mese consente di vedere come sono distribuite le corse.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="2e2cd-221">Viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-221">This gives us the output :</span></span>

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

<span data-ttu-id="2e2cd-222">In questa tabella, la prima colonna è il mese e la seconda il numero di corse effettuate nel mese.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="2e2cd-223">È inoltre possibile contare il numero totale di record nel set di dati delle corse eseguendo il comando seguente al prompt della directory Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="2e2cd-224">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="2e2cd-225">Usando comandi simili a quelli illustrati per il set di dati delle corse, è possibile eseguire query Hive dal prompt della directory Hive per il set di dati delle tariffe in modo da convalidare il numero di record.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="2e2cd-226">Viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-226">This gives us the output:</span></span>

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

<span data-ttu-id="2e2cd-227">Osservare come per entrambi i set di dati venga restituito lo stesso numero di corse mensili.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="2e2cd-228">Questo costituisce la prima conferma che i dati sono stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="2e2cd-229">Per contare il numero totale di record nel set di dati delle tariffe è possibile usare il comando seguente dal prompt della directory Hive:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="2e2cd-230">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="2e2cd-231">Anche il numero totale di record coincide in entrambe le tabelle.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="2e2cd-232">Questo costituisce la seconda conferma che i dati sono stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="2e2cd-233">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="2e2cd-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-234">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-235">In questo esempio viene identificata la licenza (numero del taxi) che ha eseguito più di 100 corse in un determinato periodo.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="2e2cd-236">Per la query verrà usata la tabella partizionata poiché è condizionata dalla variabile di partizione **month**.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="2e2cd-237">I risultati della query vengono scritti nel file locale queryoutput.tsv presente nella directory `C:\temp` del nodo head.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="2e2cd-238">Di seguito è riportato il contenuto del file *sample\_hive\_trip\_count\_by\_medallion.hql* per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="2e2cd-239">Nel set di dati relativo ai taxi di New York, la licenza identifica un taxi univoco.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="2e2cd-240">È possibile identificare i taxi "occupati" chiedendo quali di essi hanno effettuato più di un determinato numero di corse in un intervallo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="2e2cd-241">L'esempio seguente identifica i taxi che hanno effettuato oltre cento corse nei primi tre mesi e salva i risultati della query in un file locale: C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="2e2cd-242">Di seguito è riportato il contenuto del file *sample\_hive\_trip\_count\_by\_medallion.hql* per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="2e2cd-243">Dal prompt della directory Hive eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="2e2cd-244">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="2e2cd-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-245">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-246">Durante l'esplorazione di un set di dati, spesso si desidera esaminare il numero di co-occorrenze di gruppi di valori.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="2e2cd-247">L'esempio fornito in questa sezione illustra come eseguire questa operazione per i taxi e gli autisti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="2e2cd-248">Il file *sample\_hive\_trip\_count\_by\_medallion\_license.hql* raggruppa il set di dati delle tariffe in "medallion" e "hack_license" e restituisce la quantità di ogni combinazione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="2e2cd-249">Di seguito è riportato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="2e2cd-250">Questa query restituisce le combinazioni dei taxi e degli autisti, visualizzate in ordine decrescente in base al numero di corse.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="2e2cd-251">Dal prompt della directory Hive eseguire:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="2e2cd-252">I risultati della query vengono scritti nel file locale C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="2e2cd-253">Esplorazione: valutazione della qualità dei dati mediante il controllo del record di longitudine/latitudine non validi</span><span class="sxs-lookup"><span data-stu-id="2e2cd-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-254">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-255">Un obiettivo comune di analisi esplorativa dei dati è quello di eliminare i record non validi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="2e2cd-256">L'esempio riportato in questa sezione determina se i campi di longitudine o latitudine contengono un valore esterno all'area di New York.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="2e2cd-257">Poiché è probabile che in questi record siano presenti valori di longitudine/latitudine errati, è opportuno eliminarli da tutti i dati che dovranno essere usati per la modellazione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="2e2cd-258">Di seguito è riportato il contenuto del file *sample\_hive\_quality\_assessment.hql* per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="2e2cd-259">Dal prompt della directory Hive eseguire:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="2e2cd-260">L'argomento *-S* incluso in questo comando sostituisce l'immagine della schermata di stato relativa ai processi Map/Reduce di Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="2e2cd-261">Ciò è utile poiché rende più leggibile l'immagine relativa alla schermata dell'output della query Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="2e2cd-262">Esplorazione: distribuzioni in classi binarie delle mance delle corse</span><span class="sxs-lookup"><span data-stu-id="2e2cd-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-263">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-264">Per il problema di classificazione binaria descritto nella sezione [Esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , è utile sapere se è stata offerta una mancia.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="2e2cd-265">Questa distribuzione delle mance è di tipo binario:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="2e2cd-266">mancia offerta (classe 1, tip\_amount > $ 0)</span><span class="sxs-lookup"><span data-stu-id="2e2cd-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="2e2cd-267">nessuna mancia (classe 0, tip\_amount = $ 0).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="2e2cd-268">Il file *sample\_hive\_tipped\_frequencies.hql* di seguito consente di sapere se è stata offerta una mancia.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="2e2cd-269">Al prompt della directory Hive eseguire:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="2e2cd-270">Esplorazione: distribuzioni in classi nell'impostazione multiclasse</span><span class="sxs-lookup"><span data-stu-id="2e2cd-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-271">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-272">Per il problema di classificazione multiclasse descritto nella sezione [Esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , questo set di dati si presta a una classificazione naturale in cui si desidera stimare l'importo delle mance offerte.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="2e2cd-273">Per definire gli intervalli di mance nella query, è possibile usare i contenitori.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="2e2cd-274">Per ottenere le distribuzioni in classi per i vari intervalli di mance, si userà il file *sample\_hive\_tip\_range\_frequencies.hql*.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="2e2cd-275">Di seguito è riportato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-275">Below are its contents.</span></span>

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

<span data-ttu-id="2e2cd-276">Eseguire il seguente comando dalla console della riga di comando di Hadoop:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="2e2cd-277">Esplorazione: calcolare la distanza diretta tra due posizioni di latitudine e longitudine</span><span class="sxs-lookup"><span data-stu-id="2e2cd-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-278">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-279">La disponibilità di una misura della distanza diretta consente di rilevare eventuali discrepanze con la distanza effettiva della corsa.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="2e2cd-280">Questa funzionalità è stata motivata sottolineando come un passeggero sarebbe probabilmente meno incline a offrire una mancia se intuisse che l'autista ha intenzionalmente compiuto un percorso più lungo.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="2e2cd-281">Per visualizzare il confronto tra la distanza effettiva della corsa e la [distanza Haversine](http://en.wikipedia.org/wiki/Haversine_formula) tra due punti di latitudine-longitudine (distanza "grande-cerchio"), si useranno le funzioni trigonometriche disponibili in Hive., pertanto:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="2e2cd-282">Nella query sopra riportata, R è il raggio della terra in miglia e il pi greco viene convertito in radianti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="2e2cd-283">I punti di latitudine/longitudine, inoltre, sono stati "filtrati" in modo da rimuovere i valori esterni all'area di New York.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="2e2cd-284">In questo caso, i risultati vengono scritti in una directory denominata "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="2e2cd-285">La sequenza di comandi seguente crea questa directory di output, quindi esegue il comando Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="2e2cd-286">Al prompt della directory Hive eseguire:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="2e2cd-287">I risultati della query vengono scritti in nove BLOB di Azure (da ***queryoutputdir/000000\_0*** a ***queryoutputdir/000008\_0***), all'interno del contenitore predefinito del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="2e2cd-288">Per visualizzare le dimensioni dei singoli BLOB, è possibile eseguire il comando seguente dal prompt della directory Hive:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="2e2cd-289">Per visualizzare il contenuto di un file specifico, ad esempio 000000\_0, si userà invece il comando `copyToLocal` di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="2e2cd-290">In presenza di file di grandi dimensioni, l'operazione `copyToLocal` può essere molto lenta e non è quindi consigliabile.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="2e2cd-291">Uno dei vantaggi derivanti dalla disponibilità dei dati in un BLOB di Azure è la possibilità di esplorarli in Azure Machine Learning usando il modulo [Import Data][import-data].</span><span class="sxs-lookup"><span data-stu-id="2e2cd-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="2e2cd-292"><a name="#downsample"></a>Sottocampionare i dati e creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2e2cd-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="2e2cd-293">In genere, questa attività viene svolta da un **data scientist** .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="2e2cd-294">Dopo la fase di analisi esplorativa, si passerà ora a eseguire il sottocampionamento dei dati per la creazione di modelli in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="2e2cd-295">Questa sezione illustra come usare una query Hive per eseguire il sottocampionamento dei dati, a cui sarà possibile accedere dal lettore [Import Data][import-data] di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="2e2cd-296">Sottocampionare i dati</span><span class="sxs-lookup"><span data-stu-id="2e2cd-296">Down sampling the data</span></span>
<span data-ttu-id="2e2cd-297">Questa procedura si articola in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-297">There are two steps in this procedure.</span></span> <span data-ttu-id="2e2cd-298">Innanzitutto è necessario aggiungere le tabelle **nyctaxidb.trip** e **nyctaxidb.fare** a tre chiavi presenti in tutti i record: "medallion", "hack\_license" e "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="2e2cd-299">È quindi possibile generare un'etichetta di classificazione binaria **tipped** e un'etichetta di classificazione multiclasse **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="2e2cd-300">Per usare il sottocampionamento dei dati direttamente dal modulo [Import Data][import-data] in Azure Machine Learning, è necessario archiviare i risultati della query precedente in una tabella interna di Hive.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="2e2cd-301">Di seguito viene creata una tabella interna di Hive e ne viene popolato il contenuto con i dati sottocampionati e sottoposti a join.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="2e2cd-302">La query applica funzioni standard di Hive direttamente per generare l'ora del giorno, la settimana dell'anno, il giorno della settimana (1 indica lunedì e 7 indica domenica) dal campo "pickup\_datetime" e la distanza diretta tra i percorsi di partenza e arrivo.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="2e2cd-303">Per un elenco completo di queste funzionalità, gli utenti possono fare riferimento alla [funzionalità definita dall'utente LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) .</span><span class="sxs-lookup"><span data-stu-id="2e2cd-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="2e2cd-304">La query consente quindi di eseguire il sottocampionamento dei dati; in questo modo, i risultati della query possono adattarsi ad Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="2e2cd-305">Solo l'1% del set di dati originale viene importato in Studio.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="2e2cd-306">Di seguito sono riportati i contenuti del file *sample\_hive\_prepare\_for\_aml\_full.hql* che prepara i dati per la creazione del modello in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

        --- now insert contents of the join into the above internal table

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

<span data-ttu-id="2e2cd-307">Per eseguire questa query, dal prompt della directory di Hive eseguire:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="2e2cd-308">È ora disponibile una tabella interna "nyctaxidb.nyctaxi_downsampled_dataset" alla quale è possibile accedere tramite il modulo [Import Data][import-data] di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="2e2cd-309">Inoltre, sarà possibile usare questo set di dati per la creazione di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="2e2cd-310">Utilizzare il modulo Import Data in Azure Machine Learning per accedere ai dati sottocampionati</span><span class="sxs-lookup"><span data-stu-id="2e2cd-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="2e2cd-311">I prerequisiti necessari per l'inoltro di query Hive nel modulo [Import Data][import-data] di Azure Machine Learning sono l'accesso a un'area di lavoro di Azure Machine Learning e l'accesso alle credenziali del cluster e al relativo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="2e2cd-312">Di seguito sono elencate informazioni dettagliate sul modulo [Import Data][import-data] e sui parametri di input:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="2e2cd-313">**URI del server HCatalog**: se il nome del cluster è abc123, l'URI è semplicemente: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="2e2cd-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="2e2cd-314">**Nome dell'account utente di Hadoop**: il nome utente scelto per il cluster (**non** il nome utente di accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="2e2cd-315">**Password dell'account utente di Hadoop**: la password scelta per il cluster (**non** la password di accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="2e2cd-316">**Percorso dei dati di output** : ossia Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="2e2cd-317">**Nome dell'account di archiviazione di Azure** : nome dell'account di archiviazione predefinito associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="2e2cd-318">**Nome del contenitore di Azure** : nome del contenitore predefinito per il cluster, in genere corrisponde al nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="2e2cd-319">Per un cluster denominato "abc123", il nome del contenitore è semplicemente abc123.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e2cd-320">**Qualsiasi tabella su cui si desidera eseguire una query tramite il modulo [Import Data][import-data] di Azure Machine Learning deve essere una tabella interna.**</span><span class="sxs-lookup"><span data-stu-id="2e2cd-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="2e2cd-321">Di seguito è riportato un suggerimento per determinare se una tabella T in un database D.db è una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="2e2cd-322">Al prompt della directory Hive eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="2e2cd-323">Se la tabella è una tabella interna e viene popolata, il relativo contenuto deve essere visualizzato in questa posizione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="2e2cd-324">Un altro modo per determinare se una tabella è una tabella interna consiste nell'usare Esplora archivi Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="2e2cd-325">Questo strumento consente di passare al nome del contenitore del cluster predefinito e quindi filtrare in base al nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="2e2cd-326">Se la tabella e il relativo contenuto vengono visualizzati, allora si tratta di una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="2e2cd-327">Di seguito è riportato uno snapshot della query Hive e del modulo [Import Data][import-data]:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Query Hive per il modulo di importazione dei dati](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="2e2cd-329">Si noti che poiché i dati sottocampionati risiedono nel contenitore predefinito, la query Hive risultante da Azure Machine Learning è molto semplice ed è di tipo "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="2e2cd-330">È ora possibile usare il set di dati come punto di partenza per la creazione di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="2e2cd-331"><a name="mlmodel"></a>Creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2e2cd-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="2e2cd-332">A questo punto è possibile procedere con la creazione e la distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="2e2cd-333">I dati possono essere ora usati per risolvere i problemi relativi alle stime indicati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="2e2cd-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="2e2cd-334">**1. Classificazione binaria**: consente di prevedere se per la corsa è stata pagata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="2e2cd-335">**Strumento di apprendimento usato:** regressione logistica a due classi</span><span class="sxs-lookup"><span data-stu-id="2e2cd-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="2e2cd-336">a.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-336">a.</span></span> <span data-ttu-id="2e2cd-337">Per questo problema, l'etichetta (o classe) di destinazione è "tipped".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="2e2cd-338">Il set di dati sottocampionati originale dispone di alcune colonne che indicano le perdite di destinazione per questo esperimento di classificazione.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="2e2cd-339">In particolare: tip\_class, tip\_amount e total\_amount contengono informazioni sull'etichetta di destinazione non disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="2e2cd-340">È possibile rimuovere queste colonne dalla valutazione tramite il modulo [Select Columns in Dataset][select-columns].</span><span class="sxs-lookup"><span data-stu-id="2e2cd-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="2e2cd-341">Lo snapshot seguente illustra un esperimento in cui si prevede se per una corsa è stata pagata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="2e2cd-343">b.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-343">b.</span></span> <span data-ttu-id="2e2cd-344">Per questo esperimento, le distribuzioni dell'etichetta di destinazione sono approssimativamente 1:1.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="2e2cd-345">Lo snapshot seguente illustra la distribuzione delle etichette della classe relativa alla mancia per il problema di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![Distribuzione delle etichette della classe relativa alla mancia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="2e2cd-347">Di conseguenza, si ottengono un valore di AUC di 0,987 come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![Valore AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="2e2cd-349">**2. Classificazione multiclasse**: consente di stimare l'intervallo di mance pagate per una corsa in base alle classi definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="2e2cd-350">**Strumento di apprendimento usato:** regressione logistica multiclasse</span><span class="sxs-lookup"><span data-stu-id="2e2cd-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="2e2cd-351">a.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-351">a.</span></span> <span data-ttu-id="2e2cd-352">Per questo problema, l'etichetta (o classe) di destinazione è "tip\_class", che può assumere uno dei cinque valori (0, 1, 2, 3, 4).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="2e2cd-353">Come nel caso della classificazione binaria, sono presenti alcune colonne che indicano le perdite di destinazione per questo esperimento.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="2e2cd-354">In particolare: tipped, tip\_amount e total\_amount contengono informazioni sull'etichetta di destinazione non disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="2e2cd-355">È possibile rimuovere queste colonne tramite il modulo [Select Columns in Dataset][select-columns].</span><span class="sxs-lookup"><span data-stu-id="2e2cd-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="2e2cd-356">Lo snapshot seguente illustra l'esperimento che stima la possibile collocazione di una mancia (Classe 0: mancia = $ 0, classe 1: mancia > $ 0 e <= $ 5, classe 2: mancia > $ 5 e <= $ 10, classe 3: mancia > $ 10 e <= $ 20, classe 4: mancia > $ 20)</span><span class="sxs-lookup"><span data-stu-id="2e2cd-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="2e2cd-358">Di seguito è illustrata la distribuzione della classe di test effettiva.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="2e2cd-359">Si noti che, mentre la classe 0 e 1 sono prevalenti, le altre classi sono meno frequenti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![Distribuzione della classe di test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="2e2cd-361">b.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-361">b.</span></span> <span data-ttu-id="2e2cd-362">Per questo esperimento, si usa una matrice di confusione per esaminare l'accuratezza della stima.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="2e2cd-363">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-363">This is shown below.</span></span>

![Matrice di confusione](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="2e2cd-365">Si noti che mentre la precisione è abbastanza efficace in relazione alle classi più diffuse, il modello non ottiene un buon risultato di "apprendimento" sulle classi meno frequenti.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="2e2cd-366">**3. Attività di regressione**: consente di prevedere l'importo della mancia pagata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="2e2cd-367">**Strumento di apprendimento usato:** albero delle decisioni con boosting</span><span class="sxs-lookup"><span data-stu-id="2e2cd-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="2e2cd-368">a.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-368">a.</span></span> <span data-ttu-id="2e2cd-369">Per questo problema, l'etichetta (o classe) di destinazione è "tiptip\_amount".</span><span class="sxs-lookup"><span data-stu-id="2e2cd-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="2e2cd-370">In questo caso, le perdite di destinazione sono tipped, tip\_class e total\_amount; tutte queste variabili contengono informazioni sull'importo della mancia che non è in genere disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="2e2cd-371">È possibile rimuovere queste colonne tramite il modulo [Select Columns in Dataset][select-columns].</span><span class="sxs-lookup"><span data-stu-id="2e2cd-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="2e2cd-372">Lo snapshot seguente illustra l'esperimento che stima l'importo della mancia pagata.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="2e2cd-374">b.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-374">b.</span></span> <span data-ttu-id="2e2cd-375">Per problemi di regressione, l'accuratezza della stima viene misurata esaminando l'errore quadratico nelle stime, il coefficiente di determinazione e altri parametri simili,</span><span class="sxs-lookup"><span data-stu-id="2e2cd-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="2e2cd-376">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-376">We show these below.</span></span>

![Statistiche di stima](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="2e2cd-378">Si noti che il coefficiente di determinazione è 0,709, che implica che circa il 71% della varianza è rappresentato dai coefficienti del modello.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e2cd-379">Per altre informazioni su Azure Machine Learning e su come accedere e usare il servizio, consultare [Cos'è Azure Machine Learning?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="2e2cd-380">Una risorsa molto utile per la riproduzione di una serie di esperimenti di Machine Learning su Azure Machine Learning è [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="2e2cd-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="2e2cd-381">La raccolta include una vasta gamma di esperimenti e fornisce un'introduzione approfondita alle varie funzionalità di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="2e2cd-382">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="2e2cd-382">License Information</span></span>
<span data-ttu-id="2e2cd-383">Questa procedura di esempio e gli script contenuti sono forniti da Microsoft con licenza MIT.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="2e2cd-384">Selezionare il file LICENSE.txt nella directory del codice di esempio in GitHub per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2e2cd-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="2e2cd-385">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="2e2cd-385">References</span></span>
<span data-ttu-id="2e2cd-386">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="2e2cd-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="2e2cd-387">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="2e2cd-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="2e2cd-388">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="2e2cd-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
