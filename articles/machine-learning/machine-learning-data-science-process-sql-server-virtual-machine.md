---
title: aaaExplore dati in una macchina virtuale di SQL Server in Azure | Documenti Microsoft
description: "Esplorare dati e generare funzionalità in una macchina virtuale di SQL Server in Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="f088c-103"><a name="heading"></a>Elaborazione dei dati della macchina virtuale di SQL Server in Azure</span><span class="sxs-lookup"><span data-stu-id="f088c-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="f088c-104">Questo documento descrive come tooexplore dati e generare le funzionalità per i dati archiviati in una macchina virtuale di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="f088c-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="f088c-105">Questa operazione può essere eseguita gestendo i dati tramite SQL o utilizzando un linguaggio di programmazione come Python.</span><span class="sxs-lookup"><span data-stu-id="f088c-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="f088c-106">le istruzioni SQL Hello in questo documento si presuppongono che i dati siano in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f088c-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="f088c-107">In caso contrario, fare riferimento toohello cloud data science processo mappa toolearn come toomove il tooSQL dati Server.</span><span class="sxs-lookup"><span data-stu-id="f088c-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="f088c-108"><a name="SQL"></a>Utilizzo di SQL</span><span class="sxs-lookup"><span data-stu-id="f088c-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="f088c-109">Viene descritto hello seguenti attività wrangling di dati in questa sezione tramite SQL:</span><span class="sxs-lookup"><span data-stu-id="f088c-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="f088c-110">Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="f088c-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="f088c-111">Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="f088c-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="f088c-112"><a name="sql-dataexploration"></a>Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="f088c-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="f088c-113">Ecco alcuni script SQL di esempio che possono essere utilizzati tooexplore archivi di dati in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f088c-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="f088c-114">Per un esempio pratico, è possibile utilizzare hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) e fare riferimento toohello IPNB intitolato [dati NYC wrangling utilizzando SQL Server e IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) per una procedura dettagliata end-to-end.</span><span class="sxs-lookup"><span data-stu-id="f088c-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="f088c-115">Ottenere il conteggio di hello di osservazioni al giorno</span><span class="sxs-lookup"><span data-stu-id="f088c-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="f088c-116">Ottenere livelli hello in una colonna categorica</span><span class="sxs-lookup"><span data-stu-id="f088c-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="f088c-117">Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche</span><span class="sxs-lookup"><span data-stu-id="f088c-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="f088c-118">Ottenere la distribuzione hello per le colonne numeriche</span><span class="sxs-lookup"><span data-stu-id="f088c-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="f088c-119"><a name="sql-featuregen"></a>Creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="f088c-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="f088c-120">In questa sezione viene descritto come creare funzionalità tramite SQL:</span><span class="sxs-lookup"><span data-stu-id="f088c-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="f088c-121">Creazione di funzionalità basate sul conteggio</span><span class="sxs-lookup"><span data-stu-id="f088c-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="f088c-122">Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="f088c-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="f088c-123">Implementazione della funzionalità hello da una singola colonna</span><span class="sxs-lookup"><span data-stu-id="f088c-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="f088c-124">Dopo avere generato le funzionalità aggiuntive, è possibile aggiungerli come tabella di colonne toohello esistente o creare una nuova tabella con le funzionalità aggiuntive di hello e la chiave primaria, che può essere unita con la tabella originale hello.</span><span class="sxs-lookup"><span data-stu-id="f088c-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="f088c-125"><a name="sql-countfeature"></a>Creazione di funzionalità basate sul conteggio</span><span class="sxs-lookup"><span data-stu-id="f088c-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="f088c-126">Hello seguenti esempi illustrano due modi per generare le funzionalità di conteggio.</span><span class="sxs-lookup"><span data-stu-id="f088c-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="f088c-127">primo metodo Hello utilizza somma condizionale e secondo Usa metodo di hello hello clausola 'where'.</span><span class="sxs-lookup"><span data-stu-id="f088c-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="f088c-128">Questi possono quindi essere aggiunti con hello originale (tramite le colonne chiave primaria) toohave conteggio caratteristiche della tabella insieme ai dati originali hello.</span><span class="sxs-lookup"><span data-stu-id="f088c-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="f088c-129"><a name="sql-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità</span><span class="sxs-lookup"><span data-stu-id="f088c-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="f088c-130">Hello esempio seguente viene illustrato come toogenerate suddiviso funzionalità tramite la creazione di contenitori (tramite cinque bin) una colonna numerica che può essere utilizzata come una funzionalità alternativa:</span><span class="sxs-lookup"><span data-stu-id="f088c-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="f088c-131"><a name="sql-featurerollout"></a>Implementazione della funzionalità hello da una singola colonna</span><span class="sxs-lookup"><span data-stu-id="f088c-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="f088c-132">In questa sezione viene illustrato come tooroll out una singola colonna in una tabella toogenerate ulteriori funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f088c-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="f088c-133">esempio Hello si presuppone che esista una colonna di longitudine o latitudine nella tabella hello da cui si sta tentando di toogenerate funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f088c-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="f088c-134">Ecco una breve panoramica sui dati di posizione di latitudine e longitudine (lecito da stackoverflow [come toomeasure hello accuratezza di latitudine e longitudine?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="f088c-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="f088c-135">Ciò è utile toounderstand prima di campo, località featurizing hello:</span><span class="sxs-lookup"><span data-stu-id="f088c-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="f088c-136">sign Hello indica se è in corso Nord o sud, est o occidentale mondo hello.</span><span class="sxs-lookup"><span data-stu-id="f088c-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="f088c-137">Una cifra nell'ordine delle centinaia diversa da zero indica che si sta usando la longitudine invece della latitudine.</span><span class="sxs-lookup"><span data-stu-id="f088c-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="f088c-138">cifra Hello decine offre una posizione tooabout chilometri 1.000.</span><span class="sxs-lookup"><span data-stu-id="f088c-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="f088c-139">Inoltre, fornisce informazioni utili sul continente o sull'oceano in cui si trova l'utente.</span><span class="sxs-lookup"><span data-stu-id="f088c-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="f088c-140">singola unità Hello (un grado decimale) offre una posizione in alto too111 chilometri (60 miglia, circa miglia 69).</span><span class="sxs-lookup"><span data-stu-id="f088c-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="f088c-141">Inoltre, indica in quale stato o regione si trova l'utente.</span><span class="sxs-lookup"><span data-stu-id="f088c-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="f088c-142">Hello prima cifra decimale vale la pena di km too11.1: è possibile distinguere posizione hello di una città di grandi dimensioni di una città di grandi dimensioni adiacente.</span><span class="sxs-lookup"><span data-stu-id="f088c-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="f088c-143">Hello seconda posizione decimale vale la pena di km too1.1: è possibile separare una località da hello successivamente.</span><span class="sxs-lookup"><span data-stu-id="f088c-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="f088c-144">terzo decimale Hello vale la pena di m: too110 in grado di identificare un campo agricoltura di grandi dimensioni o istituzionale campus.</span><span class="sxs-lookup"><span data-stu-id="f088c-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="f088c-145">quarto decimale Hello vale la pena di m: too11 in grado di identificare le superfici.</span><span class="sxs-lookup"><span data-stu-id="f088c-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="f088c-146">È confrontabile toohello accuratezza tipico di un'unità GPS non corrette con nessuna interferenza.</span><span class="sxs-lookup"><span data-stu-id="f088c-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="f088c-147">cifra decimale quinto Hello vale la pena di m: too1.1 alberi che distinguono tra loro.</span><span class="sxs-lookup"><span data-stu-id="f088c-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="f088c-148">Livello di toothis accuratezza con unità GPS esterna può essere ottenuto solo con la correzione differenziale.</span><span class="sxs-lookup"><span data-stu-id="f088c-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="f088c-149">cifra decimale sesto Hello vale la pena di m: too0.11 che è possibile utilizzarlo per layout di strutture in dettaglio, per la progettazione di scenari, compilazione strade.</span><span class="sxs-lookup"><span data-stu-id="f088c-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="f088c-150">È più che sufficiente per rilevare i movimenti dei ghiacciai e dei fiumi.</span><span class="sxs-lookup"><span data-stu-id="f088c-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="f088c-151">È possibile ottenere questa accuratezza eseguendo misurazioni accurate con il GPS, quale quello corretto in modo differenziale.</span><span class="sxs-lookup"><span data-stu-id="f088c-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="f088c-152">le informazioni sul percorso Hello può essere trasformato come indicato di seguito, separare i area, percorso e città.</span><span class="sxs-lookup"><span data-stu-id="f088c-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="f088c-153">Si noti che è anche possibile chiamare il punto finale di REST, ad esempio disponibile all'API di Bing Maps [individuare il percorso dal punto](https://msdn.microsoft.com/library/ff701710.aspx) informazioni sulla regione/zona di tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f088c-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="f088c-154">Queste funzionalità in base alla posizione possono essere ulteriormente le funzionalità aggiuntive conteggio toogenerate usato come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f088c-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="f088c-155">A livello di codice, è possibile inserire i record di hello mediante il linguaggio scelto.</span><span class="sxs-lookup"><span data-stu-id="f088c-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="f088c-156">Potrebbe essere necessario dati hello tooinsert l'efficienza di blocchi tooimprove scrittura (per un esempio di come toodo questo uso pyodbc, vedere [tooaccess di esempio HelloWorld A SQL Server con python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="f088c-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="f088c-157">In alternativa è tooinsert dati nel database di hello utilizzando hello [utilità BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="f088c-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="f088c-158"><a name="sql-aml"></a>Connessione tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f088c-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="f088c-159">funzionalità Hello appena generato può aggiunto come colonna tooan tabella esistente o archiviati in una nuova tabella e unito in join alla tabella originale di hello per machine learning.</span><span class="sxs-lookup"><span data-stu-id="f088c-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="f088c-160">Funzionalità possono essere generate o accedere se è già stato creato, utilizzando hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f088c-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![lettori azureml][1] 

## <span data-ttu-id="f088c-162"><a name="python"></a>Utilizzo di un linguaggio di programmazione quale Python</span><span class="sxs-lookup"><span data-stu-id="f088c-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="f088c-163">Utilizzando i dati di tooexplore Python e generare funzionalità quando hello dati sono disponibile in SQL Server è dati tooprocessing simili in blob di Azure usando Python, come documentato [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f088c-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="f088c-164">dati Hello deve toobe caricati dal database hello in un frame di dati pandas e quindi possono essere elaborati ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="f088c-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="f088c-165">Abbiamo documento processo hello di connessione database toohello e il caricamento dei dati hello in frame di dati hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f088c-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="f088c-166">Hello seguente formato di stringa di connessione può essere utilizzato tooconnect tooa database di SQL Server da Python mediante pyodbc (sostituire servername, dbname, username e password con i valori specifici):</span><span class="sxs-lookup"><span data-stu-id="f088c-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="f088c-167">Hello [libreria Pandas](http://pandas.pydata.org/) in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="f088c-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="f088c-168">codice Hello seguente legge hello restituiti da un database di SQL Server in un frame di dati Pandas:</span><span class="sxs-lookup"><span data-stu-id="f088c-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="f088c-169">È ora possibile lavorare con i frame di dati Pandas hello come illustrato nell'articolo hello [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f088c-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="f088c-170">Analisi scientifica dei dati di Azure nell'esempio di azione</span><span class="sxs-lookup"><span data-stu-id="f088c-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="f088c-171">Per un esempio di questa procedura dettagliata end-to-end di hello processo di analisi scientifica dei dati di Azure usando un set di dati pubblici, vedere [processo di analisi scientifica dei dati di Azure nell'azione](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f088c-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

