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
# <span data-ttu-id="2948a-103"><a name="heading"></a>Dati di esempio in SQL Server in Azure</span><span class="sxs-lookup"><span data-stu-id="2948a-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="2948a-104">Questo documento illustra come i dati toosample archiviati in SQL Server in Azure utilizzando SQL o hello linguaggio di programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="2948a-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="2948a-105">Viene inoltre illustrato come toomove dati campionati in Azure Machine Learning tramite il salvataggio del file tooa, caricarlo tooan blob di Azure e quindi leggerlo in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2948a-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="2948a-106">campionamento Python Hello utilizza hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC libreria tooconnect tooSQL Server in Azure e hello [Pandas](http://pandas.pydata.org/) campionamento hello toodo di libreria.</span><span class="sxs-lookup"><span data-stu-id="2948a-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="2948a-107">codice di esempio SQL Hello in questo documento si presuppone che hello dati diventano in un Server SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="2948a-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="2948a-108">In caso contrario, consultare troppo[spostare dati tooSQL Server in Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) argomento per istruzioni su come toomove il tooSQL dati Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="2948a-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="2948a-109">esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2948a-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="2948a-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="2948a-110">**Why sample your data?**</span></span>
<span data-ttu-id="2948a-111">Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni.</span><span class="sxs-lookup"><span data-stu-id="2948a-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="2948a-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2948a-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="2948a-113">Il ruolo in hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="2948a-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="2948a-114">Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="2948a-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="2948a-115"><a name="SQL"></a>Utilizzo di SQL</span><span class="sxs-lookup"><span data-stu-id="2948a-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="2948a-116">In questa sezione vengono descritti i diversi metodi tramite SQL tooperform un campionamento casuale semplice sui dati hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="2948a-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="2948a-117">Scegliere il metodo in base alla dimensione dei dati e alla loro distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2948a-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="2948a-118">Hello due elementi seguenti mostrano come newid toouse in SQL Server tooperform hello campionamento.</span><span class="sxs-lookup"><span data-stu-id="2948a-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="2948a-119">Hello metodo scelto dipende casuale come si desidera toobe esempio hello (pk_id codice di esempio hello riportato di seguito viene utilizzata una chiave primaria generata automaticamente toobe).</span><span class="sxs-lookup"><span data-stu-id="2948a-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="2948a-120">Campionamento casuale meno rigoroso</span><span class="sxs-lookup"><span data-stu-id="2948a-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="2948a-121">Campionamento più casuale</span><span class="sxs-lookup"><span data-stu-id="2948a-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="2948a-122">È possibile utilizzare la clausola TABLESAMPLE per il campionamento come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2948a-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="2948a-123">È possibile un approccio migliore se la dimensione dei dati è grande (presupponendo che non sia correlati dati in più pagine) e per toocomplete query hello in un tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="2948a-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="2948a-124">È possibile esplorare e generare le funzionalità da questi dati campionati archiviandoli in una nuova tabella</span><span class="sxs-lookup"><span data-stu-id="2948a-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="2948a-125"><a name="sql-aml"></a>Connessione tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2948a-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="2948a-126">È possibile utilizzare direttamente la query di esempio hello in precedenza in Azure Machine Learning hello [l'importazione dei dati] [ import-data] dati toodown esempio hello modulo hello veloce e portarlo in un esperimento di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2948a-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="2948a-127">Cattura di schermata dell'utilizzo di dati campionato hello tooread modulo del lettore hello è illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="2948a-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![lettore sql][1]

## <span data-ttu-id="2948a-129"><a name="python"></a>Usando il linguaggio di programmazione Python hello</span><span class="sxs-lookup"><span data-stu-id="2948a-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="2948a-130">In questa sezione viene illustrato come utilizzare hello [pyodbc libreria](https://code.google.com/p/pyodbc/) tooestablish un ODBC connettersi tooa database di SQL server in Python.</span><span class="sxs-lookup"><span data-stu-id="2948a-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="2948a-131">stringa di connessione database Hello è il seguente: (replace servername, dbname, username e password con la configurazione):</span><span class="sxs-lookup"><span data-stu-id="2948a-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="2948a-132">Hello [Pandas](http://pandas.pydata.org/) libreria in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="2948a-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="2948a-133">codice Hello seguente legge un campione di 0,1% di hello dati da una tabella nel database SQL di Azure in dati Pandas:</span><span class="sxs-lookup"><span data-stu-id="2948a-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="2948a-134">È ora possibile lavorare con i dati campionato hello in frame di dati Pandas hello.</span><span class="sxs-lookup"><span data-stu-id="2948a-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="2948a-135"><a name="python-aml"></a>Connessione tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2948a-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="2948a-136">È possibile utilizzare i seguenti file di esempio codice toosave hello dati ridotti tooa hello e caricarlo tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2948a-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="2948a-137">Hello in blob hello direttamente leggere i dati in un esperimento di Azure Machine Learning usando hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="2948a-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="2948a-138">come indicato di seguito sono riportati i passaggi di Hello:</span><span class="sxs-lookup"><span data-stu-id="2948a-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="2948a-139">Scrivere il file locale di hello pandas dati frame tooa</span><span class="sxs-lookup"><span data-stu-id="2948a-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="2948a-140">Caricare un file locale tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="2948a-140">Upload local file tooAzure blob</span></span>
   
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
3. <span data-ttu-id="2948a-141">Leggere i dati dal blob di Azure con Azure Machine Learning [l'importazione dei dati] [ import-data] modulo come illustrato nella schermata hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2948a-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![lettore BLOB][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="2948a-143">Processo di analisi scientifica dei dati del Team di Hello nell'esempio di azione</span><span class="sxs-lookup"><span data-stu-id="2948a-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="2948a-144">Per un esempio di questa procedura dettagliata end-to-end del processo di analisi scientifica dei dati di Team hello un utilizzando un set di dati pubblici, vedere [Team processo di analisi scientifica dei dati in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2948a-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
