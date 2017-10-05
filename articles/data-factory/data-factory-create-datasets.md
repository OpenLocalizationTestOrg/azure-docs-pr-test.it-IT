---
title: Creare set di dati in Azure Data Factory | Microsoft Docs
description: "Informazioni su come creare set di dati in Azure Data Factory con esempi che usano proprietà quali anchorDateTime e offset."
keywords: creare set di dati, esempio di set di dati, esempio di offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="82bc8-104">Set di dati in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="82bc8-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="82bc8-105">In questo articolo vengono descritti i set di dati, la procedura di definizione dei set in formato JSON e le modalità di utilizzo nelle pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="82bc8-106">L'articolo contiene informazioni dettagliate su ogni sezione della definizione JSON del set di dati, ad esempio su struttura, disponibilità e criteri.</span><span class="sxs-lookup"><span data-stu-id="82bc8-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="82bc8-107">L'articolo offre anche esempi per l'uso delle proprietà **offset**, **anchorDateTime** e **style** in una definizione JSON del set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="82bc8-108">Se non si ha dimestichezza con Data Factory, vedere [Introduzione al servizio Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="82bc8-109">Se non si ha esperienza diretta nella creazione di data factory, vedere l'[esercitazione sulla trasformazione dei dati](data-factory-build-your-first-pipeline.md) e [quella sullo spostamento dei dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per comprendere meglio questi argomenti.</span><span class="sxs-lookup"><span data-stu-id="82bc8-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="82bc8-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="82bc8-110">Overview</span></span>
<span data-ttu-id="82bc8-111">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="82bc8-112">Una **pipeline** è un raggruppamento logico di **attività** che insieme eseguono un compito.</span><span class="sxs-lookup"><span data-stu-id="82bc8-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="82bc8-113">Le attività in una pipeline definiscono le azioni da eseguire sui dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="82bc8-114">Ad esempio, è possibile usare un'attività di copia per copiare i dati da un Server SQL locale a un'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="82bc8-115">Quindi, si può usare un'attività Hive che esegue uno script Hive in un cluster HDInsight di Azure per elaborare i dati dall'archiviazione BLOB per produrre dati di output.</span><span class="sxs-lookup"><span data-stu-id="82bc8-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="82bc8-116">Infine, è possibile usare una seconda attività di copia per copiare i dati di output in Azure SQL Data Warehouse per la compilazione delle soluzioni di report di business intelligence (BI).</span><span class="sxs-lookup"><span data-stu-id="82bc8-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="82bc8-117">Per altre informazioni su pipeline e attività, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="82bc8-118">Un'attività può non avere alcun **set di dati** di input o averne più di uno e generare uno o più set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="82bc8-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="82bc8-119">Un set di dati di input rappresenta l'input per un'attività nella pipeline, un set di dati di output rappresenta l'output dell'attività.</span><span class="sxs-lookup"><span data-stu-id="82bc8-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="82bc8-120">I set di dati identificano i dati all'interno dei diversi archivi dati, come tabelle, file, cartelle e documenti.</span><span class="sxs-lookup"><span data-stu-id="82bc8-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="82bc8-121">Un set di dati BLOB di Azure, ad esempio, specifica il contenitore BLOB e la cartella nell'archiviazione BLOB da cui la pipeline dovrà leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="82bc8-122">Prima di creare un set di dati, creare un **servizio collegato** per collegare l'archivio dati alla data factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="82bc8-123">I servizi collegati sono molto simili a stringhe di connessione e definiscono le informazioni necessarie per la connessione di Data Factory a risorse esterne.</span><span class="sxs-lookup"><span data-stu-id="82bc8-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="82bc8-124">I set di dati identificano i dati all'interno dei diversi archivi dati, come tabelle, file, cartelle e documenti di SQL.</span><span class="sxs-lookup"><span data-stu-id="82bc8-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="82bc8-125">Il servizio collegato Archiviazione di Azure,ad esempio, collega l'account di archiviazione alla data factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="82bc8-126">Un set di dati BLOB di Azure rappresenta il contenitore e la cartella BLOB che contengono i BLOB di input da elaborare.</span><span class="sxs-lookup"><span data-stu-id="82bc8-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="82bc8-127">Di seguito è riportato uno scenario di esempio.</span><span class="sxs-lookup"><span data-stu-id="82bc8-127">Here is a sample scenario.</span></span> <span data-ttu-id="82bc8-128">Per copiare i dati da un'archiviazione BLOB a un Database SQL, si creano due servizi collegati: Archiviazione di Azure e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="82bc8-129">Quindi, si creano due set di dati: un set di dati BLOB di Azure, che si riferisce al servizio collegato Archiviazione di Azure, e un set di dati della tabella SQL di Azure, che si riferisce al servizio collegato Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="82bc8-130">I servizi collegati Archiviazione di Azure e Database SQL di Azure contengono stringhe di connessione usate da Data Factory in fase di runtime per connettersi rispettivamente all'archiviazione di Azure e al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="82bc8-131">Il set di dati BLOB di Azure specifica il contenitore e una cartella BLOB che contengono i BLOB di input presenti nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="82bc8-132">Il set di dati della tabella SQL di Azure specifica la tabella SQL del database SQL in cui verranno copiati i dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="82bc8-133">Nel diagramma seguente viene illustrata la relazione tra pipeline, attività, set di dati e il servizio collegato in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="82bc8-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relazione tra pipeline, attività, set di dati, i servizi collegati](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="82bc8-135">Set di dati JSON</span><span class="sxs-lookup"><span data-stu-id="82bc8-135">Dataset JSON</span></span>
<span data-ttu-id="82bc8-136">Un set di dati in Data Factory viene definito in formato JSON come segue:</span><span class="sxs-lookup"><span data-stu-id="82bc8-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="82bc8-137">La tabella seguente descrive le proprietà nel codice JSON precedente:</span><span class="sxs-lookup"><span data-stu-id="82bc8-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="82bc8-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="82bc8-138">Property</span></span> | <span data-ttu-id="82bc8-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82bc8-139">Description</span></span> | <span data-ttu-id="82bc8-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="82bc8-140">Required</span></span> | <span data-ttu-id="82bc8-141">Default</span><span class="sxs-lookup"><span data-stu-id="82bc8-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82bc8-142">name</span><span class="sxs-lookup"><span data-stu-id="82bc8-142">name</span></span> |<span data-ttu-id="82bc8-143">Nome del set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-143">Name of the dataset.</span></span> <span data-ttu-id="82bc8-144">Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="82bc8-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="82bc8-145">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-145">Yes</span></span> |<span data-ttu-id="82bc8-146">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-146">NA</span></span> |
| <span data-ttu-id="82bc8-147">type</span><span class="sxs-lookup"><span data-stu-id="82bc8-147">type</span></span> |<span data-ttu-id="82bc8-148">Tipo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-148">Type of the dataset.</span></span> <span data-ttu-id="82bc8-149">Specificare uno dei tipi supportati da Data Factory, ad esempio AzureBlob o AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="82bc8-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="82bc8-150">Per informazioni dettagliate, vedere [Tipo di set di dati](#Type).</span><span class="sxs-lookup"><span data-stu-id="82bc8-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="82bc8-151">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-151">Yes</span></span> |<span data-ttu-id="82bc8-152">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-152">NA</span></span> |
| <span data-ttu-id="82bc8-153">structure</span><span class="sxs-lookup"><span data-stu-id="82bc8-153">structure</span></span> |<span data-ttu-id="82bc8-154">Schema del set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="82bc8-155">Per informazioni dettagliate, vedere [Struttura del set di dati](#Structure).</span><span class="sxs-lookup"><span data-stu-id="82bc8-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="82bc8-156">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-156">No</span></span> |<span data-ttu-id="82bc8-157">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-157">NA</span></span> |
| <span data-ttu-id="82bc8-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="82bc8-158">typeProperties</span></span> | <span data-ttu-id="82bc8-159">Le proprietà del tipo sono diverse per ogni tipo, ad esempio: BLOB di Azure, tabella SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="82bc8-160">Per informazioni dettagliate sui tipi supportati e le relative proprietà, vedere la sezione [Tipo di set di dati](#Type).</span><span class="sxs-lookup"><span data-stu-id="82bc8-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="82bc8-161">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-161">Yes</span></span> |<span data-ttu-id="82bc8-162">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-162">NA</span></span> |
| <span data-ttu-id="82bc8-163">external</span><span class="sxs-lookup"><span data-stu-id="82bc8-163">external</span></span> | <span data-ttu-id="82bc8-164">Flag booleano per specificare se un set di dati è generato o meno in modo esplicito da una pipeline della data factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="82bc8-165">Se il set di dati di input per un'attività non viene generato dalla pipeline corrente, impostare questo flag su true.</span><span class="sxs-lookup"><span data-stu-id="82bc8-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="82bc8-166">Impostare questo flag su true per il set di dati di input della prima attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="82bc8-167">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-167">No</span></span> |<span data-ttu-id="82bc8-168">false</span><span class="sxs-lookup"><span data-stu-id="82bc8-168">false</span></span> |
| <span data-ttu-id="82bc8-169">disponibilità</span><span class="sxs-lookup"><span data-stu-id="82bc8-169">availability</span></span> | <span data-ttu-id="82bc8-170">Definisce l'intervallo di elaborazione, ad esempio orario o giornaliero, o il modello di sezionamento per la produzione di set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="82bc8-171">Ogni unità di dati usata e prodotta da un'esecuzione di attività prende il nome di sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="82bc8-172">Se la disponibilità di un set di dati di output è impostata su giornaliera, ad esempio frequenza: giorno, intervallo: 1, viene prodotta una sezione ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="82bc8-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="82bc8-173">Per informazioni dettagliate, vedere [Disponibilità dei set di dati](#Availability).</span><span class="sxs-lookup"><span data-stu-id="82bc8-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="82bc8-174">Per informazioni dettagliate sul modello di sezionamento dei set di dati, vedere l'articolo [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="82bc8-175">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-175">Yes</span></span> |<span data-ttu-id="82bc8-176">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-176">NA</span></span> |
| <span data-ttu-id="82bc8-177">policy</span><span class="sxs-lookup"><span data-stu-id="82bc8-177">policy</span></span> |<span data-ttu-id="82bc8-178">Definisce i criteri o la condizione che devono soddisfare i sezionamenti di set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="82bc8-179">Per informazioni dettagliate, vedere la sezione [Criteri di set di dati](#Policy).</span><span class="sxs-lookup"><span data-stu-id="82bc8-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="82bc8-180">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-180">No</span></span> |<span data-ttu-id="82bc8-181">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="82bc8-182">Esempio di set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-182">Dataset example</span></span>
<span data-ttu-id="82bc8-183">Nell'esempio seguente il set di dati rappresenta la tabella **MyTable** in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="82bc8-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="82bc8-184">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="82bc8-184">Note the following points:</span></span>

* <span data-ttu-id="82bc8-185">**type** è impostato su AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="82bc8-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="82bc8-186">La proprietà del tipo **tableName**, specifica del tipo AzureSqlTable, è impostata su MyTable.</span><span class="sxs-lookup"><span data-stu-id="82bc8-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="82bc8-187">**linkedServiceName** fa riferimento a un servizio collegato di tipo AzureSqlDatabase, definito nel frammento di codice JSON successivo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="82bc8-188">L'oggetto **availability frequency** è impostato su Day e **interval** è impostato su 1.</span><span class="sxs-lookup"><span data-stu-id="82bc8-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="82bc8-189">Ciò significa che la sezione di set di dati viene prodotta ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="82bc8-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="82bc8-190">**AzureSqlLinkedService** è definito come segue:</span><span class="sxs-lookup"><span data-stu-id="82bc8-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="82bc8-191">Nel frammento di codice JSON precedente:</span><span class="sxs-lookup"><span data-stu-id="82bc8-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="82bc8-192">**type** è impostato su AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="82bc8-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="82bc8-193">La proprietà del tipo **connectionString** specifica le informazioni per la connessione a un database SQL.</span><span class="sxs-lookup"><span data-stu-id="82bc8-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="82bc8-194">Come si può notare, il servizio collegato definisce la modalità di connessione a un database SQL.</span><span class="sxs-lookup"><span data-stu-id="82bc8-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="82bc8-195">Il set di dati indica quale tabella viene usata come input e output per l'attività in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="82bc8-196">A meno che un set di dati non sia generato dalla pipeline, deve essere contrassegnato come **esterno**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="82bc8-197">Questa impostazione vale in genere per gli input della prima attività in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="82bc8-198"><a name="Type"></a> Tipo di set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="82bc8-199">Il tipo del set di dati dipende dall'archivio dati usato.</span><span class="sxs-lookup"><span data-stu-id="82bc8-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="82bc8-200">Vedere la tabella seguente per un elenco di archivi dati supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="82bc8-201">Fare clic su un archivio dati per informazioni su come creare un servizio collegato e un set di dati per tale archivio dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="82bc8-202">Gli archivi dati con * possono essere locali o in un'infrastruttura distribuita come servizio (IaaS) di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="82bc8-203">Questi archivi di dati richiedono l'installazione del [gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="82bc8-204">Nell'esempio della sezione precedente, il tipo di set di dati è impostato su **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="82bc8-205">Analogamente, per un set di dati BLOB di Azure, il tipo di set di dati è impostato su **AzureBlob** come illustrato nel codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="82bc8-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="82bc8-206"><a name="Structure"></a>Struttura del set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="82bc8-207">La sezione **structure** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="82bc8-207">The **structure** section is optional.</span></span> <span data-ttu-id="82bc8-208">Definisce lo schema del set di dati presentando una raccolta di nomi e tipi di dati delle colonne.</span><span class="sxs-lookup"><span data-stu-id="82bc8-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="82bc8-209">Usare la sezione structure per inserire informazioni sul tipo da usare per convertire i tipi e mappare le colonne dall'origine alla destinazione.</span><span class="sxs-lookup"><span data-stu-id="82bc8-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="82bc8-210">Nell'esempio seguente il set di dati include tre colonne: `slicetimestamp`, `projectname` e `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="82bc8-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="82bc8-211">Sono rispettivamente di tipo String, String e Decimal.</span><span class="sxs-lookup"><span data-stu-id="82bc8-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="82bc8-212">Ogni colonna della struttura contiene le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="82bc8-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="82bc8-213">Proprietà</span><span class="sxs-lookup"><span data-stu-id="82bc8-213">Property</span></span> | <span data-ttu-id="82bc8-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82bc8-214">Description</span></span> | <span data-ttu-id="82bc8-215">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="82bc8-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82bc8-216">name</span><span class="sxs-lookup"><span data-stu-id="82bc8-216">name</span></span> |<span data-ttu-id="82bc8-217">Nome della colonna.</span><span class="sxs-lookup"><span data-stu-id="82bc8-217">Name of the column.</span></span> |<span data-ttu-id="82bc8-218">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-218">Yes</span></span> |
| <span data-ttu-id="82bc8-219">type</span><span class="sxs-lookup"><span data-stu-id="82bc8-219">type</span></span> |<span data-ttu-id="82bc8-220">Tipo di dati della colonna.</span><span class="sxs-lookup"><span data-stu-id="82bc8-220">Data type of the column.</span></span>  |<span data-ttu-id="82bc8-221">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-221">No</span></span> |
| <span data-ttu-id="82bc8-222">culture</span><span class="sxs-lookup"><span data-stu-id="82bc8-222">culture</span></span> |<span data-ttu-id="82bc8-223">Cultura basata su .NET da usare quando il tipo è un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="82bc8-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="82bc8-224">Il valore predefinito è `en-us`.</span><span class="sxs-lookup"><span data-stu-id="82bc8-224">The default is `en-us`.</span></span> |<span data-ttu-id="82bc8-225">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-225">No</span></span> |
| <span data-ttu-id="82bc8-226">format</span><span class="sxs-lookup"><span data-stu-id="82bc8-226">format</span></span> |<span data-ttu-id="82bc8-227">Stringa di formato da usare quando il tipo è un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="82bc8-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="82bc8-228">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-228">No</span></span> |

<span data-ttu-id="82bc8-229">Attenersi alle linee guida seguenti per decidere quando includere le informazioni sulla struttura e quali elementi inserire nella sezione **structure** .</span><span class="sxs-lookup"><span data-stu-id="82bc8-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="82bc8-230">**Per le origini dati strutturate**, specificare la sezione structure solo se si vuole eseguire il mapping delle colonne di origine alle colonne del sink e i nomi delle colonne non sono uguali.</span><span class="sxs-lookup"><span data-stu-id="82bc8-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="82bc8-231">Questa tipologia di origine dati strutturata archivia le informazioni relative al tipo e allo schema dei dati insieme ai dati stessi.</span><span class="sxs-lookup"><span data-stu-id="82bc8-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="82bc8-232">Alcuni esempi di origini dati strutturate sono SQL Server, Oracle e la tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="82bc8-233">Poiché per le origini dati strutturate le informazioni sul tipo sono già disponibili, non includere le informazioni sul tipo quando si include la sezione structure.</span><span class="sxs-lookup"><span data-stu-id="82bc8-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="82bc8-234">**Per lo schema delle origini dati di lettura, in particolare l'archiviazione BLOB**, è possibile scegliere di archiviare i dati senza aggiungere alcuna informazione sullo schema o sul tipo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="82bc8-235">Per questi tipi di origini dati, includere la sezione structure per eseguire il mapping delle colonne di origine alle colonne del sink.</span><span class="sxs-lookup"><span data-stu-id="82bc8-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="82bc8-236">Includere la sezione structure anche quando il set di dati è un input per un'attività di copia e i tipi di dati del set di dati di origine devono essere convertiti in tipi nativi per il sink.</span><span class="sxs-lookup"><span data-stu-id="82bc8-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="82bc8-237">Data Factory supporta i seguenti valori per specificare informazioni sul tipo nella sezione structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset e Timespan**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="82bc8-238">Sono valori dei tipi basati su .NET e conformi a CLS (Common Language Specification).</span><span class="sxs-lookup"><span data-stu-id="82bc8-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="82bc8-239">La data factory esegue automaticamente le conversioni quando si spostano dati da un archivio dati di origine a un archivio dati di sink.</span><span class="sxs-lookup"><span data-stu-id="82bc8-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="82bc8-240">Disponibilità dei set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-240">Dataset availability</span></span>
<span data-ttu-id="82bc8-241">La sezione **availability** di un set di dati definisce l'intervallo di elaborazione, ad esempio orario, giornaliero o settimanale, per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="82bc8-242">Per altre informazioni sugli intervalli di attività, vedere [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="82bc8-243">La sezione availability seguente specifica che il set di dati di output viene generato ogni ora oppure che il set di dati di input è disponibile ogni ora:</span><span class="sxs-lookup"><span data-stu-id="82bc8-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="82bc8-244">Se la pipeline ha i seguenti orari di inizio e fine:</span><span class="sxs-lookup"><span data-stu-id="82bc8-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="82bc8-245">Viene prodotto il set di dati di output ogni ora entro gli orari di inizio e fine della pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="82bc8-246">Questa pipeline genera quindi cinque sezioni di set di dati, una per ogni intervallo di attività (00:00 - 01:00, 01: 00 - 02:00, 02:00 - 03:00, 03:00 - 04:00, 04:00 - 05:00).</span><span class="sxs-lookup"><span data-stu-id="82bc8-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="82bc8-247">La tabella seguente descrive le proprietà che è possibile usare nella sezione availability:</span><span class="sxs-lookup"><span data-stu-id="82bc8-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="82bc8-248">Proprietà</span><span class="sxs-lookup"><span data-stu-id="82bc8-248">Property</span></span> | <span data-ttu-id="82bc8-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82bc8-249">Description</span></span> | <span data-ttu-id="82bc8-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="82bc8-250">Required</span></span> | <span data-ttu-id="82bc8-251">Default</span><span class="sxs-lookup"><span data-stu-id="82bc8-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82bc8-252">frequency</span><span class="sxs-lookup"><span data-stu-id="82bc8-252">frequency</span></span> |<span data-ttu-id="82bc8-253">Specifica l'unità di tempo per la produzione di sezioni di set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="82bc8-254"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="82bc8-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="82bc8-255">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-255">Yes</span></span> |<span data-ttu-id="82bc8-256">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-256">NA</span></span> |
| <span data-ttu-id="82bc8-257">interval</span><span class="sxs-lookup"><span data-stu-id="82bc8-257">interval</span></span> |<span data-ttu-id="82bc8-258">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="82bc8-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="82bc8-259">"Frequency x interval" determina la frequenza con cui viene generata la sezione.</span><span class="sxs-lookup"><span data-stu-id="82bc8-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="82bc8-260">Se ad esempio è necessario suddividere il set di dati su base oraria, impostare <b>frequency</b> su <b>Hour</b> e <b>interval</b> su <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="82bc8-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="82bc8-261">Notare che se si specifica **frequency** come **Minute**, è necessario impostare interval su un valore non inferiore a 15.</span><span class="sxs-lookup"><span data-stu-id="82bc8-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="82bc8-262">Sì</span><span class="sxs-lookup"><span data-stu-id="82bc8-262">Yes</span></span> |<span data-ttu-id="82bc8-263">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-263">NA</span></span> |
| <span data-ttu-id="82bc8-264">style</span><span class="sxs-lookup"><span data-stu-id="82bc8-264">style</span></span> |<span data-ttu-id="82bc8-265">Specifica se la sezione deve essere generata all'inizio o alla fine dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="82bc8-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="82bc8-266">StartOfInterval</span></span></li><li><span data-ttu-id="82bc8-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="82bc8-267">EndOfInterval</span></span></li></ul><span data-ttu-id="82bc8-268">Se **frequency** è impostata su **Month** e **style** è impostata su **EndOfInterval**, la sezione viene generata l'ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="82bc8-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="82bc8-269">Se **style** è impostata su **StartOfInterval**, la sezione viene generata il primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="82bc8-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="82bc8-270">Se **frequency** è impostata su **Day** e **style** è impostata su **EndOfInterval**, la sezione viene generata nell'ultima ora del giorno.</span><span class="sxs-lookup"><span data-stu-id="82bc8-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="82bc8-271">Se **frequency** è impostata su **Hour** e **style** è impostata su **EndOfInterval**, la sezione viene generata alla fine dell'ora.</span><span class="sxs-lookup"><span data-stu-id="82bc8-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="82bc8-272">Ad esempio, una sezione per il periodo 13.00 - 14.00 viene generata alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="82bc8-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="82bc8-273">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-273">No</span></span> |<span data-ttu-id="82bc8-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="82bc8-274">EndOfInterval</span></span> |
| <span data-ttu-id="82bc8-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="82bc8-275">anchorDateTime</span></span> |<span data-ttu-id="82bc8-276">Definisce la posizione assoluta nel tempo usata dall'utilità di pianificazione per calcolare i limiti della sezione del set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="82bc8-277">Si noti che se questa proprietà include parti della data più granulari rispetto alla frequenza specificata, le parti più granulari vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="82bc8-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="82bc8-278">Ad esempio, se l'**intervallo** è **orario** (frequency: hour e interval: 1) e la proprietà **anchorDateTime** contiene **minuti e secondi**, le parti di **anchorDateTime** relative a minuti e secondi vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="82bc8-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="82bc8-279">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-279">No</span></span> |<span data-ttu-id="82bc8-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="82bc8-280">01/01/0001</span></span> |
| <span data-ttu-id="82bc8-281">offset</span><span class="sxs-lookup"><span data-stu-id="82bc8-281">offset</span></span> |<span data-ttu-id="82bc8-282">Intervallo di tempo in base al quale l'inizio e la fine di tutte le sezioni dei set di dati vengono spostate.</span><span class="sxs-lookup"><span data-stu-id="82bc8-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="82bc8-283">Notare che se si specifica sia **anchorDateTime** che **offset**, il risultato sarà lo spostamento combinato.</span><span class="sxs-lookup"><span data-stu-id="82bc8-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="82bc8-284">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-284">No</span></span> |<span data-ttu-id="82bc8-285">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="82bc8-286">Esempio di offset</span><span class="sxs-lookup"><span data-stu-id="82bc8-286">offset example</span></span>
<span data-ttu-id="82bc8-287">Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00.00 (mezzanotte) UTC (Coordinated Universal Time).</span><span class="sxs-lookup"><span data-stu-id="82bc8-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="82bc8-288">Se, invece, si desidera impostare l'ora di inizio alle 06:00 UTC, impostare l'offset come illustrato nel frammento riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="82bc8-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="82bc8-289">Esempio di anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="82bc8-289">anchorDateTime example</span></span>
<span data-ttu-id="82bc8-290">Nell'esempio seguente, il set di dati viene prodotto ogni 23 ore.</span><span class="sxs-lookup"><span data-stu-id="82bc8-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="82bc8-291">La prima sezione inizia all'ora specificata da **anchorDateTime**, che è impostata su `2017-04-19T08:00:00` (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="82bc8-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="82bc8-292">Esempio di offset/style</span><span class="sxs-lookup"><span data-stu-id="82bc8-292">offset/style example</span></span>
<span data-ttu-id="82bc8-293">Il seguente set di dati è mensile e viene generato il giorno 3 di ogni mese alle ore 08:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="82bc8-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="82bc8-294"><a name="Policy"></a>Criteri di set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="82bc8-295">La sezione **policy** nella definizione del set di dati stabilisce i criteri o la condizione che le sezioni del set di dati devono soddisfare.</span><span class="sxs-lookup"><span data-stu-id="82bc8-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="82bc8-296">Criteri di convalida</span><span class="sxs-lookup"><span data-stu-id="82bc8-296">Validation policies</span></span>
| <span data-ttu-id="82bc8-297">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="82bc8-297">Policy name</span></span> | <span data-ttu-id="82bc8-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82bc8-298">Description</span></span> | <span data-ttu-id="82bc8-299">Applicato a</span><span class="sxs-lookup"><span data-stu-id="82bc8-299">Applied to</span></span> | <span data-ttu-id="82bc8-300">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="82bc8-300">Required</span></span> | <span data-ttu-id="82bc8-301">Default</span><span class="sxs-lookup"><span data-stu-id="82bc8-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="82bc8-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="82bc8-302">minimumSizeMB</span></span> |<span data-ttu-id="82bc8-303">Verifica che i dati presenti nell'**archiviazione BLOB di Azure** soddisfino i requisiti relativi alle dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="82bc8-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="82bc8-304">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="82bc8-304">Azure Blob storage</span></span> |<span data-ttu-id="82bc8-305">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-305">No</span></span> |<span data-ttu-id="82bc8-306">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-306">NA</span></span> |
| <span data-ttu-id="82bc8-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="82bc8-307">minimumRows</span></span> |<span data-ttu-id="82bc8-308">Verifica che i dati in un **database SQL di Azure** o in una **tabella di Azure** contengano il numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="82bc8-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="82bc8-309">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="82bc8-309">Azure SQL database</span></span></li><li><span data-ttu-id="82bc8-310">Tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="82bc8-310">Azure table</span></span></li></ul> |<span data-ttu-id="82bc8-311">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-311">No</span></span> |<span data-ttu-id="82bc8-312">ND</span><span class="sxs-lookup"><span data-stu-id="82bc8-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="82bc8-313">esempi</span><span class="sxs-lookup"><span data-stu-id="82bc8-313">Examples</span></span>
<span data-ttu-id="82bc8-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="82bc8-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="82bc8-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="82bc8-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="82bc8-316">Set di dati esterni</span><span class="sxs-lookup"><span data-stu-id="82bc8-316">External datasets</span></span>
<span data-ttu-id="82bc8-317">I set di dati esterni sono quelli non prodotti da una pipeline in esecuzione nella data factory.</span><span class="sxs-lookup"><span data-stu-id="82bc8-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="82bc8-318">Se il set di dati è contrassegnato come **external**, è possibile definire i criteri di **ExternalData** in modo da influenzare il comportamento della disponibilità di sezioni dei set di dati.</span><span class="sxs-lookup"><span data-stu-id="82bc8-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="82bc8-319">A meno che non sia generato da Data Factory, il set di dati deve essere contrassegnato come **external**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="82bc8-320">Questa impostazione si applica in genere agli input della prima attività di una pipeline, a meno che non si usi il concatenamento di attività o di pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="82bc8-321">Nome</span><span class="sxs-lookup"><span data-stu-id="82bc8-321">Name</span></span> | <span data-ttu-id="82bc8-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="82bc8-322">Description</span></span> | <span data-ttu-id="82bc8-323">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="82bc8-323">Required</span></span> | <span data-ttu-id="82bc8-324">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="82bc8-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82bc8-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="82bc8-325">dataDelay</span></span> |<span data-ttu-id="82bc8-326">Tempo di ritardo del controllo della disponibilità dei dati esterni per la sezione specificata.</span><span class="sxs-lookup"><span data-stu-id="82bc8-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="82bc8-327">Ad esempio, è possibile ritardare un controllo orario usando questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="82bc8-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="82bc8-328">Si applica solo all'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="82bc8-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="82bc8-329">Ad esempio, se in questo momento sono le 13:00 e questo valore è di 10 minuti, la convalida inizia alle 13:10.</span><span class="sxs-lookup"><span data-stu-id="82bc8-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="82bc8-330">Si noti che questa impostazione non influisce sulle sezioni passate.</span><span class="sxs-lookup"><span data-stu-id="82bc8-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="82bc8-331">Le sezioni con **Slice End Time** + **dataDelay** < **Now** vengono elaborate senza alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="82bc8-332">I valori orari superiori a 23:59 ore devono essere specificati nel formato `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="82bc8-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="82bc8-333">Per specificare 24 ore, ad esempio, non usare 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="82bc8-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="82bc8-334">Usare invece 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="82bc8-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="82bc8-335">Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="82bc8-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="82bc8-336">Per 1 giorno e 4 ore, specificare 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="82bc8-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="82bc8-337">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-337">No</span></span> |<span data-ttu-id="82bc8-338">0</span><span class="sxs-lookup"><span data-stu-id="82bc8-338">0</span></span> |
| <span data-ttu-id="82bc8-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="82bc8-339">retryInterval</span></span> |<span data-ttu-id="82bc8-340">Tempo di attesa tra un errore e il tentativo successivo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="82bc8-341">Questa impostazione si applica all'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="82bc8-341">This setting applies to present time.</span></span> <span data-ttu-id="82bc8-342">Se il tentativo precedente ha avuto esito negativo, il tentativo successivo si avvia dopo il periodo **retryInterval**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="82bc8-343">Se in questo momento sono le 13:00, viene avviato il primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="82bc8-344">Se la durata per completare il primo controllo di convalida è 1 minuto e l'operazione non è riuscita, il tentativo successivo è alle 13:00 + 1 min (durata) + 1 min (intervallo tentativi) = 13:02.</span><span class="sxs-lookup"><span data-stu-id="82bc8-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="82bc8-345">Per le sezioni passate, non si verifica alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="82bc8-346">La ripetizione avviene immediatamente.</span><span class="sxs-lookup"><span data-stu-id="82bc8-346">The retry happens immediately.</span></span> |<span data-ttu-id="82bc8-347">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-347">No</span></span> |<span data-ttu-id="82bc8-348">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="82bc8-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="82bc8-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="82bc8-349">retryTimeout</span></span> |<span data-ttu-id="82bc8-350">Timeout per ogni nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="82bc8-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="82bc8-351">Se questa proprietà è impostata su 10 minuti, la convalida deve essere completata entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="82bc8-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="82bc8-352">Se sono necessari più di 10 minuti per eseguire la convalida, il tentativo viene sospeso.</span><span class="sxs-lookup"><span data-stu-id="82bc8-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="82bc8-353">Se tutti i tentativi per la convalida raggiungono il timeout, la sezione viene contrassegnata come **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="82bc8-354">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-354">No</span></span> |<span data-ttu-id="82bc8-355">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="82bc8-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="82bc8-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="82bc8-356">maximumRetry</span></span> |<span data-ttu-id="82bc8-357">Numero di tentativi di controllo della disponibilità dei dati esterni.</span><span class="sxs-lookup"><span data-stu-id="82bc8-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="82bc8-358">Il valore massimo consentito è 10.</span><span class="sxs-lookup"><span data-stu-id="82bc8-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="82bc8-359">No</span><span class="sxs-lookup"><span data-stu-id="82bc8-359">No</span></span> |<span data-ttu-id="82bc8-360">3</span><span class="sxs-lookup"><span data-stu-id="82bc8-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="82bc8-361">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-361">Create datasets</span></span>
<span data-ttu-id="82bc8-362">È possibile creare set di dati usando uno di questi strumenti o SDK:</span><span class="sxs-lookup"><span data-stu-id="82bc8-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="82bc8-363">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="82bc8-363">Copy Wizard</span></span> 
- <span data-ttu-id="82bc8-364">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="82bc8-364">Azure portal</span></span>
- <span data-ttu-id="82bc8-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82bc8-365">Visual Studio</span></span>
- <span data-ttu-id="82bc8-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82bc8-366">PowerShell</span></span>
- <span data-ttu-id="82bc8-367">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82bc8-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="82bc8-368">API REST</span><span class="sxs-lookup"><span data-stu-id="82bc8-368">REST API</span></span>
- <span data-ttu-id="82bc8-369">API .NET</span><span class="sxs-lookup"><span data-stu-id="82bc8-369">.NET API</span></span>

<span data-ttu-id="82bc8-370">Vedere le esercitazioni seguenti per istruzioni dettagliate sulla creazione di pipeline e set di dati usando uno di questi strumenti o SDK:</span><span class="sxs-lookup"><span data-stu-id="82bc8-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="82bc8-371">Creare una pipeline con un'attività di trasformazione dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="82bc8-372">Creare una pipeline con un'attività di spostamento dati</span><span class="sxs-lookup"><span data-stu-id="82bc8-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="82bc8-373">Dopo aver creato e distribuito una pipeline, è possibile gestire e monitorare le pipeline usando i pannelli del portale di Azure o l'app di gestione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="82bc8-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="82bc8-374">Vedere gli argomenti seguenti per le istruzioni dettagliate:</span><span class="sxs-lookup"><span data-stu-id="82bc8-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="82bc8-375">Monitorare e gestire le pipeline di Azure Data Factory con il portale di Azure e PowerShell</span><span class="sxs-lookup"><span data-stu-id="82bc8-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="82bc8-376">Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="82bc8-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="82bc8-377">Set di dati con ambito</span><span class="sxs-lookup"><span data-stu-id="82bc8-377">Scoped datasets</span></span>
<span data-ttu-id="82bc8-378">È possibile creare set di dati con ambito limitato a una pipeline usando la proprietà **datasets** .</span><span class="sxs-lookup"><span data-stu-id="82bc8-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="82bc8-379">Questi set di dati possono essere usati solo dalle attività all'interno di questa pipeline, non da quelle in altre pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="82bc8-380">L'esempio seguente definisce una pipeline con due set di dati, InputDataset-rdc e OutputDataset-rdc, da usare all'interno della pipeline.</span><span class="sxs-lookup"><span data-stu-id="82bc8-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="82bc8-381">I set di dati con ambito sono supportati solo con le pipeline monouso, in cui **pipelineMode** è impostata su **OneTime**.</span><span class="sxs-lookup"><span data-stu-id="82bc8-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="82bc8-382">Per i dettagli vedere [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="82bc8-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="82bc8-383">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82bc8-383">Next steps</span></span>
- <span data-ttu-id="82bc8-384">Per altre informazioni sulle pipeline, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="82bc8-385">Per altre informazioni sulle modalità di pianificazione ed esecuzione delle pipeline, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="82bc8-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
