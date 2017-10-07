---
title: aaaSample dati in SQL Server in Azure | Documenti Microsoft
description: Dati di esempio in SQL Server in Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Dati di esempio in SQL Server in Azure
Questo documento illustra come i dati toosample archiviati in SQL Server in Azure utilizzando SQL o hello linguaggio di programmazione Python. Viene inoltre illustrato come toomove dati campionati in Azure Machine Learning tramite il salvataggio del file tooa, caricarlo tooan blob di Azure e quindi leggerlo in Azure Machine Learning Studio.

campionamento Python Hello utilizza hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC libreria tooconnect tooSQL Server in Azure e hello [Pandas](http://pandas.pydata.org/) campionamento hello toodo di libreria.

> [!NOTE]
> codice di esempio SQL Hello in questo documento si presuppone che hello dati diventano in un Server SQL in Azure. In caso contrario, consultare troppo[spostare dati tooSQL Server in Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) argomento per istruzioni su come toomove il tooSQL dati Server in Azure.
> 
> 

esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Perché campionare i dati?**
Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni. Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità. Il ruolo in hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.

Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Utilizzo di SQL
In questa sezione vengono descritti i diversi metodi tramite SQL tooperform un campionamento casuale semplice sui dati hello nel database di hello. Scegliere il metodo in base alla dimensione dei dati e alla loro distribuzione.

Hello due elementi seguenti mostrano come newid toouse in SQL Server tooperform hello campionamento. Hello metodo scelto dipende casuale come si desidera toobe esempio hello (pk_id codice di esempio hello riportato di seguito viene utilizzata una chiave primaria generata automaticamente toobe).

1. Campionamento casuale meno rigoroso
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Campionamento più casuale 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

È possibile utilizzare la clausola TABLESAMPLE per il campionamento come mostrato di seguito. È possibile un approccio migliore se la dimensione dei dati è grande (presupponendo che non sia correlati dati in più pagine) e per toocomplete query hello in un tempo ragionevole.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> È possibile esplorare e generare le funzionalità da questi dati campionati archiviandoli in una nuova tabella
> 
> 

### <a name="sql-aml"></a>Connessione tooAzure Machine Learning
È possibile utilizzare direttamente la query di esempio hello in precedenza in Azure Machine Learning hello [l'importazione dei dati] [ import-data] dati toodown esempio hello modulo hello veloce e portarlo in un esperimento di Azure Machine Learning. Cattura di schermata dell'utilizzo di dati campionato hello tooread modulo del lettore hello è illustrata di seguito:

![lettore sql][1]

## <a name="python"></a>Usando il linguaggio di programmazione Python hello
In questa sezione viene illustrato come utilizzare hello [pyodbc libreria](https://code.google.com/p/pyodbc/) tooestablish un ODBC connettersi tooa database di SQL server in Python. stringa di connessione database Hello è il seguente: (replace servername, dbname, username e password con la configurazione):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [Pandas](http://pandas.pydata.org/) libreria in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python. codice Hello seguente legge un campione di 0,1% di hello dati da una tabella nel database SQL di Azure in dati Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

È ora possibile lavorare con i dati campionato hello in frame di dati Pandas hello. 

### <a name="python-aml"></a>Connessione tooAzure Machine Learning
È possibile utilizzare i seguenti file di esempio codice toosave hello dati ridotti tooa hello e caricarlo tooan blob di Azure. Hello in blob hello direttamente leggere i dati in un esperimento di Azure Machine Learning usando hello [l'importazione dei dati] [ import-data] modulo. come indicato di seguito sono riportati i passaggi di Hello: 

1. Scrivere il file locale di hello pandas dati frame tooa
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Caricare un file locale tooAzure blob
   
        from azure.storage import BlobService
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
3. Leggere i dati dal blob di Azure con Azure Machine Learning [l'importazione dei dati] [ import-data] modulo come illustrato nella schermata hello riportato di seguito:

![lettore BLOB][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Processo di analisi scientifica dei dati del Team di Hello nell'esempio di azione
Per un esempio di questa procedura dettagliata end-to-end del processo di analisi scientifica dei dati di Team hello un utilizzando un set di dati pubblici, vedere [Team processo di analisi scientifica dei dati in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
