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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Esplorare i dati nell'archiviazione BLOB di Azure con Pandas
Questo documento descrive come tooexplore i dati archiviati in Azure blob contenitore usando [Pandas](http://pandas.pydata.org/) pacchetto Python.

esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione. Questa attività è un passaggio di hello [il processo di analisi scientifica dei dati]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* Creato un account di archiviazione di Azure. Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* I dati sono stati archiviati in un account di archiviazione BLOB di Azure. Se sono necessarie istruzioni, vedere [tooand di spostamento dei dati da archiviazione di Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Caricare i dati di hello in un frame di dati Pandas
tooexplore e modificare un set di dati, deve prima essere scaricato da hello blob tooa locale file di origine, che può quindi essere caricato in un frame di dati Pandas. Di seguito sono hello passaggi toofollow per questa procedura:

1. Scaricare dati hello da Azure blob con hello seguente esempio di codice Python mediante il servizio blob. Sostituire la variabile hello nel seguente codice con i valori specifici hello: 
   
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

## <a name="blob-dataexploration"></a>Esempi di esplorazione dei dati utilizzando Pandas
Ecco alcuni esempi di modalità dati tooexplore Pandas utilizzando:

1. Controllare hello **numero di righe e colonne** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Controllare** hello alcuni primo o ultimi **righe** in hello seguente set di dati:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Controllare hello **tipo di dati** ogni colonna è stato importato come usando hello seguente codice di esempio
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Controllare hello **statistiche di base** per colonne hello hello set di dati, come indicato di seguito
   
        dataframe_blobdata.describe()
5. Esaminare il numero di hello di voci per ogni valore di colonna come indicato di seguito
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Conteggio dei valori mancanti** rispetto al numero effettivo di hello di voci in ogni colonna utilizzando hello seguente codice di esempio
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Se dispone di **valori mancanti** per una colonna specifica in dati hello, è possibile rilasciarli come indicato di seguito:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Un altro modo tooreplace i valori mancanti è con funzione di modalità hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Creare un **istogramma** tracciato con un numero variabile di distribuzione di hello tooplot bin di una variabile    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Esaminare **correlazioni** tra le variabili utilizzando un scatterplot o funzione di correlazione incorporata hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

