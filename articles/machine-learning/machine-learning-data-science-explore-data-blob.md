---
title: dati aaaExplore in Azure blob storage con Pandas | Documenti Microsoft
description: Tooexplore i dati archiviati in Azure blob come contenitore utilizzando Pandas.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="b65b7-103">Esplorare i dati nell'archiviazione BLOB di Azure con Pandas</span><span class="sxs-lookup"><span data-stu-id="b65b7-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="b65b7-104">Questo documento descrive come tooexplore i dati archiviati in Azure blob contenitore usando [Pandas](http://pandas.pydata.org/) pacchetto Python.</span><span class="sxs-lookup"><span data-stu-id="b65b7-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="b65b7-105">esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b65b7-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="b65b7-106">Questa attività è un passaggio di hello [il processo di analisi scientifica dei dati]().</span><span class="sxs-lookup"><span data-stu-id="b65b7-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="b65b7-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b65b7-107">Prerequisites</span></span>
<span data-ttu-id="b65b7-108">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="b65b7-108">This article assumes that you have:</span></span>

* <span data-ttu-id="b65b7-109">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b65b7-109">Created an Azure storage account.</span></span> <span data-ttu-id="b65b7-110">Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b65b7-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="b65b7-111">I dati sono stati archiviati in un account di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b65b7-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="b65b7-112">Se sono necessarie istruzioni, vedere [tooand di spostamento dei dati da archiviazione di Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="b65b7-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="b65b7-113">Caricare i dati di hello in un frame di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="b65b7-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="b65b7-114">tooexplore e modificare un set di dati, deve prima essere scaricato da hello blob tooa locale file di origine, che può quindi essere caricato in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="b65b7-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="b65b7-115">Di seguito sono hello passaggi toofollow per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b65b7-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="b65b7-116">Scaricare dati hello da Azure blob con hello seguente esempio di codice Python mediante il servizio blob.</span><span class="sxs-lookup"><span data-stu-id="b65b7-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="b65b7-117">Sostituire la variabile hello nel seguente codice con i valori specifici hello:</span><span class="sxs-lookup"><span data-stu-id="b65b7-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="b65b7-118">Lettura dati hello in un frame di dati Pandas da hello scaricati i file.</span><span class="sxs-lookup"><span data-stu-id="b65b7-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="b65b7-119">Ora pronto tooexplore hello dati, generare funzioni in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="b65b7-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="b65b7-120"><a name="blob-dataexploration"></a>Esempi di esplorazione dei dati utilizzando Pandas</span><span class="sxs-lookup"><span data-stu-id="b65b7-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="b65b7-121">Ecco alcuni esempi di modalità dati tooexplore Pandas utilizzando:</span><span class="sxs-lookup"><span data-stu-id="b65b7-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="b65b7-122">Controllare hello **numero di righe e colonne**</span><span class="sxs-lookup"><span data-stu-id="b65b7-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="b65b7-123">**Controllare** hello alcuni primo o ultimi **righe** in hello seguente set di dati:</span><span class="sxs-lookup"><span data-stu-id="b65b7-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="b65b7-124">Controllare hello **tipo di dati** ogni colonna è stato importato come usando hello seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="b65b7-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="b65b7-125">Controllare hello **statistiche di base** per colonne hello hello set di dati, come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="b65b7-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="b65b7-126">Esaminare il numero di hello di voci per ogni valore di colonna come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="b65b7-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="b65b7-127">**Conteggio dei valori mancanti** rispetto al numero effettivo di hello di voci in ogni colonna utilizzando hello seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="b65b7-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="b65b7-128">Se dispone di **valori mancanti** per una colonna specifica in dati hello, è possibile rilasciarli come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b65b7-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="b65b7-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="b65b7-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="b65b7-130">Un altro modo tooreplace i valori mancanti è con funzione di modalità hello:</span><span class="sxs-lookup"><span data-stu-id="b65b7-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="b65b7-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="b65b7-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="b65b7-132">Creare un **istogramma** tracciato con un numero variabile di distribuzione di hello tooplot bin di una variabile</span><span class="sxs-lookup"><span data-stu-id="b65b7-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="b65b7-133">Esaminare **correlazioni** tra le variabili utilizzando un scatterplot o funzione di correlazione incorporata hello</span><span class="sxs-lookup"><span data-stu-id="b65b7-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

