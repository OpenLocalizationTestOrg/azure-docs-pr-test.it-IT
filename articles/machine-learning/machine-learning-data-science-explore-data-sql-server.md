---
title: dati aaaExplore nella macchina virtuale SQL Server in Azure | Documenti Microsoft
description: Come tooexplore i dati archiviati in una macchina virtuale di SQL Server in Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="1e0f4-103">Esplorazione dei dati nella macchina virtuale di SQL Server in Azure</span><span class="sxs-lookup"><span data-stu-id="1e0f4-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="1e0f4-104">Questo documento descrive come tooexplore i dati archiviati in una macchina virtuale di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="1e0f4-105">Questa operazione può essere eseguita gestendo i dati tramite SQL o utilizzando un linguaggio di programmazione come Python.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="1e0f4-106">esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="1e0f4-107">Questa attività è un passaggio di hello Cortana Analitica processo (CAP).</span><span class="sxs-lookup"><span data-stu-id="1e0f4-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="1e0f4-108">le istruzioni SQL Hello in questo documento si presuppongono che i dati siano in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="1e0f4-109">In caso contrario, fare riferimento toohello cloud data science processo mappa toolearn come toomove il tooSQL dati Server.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="1e0f4-110"><a name="sql-dataexploration"></a>Esplorare i dati SQL mediante gli script SQL</span><span class="sxs-lookup"><span data-stu-id="1e0f4-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="1e0f4-111">Ecco alcuni script SQL di esempio che possono essere utilizzati tooexplore archivi di dati in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="1e0f4-112">Ottenere il conteggio di hello di osservazioni al giorno</span><span class="sxs-lookup"><span data-stu-id="1e0f4-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="1e0f4-113">Ottenere livelli hello in una colonna categorica</span><span class="sxs-lookup"><span data-stu-id="1e0f4-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="1e0f4-114">Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche</span><span class="sxs-lookup"><span data-stu-id="1e0f4-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="1e0f4-115">Ottenere la distribuzione hello per le colonne numeriche</span><span class="sxs-lookup"><span data-stu-id="1e0f4-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="1e0f4-116">Per un esempio pratico, è possibile utilizzare hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) e fare riferimento toohello IPNB intitolato [dati NYC wrangling utilizzando SQL Server e IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) per una procedura dettagliata end-to-end.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="1e0f4-117"><a name="python"></a>Esplorare i dati SQL mediante Python</span><span class="sxs-lookup"><span data-stu-id="1e0f4-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="1e0f4-118">Utilizzando i dati di tooexplore Python e generare funzionalità quando hello dati sono disponibile in SQL Server simile tooprocessing dati in blob di Azure usando Python, come documentato [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1e0f4-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="1e0f4-119">dati Hello deve toobe caricati dal database hello un pandas frame di dati e quindi possono essere elaborati ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="1e0f4-120">Abbiamo documento processo hello di connessione database toohello e caricarvi i dati di hello hello frame di dati in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="1e0f4-121">Hello seguente formato di stringa di connessione può essere utilizzato tooconnect tooa database di SQL Server da Python mediante pyodbc (sostituire servername, dbname, username e password con i valori specifici):</span><span class="sxs-lookup"><span data-stu-id="1e0f4-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="1e0f4-122">Hello [libreria Pandas](http://pandas.pydata.org/) in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="1e0f4-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="1e0f4-123">Hello codice seguente vengono letti hello restituiti da un database di SQL Server in un frame di dati Pandas:</span><span class="sxs-lookup"><span data-stu-id="1e0f4-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="1e0f4-124">È ora possibile lavorare con hello Pandas frame di dati come illustrato nell'argomento hello [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1e0f4-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="1e0f4-125">Il Cortana Analytics Process nell’esempio di azione</span><span class="sxs-lookup"><span data-stu-id="1e0f4-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="1e0f4-126">Per un esempio di questa procedura dettagliata end-to-end di hello Cortana Analitica processo usando un set di dati pubblici, vedere [hello Team processo di analisi scientifica dei dati in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1e0f4-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

