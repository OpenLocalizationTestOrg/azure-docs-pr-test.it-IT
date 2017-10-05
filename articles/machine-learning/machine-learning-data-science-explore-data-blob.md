---
title: Esplorare i dati nell'archiviazione BLOB di Azure con Pandas | Microsoft Docs
description: Come esplorare i dati archiviati nel contenitore BLOB di Azure utilizzando Pandas.
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="3a8fe-103">Esplorare i dati nell'archiviazione BLOB di Azure con Pandas</span><span class="sxs-lookup"><span data-stu-id="3a8fe-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="3a8fe-104">In questo documento viene descritto come esplorare i dati archiviati nel contenitore BLOB di Azure mediante il pacchetto Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="3a8fe-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="3a8fe-105">Il **menu** seguente collega ad argomenti che descrivono come usare gli strumenti per esplorare i dati da vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="3a8fe-106">Questa attività è un passaggio del [Processo di analisi scientifica dei dati]().</span><span class="sxs-lookup"><span data-stu-id="3a8fe-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="3a8fe-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a8fe-107">Prerequisites</span></span>
<span data-ttu-id="3a8fe-108">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-108">This article assumes that you have:</span></span>

* <span data-ttu-id="3a8fe-109">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-109">Created an Azure storage account.</span></span> <span data-ttu-id="3a8fe-110">Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3a8fe-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="3a8fe-111">I dati sono stati archiviati in un account di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="3a8fe-112">Per le istruzioni, vedere [Spostamento dei dati da e verso Archiviazione di Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="3a8fe-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="3a8fe-113">Caricare i dati in un intervallo di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="3a8fe-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="3a8fe-114">Per esplorare e modificare un set di dati, i dati devono essere innanzitutto scaricati dall'origine BLOB in un file locale che può essere quindi caricato in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="3a8fe-115">Ecco i passaggi da seguire per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="3a8fe-116">Scaricare i dati da BLOB Azure con l’esempio di codice Python riportato di seguito utilizzando il servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="3a8fe-117">Sostituire la variabile nel codice seguente con i valori specifici:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="3a8fe-118">Leggere i dati in un frame di dati Pandas dal file scaricato.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="3a8fe-119">A questo punto si è pronti per esplorare i dati e generare le funzionalità di questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="3a8fe-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="3a8fe-120"><a name="blob-dataexploration"></a>Esempi di esplorazione dei dati utilizzando Pandas</span><span class="sxs-lookup"><span data-stu-id="3a8fe-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="3a8fe-121">Di seguito sono riportati alcuni esempi dei modi per esplorare i dati utilizzando Pandas:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="3a8fe-122">Controllare il **numero di righe e colonne**</span><span class="sxs-lookup"><span data-stu-id="3a8fe-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="3a8fe-123">**Controllare** le prime o le ultime **righe** nel set di dati seguente:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="3a8fe-124">Controllare il **tipo di dati** importato in ogni colonna mediante il seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="3a8fe-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="3a8fe-125">Controllare le **statistiche di base** per le colonne nel set di dati come segue</span><span class="sxs-lookup"><span data-stu-id="3a8fe-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="3a8fe-126">Esaminare il numero di voci per ogni valore della colonna come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="3a8fe-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="3a8fe-127">**Contare i valori mancanti** rispetto al numero effettivo di voci in ogni colonna utilizzando il seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="3a8fe-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="3a8fe-128">Se si dispongono di **valori mancanti** per una colonna specifica nei dati, è possibile eliminarli come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="3a8fe-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="3a8fe-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="3a8fe-130">È possibile sostituire i valori mancanti anche con la funzione modalità:</span><span class="sxs-lookup"><span data-stu-id="3a8fe-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="3a8fe-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nome_colonna>':dataframe_blobdata['<nome_colonna>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="3a8fe-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="3a8fe-132">Creare un grafico **istogramma** utilizzando un numero variabile di contenitori per tracciare la distribuzione di una variabile</span><span class="sxs-lookup"><span data-stu-id="3a8fe-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="3a8fe-133">Esaminare le **correlazioni** tra le variabili utilizzando un grafico di dispersione o la funzione di correlazione incorporata</span><span class="sxs-lookup"><span data-stu-id="3a8fe-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

