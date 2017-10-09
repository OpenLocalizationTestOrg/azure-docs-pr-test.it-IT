---
title: set di dati aaaCreate nella Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come toocreate set di dati in Data Factory di Azure, con esempi che utilizzano le proprietà come offset e anchorDateTime."
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
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="db735-104">Set di dati in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="db735-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="db735-105">In questo articolo vengono descritti i set di dati, la procedura di definizione dei set in formato JSON e le modalità di utilizzo nelle pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="db735-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="db735-106">Fornisce informazioni dettagliate su ogni sezione (ad esempio, struttura, disponibilità e criteri) nella definizione di hello set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="db735-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="db735-107">Hello articolo sono inoltre disponibili esempi per l'utilizzo di hello **offset**, **anchorDateTime**, e **stile** proprietà in una definizione di set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="db735-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="db735-108">Se si tooData nuova Factory, vedere [tooAzure introduzione Data Factory](data-factory-introduction.md) per una panoramica.</span><span class="sxs-lookup"><span data-stu-id="db735-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="db735-109">Se non si dispone di familiarità con la creazione di data factory, è possibile acquisire una comprensione migliore per la lettura hello [esercitazione sulle trasformazioni dati](data-factory-build-your-first-pipeline.md) hello e [esercitazione lo spostamento dei dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="db735-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="db735-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="db735-110">Overview</span></span>
<span data-ttu-id="db735-111">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="db735-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="db735-112">Una **pipeline** è un raggruppamento logico di **attività** che insieme eseguono un compito.</span><span class="sxs-lookup"><span data-stu-id="db735-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="db735-113">attività Hello in una pipeline definire tooperform azioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="db735-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="db735-114">Ad esempio, è possibile utilizzare un copia attività toocopy di dati da un tooAzure di SQL Server locale nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="db735-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="db735-115">Quindi, è possibile utilizzare un'attività Hive che esegue uno script Hive in dati di tooprocess un cluster Azure HDInsight da dati di output tooproduce archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="db735-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="db735-116">Infine, è possibile utilizzare una seconda copia attività toocopy hello output dati tooAzure SQL Data Warehouse, in cui la business intelligence (BI) reporting soluzioni vengono compilate.</span><span class="sxs-lookup"><span data-stu-id="db735-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="db735-117">Per altre informazioni su pipeline e attività, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="db735-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="db735-118">Un'attività può non avere alcun **set di dati** di input o averne più di uno e generare uno o più set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="db735-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="db735-119">Un set di dati di input rappresenta hello l'input per un'attività nella pipeline hello e un set di dati di output rappresenta l'output di hello per attività hello.</span><span class="sxs-lookup"><span data-stu-id="db735-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="db735-120">I set di dati identificano i dati all'interno dei diversi archivi dati, come tabelle, file, cartelle e documenti.</span><span class="sxs-lookup"><span data-stu-id="db735-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="db735-121">Ad esempio, un set di dati Blob di Azure specifica contenitore blob hello e cartelle nell'archiviazione Blob da cui hello pipeline deve leggere i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="db735-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="db735-122">Prima di creare un set di dati, creare un **servizio collegato** toolink toohello data factory di archiviano i dati.</span><span class="sxs-lookup"><span data-stu-id="db735-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="db735-123">Servizi collegati sono molto simili a stringhe di connessione, che definiscono le informazioni di connessione hello necessarie per le risorse di tooexternal tooconnect Data Factory.</span><span class="sxs-lookup"><span data-stu-id="db735-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="db735-124">Set di dati di identificare i dati in archivi dati hello collegato, ad esempio tabelle SQL, file, cartelle e documenti.</span><span class="sxs-lookup"><span data-stu-id="db735-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="db735-125">Ad esempio, una risorsa di archiviazione di Azure collegati collegamenti al servizio una data factory toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="db735-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="db735-126">Un set di dati Blob di Azure rappresenta il contenitore di blob hello e la cartella di hello contenente hello input BLOB toobe elaborati.</span><span class="sxs-lookup"><span data-stu-id="db735-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="db735-127">Di seguito è riportato uno scenario di esempio.</span><span class="sxs-lookup"><span data-stu-id="db735-127">Here is a sample scenario.</span></span> <span data-ttu-id="db735-128">toocopy dati dal database SQL tooa archiviazione Blob, creare due servizi collegati: archiviazione di Azure e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="db735-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="db735-129">Quindi, creare due set di dati: set di dati Blob di Azure (che fa riferimento il servizio di archiviazione di Azure collegati toohello) e set di dati di tabelle di SQL Azure (che fa riferimento il servizio di Database SQL di Azure collegati toohello).</span><span class="sxs-lookup"><span data-stu-id="db735-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="db735-130">Hello archiviazione di Azure e Database SQL di Azure servizi collegati contengono stringhe di connessione che utilizza Data Factory in fase di esecuzione tooconnect tooyour di archiviazione di Azure e Database SQL di Azure, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="db735-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="db735-131">set di dati Blob di Azure Hello specifica contenitore blob hello e la cartella di blob che contiene i BLOB di input hello nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="db735-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="db735-132">set di dati tabella di SQL Azure Hello specifica tabella SQL hello nei dati SQL database toowhich hello toobe copiati.</span><span class="sxs-lookup"><span data-stu-id="db735-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="db735-133">Hello diagramma seguente illustra le relazioni di hello tra pipeline, attività, set di dati e il servizio collegato in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="db735-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relazione tra pipeline, attività, set di dati, i servizi collegati](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="db735-135">Set di dati JSON</span><span class="sxs-lookup"><span data-stu-id="db735-135">Dataset JSON</span></span>
<span data-ttu-id="db735-136">Un set di dati in Data Factory viene definito in formato JSON come segue:</span><span class="sxs-lookup"><span data-stu-id="db735-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="db735-137">Hello nella tabella seguente vengono descritte le proprietà in hello sopra JSON:</span><span class="sxs-lookup"><span data-stu-id="db735-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="db735-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="db735-138">Property</span></span> | <span data-ttu-id="db735-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db735-139">Description</span></span> | <span data-ttu-id="db735-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="db735-140">Required</span></span> | <span data-ttu-id="db735-141">Default</span><span class="sxs-lookup"><span data-stu-id="db735-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db735-142">name</span><span class="sxs-lookup"><span data-stu-id="db735-142">name</span></span> |<span data-ttu-id="db735-143">Nome del set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="db735-143">Name of hello dataset.</span></span> <span data-ttu-id="db735-144">Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="db735-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="db735-145">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-145">Yes</span></span> |<span data-ttu-id="db735-146">ND</span><span class="sxs-lookup"><span data-stu-id="db735-146">NA</span></span> |
| <span data-ttu-id="db735-147">type</span><span class="sxs-lookup"><span data-stu-id="db735-147">type</span></span> |<span data-ttu-id="db735-148">tipo di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="db735-148">Type of hello dataset.</span></span> <span data-ttu-id="db735-149">Specificare uno dei tipi di hello supportati da Data Factory (ad esempio: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="db735-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="db735-150">Per informazioni dettagliate, vedere [Tipo di set di dati](#Type).</span><span class="sxs-lookup"><span data-stu-id="db735-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="db735-151">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-151">Yes</span></span> |<span data-ttu-id="db735-152">ND</span><span class="sxs-lookup"><span data-stu-id="db735-152">NA</span></span> |
| <span data-ttu-id="db735-153">structure</span><span class="sxs-lookup"><span data-stu-id="db735-153">structure</span></span> |<span data-ttu-id="db735-154">Schema di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="db735-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="db735-155">Per informazioni dettagliate, vedere [Struttura del set di dati](#Structure).</span><span class="sxs-lookup"><span data-stu-id="db735-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="db735-156">No</span><span class="sxs-lookup"><span data-stu-id="db735-156">No</span></span> |<span data-ttu-id="db735-157">ND</span><span class="sxs-lookup"><span data-stu-id="db735-157">NA</span></span> |
| <span data-ttu-id="db735-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="db735-158">typeProperties</span></span> | <span data-ttu-id="db735-159">le proprietà di tipo Hello sono diverse per ogni tipo (ad esempio: Blob di Azure, tabelle di SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="db735-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="db735-160">Per informazioni dettagliate sui tipi di hello supportato e le relative proprietà, vedere [tipo Dataset](#Type).</span><span class="sxs-lookup"><span data-stu-id="db735-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="db735-161">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-161">Yes</span></span> |<span data-ttu-id="db735-162">ND</span><span class="sxs-lookup"><span data-stu-id="db735-162">NA</span></span> |
| <span data-ttu-id="db735-163">external</span><span class="sxs-lookup"><span data-stu-id="db735-163">external</span></span> | <span data-ttu-id="db735-164">Valore booleano flag toospecify se un set di dati generata in modo esplicito tramite una pipeline di factory di dati o non.</span><span class="sxs-lookup"><span data-stu-id="db735-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="db735-165">Se hello input set di dati per un'attività non viene generato dalla pipeline corrente hello, impostare questo flag tootrue.</span><span class="sxs-lookup"><span data-stu-id="db735-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="db735-166">Impostare questo flag tootrue per set di dati input hello della prima attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="db735-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="db735-167">No</span><span class="sxs-lookup"><span data-stu-id="db735-167">No</span></span> |<span data-ttu-id="db735-168">false</span><span class="sxs-lookup"><span data-stu-id="db735-168">false</span></span> |
| <span data-ttu-id="db735-169">disponibilità</span><span class="sxs-lookup"><span data-stu-id="db735-169">availability</span></span> | <span data-ttu-id="db735-170">Definisce hello finestra di elaborazione (ad esempio, oraria o giornaliera) o hello sezionamento modello per la produzione di hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="db735-171">Ogni unità di dati usata e prodotta da un'esecuzione di attività prende il nome di sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="db735-172">Se la disponibilità di hello di un set di dati di output è toodaily set (frequenza - Day, intervallo di-1), una sezione viene prodotta ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="db735-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="db735-173">Per informazioni dettagliate, vedere [Disponibilità dei set di dati](#Availability).</span><span class="sxs-lookup"><span data-stu-id="db735-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="db735-174">Per informazioni dettagliate sul set di dati hello sezionamento modello, vedere hello [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="db735-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="db735-175">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-175">Yes</span></span> |<span data-ttu-id="db735-176">ND</span><span class="sxs-lookup"><span data-stu-id="db735-176">NA</span></span> |
| <span data-ttu-id="db735-177">policy</span><span class="sxs-lookup"><span data-stu-id="db735-177">policy</span></span> |<span data-ttu-id="db735-178">Definisce i criteri di hello o condizione hello che devono soddisfare le sezioni di hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="db735-179">Per informazioni dettagliate, vedere hello [criteri Dataset](#Policy) sezione.</span><span class="sxs-lookup"><span data-stu-id="db735-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="db735-180">No</span><span class="sxs-lookup"><span data-stu-id="db735-180">No</span></span> |<span data-ttu-id="db735-181">ND</span><span class="sxs-lookup"><span data-stu-id="db735-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="db735-182">Esempio di set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-182">Dataset example</span></span>
<span data-ttu-id="db735-183">Nell'esempio seguente di hello, hello set di dati rappresenta una tabella denominata **MyTable** in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="db735-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="db735-184">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="db735-184">Note hello following points:</span></span>

* <span data-ttu-id="db735-185">**tipo** è impostato tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="db735-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="db735-186">**tableName** (tipo tooAzureSqlTable specifico) è impostata tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="db735-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="db735-187">**linkedServiceName** fa riferimento a servizio tooa collegato di tipo AzureSqlDatabase, definita nel frammento JSON seguente hello.</span><span class="sxs-lookup"><span data-stu-id="db735-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="db735-188">**frequenza di disponibilità** è impostata, tooDay e **intervallo** è impostato too1.</span><span class="sxs-lookup"><span data-stu-id="db735-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="db735-189">Ciò significa che tale sezione del set di dati hello viene prodotta ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="db735-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="db735-190">**AzureSqlLinkedService** è definito come segue:</span><span class="sxs-lookup"><span data-stu-id="db735-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="db735-191">Nel precedente frammento di codice JSON di hello:</span><span class="sxs-lookup"><span data-stu-id="db735-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="db735-192">**tipo** è impostato tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="db735-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="db735-193">**connectionString** proprietà di tipo specifica informazioni tooconnect tooa SQL database.</span><span class="sxs-lookup"><span data-stu-id="db735-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="db735-194">Come si può notare, hello servizio collegato definisce come database SQL tooa tooconnect.</span><span class="sxs-lookup"><span data-stu-id="db735-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="db735-195">set di dati Hello definisce quale tabella viene utilizzato come input e output per l'attività hello in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="db735-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="db735-196">Se non è in corso un set di dati di produzione dalla pipeline di hello, deve essere contrassegnato come **esterno**.</span><span class="sxs-lookup"><span data-stu-id="db735-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="db735-197">Questa impostazione si applica in genere tooinputs della prima attività in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="db735-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="db735-198"><a name="Type"></a> Tipo di set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="db735-199">tipo Hello del set di dati hello dipende dall'archivio dati hello che è utilizzare.</span><span class="sxs-lookup"><span data-stu-id="db735-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="db735-200">Vedere la seguente tabella per un elenco di archivi di dati supportati da Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="db735-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="db735-201">Fare clic su un toolearn archivio dati come toocreate un servizio collegato e un set di dati per tali dati archivio.</span><span class="sxs-lookup"><span data-stu-id="db735-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="db735-202">Gli archivi dati con * possono essere locali o in un'infrastruttura distribuita come servizio (IaaS) di Azure.</span><span class="sxs-lookup"><span data-stu-id="db735-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="db735-203">Questi archivi dati richiedono tooinstall [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="db735-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="db735-204">Nell'esempio hello nella sezione precedente di hello, tipo di hello del set di dati hello è impostato troppo**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="db735-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="db735-205">Analogamente, per un set di dati Blob di Azure, hello tipo di set di dati hello è impostato troppo**AzureBlob**, come illustrato nella seguente JSON hello:</span><span class="sxs-lookup"><span data-stu-id="db735-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

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

## <span data-ttu-id="db735-206"><a name="Structure"></a>Struttura del set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="db735-207">Hello **struttura** sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="db735-207">hello **structure** section is optional.</span></span> <span data-ttu-id="db735-208">Definisce schema hello di hello set di dati contenente una raccolta di nomi e i tipi di dati delle colonne.</span><span class="sxs-lookup"><span data-stu-id="db735-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="db735-209">Utilizzare hello struttura sezione tooprovide le informazioni sul tipo tooconvert utilizzati tipi e il mapping delle colonne hello origine toohello di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db735-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="db735-210">Nell'esempio seguente di hello, set di dati hello ha tre colonne: `slicetimestamp`, `projectname`, e `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="db735-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="db735-211">Sono rispettivamente di tipo String, String e Decimal.</span><span class="sxs-lookup"><span data-stu-id="db735-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="db735-212">Ogni colonna della struttura di hello contiene hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="db735-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="db735-213">Proprietà</span><span class="sxs-lookup"><span data-stu-id="db735-213">Property</span></span> | <span data-ttu-id="db735-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db735-214">Description</span></span> | <span data-ttu-id="db735-215">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="db735-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db735-216">name</span><span class="sxs-lookup"><span data-stu-id="db735-216">name</span></span> |<span data-ttu-id="db735-217">Nome della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="db735-217">Name of hello column.</span></span> |<span data-ttu-id="db735-218">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-218">Yes</span></span> |
| <span data-ttu-id="db735-219">type</span><span class="sxs-lookup"><span data-stu-id="db735-219">type</span></span> |<span data-ttu-id="db735-220">Tipo di dati della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="db735-220">Data type of hello column.</span></span>  |<span data-ttu-id="db735-221">No</span><span class="sxs-lookup"><span data-stu-id="db735-221">No</span></span> |
| <span data-ttu-id="db735-222">culture</span><span class="sxs-lookup"><span data-stu-id="db735-222">culture</span></span> |<span data-ttu-id="db735-223">. Le impostazioni cultura basate su NET toobe usato quando il tipo di hello è un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="db735-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="db735-224">valore predefinito di Hello è `en-us`.</span><span class="sxs-lookup"><span data-stu-id="db735-224">hello default is `en-us`.</span></span> |<span data-ttu-id="db735-225">No</span><span class="sxs-lookup"><span data-stu-id="db735-225">No</span></span> |
| <span data-ttu-id="db735-226">format</span><span class="sxs-lookup"><span data-stu-id="db735-226">format</span></span> |<span data-ttu-id="db735-227">Formato stringa toobe usato quando il tipo di hello è un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="db735-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="db735-228">No</span><span class="sxs-lookup"><span data-stu-id="db735-228">No</span></span> |

<span data-ttu-id="db735-229">Hello linee guida seguenti consentono di determinare quando tooinclude struttura informazioni e quali tooinclude in hello **struttura** sezione.</span><span class="sxs-lookup"><span data-stu-id="db735-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="db735-230">**Per le origini dati strutturati**, specificare sezione struttura hello solo se si desidera eseguire il mapping di colonne toosink colonne di origine e i relativi nomi sono hello non uguali.</span><span class="sxs-lookup"><span data-stu-id="db735-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="db735-231">Questo tipo di origine di dati strutturati archivia le informazioni dello schema e il tipo di dati insieme ai dati hello stesso.</span><span class="sxs-lookup"><span data-stu-id="db735-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="db735-232">Alcuni esempi di origini dati strutturate sono SQL Server, Oracle e la tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="db735-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="db735-233">Informazioni sul tipo è già disponibile per le origini dati strutturati, non è necessario includere le informazioni sul tipo quando si include una sezione di struttura hello.</span><span class="sxs-lookup"><span data-stu-id="db735-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="db735-234">**Per lo schema su origini dei dati letti (in particolare, archiviazione Blob)**, è possibile scegliere i dati toostore senza archiviare le informazioni di tipo o schema con dati hello.</span><span class="sxs-lookup"><span data-stu-id="db735-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="db735-235">Per questi tipi di origini dati, è possibile includere struttura quando si desidera toomap origine colonne toosink colonne.</span><span class="sxs-lookup"><span data-stu-id="db735-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="db735-236">Includere inoltre struttura quando hello set di dati è un input per un'attività di copia e tipi di dati del set di dati di origine devono essere convertito toonative tipi per il sink hello.</span><span class="sxs-lookup"><span data-stu-id="db735-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="db735-237">Data Factory supporta i seguenti valori per fornire informazioni sul tipo di struttura hello: **Int16, Int32, Int64, Single, Double, Decimal, Byte [], valore booleano, stringa, Guid, Datetime, Datetimeoffset e Timespan**.</span><span class="sxs-lookup"><span data-stu-id="db735-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="db735-238">Sono valori dei tipi basati su .NET e conformi a CLS (Common Language Specification).</span><span class="sxs-lookup"><span data-stu-id="db735-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="db735-239">Data Factory esegue automaticamente le conversioni di tipo quando si spostano dati da un'origine tooa archiviano dati sink.</span><span class="sxs-lookup"><span data-stu-id="db735-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="db735-240">Disponibilità dei set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-240">Dataset availability</span></span>
<span data-ttu-id="db735-241">Hello **disponibilità** sezione in un set di dati definisce l'elaborazione finestra hello (ad esempio orario, giornaliero, o settimanale) per hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="db735-242">Per altre informazioni sugli intervalli di attività, vedere [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="db735-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="db735-243">Hello seguente sezione di disponibilità specifica che hello set di dati di output è sia generate ogni ora o set di dati input hello è disponibile ogni ora:</span><span class="sxs-lookup"><span data-stu-id="db735-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="db735-244">Se la pipeline hello ha hello dopo l'ora di inizio e fine:</span><span class="sxs-lookup"><span data-stu-id="db735-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="db735-245">Hello set di dati di output viene generato all'interno della pipeline hello inizio ogni ora e di fine.</span><span class="sxs-lookup"><span data-stu-id="db735-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="db735-246">Questa pipeline genera quindi cinque sezioni di set di dati, una per ogni intervallo di attività (00:00 - 01:00, 01: 00 - 02:00, 02:00 - 03:00, 03:00 - 04:00, 04:00 - 05:00).</span><span class="sxs-lookup"><span data-stu-id="db735-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="db735-247">Hello nella tabella seguente vengono descritte le proprietà che è possibile utilizzare nella sezione di disponibilità hello:</span><span class="sxs-lookup"><span data-stu-id="db735-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="db735-248">Proprietà</span><span class="sxs-lookup"><span data-stu-id="db735-248">Property</span></span> | <span data-ttu-id="db735-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db735-249">Description</span></span> | <span data-ttu-id="db735-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="db735-250">Required</span></span> | <span data-ttu-id="db735-251">Default</span><span class="sxs-lookup"><span data-stu-id="db735-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db735-252">frequency</span><span class="sxs-lookup"><span data-stu-id="db735-252">frequency</span></span> |<span data-ttu-id="db735-253">Specifica l'unità di tempo hello per la produzione di sezione set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="db735-254"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="db735-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="db735-255">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-255">Yes</span></span> |<span data-ttu-id="db735-256">ND</span><span class="sxs-lookup"><span data-stu-id="db735-256">NA</span></span> |
| <span data-ttu-id="db735-257">interval</span><span class="sxs-lookup"><span data-stu-id="db735-257">interval</span></span> |<span data-ttu-id="db735-258">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="db735-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="db735-259">"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta.</span><span class="sxs-lookup"><span data-stu-id="db735-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="db735-260">Ad esempio, se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="db735-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="db735-261">Si noti che se si specifica **frequenza** come **minuto**, è necessario impostare hello intervallo toono inferiore a 15.</span><span class="sxs-lookup"><span data-stu-id="db735-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="db735-262">Sì</span><span class="sxs-lookup"><span data-stu-id="db735-262">Yes</span></span> |<span data-ttu-id="db735-263">ND</span><span class="sxs-lookup"><span data-stu-id="db735-263">NA</span></span> |
| <span data-ttu-id="db735-264">style</span><span class="sxs-lookup"><span data-stu-id="db735-264">style</span></span> |<span data-ttu-id="db735-265">Specifica se deve essere prodotta sezione hello hello inizio o alla fine dell'intervallo "hello".</span><span class="sxs-lookup"><span data-stu-id="db735-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="db735-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="db735-266">StartOfInterval</span></span></li><li><span data-ttu-id="db735-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="db735-267">EndOfInterval</span></span></li></ul><span data-ttu-id="db735-268">Se **frequenza** è troppo**mese**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta hello ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="db735-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="db735-269">Se **stile** è troppo**StartOfInterval**, hello sezione viene prodotta hello primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="db735-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="db735-270">Se **frequenza** è troppo**giorno**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta nell'ultima ora del giorno hello hello.</span><span class="sxs-lookup"><span data-stu-id="db735-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="db735-271">Se **frequenza** è troppo**ora**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta alla fine hello ora hello.</span><span class="sxs-lookup"><span data-stu-id="db735-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="db735-272">Ad esempio, per una sezione per hello periodo 1 PM - 2 PM, sezione di hello viene prodotta alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="db735-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="db735-273">No</span><span class="sxs-lookup"><span data-stu-id="db735-273">No</span></span> |<span data-ttu-id="db735-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="db735-274">EndOfInterval</span></span> |
| <span data-ttu-id="db735-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="db735-275">anchorDateTime</span></span> |<span data-ttu-id="db735-276">Definisce una posizione assoluta di hello in utilizzata dai limiti di intervallo di hello dell'utilità di pianificazione toocompute set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="db735-277">Si noti che se questo propoerty ha parti di date più granulari di hello specificato frequenza, hello parti più granulari verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="db735-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="db735-278">Ad esempio, se hello **intervallo** è **oraria** (frequenza: ora e intervallo: 1), hello e **anchorDateTime** contiene **minuti e secondi**, quindi hello minuti e secondi parti di **anchorDateTime** vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="db735-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="db735-279">No</span><span class="sxs-lookup"><span data-stu-id="db735-279">No</span></span> |<span data-ttu-id="db735-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="db735-280">01/01/0001</span></span> |
| <span data-ttu-id="db735-281">offset</span><span class="sxs-lookup"><span data-stu-id="db735-281">offset</span></span> |<span data-ttu-id="db735-282">Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati.</span><span class="sxs-lookup"><span data-stu-id="db735-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="db735-283">Si noti che se entrambi **anchorDateTime** e **offset** viene specificato, il risultato di hello MAIUSC hello combinato.</span><span class="sxs-lookup"><span data-stu-id="db735-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="db735-284">No</span><span class="sxs-lookup"><span data-stu-id="db735-284">No</span></span> |<span data-ttu-id="db735-285">ND</span><span class="sxs-lookup"><span data-stu-id="db735-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="db735-286">Esempio di offset</span><span class="sxs-lookup"><span data-stu-id="db735-286">offset example</span></span>
<span data-ttu-id="db735-287">Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00.00 (mezzanotte) UTC (Coordinated Universal Time).</span><span class="sxs-lookup"><span data-stu-id="db735-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="db735-288">Se si desidera hello inizio ora toobe 6: 00 UTC ora invece, impostare hello offset come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="db735-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="db735-289">Esempio di anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="db735-289">anchorDateTime example</span></span>
<span data-ttu-id="db735-290">Nell'esempio seguente di hello, hello set di dati viene prodotta una volta ogni 23 ore.</span><span class="sxs-lookup"><span data-stu-id="db735-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="db735-291">Hello prima sezione viene avviato in hello momento specificato dal **anchorDateTime**, questo valore è impostato troppo`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="db735-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="db735-292">Esempio di offset/style</span><span class="sxs-lookup"><span data-stu-id="db735-292">offset/style example</span></span>
<span data-ttu-id="db735-293">Hello seguente set di dati è mensile e viene prodotta hello 3 ° di ogni mese alle ore 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="db735-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="db735-294"><a name="Policy"></a>Criteri di set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="db735-295">Hello **criteri** sezione nella definizione di set di dati hello definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare.</span><span class="sxs-lookup"><span data-stu-id="db735-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="db735-296">Criteri di convalida</span><span class="sxs-lookup"><span data-stu-id="db735-296">Validation policies</span></span>
| <span data-ttu-id="db735-297">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="db735-297">Policy name</span></span> | <span data-ttu-id="db735-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db735-298">Description</span></span> | <span data-ttu-id="db735-299">Troppo applicato</span><span class="sxs-lookup"><span data-stu-id="db735-299">Applied too</span></span>| <span data-ttu-id="db735-300">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="db735-300">Required</span></span> | <span data-ttu-id="db735-301">Default</span><span class="sxs-lookup"><span data-stu-id="db735-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="db735-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="db735-302">minimumSizeMB</span></span> |<span data-ttu-id="db735-303">Convalida i dati di hello **archiviazione Blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="db735-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="db735-304">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="db735-304">Azure Blob storage</span></span> |<span data-ttu-id="db735-305">No</span><span class="sxs-lookup"><span data-stu-id="db735-305">No</span></span> |<span data-ttu-id="db735-306">ND</span><span class="sxs-lookup"><span data-stu-id="db735-306">NA</span></span> |
| <span data-ttu-id="db735-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="db735-307">minimumRows</span></span> |<span data-ttu-id="db735-308">Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="db735-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="db735-309">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="db735-309">Azure SQL database</span></span></li><li><span data-ttu-id="db735-310">Tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="db735-310">Azure table</span></span></li></ul> |<span data-ttu-id="db735-311">No</span><span class="sxs-lookup"><span data-stu-id="db735-311">No</span></span> |<span data-ttu-id="db735-312">ND</span><span class="sxs-lookup"><span data-stu-id="db735-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="db735-313">esempi</span><span class="sxs-lookup"><span data-stu-id="db735-313">Examples</span></span>
<span data-ttu-id="db735-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="db735-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="db735-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="db735-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="db735-316">Set di dati esterni</span><span class="sxs-lookup"><span data-stu-id="db735-316">External datasets</span></span>
<span data-ttu-id="db735-317">Set di dati esterni sono quelli che non sono state prodotte da una pipeline in esecuzione in data factory di hello hello.</span><span class="sxs-lookup"><span data-stu-id="db735-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="db735-318">Se il set di dati hello è contrassegnato come **esterno**, hello **ExternalData** criteri possono essere definiti tooinfluence hello comportamento di disponibilità di sezione hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="db735-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="db735-319">A meno che non sia generato da Data Factory, il set di dati deve essere contrassegnato come **external**.</span><span class="sxs-lookup"><span data-stu-id="db735-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="db735-320">Questa impostazione si applica in genere input toohello della prima attività in una pipeline, a meno che l'attività o il concatenamento della pipeline in uso.</span><span class="sxs-lookup"><span data-stu-id="db735-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="db735-321">Nome</span><span class="sxs-lookup"><span data-stu-id="db735-321">Name</span></span> | <span data-ttu-id="db735-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db735-322">Description</span></span> | <span data-ttu-id="db735-323">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="db735-323">Required</span></span> | <span data-ttu-id="db735-324">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="db735-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db735-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="db735-325">dataDelay</span></span> |<span data-ttu-id="db735-326">tempo di Hello hello toodelay verificare hello disponibilità di dati esterni di hello per hello assegnato sezione.</span><span class="sxs-lookup"><span data-stu-id="db735-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="db735-327">Ad esempio, è possibile ritardare un controllo orario usando questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="db735-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="db735-328">Hello impostazione si applica solo toohello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="db735-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="db735-329">Ad esempio, se è 1:00 PM subito e questo valore è 10 minuti, convalida hello inizia alle ore 1:10.</span><span class="sxs-lookup"><span data-stu-id="db735-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="db735-330">Si noti che questa impostazione non influisce sulle sezioni in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="db735-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="db735-331">Le sezioni con **Slice End Time** + **dataDelay** < **Now** vengono elaborate senza alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="db735-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="db735-332">Volte maggiore di 23:59 ore devono essere specificate tramite hello `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="db735-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="db735-333">Ad esempio, toospecify 24 ore, non utilizzare 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="db735-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="db735-334">Usare invece 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="db735-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="db735-335">Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="db735-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="db735-336">Per 1 giorno e 4 ore, specificare 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="db735-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="db735-337">No</span><span class="sxs-lookup"><span data-stu-id="db735-337">No</span></span> |<span data-ttu-id="db735-338">0</span><span class="sxs-lookup"><span data-stu-id="db735-338">0</span></span> |
| <span data-ttu-id="db735-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="db735-339">retryInterval</span></span> |<span data-ttu-id="db735-340">tempo di attesa Hello tra un tentativo successivo di errore e hello.</span><span class="sxs-lookup"><span data-stu-id="db735-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="db735-341">Questa impostazione si applica ora toopresent.</span><span class="sxs-lookup"><span data-stu-id="db735-341">This setting applies toopresent time.</span></span> <span data-ttu-id="db735-342">Se non è riuscita, provare precedente hello successivo tentativo di hello è dopo hello **retryInterval** periodo.</span><span class="sxs-lookup"><span data-stu-id="db735-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="db735-343">Se è 1:00 PM al momento, iniziamo hello primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="db735-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="db735-344">Se hello durata toocomplete hello primo controllo di convalida è 1 minuto e operazione hello non riuscita, tentativo successivo di hello è 1:00 + 1 min (durata) + 1 minuto (intervallo tra tentativi) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="db735-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="db735-345">Per le sezioni hello precedente, non si verifica alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="db735-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="db735-346">Riprova Hello si verifica immediatamente.</span><span class="sxs-lookup"><span data-stu-id="db735-346">hello retry happens immediately.</span></span> |<span data-ttu-id="db735-347">No</span><span class="sxs-lookup"><span data-stu-id="db735-347">No</span></span> |<span data-ttu-id="db735-348">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="db735-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="db735-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="db735-349">retryTimeout</span></span> |<span data-ttu-id="db735-350">timeout di Hello per ogni nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="db735-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="db735-351">Se questa proprietà è impostata too10 minuti, la convalida di hello deve essere completata entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="db735-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="db735-352">Se impiega più tempo rispetto alla convalida hello tooperform di 10 minuti, hello ripetere verifica il timeout.</span><span class="sxs-lookup"><span data-stu-id="db735-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="db735-353">Se tutti i tentativi per timeout convalida hello hello sezione è contrassegnata come **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="db735-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="db735-354">No</span><span class="sxs-lookup"><span data-stu-id="db735-354">No</span></span> |<span data-ttu-id="db735-355">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="db735-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="db735-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="db735-356">maximumRetry</span></span> |<span data-ttu-id="db735-357">Hello numero di volte in cui toocheck per la disponibilità di dati esterni hello hello.</span><span class="sxs-lookup"><span data-stu-id="db735-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="db735-358">Hello valore massimo consentito è 10.</span><span class="sxs-lookup"><span data-stu-id="db735-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="db735-359">No</span><span class="sxs-lookup"><span data-stu-id="db735-359">No</span></span> |<span data-ttu-id="db735-360">3</span><span class="sxs-lookup"><span data-stu-id="db735-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="db735-361">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="db735-361">Create datasets</span></span>
<span data-ttu-id="db735-362">È possibile creare set di dati usando uno di questi strumenti o SDK:</span><span class="sxs-lookup"><span data-stu-id="db735-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="db735-363">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="db735-363">Copy Wizard</span></span> 
- <span data-ttu-id="db735-364">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="db735-364">Azure portal</span></span>
- <span data-ttu-id="db735-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db735-365">Visual Studio</span></span>
- <span data-ttu-id="db735-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db735-366">PowerShell</span></span>
- <span data-ttu-id="db735-367">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db735-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="db735-368">API REST</span><span class="sxs-lookup"><span data-stu-id="db735-368">REST API</span></span>
- <span data-ttu-id="db735-369">API .NET</span><span class="sxs-lookup"><span data-stu-id="db735-369">.NET API</span></span>

<span data-ttu-id="db735-370">Hello seguenti esercitazioni per istruzioni dettagliate per la creazione di pipeline e set di dati utilizzando uno di questi strumenti o il SDK, vedere:</span><span class="sxs-lookup"><span data-stu-id="db735-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="db735-371">Creare una pipeline con un'attività di trasformazione dati</span><span class="sxs-lookup"><span data-stu-id="db735-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="db735-372">Creare una pipeline con un'attività di spostamento dati</span><span class="sxs-lookup"><span data-stu-id="db735-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="db735-373">Dopo una pipeline viene creata e distribuita, è possibile gestire e monitorare le pipeline utilizzando hello pannelli portali Azure o un'app di gestione e monitoraggio hello.</span><span class="sxs-lookup"><span data-stu-id="db735-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="db735-374">Hello seguenti argomenti per informazioni dettagliate, vedere:</span><span class="sxs-lookup"><span data-stu-id="db735-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="db735-375">Monitorare e gestire le pipeline di Azure Data Factory con il portale di Azure e PowerShell</span><span class="sxs-lookup"><span data-stu-id="db735-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="db735-376">Monitorare e gestire le pipeline con hello monitoraggio e gestione delle app</span><span class="sxs-lookup"><span data-stu-id="db735-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="db735-377">Set di dati con ambito</span><span class="sxs-lookup"><span data-stu-id="db735-377">Scoped datasets</span></span>
<span data-ttu-id="db735-378">È possibile creare set di dati con ambito tooa pipeline utilizzando hello **set di dati** proprietà.</span><span class="sxs-lookup"><span data-stu-id="db735-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="db735-379">Questi set di dati possono essere usati solo dalle attività all'interno di questa pipeline, non da quelle in altre pipeline.</span><span class="sxs-lookup"><span data-stu-id="db735-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="db735-380">Hello di esempio seguente definisce una pipeline con due set di dati (InputDataset rdc e OutputDataset rdc) toobe utilizzati all'interno della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="db735-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="db735-381">Set di dati con ambito sono supportati solo con le pipeline monouso (dove **pipelineMode** è troppo**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="db735-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="db735-382">Per i dettagli vedere [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="db735-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="db735-383">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db735-383">Next steps</span></span>
- <span data-ttu-id="db735-384">Per altre informazioni sulle pipeline, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="db735-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="db735-385">Per altre informazioni sulle modalità di pianificazione ed esecuzione delle pipeline, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="db735-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
