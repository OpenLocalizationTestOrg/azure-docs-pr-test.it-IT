---
title: Pianificazione ed esecuzione con Data Factory | Documentazione Microsoft
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="e1ca6-103">Pianificazione ed esecuzione con Data Factory</span><span class="sxs-lookup"><span data-stu-id="e1ca6-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="e1ca6-104">Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="e1ca6-105">L'articolo presuppone la conoscenza dei concetti di base del modello applicativo di Data Factory: attività, pipeline, servizi collegati e set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="e1ca6-106">Per i concetti di base di Data Factory di Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="e1ca6-107">Introduzione al servizio Data factory</span><span class="sxs-lookup"><span data-stu-id="e1ca6-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="e1ca6-108">Pipeline</span><span class="sxs-lookup"><span data-stu-id="e1ca6-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="e1ca6-109">Set di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="e1ca6-110">Ora di inizio e ora di fine della pipeline</span><span class="sxs-lookup"><span data-stu-id="e1ca6-110">Start and end times of pipeline</span></span>
<span data-ttu-id="e1ca6-111">Una pipeline è attiva solo tra l'ora di **inizio** e l'ora di **fine**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="e1ca6-112">Non viene eseguita prima dell'ora di inizio o dopo l'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="e1ca6-113">Se messa in pausa, la pipeline non viene eseguita, indipendentemente dall'ora di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="e1ca6-114">Per essere eseguita, una pipeline non deve essere in pausa.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="e1ca6-115">Queste impostazioni (inizio, fine, in pausa) sono disponibili nella definizione di pipeline:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="e1ca6-116">Per altre informazioni su queste proprietà, vedere l'articolo [Creare pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="e1ca6-117">Pianificare l'esecuzione di un'attività</span><span class="sxs-lookup"><span data-stu-id="e1ca6-117">Specify schedule for an activity</span></span>
<span data-ttu-id="e1ca6-118">Non è la pipeline a essere eseguita,</span><span class="sxs-lookup"><span data-stu-id="e1ca6-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="e1ca6-119">ma sono le attività della pipeline a essere eseguite nel contesto generale della pipeline.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="e1ca6-120">La sezione **Utilità di pianificazione** del file JSON dell'attività consente di specificare una pianificazione ricorrente per l'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="e1ca6-121">Ad esempio, è possibile pianificare l'attività perché venga eseguita a cadenza oraria, come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="e1ca6-122">Come illustrato nel diagramma seguente, pianificando un'attività si crea una serie di finestre a cascata con l'ora di inizio e di fine della pipeline.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="e1ca6-123">Le finestre a cascata sono costituite da una serie di intervalli temporali di dimensioni fisse, contigui e non sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="e1ca6-124">Queste finestre logiche a cascata per un'attività vengono denominate **finestre attività**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Esempio di utilità di pianificazione delle attività](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="e1ca6-126">La proprietà **scheduler** per un'attività è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="e1ca6-127">Se specificata, questa proprietà deve corrispondere alla cadenza indicata nella definizione del set di dati di output per l'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="e1ca6-128">Attualmente, è il set di dati di output a determinare la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="e1ca6-129">Pertanto, anche se l'attività non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="e1ca6-130">Specificare una pianificazione per un set di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="e1ca6-131">Un'attività in una pipeline di Data Factory può non avere alcun **set di dati** di input o può averne più di uno e generare uno o più set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="e1ca6-132">Per un'attività è possibile specificare la cadenza con cui sono resi disponibili i dati di input o sono generati i dati di output usando la sezione **availability** nelle definizioni dei set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="e1ca6-133">La proprietà **frequency** nella sezione **availability** specifica l'unità di tempo.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="e1ca6-134">I valori consentiti per la frequenza sono: Minute, Hour, Day, Week, e Month (minuto, ora, giorno, settimana e mese).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="e1ca6-135">La proprietà **interval** nella sezione availability consente di specificare un moltiplicatore di frequenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="e1ca6-136">Ad esempio: se la frequenza è impostata su Day e interval è impostato su 1 per un set di dati di output, questi saranno prodotti con cadenza giornaliera.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="e1ca6-137">Se si specifica frequency come Minute, è consigliabile impostare interval su un valore non inferiore a 15.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="e1ca6-138">Nell'esempio seguente, i dati di input sono disponibili ogni ora e i dati di output sono generati con cadenza oraria (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="e1ca6-139">**Set di dati di input:**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="e1ca6-140">**Set di dati di output**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-140">**Output dataset**</span></span>

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

<span data-ttu-id="e1ca6-141">Attualmente, **è il set di dati di output a determinare la pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="e1ca6-142">In altre parole, la pianificazione specificata per il set di dati di output viene usata per eseguire un'attività in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="e1ca6-143">Pertanto, anche se l'attività non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="e1ca6-144">Se l'attività non richiede input, è possibile ignorare la creazione del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="e1ca6-145">Nella definizione di pipeline seguente, la proprietà **scheduler** viene usata per specificare una pianificazione per l'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="e1ca6-146">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-146">This property is optional.</span></span> <span data-ttu-id="e1ca6-147">Attualmente, la pianificazione dell'attività deve corrispondere alla pianificazione specificata per il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="e1ca6-148">In questo esempio, l'attività viene eseguita ogni ora tra l'ora di inizio e quella di fine della pipeline.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="e1ca6-149">I dati di output sono prodotti con cadenza oraria per finestre di tre ore (08:00 - 09:00, 09:00 - 10:00 e 10:00 - 11:00).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="e1ca6-150">Ogni unità di dati usata o prodotta da un'esecuzione di attività prende il nome di **sezione di dati**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="e1ca6-151">Nel diagramma seguente viene illustrato un esempio di attività con un set di dati di input e un set di dati di output:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Utilità di pianificazione della disponibilità](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="e1ca6-153">Il diagramma illustra le sezioni di dati orarie per i set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="e1ca6-154">Il diagramma mostra tre sezioni di input che sono pronte per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="e1ca6-155">L'attività 10-11 AM è in corso e produce la sezione di output 10-11 AM.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="e1ca6-156">È possibile accedere all'intervallo di tempo associato alla sezione corrente nel set di dati JSON usando le variabili [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="e1ca6-157">Allo stesso modo, è possibile accedere all'intervallo di tempo associato a una finestra di attività usando WindowStart e WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="e1ca6-158">La pianificazione di un'attività deve corrispondere alla pianificazione del set di dati di output per l'attività stessa.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="e1ca6-159">Di conseguenza, i valori SliceStart e SliceEnd sono rispettivamente uguali ai valori WindowStart e WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="e1ca6-160">Per altre informazioni su queste variabili, vedere gli articoli [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="e1ca6-161">È possibile usare queste variabili per scopi diversi nel file JSON dell'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="e1ca6-162">Ad esempio, è possibile usarle per selezionare i dati dai set di dati di input e output che rappresentano i dati della serie temporale (ad esempio, dalle 08:00 alle 09:00).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="e1ca6-163">L'esempio usa anche **WindowStart** e **WindowEnd** per selezionare i dati pertinenti per l'esecuzione di un'attività e copiarli in un BLOB con un elemento **folderPath** appropriato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="e1ca6-164">All'oggetto **folderPath** sono applicati parametri per avere una cartella separata per ogni ora.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="e1ca6-165">Nell'esempio precedente, la pianificazione specificata per i set di dati di input e di output è la stessa (cadenza oraria).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="e1ca6-166">Se il set di dati di input per l'attività è disponibile con una frequenza diversa, ad esempio ogni 15 minuti, l'attività che genera il set di dati di output viene eseguita ancora una volta con cadenza oraria, poiché è il set di dati di output a impostare la pianificazione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="e1ca6-167">Per altre informazioni, vedere [Modellare i set di dati con frequenze diverse](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="e1ca6-168">Disponibilità e criteri dei set di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-168">Dataset availability and policies</span></span>
<span data-ttu-id="e1ca6-169">È stato illustrato l'uso delle proprietà frequency e interval nella sezione availability della definizione di set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="e1ca6-170">Esistono alcune altre proprietà che influiscono sulla pianificazione e l'esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="e1ca6-171">Disponibilità dei set di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-171">Dataset availability</span></span> 
<span data-ttu-id="e1ca6-172">La tabella seguente descrive le proprietà che è possibile usare nella sezione **availability**:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="e1ca6-173">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e1ca6-173">Property</span></span> | <span data-ttu-id="e1ca6-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1ca6-174">Description</span></span> | <span data-ttu-id="e1ca6-175">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e1ca6-175">Required</span></span> | <span data-ttu-id="e1ca6-176">Default</span><span class="sxs-lookup"><span data-stu-id="e1ca6-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1ca6-177">frequency</span><span class="sxs-lookup"><span data-stu-id="e1ca6-177">frequency</span></span> |<span data-ttu-id="e1ca6-178">Specifica l'unità di tempo per la produzione di sezioni di set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="e1ca6-179"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="e1ca6-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="e1ca6-180">Sì</span><span class="sxs-lookup"><span data-stu-id="e1ca6-180">Yes</span></span> |<span data-ttu-id="e1ca6-181">ND</span><span class="sxs-lookup"><span data-stu-id="e1ca6-181">NA</span></span> |
| <span data-ttu-id="e1ca6-182">interval</span><span class="sxs-lookup"><span data-stu-id="e1ca6-182">interval</span></span> |<span data-ttu-id="e1ca6-183">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="e1ca6-184">"Intervallo di frequenza x" determina la frequenza con cui viene generata la sezione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="e1ca6-185">Se è necessario suddividere il set di dati su base oraria, impostare l'opzione <b>Frequenza</b> su <b>Ora</b> e <b>Intervallo</b> su <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="e1ca6-186"><b>Nota</b> : se si specifica frequency come Minute, è consigliabile impostare interval su un valore non inferiore a 15</span><span class="sxs-lookup"><span data-stu-id="e1ca6-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="e1ca6-187">Sì</span><span class="sxs-lookup"><span data-stu-id="e1ca6-187">Yes</span></span> |<span data-ttu-id="e1ca6-188">ND</span><span class="sxs-lookup"><span data-stu-id="e1ca6-188">NA</span></span> |
| <span data-ttu-id="e1ca6-189">style</span><span class="sxs-lookup"><span data-stu-id="e1ca6-189">style</span></span> |<span data-ttu-id="e1ca6-190">Specifica se la sezione deve essere generata all'inizio o alla fine dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="e1ca6-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="e1ca6-191">StartOfInterval</span></span></li><li><span data-ttu-id="e1ca6-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="e1ca6-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="e1ca6-193">Se frequency è impostato su Month e style è impostato su EndOfInterval, la sezione viene generata l'ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="e1ca6-194">Se style è impostato su StartOfInterval, la sezione viene generata il primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="e1ca6-195">Se l'opzione Frequnza è impostata su Mese e l'opzione Stile è impostata su EndOfInterval, la sezione viene generata l'ultima ora del giorno.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="e1ca6-196">Se frequency è impostato su Hour e style è impostato su EndOfInterval, la sezione viene generata alla fine dell'ora.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="e1ca6-197">Ad esempio, una sezione per il periodo 13.00 - 14.00 viene generata alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="e1ca6-198">No</span><span class="sxs-lookup"><span data-stu-id="e1ca6-198">No</span></span> |<span data-ttu-id="e1ca6-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="e1ca6-199">EndOfInterval</span></span> |
| <span data-ttu-id="e1ca6-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="e1ca6-200">anchorDateTime</span></span> |<span data-ttu-id="e1ca6-201">Definisce la posizione assoluta nel tempo usata dall'utilità di pianificazione per calcolare i limiti della sezione del set di dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="e1ca6-202"><b>Nota:</b> se AnchorDateTime include parti della data più granulari rispetto alla frequenza, le parti più granulari vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="e1ca6-203">Ad esempio, se l'<b>intervallo</b> è <b>orario</b> (ovvero frequenza: ora e intervallo: 1) e <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>, le parti <b>minuti e secondi</b> di AnchorDateTime vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="e1ca6-204">No</span><span class="sxs-lookup"><span data-stu-id="e1ca6-204">No</span></span> |<span data-ttu-id="e1ca6-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="e1ca6-205">01/01/0001</span></span> |
| <span data-ttu-id="e1ca6-206">offset</span><span class="sxs-lookup"><span data-stu-id="e1ca6-206">offset</span></span> |<span data-ttu-id="e1ca6-207">Intervallo di tempo in base al quale l'inizio e la fine di tutte le sezioni dei set di dati vengono spostate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="e1ca6-208"><b>Nota:</b> se vengono specificati sia anchorDateTime che offset, il risultato sarà lo spostamento combinato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="e1ca6-209">No</span><span class="sxs-lookup"><span data-stu-id="e1ca6-209">No</span></span> |<span data-ttu-id="e1ca6-210">ND</span><span class="sxs-lookup"><span data-stu-id="e1ca6-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="e1ca6-211">Esempio di offset</span><span class="sxs-lookup"><span data-stu-id="e1ca6-211">offset example</span></span>
<span data-ttu-id="e1ca6-212">Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00:00, mezzanotte, ora UTC.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="e1ca6-213">Se, invece, si desidera impostare l'ora di inizio alle 06:00 UTC, impostare l'offset come illustrato nel frammento riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="e1ca6-214">Esempio di anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="e1ca6-214">anchorDateTime example</span></span>
<span data-ttu-id="e1ca6-215">Nell'esempio seguente, il set di dati viene prodotto ogni 23 ore.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="e1ca6-216">La prima sezione inizia all'ora specificata da anchorDateTime, che è impostato su `2017-04-19T08:00:00` (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="e1ca6-217">Esempio di offset/style</span><span class="sxs-lookup"><span data-stu-id="e1ca6-217">offset/style Example</span></span>
<span data-ttu-id="e1ca6-218">Il seguente set di dati è un set di dati mensile e viene generato il 3 di ogni mese alle ore 08:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="e1ca6-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="e1ca6-219">Criteri di set di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-219">Dataset policy</span></span>
<span data-ttu-id="e1ca6-220">Per un set di dati è possibile definire anche un criterio di convalida che specifica in che modo i dati generati dall'esecuzione di una sezione possono essere convalidati prima che siano pronti per l'uso.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="e1ca6-221">In questi casi, al termine del processo di esecuzione, lo stato della sezione di output viene impostato su **In attesa** con lo stato secondario impostato su **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="e1ca6-222">Al termine della convalida, lo stato viene impostato invece su **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="e1ca6-223">Se una sezione di dati è stata correttamente generata ma non ha superato il processo di convalida, le esecuzioni di attività per le sezioni a valle dipendenti da questa sezione non vengono elaborate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="e1ca6-224">[Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) vengono descritti i vari stati disponibili per le sezioni di dati di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="e1ca6-225">La sezione **policy** nella definizione del set di dati stabilisce i criteri o la condizione che le sezioni del set di dati devono soddisfare.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="e1ca6-226">La tabella seguente descrive le proprietà che è possibile usare nella sezione **policy**:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="e1ca6-227">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="e1ca6-227">Policy Name</span></span> | <span data-ttu-id="e1ca6-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1ca6-228">Description</span></span> | <span data-ttu-id="e1ca6-229">Applicato a</span><span class="sxs-lookup"><span data-stu-id="e1ca6-229">Applied To</span></span> | <span data-ttu-id="e1ca6-230">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e1ca6-230">Required</span></span> | <span data-ttu-id="e1ca6-231">Default</span><span class="sxs-lookup"><span data-stu-id="e1ca6-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e1ca6-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="e1ca6-232">minimumSizeMB</span></span> | <span data-ttu-id="e1ca6-233">Verifica che i dati in un **BLOB di Azure** soddisfino i requisiti relativi alle dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="e1ca6-234">BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="e1ca6-234">Azure Blob</span></span> |<span data-ttu-id="e1ca6-235">No</span><span class="sxs-lookup"><span data-stu-id="e1ca6-235">No</span></span> |<span data-ttu-id="e1ca6-236">ND</span><span class="sxs-lookup"><span data-stu-id="e1ca6-236">NA</span></span> |
| <span data-ttu-id="e1ca6-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="e1ca6-237">minimumRows</span></span> | <span data-ttu-id="e1ca6-238">Verifica che i dati in un **database SQL di Azure** o in una **tabella di Azure** contengano il numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="e1ca6-239">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e1ca6-239">Azure SQL Database</span></span></li><li><span data-ttu-id="e1ca6-240">tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="e1ca6-240">Azure Table</span></span></li></ul> |<span data-ttu-id="e1ca6-241">No</span><span class="sxs-lookup"><span data-stu-id="e1ca6-241">No</span></span> |<span data-ttu-id="e1ca6-242">ND</span><span class="sxs-lookup"><span data-stu-id="e1ca6-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="e1ca6-243">esempi</span><span class="sxs-lookup"><span data-stu-id="e1ca6-243">Examples</span></span>
<span data-ttu-id="e1ca6-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="e1ca6-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="e1ca6-246">Per altre informazioni sulle proprietà e gli esempi precedenti, vedere l'articolo [Creare i set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="e1ca6-247">Criteri di attività</span><span class="sxs-lookup"><span data-stu-id="e1ca6-247">Activity policies</span></span>
<span data-ttu-id="e1ca6-248">I criteri influiscono sul comportamento in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione di una tabella.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="e1ca6-249">La tabella seguente fornisce informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-249">The following table provides the details.</span></span>

| <span data-ttu-id="e1ca6-250">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e1ca6-250">Property</span></span> | <span data-ttu-id="e1ca6-251">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="e1ca6-251">Permitted values</span></span> | <span data-ttu-id="e1ca6-252">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="e1ca6-252">Default Value</span></span> | <span data-ttu-id="e1ca6-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1ca6-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1ca6-254">Concorrenza</span><span class="sxs-lookup"><span data-stu-id="e1ca6-254">concurrency</span></span> |<span data-ttu-id="e1ca6-255">Integer </span><span class="sxs-lookup"><span data-stu-id="e1ca6-255">Integer</span></span> <br/><br/><span data-ttu-id="e1ca6-256">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="e1ca6-256">Max value: 10</span></span> |<span data-ttu-id="e1ca6-257">1</span><span class="sxs-lookup"><span data-stu-id="e1ca6-257">1</span></span> |<span data-ttu-id="e1ca6-258">Numero di esecuzioni simultanee dell'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="e1ca6-259">Determina il numero di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="e1ca6-260">Ad esempio, se un'attività deve passare attraverso grandi set di dati disponibili, con un valore di concorrenza maggiore che consente di velocizzare l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="e1ca6-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="e1ca6-261">executionPriorityOrder</span></span> |<span data-ttu-id="e1ca6-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="e1ca6-262">NewestFirst</span></span><br/><br/><span data-ttu-id="e1ca6-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="e1ca6-263">OldestFirst</span></span> |<span data-ttu-id="e1ca6-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="e1ca6-264">OldestFirst</span></span> |<span data-ttu-id="e1ca6-265">Determina l'ordine delle sezioni di dati che vengono elaborate.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="e1ca6-266">Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="e1ca6-267">Se si imposta executionPriorityOrder su NewestFirst, viene elaborata per prima la sezione delle 17:00.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="e1ca6-268">Allo stesso modo, se si imposta executionPriorityORder su OldestFIrst, verrà elaborata per prima la sezione delle 16:00.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="e1ca6-269">retry</span><span class="sxs-lookup"><span data-stu-id="e1ca6-269">retry</span></span> |<span data-ttu-id="e1ca6-270">Integer </span><span class="sxs-lookup"><span data-stu-id="e1ca6-270">Integer</span></span><br/><br/><span data-ttu-id="e1ca6-271">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="e1ca6-271">Max value can be 10</span></span> |<span data-ttu-id="e1ca6-272">0</span><span class="sxs-lookup"><span data-stu-id="e1ca6-272">0</span></span> |<span data-ttu-id="e1ca6-273">Numero di tentativi prima che l'elaborazione dei dati per la sezione sia contrassegnata come errore.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="e1ca6-274">L'esecuzione dell’attività per una sezione di dati viene ritentata fino al numero di tentativi specificato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="e1ca6-275">Il tentativo viene eseguito appena possibile dopo l'errore.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="e1ca6-276">timeout</span><span class="sxs-lookup"><span data-stu-id="e1ca6-276">timeout</span></span> |<span data-ttu-id="e1ca6-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1ca6-277">TimeSpan</span></span> |<span data-ttu-id="e1ca6-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e1ca6-278">00:00:00</span></span> |<span data-ttu-id="e1ca6-279">Timeout per l'attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-279">Timeout for the activity.</span></span> <span data-ttu-id="e1ca6-280">Esempio: 00:10:00 (implica un timeout di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="e1ca6-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="e1ca6-281">Se un valore non è specificato o è 0, il timeout è infinito.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="e1ca6-282">Se il tempo di elaborazione dei dati in una sezione supera il valore di timeout, viene annullato e il sistema prova a ripetere l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="e1ca6-283">Il numero di tentativi dipende dalla proprietà retry.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="e1ca6-284">Quando si verifica il timeout, lo stato viene impostato su TimedOut.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="e1ca6-285">delay</span><span class="sxs-lookup"><span data-stu-id="e1ca6-285">delay</span></span> |<span data-ttu-id="e1ca6-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1ca6-286">TimeSpan</span></span> |<span data-ttu-id="e1ca6-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e1ca6-287">00:00:00</span></span> |<span data-ttu-id="e1ca6-288">Specificare il ritardo prima che abbia inizio l'elaborazione dei dati della sezione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="e1ca6-289">L'esecuzione dell'attività per una sezione di dati viene avviata non appena il ritardo supera il tempo di esecuzione previsto.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="e1ca6-290">Esempio: 00:10:00 (implica un ritardo di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="e1ca6-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="e1ca6-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="e1ca6-291">longRetry</span></span> |<span data-ttu-id="e1ca6-292">Integer </span><span class="sxs-lookup"><span data-stu-id="e1ca6-292">Integer</span></span><br/><br/><span data-ttu-id="e1ca6-293">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="e1ca6-293">Max value: 10</span></span> |<span data-ttu-id="e1ca6-294">1</span><span class="sxs-lookup"><span data-stu-id="e1ca6-294">1</span></span> |<span data-ttu-id="e1ca6-295">Numero di tentativi estesi prima che l'esecuzione della sezione dia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="e1ca6-296">I tentativi longRetry sono distanziati da longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="e1ca6-297">Pertanto, se è necessario specificare un tempo tra i tentativi, utilizzare longRetry.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="e1ca6-298">Se si specificano sia Retry che longRetry, ogni tentativo longRetry include tentativi Retry e il numero massimo di tentativi corrisponde a Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="e1ca6-299">Ad esempio, se si hanno le seguenti impostazioni nel criterio attività:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="e1ca6-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="e1ca6-300">Retry: 3</span></span><br/><span data-ttu-id="e1ca6-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="e1ca6-301">longRetry: 2</span></span><br/><span data-ttu-id="e1ca6-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="e1ca6-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="e1ca6-303">si presume che la sezione da eseguire sia solo una, con stato Waiting, e che l'esecuzione dell'attività abbia ogni volta esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="e1ca6-304">All’inizio vi saranno tre tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="e1ca6-305">Dopo ogni tentativo, lo stato della sezione sarà Retry.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="e1ca6-306">Una volta terminati i 3 tentativi sulla sezione, lo stato sarà LongRetry.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="e1ca6-307">Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="e1ca6-308">Al termine, lo stato della sezione sarà Failed e non verranno eseguiti altri tentativi.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="e1ca6-309">Quindi, sono stati eseguiti 6 tentativi.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="e1ca6-310">Se un'esecuzione ha esito positivo, lo stato della sezione sarà Ready e non saranno ripetuti altri tentativi.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="e1ca6-311">longRetry può essere usato nelle situazioni in cui i dati dipendenti arrivano in orari non deterministici o l'ambiente complessivo in cui si verifica l'elaborazione dei dati è debole.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="e1ca6-312">In tali casi, l'esecuzione di tentativi consecutivi potrebbe non essere utile, mentre l'applicazione di un intervallo consente di ottenere il risultato voluto.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="e1ca6-313">Attenzione: non impostare valori elevati per longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="e1ca6-314">In genere, valori più elevati comportano altri problemi sistemici.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="e1ca6-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="e1ca6-315">longRetryInterval</span></span> |<span data-ttu-id="e1ca6-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1ca6-316">TimeSpan</span></span> |<span data-ttu-id="e1ca6-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e1ca6-317">00:00:00</span></span> |<span data-ttu-id="e1ca6-318">Il ritardo tra tentativi longRetry</span><span class="sxs-lookup"><span data-stu-id="e1ca6-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="e1ca6-319">Per altre informazioni, vedere l'articolo [Pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="e1ca6-320">Elaborazione parallela delle sezioni di dati</span><span class="sxs-lookup"><span data-stu-id="e1ca6-320">Parallel processing of data slices</span></span>
<span data-ttu-id="e1ca6-321">È possibile impostare la data di inizio della pipeline nel passato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="e1ca6-322">Così facendo, Data Factory calcolerà automaticamente tutte le sezioni di dati nel passato recuperando le informazioni e ne avvierà l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="e1ca6-323">Ad esempio: si crea una pipeline con data di inizio 01.04.2017 e la data corrente è 10.04.2017.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="e1ca6-324">Se il set di dati di output ha cadenza giornaliera, Data Factory inizierà immediatamente l'elaborazione di tutte le sezioni dal 01.04.2017 al 09.04.2017 perché la data di inizio è nel passato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="e1ca6-325">La sezione dal 10.04.2017 non verrà ancora elaborata perché il valore della proprietà di stile nella sezione availability è EndOfInterval per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="e1ca6-326">La sezione meno recente verrà elaborata per prima perché il valore predefinito di executionPriorityOrder è OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="e1ca6-327">Per una descrizione della proprietà style, vedere la sezione [disponibilità dei set di dati](#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="e1ca6-328">Per una descrizione della sezione executionPriorityOrder, vedere la sezione [criteri di attività](#activity-policies).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="e1ca6-329">È possibile configurare le sezioni di dati recuperati perché siano eseguite in parallelo, impostando la proprietà **concurrency** nella sezione **policy** dell'attività JSON.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="e1ca6-330">Questa proprietà determina il numero di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="e1ca6-331">Il valore predefinito per questa proprietà è 1.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="e1ca6-332">Pertanto, per impostazione predefinita viene elaborata una sola sezione alla volta.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="e1ca6-333">Il valore massimo è 10.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-333">The maximum value is 10.</span></span> <span data-ttu-id="e1ca6-334">Se una pipeline deve passare attraverso grandi set di dati disponibili, con un valore di concorrenza maggiore che consente di velocizzare l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="e1ca6-335">Nuova esecuzione di una sezione di dati non riuscita</span><span class="sxs-lookup"><span data-stu-id="e1ca6-335">Rerun a failed data slice</span></span>
<span data-ttu-id="e1ca6-336">Quando si verifica un errore durante l'elaborazione di una sezione di dati, è possibile scoprire perché l'elaborazione di una sezione non è riuscita tramite i pannelli del portale di Azure o l'App Monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="e1ca6-337">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline con i pannelli del portale di Azure](data-factory-monitor-manage-pipelines.md) o [App di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="e1ca6-338">Si consideri l'esempio seguente che descrive due attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="e1ca6-339">Activity1 e Activity 2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="e1ca6-340">Activity1 usa una sezione di Dataset1 e genera una sezione di Dataset2, che viene usata come input da Activity2 per produrre una sezione del set di dati finale.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Sezione non riuscita](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="e1ca6-342">Il diagramma illustra che in una delle tre sezioni recenti si è verificato un errore durante la produzione della sezione 9-10 AM per Dataset2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="e1ca6-343">Data Factory tiene automaticamente traccia della dipendenza per il set di dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="e1ca6-344">Di conseguenza, non viene avviata l'esecuzione dell'attività per la sezione di downstream 9-10 AM.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="e1ca6-345">Gli strumenti di monitoraggio e gestione di Data Factory consentono inoltre di analizzare i log di diagnostica relativi alla sezione con esito negativo e individuare facilmente la causa principale del problema per permetterne la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="e1ca6-346">Dopo aver risolto il problema, è possibile avviare facilmente l'esecuzione di attività per generare la sezione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="e1ca6-347">Per altre informazioni su come riavviare le esecuzioni o per comprendere le transizioni di stato per le sezioni di dati, vedere [Monitorare e gestire le pipeline con i pannelli del portale di Azure](data-factory-monitor-manage-pipelines.md) o [App di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="e1ca6-348">Dopo che la sezione 9-10 AM di **Dataset2**è stata eseguita nuovamente, Data Factory avvia l'esecuzione della sezione dipendente 9-10 AM nel set di dati finale.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="e1ca6-350">Attività multiple in una pipeline</span><span class="sxs-lookup"><span data-stu-id="e1ca6-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="e1ca6-351">È possibile avere più di un'attività in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="e1ca6-352">Se si hanno più attività in una pipeline e l'output di un'attività non è l'input di un'altra attività, le attività possono essere eseguite in parallelo se le sezioni di dati di input per le attività sono pronte.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="e1ca6-353">È possibile concatenare due attività, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input di altre attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="e1ca6-354">Le attività possono essere nella stessa pipeline o in pipeline diverse.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="e1ca6-355">La seconda attività viene eseguita solo quando la prima viene completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="e1ca6-356">Ad esempio, si consideri il caso seguente in cui una pipeline ha due attività:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="e1ca6-357">L'attività A1, che richiede il set di dati di input esterno D1 e produce il set di dati di output D2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="e1ca6-358">L'attività A2, che richiede l'input del set di dati D2 e produce il set di dati di output D3.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="e1ca6-359">In questo scenario, le attività A1 e A2 si trovano nella stessa pipeline.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="e1ca6-360">L'attività A1 viene eseguita quando i dati esterni sono disponibili e viene raggiunta la frequenza di disponibilità pianificata.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="e1ca6-361">L'attività A2 viene eseguita quando le sezioni pianificate di D2 diventano disponibili e viene raggiunta la frequenza di disponibilità pianificata.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="e1ca6-362">Se è presente un errore in una delle sezioni del set di dati D2, A2 non verrà eseguita per tale sezione fino a quando non diventa disponibile.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="e1ca6-363">La visualizzazione diagramma con entrambe le attività nella stessa pipeline sarebbe simile al diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Concatenamento di attività nella stessa pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="e1ca6-365">Come accennato in precedenza, le attività possono trovarsi in pipeline diverse.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="e1ca6-366">In questo caso, la visualizzazione diagramma sarebbe simile al diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Concatenamento di attività in due pipeline](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="e1ca6-368">Per un esempio, vedere la sezione [copiare in sequenza](#copy-sequentially) nell'appendice.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="e1ca6-369">Modellare i set di dati con frequenze diverse</span><span class="sxs-lookup"><span data-stu-id="e1ca6-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="e1ca6-370">Negli esempi, la finestra di pianificazione dell'attività e le frequenze relative ai set di dati di input e di output erano identiche.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="e1ca6-371">Alcuni scenari richiedono tuttavia la possibilità di generare output a una frequenza diversa da quella degli input.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="e1ca6-372">Data Factory supporta la modellazione di questi scenari.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="e1ca6-373">Esempio 1: Generazione di un report di output giornaliero per i dati di input, disponibile ogni ora</span><span class="sxs-lookup"><span data-stu-id="e1ca6-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="e1ca6-374">Si consideri uno scenario in cui i dati delle misurazioni di input dei sensori sono disponibili ogni ora nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="e1ca6-375">Si intende generare un report aggregato giornaliero con statistiche, ad esempio media, max e min, per il giorno con [attività Hive di Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="e1ca6-376">Ecco come modellare questo scenario con Data Factory:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="e1ca6-377">**Set di dati di input**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-377">**Input dataset**</span></span>

<span data-ttu-id="e1ca6-378">I file di input vengono rilasciati ogni ora nella cartella relativa al giorno specificato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="e1ca6-379">Il valore di disponibilità per l'input è impostato su **Hour** (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="e1ca6-380">**Set di dati di output**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-380">**Output dataset**</span></span>

<span data-ttu-id="e1ca6-381">Un file di output viene creato ogni giorno nella cartella relativa al giorno corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="e1ca6-382">Il valore di disponibilità per l'output è impostato su **Day** (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="e1ca6-383">**Attività: attività Hive in una pipeline**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="e1ca6-384">Lo script Hive riceve le informazioni *DateTime* appropriate sotto forma di parametri che usano la variabile **WindowStart** , come illustrato nel frammento seguente.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="e1ca6-385">Lo script Hive usa quindi questa variabile per caricare i dati dall'apposita cartella relativa al giorno ed eseguire l'aggregazione per generare l'output.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="e1ca6-386">Il diagramma seguente illustra lo scenario dal punto di vista della dipendenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Dipendenza dei dati](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="e1ca6-388">Per ogni giorno, la sezione di output dipende dalle 24 sezioni orarie ottenute dal set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="e1ca6-389">Data Factory calcola automaticamente queste dipendenze prevedendo le sezioni di dati di input che rientrano nello stesso periodo di tempo della sezione di output da produrre.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="e1ca6-390">Se una delle 24 sezioni di input non è disponibile, Data Factory attenderà che la sezione di input sia pronta prima di avviare l'esecuzione dell'attività giornaliera.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="e1ca6-391">Esempio 2: Definizione di una dipendenza con espressioni e funzioni di Data Factory</span><span class="sxs-lookup"><span data-stu-id="e1ca6-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="e1ca6-392">Si consideri ora un altro scenario</span><span class="sxs-lookup"><span data-stu-id="e1ca6-392">Let’s consider another scenario.</span></span> <span data-ttu-id="e1ca6-393">Si supponga di avere un'attività Hive che elabora i due set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="e1ca6-394">Uno di questi dispone di nuovi dati ogni giorno, mentre l'altro li riceve ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="e1ca6-395">Si supponga inoltre di voler eseguire un join tra i due input e produrre un output ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="e1ca6-396">L'approccio semplice, in cui Data Factory determina automaticamente le sezioni di input da elaborare tramite l'allineamento con il periodo di tempo della sezione dei dati di output, non funziona.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="e1ca6-397">È necessario definire un nuovo approccio per ogni esecuzione di attività in cui Data Factory possa usare la sezione di dati dell'ultima settimana per il set di dati di input settimanale.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="e1ca6-398">Per implementare questo comportamento, è possibile usare le funzioni di Azure Data Factory, come illustrato nel frammento seguente.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="e1ca6-399">**Input1: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="e1ca6-400">Il primo input è il BLOB di Azure aggiornato ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="e1ca6-401">**Input2: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="e1ca6-402">Input2 è il BLOB di Azure aggiornato ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="e1ca6-403">**Output: BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-403">**Output: Azure blob**</span></span>

<span data-ttu-id="e1ca6-404">Un file di output viene creato ogni giorno nella cartella relativa al giorno corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="e1ca6-405">Il valore di disponibilità per l'output è impostato su **day** (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e1ca6-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="e1ca6-406">**Attività: attività Hive in una pipeline**</span><span class="sxs-lookup"><span data-stu-id="e1ca6-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="e1ca6-407">L'attività Hive usa i due input e genera una sezione di output giornaliera.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="e1ca6-408">È possibile specificare che la sezione di output giornaliera dipenda dalla sezione di input della settimana precedente per l'input settimanale procedendo come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="e1ca6-409">Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="e1ca6-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="e1ca6-410">Appendice</span><span class="sxs-lookup"><span data-stu-id="e1ca6-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="e1ca6-411">Esempio: copiare in sequenza</span><span class="sxs-lookup"><span data-stu-id="e1ca6-411">Example: copy sequentially</span></span>
<span data-ttu-id="e1ca6-412">È possibile eseguire più operazioni di copia l'una dopo l'altra in modo sequenziale o ordinato.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="e1ca6-413">Ad esempio, si supponga di avere due attività di copia in una pipeline (CopyActivity1 e CopyActivity2) con i set di dati di input e output seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="e1ca6-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="e1ca6-414">CopyActivity1</span></span>

<span data-ttu-id="e1ca6-415">Input: Dataset.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-415">Input: Dataset.</span></span> <span data-ttu-id="e1ca6-416">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-416">Output: Dataset2.</span></span>

<span data-ttu-id="e1ca6-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="e1ca6-417">CopyActivity2</span></span>

<span data-ttu-id="e1ca6-418">Input: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-418">Input: Dataset2.</span></span>  <span data-ttu-id="e1ca6-419">Output: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-419">Output: Dataset3.</span></span>

<span data-ttu-id="e1ca6-420">CopyActivity2 viene eseguita solo se l'esecuzione di CopyActivity1 è riuscita e Dataset2 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="e1ca6-421">Ecco la pipeline JSON di esempio:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="e1ca6-422">Si noti che nell'esempio, il set di dati di output della prima attività di copia (Dataset2) è specificato come input per la seconda attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="e1ca6-423">La seconda attività viene quindi eseguita solo quando è pronto il set di dati di output dalla prima attività.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="e1ca6-424">Nell'esempio, CopyActivity2 può avere un input diverso, ad esempio Dataset3, ma è necessario specificare Dataset2 anche come input per CopyActivity2, in modo che l'attività non venga eseguita fino a quando CopyActivity1 non è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="e1ca6-425">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-425">For example:</span></span>

<span data-ttu-id="e1ca6-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="e1ca6-426">CopyActivity1</span></span>

<span data-ttu-id="e1ca6-427">Input: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-427">Input: Dataset1.</span></span> <span data-ttu-id="e1ca6-428">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-428">Output: Dataset2.</span></span>

<span data-ttu-id="e1ca6-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="e1ca6-429">CopyActivity2</span></span>

<span data-ttu-id="e1ca6-430">Input: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="e1ca6-431">Output: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="e1ca6-432">Si noti che nell'esempio vengono specificati due set di dati di input per la seconda attività di copia.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="e1ca6-433">Quando si specificano più input, solo il primo set di dati di input viene usato per la copia dei dati e gli altri set di dati vengono usati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="e1ca6-434">L'esecuzione di CopyActivity2 si avvia solo dopo che le seguenti condizioni sono soddisfatte:</span><span class="sxs-lookup"><span data-stu-id="e1ca6-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="e1ca6-435">L’esecuzione di CopyActivity1 è riuscita e Dataset2 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="e1ca6-436">Questo set di dati non viene usato per la copia dei dati in Dataset4.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="e1ca6-437">La sua funzione è semplicemente quella di pianificare la dipendenza per CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="e1ca6-438">Dataset3 è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-438">Dataset3 is available.</span></span> <span data-ttu-id="e1ca6-439">Questo set di dati rappresenta i dati che vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="e1ca6-439">This dataset represents the data that is copied to the destination.</span></span> 