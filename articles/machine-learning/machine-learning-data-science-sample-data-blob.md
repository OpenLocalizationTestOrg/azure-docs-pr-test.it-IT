---
title: archiviazione blob di dati aaaSample in Azure | Documenti Microsoft
description: Dati di esempio nell'archivio BLOB di Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="5b930-103"><a name="heading"></a>Dati di esempio nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5b930-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="5b930-104">In questo documento vengono descritti i dati di campionamento che è possibile memorizzare nell'archivio BLOB di Azure scaricandoli a livello di programmazione ed eseguendo il successivo campionamento tramite le procedure scritte in Python.</span><span class="sxs-lookup"><span data-stu-id="5b930-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="5b930-105">esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b930-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="5b930-106">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="5b930-106">**Why sample your data?**</span></span>
<span data-ttu-id="5b930-107">Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni.</span><span class="sxs-lookup"><span data-stu-id="5b930-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="5b930-108">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5b930-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="5b930-109">Il relativo ruolo nel processo di Cortana Analitica hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="5b930-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="5b930-110">Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5b930-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="5b930-111">Download e sotto-campionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="5b930-111">Download and down-sample data</span></span>
1. <span data-ttu-id="5b930-112">Scaricare dati hello dall'archiviazione blob di Azure usando il servizio blob hello da hello codice Python di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="5b930-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="5b930-113">Leggere i dati in un frame di dati Pandas dal file hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5b930-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="5b930-114">Esempio dati hello utilizzando hello `numpy`del `random.choice` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b930-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="5b930-115">Ora è possibile utilizzare hello sopra il frame di dati con % 1: esempio hello per un'ulteriore analisi e la generazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5b930-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="5b930-116"><a name="heading"></a>Caricamento e lettura dei dati in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b930-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="5b930-117">È possibile utilizzare i seguenti dati di esempio codice hello toodown esempio hello e utilizzarlo direttamente in Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="5b930-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="5b930-118">Scrivere il file locale tooa hello dati frame</span><span class="sxs-lookup"><span data-stu-id="5b930-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="5b930-119">Caricare tooan file locale hello Azure blob tramite hello seguente codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="5b930-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="5b930-120">Leggere i dati di hello dal blob di Azure con Azure Machine Learning hello [l'importazione dei dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) come illustrato nell'immagine di hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b930-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![lettore BLOB](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

