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
# <a name="heading"></a>Dati di esempio nell'archivio BLOB di Azure
In questo documento vengono descritti i dati di campionamento che è possibile memorizzare nell'archivio BLOB di Azure scaricandoli a livello di programmazione ed eseguendo il successivo campionamento tramite le procedure scritte in Python.

esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Perché campionare i dati?**
Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni. Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità. Il relativo ruolo nel processo di Cortana Analitica hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.

Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>Download e sotto-campionamento dei dati
1. Scaricare dati hello dall'archiviazione blob di Azure usando il servizio blob hello da hello codice Python di esempio seguente: 
   
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

2. Leggere i dati in un frame di dati Pandas dal file hello scaricato in precedenza.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Esempio dati hello utilizzando hello `numpy`del `random.choice` come indicato di seguito:
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Ora è possibile utilizzare hello sopra il frame di dati con % 1: esempio hello per un'ulteriore analisi e la generazione di funzionalità.

## <a name="heading"></a>Caricamento e lettura dei dati in Azure Machine Learning
È possibile utilizzare i seguenti dati di esempio codice hello toodown esempio hello e utilizzarlo direttamente in Azure Machine Learning:

1. Scrivere il file locale tooa hello dati frame
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Caricare tooan file locale hello Azure blob tramite hello seguente codice di esempio:
   
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

3. Leggere i dati di hello dal blob di Azure con Azure Machine Learning hello [l'importazione dei dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) come illustrato nell'immagine di hello riportata di seguito:

![lettore BLOB](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

