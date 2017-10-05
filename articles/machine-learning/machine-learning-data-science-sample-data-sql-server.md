---
title: Dati di esempio di SQL Server in Azure| Microsoft Docs
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
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="84f9c-103"><a name="heading"></a>Dati di esempio in SQL Server in Azure</span><span class="sxs-lookup"><span data-stu-id="84f9c-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="84f9c-104">Questo documento illustra come campionare dati archiviati in SQL Server su Azure usando SQL o il linguaggio di programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="84f9c-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="84f9c-105">Viene inoltre illustrato come spostare i dati campionati in Azure Machine Learning salvandoli in un file, caricandoli in un BLOB di Azure e quindi leggendoli in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="84f9c-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="84f9c-106">Il campionamento di Python usa la libreria ODBC [pyodbc](https://code.google.com/p/pyodbc/) per connettersi al server SQL in Azure e la libreria [Pandas](http://pandas.pydata.org/) per creare il campionamento.</span><span class="sxs-lookup"><span data-stu-id="84f9c-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="84f9c-107">Il codice SQL di esempio riportato in questo documento presuppone che i dati si trovino in un server SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="84f9c-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="84f9c-108">In caso contrario, fare riferimento all'argomento sullo [Spostamento dei dati in SQL Server in una macchina virtuale di Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) per istruzioni su come spostare i dati in SQL Server su Azure.</span><span class="sxs-lookup"><span data-stu-id="84f9c-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="84f9c-109">Il **menu** seguente contiene collegamenti ad argomenti che descrivono come campionare dati di vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="84f9c-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="84f9c-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="84f9c-110">**Why sample your data?**</span></span>
<span data-ttu-id="84f9c-111">Se il set di dati da analizzare è grande, è in genere opportuno sottocampionare i dati per ridurlo e ottenere dimensioni inferiori più facilmente gestibili ma comunque rappresentative.</span><span class="sxs-lookup"><span data-stu-id="84f9c-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="84f9c-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="84f9c-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="84f9c-113">Il suo ruolo nel [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) consiste nell'abilitare la creazione relativa a prototipi di funzioni di elaborazione dei dati e di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84f9c-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="84f9c-114">Questo campionamento è un passaggio del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="84f9c-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="84f9c-115"><a name="SQL"></a>Utilizzo di SQL</span><span class="sxs-lookup"><span data-stu-id="84f9c-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="84f9c-116">In questa sezione vengono descritti alcuni metodi di utilizzo di SQL per eseguire il campionamento casuale semplice dei dati all'interno del database.</span><span class="sxs-lookup"><span data-stu-id="84f9c-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="84f9c-117">Scegliere il metodo in base alla dimensione dei dati e alla loro distribuzione.</span><span class="sxs-lookup"><span data-stu-id="84f9c-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="84f9c-118">Gli elementi riportati di seguito mostrano come utilizzare il valore newId in SQL Server per effettuare il campionamento.</span><span class="sxs-lookup"><span data-stu-id="84f9c-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="84f9c-119">Il metodo scelto dipende dal livello di casualità previsto per il campionamento da eseguire (il valore pk_id nel codice di esempio riportato in basso si presuppone che sia una chiave primaria generata automaticamente).</span><span class="sxs-lookup"><span data-stu-id="84f9c-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="84f9c-120">Campionamento casuale meno rigoroso</span><span class="sxs-lookup"><span data-stu-id="84f9c-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="84f9c-121">Campionamento più casuale</span><span class="sxs-lookup"><span data-stu-id="84f9c-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="84f9c-122">È possibile utilizzare la clausola TABLESAMPLE per il campionamento come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="84f9c-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="84f9c-123">Può trattarsi di un approccio più efficace se i dati sono di grandi dimensioni (presupponendo che i dati in pagine diverse non siano correlati) e per completare la query in un tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="84f9c-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="84f9c-124">È possibile esplorare e generare le funzionalità da questi dati campionati archiviandoli in una nuova tabella</span><span class="sxs-lookup"><span data-stu-id="84f9c-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="84f9c-125"><a name="sql-aml"></a>Connessione ad Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84f9c-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="84f9c-126">È possibile usare direttamente le query di esempio riportate sopra nel modulo [Import Data][import-data] (Importazione dati) di Azure Machine Learning per sottocampionare i dati in modo immediato e inserirli in un esperimento di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84f9c-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="84f9c-127">Di seguito viene riportata una schermata relativa all'uso del modulo Reader per leggere i dati campionati:</span><span class="sxs-lookup"><span data-stu-id="84f9c-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![lettore sql][1]

## <span data-ttu-id="84f9c-129"><a name="python"></a>Utilizzo del linguaggio di programmazione Python</span><span class="sxs-lookup"><span data-stu-id="84f9c-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="84f9c-130">In questa sezione viene mostrato l'uso della [libreria pyodbc](https://code.google.com/p/pyodbc/) per stabilire un collegamento ODBC al database di un server SQL in Python.</span><span class="sxs-lookup"><span data-stu-id="84f9c-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="84f9c-131">La stringa di connessione del database è la seguente: (sostituire servername, dbname, username e password con la propria configurazione):</span><span class="sxs-lookup"><span data-stu-id="84f9c-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="84f9c-132">La libreria [Pandas](http://pandas.pydata.org/) in Python fornisce una vasta gamma di strutture di dati e strumenti di analisi dei dati per la manipolazione dei dati nella programmazione in Python.</span><span class="sxs-lookup"><span data-stu-id="84f9c-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="84f9c-133">Nel codice riportato di seguito si legge un campionamento dello 0,1% dei dati di una tabella nel database SQL di Azure in un frame di dati Pandas:</span><span class="sxs-lookup"><span data-stu-id="84f9c-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="84f9c-134">È ora possibile lavorare con i dati campionati nel frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="84f9c-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="84f9c-135"><a name="python-aml"></a>Connessione ad Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84f9c-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="84f9c-136">È possibile utilizzare il codice di esempio seguente per salvare i dati ricampionati in un file e caricarli in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="84f9c-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="84f9c-137">I dati del BLOB possono essere letti direttamente in un esperimento di Azure Machine Learning con il modulo [Import Data][import-data] (Importazione dati).</span><span class="sxs-lookup"><span data-stu-id="84f9c-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="84f9c-138">Attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="84f9c-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="84f9c-139">Scrivere il frame di dati Pandas in un file locale</span><span class="sxs-lookup"><span data-stu-id="84f9c-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="84f9c-140">Caricare il file locale nel BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="84f9c-140">Upload local file to Azure blob</span></span>
   
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
3. <span data-ttu-id="84f9c-141">Leggere i dati nel BLOB di Azure usando il modulo [Import Data][import-data] (Importazione dati) di Azure Machine Learning come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="84f9c-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![lettore BLOB][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="84f9c-143">Esempio del Processo di analisi scientifica dei dati per i team</span><span class="sxs-lookup"><span data-stu-id="84f9c-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="84f9c-144">Per un esempio della procedura dettagliata end-to-end del Processo di analisi scientifica dei dati per i team usando un set di dati pubblici, vedere [Processo di analisi scientifica dei dati per i team in azione: uso di SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="84f9c-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
