---
title: Elaborare i dati BLOB di Azure con analisi avanzate | Documentazione Microsoft
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="9b991-103"><a name="heading"></a>Elaborare i dati BLOB di Azure con analisi avanzate</span><span class="sxs-lookup"><span data-stu-id="9b991-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="9b991-104">In questo documento vengono descritte l'esplorazione dei dati e la creazione di funzionalità da dati archiviati nell’archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b991-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="9b991-105">Caricare i dati in un intervallo di dati Pandas</span><span class="sxs-lookup"><span data-stu-id="9b991-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="9b991-106">Per esplorare e modificare un set di dati, i dati devono essere scaricati dall'origine BLOB in un file locale che può essere quindi caricato in un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="9b991-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="9b991-107">Ecco i passaggi da seguire per questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9b991-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="9b991-108">Scaricare i dati da BLOB Azure con il codice Python di esempio riportato di seguito utilizzando il servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="9b991-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="9b991-109">Sostituire la variabile nel codice riportato di seguito con i valori specifici:</span><span class="sxs-lookup"><span data-stu-id="9b991-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="9b991-110">Leggere i dati in un frame di dati Pandas dal file scaricato.</span><span class="sxs-lookup"><span data-stu-id="9b991-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="9b991-111">A questo punto si è pronti per esplorare i dati e generare le funzionalità di questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="9b991-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="9b991-112"><a name="blob-dataexploration"></a>Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="9b991-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="9b991-113">Di seguito sono riportati alcuni esempi dei modi per esplorare i dati utilizzando Pandas:</span><span class="sxs-lookup"><span data-stu-id="9b991-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="9b991-114">Controllare il numero di righe e colonne</span><span class="sxs-lookup"><span data-stu-id="9b991-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="9b991-115">Controllare le prime o le ultime righe nel set di dati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="9b991-116">Controllare il tipo di dati importato in ogni colonna mediante il seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="9b991-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="9b991-117">Controllare le statistiche di base per le colonne nel set di dati come segue</span><span class="sxs-lookup"><span data-stu-id="9b991-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="9b991-118">Esaminare il numero di voci per ogni valore della colonna come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="9b991-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="9b991-119">Contare i valori mancanti rispetto al numero effettivo di voci in ogni colonna utilizzando il seguente codice di esempio</span><span class="sxs-lookup"><span data-stu-id="9b991-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="9b991-120">Se si dispongono di valori mancanti per una colonna specifica nei dati, è possibile eliminarli come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="9b991-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="9b991-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="9b991-122">È possibile sostituire i valori mancanti anche con la funzione modalità:</span><span class="sxs-lookup"><span data-stu-id="9b991-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="9b991-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="9b991-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="9b991-124">Creare un grafico istogramma utilizzando un numero variabile di contenitori per tracciare la distribuzione di una variabile</span><span class="sxs-lookup"><span data-stu-id="9b991-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="9b991-125">Esaminare le correlazioni tra le variabili utilizzando un grafico di dispersione o la funzione di correlazione incorporata</span><span class="sxs-lookup"><span data-stu-id="9b991-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="9b991-126"><a name="blob-featuregen"></a>Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="9b991-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="9b991-127">È quindi possibile generare funzionalità tramite Python come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="9b991-128"><a name="blob-countfeature"></a>Valore dell'indicatore basato sulla creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="9b991-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="9b991-129">Le funzionalità relative alle categorie possono essere create come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="9b991-130">Controllare la distribuzione della colonna relativa alla categoria:</span><span class="sxs-lookup"><span data-stu-id="9b991-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="9b991-131">Generare i valori dell'indicatore per ognuno dei valori della colonna</span><span class="sxs-lookup"><span data-stu-id="9b991-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="9b991-132">Unire la colonna indicatore con il frame di dati originale</span><span class="sxs-lookup"><span data-stu-id="9b991-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="9b991-133">Rimuovere la variabile originale:</span><span class="sxs-lookup"><span data-stu-id="9b991-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="9b991-134"><a name="blob-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="9b991-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="9b991-135">Per creare funzionalità in contenitori, procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="9b991-136">Aggiungere una sequenza di colonne per suddividere una colonna numerica</span><span class="sxs-lookup"><span data-stu-id="9b991-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="9b991-137">Convertire la creazione di contenitori in una sequenza di variabili booleane</span><span class="sxs-lookup"><span data-stu-id="9b991-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="9b991-138">Infine, aggiungere di nuovo le variabili fittizie al frame di dati originale</span><span class="sxs-lookup"><span data-stu-id="9b991-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="9b991-139"><a name="sql-featuregen"></a>Scrittura dei dati nel BLOB di Azure e utilizzo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9b991-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="9b991-140">Dopo avere esaminato i dati e creato le funzionalità necessarie, è possibile caricare i dati (campionati o completi) in un BLOB di Azure e utilizzarli in Azure Machine Learning attenendosi alla procedura seguente. Tenere presente che le funzionalità aggiuntive possono essere create anche in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9b991-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="9b991-141">Scrivere il frame di dati in file locali</span><span class="sxs-lookup"><span data-stu-id="9b991-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="9b991-142">Caricare i dati nel BLOB di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="9b991-143">Ora è possibile leggere i dati dal BLOB usando il modulo [Import Data][import-data] di Azure Machine Learning, come illustra la schermata riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b991-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![lettore BLOB][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

