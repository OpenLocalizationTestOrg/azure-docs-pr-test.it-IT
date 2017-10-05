---
title: Campionare i dati nell'archivio BLOB di Azure| Documentazione Microsoft
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="91f6a-103"><a name="heading"></a>Dati di esempio nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="91f6a-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="91f6a-104">In questo documento vengono descritti i dati di campionamento che è possibile memorizzare nell'archivio BLOB di Azure scaricandoli a livello di programmazione ed eseguendo il successivo campionamento tramite le procedure scritte in Python.</span><span class="sxs-lookup"><span data-stu-id="91f6a-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="91f6a-105">Il **menu** seguente contiene collegamenti ad argomenti che descrivono come campionare dati di vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="91f6a-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="91f6a-106">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="91f6a-106">**Why sample your data?**</span></span>
<span data-ttu-id="91f6a-107">Se il set di dati da analizzare è grande, è in genere opportuno sottocampionare i dati per ridurlo e ottenere dimensioni inferiori più facilmente gestibili ma comunque rappresentative.</span><span class="sxs-lookup"><span data-stu-id="91f6a-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="91f6a-108">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="91f6a-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="91f6a-109">Il suo ruolo nel Cortana Analytics Process consiste nell'abilitare la creazione relativa a prototipi di funzioni di elaborazione dei dati e di modelli per l'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="91f6a-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="91f6a-110">Questo campionamento è un passaggio del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="91f6a-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="91f6a-111">Download e sotto-campionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="91f6a-111">Download and down-sample data</span></span>
1. <span data-ttu-id="91f6a-112">Scaricare i dati dall'archivio BLOB di Azure usando il servizio BLOB del seguente codice Python di esempio:</span><span class="sxs-lookup"><span data-stu-id="91f6a-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="91f6a-113">Leggere i dati all'interno di un frame di dati Pandas dal file scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="91f6a-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="91f6a-114">Eseguire il sotto-campionamento dei dati usando `numpy`di `random.choice` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="91f6a-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="91f6a-115">A questo punto, è possibile utilizzare il frame di dati precedente con il campione dell'1% per esplorare ulteriormente i dati e creare funzionalità.</span><span class="sxs-lookup"><span data-stu-id="91f6a-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="91f6a-116"><a name="heading"></a>Caricamento e lettura dei dati in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="91f6a-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="91f6a-117">Per sottocampionare i dati e usarli direttamente in Azure Machine Learning, è possibile usare il codice di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="91f6a-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="91f6a-118">Scrivere il frame di dati su un file locale</span><span class="sxs-lookup"><span data-stu-id="91f6a-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="91f6a-119">Caricare il file locale su un BLOB di Azure usante il seguente codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="91f6a-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="91f6a-120">Leggere i dati del BLOB di Azure con [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) (Importazione dati) di Azure Machine Learning, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="91f6a-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![lettore BLOB](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

