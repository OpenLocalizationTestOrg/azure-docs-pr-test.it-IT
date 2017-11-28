---
title: aaaProcess Azure blob di dati con analitica avanzate | Documenti Microsoft
description: Elaborare dati nell'archivio BLOB di Azure.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="8d9f0-103"><a name="heading"></a>Elaborare i dati BLOB di Azure con analisi avanzate</span><span class="sxs-lookup"><span data-stu-id="8d9f0-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="8d9f0-104">In questo documento vengono descritte l'esplorazione dei dati e la creazione di funzionalità da dati archiviati nell’archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="8d9f0-105">Caricare i dati di hello in un frame di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="8d9f0-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="8d9f0-106">In ordine tooexplore e modificare un set di dati, deve essere scaricato da hello blob tooa locale file di origine che può quindi essere caricati in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="8d9f0-107">Di seguito sono hello passaggi toofollow per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="8d9f0-108">Scaricare dati hello da Azure blob con hello seguente codice Python di esempio mediante il servizio blob.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="8d9f0-109">Con i valori specifici, sostituire variabile hello in codice hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="8d9f0-110">Lettura dati hello in un frame di dati Pandas da hello scaricati i file.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="8d9f0-111">Ora pronto tooexplore hello dati, generare funzioni in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="8d9f0-112"><a name="blob-dataexploration"></a>Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="8d9f0-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="8d9f0-113">Ecco alcuni esempi di modalità dati tooexplore Pandas utilizzando:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="8d9f0-114">Controllare hello numero di righe e colonne</span><span class="sxs-lookup"><span data-stu-id="8d9f0-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="8d9f0-115">Controllare hello prima o ultima alcune righe nel set di dati di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="8d9f0-116">Controllare il tipo di dati hello che ogni colonna è stato importato come usando hello seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="8d9f0-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="8d9f0-117">Verificare di statistiche di base hello per le colonne di hello nel set di dati hello come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="8d9f0-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="8d9f0-118">Esaminare il numero di hello di voci per ogni valore di colonna come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="8d9f0-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="8d9f0-119">Numero di valori mancanti rispetto al numero effettivo di hello di voci in ogni colonna utilizzando hello seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="8d9f0-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="8d9f0-120">Se si dispone di valori mancanti per una determinata colonna nei dati di hello, vengono rilasciati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="8d9f0-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="8d9f0-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="8d9f0-122">Un altro modo tooreplace i valori mancanti è con funzione di modalità hello:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="8d9f0-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="8d9f0-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="8d9f0-124">Creare un tracciato di istogramma con un numero variabile di distribuzione di hello tooplot bin di una variabile</span><span class="sxs-lookup"><span data-stu-id="8d9f0-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="8d9f0-125">Esaminare le correlazioni tra le variabili utilizzando un scatterplot o funzione di correlazione incorporata hello</span><span class="sxs-lookup"><span data-stu-id="8d9f0-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="8d9f0-126"><a name="blob-featuregen"></a>Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="8d9f0-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="8d9f0-127">È quindi possibile generare funzionalità tramite Python come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="8d9f0-128"><a name="blob-countfeature"></a>Valore dell'indicatore basato sulla creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="8d9f0-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="8d9f0-129">Le funzionalità relative alle categorie possono essere create come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="8d9f0-130">Controllare la distribuzione di hello di colonna categorica hello:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="8d9f0-131">Generare i valori dell'indicatore per ognuno dei valori di colonna hello</span><span class="sxs-lookup"><span data-stu-id="8d9f0-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="8d9f0-132">Aggiungere la colonna indicatore hello con frame di dati originale hello</span><span class="sxs-lookup"><span data-stu-id="8d9f0-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="8d9f0-133">Rimuovere hello originale variabile:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="8d9f0-134"><a name="blob-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="8d9f0-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="8d9f0-135">Per creare funzionalità in contenitori, procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="8d9f0-136">Aggiungere una sequenza di colonne toobin una colonna numerica</span><span class="sxs-lookup"><span data-stu-id="8d9f0-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="8d9f0-137">Convertire una sequenza tooa binning delle variabili booleane</span><span class="sxs-lookup"><span data-stu-id="8d9f0-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="8d9f0-138">Infine, creare un Join hello variabili fittizio toohello indietro originale frame di dati</span><span class="sxs-lookup"><span data-stu-id="8d9f0-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="8d9f0-139"><a name="sql-featuregen"></a>La scrittura dei dati, eseguire il backup tooAzure blob e l'utilizzo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8d9f0-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="8d9f0-140">Dopo aver esplorato i dati hello e creato hello le funzionalità necessarie, è possibile caricare i dati hello (campionate o trasformato) tooan Azure blob e usarla in Azure Machine Learning che usano hello alla procedura seguente: si noti che è possono creare funzionalità aggiuntive in hello Azure Machine Learning Studio anche.</span><span class="sxs-lookup"><span data-stu-id="8d9f0-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="8d9f0-141">Scrivere il file toolocal frame di dati hello</span><span class="sxs-lookup"><span data-stu-id="8d9f0-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="8d9f0-142">Caricare blob tooAzure di hello dati come segue:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="8d9f0-143">Ora hello dati possono essere letti dall'utilizzo di blob hello hello Azure Machine Learning [l'importazione dei dati] [ import-data] modulo come illustrato nella schermata di hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d9f0-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![lettore BLOB][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

