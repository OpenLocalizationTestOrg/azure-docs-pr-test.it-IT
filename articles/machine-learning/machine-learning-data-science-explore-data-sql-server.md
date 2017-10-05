---
title: Esplorare i dati in una macchina virtuale di SQL Server in Azure| Microsoft Docs
description: Come esplorare i dati archiviati in una macchina virtuale SQL Server in Azure.
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
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="3b7f5-103">Esplorazione dei dati nella macchina virtuale di SQL Server in Azure</span><span class="sxs-lookup"><span data-stu-id="3b7f5-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="3b7f5-104">In questo documento viene illustrato come esplorare i dati archiviati in una macchina virtuale SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="3b7f5-105">Questa operazione può essere eseguita gestendo i dati tramite SQL o utilizzando un linguaggio di programmazione come Python.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="3b7f5-106">Il **menu** seguente collega ad argomenti che descrivono come usare gli strumenti per esplorare i dati da vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="3b7f5-107">Questa attività è un passaggio nel Cortana Analytics Process (CAP).</span><span class="sxs-lookup"><span data-stu-id="3b7f5-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="3b7f5-108">Le istruzioni SQL di esempio fornite nel documento presuppongono che i dati si trovino in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="3b7f5-109">In caso contrario, fare riferimento al processo di analisi scientifica dei dati cloud per visualizzare informazioni su come spostare i dati in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="3b7f5-110"><a name="sql-dataexploration"></a>Esplorare i dati SQL mediante gli script SQL</span><span class="sxs-lookup"><span data-stu-id="3b7f5-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="3b7f5-111">Di seguito, sono riportati alcuni script SQL di esempio da utilizzare per esplorare gli archivi dati in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="3b7f5-112">Visualizzare il numero di osservazioni per giorno</span><span class="sxs-lookup"><span data-stu-id="3b7f5-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="3b7f5-113">Visualizzare i livelli in una colonna di categoria</span><span class="sxs-lookup"><span data-stu-id="3b7f5-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="3b7f5-114">Visualizzare il numero di livelli in una combinazione di due colonne di categoria</span><span class="sxs-lookup"><span data-stu-id="3b7f5-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="3b7f5-115">Visualizzare la distribuzione per colonne numeriche </span><span class="sxs-lookup"><span data-stu-id="3b7f5-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="3b7f5-116">Per un esempio pratico, è possibile usare il [set di dati dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/) e vedere l'IPNB intitolato [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) (Gestione dei dati di NYC tramite IPython Notebook e SQL Server) per una procedura dettagliata end-to-end.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="3b7f5-117"><a name="python"></a>Esplorare i dati SQL mediante Python</span><span class="sxs-lookup"><span data-stu-id="3b7f5-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="3b7f5-118">L'uso di Python per esplorare i dati e creare funzionalità, se i dati si trovano in SQL Server, funziona in modo analogo all'elaborazione dei dati BLOB di Azure tramite Python, come illustrato in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md) (Elaborare i dati BLOB di Azure in un ambiente di analisi scientifica dei dati).</span><span class="sxs-lookup"><span data-stu-id="3b7f5-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="3b7f5-119">I dati devono essere caricati dal database nei frame di dati Panda. A questo punto, è possibile elaborarli ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="3b7f5-120">In questa sezione, è stato descritto il processo di connessione al database per caricare dati all'interno di un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="3b7f5-121">Il seguente formato della stringa di connessione può essere usato per connettersi a un database di SQL Server da Pyhton usando pyodbc (sostituire il nome del server, quello del database, il nome utente e la password con i valori personalizzati):</span><span class="sxs-lookup"><span data-stu-id="3b7f5-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3b7f5-122">La [libreria Pandas](http://pandas.pydata.org/) in Python fornisce una vasta gamma di strutture di dati e strumenti di analisi dei dati per la manipolazione dei dati nella programmazione in Python.</span><span class="sxs-lookup"><span data-stu-id="3b7f5-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3b7f5-123">Il codice seguente consente di leggere i risultati restituiti da un database di SQL Server all'interno di un frame di dati di Pandas:</span><span class="sxs-lookup"><span data-stu-id="3b7f5-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="3b7f5-124">A questo punto, è possibile usare il frame di dati di Pandas, come descritto nell'argomento [Elaborazione dei dati BLOB di Azure nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="3b7f5-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="3b7f5-125">Il Cortana Analytics Process nell’esempio di azione</span><span class="sxs-lookup"><span data-stu-id="3b7f5-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="3b7f5-126">Per un esempio della procedura dettagliata end-to-end del Cortana Analytics Process tramite un set di dati pubblico, vedere [Processo di analisi scientifica dei dati per i team in azione: uso di SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3b7f5-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

