---
title: aaaScheduling e l'esecuzione con Data Factory | Documenti Microsoft
description: Informazioni sugli aspetti di pianificazione ed esecuzione del modello applicativo di Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="0fdea-103">Pianificazione ed esecuzione con Data Factory</span><span class="sxs-lookup"><span data-stu-id="0fdea-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="0fdea-104">Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di hello Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0fdea-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="0fdea-105">L'articolo presuppone la conoscenza dei concetti di base del modello applicativo di Data Factory: attività, pipeline, servizi collegati e set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="0fdea-106">Per concetti di base di Azure Data Factory, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="0fdea-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="0fdea-107">Introduzione tooData Factory</span><span class="sxs-lookup"><span data-stu-id="0fdea-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="0fdea-108">Pipeline</span><span class="sxs-lookup"><span data-stu-id="0fdea-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="0fdea-109">Set di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="0fdea-110">Ora di inizio e ora di fine della pipeline</span><span class="sxs-lookup"><span data-stu-id="0fdea-110">Start and end times of pipeline</span></span>
<span data-ttu-id="0fdea-111">Una pipeline è attiva solo tra l'ora di **inizio** e l'ora di **fine**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="0fdea-112">Non viene eseguita prima dell'ora di inizio hello o dopo l'ora di fine hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="0fdea-113">Se la pipeline di hello è sospesa, non viene eseguito indipendentemente dal relativo ora di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="0fdea-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="0fdea-114">Per toorun una pipeline, consigliabile non sospesa.</span><span class="sxs-lookup"><span data-stu-id="0fdea-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="0fdea-115">Queste impostazioni (inizio, fine, in pausa) disponibili nella definizione di pipeline hello:</span><span class="sxs-lookup"><span data-stu-id="0fdea-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="0fdea-116">Per altre informazioni su queste proprietà, vedere l'articolo [Creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="0fdea-117">Pianificare l'esecuzione di un'attività</span><span class="sxs-lookup"><span data-stu-id="0fdea-117">Specify schedule for an activity</span></span>
<span data-ttu-id="0fdea-118">Non è pipeline hello che viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="0fdea-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="0fdea-119">Si tratta di attività hello nella pipeline hello che vengono eseguite in hello contesto complessivo della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="0fdea-120">È possibile specificare una pianificazione ricorrente per un'attività tramite hello **dell'utilità di pianificazione** sezione del formato JSON dell'attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="0fdea-121">Ad esempio, è possibile pianificare un toorun attività ogni ora come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0fdea-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="0fdea-122">Come illustrato nel seguente diagramma hello, che specifica che una pianificazione per un'attività crea una serie di finestre a cascata con in hello della pipeline di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="0fdea-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="0fdea-123">Le finestre a cascata sono costituite da una serie di intervalli temporali di dimensioni fisse, contigui e non sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="0fdea-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="0fdea-124">Queste finestre logiche a cascata per un'attività vengono denominate **finestre attività**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Esempio di utilità di pianificazione delle attività](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="0fdea-126">Hello **dell'utilità di pianificazione** proprietà per un'attività è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0fdea-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="0fdea-127">Se si specifica questa proprietà, deve corrispondere a cadenza hello specificate nella definizione di hello del set di dati di output per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="0fdea-128">Set di dati di output è attualmente, quali unità hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="0fdea-129">Pertanto, è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="0fdea-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="0fdea-130">Specificare una pianificazione per un set di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="0fdea-131">Un'attività in una pipeline di Data Factory può non avere alcun **set di dati** di input o può averne più di uno e generare uno o più set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="0fdea-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="0fdea-132">Per un'attività, è possibile specificare una frequenza di hello quali hello dati di input sono disponibili o dati di output di hello viene generati utilizzando hello **disponibilità** sezione nelle definizioni di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="0fdea-133">**Frequenza** in hello **disponibilità** sezione specifica di unità di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="0fdea-134">Hello i valori consentiti per la frequenza sono: minuto, ora, giorno, settimana e mese.</span><span class="sxs-lookup"><span data-stu-id="0fdea-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="0fdea-135">Hello **intervallo** proprietà nella sezione di disponibilità hello consente di specificare un moltiplicatore di frequenza.</span><span class="sxs-lookup"><span data-stu-id="0fdea-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="0fdea-136">Ad esempio: se la frequenza di hello è impostata tooDay e l'intervallo è impostato too1 per un set di dati di output, i dati di output di hello viene prodotta ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="0fdea-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="0fdea-137">Se si specifica la frequenza di hello minuto, è consigliabile impostare hello intervallo toono inferiore a 15.</span><span class="sxs-lookup"><span data-stu-id="0fdea-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="0fdea-138">Nell'esempio seguente di hello, dati di input hello sono disponibili ogni ora e dati di output di hello viene generati ogni ora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="0fdea-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="0fdea-139">**Set di dati di input:**</span><span class="sxs-lookup"><span data-stu-id="0fdea-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="0fdea-140">**Set di dati di output**</span><span class="sxs-lookup"><span data-stu-id="0fdea-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="0fdea-141">Attualmente, **pianificazione hello unità set di dati di output**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="0fdea-142">In altre parole, pianificazione hello specificata per il set di dati di hello output è toorun usato un'attività in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="0fdea-143">Pertanto, è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="0fdea-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="0fdea-144">Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="0fdea-145">In seguito hello pipeline definizione, hello **dell'utilità di pianificazione** proprietà è pianificazione toospecify utilizzati per attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="0fdea-146">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0fdea-146">This property is optional.</span></span> <span data-ttu-id="0fdea-147">Attualmente, pianificazione hello per attività hello deve corrispondere pianificazione hello specificata per il set di dati di hello output.</span><span class="sxs-lookup"><span data-stu-id="0fdea-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="0fdea-148">In questo esempio viene eseguito ogni ora di hello attività tra hello inizio e di fine della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="0fdea-149">per windows a tre ore (8 AM - 09 AM, 09: 00:10:00 e AM 10-11 AM), dati di output di Hello viene prodotta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="0fdea-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="0fdea-150">Ogni unità di dati usata o prodotta da un'esecuzione di attività prende il nome di **sezione di dati**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="0fdea-151">Hello seguente diagramma viene illustrato un esempio di un'attività con un set di dati di input e un set di dati di output:</span><span class="sxs-lookup"><span data-stu-id="0fdea-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Utilità di pianificazione della disponibilità](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="0fdea-153">diagramma di Hello Mostra hello ogni ora per hello sezioni di dati di input e output di set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="0fdea-154">diagramma di Hello mostra tre intervalli di input che sono pronti per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="0fdea-155">attività 10: 11 AM Hello è in corso, producendo una sezione di output di hello 10 11 AM.</span><span class="sxs-lookup"><span data-stu-id="0fdea-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="0fdea-156">È possibile accedere a intervallo di tempo hello associata utilizzando variabili di intervallo corrente di hello hello set di dati JSON: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="0fdea-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="0fdea-157">Analogamente, è possibile accedere intervallo di tempo hello associata a una finestra attività utilizzando hello WindowStart e WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="0fdea-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="0fdea-158">pianificazione di Hello di un'attività deve corrispondere pianificazione hello del set di dati per l'attività hello output di hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="0fdea-159">Pertanto, hello SliceStart e SliceEnd valori sono hello stesso come valori WindowStart e WindowEnd rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="0fdea-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="0fdea-160">Per altre informazioni su queste variabili, vedere gli articoli [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="0fdea-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="0fdea-161">È possibile usare queste variabili per scopi diversi nel file JSON dell'attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="0fdea-162">Ad esempio, è possibile utilizzare tali dati tooselect di input e output set di dati che rappresenta dati della serie temporale (ad esempio: 8 AM too9 AM).</span><span class="sxs-lookup"><span data-stu-id="0fdea-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="0fdea-163">Questo esempio Usa anche **WindowStart** e **WindowEnd** tooselect dati rilevanti per un'attività Esegui e copiarlo tooa blob con hello appropriato **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="0fdea-164">Hello **folderPath** è toohave con parametri di una cartella separata per ogni ora.</span><span class="sxs-lookup"><span data-stu-id="0fdea-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="0fdea-165">In hello sopra riportato, pianificazione hello specificata per il set di dati di input e output è hello stesso (ogni ora).</span><span class="sxs-lookup"><span data-stu-id="0fdea-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="0fdea-166">Se il set di dati input hello per attività hello è disponibile una frequenza diversa, ad esempio ogni 15 minuti, attività hello che produce questo set di dati di output esegue ancora una volta all'ora come set di dati output hello quali unità hello pianificazione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="0fdea-167">Per altre informazioni, vedere [Modellare i set di dati con frequenze diverse](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="0fdea-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="0fdea-168">Disponibilità e criteri dei set di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-168">Dataset availability and policies</span></span>
<span data-ttu-id="0fdea-169">È stato illustrato l'utilizzo di hello di frequenza e l'intervallo di proprietà nella sezione di disponibilità hello della definizione di set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="0fdea-170">Esistono alcune altre proprietà che influiscono sulla pianificazione hello e l'esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="0fdea-171">Disponibilità dei set di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-171">Dataset availability</span></span> 
<span data-ttu-id="0fdea-172">Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **disponibilità** sezione:</span><span class="sxs-lookup"><span data-stu-id="0fdea-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="0fdea-173">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0fdea-173">Property</span></span> | <span data-ttu-id="0fdea-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0fdea-174">Description</span></span> | <span data-ttu-id="0fdea-175">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="0fdea-175">Required</span></span> | <span data-ttu-id="0fdea-176">Default</span><span class="sxs-lookup"><span data-stu-id="0fdea-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fdea-177">frequency</span><span class="sxs-lookup"><span data-stu-id="0fdea-177">frequency</span></span> |<span data-ttu-id="0fdea-178">Specifica l'unità di tempo hello per la produzione di sezione set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="0fdea-179"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="0fdea-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="0fdea-180">Sì</span><span class="sxs-lookup"><span data-stu-id="0fdea-180">Yes</span></span> |<span data-ttu-id="0fdea-181">ND</span><span class="sxs-lookup"><span data-stu-id="0fdea-181">NA</span></span> |
| <span data-ttu-id="0fdea-182">interval</span><span class="sxs-lookup"><span data-stu-id="0fdea-182">interval</span></span> |<span data-ttu-id="0fdea-183">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="0fdea-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="0fdea-184">"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta.</span><span class="sxs-lookup"><span data-stu-id="0fdea-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="0fdea-185">Se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="0fdea-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="0fdea-186"><b>Nota</b>: se si specifica Frequency come Minute, si consiglia di impostare hello intervallo toono inferiore a 15</span><span class="sxs-lookup"><span data-stu-id="0fdea-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="0fdea-187">Sì</span><span class="sxs-lookup"><span data-stu-id="0fdea-187">Yes</span></span> |<span data-ttu-id="0fdea-188">ND</span><span class="sxs-lookup"><span data-stu-id="0fdea-188">NA</span></span> |
| <span data-ttu-id="0fdea-189">style</span><span class="sxs-lookup"><span data-stu-id="0fdea-189">style</span></span> |<span data-ttu-id="0fdea-190">Specifica se la sezione hello deve essere prodotta all'hello inizio/fine dell'intervallo "hello".</span><span class="sxs-lookup"><span data-stu-id="0fdea-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="0fdea-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="0fdea-191">StartOfInterval</span></span></li><li><span data-ttu-id="0fdea-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0fdea-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="0fdea-193">Se Frequency è impostato tooMonth e style è impostato tooEndOfInterval, hello sezione viene prodotta hello ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="0fdea-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="0fdea-194">Se lo stile di hello è impostato tooStartOfInterval, hello sezione viene prodotta hello primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="0fdea-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="0fdea-195">Se Frequency è impostato tooDay e style è impostato tooEndOfInterval, sezione hello viene prodotta nell'ultima ora del giorno hello hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="0fdea-196">Se Frequency è impostato tooHour e style è impostato tooEndOfInterval, sezione hello viene prodotta alla fine hello ora hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="0fdea-197">Ad esempio, per una sezione per periodo 1 PM – 2 PM, sezione di hello viene prodotta alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="0fdea-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="0fdea-198">No</span><span class="sxs-lookup"><span data-stu-id="0fdea-198">No</span></span> |<span data-ttu-id="0fdea-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0fdea-199">EndOfInterval</span></span> |
| <span data-ttu-id="0fdea-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0fdea-200">anchorDateTime</span></span> |<span data-ttu-id="0fdea-201">Definisce una posizione assoluta di hello in utilizzata dai limiti di sezione dell'utilità di pianificazione toocompute set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="0fdea-202"><b>Nota</b>: se hello AnchorDateTime ha parti di date più granulari frequenza hello in hello parti più granulari verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="0fdea-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="0fdea-203">Ad esempio, se hello <b>intervallo</b> è <b>oraria</b> (frequenza: ora e intervallo: 1) e hello <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>, quindi hello <b>minuti e secondi</b> parti di hello AnchorDateTime verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="0fdea-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="0fdea-204">No</span><span class="sxs-lookup"><span data-stu-id="0fdea-204">No</span></span> |<span data-ttu-id="0fdea-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="0fdea-205">01/01/0001</span></span> |
| <span data-ttu-id="0fdea-206">offset</span><span class="sxs-lookup"><span data-stu-id="0fdea-206">offset</span></span> |<span data-ttu-id="0fdea-207">Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="0fdea-208"><b>Nota</b>: se vengono specificati sia anchorDateTime che offset, il risultato di hello è MAIUSC hello combinato.</span><span class="sxs-lookup"><span data-stu-id="0fdea-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="0fdea-209">No</span><span class="sxs-lookup"><span data-stu-id="0fdea-209">No</span></span> |<span data-ttu-id="0fdea-210">ND</span><span class="sxs-lookup"><span data-stu-id="0fdea-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="0fdea-211">Esempio di offset</span><span class="sxs-lookup"><span data-stu-id="0fdea-211">offset example</span></span>
<span data-ttu-id="0fdea-212">Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00:00, mezzanotte, ora UTC.</span><span class="sxs-lookup"><span data-stu-id="0fdea-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="0fdea-213">Se si desidera hello inizio ora toobe 6: 00 UTC ora invece, impostare hello offset come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="0fdea-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="0fdea-214">Esempio di anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0fdea-214">anchorDateTime example</span></span>
<span data-ttu-id="0fdea-215">Nell'esempio seguente di hello, hello set di dati viene prodotta una volta ogni 23 ore.</span><span class="sxs-lookup"><span data-stu-id="0fdea-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="0fdea-216">Hello prima sezione viene avviata in fase di hello specificato da anchorDateTime hello, che è stato impostato troppo`2017-04-19T08:00:00` (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="0fdea-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="0fdea-217">Esempio di offset/style</span><span class="sxs-lookup"><span data-stu-id="0fdea-217">offset/style Example</span></span>
<span data-ttu-id="0fdea-218">è un set di dati mensili Hello seguente set di dati e viene prodotta 3 ° di ogni mese alle ore 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="0fdea-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="0fdea-219">Criteri di set di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-219">Dataset policy</span></span>
<span data-ttu-id="0fdea-220">Un set di dati è stato definito un criterio di convalida che specifica come dati hello generati dall'esecuzione di una sezione possono essere convalidati prima che sia pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="0fdea-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="0fdea-221">In questi casi, al termine dell'esecuzione, sezione hello hello output sezione stato viene modificato troppo**in attesa** con uno stato secondario di **convalida**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="0fdea-222">Una volta convalidate sezioni hello, lo stato della sezione hello modificato anche**pronto**.</span><span class="sxs-lookup"><span data-stu-id="0fdea-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="0fdea-223">Se una sezione di dati è stato prodotto ma non ha superato la convalida di hello, esecuzioni di attività per sezioni downstream che dipendono da questa sezione non vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="0fdea-224">[Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) copre hello vari stati di sezioni di dati in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0fdea-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="0fdea-225">Hello **criteri** sezione nella definizione di set di dati definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare.</span><span class="sxs-lookup"><span data-stu-id="0fdea-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="0fdea-226">Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **criteri** sezione:</span><span class="sxs-lookup"><span data-stu-id="0fdea-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="0fdea-227">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="0fdea-227">Policy Name</span></span> | <span data-ttu-id="0fdea-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0fdea-228">Description</span></span> | <span data-ttu-id="0fdea-229">Troppo applicato</span><span class="sxs-lookup"><span data-stu-id="0fdea-229">Applied too</span></span>| <span data-ttu-id="0fdea-230">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="0fdea-230">Required</span></span> | <span data-ttu-id="0fdea-231">Default</span><span class="sxs-lookup"><span data-stu-id="0fdea-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0fdea-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="0fdea-232">minimumSizeMB</span></span> | <span data-ttu-id="0fdea-233">Convalida i dati di hello un **blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="0fdea-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="0fdea-234">BLOB Azure</span><span class="sxs-lookup"><span data-stu-id="0fdea-234">Azure Blob</span></span> |<span data-ttu-id="0fdea-235">No</span><span class="sxs-lookup"><span data-stu-id="0fdea-235">No</span></span> |<span data-ttu-id="0fdea-236">ND</span><span class="sxs-lookup"><span data-stu-id="0fdea-236">NA</span></span> |
| <span data-ttu-id="0fdea-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="0fdea-237">minimumRows</span></span> | <span data-ttu-id="0fdea-238">Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="0fdea-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="0fdea-239">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="0fdea-239">Azure SQL Database</span></span></li><li><span data-ttu-id="0fdea-240">tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="0fdea-240">Azure Table</span></span></li></ul> |<span data-ttu-id="0fdea-241">No</span><span class="sxs-lookup"><span data-stu-id="0fdea-241">No</span></span> |<span data-ttu-id="0fdea-242">ND</span><span class="sxs-lookup"><span data-stu-id="0fdea-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="0fdea-243">esempi</span><span class="sxs-lookup"><span data-stu-id="0fdea-243">Examples</span></span>
<span data-ttu-id="0fdea-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="0fdea-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="0fdea-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="0fdea-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="0fdea-246">Per altre informazioni sulle proprietà e gli esempi precedenti, vedere l'articolo [Creare i set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="0fdea-247">Criteri di attività</span><span class="sxs-lookup"><span data-stu-id="0fdea-247">Activity policies</span></span>
<span data-ttu-id="0fdea-248">Criteri influiscono sul comportamento di hello in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione hello di una tabella.</span><span class="sxs-lookup"><span data-stu-id="0fdea-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="0fdea-249">Hello nella tabella seguente fornisce dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="0fdea-250">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0fdea-250">Property</span></span> | <span data-ttu-id="0fdea-251">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="0fdea-251">Permitted values</span></span> | <span data-ttu-id="0fdea-252">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="0fdea-252">Default Value</span></span> | <span data-ttu-id="0fdea-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0fdea-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fdea-254">Concorrenza</span><span class="sxs-lookup"><span data-stu-id="0fdea-254">concurrency</span></span> |<span data-ttu-id="0fdea-255">Integer </span><span class="sxs-lookup"><span data-stu-id="0fdea-255">Integer</span></span> <br/><br/><span data-ttu-id="0fdea-256">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="0fdea-256">Max value: 10</span></span> |<span data-ttu-id="0fdea-257">1</span><span class="sxs-lookup"><span data-stu-id="0fdea-257">1</span></span> |<span data-ttu-id="0fdea-258">Numero di esecuzioni simultanee dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="0fdea-259">Determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="0fdea-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="0fdea-260">Ad esempio, se un'attività deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="0fdea-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="0fdea-261">executionPriorityOrder</span></span> |<span data-ttu-id="0fdea-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="0fdea-262">NewestFirst</span></span><br/><br/><span data-ttu-id="0fdea-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0fdea-263">OldestFirst</span></span> |<span data-ttu-id="0fdea-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0fdea-264">OldestFirst</span></span> |<span data-ttu-id="0fdea-265">Determina hello ordinamento delle sezioni di dati che vengono elaborate.</span><span class="sxs-lookup"><span data-stu-id="0fdea-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="0fdea-266">Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="0fdea-267">Se si imposta executionPriorityOrder di hello toobe NewestFirst, slice hello 17: 00 viene elaborata per prima.</span><span class="sxs-lookup"><span data-stu-id="0fdea-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="0fdea-268">Allo stesso modo se si imposta executionPriorityORder di hello toobe OldestFIrst, viene elaborato sezione hello 4 ore.</span><span class="sxs-lookup"><span data-stu-id="0fdea-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="0fdea-269">retry</span><span class="sxs-lookup"><span data-stu-id="0fdea-269">retry</span></span> |<span data-ttu-id="0fdea-270">Integer </span><span class="sxs-lookup"><span data-stu-id="0fdea-270">Integer</span></span><br/><br/><span data-ttu-id="0fdea-271">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="0fdea-271">Max value can be 10</span></span> |<span data-ttu-id="0fdea-272">0</span><span class="sxs-lookup"><span data-stu-id="0fdea-272">0</span></span> |<span data-ttu-id="0fdea-273">Numero di tentativi prima dell'elaborazione dei dati di hello per sezione hello è contrassegnato come errore.</span><span class="sxs-lookup"><span data-stu-id="0fdea-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="0fdea-274">Esecuzione di attività per una sezione di dati viene ripetuta backup toohello specificato numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="0fdea-275">Riprova Hello viene eseguito appena possibile dopo l'errore hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="0fdea-276">timeout</span><span class="sxs-lookup"><span data-stu-id="0fdea-276">timeout</span></span> |<span data-ttu-id="0fdea-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0fdea-277">TimeSpan</span></span> |<span data-ttu-id="0fdea-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0fdea-278">00:00:00</span></span> |<span data-ttu-id="0fdea-279">Timeout per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-279">Timeout for hello activity.</span></span> <span data-ttu-id="0fdea-280">Esempio: 00:10:00 (implica un timeout di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="0fdea-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="0fdea-281">Se un valore viene omesso o è 0, hello timeout è infinito.</span><span class="sxs-lookup"><span data-stu-id="0fdea-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="0fdea-282">Se il tempo di elaborazione di dati hello in una sezione supera il valore di timeout di hello, viene annullata e sistema hello tenta l'elaborazione di hello tooretry.</span><span class="sxs-lookup"><span data-stu-id="0fdea-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="0fdea-283">numero di tentativi di Hello dipende dalla proprietà retry hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="0fdea-284">Quando si verifica il timeout, hello stato tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="0fdea-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="0fdea-285">delay</span><span class="sxs-lookup"><span data-stu-id="0fdea-285">delay</span></span> |<span data-ttu-id="0fdea-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0fdea-286">TimeSpan</span></span> |<span data-ttu-id="0fdea-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0fdea-287">00:00:00</span></span> |<span data-ttu-id="0fdea-288">Specificare il ritardo di hello prima dell'elaborazione di dati di hello sezione inizia.</span><span class="sxs-lookup"><span data-stu-id="0fdea-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="0fdea-289">esecuzione di Hello dell'attività per una sezione di dati viene avviata dopo hello ritardo passato hello previsto tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="0fdea-290">Esempio: 00:10:00 (implica un ritardo di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="0fdea-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="0fdea-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="0fdea-291">longRetry</span></span> |<span data-ttu-id="0fdea-292">Integer </span><span class="sxs-lookup"><span data-stu-id="0fdea-292">Integer</span></span><br/><br/><span data-ttu-id="0fdea-293">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="0fdea-293">Max value: 10</span></span> |<span data-ttu-id="0fdea-294">1</span><span class="sxs-lookup"><span data-stu-id="0fdea-294">1</span></span> |<span data-ttu-id="0fdea-295">numero di Hello di long tentativi prima dell'esecuzione della sezione hello è non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="0fdea-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="0fdea-296">I tentativi longRetry sono distanziati da longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0fdea-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="0fdea-297">Pertanto, se è necessario toospecify un intervallo tra tentativi, usare quindi longRetry.</span><span class="sxs-lookup"><span data-stu-id="0fdea-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="0fdea-298">Se vengono specificati Retry e longRetry, ogni tentativo longRetry include nuovi tentativi e numero massimo di tentativi di hello è Riprova * longRetry.</span><span class="sxs-lookup"><span data-stu-id="0fdea-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="0fdea-299">Ad esempio, se si dispone delle seguenti impostazioni in criteri attività hello hello:</span><span class="sxs-lookup"><span data-stu-id="0fdea-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="0fdea-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="0fdea-300">Retry: 3</span></span><br/><span data-ttu-id="0fdea-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="0fdea-301">longRetry: 2</span></span><br/><span data-ttu-id="0fdea-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="0fdea-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="0fdea-303">Si supponga che sia presente solo una sezione tooexecute (lo stato è in attesa) e l'esecuzione dell'attività hello ha esito negativo di ogni volta.</span><span class="sxs-lookup"><span data-stu-id="0fdea-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="0fdea-304">All’inizio vi saranno tre tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="0fdea-305">Dopo ogni tentativo, lo stato della sezione hello sarà Retry.</span><span class="sxs-lookup"><span data-stu-id="0fdea-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="0fdea-306">Dopo aver innanzitutto 3 tentativi di failover, lo stato della sezione hello sarebbe LongRetry.</span><span class="sxs-lookup"><span data-stu-id="0fdea-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="0fdea-307">Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="0fdea-308">Successivamente, lo stato della sezione hello sarà Failed e non più necessario tentativi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="0fdea-309">Quindi, sono stati eseguiti 6 tentativi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="0fdea-310">Se qualsiasi esecuzione ha esito positivo, lo stato della sezione hello sarà Ready e non più tentativi.</span><span class="sxs-lookup"><span data-stu-id="0fdea-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="0fdea-311">longRetry possono essere utilizzati in situazioni in cui dipendenti dati arrivano a volte non deterministica o hello ambiente generale non è affidabile in cui l'elaborazione dei dati si verifica.</span><span class="sxs-lookup"><span data-stu-id="0fdea-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="0fdea-312">In questi casi, potrebbe non aiutare eseguire tentativi uno dopo l'altro e in questo modo, dopo un intervallo di risultati in fase di hello desiderato output.</span><span class="sxs-lookup"><span data-stu-id="0fdea-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="0fdea-313">Attenzione: non impostare valori elevati per longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0fdea-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="0fdea-314">In genere, valori più elevati comportano altri problemi sistemici.</span><span class="sxs-lookup"><span data-stu-id="0fdea-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="0fdea-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="0fdea-315">longRetryInterval</span></span> |<span data-ttu-id="0fdea-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0fdea-316">TimeSpan</span></span> |<span data-ttu-id="0fdea-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0fdea-317">00:00:00</span></span> |<span data-ttu-id="0fdea-318">ritardo Hello tra nuovi tentativi lunghi</span><span class="sxs-lookup"><span data-stu-id="0fdea-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="0fdea-319">Per altre informazioni, vedere l'articolo [Pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="0fdea-320">Elaborazione parallela delle sezioni di dati</span><span class="sxs-lookup"><span data-stu-id="0fdea-320">Parallel processing of data slices</span></span>
<span data-ttu-id="0fdea-321">È possibile impostare la data di inizio hello per pipeline hello in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="0fdea-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="0fdea-322">Quando si esegue questa operazione, Data Factory Calcola (riempimenti indietro) tutte le sezioni di dati in hello ultimi automaticamente e inizia l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="0fdea-323">Ad esempio: se si crea una pipeline con data di inizio 2017-04-01 e hello data corrente è 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="0fdea-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="0fdea-324">Se l'output ritmo hello di hello set di dati è ogni giorno, Data Factory avvia l'elaborazione di tutte le sezioni di hello da 2017-04-01 too2017-04-09 immediatamente perché hello data di inizio è hello precedente.</span><span class="sxs-lookup"><span data-stu-id="0fdea-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="0fdea-325">Hello sezione da 2017-04-10 non viene elaborata ancora perché il valore di hello della proprietà di stile nella sezione di disponibilità hello EndOfInterval per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0fdea-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="0fdea-326">Hello sezione meno recente viene elaborato per primo come valore predefinito di hello valore executionPriorityOrder è OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="0fdea-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="0fdea-327">Per una descrizione della proprietà di stile hello, vedere [disponibilità dataset](#dataset-availability) sezione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="0fdea-328">Per una descrizione della sezione executionPriorityOrder hello, vedere hello [criteri attività](#activity-policies) sezione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="0fdea-329">È possibile configurare toobe sezioni di dati riempito back elaborati in parallelo da hello impostazione **concorrenza** proprietà hello **criteri** sezione del formato JSON dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="0fdea-330">Questa proprietà determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="0fdea-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="0fdea-331">il valore predefinito Hello per la proprietà di concorrenza hello è 1.</span><span class="sxs-lookup"><span data-stu-id="0fdea-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="0fdea-332">Pertanto, per impostazione predefinita viene elaborata una sola sezione alla volta.</span><span class="sxs-lookup"><span data-stu-id="0fdea-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="0fdea-333">valore massimo Hello è 10.</span><span class="sxs-lookup"><span data-stu-id="0fdea-333">hello maximum value is 10.</span></span> <span data-ttu-id="0fdea-334">Quando una pipeline deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="0fdea-335">Nuova esecuzione di una sezione di dati non riuscita</span><span class="sxs-lookup"><span data-stu-id="0fdea-335">Rerun a failed data slice</span></span>
<span data-ttu-id="0fdea-336">Quando si verifica un errore durante l'elaborazione di una sezione di dati, è possibile scoprire perché non è riuscita l'elaborazione di hello di una sezione utilizzando pannelli portali Azure o i Monitor e gestire App.</span><span class="sxs-lookup"><span data-stu-id="0fdea-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="0fdea-337">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline con i pannelli del portale di Azure](data-factory-monitor-manage-pipelines.md) o [App di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="0fdea-338">Prendere in considerazione hello seguente esempio, due attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="0fdea-339">Activity1 e Activity 2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="0fdea-340">Activity1 utilizza una sezione di Dataset1 e produce una sezione del set di dati 2, che viene utilizzata come input dal Activity2 tooproduce una sezione di hello set di dati finale.</span><span class="sxs-lookup"><span data-stu-id="0fdea-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Sezione non riuscita](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="0fdea-342">Hello diagramma viene mostrato che da tre sezioni di recente, si è verificato una sezione di 9 10 AM errore produzione hello per Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="0fdea-343">Data Factory rileva automaticamente le dipendenze per set di dati serie hello ora.</span><span class="sxs-lookup"><span data-stu-id="0fdea-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="0fdea-344">Di conseguenza, non viene avviato per intervallo di hello AM 9-10 a valle di esecuzione dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="0fdea-345">Strumenti di gestione e monitoraggio di Factory dati consentono di organizzare toodrill in log di diagnostica hello per la radice hello hello sezione tooeasily trova causare per problema hello e risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="0fdea-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="0fdea-346">Dopo avere risolto il problema di hello, è possibile avviare facilmente attività hello eseguire tooproduce hello sezione.</span><span class="sxs-lookup"><span data-stu-id="0fdea-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="0fdea-347">Per ulteriori informazioni su come toorerun e comprendere le transizioni di stato per le sezioni di dati, vedere [monitoraggio e gestione delle pipeline utilizzando pannelli portali Azure](data-factory-monitor-manage-pipelines.md) o [monitoraggio e gestione di app](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="0fdea-348">Dopo che si esegue nuovamente hello 9 10 AM sezionare per **Dataset2**, Data Factory avvia hello eseguita per sezione di hello AM 9 10 dipendenti hello set di dati finale.</span><span class="sxs-lookup"><span data-stu-id="0fdea-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="0fdea-350">Attività multiple in una pipeline</span><span class="sxs-lookup"><span data-stu-id="0fdea-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="0fdea-351">È possibile avere più di un'attività in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="0fdea-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="0fdea-352">Se si dispone di più attività in una pipeline e output di hello di un'attività non è un input di un'altra attività, le attività di hello possono essere eseguite in parallelo se gli intervalli di dati di input per le attività di hello pronti.</span><span class="sxs-lookup"><span data-stu-id="0fdea-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="0fdea-353">È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="0fdea-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="0fdea-354">è possibile l'attività di Hello in hello stessa pipeline o in una pipeline diverse.</span><span class="sxs-lookup"><span data-stu-id="0fdea-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="0fdea-355">seconda attività Hello viene eseguita solo quando hello prima uno completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="0fdea-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="0fdea-356">Si consideri ad esempio hello caso in cui una pipeline ha due attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fdea-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="0fdea-357">L'attività A1, che richiede il set di dati di input esterno D1 e produce il set di dati di output D2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="0fdea-358">L'attività A2, che richiede l'input del set di dati D2 e produce il set di dati di output D3.</span><span class="sxs-lookup"><span data-stu-id="0fdea-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="0fdea-359">In questo scenario, l'attività A1 e A2 sono in hello stessa pipeline.</span><span class="sxs-lookup"><span data-stu-id="0fdea-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="0fdea-360">attività Hello che a1 viene eseguito quando sono disponibili dati esterni hello e frequenza disponibilità hello pianificata viene raggiunto.</span><span class="sxs-lookup"><span data-stu-id="0fdea-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="0fdea-361">Hello attività A2 viene eseguito quando hello intervalli pianificati da D2 diventano disponibili e hello frequenza disponibilità pianificata viene raggiunto.</span><span class="sxs-lookup"><span data-stu-id="0fdea-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="0fdea-362">Se si verifica un errore in uno degli intervalli di hello nel set di dati D2, A2 non viene eseguito per tale sezione finché diventa disponibile.</span><span class="sxs-lookup"><span data-stu-id="0fdea-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="0fdea-363">Hello vista diagramma con entrambe le attività in hello stessa pipeline avrà un aspetto analogo hello seguente diagramma:</span><span class="sxs-lookup"><span data-stu-id="0fdea-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Concatenamento di attività in hello stessa pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="0fdea-365">Come accennato in precedenza, potrebbe essere attività hello nella pipeline diverse.</span><span class="sxs-lookup"><span data-stu-id="0fdea-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="0fdea-366">In tale scenario, vista diagramma hello sarebbe simile hello seguente diagramma:</span><span class="sxs-lookup"><span data-stu-id="0fdea-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Concatenamento di attività in due pipeline](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="0fdea-368">Vedere hello [copiare in sequenza](#copy-sequentially) sezione Appendice hello per un esempio.</span><span class="sxs-lookup"><span data-stu-id="0fdea-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="0fdea-369">Modellare i set di dati con frequenze diverse</span><span class="sxs-lookup"><span data-stu-id="0fdea-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="0fdea-370">Negli esempi di hello, le frequenze di hello per input e output set di dati e hello attività periodi pianificati sono stati hello stesso.</span><span class="sxs-lookup"><span data-stu-id="0fdea-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="0fdea-371">Alcuni scenari richiedono l'output di tooproduce hello possibilità a una frequenza diversa da frequenze hello di uno o più input.</span><span class="sxs-lookup"><span data-stu-id="0fdea-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="0fdea-372">Data Factory supporta la modellazione di questi scenari.</span><span class="sxs-lookup"><span data-stu-id="0fdea-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="0fdea-373">Esempio 1: Generazione di un report di output giornaliero per i dati di input, disponibile ogni ora</span><span class="sxs-lookup"><span data-stu-id="0fdea-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="0fdea-374">Si consideri uno scenario in cui i dati delle misurazioni di input dei sensori sono disponibili ogni ora nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fdea-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="0fdea-375">Si desidera tooproduce un report giornaliero di aggregazione con statistiche, ad esempio Media, massimo e minimo per il giorno hello con [attività hive di Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0fdea-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="0fdea-376">Ecco come modellare questo scenario con Data Factory:</span><span class="sxs-lookup"><span data-stu-id="0fdea-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="0fdea-377">**Set di dati di input**</span><span class="sxs-lookup"><span data-stu-id="0fdea-377">**Input dataset**</span></span>

<span data-ttu-id="0fdea-378">Hello input ogni ora vengono eliminati i file nella cartella hello hello giorno specificato.</span><span class="sxs-lookup"><span data-stu-id="0fdea-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="0fdea-379">Il valore di disponibilità per l'input è impostato su **Hour** (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0fdea-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="0fdea-380">**Set di dati di output**</span><span class="sxs-lookup"><span data-stu-id="0fdea-380">**Output dataset**</span></span>

<span data-ttu-id="0fdea-381">Viene creato ogni giorno di un file di output nella cartella hello del giorno.</span><span class="sxs-lookup"><span data-stu-id="0fdea-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="0fdea-382">Il valore di disponibilità per l'output è impostato su **Day** (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0fdea-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0fdea-383">**Attività: attività Hive in una pipeline**</span><span class="sxs-lookup"><span data-stu-id="0fdea-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="0fdea-384">script hive Hello riceve hello appropriato *DateTime* informazioni come parametri che utilizzano hello **WindowStart** variabile, come illustrato nel seguente frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="0fdea-385">script hive Hello utilizza questi dati di hello tooload variabile dalla cartella corretta hello per giorno hello ed eseguire l'output di hello aggregazione toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="0fdea-386">Hello diagramma seguente illustra uno scenario di hello da un punto di vista di dipendenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Dipendenza dei dati](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="0fdea-388">sezione di output di Hello per ogni giorno dipende da 24 orarie sezioni da un set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0fdea-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="0fdea-389">Data Factory calcola queste dipendenze automaticamente, immaginando hello porzioni di dati di input che rientrano in hello stesso periodo di tempo come hello toobe sezione output generato.</span><span class="sxs-lookup"><span data-stu-id="0fdea-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="0fdea-390">Se una delle sezioni di input hello 24 non è disponibile, Data Factory attende hello sezione input toobe pronto prima di avviare l'esecuzione dell'attività giornaliera hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="0fdea-391">Esempio 2: Definizione di una dipendenza con espressioni e funzioni di Data Factory</span><span class="sxs-lookup"><span data-stu-id="0fdea-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="0fdea-392">Si consideri ora un altro scenario</span><span class="sxs-lookup"><span data-stu-id="0fdea-392">Let’s consider another scenario.</span></span> <span data-ttu-id="0fdea-393">Si supponga di avere un'attività Hive che elabora i due set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0fdea-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="0fdea-394">Uno di questi dispone di nuovi dati ogni giorno, mentre l'altro li riceve ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="0fdea-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="0fdea-395">Si supponga che si desiderava toodo un join tra due input hello e produrre un output di ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="0fdea-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="0fdea-396">un approccio di Hello in cui Data Factory automaticamente fascicolazione input di destra hello seziona tooprocess allineando output toohello periodo tempo della sezione di dati non funziona.</span><span class="sxs-lookup"><span data-stu-id="0fdea-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="0fdea-397">È necessario specificare che per ogni esecuzione dell'attività, hello Data Factory deve usare la sezione di dati della settimana scorsa per hello settimanale input set di dati.</span><span class="sxs-lookup"><span data-stu-id="0fdea-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="0fdea-398">Si utilizzano funzioni di Data Factory di Azure, come illustrato nel seguente frammento di codice tooimplement hello questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="0fdea-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="0fdea-399">**Input1: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="0fdea-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="0fdea-400">Hello primo input del blob di Azure hello viene aggiornata ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="0fdea-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0fdea-401">**Input2: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="0fdea-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="0fdea-402">Input2 è hello blob di Azure viene aggiornato settimanalmente.</span><span class="sxs-lookup"><span data-stu-id="0fdea-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="0fdea-403">**Output: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="0fdea-403">**Output: Azure blob**</span></span>

<span data-ttu-id="0fdea-404">Ogni giorno viene creato un file di output nella cartella hello per giorno hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="0fdea-405">Disponibilità di output è troppo**giorno** (frequenza: Day, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="0fdea-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0fdea-406">**Attività: attività Hive in una pipeline**</span><span class="sxs-lookup"><span data-stu-id="0fdea-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="0fdea-407">attività hive Hello accetta hello due input e produce una sezione di output ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="0fdea-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="0fdea-408">È possibile specificare toodepend sezione output di ogni giorno in hello porzione di input della settimana precedente per l'input settimanale, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0fdea-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="0fdea-409">Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="0fdea-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="0fdea-410">Appendice</span><span class="sxs-lookup"><span data-stu-id="0fdea-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="0fdea-411">Esempio: copiare in sequenza</span><span class="sxs-lookup"><span data-stu-id="0fdea-411">Example: copy sequentially</span></span>
<span data-ttu-id="0fdea-412">È possibile toorun più operazioni di copia uno dopo l'altro in modo sequenziale o ordinato.</span><span class="sxs-lookup"><span data-stu-id="0fdea-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="0fdea-413">Ad esempio, potrebbe essere due copia le attività di input in una pipeline (CopyActivity1 e CopyActivity2) con hello seguente dati output set di dati:</span><span class="sxs-lookup"><span data-stu-id="0fdea-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="0fdea-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="0fdea-414">CopyActivity1</span></span>

<span data-ttu-id="0fdea-415">Input: Dataset.</span><span class="sxs-lookup"><span data-stu-id="0fdea-415">Input: Dataset.</span></span> <span data-ttu-id="0fdea-416">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-416">Output: Dataset2.</span></span>

<span data-ttu-id="0fdea-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="0fdea-417">CopyActivity2</span></span>

<span data-ttu-id="0fdea-418">Input: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-418">Input: Dataset2.</span></span>  <span data-ttu-id="0fdea-419">Output: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="0fdea-419">Output: Dataset3.</span></span>

<span data-ttu-id="0fdea-420">CopyActivity2 viene eseguito solo se è stata eseguita correttamente hello CopyActivity1 e Dataset2 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="0fdea-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="0fdea-421">Di seguito è riportata la pipeline di esempio hello JSON:</span><span class="sxs-lookup"><span data-stu-id="0fdea-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="0fdea-422">Si noti che nell'esempio hello, il set di dati di hello output di hello prima attività di copia (Dataset2) è specificato come input per la seconda attività hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="0fdea-423">Pertanto, hello seconda attività viene eseguita solo quando il set di dati di hello output dalla prima attività hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="0fdea-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="0fdea-424">Nell'esempio hello CopyActivity2 può avere un input diverso, ad esempio Dataset3, ma è specificare Dataset2 come un input tooCopyActivity2, in modo attività hello non viene eseguito fino al completamento CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="0fdea-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="0fdea-425">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0fdea-425">For example:</span></span>

<span data-ttu-id="0fdea-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="0fdea-426">CopyActivity1</span></span>

<span data-ttu-id="0fdea-427">Input: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="0fdea-427">Input: Dataset1.</span></span> <span data-ttu-id="0fdea-428">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-428">Output: Dataset2.</span></span>

<span data-ttu-id="0fdea-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="0fdea-429">CopyActivity2</span></span>

<span data-ttu-id="0fdea-430">Input: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="0fdea-431">Output: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="0fdea-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="0fdea-432">Si noti che nell'esempio hello, due set di dati di input specificati per attività di copia secondo hello.</span><span class="sxs-lookup"><span data-stu-id="0fdea-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="0fdea-433">Quando vengono specificate più input, viene utilizzato solo hello primo input set di dati per la copia dei dati, ma altri set di dati vengono utilizzati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0fdea-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="0fdea-434">CopyActivity2 inizi solo dopo hello seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="0fdea-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="0fdea-435">L’esecuzione di CopyActivity1 è riuscita e Dataset2 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="0fdea-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="0fdea-436">Questo set di dati non viene utilizzato quando si copiano dati tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="0fdea-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="0fdea-437">La sua funzione è semplicemente quella di pianificare la dipendenza per CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="0fdea-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="0fdea-438">Dataset3 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="0fdea-438">Dataset3 is available.</span></span> <span data-ttu-id="0fdea-439">Questo set di dati rappresenta dati hello destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="0fdea-439">This dataset represents hello data that is copied toohello destination.</span></span> 
