---
title: "Creare funzionalità per i dati di archiviazione BLOB di Azure mediante Panda | Microsoft Docs"
description: "Come creare funzionalità per i dati archiviati nel contenitore BLOB di Azure mediante il pacchetto Python di Panda."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="37b58-103">Creare funzionalità per i dati di archiviazione BLOB di Azure tramite Panda</span><span class="sxs-lookup"><span data-stu-id="37b58-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="37b58-104">Questo documento tratta come creare funzionalità per i dati archiviati nel contenitore BLOB di Azure mediante il pacchetto Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="37b58-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="37b58-105">Una volta mostrato come caricare i dati in un frame di dati Panda, viene illustrato come generare funzionalità relative alle categorie usando script Python con i valori di indicatore e funzionalità per la creazione di contenitori.</span><span class="sxs-lookup"><span data-stu-id="37b58-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="37b58-106">Questo **menu** fornisce collegamenti ad argomenti che descrivono come creare funzionalità per dati in diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="37b58-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="37b58-107">Questa attività è un passaggio del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="37b58-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37b58-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="37b58-108">Prerequisites</span></span>
<span data-ttu-id="37b58-109">Questo articolo si basa sul presupposto che sia stato creato un account di archiviazione BLOB di Azure e vi siano stati archiviati dati.</span><span class="sxs-lookup"><span data-stu-id="37b58-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="37b58-110">Per istruzioni su come configurare un account, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="37b58-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="37b58-111">Caricare i dati in un intervallo di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="37b58-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="37b58-112">Per esplorare e modificare un set di dati, i dati devono essere scaricati dall'origine BLOB in un file locale che può essere quindi caricato in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="37b58-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="37b58-113">Ecco i passaggi da seguire per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="37b58-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="37b58-114">Scaricare i dati da BLOB Azure con il codice Python di esempio riportato di seguito utilizzando il servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="37b58-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="37b58-115">Sostituire la variabile nel codice riportato di seguito con i valori specifici:</span><span class="sxs-lookup"><span data-stu-id="37b58-115">Replace the variable in the code below with your specific values:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="37b58-116">Leggere i dati in un frame di dati Pandas dal file scaricato.</span><span class="sxs-lookup"><span data-stu-id="37b58-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="37b58-117">A questo punto si è pronti per esplorare i dati e generare le funzionalità di questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="37b58-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="37b58-118"><a name="blob-featuregen"></a>Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="37b58-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="37b58-119">Le due sezioni successive illustrano come generare caratteristiche relative alle categorie con i valori dell'indicatore e caratteristiche per la creazione di contenitori mediante gli script di Python.</span><span class="sxs-lookup"><span data-stu-id="37b58-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="37b58-120"><a name="blob-countfeature"></a>Valore dell'indicatore basato sulla creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="37b58-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="37b58-121">Le funzionalità relative alle categorie possono essere create come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="37b58-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="37b58-122">Controllare la distribuzione della colonna relativa alla categoria:</span><span class="sxs-lookup"><span data-stu-id="37b58-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="37b58-123">Generare i valori dell'indicatore per ognuno dei valori della colonna</span><span class="sxs-lookup"><span data-stu-id="37b58-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="37b58-124">Unire la colonna indicatore con il frame di dati originale</span><span class="sxs-lookup"><span data-stu-id="37b58-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="37b58-125">Rimuovere la variabile originale:</span><span class="sxs-lookup"><span data-stu-id="37b58-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="37b58-126"><a name="blob-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="37b58-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="37b58-127">Per creare funzionalità in contenitori, procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="37b58-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="37b58-128">Aggiungere una sequenza di colonne per suddividere una colonna numerica</span><span class="sxs-lookup"><span data-stu-id="37b58-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="37b58-129">Convertire la creazione di contenitori in una sequenza di variabili booleane</span><span class="sxs-lookup"><span data-stu-id="37b58-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="37b58-130">Infine, aggiungere di nuovo le variabili fittizie al frame di dati originale</span><span class="sxs-lookup"><span data-stu-id="37b58-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="37b58-131"><a name="sql-featuregen"></a>Scrittura dei dati nel BLOB di Azure e utilizzo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="37b58-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="37b58-132">Dopo avere esaminato i dati e creato le funzionalità necessarie, è possibile caricare i dati (campionati o completi) in un BLOB di Azure e utilizzarli in Azure Machine Learning attenendosi alla procedura seguente. Tenere presente che le funzionalità aggiuntive possono essere create anche in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="37b58-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="37b58-133">Scrivere il frame di dati in file locali</span><span class="sxs-lookup"><span data-stu-id="37b58-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="37b58-134">Caricare i dati nel BLOB di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="37b58-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="37b58-135">Ora i dati possono essere letti dal BLOB utilizzando il modulo [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) di Azure Machine Learning, come illustrato nella schermata riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="37b58-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![lettore BLOB](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

