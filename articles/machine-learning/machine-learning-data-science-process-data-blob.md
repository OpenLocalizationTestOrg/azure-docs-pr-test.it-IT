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
# <a name="heading"></a>Elaborare i dati BLOB di Azure con analisi avanzate
In questo documento vengono descritte l'esplorazione dei dati e la creazione di funzionalità da dati archiviati nell’archivio BLOB di Azure. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Caricare i dati di hello in un frame di dati Pandas
In ordine tooexplore e modificare un set di dati, deve essere scaricato da hello blob tooa locale file di origine che può quindi essere caricati in un frame di dati Pandas. Di seguito sono hello passaggi toofollow per questa procedura:

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

## <a name="blob-dataexploration"></a>Esplorazione dei dati
Ecco alcuni esempi di modalità dati tooexplore Pandas utilizzando:

1. Controllare hello numero di righe e colonne 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Controllare hello prima o ultima alcune righe nel set di dati di hello come indicato di seguito:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Controllare il tipo di dati hello che ogni colonna è stato importato come usando hello seguente codice di esempio
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Verificare di statistiche di base hello per le colonne di hello nel set di dati hello come indicato di seguito
   
        dataframe_blobdata.describe()
5. Esaminare il numero di hello di voci per ogni valore di colonna come indicato di seguito
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Numero di valori mancanti rispetto al numero effettivo di hello di voci in ogni colonna utilizzando hello seguente codice di esempio
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Se si dispone di valori mancanti per una determinata colonna nei dati di hello, vengono rilasciati come indicato di seguito:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Un altro modo tooreplace i valori mancanti è con funzione di modalità hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Creare un tracciato di istogramma con un numero variabile di distribuzione di hello tooplot bin di una variabile    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Esaminare le correlazioni tra le variabili utilizzando un scatterplot o funzione di correlazione incorporata hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Creazione di funzionalità
È quindi possibile generare funzionalità tramite Python come indicato di seguito:

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
3. Ora hello dati possono essere letti dall'utilizzo di blob hello hello Azure Machine Learning [l'importazione dei dati] [ import-data] modulo come illustrato nella schermata di hello riportata di seguito:

![lettore BLOB][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

