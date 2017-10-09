---
title: "funzionalità aaaCreate per Azure blob di dati di archiviazione utilizzando Panda | Documenti Microsoft"
description: "Come toocreate funzionalità per i dati archiviati nel contenitore blob di Azure con il pacchetto di Python Panda hello."
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="98855-103">Creare funzionalità per i dati di archiviazione BLOB di Azure tramite Panda</span><span class="sxs-lookup"><span data-stu-id="98855-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="98855-104">Questo documento illustra come toocreate funzionalità per i dati archiviati nel contenitore di blob di Azure tramite hello [Pandas](http://pandas.pydata.org/) pacchetto Python.</span><span class="sxs-lookup"><span data-stu-id="98855-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="98855-105">Dopo la struttura di dati di hello tooload in un frame di dati Panda, illustrato come toogenerate funzioni categoriche utilizzando script Python con valori di indicatore e le funzionalità di creazione di contenitori.</span><span class="sxs-lookup"><span data-stu-id="98855-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="98855-106">Questo **menu** collegamenti tootopics che descrivono come toocreate funzionalità per i dati in vari ambienti.</span><span class="sxs-lookup"><span data-stu-id="98855-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="98855-107">Questa attività è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="98855-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98855-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="98855-108">Prerequisites</span></span>
<span data-ttu-id="98855-109">Questo articolo si basa sul presupposto che sia stato creato un account di archiviazione BLOB di Azure e vi siano stati archiviati dati.</span><span class="sxs-lookup"><span data-stu-id="98855-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="98855-110">Se è necessario tooset istruzioni un account, vedere [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="98855-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="98855-111">Caricare i dati di hello in un frame di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="98855-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="98855-112">In ordine toodo esplorare e modificare un set di dati, deve essere scaricato da hello blob tooa locale file di origine che può quindi essere caricati in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="98855-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="98855-113">Di seguito sono hello passaggi toofollow per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="98855-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="98855-114">Scaricare dati hello da Azure blob con hello seguente codice Python di esempio mediante il servizio blob.</span><span class="sxs-lookup"><span data-stu-id="98855-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="98855-115">Con i valori specifici, sostituire variabile hello in codice hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="98855-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="98855-116">Lettura dati hello in un frame di dati Pandas da hello scaricati i file.</span><span class="sxs-lookup"><span data-stu-id="98855-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="98855-117">Ora pronto tooexplore hello dati, generare funzioni in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="98855-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="98855-118"><a name="blob-featuregen"></a>Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="98855-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="98855-119">Hello nelle due sezioni successive mostrano come toogenerate funzionalità categorica con valori di indicatore e binning funzionalità tramite script Python.</span><span class="sxs-lookup"><span data-stu-id="98855-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="98855-120"><a name="blob-countfeature"></a>Valore dell'indicatore basato sulla creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="98855-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="98855-121">Le funzionalità relative alle categorie possono essere create come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="98855-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="98855-122">Controllare la distribuzione di hello di colonna categorica hello:</span><span class="sxs-lookup"><span data-stu-id="98855-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="98855-123">Generare i valori dell'indicatore per ognuno dei valori di colonna hello</span><span class="sxs-lookup"><span data-stu-id="98855-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="98855-124">Aggiungere la colonna indicatore hello con frame di dati originale hello</span><span class="sxs-lookup"><span data-stu-id="98855-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="98855-125">Rimuovere hello originale variabile:</span><span class="sxs-lookup"><span data-stu-id="98855-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="98855-126"><a name="blob-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="98855-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="98855-127">Per creare funzionalità in contenitori, procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="98855-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="98855-128">Aggiungere una sequenza di colonne toobin una colonna numerica</span><span class="sxs-lookup"><span data-stu-id="98855-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="98855-129">Convertire una sequenza tooa binning delle variabili booleane</span><span class="sxs-lookup"><span data-stu-id="98855-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="98855-130">Infine, creare un Join hello variabili fittizio toohello indietro originale frame di dati</span><span class="sxs-lookup"><span data-stu-id="98855-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="98855-131"><a name="sql-featuregen"></a>La scrittura dei dati, eseguire il backup tooAzure blob e l'utilizzo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98855-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="98855-132">Dopo aver esplorato i dati hello e creato hello le funzionalità necessarie, è possibile caricare i dati hello (campionate o trasformato) tooan Azure blob e usarla in Azure Machine Learning che usano hello alla procedura seguente: si noti che è possono creare funzionalità aggiuntive in hello Azure Machine Learning Studio anche.</span><span class="sxs-lookup"><span data-stu-id="98855-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="98855-133">Scrivere il file toolocal frame di dati hello</span><span class="sxs-lookup"><span data-stu-id="98855-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="98855-134">Caricare blob tooAzure di hello dati come segue:</span><span class="sxs-lookup"><span data-stu-id="98855-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="98855-135">Ora hello dati possono essere letti dall'utilizzo di blob hello hello Azure Machine Learning [l'importazione dei dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modulo come illustrato nella schermata di hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="98855-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![lettore BLOB](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

