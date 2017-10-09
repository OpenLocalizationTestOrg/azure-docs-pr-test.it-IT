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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Creare funzionalità per i dati di archiviazione BLOB di Azure tramite Panda
Questo documento illustra come toocreate funzionalità per i dati archiviati nel contenitore di blob di Azure tramite hello [Pandas](http://pandas.pydata.org/) pacchetto Python. Dopo la struttura di dati di hello tooload in un frame di dati Panda, illustrato come toogenerate funzioni categoriche utilizzando script Python con valori di indicatore e le funzionalità di creazione di contenitori.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Questo **menu** collegamenti tootopics che descrivono come toocreate funzionalità per i dati in vari ambienti. Questa attività è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si basa sul presupposto che sia stato creato un account di archiviazione BLOB di Azure e vi siano stati archiviati dati. Se è necessario tooset istruzioni un account, vedere [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Caricare i dati di hello in un frame di dati Pandas
In ordine toodo esplorare e modificare un set di dati, deve essere scaricato da hello blob tooa locale file di origine che può quindi essere caricati in un frame di dati Pandas. Di seguito sono hello passaggi toofollow per questa procedura:

1. Scaricare dati hello da Azure blob con hello seguente codice Python di esempio mediante il servizio blob. Con i valori specifici, sostituire variabile hello in codice hello riportato di seguito:
   
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
2. Lettura dati hello in un frame di dati Pandas da hello scaricati i file.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Ora pronto tooexplore hello dati, generare funzioni in questo set di dati.

## <a name="blob-featuregen"></a>Creazione di funzionalità
Hello nelle due sezioni successive mostrano come toogenerate funzionalità categorica con valori di indicatore e binning funzionalità tramite script Python.

### <a name="blob-countfeature"></a>Valore dell'indicatore basato sulla creazione di funzionalità
Le funzionalità relative alle categorie possono essere create come indicato di seguito:

1. Controllare la distribuzione di hello di colonna categorica hello:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Generare i valori dell'indicatore per ognuno dei valori di colonna hello
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Aggiungere la colonna indicatore hello con frame di dati originale hello
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Rimuovere hello originale variabile:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità
Per creare funzionalità in contenitori, procedere come indicato di seguito:

1. Aggiungere una sequenza di colonne toobin una colonna numerica
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Convertire una sequenza tooa binning delle variabili booleane
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Infine, creare un Join hello variabili fittizio toohello indietro originale frame di dati
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>La scrittura dei dati, eseguire il backup tooAzure blob e l'utilizzo in Azure Machine Learning
Dopo aver esplorato i dati hello e creato hello le funzionalità necessarie, è possibile caricare i dati hello (campionate o trasformato) tooan Azure blob e usarla in Azure Machine Learning che usano hello alla procedura seguente: si noti che è possono creare funzionalità aggiuntive in hello Azure Machine Learning Studio anche.

1. Scrivere il file toolocal frame di dati hello
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Caricare blob tooAzure di hello dati come segue:
   
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
3. Ora hello dati possono essere letti dall'utilizzo di blob hello hello Azure Machine Learning [l'importazione dei dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modulo come illustrato nella schermata di hello riportata di seguito:

![lettore BLOB](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

