---
title: Azure Data Factory - Informazioni di riferimento sugli script JSON | Documentazione Microsoft
description: "Questo articolo fornisce gli schemi JSON per le entità di Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="555cc-103">Azure Data Factory - Informazioni di riferimento sugli script JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="555cc-104">Questo articolo fornisce gli schemi JSON ed esempi per la definizione di entità di Azure Data Factory (pipeline, attività, set di dati e servizi collegati).</span><span class="sxs-lookup"><span data-stu-id="555cc-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="555cc-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="555cc-105">Pipeline</span></span> 
<span data-ttu-id="555cc-106">La struttura di livello superiore per una definizione di pipeline è la seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="555cc-107">Nella tabella seguente vengono descritte le proprietà all'interno della definizione JSON della pipeline:</span><span class="sxs-lookup"><span data-stu-id="555cc-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="555cc-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-108">Property</span></span> | <span data-ttu-id="555cc-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-109">Description</span></span> | <span data-ttu-id="555cc-110">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="555cc-111">name</span><span class="sxs-lookup"><span data-stu-id="555cc-111">name</span></span> | <span data-ttu-id="555cc-112">Nome della pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-112">Name of the pipeline.</span></span> <span data-ttu-id="555cc-113">Specificare un nome che rappresenta l'azione che l'attività o la pipeline è configurata per eseguire</span><span class="sxs-lookup"><span data-stu-id="555cc-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="555cc-114">Numero massimo di caratteri: 260</span><span class="sxs-lookup"><span data-stu-id="555cc-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="555cc-115">Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</span><span class="sxs-lookup"><span data-stu-id="555cc-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="555cc-116">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</span><span class="sxs-lookup"><span data-stu-id="555cc-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="555cc-117">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-117">Yes</span></span> |
| <span data-ttu-id="555cc-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-118">description</span></span> |<span data-ttu-id="555cc-119">Testo descrittivo per lo scopo dell'attività o della pipeline</span><span class="sxs-lookup"><span data-stu-id="555cc-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="555cc-120">No</span><span class="sxs-lookup"><span data-stu-id="555cc-120">No</span></span> |
| <span data-ttu-id="555cc-121">attività</span><span class="sxs-lookup"><span data-stu-id="555cc-121">activities</span></span> | <span data-ttu-id="555cc-122">Contiene un elenco di attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-122">Contains a list of activities.</span></span> | <span data-ttu-id="555cc-123">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-123">Yes</span></span> |
| <span data-ttu-id="555cc-124">start</span><span class="sxs-lookup"><span data-stu-id="555cc-124">start</span></span> |<span data-ttu-id="555cc-125">Data e ora di inizio per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="555cc-126">Devono essere nel [formato ISO](http://en.wikipedia.org/wiki/ISO_8601),</span><span class="sxs-lookup"><span data-stu-id="555cc-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="555cc-127">ad esempio: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="555cc-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="555cc-128">È possibile specificare un'ora locale, ad esempio in base al fuso orario EST.</span><span class="sxs-lookup"><span data-stu-id="555cc-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="555cc-129">Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.</span><span class="sxs-lookup"><span data-stu-id="555cc-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="555cc-130">Le proprietà start ed end insieme specificano il periodo attivo per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="555cc-131">Le sezioni di output vengono generate solo in questo periodo attivo.</span><span class="sxs-lookup"><span data-stu-id="555cc-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="555cc-132">No</span><span class="sxs-lookup"><span data-stu-id="555cc-132">No</span></span><br/><br/><span data-ttu-id="555cc-133">Se si specifica un valore per la proprietà di fine, è necessario specificare un valore anche per la proprietà di avvio.</span><span class="sxs-lookup"><span data-stu-id="555cc-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="555cc-134">L'ora di inizio e l'ora di fine possono essere entrambe vuote per creare una pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="555cc-135">È necessario specificare entrambi i valori per impostare un periodo attivo per l'esecuzione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="555cc-136">Se non si specificano le ore di inizio e fine durante la creazione di una pipeline, è possibile impostare tali valori in un secondo momento usando il cmdlet Set-AzureRmDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="555cc-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="555cc-137">end</span><span class="sxs-lookup"><span data-stu-id="555cc-137">end</span></span> |<span data-ttu-id="555cc-138">Data e ora di fine per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-138">End date-time for the pipeline.</span></span> <span data-ttu-id="555cc-139">Se specificate, devono essere in formato ISO.</span><span class="sxs-lookup"><span data-stu-id="555cc-139">If specified must be in ISO format.</span></span> <span data-ttu-id="555cc-140">Ad esempio: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="555cc-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="555cc-141">È possibile specificare un'ora locale, ad esempio in base al fuso orario EST.</span><span class="sxs-lookup"><span data-stu-id="555cc-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="555cc-142">Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.</span><span class="sxs-lookup"><span data-stu-id="555cc-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="555cc-143">Per eseguire la pipeline illimitatamente, specificare 9999-09-09 come valore per la proprietà end.</span><span class="sxs-lookup"><span data-stu-id="555cc-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="555cc-144">No</span><span class="sxs-lookup"><span data-stu-id="555cc-144">No</span></span> <br/><br/><span data-ttu-id="555cc-145">Se si specifica un valore per la proprietà di avvio, è necessario specificare un valore anche per la proprietà di fine.</span><span class="sxs-lookup"><span data-stu-id="555cc-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="555cc-146">Vedere le note della proprietà **start** .</span><span class="sxs-lookup"><span data-stu-id="555cc-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="555cc-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="555cc-147">isPaused</span></span> |<span data-ttu-id="555cc-148">Se impostato su true, la pipeline non viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="555cc-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="555cc-149">Valore predefinito = false.</span><span class="sxs-lookup"><span data-stu-id="555cc-149">Default value = false.</span></span> <span data-ttu-id="555cc-150">È possibile usare questa proprietà per abilitare o disabilitare.</span><span class="sxs-lookup"><span data-stu-id="555cc-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="555cc-151">No</span><span class="sxs-lookup"><span data-stu-id="555cc-151">No</span></span> |
| <span data-ttu-id="555cc-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="555cc-152">pipelineMode</span></span> |<span data-ttu-id="555cc-153">Metodo di pianificazione delle esecuzioni per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="555cc-154">I valori consentiti sono scheduled (predefinito) e onetime.</span><span class="sxs-lookup"><span data-stu-id="555cc-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="555cc-155">"Scheduled" indica che la pipeline viene eseguita a intervalli di tempo specificati in base al periodo di attività, ovvero all'ora di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="555cc-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="555cc-156">"Onetime" indica che la pipeline viene eseguita una sola volta.</span><span class="sxs-lookup"><span data-stu-id="555cc-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="555cc-157">Al momento, dopo aver creato una pipeline monouso non è possibile modificarla o aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="555cc-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="555cc-158">Per informazioni dettagliate sull'impostazione onetime, vedere la sezione [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="555cc-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="555cc-159">No</span><span class="sxs-lookup"><span data-stu-id="555cc-159">No</span></span> |
| <span data-ttu-id="555cc-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="555cc-160">expirationTime</span></span> |<span data-ttu-id="555cc-161">Periodo di tempo dopo la creazione in cui la pipeline è valida e deve rimanere con provisioning eseguito.</span><span class="sxs-lookup"><span data-stu-id="555cc-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="555cc-162">Se non ha esecuzioni attive, non riuscite o in sospeso, quando viene raggiunta la scadenza, la pipeline viene eliminata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="555cc-163">No</span><span class="sxs-lookup"><span data-stu-id="555cc-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="555cc-164">Attività</span><span class="sxs-lookup"><span data-stu-id="555cc-164">Activity</span></span> 
<span data-ttu-id="555cc-165">La struttura di livello superiore per un'attività all'interno di una definizione di pipeline (elemento attività) è la seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="555cc-166">Nella tabella seguente vengono descritte le proprietà all'interno della definizione JSON dell'attività:</span><span class="sxs-lookup"><span data-stu-id="555cc-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="555cc-167">Tag</span><span class="sxs-lookup"><span data-stu-id="555cc-167">Tag</span></span> | <span data-ttu-id="555cc-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-168">Description</span></span> | <span data-ttu-id="555cc-169">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-170">name</span><span class="sxs-lookup"><span data-stu-id="555cc-170">name</span></span> |<span data-ttu-id="555cc-171">Nome dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-171">Name of the activity.</span></span> <span data-ttu-id="555cc-172">Specificare un nome che rappresenta l'azione che l'attività è configurata per eseguire</span><span class="sxs-lookup"><span data-stu-id="555cc-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="555cc-173">Numero massimo di caratteri: 260</span><span class="sxs-lookup"><span data-stu-id="555cc-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="555cc-174">Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</span><span class="sxs-lookup"><span data-stu-id="555cc-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="555cc-175">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</span><span class="sxs-lookup"><span data-stu-id="555cc-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="555cc-176">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-176">Yes</span></span> |
| <span data-ttu-id="555cc-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-177">description</span></span> |<span data-ttu-id="555cc-178">Testo descrittivo per lo scopo dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="555cc-179">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-179">Yes</span></span> |
| <span data-ttu-id="555cc-180">type</span><span class="sxs-lookup"><span data-stu-id="555cc-180">type</span></span> |<span data-ttu-id="555cc-181">Specifica il tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-181">Specifies the type of the activity.</span></span> <span data-ttu-id="555cc-182">Per informazioni sui diversi tipi di attività, vedere le sezioni [ARCHIVIAZIONE DEI DATI](#data-stores) e [ATTIVITÀ DI TRASFORMAZIONE DEI DATI](#data-transformation-activities).</span><span class="sxs-lookup"><span data-stu-id="555cc-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="555cc-183">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-183">Yes</span></span> |
| <span data-ttu-id="555cc-184">inputs</span><span class="sxs-lookup"><span data-stu-id="555cc-184">inputs</span></span> |<span data-ttu-id="555cc-185">Tabelle di input usate dall'attività</span><span class="sxs-lookup"><span data-stu-id="555cc-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="555cc-186">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-186">Yes</span></span> |
| <span data-ttu-id="555cc-187">outputs</span><span class="sxs-lookup"><span data-stu-id="555cc-187">outputs</span></span> |<span data-ttu-id="555cc-188">Tabelle di output usate dall'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="555cc-189">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-189">Yes</span></span> |
| <span data-ttu-id="555cc-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="555cc-190">linkedServiceName</span></span> |<span data-ttu-id="555cc-191">Nome del servizio collegato usato dall'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="555cc-192">Per un'attività può essere necessario specificare il servizio collegato che collega all'ambiente di calcolo richiesto.</span><span class="sxs-lookup"><span data-stu-id="555cc-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="555cc-193">Sì per attività di HDInsight, attività di Azure Machine Learning e attività delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="555cc-194">No per tutto il resto</span><span class="sxs-lookup"><span data-stu-id="555cc-194">No for all others</span></span> |
| <span data-ttu-id="555cc-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="555cc-195">typeProperties</span></span> |<span data-ttu-id="555cc-196">Le proprietà nella sezione typeProperties dipendono dal tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="555cc-197">No</span><span class="sxs-lookup"><span data-stu-id="555cc-197">No</span></span> |
| <span data-ttu-id="555cc-198">policy</span><span class="sxs-lookup"><span data-stu-id="555cc-198">policy</span></span> |<span data-ttu-id="555cc-199">Criteri che influiscono sul comportamento di runtime dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="555cc-200">Se vengono omessi, vengono usati i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="555cc-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="555cc-201">No</span><span class="sxs-lookup"><span data-stu-id="555cc-201">No</span></span> |
| <span data-ttu-id="555cc-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="555cc-202">scheduler</span></span> |<span data-ttu-id="555cc-203">La proprietà "scheduler" viene usata per definire la pianificazione per l'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="555cc-204">Le relative proprietà secondarie sono quelle indicate nella sezione [Disponibilità dei set di dati](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="555cc-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="555cc-205">No</span><span class="sxs-lookup"><span data-stu-id="555cc-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="555cc-206">Criteri</span><span class="sxs-lookup"><span data-stu-id="555cc-206">Policies</span></span>
<span data-ttu-id="555cc-207">I criteri influiscono sul comportamento in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione di una tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="555cc-208">La tabella seguente fornisce informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="555cc-208">The following table provides the details.</span></span>

| <span data-ttu-id="555cc-209">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-209">Property</span></span> | <span data-ttu-id="555cc-210">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-210">Permitted values</span></span> | <span data-ttu-id="555cc-211">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="555cc-211">Default Value</span></span> | <span data-ttu-id="555cc-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-213">Concorrenza</span><span class="sxs-lookup"><span data-stu-id="555cc-213">concurrency</span></span> |<span data-ttu-id="555cc-214">Integer </span><span class="sxs-lookup"><span data-stu-id="555cc-214">Integer</span></span> <br/><br/><span data-ttu-id="555cc-215">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="555cc-215">Max value: 10</span></span> |<span data-ttu-id="555cc-216">1</span><span class="sxs-lookup"><span data-stu-id="555cc-216">1</span></span> |<span data-ttu-id="555cc-217">Numero di esecuzioni simultanee dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="555cc-218">Determina il numero di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="555cc-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="555cc-219">Ad esempio, se un'attività deve passare attraverso grandi set di dati disponibili, con un valore di concorrenza maggiore che consente di velocizzare l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="555cc-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="555cc-220">executionPriorityOrder</span></span> |<span data-ttu-id="555cc-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="555cc-221">NewestFirst</span></span><br/><br/><span data-ttu-id="555cc-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="555cc-222">OldestFirst</span></span> |<span data-ttu-id="555cc-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="555cc-223">OldestFirst</span></span> |<span data-ttu-id="555cc-224">Determina l'ordine delle sezioni di dati che vengono elaborate.</span><span class="sxs-lookup"><span data-stu-id="555cc-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="555cc-225">Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="555cc-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="555cc-226">Se si imposta executionPriorityOrder su NewestFirst, viene elaborata per prima la sezione delle 17:00.</span><span class="sxs-lookup"><span data-stu-id="555cc-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="555cc-227">Allo stesso modo, se si imposta executionPriorityORder su OldestFIrst, verrà elaborata per prima la sezione delle 16:00.</span><span class="sxs-lookup"><span data-stu-id="555cc-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="555cc-228">retry</span><span class="sxs-lookup"><span data-stu-id="555cc-228">retry</span></span> |<span data-ttu-id="555cc-229">Integer </span><span class="sxs-lookup"><span data-stu-id="555cc-229">Integer</span></span><br/><br/><span data-ttu-id="555cc-230">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="555cc-230">Max value can be 10</span></span> |<span data-ttu-id="555cc-231">0</span><span class="sxs-lookup"><span data-stu-id="555cc-231">0</span></span> |<span data-ttu-id="555cc-232">Numero di tentativi prima che l'elaborazione dei dati per la sezione sia contrassegnata come errore.</span><span class="sxs-lookup"><span data-stu-id="555cc-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="555cc-233">L'esecuzione dell’attività per una sezione di dati viene ritentata fino al numero di tentativi specificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="555cc-234">Il tentativo viene eseguito appena possibile dopo l'errore.</span><span class="sxs-lookup"><span data-stu-id="555cc-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="555cc-235">timeout</span><span class="sxs-lookup"><span data-stu-id="555cc-235">timeout</span></span> |<span data-ttu-id="555cc-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="555cc-236">TimeSpan</span></span> |<span data-ttu-id="555cc-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="555cc-237">00:00:00</span></span> |<span data-ttu-id="555cc-238">Timeout per l'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-238">Timeout for the activity.</span></span> <span data-ttu-id="555cc-239">Esempio: 00:10:00 (implica un timeout di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="555cc-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="555cc-240">Se un valore non è specificato o è 0, il timeout è infinito.</span><span class="sxs-lookup"><span data-stu-id="555cc-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="555cc-241">Se il tempo di elaborazione dei dati in una sezione supera il valore di timeout, viene annullato e il sistema prova a ripetere l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="555cc-242">Il numero di tentativi dipende dalla proprietà retry.</span><span class="sxs-lookup"><span data-stu-id="555cc-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="555cc-243">Quando si verifica il timeout, lo stato viene impostato su TimedOut.</span><span class="sxs-lookup"><span data-stu-id="555cc-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="555cc-244">delay</span><span class="sxs-lookup"><span data-stu-id="555cc-244">delay</span></span> |<span data-ttu-id="555cc-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="555cc-245">TimeSpan</span></span> |<span data-ttu-id="555cc-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="555cc-246">00:00:00</span></span> |<span data-ttu-id="555cc-247">Specificare il ritardo prima che abbia inizio l'elaborazione dei dati della sezione.</span><span class="sxs-lookup"><span data-stu-id="555cc-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="555cc-248">L'esecuzione dell'attività per una sezione di dati viene avviata non appena il ritardo supera il tempo di esecuzione previsto.</span><span class="sxs-lookup"><span data-stu-id="555cc-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="555cc-249">Esempio: 00:10:00 (implica un ritardo di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="555cc-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="555cc-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="555cc-250">longRetry</span></span> |<span data-ttu-id="555cc-251">Integer </span><span class="sxs-lookup"><span data-stu-id="555cc-251">Integer</span></span><br/><br/><span data-ttu-id="555cc-252">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="555cc-252">Max value: 10</span></span> |<span data-ttu-id="555cc-253">1</span><span class="sxs-lookup"><span data-stu-id="555cc-253">1</span></span> |<span data-ttu-id="555cc-254">Numero di tentativi estesi prima che l'esecuzione della sezione dia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="555cc-255">I tentativi longRetry sono distanziati da longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="555cc-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="555cc-256">Pertanto, se è necessario specificare un tempo tra i tentativi, utilizzare longRetry.</span><span class="sxs-lookup"><span data-stu-id="555cc-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="555cc-257">Se si specificano sia Retry che longRetry, ogni tentativo longRetry include tentativi Retry e il numero massimo di tentativi corrisponde a Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="555cc-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="555cc-258">Ad esempio, se si hanno le seguenti impostazioni nel criterio attività:</span><span class="sxs-lookup"><span data-stu-id="555cc-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="555cc-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="555cc-259">Retry: 3</span></span><br/><span data-ttu-id="555cc-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="555cc-260">longRetry: 2</span></span><br/><span data-ttu-id="555cc-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="555cc-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="555cc-262">si presume che la sezione da eseguire sia solo una, con stato Waiting, e che l'esecuzione dell'attività abbia ogni volta esito negativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="555cc-263">All’inizio vi saranno tre tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="555cc-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="555cc-264">Dopo ogni tentativo, lo stato della sezione sarà Retry.</span><span class="sxs-lookup"><span data-stu-id="555cc-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="555cc-265">Una volta terminati i 3 tentativi sulla sezione, lo stato sarà LongRetry.</span><span class="sxs-lookup"><span data-stu-id="555cc-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="555cc-266">Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="555cc-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="555cc-267">Al termine, lo stato della sezione sarà Failed e non verranno eseguiti altri tentativi.</span><span class="sxs-lookup"><span data-stu-id="555cc-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="555cc-268">Quindi, sono stati eseguiti 6 tentativi.</span><span class="sxs-lookup"><span data-stu-id="555cc-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="555cc-269">Se un'esecuzione ha esito positivo, lo stato della sezione sarà Ready e non saranno ripetuti altri tentativi.</span><span class="sxs-lookup"><span data-stu-id="555cc-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="555cc-270">longRetry può essere usato nelle situazioni in cui i dati dipendenti arrivano in orari non deterministici o l'ambiente complessivo in cui si verifica l'elaborazione dei dati è debole.</span><span class="sxs-lookup"><span data-stu-id="555cc-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="555cc-271">In tali casi, l'esecuzione di tentativi consecutivi potrebbe non essere utile, mentre l'applicazione di un intervallo consente di ottenere il risultato voluto.</span><span class="sxs-lookup"><span data-stu-id="555cc-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="555cc-272">Attenzione: non impostare valori elevati per longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="555cc-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="555cc-273">In genere, valori più elevati comportano altri problemi sistemici.</span><span class="sxs-lookup"><span data-stu-id="555cc-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="555cc-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="555cc-274">longRetryInterval</span></span> |<span data-ttu-id="555cc-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="555cc-275">TimeSpan</span></span> |<span data-ttu-id="555cc-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="555cc-276">00:00:00</span></span> |<span data-ttu-id="555cc-277">Il ritardo tra tentativi longRetry</span><span class="sxs-lookup"><span data-stu-id="555cc-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="555cc-278">sezione typeProperties</span><span class="sxs-lookup"><span data-stu-id="555cc-278">typeProperties section</span></span>
<span data-ttu-id="555cc-279">La sezione typeProperties è diversa per ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="555cc-280">Le attività di trasformazione dispongono delle sole proprietà del tipo.</span><span class="sxs-lookup"><span data-stu-id="555cc-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="555cc-281">Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="555cc-282">L'**attività di copia** ha due sottosezioni nella sezione typeProperties: **origine** e **sink**.</span><span class="sxs-lookup"><span data-stu-id="555cc-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="555cc-283">Vedere la sezione [Archivi dati](#data-stores) in questo articolo per esempi JSON che mostrano come usare un archivio dati come origine e/o sink.</span><span class="sxs-lookup"><span data-stu-id="555cc-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="555cc-284">Esempio di una pipeline di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-284">Sample copy pipeline</span></span>
<span data-ttu-id="555cc-285">In questa pipeline di esempio è presente un'attività di tipo **Copy** in the **attività** .</span><span class="sxs-lookup"><span data-stu-id="555cc-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="555cc-286">In questo esempio, [Copia attività](data-factory-data-movement-activities.md) consente di copiare i dati da un archivio BLOB di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="555cc-287">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="555cc-287">Note the following points:</span></span>

* <span data-ttu-id="555cc-288">Nella sezione delle attività esiste una sola attività con l'oggetto **type** impostato su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="555cc-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="555cc-289">L'input per l'attività è impostato su **InputDataset** e l'output è impostato su **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="555cc-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="555cc-290">Nella sezione **typeProperties** vengono specificati **BlobSource** come tipo di origine e **SqlSink** come tipo di sink.</span><span class="sxs-lookup"><span data-stu-id="555cc-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="555cc-291">Vedere la sezione [Archivi dati](#data-stores) in questo articolo per esempi JSON che mostrano come usare un archivio dati come origine e/o sink.</span><span class="sxs-lookup"><span data-stu-id="555cc-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="555cc-292">Per la procedura completa di creazione di questa pipeline, vedere [Esercitazione: copiare i dati dall'archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="555cc-293">Esempio di una pipeline di trasformazione</span><span class="sxs-lookup"><span data-stu-id="555cc-293">Sample transformation pipeline</span></span>
<span data-ttu-id="555cc-294">In questa pipeline di esempio è presente un'attività di tipo **HDInsightHive** in the **attività** .</span><span class="sxs-lookup"><span data-stu-id="555cc-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="555cc-295">In questo esempio, l' [attività Hive di HDInsight](data-factory-hive-activity.md) trasforma i dati da un archivio BLOB di Azure tramite l'esecuzione di un file di script Hive in un cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="555cc-296">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="555cc-296">Note the following points:</span></span> 

* <span data-ttu-id="555cc-297">Nella sezione attività esiste una sola attività con l'oggetto **type** impostato su **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="555cc-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="555cc-298">Il file di script Hive, **partitionweblogs.hql**, è archiviato nell'account di archiviazione di Azure (specificato da scriptLinkedService, denominato **AzureStorageLinkedService**) e nella cartella **script** nel contenitore **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="555cc-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="555cc-299">La sezione **defines** viene usata per specificare le impostazioni di runtime che vengono passate allo script Hive come valori di configurazione Hive, ad esempio `${hiveconf:inputtable}` e `${hiveconf:partitionedtable}`.</span><span class="sxs-lookup"><span data-stu-id="555cc-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="555cc-300">Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="555cc-301">Per la procedura completa della creazione di questa pipeline, vedere [Esercitazione: creare la prima pipeline per elaborare i dati usando il cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="555cc-302">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-302">Linked service</span></span>
<span data-ttu-id="555cc-303">La struttura di livello superiore per una definizione di servizio collegato è la seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="555cc-304">Nella tabella seguente vengono descritte le proprietà all'interno della definizione JSON dell'attività:</span><span class="sxs-lookup"><span data-stu-id="555cc-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="555cc-305">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-305">Property</span></span> | <span data-ttu-id="555cc-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-306">Description</span></span> | <span data-ttu-id="555cc-307">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="555cc-308">name</span><span class="sxs-lookup"><span data-stu-id="555cc-308">name</span></span> | <span data-ttu-id="555cc-309">Nome del servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-309">Name of the linked service.</span></span> | <span data-ttu-id="555cc-310">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-310">Yes</span></span> | 
| <span data-ttu-id="555cc-311">proprietà - tipo</span><span class="sxs-lookup"><span data-stu-id="555cc-311">properties - type</span></span> | <span data-ttu-id="555cc-312">Tipo di servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-312">Type of the linked service.</span></span> <span data-ttu-id="555cc-313">Ad esempio: archiviazione di Azure, database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="555cc-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="555cc-314">typeProperties</span></span> | <span data-ttu-id="555cc-315">La sezione typeProperties contiene elementi che sono diversi per ogni archivio dati o ambiente di calcolo.</span><span class="sxs-lookup"><span data-stu-id="555cc-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="555cc-316">Vedere la sezione [Archivi dati](#datastores) per tutti i servizi collegati agli archivi dati e la sezione [Ambienti di calcolo](#compute-environments) per tutti i servizi collegati agli ambienti di calcolo.</span><span class="sxs-lookup"><span data-stu-id="555cc-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="555cc-317">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-317">Dataset</span></span> 
<span data-ttu-id="555cc-318">Un set di dati in Azure Data Factory viene definito come segue:</span><span class="sxs-lookup"><span data-stu-id="555cc-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="555cc-319">La tabella seguente descrive le proprietà nel codice JSON precedente:</span><span class="sxs-lookup"><span data-stu-id="555cc-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="555cc-320">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-320">Property</span></span> | <span data-ttu-id="555cc-321">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-321">Description</span></span> | <span data-ttu-id="555cc-322">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-322">Required</span></span> | <span data-ttu-id="555cc-323">Default</span><span class="sxs-lookup"><span data-stu-id="555cc-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-324">name</span><span class="sxs-lookup"><span data-stu-id="555cc-324">name</span></span> | <span data-ttu-id="555cc-325">Nome del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-325">Name of the dataset.</span></span> <span data-ttu-id="555cc-326">Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="555cc-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="555cc-327">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-327">Yes</span></span> |<span data-ttu-id="555cc-328">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-328">NA</span></span> |
| <span data-ttu-id="555cc-329">type</span><span class="sxs-lookup"><span data-stu-id="555cc-329">type</span></span> | <span data-ttu-id="555cc-330">Tipo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-330">Type of the dataset.</span></span> <span data-ttu-id="555cc-331">Specificare uno dei tipi supportati da Azure Data Factory, ad esempio AzureBlob, AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="555cc-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="555cc-332">Vedere la sezione [Archivi dati](#data-stores) per tutti gli archivi dati e i tipi di set di dati supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="555cc-333">structure</span><span class="sxs-lookup"><span data-stu-id="555cc-333">structure</span></span> | <span data-ttu-id="555cc-334">Schema del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-334">Schema of the dataset.</span></span> <span data-ttu-id="555cc-335">Contiene le colonne, i tipi e così via.</span><span class="sxs-lookup"><span data-stu-id="555cc-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="555cc-336">No</span><span class="sxs-lookup"><span data-stu-id="555cc-336">No</span></span> |<span data-ttu-id="555cc-337">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-337">NA</span></span> |
| <span data-ttu-id="555cc-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="555cc-338">typeProperties</span></span> | <span data-ttu-id="555cc-339">Proprietà che corrispondono al tipo selezionato.</span><span class="sxs-lookup"><span data-stu-id="555cc-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="555cc-340">Vedere la sezione [Archivi dati](#data-stores) per i tipi supportati e le rispettive proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="555cc-341">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-341">Yes</span></span> |<span data-ttu-id="555cc-342">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-342">NA</span></span> |
| <span data-ttu-id="555cc-343">external</span><span class="sxs-lookup"><span data-stu-id="555cc-343">external</span></span> | <span data-ttu-id="555cc-344">Flag booleano per specificare se un set di dati è generato o meno in modo esplicito da una pipeline della data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="555cc-345">No</span><span class="sxs-lookup"><span data-stu-id="555cc-345">No</span></span> |<span data-ttu-id="555cc-346">false</span><span class="sxs-lookup"><span data-stu-id="555cc-346">false</span></span> |
| <span data-ttu-id="555cc-347">disponibilità</span><span class="sxs-lookup"><span data-stu-id="555cc-347">availability</span></span> | <span data-ttu-id="555cc-348">Definisce la finestra di elaborazione o il modello di sezionamento per la produzione di set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="555cc-349">Per informazioni dettagliate sul modello di sezionamento dei set di dati, vedere l'articolo [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="555cc-350">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-350">Yes</span></span> |<span data-ttu-id="555cc-351">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-351">NA</span></span> |
| <span data-ttu-id="555cc-352">policy</span><span class="sxs-lookup"><span data-stu-id="555cc-352">policy</span></span> |<span data-ttu-id="555cc-353">Definisce i criteri o la condizione che devono soddisfare i sezionamenti di set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="555cc-354">Per informazioni dettagliate, vedere la sezione [Criteri di set di dati](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="555cc-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="555cc-355">No</span><span class="sxs-lookup"><span data-stu-id="555cc-355">No</span></span> |<span data-ttu-id="555cc-356">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-356">NA</span></span> |

<span data-ttu-id="555cc-357">Ogni colonna della sezione **struttura** contiene le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="555cc-358">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-358">Property</span></span> | <span data-ttu-id="555cc-359">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-359">Description</span></span> | <span data-ttu-id="555cc-360">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-361">name</span><span class="sxs-lookup"><span data-stu-id="555cc-361">name</span></span> |<span data-ttu-id="555cc-362">Nome della colonna.</span><span class="sxs-lookup"><span data-stu-id="555cc-362">Name of the column.</span></span> |<span data-ttu-id="555cc-363">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-363">Yes</span></span> |
| <span data-ttu-id="555cc-364">type</span><span class="sxs-lookup"><span data-stu-id="555cc-364">type</span></span> |<span data-ttu-id="555cc-365">Tipo di dati della colonna.</span><span class="sxs-lookup"><span data-stu-id="555cc-365">Data type of the column.</span></span>  |<span data-ttu-id="555cc-366">No</span><span class="sxs-lookup"><span data-stu-id="555cc-366">No</span></span> |
| <span data-ttu-id="555cc-367">culture</span><span class="sxs-lookup"><span data-stu-id="555cc-367">culture</span></span> |<span data-ttu-id="555cc-368">Impostazioni cultura basate su .NET da usare quando il tipo è specificato ed un tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="555cc-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="555cc-369">Il valore predefinito è `en-us`.</span><span class="sxs-lookup"><span data-stu-id="555cc-369">Default is `en-us`.</span></span> |<span data-ttu-id="555cc-370">No</span><span class="sxs-lookup"><span data-stu-id="555cc-370">No</span></span> |
| <span data-ttu-id="555cc-371">format</span><span class="sxs-lookup"><span data-stu-id="555cc-371">format</span></span> |<span data-ttu-id="555cc-372">Stringa di formato da usare quando il tipo è specificato ed è un tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="555cc-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="555cc-373">No</span><span class="sxs-lookup"><span data-stu-id="555cc-373">No</span></span> |

<span data-ttu-id="555cc-374">Nell'esempio seguente il set di dati ha tre colonne, ovvero `slicetimestamp`, `projectname` e `pageviews`, che sono rispettivamente di tipo String, String e Decimal.</span><span class="sxs-lookup"><span data-stu-id="555cc-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="555cc-375">La tabella seguente descrive le proprietà che è possibile usare nella sezione **availability**:</span><span class="sxs-lookup"><span data-stu-id="555cc-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="555cc-376">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-376">Property</span></span> | <span data-ttu-id="555cc-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-377">Description</span></span> | <span data-ttu-id="555cc-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-378">Required</span></span> | <span data-ttu-id="555cc-379">Default</span><span class="sxs-lookup"><span data-stu-id="555cc-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-380">frequency</span><span class="sxs-lookup"><span data-stu-id="555cc-380">frequency</span></span> |<span data-ttu-id="555cc-381">Specifica l'unità di tempo per la produzione di sezioni di set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="555cc-382"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="555cc-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="555cc-383">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-383">Yes</span></span> |<span data-ttu-id="555cc-384">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-384">NA</span></span> |
| <span data-ttu-id="555cc-385">interval</span><span class="sxs-lookup"><span data-stu-id="555cc-385">interval</span></span> |<span data-ttu-id="555cc-386">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="555cc-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="555cc-387">"Intervallo di frequenza x" determina la frequenza con cui viene generata la sezione.</span><span class="sxs-lookup"><span data-stu-id="555cc-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="555cc-388">Se è necessario suddividere il set di dati su base oraria, impostare l'opzione <b>Frequenza</b> su <b>Ora</b> e <b>Intervallo</b> su <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="555cc-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="555cc-389"><b>Nota</b> : se si specifica frequency come Minute, è consigliabile impostare interval su un valore non inferiore a 15</span><span class="sxs-lookup"><span data-stu-id="555cc-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="555cc-390">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-390">Yes</span></span> |<span data-ttu-id="555cc-391">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-391">NA</span></span> |
| <span data-ttu-id="555cc-392">style</span><span class="sxs-lookup"><span data-stu-id="555cc-392">style</span></span> |<span data-ttu-id="555cc-393">Specifica se la sezione deve essere generata all'inizio o alla fine dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="555cc-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="555cc-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="555cc-394">StartOfInterval</span></span></li><li><span data-ttu-id="555cc-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="555cc-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="555cc-396">Se frequency è impostato su Month e style è impostato su EndOfInterval, la sezione viene generata l'ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="555cc-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="555cc-397">Se style è impostato su StartOfInterval, la sezione viene generata il primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="555cc-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="555cc-398">Se l'opzione Frequnza è impostata su Mese e l'opzione Stile è impostata su EndOfInterval, la sezione viene generata l'ultima ora del giorno.</span><span class="sxs-lookup"><span data-stu-id="555cc-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="555cc-399">Se frequency è impostato su Hour e style è impostato su EndOfInterval, la sezione viene generata alla fine dell'ora.</span><span class="sxs-lookup"><span data-stu-id="555cc-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="555cc-400">Ad esempio, una sezione per il periodo 13.00 - 14.00 viene generata alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="555cc-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="555cc-401">No</span><span class="sxs-lookup"><span data-stu-id="555cc-401">No</span></span> |<span data-ttu-id="555cc-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="555cc-402">EndOfInterval</span></span> |
| <span data-ttu-id="555cc-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="555cc-403">anchorDateTime</span></span> |<span data-ttu-id="555cc-404">Definisce la posizione assoluta nel tempo usata dall'utilità di pianificazione per calcolare i limiti della sezione del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="555cc-405"><b>Nota:</b> se AnchorDateTime include parti della data più granulari rispetto alla frequenza, le parti più granulari vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="555cc-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="555cc-406">Ad esempio, se l'<b>intervallo</b> è <b>orario</b> (ovvero frequenza: ora e intervallo: 1) e <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>, le parti <b>minuti e secondi</b> di AnchorDateTime vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="555cc-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="555cc-407">No</span><span class="sxs-lookup"><span data-stu-id="555cc-407">No</span></span> |<span data-ttu-id="555cc-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="555cc-408">01/01/0001</span></span> |
| <span data-ttu-id="555cc-409">offset</span><span class="sxs-lookup"><span data-stu-id="555cc-409">offset</span></span> |<span data-ttu-id="555cc-410">Intervallo di tempo in base al quale l'inizio e la fine di tutte le sezioni dei set di dati vengono spostate.</span><span class="sxs-lookup"><span data-stu-id="555cc-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="555cc-411"><b>Nota:</b> se vengono specificati sia anchorDateTime che offset, il risultato sarà lo spostamento combinato.</span><span class="sxs-lookup"><span data-stu-id="555cc-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="555cc-412">No</span><span class="sxs-lookup"><span data-stu-id="555cc-412">No</span></span> |<span data-ttu-id="555cc-413">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-413">NA</span></span> |

<span data-ttu-id="555cc-414">La sezione availability seguente specifica che il set di dati di output viene generato ogni ora oppure che il set di dati di input è disponibile ogni ora:</span><span class="sxs-lookup"><span data-stu-id="555cc-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="555cc-415">La sezione **policy** nella definizione del set di dati stabilisce i criteri o la condizione che le sezioni del set di dati devono soddisfare.</span><span class="sxs-lookup"><span data-stu-id="555cc-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="555cc-416">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="555cc-416">Policy Name</span></span> | <span data-ttu-id="555cc-417">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-417">Description</span></span> | <span data-ttu-id="555cc-418">Applicato a</span><span class="sxs-lookup"><span data-stu-id="555cc-418">Applied To</span></span> | <span data-ttu-id="555cc-419">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-419">Required</span></span> | <span data-ttu-id="555cc-420">Default</span><span class="sxs-lookup"><span data-stu-id="555cc-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="555cc-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="555cc-421">minimumSizeMB</span></span> |<span data-ttu-id="555cc-422">Verifica che i dati in un **BLOB di Azure** soddisfino i requisiti relativi alle dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="555cc-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="555cc-423">BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-423">Azure Blob</span></span> |<span data-ttu-id="555cc-424">No</span><span class="sxs-lookup"><span data-stu-id="555cc-424">No</span></span> |<span data-ttu-id="555cc-425">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-425">NA</span></span> |
| <span data-ttu-id="555cc-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="555cc-426">minimumRows</span></span> |<span data-ttu-id="555cc-427">Verifica che i dati in un **database SQL di Azure** o in una **tabella di Azure** contengano il numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="555cc-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="555cc-428">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-428">Azure SQL Database</span></span></li><li><span data-ttu-id="555cc-429">tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-429">Azure Table</span></span></li></ul> |<span data-ttu-id="555cc-430">No</span><span class="sxs-lookup"><span data-stu-id="555cc-430">No</span></span> |<span data-ttu-id="555cc-431">ND</span><span class="sxs-lookup"><span data-stu-id="555cc-431">NA</span></span> |

<span data-ttu-id="555cc-432">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="555cc-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="555cc-433">A meno che un set di dati non sia generato da Azure Data Factory, deve essere contrassegnato come **external**.</span><span class="sxs-lookup"><span data-stu-id="555cc-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="555cc-434">Questa impostazione si applica in genere agli input della prima attività in una pipeline, a meno che non si usi il concatenamento di attività o di pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="555cc-435">name</span><span class="sxs-lookup"><span data-stu-id="555cc-435">Name</span></span> | <span data-ttu-id="555cc-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-436">Description</span></span> | <span data-ttu-id="555cc-437">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-437">Required</span></span> | <span data-ttu-id="555cc-438">Default Value</span><span class="sxs-lookup"><span data-stu-id="555cc-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="555cc-439">dataDelay</span></span> |<span data-ttu-id="555cc-440">Tempo di attesa per il controllo sulla disponibilità dei dati esterni per il sezionamento specificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="555cc-441">Ad esempio, se i dati sono disponibili ogni ora, il controllo per vedere se i dati esterni sono disponibili e la sezione corrispondente è Ready può essere ritardato usando dataDelay.</span><span class="sxs-lookup"><span data-stu-id="555cc-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="555cc-442">Si applica solo all'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="555cc-442">Only applies to the present time.</span></span>  <span data-ttu-id="555cc-443">Ad esempio, se in questo momento sono le 13:00 e questo valore è di 10 minuti, la convalida inizia alle 13:10.</span><span class="sxs-lookup"><span data-stu-id="555cc-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="555cc-444">Questa impostazione non influisce sulle sezioni nel passato; le sezioni con i parametri Ora di fine sezione + dataDelay < Ora vengono elaborate senza alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="555cc-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="555cc-445">Valori superiori a 23:59 ore devono essere specificati nel formato `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="555cc-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="555cc-446">Per specificare 24 ore, ad esempio, non utilizzare 24:00:00; utilizzare invece 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="555cc-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="555cc-447">Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="555cc-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="555cc-448">Per 1 giorno e 4 ore, specificare 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="555cc-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="555cc-449">No</span><span class="sxs-lookup"><span data-stu-id="555cc-449">No</span></span> |<span data-ttu-id="555cc-450">0</span><span class="sxs-lookup"><span data-stu-id="555cc-450">0</span></span> |
| <span data-ttu-id="555cc-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="555cc-451">retryInterval</span></span> |<span data-ttu-id="555cc-452">Il tempo di attesa tra un errore e il successivo tentativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="555cc-453">Se un tentativo non riesce, il tentativo successivo avviene dopo retryInterval.</span><span class="sxs-lookup"><span data-stu-id="555cc-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="555cc-454">Se in questo momento sono le 13:00, viene avviato il primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="555cc-455">Se la durata per completare il primo controllo di convalida è 1 minuto e l'operazione non è riuscita, il tentativo successivo è alle 13:00 + 1 min (durata) + 1 min (intervallo tentativi) = 13:02.</span><span class="sxs-lookup"><span data-stu-id="555cc-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="555cc-456">Per le sezioni passate, non si verifica alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="555cc-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="555cc-457">La ripetizione avviene immediatamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-457">The retry happens immediately.</span></span> |<span data-ttu-id="555cc-458">No</span><span class="sxs-lookup"><span data-stu-id="555cc-458">No</span></span> |<span data-ttu-id="555cc-459">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="555cc-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="555cc-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-460">retryTimeout</span></span> |<span data-ttu-id="555cc-461">Timeout per ogni nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="555cc-462">Se questa proprietà è impostata su 10 minuti, la convalida deve essere completata entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="555cc-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="555cc-463">Se sono necessari più di 10 minuti per eseguire la convalida, il tentativo viene sospeso.</span><span class="sxs-lookup"><span data-stu-id="555cc-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="555cc-464">Se tutti i tentativi per la convalida scadono, la sezione viene contrassegnata come TimedOut.</span><span class="sxs-lookup"><span data-stu-id="555cc-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="555cc-465">No</span><span class="sxs-lookup"><span data-stu-id="555cc-465">No</span></span> |<span data-ttu-id="555cc-466">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="555cc-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="555cc-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="555cc-467">maximumRetry</span></span> |<span data-ttu-id="555cc-468">Numero di volte per controllare la disponibilità dei dati esterni.</span><span class="sxs-lookup"><span data-stu-id="555cc-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="555cc-469">Il valore massimo consentito è 10.</span><span class="sxs-lookup"><span data-stu-id="555cc-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="555cc-470">No</span><span class="sxs-lookup"><span data-stu-id="555cc-470">No</span></span> |<span data-ttu-id="555cc-471">3</span><span class="sxs-lookup"><span data-stu-id="555cc-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="555cc-472">Archivi dati</span><span class="sxs-lookup"><span data-stu-id="555cc-472">DATA STORES</span></span>
<span data-ttu-id="555cc-473">La sezione [Servizi collegati](#linked-service) ha fornito le descrizioni degli elementi JSON comuni a tutti i tipi di servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="555cc-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="555cc-474">Questa sezione fornisce informazioni sugli elementi JSON specifici di ogni archivio dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="555cc-475">La sezione [Set di dati ](#dataset) ha fornito le descrizioni degli elementi JSON comuni a tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="555cc-476">Questa sezione fornisce informazioni sugli elementi JSON specifici di ogni archivio dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="555cc-477">La sezione [Attività](#activity) ha fornito le descrizioni degli elementi JSON comuni a tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="555cc-478">Questa sezione fornisce informazioni sugli elementi JSON specifici di ogni archivio dati quando è usato come origine/sink in un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="555cc-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="555cc-479">Fare clic sul collegamento all'archivio a cui si è interessati per visualizzare gli schemi JSON per i servizi collegati, il set di dati e l'origine/sink dell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="555cc-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="555cc-480">Categoria</span><span class="sxs-lookup"><span data-stu-id="555cc-480">Category</span></span> | <span data-ttu-id="555cc-481">Archivio dati</span><span class="sxs-lookup"><span data-stu-id="555cc-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="555cc-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="555cc-482">**Azure**</span></span> |[<span data-ttu-id="555cc-483">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="555cc-484">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="555cc-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="555cc-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="555cc-486">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="555cc-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="555cc-488">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="555cc-489">Archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="555cc-490">**Database**</span><span class="sxs-lookup"><span data-stu-id="555cc-490">**Databases**</span></span> |[<span data-ttu-id="555cc-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="555cc-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="555cc-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="555cc-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="555cc-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="555cc-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="555cc-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="555cc-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="555cc-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="555cc-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="555cc-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="555cc-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="555cc-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="555cc-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="555cc-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="555cc-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="555cc-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="555cc-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="555cc-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="555cc-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="555cc-501">**NoSQL**</span></span> |[<span data-ttu-id="555cc-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="555cc-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="555cc-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="555cc-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="555cc-504">**File**</span><span class="sxs-lookup"><span data-stu-id="555cc-504">**File**</span></span> |[<span data-ttu-id="555cc-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="555cc-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="555cc-506">File system</span><span class="sxs-lookup"><span data-stu-id="555cc-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="555cc-507">FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="555cc-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="555cc-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="555cc-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="555cc-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="555cc-510">**Altro**</span><span class="sxs-lookup"><span data-stu-id="555cc-510">**Others**</span></span> |[<span data-ttu-id="555cc-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="555cc-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="555cc-512">OData</span><span class="sxs-lookup"><span data-stu-id="555cc-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="555cc-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="555cc-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="555cc-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="555cc-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="555cc-515">Tabella Web</span><span class="sxs-lookup"><span data-stu-id="555cc-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="555cc-516">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-517">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-517">Linked service</span></span>
<span data-ttu-id="555cc-518">Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="555cc-519">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="555cc-520">Per collegare un account di Archiviazione di Azure a una data factory tramite la **chiave dell'account**, creare un servizio collegato di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="555cc-521">Per definire un servizio collegato di Archiviazione di Azure, impostare il **tipo** di servizio collegato su **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="555cc-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="555cc-522">Specificare quindi le seguenti proprietà nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-523">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-523">Property</span></span> | <span data-ttu-id="555cc-524">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-524">Description</span></span> | <span data-ttu-id="555cc-525">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-526">connectionString</span></span> |<span data-ttu-id="555cc-527">Specificare le informazioni necessarie per connettersi all’archivio Azure per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="555cc-528">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="555cc-529">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="555cc-530">Servizio collegato di firma di accesso condiviso Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="555cc-531">Il servizio collegato di firma di accesso condiviso Archiviazione di Azure consente di collegare un account di Archiviazione di Azure a Data factory di Azure tramite una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="555cc-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="555cc-532">Offre a Data factory un accesso con restrizioni o limiti di tempo a tutte le risorse o a risorse specifiche (BLOB/contenitore) nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="555cc-533">Per collegare un account di Archiviazione di Azure a una data factory tramite la firma di accesso condiviso, creare un servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="555cc-534">Per definire un Servizio collegato di firma di accesso condiviso Archiviazione di Azure, impostare il **tipo** del servizio collegato su **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="555cc-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="555cc-535">Specificare quindi le seguenti proprietà nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="555cc-536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-536">Property</span></span> | <span data-ttu-id="555cc-537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-537">Description</span></span> | <span data-ttu-id="555cc-538">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="555cc-539">sasUri</span></span> |<span data-ttu-id="555cc-540">Specificare l'URI della firma di accesso condiviso per le risorse di Archiviazione di Azure come BLOB, contenitore o tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="555cc-541">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="555cc-542">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="555cc-543">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione BLOB di Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-544">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-544">Dataset</span></span>
<span data-ttu-id="555cc-545">Per definire un set di dati BLOB di Azure, impostare il **tipo** del set di dati su **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="555cc-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="555cc-546">Specificare quindi le proprietà seguenti specifiche del BLOB di Azure nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-547">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-547">Property</span></span> | <span data-ttu-id="555cc-548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-548">Description</span></span> | <span data-ttu-id="555cc-549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-550">folderPath</span></span> |<span data-ttu-id="555cc-551">Percorso del contenitore e della cartella nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="555cc-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="555cc-552">Esempio: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="555cc-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="555cc-553">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-553">Yes</span></span> |
| <span data-ttu-id="555cc-554">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-554">fileName</span></span> |<span data-ttu-id="555cc-555">Nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="555cc-555">Name of the blob.</span></span> <span data-ttu-id="555cc-556">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="555cc-557">Se si specifica un filename, l'attività, inclusa la copia, funziona sul BLOB specifico.</span><span class="sxs-lookup"><span data-stu-id="555cc-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="555cc-558">Quando fileName non è specificato, la copia include tutti i BLOB in folderPath per il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="555cc-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="555cc-559">Quando fileName non viene specificato per un set di dati di output, il nome del file generato avrà il formato seguente: Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="555cc-560">No</span><span class="sxs-lookup"><span data-stu-id="555cc-560">No</span></span> |
| <span data-ttu-id="555cc-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-561">partitionedBy</span></span> |<span data-ttu-id="555cc-562">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="555cc-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="555cc-563">Può essere utilizzata per specificare una proprietà folderPath dinamica e un nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="555cc-564">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="555cc-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-565">No</span><span class="sxs-lookup"><span data-stu-id="555cc-565">No</span></span> |
| <span data-ttu-id="555cc-566">format</span><span class="sxs-lookup"><span data-stu-id="555cc-566">format</span></span> | <span data-ttu-id="555cc-567">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-568">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-569">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-570">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-571">No</span><span class="sxs-lookup"><span data-stu-id="555cc-571">No</span></span> |
| <span data-ttu-id="555cc-572">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-572">compression</span></span> | <span data-ttu-id="555cc-573">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-574">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-575">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-576">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-577">No</span><span class="sxs-lookup"><span data-stu-id="555cc-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-578">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-578">Example</span></span>

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


<span data-ttu-id="555cc-579">Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="555cc-580">BlobSource in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="555cc-581">Se si copiano dati da Archiviazione BLOB di Azure, impostare il **tipo di origine** dell'attività di copia su **BlobSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="555cc-582">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-582">Property</span></span> | <span data-ttu-id="555cc-583">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-583">Description</span></span> | <span data-ttu-id="555cc-584">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-584">Allowed values</span></span> | <span data-ttu-id="555cc-585">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-586">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-586">recursive</span></span> |<span data-ttu-id="555cc-587">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-588">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="555cc-588">True (default value), False</span></span> |<span data-ttu-id="555cc-589">No</span><span class="sxs-lookup"><span data-stu-id="555cc-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="555cc-590">Esempio: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="555cc-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="555cc-591">BlobSink in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="555cc-592">Se si copiano dati in Archiviazione BLOB di Azure, impostare il **tipo di sink** dell'attività di copia su **BlobSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-593">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-593">Property</span></span> | <span data-ttu-id="555cc-594">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-594">Description</span></span> | <span data-ttu-id="555cc-595">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-595">Allowed values</span></span> | <span data-ttu-id="555cc-596">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="555cc-597">copyBehavior</span></span> |<span data-ttu-id="555cc-598">Definisce il comportamento di copia quando l'origine è BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="555cc-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="555cc-599"><b>PreserveHierarchy:</b> mantiene la gerarchia dei file nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="555cc-600">Il percorso relativo del file di origine nella cartella di origine è identico al percorso relativo del file di destinazione nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="555cc-601"><b>FlattenHierarchy</b>: tutti i file della cartella di origine si trovano nel primo livello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="555cc-602">Il nome dei file di destinazione viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="555cc-603"><b>MergeFiles (valore predefinito)</b>: unisce tutti i file della cartella di origine in un solo file.</span><span class="sxs-lookup"><span data-stu-id="555cc-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="555cc-604">Se viene specificato il nome file/BLOB, il nome file unito sarà il nome specificato. In caso contrario, sarà il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="555cc-605">No</span><span class="sxs-lookup"><span data-stu-id="555cc-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="555cc-606">Esempio: BlobSink</span><span class="sxs-lookup"><span data-stu-id="555cc-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-607">Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="555cc-608">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="555cc-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-609">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-609">Linked service</span></span>
<span data-ttu-id="555cc-610">Per definire un servizio collegato di Azure Data Lake Store, impostare il tipo di servizio collegato su **AzureDataLakeStore** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-611">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-611">Property</span></span> | <span data-ttu-id="555cc-612">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-612">Description</span></span> | <span data-ttu-id="555cc-613">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-614">type</span><span class="sxs-lookup"><span data-stu-id="555cc-614">type</span></span> | <span data-ttu-id="555cc-615">La proprietà type deve essere impostata su: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="555cc-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="555cc-616">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-616">Yes</span></span> |
| <span data-ttu-id="555cc-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="555cc-617">dataLakeStoreUri</span></span> | <span data-ttu-id="555cc-618">Specificare le informazioni sull'account Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="555cc-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="555cc-619">Ha il formato seguente: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="555cc-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="555cc-620">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-620">Yes</span></span> |
| <span data-ttu-id="555cc-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="555cc-621">subscriptionId</span></span> | <span data-ttu-id="555cc-622">ID sottoscrizione di Azure a cui il Data Lake Store appartiene.</span><span class="sxs-lookup"><span data-stu-id="555cc-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="555cc-623">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="555cc-623">Required for sink</span></span> |
| <span data-ttu-id="555cc-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="555cc-624">resourceGroupName</span></span> | <span data-ttu-id="555cc-625">Nome del gruppo di risorse di Azure a cui il Data Lake Store appartiene.</span><span class="sxs-lookup"><span data-stu-id="555cc-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="555cc-626">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="555cc-626">Required for sink</span></span> |
| <span data-ttu-id="555cc-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="555cc-627">servicePrincipalId</span></span> | <span data-ttu-id="555cc-628">Specificare l'ID client dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-628">Specify the application's client ID.</span></span> | <span data-ttu-id="555cc-629">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="555cc-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="555cc-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="555cc-630">servicePrincipalKey</span></span> | <span data-ttu-id="555cc-631">Specificare la chiave dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-631">Specify the application's key.</span></span> | <span data-ttu-id="555cc-632">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="555cc-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="555cc-633">tenant</span><span class="sxs-lookup"><span data-stu-id="555cc-633">tenant</span></span> | <span data-ttu-id="555cc-634">Specificare le informazioni sul tenant (nome di dominio o ID tenant) in cui si trova l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="555cc-635">È possibile recuperarlo passando il cursore del mouse sull'angolo superiore destro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="555cc-636">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="555cc-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="555cc-637">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="555cc-637">authorization</span></span> | <span data-ttu-id="555cc-638">Fare clic sul pulsante **Autorizza** nell'**editor di Data Factory** e immettere le credenziali per assegnare l'URL di autorizzazione generato automaticamente a questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="555cc-639">Sì (per l'autenticazione basata su credenziali utente)</span><span class="sxs-lookup"><span data-stu-id="555cc-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="555cc-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="555cc-640">sessionId</span></span> | <span data-ttu-id="555cc-641">ID sessione OAuth dalla sessione di autorizzazione oauth.</span><span class="sxs-lookup"><span data-stu-id="555cc-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="555cc-642">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="555cc-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="555cc-643">Questa impostazione viene generata automaticamente quando si usa l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="555cc-644">Sì (per l'autenticazione basata su credenziali utente)</span><span class="sxs-lookup"><span data-stu-id="555cc-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="555cc-645">Esempio: uso dell'autenticazione basata su entità servizio</span><span class="sxs-lookup"><span data-stu-id="555cc-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="555cc-646">Esempio: uso dell'autenticazione basata su credenziali utente</span><span class="sxs-lookup"><span data-stu-id="555cc-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="555cc-647">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-648">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-648">Dataset</span></span>
<span data-ttu-id="555cc-649">Per definire un set di dati Azure Data Lake Store, impostare il **tipo** del set di dati **AzureDataLakeStore**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-650">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-650">Property</span></span> | <span data-ttu-id="555cc-651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-651">Description</span></span> | <span data-ttu-id="555cc-652">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-653">folderPath</span></span> |<span data-ttu-id="555cc-654">Percorso del contenitore e della cartella nell'Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="555cc-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="555cc-655">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-655">Yes</span></span> |
| <span data-ttu-id="555cc-656">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-656">fileName</span></span> |<span data-ttu-id="555cc-657">Il nome del file in fileName nell'archivio di Azure Data Lake è facoltativo e distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="555cc-658">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="555cc-659">Se si specifica un filename, l'attività, inclusa la copia, funziona sul file specifico.</span><span class="sxs-lookup"><span data-stu-id="555cc-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="555cc-660">Quando fileName non è specificato, la copia include tutti i file in folderPath per il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="555cc-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="555cc-661">Quando fileName non viene specificato per un set di dati di output, il nome del file generato avrà il formato seguente: Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="555cc-662">No</span><span class="sxs-lookup"><span data-stu-id="555cc-662">No</span></span> |
| <span data-ttu-id="555cc-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-663">partitionedBy</span></span> |<span data-ttu-id="555cc-664">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="555cc-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="555cc-665">Può essere utilizzata per specificare una proprietà folderPath dinamica e un nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="555cc-666">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="555cc-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-667">No</span><span class="sxs-lookup"><span data-stu-id="555cc-667">No</span></span> |
| <span data-ttu-id="555cc-668">format</span><span class="sxs-lookup"><span data-stu-id="555cc-668">format</span></span> | <span data-ttu-id="555cc-669">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-670">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-671">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-672">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-673">No</span><span class="sxs-lookup"><span data-stu-id="555cc-673">No</span></span> |
| <span data-ttu-id="555cc-674">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-674">compression</span></span> | <span data-ttu-id="555cc-675">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-676">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-677">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-678">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-679">No</span><span class="sxs-lookup"><span data-stu-id="555cc-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-680">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-681">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="555cc-682">Origine Azure Data Lake Store in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="555cc-683">Se si copiano dati da Azure Data Lake Store, impostare il **tipo di origine** dell'attività di copia su **AzureDataLakeStoreSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="555cc-684">**AzureDataLakeStoreSource** supporta le proprietà seguenti della sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="555cc-685">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-685">Property</span></span> | <span data-ttu-id="555cc-686">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-686">Description</span></span> | <span data-ttu-id="555cc-687">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-687">Allowed values</span></span> | <span data-ttu-id="555cc-688">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-689">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-689">recursive</span></span> |<span data-ttu-id="555cc-690">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-691">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="555cc-691">True (default value), False</span></span> |<span data-ttu-id="555cc-692">No</span><span class="sxs-lookup"><span data-stu-id="555cc-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="555cc-693">Esempio: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="555cc-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-694">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="555cc-695">Sink Azure Data Lake Store in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-696">Se si copiano dati in Azure Data Lake Store, impostare il **tipo di sink**  dell'attività di copia su **AzureDataLakeStoreSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-697">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-697">Property</span></span> | <span data-ttu-id="555cc-698">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-698">Description</span></span> | <span data-ttu-id="555cc-699">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-699">Allowed values</span></span> | <span data-ttu-id="555cc-700">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="555cc-701">copyBehavior</span></span> |<span data-ttu-id="555cc-702">Specifica il comportamento di copia.</span><span class="sxs-lookup"><span data-stu-id="555cc-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="555cc-703"><b>PreserveHierarchy:</b> mantiene la gerarchia dei file nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="555cc-704">Il percorso relativo del file di origine nella cartella di origine è identico al percorso relativo del file di destinazione nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="555cc-705"><b>FlattenHierarchy</b>: tutti i file della cartella di origine vengono creati nel primo livello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="555cc-706">Il nome dei file di destinazione viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="555cc-707"><b>MergeFiles</b>: unisce tutti i file della cartella di origine in un solo file.</span><span class="sxs-lookup"><span data-stu-id="555cc-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="555cc-708">Se viene specificato il nome file/BLOB, il nome file unito sarà il nome specificato. In caso contrario, sarà il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="555cc-709">No</span><span class="sxs-lookup"><span data-stu-id="555cc-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="555cc-710">Esempio: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="555cc-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-711">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="555cc-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="555cc-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="555cc-713">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-713">Linked service</span></span>
<span data-ttu-id="555cc-714">Per definire un servizio collegato di Azure Cosmos DB, impostare il **tipo** di servizio collegato su **DocumentDb** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-715">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="555cc-715">**Property**</span></span> | <span data-ttu-id="555cc-716">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="555cc-716">**Description**</span></span> | <span data-ttu-id="555cc-717">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="555cc-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-718">connectionString</span></span> |<span data-ttu-id="555cc-719">Specificare le informazioni necessarie per connettersi al database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="555cc-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="555cc-720">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-721">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="555cc-722">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-723">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-723">Dataset</span></span>
<span data-ttu-id="555cc-724">Per definire un set di dati Azure Cosmos DB, impostare il **tipo** di set di dati su **DocumentDbCollection**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-725">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="555cc-725">**Property**</span></span> | <span data-ttu-id="555cc-726">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="555cc-726">**Description**</span></span> | <span data-ttu-id="555cc-727">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="555cc-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="555cc-728">collectionName</span></span> |<span data-ttu-id="555cc-729">Nome della raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="555cc-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="555cc-730">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-731">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="555cc-732">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="555cc-733">Origine della raccolta Azure Cosmos DB in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="555cc-734">Se si copiano dati da un archivio Azure Cosmos DB, impostare il **tipo di origine** dell'attività di copia su **DocumentDbCollectionSource** e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-735">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="555cc-735">**Property**</span></span> | <span data-ttu-id="555cc-736">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="555cc-736">**Description**</span></span> | <span data-ttu-id="555cc-737">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="555cc-737">**Allowed values**</span></span> | <span data-ttu-id="555cc-738">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="555cc-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-739">query</span><span class="sxs-lookup"><span data-stu-id="555cc-739">query</span></span> |<span data-ttu-id="555cc-740">Specificare la query per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-740">Specify the query to read data.</span></span> |<span data-ttu-id="555cc-741">Stringa di query supportata da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="555cc-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="555cc-742">Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="555cc-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="555cc-743">No</span><span class="sxs-lookup"><span data-stu-id="555cc-743">No</span></span> <br/><br/><span data-ttu-id="555cc-744">Se non specificato, l'istruzione SQL eseguita: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="555cc-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="555cc-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="555cc-745">nestingSeparator</span></span> |<span data-ttu-id="555cc-746">Carattere speciale per indicare che il documento è nidificato</span><span class="sxs-lookup"><span data-stu-id="555cc-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="555cc-747">Qualsiasi carattere.</span><span class="sxs-lookup"><span data-stu-id="555cc-747">Any character.</span></span> <br/><br/><span data-ttu-id="555cc-748">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="555cc-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="555cc-749">Azure Data Factory consente di indicare una gerarchia tramite nestingSeparator, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="555cc-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="555cc-750">negli esempi precedenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-750">in the above examples.</span></span> <span data-ttu-id="555cc-751">Con il separatore, l'attività copia genererà l'oggetto "Name" con tre elementi figlio First, Middle e Last, in base a "Name.First", "Name.Middle" e "Name.Last" nella definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="555cc-752">No</span><span class="sxs-lookup"><span data-stu-id="555cc-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-753">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="555cc-754">Sink della raccolta Azure Cosmos DB in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-755">Se si copiano dati in Azure Cosmos DB, impostare il **tipo di sink** dell'attività di copia su **DocumentDbCollectionSink** e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-756">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="555cc-756">**Property**</span></span> | <span data-ttu-id="555cc-757">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="555cc-757">**Description**</span></span> | <span data-ttu-id="555cc-758">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="555cc-758">**Allowed values**</span></span> | <span data-ttu-id="555cc-759">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="555cc-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="555cc-760">nestingSeparator</span></span> |<span data-ttu-id="555cc-761">È necessario un carattere speciale nel nome della colonna di origine per indicare tale documento nidificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="555cc-762">Per l'esempio sopra: `Name.First` nella tabella di output produce la struttura JSON seguente nel documento di Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="555cc-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="555cc-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="555cc-763">"Name": {</span></span><br/>    <span data-ttu-id="555cc-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="555cc-764">"First": "John"</span></span><br/><span data-ttu-id="555cc-765">},</span><span class="sxs-lookup"><span data-stu-id="555cc-765">},</span></span> |<span data-ttu-id="555cc-766">Carattere utilizzato per separare i livelli di nidificazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="555cc-767">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="555cc-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="555cc-768">Carattere utilizzato per separare i livelli di nidificazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="555cc-769">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="555cc-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="555cc-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-770">writeBatchSize</span></span> |<span data-ttu-id="555cc-771">Numero di richieste in parallelo per il servizio Azure Cosmos DB per creare documenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="555cc-772">È possibile ottimizzare le prestazioni quando si copiano dati da e verso Azure Cosmos DB usando questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="555cc-773">È possibile prevedere prestazioni migliori quando si aumenta writeBatchSize, poiché vengono inviate più richieste in parallelo a Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="555cc-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="555cc-774">Tuttavia è necessario evitare la limitazione che può generare il messaggio di errore: "La frequenza delle richieste è troppo elevata".</span><span class="sxs-lookup"><span data-stu-id="555cc-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="555cc-775">La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile usare una raccolta migliore (ad esempio, S3) per poter disporre della maggiore velocità effettiva possibile (2.500 unità richieste al secondo).</span><span class="sxs-lookup"><span data-stu-id="555cc-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="555cc-776">Integer</span><span class="sxs-lookup"><span data-stu-id="555cc-776">Integer</span></span> |<span data-ttu-id="555cc-777">No (valore predefinito: 5)</span><span class="sxs-lookup"><span data-stu-id="555cc-777">No (default: 5)</span></span> |
| <span data-ttu-id="555cc-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-778">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-779">Tempo di attesa per il completamento dell’operazione prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="555cc-780">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-780">timespan</span></span><br/><br/> <span data-ttu-id="555cc-781">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="555cc-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="555cc-782">No</span><span class="sxs-lookup"><span data-stu-id="555cc-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-783">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="555cc-784">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="555cc-785">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-786">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-786">Linked service</span></span>
<span data-ttu-id="555cc-787">Per definire un servizio collegato di Database SQL di Azure, impostare il **tipo** di servizio collegato su **AzureSqlDatabase**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-788">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-788">Property</span></span> | <span data-ttu-id="555cc-789">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-789">Description</span></span> | <span data-ttu-id="555cc-790">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-791">connectionString</span></span> |<span data-ttu-id="555cc-792">Specificare le informazioni necessarie per connettersi all'istanza di database SQL di Azure per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="555cc-793">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-794">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="555cc-795">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-796">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-796">Dataset</span></span>
<span data-ttu-id="555cc-797">Per definire un set di dati del Database SQL di Azure, impostare il **tipo** di set di dati su **AzureSqlTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-798">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-798">Property</span></span> | <span data-ttu-id="555cc-799">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-799">Description</span></span> | <span data-ttu-id="555cc-800">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-801">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-801">tableName</span></span> |<span data-ttu-id="555cc-802">Nome della tabella o vista nell'istanza di database SQL di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="555cc-803">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-804">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="555cc-805">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="555cc-806">Origine SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="555cc-807">Se si copiano dati da un database SQL di Azure, impostare il **tipo di origine** dell'attività di copia su **SqlSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-808">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-808">Property</span></span> | <span data-ttu-id="555cc-809">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-809">Description</span></span> | <span data-ttu-id="555cc-810">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-810">Allowed values</span></span> | <span data-ttu-id="555cc-811">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="555cc-812">sqlReaderQuery</span></span> |<span data-ttu-id="555cc-813">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-813">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-814">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-814">SQL query string.</span></span> <span data-ttu-id="555cc-815">Esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-816">No</span><span class="sxs-lookup"><span data-stu-id="555cc-816">No</span></span> |
| <span data-ttu-id="555cc-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="555cc-818">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="555cc-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="555cc-819">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-819">Name of the stored procedure.</span></span> |<span data-ttu-id="555cc-820">No</span><span class="sxs-lookup"><span data-stu-id="555cc-820">No</span></span> |
| <span data-ttu-id="555cc-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-821">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-822">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="555cc-823">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="555cc-823">Name/value pairs.</span></span> <span data-ttu-id="555cc-824">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="555cc-825">No</span><span class="sxs-lookup"><span data-stu-id="555cc-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-826">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="555cc-827">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="555cc-828">Sink SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-829">Se si copiano dati in un database SQL di Azure, impostare il **tipo di sink** dell'attività di copia su **SqlSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-830">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-830">Property</span></span> | <span data-ttu-id="555cc-831">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-831">Description</span></span> | <span data-ttu-id="555cc-832">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-832">Allowed values</span></span> | <span data-ttu-id="555cc-833">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-834">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-835">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="555cc-836">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-836">timespan</span></span><br/><br/> <span data-ttu-id="555cc-837">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="555cc-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="555cc-838">No</span><span class="sxs-lookup"><span data-stu-id="555cc-838">No</span></span> |
| <span data-ttu-id="555cc-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-839">writeBatchSize</span></span> |<span data-ttu-id="555cc-840">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="555cc-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="555cc-841">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="555cc-841">Integer (number of rows)</span></span> |<span data-ttu-id="555cc-842">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="555cc-842">No (default: 10000)</span></span> |
| <span data-ttu-id="555cc-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="555cc-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="555cc-844">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="555cc-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="555cc-845">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="555cc-845">A query statement.</span></span> |<span data-ttu-id="555cc-846">No</span><span class="sxs-lookup"><span data-stu-id="555cc-846">No</span></span> |
| <span data-ttu-id="555cc-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="555cc-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="555cc-848">Specificare il nome di una colonna in cui inserire nell'attività di copia l'identificatore di sezione generato automaticamente che verrà usato per pulire i dati di una sezione specifica quando viene ripetuta l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="555cc-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="555cc-849">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="555cc-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="555cc-850">No</span><span class="sxs-lookup"><span data-stu-id="555cc-850">No</span></span> |
| <span data-ttu-id="555cc-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="555cc-852">Nome della stored procedure che esegue l'upsert (aggiornamenti/inserimenti) nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="555cc-853">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-853">Name of the stored procedure.</span></span> |<span data-ttu-id="555cc-854">No</span><span class="sxs-lookup"><span data-stu-id="555cc-854">No</span></span> |
| <span data-ttu-id="555cc-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-855">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-856">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="555cc-857">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="555cc-857">Name/value pairs.</span></span> <span data-ttu-id="555cc-858">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="555cc-859">No</span><span class="sxs-lookup"><span data-stu-id="555cc-859">No</span></span> |
| <span data-ttu-id="555cc-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="555cc-860">sqlWriterTableType</span></span> |<span data-ttu-id="555cc-861">Specificare il nome di un tipo di tabella da usare nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="555cc-862">L'attività di copia rende i dati spostati disponibili in una tabella temporanea con questo tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="555cc-863">Il codice della stored procedure può quindi unire i dati copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="555cc-864">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-864">A table type name.</span></span> |<span data-ttu-id="555cc-865">No</span><span class="sxs-lookup"><span data-stu-id="555cc-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-866">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-867">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="555cc-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-869">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-869">Linked service</span></span>
<span data-ttu-id="555cc-870">Per definire un servizio collegato di Azure SQL Data Warehouse, impostare il **tipo** di servizio collegato su **AzureSqlDW**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-871">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-871">Property</span></span> | <span data-ttu-id="555cc-872">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-872">Description</span></span> | <span data-ttu-id="555cc-873">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-874">connectionString</span></span> |<span data-ttu-id="555cc-875">Specificare le informazioni necessarie per connettersi all'istanza di Azure SQL Data Warehouse per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="555cc-876">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="555cc-877">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="555cc-878">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-879">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-879">Dataset</span></span>
<span data-ttu-id="555cc-880">Per definire un set di dati di Azure SQL Data Warehouse, impostare il **tipo** di set di dati su **AzureSqlDWTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-881">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-881">Property</span></span> | <span data-ttu-id="555cc-882">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-882">Description</span></span> | <span data-ttu-id="555cc-883">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-884">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-884">tableName</span></span> |<span data-ttu-id="555cc-885">Nome della tabella o della visualizzazione nell'istanza del database SQL Data Warehouse di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="555cc-886">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-887">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-888">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="555cc-889">Origine SQL DW nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="555cc-890">Se si copiano dati da un Azure SQL Data Warehouse, impostare il **tipo di origine** dell'attività di copia su **SqlDWSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-891">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-891">Property</span></span> | <span data-ttu-id="555cc-892">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-892">Description</span></span> | <span data-ttu-id="555cc-893">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-893">Allowed values</span></span> | <span data-ttu-id="555cc-894">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="555cc-895">sqlReaderQuery</span></span> |<span data-ttu-id="555cc-896">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-896">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-897">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-897">SQL query string.</span></span> <span data-ttu-id="555cc-898">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-899">No</span><span class="sxs-lookup"><span data-stu-id="555cc-899">No</span></span> |
| <span data-ttu-id="555cc-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="555cc-901">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="555cc-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="555cc-902">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-902">Name of the stored procedure.</span></span> |<span data-ttu-id="555cc-903">No</span><span class="sxs-lookup"><span data-stu-id="555cc-903">No</span></span> |
| <span data-ttu-id="555cc-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-904">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-905">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="555cc-906">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="555cc-906">Name/value pairs.</span></span> <span data-ttu-id="555cc-907">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="555cc-908">No</span><span class="sxs-lookup"><span data-stu-id="555cc-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-909">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-910">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="555cc-911">Sink SQL DW nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-912">Se si copiano dati in un Azure SQL Data Warehouse, impostare il **tipo di sink** dell'attività di copia su **SqlDWSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-913">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-913">Property</span></span> | <span data-ttu-id="555cc-914">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-914">Description</span></span> | <span data-ttu-id="555cc-915">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-915">Allowed values</span></span> | <span data-ttu-id="555cc-916">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="555cc-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="555cc-918">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="555cc-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="555cc-919">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="555cc-919">A query statement.</span></span> |<span data-ttu-id="555cc-920">No</span><span class="sxs-lookup"><span data-stu-id="555cc-920">No</span></span> |
| <span data-ttu-id="555cc-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="555cc-921">allowPolyBase</span></span> |<span data-ttu-id="555cc-922">Indica se usare PolyBase, quando applicabile, invece del meccanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="555cc-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="555cc-923">**L'uso di PolyBase è il modo consigliato per caricare dati in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="555cc-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="555cc-924">True </span><span class="sxs-lookup"><span data-stu-id="555cc-924">True</span></span> <br/><span data-ttu-id="555cc-925">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="555cc-925">False (default)</span></span> |<span data-ttu-id="555cc-926">No</span><span class="sxs-lookup"><span data-stu-id="555cc-926">No</span></span> |
| <span data-ttu-id="555cc-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="555cc-927">polyBaseSettings</span></span> |<span data-ttu-id="555cc-928">Gruppo di proprietà che è possibile specificare quando la proprietà **allowPolybase** è impostata su **true**.</span><span class="sxs-lookup"><span data-stu-id="555cc-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="555cc-929">No</span><span class="sxs-lookup"><span data-stu-id="555cc-929">No</span></span> |
| <span data-ttu-id="555cc-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="555cc-930">rejectValue</span></span> |<span data-ttu-id="555cc-931">Specifica il numero o la percentuale di righe che è possibile rifiutare prima che la query abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="555cc-932">Per altre informazioni sulle opzioni di rifiuto di PolyBase, vedere la sezione **Arguments** (Argomenti) in [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) .</span><span class="sxs-lookup"><span data-stu-id="555cc-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="555cc-933">0 (impostazione predefinita), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="555cc-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="555cc-934">No</span><span class="sxs-lookup"><span data-stu-id="555cc-934">No</span></span> |
| <span data-ttu-id="555cc-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="555cc-935">rejectType</span></span> |<span data-ttu-id="555cc-936">Indica se l'opzione rejectValue viene specificata come valore letterale o come percentuale.</span><span class="sxs-lookup"><span data-stu-id="555cc-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="555cc-937">Value (impostazione predefinita), Percentage</span><span class="sxs-lookup"><span data-stu-id="555cc-937">Value (default), Percentage</span></span> |<span data-ttu-id="555cc-938">No</span><span class="sxs-lookup"><span data-stu-id="555cc-938">No</span></span> |
| <span data-ttu-id="555cc-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="555cc-939">rejectSampleValue</span></span> |<span data-ttu-id="555cc-940">Determina il numero di righe da recuperare prima che PolyBase ricalcoli la percentuale di righe rifiutate.</span><span class="sxs-lookup"><span data-stu-id="555cc-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="555cc-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="555cc-941">1, 2, …</span></span> |<span data-ttu-id="555cc-942">Sì se **rejectType** è **percentage**</span><span class="sxs-lookup"><span data-stu-id="555cc-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="555cc-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="555cc-943">useTypeDefault</span></span> |<span data-ttu-id="555cc-944">Specifica come gestire i valori mancanti nei file con testo delimitato quando PolyBase recupera dati dal file di testo.</span><span class="sxs-lookup"><span data-stu-id="555cc-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="555cc-945">Per altre informazioni su questa proprietà, vedere la sezione Arguments (Argomenti) in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="555cc-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="555cc-946">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-946">True, False (default)</span></span> |<span data-ttu-id="555cc-947">No</span><span class="sxs-lookup"><span data-stu-id="555cc-947">No</span></span> |
| <span data-ttu-id="555cc-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-948">writeBatchSize</span></span> |<span data-ttu-id="555cc-949">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="555cc-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="555cc-950">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="555cc-950">Integer (number of rows)</span></span> |<span data-ttu-id="555cc-951">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="555cc-951">No (default: 10000)</span></span> |
| <span data-ttu-id="555cc-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-952">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-953">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="555cc-954">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-954">timespan</span></span><br/><br/> <span data-ttu-id="555cc-955">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="555cc-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="555cc-956">No</span><span class="sxs-lookup"><span data-stu-id="555cc-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-957">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-958">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="555cc-959">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-960">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-960">Linked service</span></span>
<span data-ttu-id="555cc-961">Per definire un servizio collegato di Ricerca di Azure, impostare il **tipo** di servizio collegato su **AzureSearch** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-962">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-962">Property</span></span> | <span data-ttu-id="555cc-963">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-963">Description</span></span> | <span data-ttu-id="555cc-964">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="555cc-965">URL</span><span class="sxs-lookup"><span data-stu-id="555cc-965">url</span></span> | <span data-ttu-id="555cc-966">URL del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="555cc-967">sì</span><span class="sxs-lookup"><span data-stu-id="555cc-967">Yes</span></span> |
| <span data-ttu-id="555cc-968">key</span><span class="sxs-lookup"><span data-stu-id="555cc-968">key</span></span> | <span data-ttu-id="555cc-969">Chiave amministratore del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="555cc-970">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-971">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="555cc-972">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-973">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-973">Dataset</span></span>
<span data-ttu-id="555cc-974">Per definire un set di dati di Ricerca di Azure, impostare il **tipo** di set di dati su **AzureSearchIndex** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-975">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-975">Property</span></span> | <span data-ttu-id="555cc-976">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-976">Description</span></span> | <span data-ttu-id="555cc-977">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="555cc-978">type</span><span class="sxs-lookup"><span data-stu-id="555cc-978">type</span></span> | <span data-ttu-id="555cc-979">La proprietà type deve essere impostata su **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="555cc-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="555cc-980">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-980">Yes</span></span> |
| <span data-ttu-id="555cc-981">indexName</span><span class="sxs-lookup"><span data-stu-id="555cc-981">indexName</span></span> | <span data-ttu-id="555cc-982">Nome dell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-982">Name of the Azure Search index.</span></span> <span data-ttu-id="555cc-983">Il servizio Data Factory non crea l'indice.</span><span class="sxs-lookup"><span data-stu-id="555cc-983">Data Factory does not create the index.</span></span> <span data-ttu-id="555cc-984">L'indice deve essere presente in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="555cc-985">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-986">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="555cc-987">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="555cc-988">Sink Indice di Ricerca di Azure in attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-989">Se si copiano dati in un indice di Ricerca di Azure, impostare il **tipo di sink**  dell'attività di copia su **AzureSearchIndexSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-990">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-990">Property</span></span> | <span data-ttu-id="555cc-991">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-991">Description</span></span> | <span data-ttu-id="555cc-992">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-992">Allowed values</span></span> | <span data-ttu-id="555cc-993">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="555cc-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="555cc-994">WriteBehavior</span></span> | <span data-ttu-id="555cc-995">Specifica se eseguire un'unione o una sostituzione quando nell'indice esiste già un documento.</span><span class="sxs-lookup"><span data-stu-id="555cc-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="555cc-996">Merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="555cc-996">Merge (default)</span></span><br/><span data-ttu-id="555cc-997">Carica</span><span class="sxs-lookup"><span data-stu-id="555cc-997">Upload</span></span>| <span data-ttu-id="555cc-998">No</span><span class="sxs-lookup"><span data-stu-id="555cc-998">No</span></span> |
| <span data-ttu-id="555cc-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-999">WriteBatchSize</span></span> | <span data-ttu-id="555cc-1000">Consente di caricare dati nell'indice di Ricerca di Azure quando le dimensioni del buffer raggiungono il valore indicato da writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="555cc-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="555cc-1001">Da 1 a 1000.</span><span class="sxs-lookup"><span data-stu-id="555cc-1001">1 to 1,000.</span></span> <span data-ttu-id="555cc-1002">Il valore predefinito è 1000.</span><span class="sxs-lookup"><span data-stu-id="555cc-1002">Default value is 1000.</span></span> | <span data-ttu-id="555cc-1003">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1004">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1005">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="555cc-1006">Archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1007">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1007">Linked service</span></span>
<span data-ttu-id="555cc-1008">Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="555cc-1009">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="555cc-1010">Per collegare un account di Archiviazione di Azure a una data factory tramite la **chiave dell'account**, creare un servizio collegato di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="555cc-1011">Per definire un servizio collegato di Archiviazione di Azure, impostare il **tipo** di servizio collegato su **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="555cc-1012">Specificare quindi le seguenti proprietà nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1013">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1013">Property</span></span> | <span data-ttu-id="555cc-1014">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1014">Description</span></span> | <span data-ttu-id="555cc-1015">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-1016">type</span><span class="sxs-lookup"><span data-stu-id="555cc-1016">type</span></span> |<span data-ttu-id="555cc-1017">La proprietà type deve essere impostata su: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="555cc-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="555cc-1018">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1018">Yes</span></span> |
| <span data-ttu-id="555cc-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-1019">connectionString</span></span> |<span data-ttu-id="555cc-1020">Specificare le informazioni necessarie per connettersi all’archivio Azure per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="555cc-1021">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1021">Yes</span></span> |

<span data-ttu-id="555cc-1022">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="555cc-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="555cc-1023">Servizio collegato di firma di accesso condiviso Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="555cc-1024">Il servizio collegato di firma di accesso condiviso Archiviazione di Azure consente di collegare un account di Archiviazione di Azure a Data factory di Azure tramite una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="555cc-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="555cc-1025">Offre a Data factory un accesso con restrizioni o limiti di tempo a tutte le risorse o a risorse specifiche (BLOB/contenitore) nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="555cc-1026">Per collegare un account di Archiviazione di Azure a una data factory tramite la firma di accesso condiviso, creare un servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="555cc-1027">Per definire un Servizio collegato di firma di accesso condiviso Archiviazione di Azure, impostare il **tipo** del servizio collegato su **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="555cc-1028">Specificare quindi le seguenti proprietà nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="555cc-1029">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1029">Property</span></span> | <span data-ttu-id="555cc-1030">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1030">Description</span></span> | <span data-ttu-id="555cc-1031">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-1032">type</span><span class="sxs-lookup"><span data-stu-id="555cc-1032">type</span></span> |<span data-ttu-id="555cc-1033">La proprietà type deve essere impostata su: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="555cc-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="555cc-1034">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1034">Yes</span></span> |
| <span data-ttu-id="555cc-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="555cc-1035">sasUri</span></span> |<span data-ttu-id="555cc-1036">Specificare l'URI della firma di accesso condiviso per le risorse di Archiviazione di Azure come BLOB, contenitore o tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="555cc-1037">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1037">Yes</span></span> |

<span data-ttu-id="555cc-1038">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="555cc-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="555cc-1039">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1040">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1040">Dataset</span></span>
<span data-ttu-id="555cc-1041">Per definire un set di dati di Archiviazione tabelle di Azure, impostare il **tipo** di set di dati su **AzureTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1042">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1042">Property</span></span> | <span data-ttu-id="555cc-1043">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1043">Description</span></span> | <span data-ttu-id="555cc-1044">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1045">tableName</span></span> |<span data-ttu-id="555cc-1046">Nome della tabella nell'istanza del database di tabelle di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="555cc-1047">Sì.</span><span class="sxs-lookup"><span data-stu-id="555cc-1047">Yes.</span></span> <span data-ttu-id="555cc-1048">Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="555cc-1049">Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1050">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1051">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="555cc-1052">Origine Tabella di Azure nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1053">Se si copiano dati dall'archiviazione tabelle di Azure, impostare il **tipo di origine** dell'attività di copia su **AzureTableSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1054">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1054">Property</span></span> | <span data-ttu-id="555cc-1055">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1055">Description</span></span> | <span data-ttu-id="555cc-1056">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1056">Allowed values</span></span> | <span data-ttu-id="555cc-1057">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="555cc-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="555cc-1059">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1060">Stringa di query della tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1060">Azure table query string.</span></span> <span data-ttu-id="555cc-1061">Vedere gli esempi nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="555cc-1061">See examples in the next section.</span></span> |<span data-ttu-id="555cc-1062">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-1062">No.</span></span> <span data-ttu-id="555cc-1063">Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="555cc-1064">Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="555cc-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="555cc-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="555cc-1066">Indica se ignorare l'eccezione di tabella inesistente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="555cc-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="555cc-1067">TRUE</span></span><br/><span data-ttu-id="555cc-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="555cc-1068">FALSE</span></span> |<span data-ttu-id="555cc-1069">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1070">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1071">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="555cc-1072">Sink Tabella di Azure nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-1073">Se si copiano dati in un'archiviazione tabelle di Azure, impostare il **tipo di sink** dell'attività di copia su **AzureTableSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-1074">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1074">Property</span></span> | <span data-ttu-id="555cc-1075">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1075">Description</span></span> | <span data-ttu-id="555cc-1076">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1076">Allowed values</span></span> | <span data-ttu-id="555cc-1077">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="555cc-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="555cc-1079">Valore predefinito della chiave di partizione che può essere usato dal sink.</span><span class="sxs-lookup"><span data-stu-id="555cc-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="555cc-1080">Valore stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-1080">A string value.</span></span> |<span data-ttu-id="555cc-1081">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1081">No</span></span> |
| <span data-ttu-id="555cc-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="555cc-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="555cc-1083">Specificare il nome della colonna i cui valori vengono usati come chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="555cc-1084">Se non specificato, AzureTableDefaultPartitionKeyValue viene usato come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="555cc-1085">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="555cc-1085">A column name.</span></span> |<span data-ttu-id="555cc-1086">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1086">No</span></span> |
| <span data-ttu-id="555cc-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="555cc-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="555cc-1088">Specificare il nome della colonna i cui valori vengono usati come chiavi di riga.</span><span class="sxs-lookup"><span data-stu-id="555cc-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="555cc-1089">Se non specificato, usare un GUID per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="555cc-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="555cc-1090">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="555cc-1090">A column name.</span></span> |<span data-ttu-id="555cc-1091">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1091">No</span></span> |
| <span data-ttu-id="555cc-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="555cc-1092">azureTableInsertType</span></span> |<span data-ttu-id="555cc-1093">Modalità di inserimento dei dati in una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="555cc-1094">Questa proprietà verifica se per le righe esistenti nella tabella di output con chiavi di partizione e di riga corrispondenti i valori vengono sostituiti o uniti.</span><span class="sxs-lookup"><span data-stu-id="555cc-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="555cc-1095">Per scoprire come funzionano queste impostazioni (unione e sostituzione), vedere gli argomenti [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Inserire o unire un'entità) e [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Inserire o sostituire un'entità).</span><span class="sxs-lookup"><span data-stu-id="555cc-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="555cc-1096">Queste impostazioni vengono applicate a livello di riga, non a livello di tabella, e nessuna delle due opzioni elimina le righe della tabella di output che non esistono nell'input.</span><span class="sxs-lookup"><span data-stu-id="555cc-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="555cc-1097">merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="555cc-1097">merge (default)</span></span><br/><span data-ttu-id="555cc-1098">replace</span><span class="sxs-lookup"><span data-stu-id="555cc-1098">replace</span></span> |<span data-ttu-id="555cc-1099">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1099">No</span></span> |
| <span data-ttu-id="555cc-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-1100">writeBatchSize</span></span> |<span data-ttu-id="555cc-1101">Inserisce dati nella tabella di Azure quando viene raggiunto il writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="555cc-1102">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="555cc-1102">Integer (number of rows)</span></span> |<span data-ttu-id="555cc-1103">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="555cc-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="555cc-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-1104">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-1105">Inserisce i dati nella tabella di Azure quando viene raggiunto writeBatchSize o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="555cc-1106">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-1106">timespan</span></span><br/><br/><span data-ttu-id="555cc-1107">Ad esempio: "00:20:00" (20 minuti)</span><span class="sxs-lookup"><span data-stu-id="555cc-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="555cc-1108">No. (il valore predefinito è il timeout del client di archiviazione pari a 90 secondi)</span><span class="sxs-lookup"><span data-stu-id="555cc-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1109">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="555cc-1110">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="555cc-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="555cc-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1112">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1112">Linked service</span></span>
<span data-ttu-id="555cc-1113">Per definire un servizio collegato di Amazon Redshift, impostare il **tipo** di servizio collegato su **AmazonRedshift** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1114">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1114">Property</span></span> | <span data-ttu-id="555cc-1115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1115">Description</span></span> | <span data-ttu-id="555cc-1116">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1117">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1117">server</span></span> |<span data-ttu-id="555cc-1118">Indirizzo IP o nome host del server Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="555cc-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="555cc-1119">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1119">Yes</span></span> |
| <span data-ttu-id="555cc-1120">port</span><span class="sxs-lookup"><span data-stu-id="555cc-1120">port</span></span> |<span data-ttu-id="555cc-1121">Il numero della porta TCP che il server Amazon Redshift usa per ascoltare le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="555cc-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="555cc-1122">No, valore predefinito: 5439</span><span class="sxs-lookup"><span data-stu-id="555cc-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="555cc-1123">database</span><span class="sxs-lookup"><span data-stu-id="555cc-1123">database</span></span> |<span data-ttu-id="555cc-1124">Nome del database Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="555cc-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="555cc-1125">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1125">Yes</span></span> |
| <span data-ttu-id="555cc-1126">Nome utente</span><span class="sxs-lookup"><span data-stu-id="555cc-1126">username</span></span> |<span data-ttu-id="555cc-1127">Nome dell'utente che ha accesso al database.</span><span class="sxs-lookup"><span data-stu-id="555cc-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="555cc-1128">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1128">Yes</span></span> |
| <span data-ttu-id="555cc-1129">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1129">password</span></span> |<span data-ttu-id="555cc-1130">La password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1130">Password for the user account.</span></span> |<span data-ttu-id="555cc-1131">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1132">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="555cc-1133">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1134">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1134">Dataset</span></span>
<span data-ttu-id="555cc-1135">Per definire un set di dati di AmazonRedshift, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1136">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1136">Property</span></span> | <span data-ttu-id="555cc-1137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1137">Description</span></span> | <span data-ttu-id="555cc-1138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1139">tableName</span></span> |<span data-ttu-id="555cc-1140">Nome della tabella nel database Amazon Redshift a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="555cc-1141">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="555cc-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-1142">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="555cc-1143">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1144">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="555cc-1145">Se si copiano dati da Amazon Redshift, impostare il **tipo di origine** dell'attività di copia su **SqlRelationalSourceSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1146">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1146">Property</span></span> | <span data-ttu-id="555cc-1147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1147">Description</span></span> | <span data-ttu-id="555cc-1148">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1148">Allowed values</span></span> | <span data-ttu-id="555cc-1149">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1150">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1150">query</span></span> |<span data-ttu-id="555cc-1151">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1152">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1152">SQL query string.</span></span> <span data-ttu-id="555cc-1153">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-1154">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1155">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="555cc-1156">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="555cc-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="555cc-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1158">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1158">Linked service</span></span>
<span data-ttu-id="555cc-1159">Per definire un servizio collegato di IBM DB2, impostare il **tipo** di servizio collegato su **OnPremisesDB2** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1160">Property</span></span> | <span data-ttu-id="555cc-1161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1161">Description</span></span> | <span data-ttu-id="555cc-1162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1163">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1163">server</span></span> |<span data-ttu-id="555cc-1164">Nome del server DB2.</span><span class="sxs-lookup"><span data-stu-id="555cc-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="555cc-1165">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1165">Yes</span></span> |
| <span data-ttu-id="555cc-1166">database</span><span class="sxs-lookup"><span data-stu-id="555cc-1166">database</span></span> |<span data-ttu-id="555cc-1167">Nome del database DB2.</span><span class="sxs-lookup"><span data-stu-id="555cc-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="555cc-1168">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1168">Yes</span></span> |
| <span data-ttu-id="555cc-1169">schema</span><span class="sxs-lookup"><span data-stu-id="555cc-1169">schema</span></span> |<span data-ttu-id="555cc-1170">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="555cc-1170">Name of the schema in the database.</span></span> <span data-ttu-id="555cc-1171">Il nome dello schema fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="555cc-1172">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1172">No</span></span> |
| <span data-ttu-id="555cc-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1173">authenticationType</span></span> |<span data-ttu-id="555cc-1174">Tipo di autenticazione usato per connettersi al database DB2.</span><span class="sxs-lookup"><span data-stu-id="555cc-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="555cc-1175">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="555cc-1176">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1176">Yes</span></span> |
| <span data-ttu-id="555cc-1177">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1177">username</span></span> |<span data-ttu-id="555cc-1178">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="555cc-1179">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1179">No</span></span> |
| <span data-ttu-id="555cc-1180">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1180">password</span></span> |<span data-ttu-id="555cc-1181">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-1182">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1182">No</span></span> |
| <span data-ttu-id="555cc-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1183">gatewayName</span></span> |<span data-ttu-id="555cc-1184">Nome del gateway che il servizio Data factory deve usare per connettersi al database DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="555cc-1185">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1186">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="555cc-1187">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1188">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1188">Dataset</span></span>
<span data-ttu-id="555cc-1189">Per definire un set di dati di DB2, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="555cc-1190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1190">Property</span></span> | <span data-ttu-id="555cc-1191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1191">Description</span></span> | <span data-ttu-id="555cc-1192">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1193">tableName</span></span> |<span data-ttu-id="555cc-1194">Nome della tabella nell'istanza del database DB2 a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="555cc-1195">La proprietà tableName fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="555cc-1196">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="555cc-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="555cc-1197">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1198">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1199">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1200">Se si copiano dati da IBM DB2, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1201">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1201">Property</span></span> | <span data-ttu-id="555cc-1202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1202">Description</span></span> | <span data-ttu-id="555cc-1203">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1203">Allowed values</span></span> | <span data-ttu-id="555cc-1204">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1205">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1205">query</span></span> |<span data-ttu-id="555cc-1206">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1207">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1207">SQL query string.</span></span> <span data-ttu-id="555cc-1208">Ad esempio: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="555cc-1209">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1210">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="555cc-1211">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="555cc-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="555cc-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1213">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1213">Linked service</span></span>
<span data-ttu-id="555cc-1214">Per definire un servizio collegato di MySQL, impostare il **tipo** di servizio collegato su **OnPremisesMySql** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1215">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1215">Property</span></span> | <span data-ttu-id="555cc-1216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1216">Description</span></span> | <span data-ttu-id="555cc-1217">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1218">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1218">server</span></span> |<span data-ttu-id="555cc-1219">Nome del server MySQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="555cc-1220">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1220">Yes</span></span> |
| <span data-ttu-id="555cc-1221">database</span><span class="sxs-lookup"><span data-stu-id="555cc-1221">database</span></span> |<span data-ttu-id="555cc-1222">Nome del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="555cc-1223">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1223">Yes</span></span> |
| <span data-ttu-id="555cc-1224">schema</span><span class="sxs-lookup"><span data-stu-id="555cc-1224">schema</span></span> |<span data-ttu-id="555cc-1225">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="555cc-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="555cc-1226">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1226">No</span></span> |
| <span data-ttu-id="555cc-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1227">authenticationType</span></span> |<span data-ttu-id="555cc-1228">Tipo di autenticazione usato per connettersi al database MySQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="555cc-1229">I valori possibili sono:`Basic`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="555cc-1230">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1230">Yes</span></span> |
| <span data-ttu-id="555cc-1231">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1231">username</span></span> |<span data-ttu-id="555cc-1232">Specificare nome utente per la connessione al database MySQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="555cc-1233">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1233">Yes</span></span> |
| <span data-ttu-id="555cc-1234">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1234">password</span></span> |<span data-ttu-id="555cc-1235">Specificare la password per l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="555cc-1236">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1236">Yes</span></span> |
| <span data-ttu-id="555cc-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1237">gatewayName</span></span> |<span data-ttu-id="555cc-1238">Nome del gateway che il servizio Data factory deve usare per connettersi al database MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="555cc-1239">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1240">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="555cc-1241">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1242">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1242">Dataset</span></span>
<span data-ttu-id="555cc-1243">Per definire un set di dati di MySQL, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1244">Property</span></span> | <span data-ttu-id="555cc-1245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1245">Description</span></span> | <span data-ttu-id="555cc-1246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1247">tableName</span></span> |<span data-ttu-id="555cc-1248">Nome della tabella nell'istanza del database MySQL a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="555cc-1249">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="555cc-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1250">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="555cc-1251">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1252">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1253">Se si copiano dati da un database MySQL, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1254">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1254">Property</span></span> | <span data-ttu-id="555cc-1255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1255">Description</span></span> | <span data-ttu-id="555cc-1256">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1256">Allowed values</span></span> | <span data-ttu-id="555cc-1257">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1258">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1258">query</span></span> |<span data-ttu-id="555cc-1259">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1260">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1260">SQL query string.</span></span> <span data-ttu-id="555cc-1261">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-1262">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-1263">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1264">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="555cc-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="555cc-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-1266">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1266">Linked service</span></span>
<span data-ttu-id="555cc-1267">Per definire un servizio collegato di Oracle, impostare il **tipo** di servizio collegato su **OnPremisesOracle** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1268">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1268">Property</span></span> | <span data-ttu-id="555cc-1269">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1269">Description</span></span> | <span data-ttu-id="555cc-1270">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="555cc-1271">driverType</span></span> | <span data-ttu-id="555cc-1272">Specificare il driver da usare per copiare i dati da/verso il database Oracle.</span><span class="sxs-lookup"><span data-stu-id="555cc-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="555cc-1273">I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="555cc-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="555cc-1274">Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="555cc-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="555cc-1275">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1275">No</span></span> |
| <span data-ttu-id="555cc-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-1276">connectionString</span></span> | <span data-ttu-id="555cc-1277">Specificare le informazioni necessarie per connettersi all'istanza del database Oracle per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="555cc-1278">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1278">Yes</span></span> |
| <span data-ttu-id="555cc-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1279">gatewayName</span></span> | <span data-ttu-id="555cc-1280">Nome del gateway usato per connettersi al server Oracle locale</span><span class="sxs-lookup"><span data-stu-id="555cc-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="555cc-1281">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1282">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="555cc-1283">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1284">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1284">Dataset</span></span>
<span data-ttu-id="555cc-1285">Per definire un set di dati di Oracle, impostare il **tipo** di set di dati su **OracleTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1286">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1286">Property</span></span> | <span data-ttu-id="555cc-1287">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1287">Description</span></span> | <span data-ttu-id="555cc-1288">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1289">tableName</span></span> |<span data-ttu-id="555cc-1290">Nome della tabella nell'istanza del database Oracle a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="555cc-1291">No, se **oracleReaderQuery** di **OracleSource** è specificato</span><span class="sxs-lookup"><span data-stu-id="555cc-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1292">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="555cc-1293">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="555cc-1294">Origine Oracle nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1295">Se si copiano dati da un database Oracle, impostare il **tipo di origine** dell'attività di copia su **OracleSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1296">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1296">Property</span></span> | <span data-ttu-id="555cc-1297">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1297">Description</span></span> | <span data-ttu-id="555cc-1298">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1298">Allowed values</span></span> | <span data-ttu-id="555cc-1299">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="555cc-1300">oracleReaderQuery</span></span> |<span data-ttu-id="555cc-1301">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1302">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1302">SQL query string.</span></span> <span data-ttu-id="555cc-1303">Ad esempio: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="555cc-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="555cc-1304">Se non specificato, l'istruzione SQL eseguita: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="555cc-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="555cc-1305">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1306">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1307">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="555cc-1308">Sink Oracle nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-1309">Se si copiano dati in un database Oracle, impostare il **tipo di sink** dell'attività di copia su **OracleSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-1310">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1310">Property</span></span> | <span data-ttu-id="555cc-1311">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1311">Description</span></span> | <span data-ttu-id="555cc-1312">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1312">Allowed values</span></span> | <span data-ttu-id="555cc-1313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-1314">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-1315">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="555cc-1316">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-1316">timespan</span></span><br/><br/> <span data-ttu-id="555cc-1317">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="555cc-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="555cc-1318">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1318">No</span></span> |
| <span data-ttu-id="555cc-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-1319">writeBatchSize</span></span> |<span data-ttu-id="555cc-1320">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="555cc-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="555cc-1321">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="555cc-1321">Integer (number of rows)</span></span> |<span data-ttu-id="555cc-1322">No (valore predefinito: 100)</span><span class="sxs-lookup"><span data-stu-id="555cc-1322">No (default: 100)</span></span> |
| <span data-ttu-id="555cc-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="555cc-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="555cc-1324">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="555cc-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="555cc-1325">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="555cc-1325">A query statement.</span></span> |<span data-ttu-id="555cc-1326">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1326">No</span></span> |
| <span data-ttu-id="555cc-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="555cc-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="555cc-1328">Specificare il nome della colonna per l'attività di copia da riempire con l'identificatore di sezione generato automaticamente, che viene usato per eliminare i dati di una sezione specifica quando viene nuovamente eseguita.</span><span class="sxs-lookup"><span data-stu-id="555cc-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="555cc-1329">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="555cc-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="555cc-1330">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1331">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="555cc-1332">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="555cc-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="555cc-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1334">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1334">Linked service</span></span>
<span data-ttu-id="555cc-1335">Per definire un servizio collegato di PostgreSQL, impostare il **tipo** di servizio collegato su **OnPremisesPostgreSql** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1336">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1336">Property</span></span> | <span data-ttu-id="555cc-1337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1337">Description</span></span> | <span data-ttu-id="555cc-1338">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1339">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1339">server</span></span> |<span data-ttu-id="555cc-1340">Nome del server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="555cc-1341">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1341">Yes</span></span> |
| <span data-ttu-id="555cc-1342">database</span><span class="sxs-lookup"><span data-stu-id="555cc-1342">database</span></span> |<span data-ttu-id="555cc-1343">Nome del database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="555cc-1344">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1344">Yes</span></span> |
| <span data-ttu-id="555cc-1345">schema</span><span class="sxs-lookup"><span data-stu-id="555cc-1345">schema</span></span> |<span data-ttu-id="555cc-1346">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="555cc-1346">Name of the schema in the database.</span></span> <span data-ttu-id="555cc-1347">Il nome dello schema fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="555cc-1348">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1348">No</span></span> |
| <span data-ttu-id="555cc-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1349">authenticationType</span></span> |<span data-ttu-id="555cc-1350">Tipo di autenticazione usato per connettersi al database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="555cc-1351">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="555cc-1352">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1352">Yes</span></span> |
| <span data-ttu-id="555cc-1353">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1353">username</span></span> |<span data-ttu-id="555cc-1354">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="555cc-1355">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1355">No</span></span> |
| <span data-ttu-id="555cc-1356">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1356">password</span></span> |<span data-ttu-id="555cc-1357">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-1358">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1358">No</span></span> |
| <span data-ttu-id="555cc-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1359">gatewayName</span></span> |<span data-ttu-id="555cc-1360">Nome del gateway che il servizio Data factory deve usare per connettersi al database PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="555cc-1361">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1362">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="555cc-1363">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1364">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1364">Dataset</span></span>
<span data-ttu-id="555cc-1365">Per definire un set di dati di PostgreSQL, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1366">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1366">Property</span></span> | <span data-ttu-id="555cc-1367">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1367">Description</span></span> | <span data-ttu-id="555cc-1368">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1369">tableName</span></span> |<span data-ttu-id="555cc-1370">Nome della tabella nell'istanza del database PostgreSQL a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="555cc-1371">La proprietà tableName fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="555cc-1372">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="555cc-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1373">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="555cc-1374">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1375">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1376">Se si copiano dati da un database PostgreSQL, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1377">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1377">Property</span></span> | <span data-ttu-id="555cc-1378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1378">Description</span></span> | <span data-ttu-id="555cc-1379">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1379">Allowed values</span></span> | <span data-ttu-id="555cc-1380">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1381">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1381">query</span></span> |<span data-ttu-id="555cc-1382">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1383">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1383">SQL query string.</span></span> <span data-ttu-id="555cc-1384">Ad esempio: "query": "select * from \"Schema\".\"Tabella\"".</span><span class="sxs-lookup"><span data-stu-id="555cc-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="555cc-1385">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1386">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1387">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="555cc-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-1389">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1389">Linked service</span></span>
<span data-ttu-id="555cc-1390">Per definire un servizio collegato di SAP Business Warehouse (BW), impostare il **tipo** di servizio collegato su **SapBw**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="555cc-1391">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1391">Property</span></span> | <span data-ttu-id="555cc-1392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1392">Description</span></span> | <span data-ttu-id="555cc-1393">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1393">Allowed values</span></span> | <span data-ttu-id="555cc-1394">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="555cc-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="555cc-1395">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1395">server</span></span> | <span data-ttu-id="555cc-1396">Nome del server in cui si trova l'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="555cc-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="555cc-1397">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1397">string</span></span> | <span data-ttu-id="555cc-1398">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1398">Yes</span></span>
<span data-ttu-id="555cc-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="555cc-1399">systemNumber</span></span> | <span data-ttu-id="555cc-1400">Numero del sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="555cc-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="555cc-1401">Numero decimale a due cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="555cc-1402">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1402">Yes</span></span>
<span data-ttu-id="555cc-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="555cc-1403">clientId</span></span> | <span data-ttu-id="555cc-1404">ID del client nel sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="555cc-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="555cc-1405">Numero decimale a tre cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="555cc-1406">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1406">Yes</span></span>
<span data-ttu-id="555cc-1407">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1407">username</span></span> | <span data-ttu-id="555cc-1408">Nome dell'utente che ha accesso al server SAP</span><span class="sxs-lookup"><span data-stu-id="555cc-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="555cc-1409">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1409">string</span></span> | <span data-ttu-id="555cc-1410">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1410">Yes</span></span>
<span data-ttu-id="555cc-1411">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1411">password</span></span> | <span data-ttu-id="555cc-1412">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1412">Password for the user.</span></span> | <span data-ttu-id="555cc-1413">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1413">string</span></span> | <span data-ttu-id="555cc-1414">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1414">Yes</span></span>
<span data-ttu-id="555cc-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1415">gatewayName</span></span> | <span data-ttu-id="555cc-1416">Nome del gateway che il servizio Data factory deve usare per connettersi all'istanza di SAP BW locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="555cc-1417">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1417">string</span></span> | <span data-ttu-id="555cc-1418">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1418">Yes</span></span>
<span data-ttu-id="555cc-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1419">encryptedCredential</span></span> | <span data-ttu-id="555cc-1420">Stringa di credenziali crittografata.</span><span class="sxs-lookup"><span data-stu-id="555cc-1420">The encrypted credential string.</span></span> | <span data-ttu-id="555cc-1421">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1421">string</span></span> | <span data-ttu-id="555cc-1422">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-1423">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="555cc-1424">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1425">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1425">Dataset</span></span>
<span data-ttu-id="555cc-1426">Per definire un set di dati SAP BW, impostare il **tipo** del set di dati su **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="555cc-1427">Il set di dati SAP BW di tipo **RelationalTable** non supporta alcuna proprietà specifica del tipo.</span><span class="sxs-lookup"><span data-stu-id="555cc-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="555cc-1428">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="555cc-1429">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1430">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1431">Se si copiano dati da SAP Business Warehouse, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1432">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1432">Property</span></span> | <span data-ttu-id="555cc-1433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1433">Description</span></span> | <span data-ttu-id="555cc-1434">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1434">Allowed values</span></span> | <span data-ttu-id="555cc-1435">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1436">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1436">query</span></span> | <span data-ttu-id="555cc-1437">Specifica la query MDX che consente di leggere i dati dall'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="555cc-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="555cc-1438">Query MDX.</span><span class="sxs-lookup"><span data-stu-id="555cc-1438">MDX query.</span></span> | <span data-ttu-id="555cc-1439">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1440">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1441">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="555cc-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="555cc-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1443">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1443">Linked service</span></span>
<span data-ttu-id="555cc-1444">Per definire un servizio collegato di SAP HANA, impostare il **tipo** di servizio collegato su **SapHana** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="555cc-1445">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1445">Property</span></span> | <span data-ttu-id="555cc-1446">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1446">Description</span></span> | <span data-ttu-id="555cc-1447">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1447">Allowed values</span></span> | <span data-ttu-id="555cc-1448">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="555cc-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="555cc-1449">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1449">server</span></span> | <span data-ttu-id="555cc-1450">Nome del server in cui si trova l'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="555cc-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="555cc-1451">Se il server usa una porta personalizzata, specificare `server:port`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="555cc-1452">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1452">string</span></span> | <span data-ttu-id="555cc-1453">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1453">Yes</span></span>
<span data-ttu-id="555cc-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1454">authenticationType</span></span> | <span data-ttu-id="555cc-1455">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1455">Type of authentication.</span></span> | <span data-ttu-id="555cc-1456">string.</span><span class="sxs-lookup"><span data-stu-id="555cc-1456">string.</span></span> <span data-ttu-id="555cc-1457">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="555cc-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="555cc-1458">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1458">Yes</span></span> 
<span data-ttu-id="555cc-1459">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1459">username</span></span> | <span data-ttu-id="555cc-1460">Nome dell'utente che ha accesso al server SAP</span><span class="sxs-lookup"><span data-stu-id="555cc-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="555cc-1461">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1461">string</span></span> | <span data-ttu-id="555cc-1462">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1462">Yes</span></span>
<span data-ttu-id="555cc-1463">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1463">password</span></span> | <span data-ttu-id="555cc-1464">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1464">Password for the user.</span></span> | <span data-ttu-id="555cc-1465">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1465">string</span></span> | <span data-ttu-id="555cc-1466">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1466">Yes</span></span>
<span data-ttu-id="555cc-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1467">gatewayName</span></span> | <span data-ttu-id="555cc-1468">Nome del gateway che il servizio Data factory deve usare per connettersi all'istanza di SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="555cc-1469">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1469">string</span></span> | <span data-ttu-id="555cc-1470">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1470">Yes</span></span>
<span data-ttu-id="555cc-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1471">encryptedCredential</span></span> | <span data-ttu-id="555cc-1472">Stringa di credenziali crittografata.</span><span class="sxs-lookup"><span data-stu-id="555cc-1472">The encrypted credential string.</span></span> | <span data-ttu-id="555cc-1473">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1473">string</span></span> | <span data-ttu-id="555cc-1474">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-1475">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="555cc-1476">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="555cc-1477">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1477">Dataset</span></span>
<span data-ttu-id="555cc-1478">Per definire un set di dati SAP HANA, impostare il **tipo** del set di dati su **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="555cc-1479">Il set di dati SAP HANA di tipo **RelationalTable** non supporta alcuna proprietà specifica del tipo.</span><span class="sxs-lookup"><span data-stu-id="555cc-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="555cc-1480">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="555cc-1481">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1482">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1483">Se si copiano dati da un archivio dati SAP HANA, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1484">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1484">Property</span></span> | <span data-ttu-id="555cc-1485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1485">Description</span></span> | <span data-ttu-id="555cc-1486">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1486">Allowed values</span></span> | <span data-ttu-id="555cc-1487">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1488">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1488">query</span></span> | <span data-ttu-id="555cc-1489">Specifica la query SQL che consente di leggere i dati dall'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="555cc-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="555cc-1490">Query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1490">SQL query.</span></span> | <span data-ttu-id="555cc-1491">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-1492">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1493">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="555cc-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="555cc-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1495">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1495">Linked service</span></span>
<span data-ttu-id="555cc-1496">È stato creato un servizio collegato di tipo **OnPremisesSqlServer** per collegare un database di SQL Server locale a una data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="555cc-1497">La tabella seguente contiene le descrizioni degli elementi JSON specifici per il servizio collegato di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="555cc-1498">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato SQL Server.</span><span class="sxs-lookup"><span data-stu-id="555cc-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="555cc-1499">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1499">Property</span></span> | <span data-ttu-id="555cc-1500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1500">Description</span></span> | <span data-ttu-id="555cc-1501">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1502">type</span><span class="sxs-lookup"><span data-stu-id="555cc-1502">type</span></span> |<span data-ttu-id="555cc-1503">La proprietà type deve essere impostata su **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="555cc-1504">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1504">Yes</span></span> |
| <span data-ttu-id="555cc-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-1505">connectionString</span></span> |<span data-ttu-id="555cc-1506">Specificare le informazioni di connectionString necessarie per connettersi al database di SQL Server locale usando l'autenticazione di SQL o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="555cc-1507">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1507">Yes</span></span> |
| <span data-ttu-id="555cc-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1508">gatewayName</span></span> |<span data-ttu-id="555cc-1509">Nome del gateway che il servizio Data factory deve usare per connettersi al database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="555cc-1510">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1510">Yes</span></span> |
| <span data-ttu-id="555cc-1511">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1511">username</span></span> |<span data-ttu-id="555cc-1512">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="555cc-1513">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="555cc-1514">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1514">No</span></span> |
| <span data-ttu-id="555cc-1515">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1515">password</span></span> |<span data-ttu-id="555cc-1516">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-1517">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1517">No</span></span> |

<span data-ttu-id="555cc-1518">È possibile crittografare le credenziali usando il cmdlet **New-AzureRmDataFactoryEncryptValue** e usarle nella stringa di connessione, come illustrato nell'esempio seguente (proprietà **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="555cc-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="555cc-1519">Esempio: JSON per l'uso dell'autenticazione SQL</span><span class="sxs-lookup"><span data-stu-id="555cc-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="555cc-1520">Esempio: JSON per l'uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="555cc-1521">Se vengono specificati nome utente e password, il gateway li usa per rappresentare l'account utente specificato per la connessione al database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="555cc-1522">In caso contrario, il gateway si connette a SQL Server direttamente con il contesto di sicurezza del gateway (l'account di avvio).</span><span class="sxs-lookup"><span data-stu-id="555cc-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="555cc-1523">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1524">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1524">Dataset</span></span>
<span data-ttu-id="555cc-1525">Per definire un set di dati di SQL Server, impostare il **tipo** di set di dati su **SqlServerTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1526">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1526">Property</span></span> | <span data-ttu-id="555cc-1527">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1527">Description</span></span> | <span data-ttu-id="555cc-1528">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1529">tableName</span></span> |<span data-ttu-id="555cc-1530">Nome della tabella o vista nell'istanza del database di SQL Server a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="555cc-1531">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1532">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1533">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="555cc-1534">Origine SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1535">Se si copiano dati da un database SQL Server, impostare il **tipo di origine** dell'attività di copia su **SqlSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1536">Property</span></span> | <span data-ttu-id="555cc-1537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1537">Description</span></span> | <span data-ttu-id="555cc-1538">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1538">Allowed values</span></span> | <span data-ttu-id="555cc-1539">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="555cc-1540">sqlReaderQuery</span></span> |<span data-ttu-id="555cc-1541">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1542">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1542">SQL query string.</span></span> <span data-ttu-id="555cc-1543">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="555cc-1544">Può fare riferimento a più tabelle del database a cui fa riferimento il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="555cc-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="555cc-1545">Se non specificato, l'istruzione SQL eseguita: selezionare da MyTable.</span><span class="sxs-lookup"><span data-stu-id="555cc-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="555cc-1546">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1546">No</span></span> |
| <span data-ttu-id="555cc-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="555cc-1548">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="555cc-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="555cc-1549">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="555cc-1550">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1550">No</span></span> |
| <span data-ttu-id="555cc-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-1551">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-1552">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="555cc-1553">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="555cc-1553">Name/value pairs.</span></span> <span data-ttu-id="555cc-1554">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="555cc-1555">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1555">No</span></span> |

<span data-ttu-id="555cc-1556">Se la proprietà **sqlReaderQuery** è specificata per SqlSource, l'attività di copia esegue questa query nell'origine del database del server di SQL per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="555cc-1557">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="555cc-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="555cc-1558">Se non si specifica il parametro sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura vengono usate per compilare una query da eseguire nel database del server di SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="555cc-1559">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="555cc-1560">Quando si usa **sqlReaderStoredProcedureName** è necessario specificare un valore per la proprietà **tableName** nel set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="555cc-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="555cc-1561">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="555cc-1562">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1563">In questo esempio la proprietà **sqlReaderQuery** è specificata per SqlSource.</span><span class="sxs-lookup"><span data-stu-id="555cc-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="555cc-1564">L'attività di copia esegue questa query nell'origine del database del server SQL per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="555cc-1565">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="555cc-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="555cc-1566">La proprietà sqlReaderQuery può fare riferimento a più tabelle nel database a cui fa riferimento il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="555cc-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="555cc-1567">Non è limitato solo alla tabella impostata come typeProperty tableName del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="555cc-1568">Se non si specifica il parametro sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura vengono usate per compilare una query di selezione da eseguire nel database del server di SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="555cc-1569">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="555cc-1570">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="555cc-1571">Sink SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-1572">Se si copiano dati da un database SQL Server, impostare il **tipo di sink** dell'attività di copia su **SqlSink**e specificare le proprietà seguenti nella sezione **ink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-1573">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1573">Property</span></span> | <span data-ttu-id="555cc-1574">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1574">Description</span></span> | <span data-ttu-id="555cc-1575">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1575">Allowed values</span></span> | <span data-ttu-id="555cc-1576">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-1577">writeBatchTimeout</span></span> |<span data-ttu-id="555cc-1578">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="555cc-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="555cc-1579">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="555cc-1579">timespan</span></span><br/><br/> <span data-ttu-id="555cc-1580">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="555cc-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="555cc-1581">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1581">No</span></span> |
| <span data-ttu-id="555cc-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="555cc-1582">writeBatchSize</span></span> |<span data-ttu-id="555cc-1583">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="555cc-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="555cc-1584">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="555cc-1584">Integer (number of rows)</span></span> |<span data-ttu-id="555cc-1585">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="555cc-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="555cc-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="555cc-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="555cc-1587">Specificare la query per l'attività di copia da eseguire in modo che i dati di una sezione specifica vengano eliminati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="555cc-1588">Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="555cc-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="555cc-1589">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="555cc-1589">A query statement.</span></span> |<span data-ttu-id="555cc-1590">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1590">No</span></span> |
| <span data-ttu-id="555cc-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="555cc-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="555cc-1592">Specificare il nome della colonna per l'attività di copia da riempire con l'identificatore di sezione generato automaticamente, che viene usato per eliminare i dati di una sezione specifica quando viene nuovamente eseguita.</span><span class="sxs-lookup"><span data-stu-id="555cc-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="555cc-1593">Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="555cc-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="555cc-1594">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="555cc-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="555cc-1595">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1595">No</span></span> |
| <span data-ttu-id="555cc-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="555cc-1597">Nome della stored procedure che esegue l'upsert (aggiornamenti/inserimenti) nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="555cc-1598">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="555cc-1599">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1599">No</span></span> |
| <span data-ttu-id="555cc-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-1600">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-1601">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="555cc-1602">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="555cc-1602">Name/value pairs.</span></span> <span data-ttu-id="555cc-1603">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="555cc-1604">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1604">No</span></span> |
| <span data-ttu-id="555cc-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="555cc-1605">sqlWriterTableType</span></span> |<span data-ttu-id="555cc-1606">Specificare il tipo di tabella da usare nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="555cc-1607">L'attività di copia rende i dati spostati disponibili in una tabella temporanea con questo tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="555cc-1608">Il codice della stored procedure può quindi unire i dati copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="555cc-1609">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1609">A table type name.</span></span> |<span data-ttu-id="555cc-1610">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1611">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1611">Example</span></span>
<span data-ttu-id="555cc-1612">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="555cc-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="555cc-1613">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo **sink** è impostato su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1614">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="555cc-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="555cc-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1616">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1616">Linked service</span></span>
<span data-ttu-id="555cc-1617">Per definire un servizio collegato di Sybase, impostare il **tipo** di servizio collegato su **OnPremisesSybase** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1618">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1618">Property</span></span> | <span data-ttu-id="555cc-1619">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1619">Description</span></span> | <span data-ttu-id="555cc-1620">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1621">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1621">server</span></span> |<span data-ttu-id="555cc-1622">Nome del server Sybase.</span><span class="sxs-lookup"><span data-stu-id="555cc-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="555cc-1623">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1623">Yes</span></span> |
| <span data-ttu-id="555cc-1624">database</span><span class="sxs-lookup"><span data-stu-id="555cc-1624">database</span></span> |<span data-ttu-id="555cc-1625">Nome del database Sybase.</span><span class="sxs-lookup"><span data-stu-id="555cc-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="555cc-1626">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1626">Yes</span></span> |
| <span data-ttu-id="555cc-1627">schema</span><span class="sxs-lookup"><span data-stu-id="555cc-1627">schema</span></span> |<span data-ttu-id="555cc-1628">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="555cc-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="555cc-1629">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1629">No</span></span> |
| <span data-ttu-id="555cc-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1630">authenticationType</span></span> |<span data-ttu-id="555cc-1631">Tipo di autenticazione usato per connettersi al database Sybase.</span><span class="sxs-lookup"><span data-stu-id="555cc-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="555cc-1632">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="555cc-1633">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1633">Yes</span></span> |
| <span data-ttu-id="555cc-1634">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1634">username</span></span> |<span data-ttu-id="555cc-1635">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="555cc-1636">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1636">No</span></span> |
| <span data-ttu-id="555cc-1637">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1637">password</span></span> |<span data-ttu-id="555cc-1638">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-1639">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1639">No</span></span> |
| <span data-ttu-id="555cc-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1640">gatewayName</span></span> |<span data-ttu-id="555cc-1641">Nome del gateway che il servizio Data factory deve usare per connettersi al database Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="555cc-1642">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1643">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="555cc-1644">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1645">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1645">Dataset</span></span>
<span data-ttu-id="555cc-1646">Per definire un set di dati di Sybase, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1647">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1647">Property</span></span> | <span data-ttu-id="555cc-1648">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1648">Description</span></span> | <span data-ttu-id="555cc-1649">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1650">tableName</span></span> |<span data-ttu-id="555cc-1651">Nome della tabella nell'istanza del database Sybase a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="555cc-1652">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="555cc-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1653">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1654">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1655">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1656">Se si copiano dati da un database Sybase, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1657">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1657">Property</span></span> | <span data-ttu-id="555cc-1658">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1658">Description</span></span> | <span data-ttu-id="555cc-1659">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1659">Allowed values</span></span> | <span data-ttu-id="555cc-1660">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1661">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1661">query</span></span> |<span data-ttu-id="555cc-1662">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1663">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1663">SQL query string.</span></span> <span data-ttu-id="555cc-1664">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-1665">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="555cc-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1666">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1667">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="555cc-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="555cc-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1669">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1669">Linked service</span></span>
<span data-ttu-id="555cc-1670">Per definire un servizio collegato di Teradata, impostare il **tipo** di servizio collegato su **OnPremisesTeradata** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1671">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1671">Property</span></span> | <span data-ttu-id="555cc-1672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1672">Description</span></span> | <span data-ttu-id="555cc-1673">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1674">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1674">server</span></span> |<span data-ttu-id="555cc-1675">Nome del server Teradata.</span><span class="sxs-lookup"><span data-stu-id="555cc-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="555cc-1676">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1676">Yes</span></span> |
| <span data-ttu-id="555cc-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1677">authenticationType</span></span> |<span data-ttu-id="555cc-1678">Tipo di autenticazione usato per connettersi al database Teradata.</span><span class="sxs-lookup"><span data-stu-id="555cc-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="555cc-1679">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="555cc-1680">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1680">Yes</span></span> |
| <span data-ttu-id="555cc-1681">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1681">username</span></span> |<span data-ttu-id="555cc-1682">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="555cc-1683">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1683">No</span></span> |
| <span data-ttu-id="555cc-1684">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1684">password</span></span> |<span data-ttu-id="555cc-1685">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-1686">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1686">No</span></span> |
| <span data-ttu-id="555cc-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1687">gatewayName</span></span> |<span data-ttu-id="555cc-1688">Nome del gateway che il servizio Data factory deve usare per connettersi al database Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="555cc-1689">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1690">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="555cc-1691">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1692">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1692">Dataset</span></span>
<span data-ttu-id="555cc-1693">Per definire un set di dati BLOB di Teradata, impostare il **tipo** del set di dati su **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="555cc-1694">Attualmente non sono disponibili proprietà di tipo supportate per il set di dati Teradata.</span><span class="sxs-lookup"><span data-stu-id="555cc-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="555cc-1695">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1696">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-1697">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1698">Se si copiano dati da un database Teradata, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1699">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1699">Property</span></span> | <span data-ttu-id="555cc-1700">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1700">Description</span></span> | <span data-ttu-id="555cc-1701">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1701">Allowed values</span></span> | <span data-ttu-id="555cc-1702">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1703">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1703">query</span></span> |<span data-ttu-id="555cc-1704">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1705">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1705">SQL query string.</span></span> <span data-ttu-id="555cc-1706">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-1707">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1708">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="555cc-1709">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="555cc-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="555cc-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-1711">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1711">Linked service</span></span>
<span data-ttu-id="555cc-1712">Per definire un servizio collegato di Cassandra, impostare il **tipo** di servizio collegato su **OnPremisesCassandra** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1713">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1713">Property</span></span> | <span data-ttu-id="555cc-1714">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1714">Description</span></span> | <span data-ttu-id="555cc-1715">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1716">host</span><span class="sxs-lookup"><span data-stu-id="555cc-1716">host</span></span> |<span data-ttu-id="555cc-1717">Uno o più indirizzi IP o nomi host di server Cassandra.</span><span class="sxs-lookup"><span data-stu-id="555cc-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="555cc-1718">Specificare un elenco delimitato da virgole degli indirizzi IP o nomi host per la connessione a tutti i server contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="555cc-1719">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1719">Yes</span></span> |
| <span data-ttu-id="555cc-1720">port</span><span class="sxs-lookup"><span data-stu-id="555cc-1720">port</span></span> |<span data-ttu-id="555cc-1721">La porta TCP che il server Cassandra usa per ascoltare le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="555cc-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="555cc-1722">No, valore predefinito: 9042</span><span class="sxs-lookup"><span data-stu-id="555cc-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="555cc-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1723">authenticationType</span></span> |<span data-ttu-id="555cc-1724">Di base o anonima</span><span class="sxs-lookup"><span data-stu-id="555cc-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="555cc-1725">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1725">Yes</span></span> |
| <span data-ttu-id="555cc-1726">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1726">username</span></span> |<span data-ttu-id="555cc-1727">Specificare il nome utente per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="555cc-1728">Sì, se authenticationType è impostato su Basic.</span><span class="sxs-lookup"><span data-stu-id="555cc-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="555cc-1729">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1729">password</span></span> |<span data-ttu-id="555cc-1730">Specifica la password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1730">Specify password for the user account.</span></span> |<span data-ttu-id="555cc-1731">Sì, se authenticationType è impostato su Basic.</span><span class="sxs-lookup"><span data-stu-id="555cc-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="555cc-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1732">gatewayName</span></span> |<span data-ttu-id="555cc-1733">Il nome del gateway che viene usato per connettersi al database Cassandra locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="555cc-1734">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1734">Yes</span></span> |
| <span data-ttu-id="555cc-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1735">encryptedCredential</span></span> |<span data-ttu-id="555cc-1736">Credenziali crittografate dal gateway.</span><span class="sxs-lookup"><span data-stu-id="555cc-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="555cc-1737">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1738">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="555cc-1739">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-1740">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1740">Dataset</span></span>
<span data-ttu-id="555cc-1741">Per definire un set di dati di Cassandra, impostare il **tipo** di set di dati su **Table**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1742">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1742">Property</span></span> | <span data-ttu-id="555cc-1743">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1743">Description</span></span> | <span data-ttu-id="555cc-1744">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="555cc-1745">keyspace</span></span> |<span data-ttu-id="555cc-1746">Nome del keyspace o schema nel database Cassandra.</span><span class="sxs-lookup"><span data-stu-id="555cc-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="555cc-1747">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="555cc-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="555cc-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-1748">tableName</span></span> |<span data-ttu-id="555cc-1749">Nome della tabella in un database Cassandra.</span><span class="sxs-lookup"><span data-stu-id="555cc-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="555cc-1750">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="555cc-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1751">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1752">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="555cc-1753">Origine Cassandra nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1754">Se si copiano dati da Cassandra, impostare il **tipo di origine** dell'attività di copia su **Source**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1755">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1755">Property</span></span> | <span data-ttu-id="555cc-1756">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1756">Description</span></span> | <span data-ttu-id="555cc-1757">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1757">Allowed values</span></span> | <span data-ttu-id="555cc-1758">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1759">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1759">query</span></span> |<span data-ttu-id="555cc-1760">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1761">Query SQL-92 o query CQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="555cc-1762">Vedere il [riferimento a CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="555cc-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="555cc-1763">Quando si usa una query SQL, specificare **nome keyspace.nome tabella** per indicare la tabella su cui eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="555cc-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="555cc-1764">No (se tableName e keyspace sul set di dati sono definiti).</span><span class="sxs-lookup"><span data-stu-id="555cc-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="555cc-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="555cc-1765">consistencyLevel</span></span> |<span data-ttu-id="555cc-1766">Il livello di coerenza specifica quante repliche devono rispondere a una richiesta di lettura prima della restituzione dei dati all'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="555cc-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="555cc-1767">Cassandra controlla il numero di repliche specificato perché i dati soddisfino la richiesta di lettura.</span><span class="sxs-lookup"><span data-stu-id="555cc-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="555cc-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="555cc-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="555cc-1769">Per informazioni dettagliate, vedere [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configurazione della coerenza dei dati).</span><span class="sxs-lookup"><span data-stu-id="555cc-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="555cc-1770">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-1770">No.</span></span> <span data-ttu-id="555cc-1771">Il valore predefinito è ONE.</span><span class="sxs-lookup"><span data-stu-id="555cc-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1772">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-1773">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="555cc-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="555cc-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-1775">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1775">Linked service</span></span>
<span data-ttu-id="555cc-1776">Per definire un servizio collegato di MongoDB, impostare il **tipo** di servizio collegato su **OnPremisesMongoDB** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1777">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1777">Property</span></span> | <span data-ttu-id="555cc-1778">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1778">Description</span></span> | <span data-ttu-id="555cc-1779">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1780">server</span><span class="sxs-lookup"><span data-stu-id="555cc-1780">server</span></span> |<span data-ttu-id="555cc-1781">Indirizzo IP o nome host del server MongoDB.</span><span class="sxs-lookup"><span data-stu-id="555cc-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="555cc-1782">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1782">Yes</span></span> |
| <span data-ttu-id="555cc-1783">port</span><span class="sxs-lookup"><span data-stu-id="555cc-1783">port</span></span> |<span data-ttu-id="555cc-1784">Porta TCP che il server MongoDB usa per ascoltare le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="555cc-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="555cc-1785">Facoltativo, valore predefinito: 27017</span><span class="sxs-lookup"><span data-stu-id="555cc-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="555cc-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-1786">authenticationType</span></span> |<span data-ttu-id="555cc-1787">Di base o anonima.</span><span class="sxs-lookup"><span data-stu-id="555cc-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="555cc-1788">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1788">Yes</span></span> |
| <span data-ttu-id="555cc-1789">username</span><span class="sxs-lookup"><span data-stu-id="555cc-1789">username</span></span> |<span data-ttu-id="555cc-1790">Account utente per accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="555cc-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="555cc-1791">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="555cc-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="555cc-1792">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1792">password</span></span> |<span data-ttu-id="555cc-1793">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1793">Password for the user.</span></span> |<span data-ttu-id="555cc-1794">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="555cc-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="555cc-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="555cc-1795">authSource</span></span> |<span data-ttu-id="555cc-1796">Nome del database MongoDB che si vuole usare per controllare le credenziali di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="555cc-1797">Facoltativo (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="555cc-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="555cc-1798">Predefinito: usa l'account di amministrazione e il database specificato usando la proprietà databaseName.</span><span class="sxs-lookup"><span data-stu-id="555cc-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="555cc-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="555cc-1799">databaseName</span></span> |<span data-ttu-id="555cc-1800">Nome del database MongoDB a cui si vuole accedere.</span><span class="sxs-lookup"><span data-stu-id="555cc-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="555cc-1801">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1801">Yes</span></span> |
| <span data-ttu-id="555cc-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1802">gatewayName</span></span> |<span data-ttu-id="555cc-1803">Nome del gateway che accede all'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="555cc-1804">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1804">Yes</span></span> |
| <span data-ttu-id="555cc-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1805">encryptedCredential</span></span> |<span data-ttu-id="555cc-1806">Credenziali crittografate in base al gateway.</span><span class="sxs-lookup"><span data-stu-id="555cc-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="555cc-1807">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="555cc-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1808">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="555cc-1809">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1810">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1810">Dataset</span></span>
<span data-ttu-id="555cc-1811">Per definire un set di dati MongoDB, impostare il **tipo** del set di dati su **DbCollection**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1812">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1812">Property</span></span> | <span data-ttu-id="555cc-1813">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1813">Description</span></span> | <span data-ttu-id="555cc-1814">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="555cc-1815">collectionName</span></span> |<span data-ttu-id="555cc-1816">Nome della raccolta nel database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="555cc-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="555cc-1817">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1818">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="555cc-1819">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="555cc-1820">Origine MongoDB nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1821">Se si copiano dati da MongoDB, impostare il **tipo di origine** dell'attività di copia su **Source**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1822">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1822">Property</span></span> | <span data-ttu-id="555cc-1823">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1823">Description</span></span> | <span data-ttu-id="555cc-1824">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1824">Allowed values</span></span> | <span data-ttu-id="555cc-1825">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1826">query</span><span class="sxs-lookup"><span data-stu-id="555cc-1826">query</span></span> |<span data-ttu-id="555cc-1827">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-1828">Stringa di query SQL-92.</span><span class="sxs-lookup"><span data-stu-id="555cc-1828">SQL-92 query string.</span></span> <span data-ttu-id="555cc-1829">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-1830">No, se **collectionName** di **set di dati** è specificato</span><span class="sxs-lookup"><span data-stu-id="555cc-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1831">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1832">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="555cc-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="555cc-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-1834">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1834">Linked service</span></span>
<span data-ttu-id="555cc-1835">Per definire un servizio collegato di Amazon S3, impostare il **tipo** di servizio collegato su **AwsAccessKey** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-1836">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1836">Property</span></span> | <span data-ttu-id="555cc-1837">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1837">Description</span></span> | <span data-ttu-id="555cc-1838">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1838">Allowed values</span></span> | <span data-ttu-id="555cc-1839">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="555cc-1840">accessKeyID</span></span> |<span data-ttu-id="555cc-1841">ID della chiave di accesso segreta.</span><span class="sxs-lookup"><span data-stu-id="555cc-1841">ID of the secret access key.</span></span> |<span data-ttu-id="555cc-1842">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1842">string</span></span> |<span data-ttu-id="555cc-1843">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1843">Yes</span></span> |
| <span data-ttu-id="555cc-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="555cc-1844">secretAccessKey</span></span> |<span data-ttu-id="555cc-1845">La stessa chiave di accesso segreta.</span><span class="sxs-lookup"><span data-stu-id="555cc-1845">The secret access key itself.</span></span> |<span data-ttu-id="555cc-1846">La stringa segreta crittografata</span><span class="sxs-lookup"><span data-stu-id="555cc-1846">Encrypted secret string</span></span> |<span data-ttu-id="555cc-1847">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-1848">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="555cc-1849">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1850">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1850">Dataset</span></span>
<span data-ttu-id="555cc-1851">Per definire un set di dati di Amazon S3, impostare il **tipo** di set di dati su **AmazonS3**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1852">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1852">Property</span></span> | <span data-ttu-id="555cc-1853">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1853">Description</span></span> | <span data-ttu-id="555cc-1854">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1854">Allowed values</span></span> | <span data-ttu-id="555cc-1855">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="555cc-1856">bucketName</span></span> |<span data-ttu-id="555cc-1857">Il nome del bucket S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1857">The S3 bucket name.</span></span> |<span data-ttu-id="555cc-1858">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1858">String</span></span> |<span data-ttu-id="555cc-1859">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1859">Yes</span></span> |
| <span data-ttu-id="555cc-1860">key</span><span class="sxs-lookup"><span data-stu-id="555cc-1860">key</span></span> |<span data-ttu-id="555cc-1861">La chiave dell'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1861">The S3 object key.</span></span> |<span data-ttu-id="555cc-1862">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1862">String</span></span> |<span data-ttu-id="555cc-1863">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1863">No</span></span> |
| <span data-ttu-id="555cc-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="555cc-1864">prefix</span></span> |<span data-ttu-id="555cc-1865">Il prefisso per la chiave dell'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="555cc-1866">Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="555cc-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="555cc-1867">Si applica solo quando la chiave è vuota.</span><span class="sxs-lookup"><span data-stu-id="555cc-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="555cc-1868">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1868">String</span></span> |<span data-ttu-id="555cc-1869">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1869">No</span></span> |
| <span data-ttu-id="555cc-1870">version</span><span class="sxs-lookup"><span data-stu-id="555cc-1870">version</span></span> |<span data-ttu-id="555cc-1871">La versione dell'oggetto S3 se è stato abilitato il controllo delle versioni S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="555cc-1872">string</span><span class="sxs-lookup"><span data-stu-id="555cc-1872">String</span></span> |<span data-ttu-id="555cc-1873">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1873">No</span></span> |
| <span data-ttu-id="555cc-1874">format</span><span class="sxs-lookup"><span data-stu-id="555cc-1874">format</span></span> | <span data-ttu-id="555cc-1875">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-1876">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-1877">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-1878">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-1879">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1879">No</span></span> | |
| <span data-ttu-id="555cc-1880">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-1880">compression</span></span> | <span data-ttu-id="555cc-1881">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-1882">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-1883">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-1884">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-1885">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="555cc-1886">bucketName + chiave specifica la posizione dell'oggetto S3 in cui il bucket è il contenitore radice per gli oggetti S3 e la chiave rappresenta il percorso completo all'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="555cc-1887">Esempio: set di dati di esempio con prefisso</span><span class="sxs-lookup"><span data-stu-id="555cc-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="555cc-1888">Esempio: set di dati di esempio con versione</span><span class="sxs-lookup"><span data-stu-id="555cc-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="555cc-1889">Esempio: percorsi dinamici per S3</span><span class="sxs-lookup"><span data-stu-id="555cc-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="555cc-1890">Nell'esempio, vengono utilizzati dei valori fissi per le proprietà chiave e bucketName nel set di dati Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="555cc-1891">È possibile fare in modo che Data Factory calcoli la chiave e il bucketName dinamicamente in fase di runtime utilizzando le variabili di sistema, come SliceStart.</span><span class="sxs-lookup"><span data-stu-id="555cc-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="555cc-1892">È possibile eseguire la stessa operazione per la proprietà prefix di un set di dati di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="555cc-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="555cc-1893">Per un elenco delle funzioni e delle variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="555cc-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="555cc-1894">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="555cc-1895">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1896">Se si copiano dati da Amazon S3, impostare il **tipo di origine** dell'attività di copia su **FileSystemSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="555cc-1897">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1897">Property</span></span> | <span data-ttu-id="555cc-1898">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1898">Description</span></span> | <span data-ttu-id="555cc-1899">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1899">Allowed values</span></span> | <span data-ttu-id="555cc-1900">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1901">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-1901">recursive</span></span> |<span data-ttu-id="555cc-1902">Specifica se elencare in modo ricorsivo gli oggetti S3 sotto la directory.</span><span class="sxs-lookup"><span data-stu-id="555cc-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="555cc-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="555cc-1903">true/false</span></span> |<span data-ttu-id="555cc-1904">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-1905">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="555cc-1906">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="555cc-1907">File system</span><span class="sxs-lookup"><span data-stu-id="555cc-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-1908">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1908">Linked service</span></span>
<span data-ttu-id="555cc-1909">È possibile collegare un file system locale a una data factory di Azure con il servizio collegato del **file server locale**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="555cc-1910">La tabella seguente include le descrizioni degli elementi JSON specifici del servizio collegato del file server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="555cc-1911">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1911">Property</span></span> | <span data-ttu-id="555cc-1912">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1912">Description</span></span> | <span data-ttu-id="555cc-1913">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1914">type</span><span class="sxs-lookup"><span data-stu-id="555cc-1914">type</span></span> |<span data-ttu-id="555cc-1915">Verificare che la proprietà type sia impostata su **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="555cc-1916">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1916">Yes</span></span> |
| <span data-ttu-id="555cc-1917">host</span><span class="sxs-lookup"><span data-stu-id="555cc-1917">host</span></span> |<span data-ttu-id="555cc-1918">Specifica il percorso radice della cartella da copiare.</span><span class="sxs-lookup"><span data-stu-id="555cc-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="555cc-1919">Usare il carattere di escape '\' per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="555cc-1920">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="555cc-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="555cc-1921">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1921">Yes</span></span> |
| <span data-ttu-id="555cc-1922">userid</span><span class="sxs-lookup"><span data-stu-id="555cc-1922">userid</span></span> |<span data-ttu-id="555cc-1923">Specificare l'ID dell'utente che ha accesso al server.</span><span class="sxs-lookup"><span data-stu-id="555cc-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="555cc-1924">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="555cc-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="555cc-1925">password</span><span class="sxs-lookup"><span data-stu-id="555cc-1925">password</span></span> |<span data-ttu-id="555cc-1926">Specificare la password per l'utente (userid).</span><span class="sxs-lookup"><span data-stu-id="555cc-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="555cc-1927">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="555cc-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="555cc-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1928">encryptedCredential</span></span> |<span data-ttu-id="555cc-1929">Specificare le credenziali crittografate che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="555cc-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="555cc-1930">No (se si sceglie di specificare ID utente e password in testo normale)</span><span class="sxs-lookup"><span data-stu-id="555cc-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="555cc-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-1931">gatewayName</span></span> |<span data-ttu-id="555cc-1932">Specifica il nome del gateway che Data Factory deve usare per connettersi al file server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="555cc-1933">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="555cc-1934">Definizioni del percorso della cartella di esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="555cc-1935">Scenario</span><span class="sxs-lookup"><span data-stu-id="555cc-1935">Scenario</span></span> | <span data-ttu-id="555cc-1936">Host nella definizione del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-1936">Host in linked service definition</span></span> | <span data-ttu-id="555cc-1937">folderPath nella definizione del set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1938">Cartella locale nel computer del gateway di gestione dati: </span><span class="sxs-lookup"><span data-stu-id="555cc-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="555cc-1939">Esempi: D:\\\* o D:\cartella\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="555cc-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="555cc-1940">D:\\\\ (per Gateway di gestione dati versione 2.0 e successive)</span><span class="sxs-lookup"><span data-stu-id="555cc-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="555cc-1941">localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati)</span><span class="sxs-lookup"><span data-stu-id="555cc-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="555cc-1942">.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="555cc-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="555cc-1943">D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0)</span><span class="sxs-lookup"><span data-stu-id="555cc-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="555cc-1944">Cartella condivisa remota: </span><span class="sxs-lookup"><span data-stu-id="555cc-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="555cc-1945">Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="555cc-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="555cc-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="555cc-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="555cc-1947">.\\\\ o cartella\\\\sottocartella</span><span class="sxs-lookup"><span data-stu-id="555cc-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="555cc-1948">Esempio: Uso di nome utente e password in testo normale</span><span class="sxs-lookup"><span data-stu-id="555cc-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="555cc-1949">Esempio: Uso di encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="555cc-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="555cc-1950">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-1951">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-1951">Dataset</span></span>
<span data-ttu-id="555cc-1952">Per definire un set di dati di File System, impostare il **tipo** di set di dati su **FileShare**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-1953">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1953">Property</span></span> | <span data-ttu-id="555cc-1954">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1954">Description</span></span> | <span data-ttu-id="555cc-1955">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-1956">folderPath</span></span> |<span data-ttu-id="555cc-1957">Specifica il percorso secondario della cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="555cc-1958">Usare il carattere di escape '\' per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="555cc-1959">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="555cc-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="555cc-1960">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="555cc-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="555cc-1961">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-1961">Yes</span></span> |
| <span data-ttu-id="555cc-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-1962">fileName</span></span> |<span data-ttu-id="555cc-1963">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="555cc-1964">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="555cc-1965">Quando fileName non viene specificato per un set di dati di output, il formato del nome del file generato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="555cc-1966">`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="555cc-1967">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1967">No</span></span> |
| <span data-ttu-id="555cc-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="555cc-1968">fileFilter</span></span> |<span data-ttu-id="555cc-1969">Specificare un filtro da usare per selezionare un sottoinsieme di file in folderPath anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="555cc-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="555cc-1970">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="555cc-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="555cc-1971">Esempio 1: "fileFilter": "*. log"</span><span class="sxs-lookup"><span data-stu-id="555cc-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="555cc-1972">Esempio 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="555cc-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="555cc-1973">Si noti che fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="555cc-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="555cc-1974">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1974">No</span></span> |
| <span data-ttu-id="555cc-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-1975">partitionedBy</span></span> |<span data-ttu-id="555cc-1976">È possibile usare partitionedBy per specificare un valore folderPath/fileName dinamico per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="555cc-1977">Un esempio è folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-1978">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1978">No</span></span> |
| <span data-ttu-id="555cc-1979">format</span><span class="sxs-lookup"><span data-stu-id="555cc-1979">format</span></span> | <span data-ttu-id="555cc-1980">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-1981">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-1982">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-1983">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-1984">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1984">No</span></span> |
| <span data-ttu-id="555cc-1985">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-1985">compression</span></span> | <span data-ttu-id="555cc-1986">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-1987">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce).</span><span class="sxs-lookup"><span data-stu-id="555cc-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-1988">vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-1989">No</span><span class="sxs-lookup"><span data-stu-id="555cc-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="555cc-1990">Non è possibile usare fileName e fileFilter contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-1991">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-1992">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="555cc-1993">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="555cc-1994">Se si copiano dati da File System, impostare il **tipo di origine** dell'attività di copia su **FileSystemSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-1995">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-1995">Property</span></span> | <span data-ttu-id="555cc-1996">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-1996">Description</span></span> | <span data-ttu-id="555cc-1997">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-1997">Allowed values</span></span> | <span data-ttu-id="555cc-1998">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-1999">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-1999">recursive</span></span> |<span data-ttu-id="555cc-2000">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-2001">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-2001">True, False (default)</span></span> |<span data-ttu-id="555cc-2002">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2003">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="555cc-2004">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="555cc-2005">Sink File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="555cc-2006">Se si copiano dati in File System, impostare il **tipo di sink** dell'attività di copia su **FileSystemSink**e specificare le proprietà seguenti nella sezione **sink**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="555cc-2007">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2007">Property</span></span> | <span data-ttu-id="555cc-2008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2008">Description</span></span> | <span data-ttu-id="555cc-2009">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2009">Allowed values</span></span> | <span data-ttu-id="555cc-2010">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="555cc-2011">copyBehavior</span></span> |<span data-ttu-id="555cc-2012">Definisce il comportamento di copia quando l'origine è BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="555cc-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="555cc-2013">**PreserveHierarchy:** mantiene la gerarchia dei file nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="555cc-2014">Il percorso relativo del file di origine nella cartella di origine è identico al percorso relativo del file di destinazione nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="555cc-2015">**FlattenHierarchy**: tutti i file della cartella di origine vengono creati nel primo livello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="555cc-2016">Il nome dei file di destinazione viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="555cc-2017">**MergeFiles**: unisce tutti i file della cartella di origine in un solo file.</span><span class="sxs-lookup"><span data-stu-id="555cc-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="555cc-2018">Se il nome file/BLOB viene specificato, il nome del file unito sarà il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="555cc-2019">In caso contrario, verrà usato un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="555cc-2020">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2020">No</span></span> |
<span data-ttu-id="555cc-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="555cc-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-2022">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-2023">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="555cc-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-2025">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2025">Linked service</span></span>
<span data-ttu-id="555cc-2026">Per definire un servizio collegato di FTP, impostare il **tipo** di servizio collegato su **FtpServer** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2027">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2027">Property</span></span> | <span data-ttu-id="555cc-2028">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2028">Description</span></span> | <span data-ttu-id="555cc-2029">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2029">Required</span></span> | <span data-ttu-id="555cc-2030">Default</span><span class="sxs-lookup"><span data-stu-id="555cc-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2031">host</span><span class="sxs-lookup"><span data-stu-id="555cc-2031">host</span></span> |<span data-ttu-id="555cc-2032">Nome o indirizzo IP del server FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="555cc-2033">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="555cc-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2034">authenticationType</span></span> |<span data-ttu-id="555cc-2035">Specificare il tipo di autenticazione</span><span class="sxs-lookup"><span data-stu-id="555cc-2035">Specify authentication type</span></span> |<span data-ttu-id="555cc-2036">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2036">Yes</span></span> |<span data-ttu-id="555cc-2037">Di base, anonimo</span><span class="sxs-lookup"><span data-stu-id="555cc-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="555cc-2038">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2038">username</span></span> |<span data-ttu-id="555cc-2039">Utente che ha accesso al server FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="555cc-2040">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="555cc-2041">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2041">password</span></span> |<span data-ttu-id="555cc-2042">Password per l'utente (nome utente)</span><span class="sxs-lookup"><span data-stu-id="555cc-2042">Password for the user (username)</span></span> |<span data-ttu-id="555cc-2043">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="555cc-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-2044">encryptedCredential</span></span> |<span data-ttu-id="555cc-2045">Credenziali crittografate per accedere al server FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="555cc-2046">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="555cc-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2047">gatewayName</span></span> |<span data-ttu-id="555cc-2048">Nome del gateway di Gateway di gestione dati per connettersi a un server FTP locale</span><span class="sxs-lookup"><span data-stu-id="555cc-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="555cc-2049">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="555cc-2050">port</span><span class="sxs-lookup"><span data-stu-id="555cc-2050">port</span></span> |<span data-ttu-id="555cc-2051">Porta su cui è in ascolto il server FTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="555cc-2052">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2052">No</span></span> |<span data-ttu-id="555cc-2053">21</span><span class="sxs-lookup"><span data-stu-id="555cc-2053">21</span></span> |
| <span data-ttu-id="555cc-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="555cc-2054">enableSsl</span></span> |<span data-ttu-id="555cc-2055">Specificare se usare FTP su un canale SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="555cc-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="555cc-2056">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2056">No</span></span> |<span data-ttu-id="555cc-2057">true</span><span class="sxs-lookup"><span data-stu-id="555cc-2057">true</span></span> |
| <span data-ttu-id="555cc-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="555cc-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="555cc-2059">Specificare se abilitare la convalida del certificato SSL del server quando si usa FTP sul canale SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="555cc-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="555cc-2060">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2060">No</span></span> |<span data-ttu-id="555cc-2061">true</span><span class="sxs-lookup"><span data-stu-id="555cc-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="555cc-2062">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="555cc-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="555cc-2063">Esempio: uso di nome utente e password in testo normale per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="555cc-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="555cc-2064">Esempio: uso di porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="555cc-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="555cc-2065">Esempio: uso di encryptedCredential per autenticazione e gateway</span><span class="sxs-lookup"><span data-stu-id="555cc-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="555cc-2066">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-2067">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2067">Dataset</span></span>
<span data-ttu-id="555cc-2068">Per definire un set di dati di FTP, impostare il **tipo** di set di dati su **FileShare**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2069">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2069">Property</span></span> | <span data-ttu-id="555cc-2070">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2070">Description</span></span> | <span data-ttu-id="555cc-2071">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-2072">folderPath</span></span> |<span data-ttu-id="555cc-2073">Sottopercorso alla cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2073">Sub path to the folder.</span></span> <span data-ttu-id="555cc-2074">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="555cc-2075">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="555cc-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="555cc-2076">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="555cc-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="555cc-2077">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2077">Yes</span></span> 
| <span data-ttu-id="555cc-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-2078">fileName</span></span> |<span data-ttu-id="555cc-2079">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="555cc-2080">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="555cc-2081">Quando fileName non viene specificato per un set di dati di output, il nome del file generato sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="555cc-2082">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="555cc-2083">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2083">No</span></span> |
| <span data-ttu-id="555cc-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="555cc-2084">fileFilter</span></span> |<span data-ttu-id="555cc-2085">Specificare un filtro da usare per selezionare un sottoinsieme di file in folderPath anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="555cc-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="555cc-2086">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="555cc-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="555cc-2087">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="555cc-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="555cc-2088">Esempio 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="555cc-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="555cc-2089">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="555cc-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="555cc-2090">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="555cc-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="555cc-2091">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2091">No</span></span> |
| <span data-ttu-id="555cc-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-2092">partitionedBy</span></span> |<span data-ttu-id="555cc-2093">partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="555cc-2094">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-2095">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2095">No</span></span> |
| <span data-ttu-id="555cc-2096">format</span><span class="sxs-lookup"><span data-stu-id="555cc-2096">format</span></span> | <span data-ttu-id="555cc-2097">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-2098">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-2099">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-2100">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-2101">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2101">No</span></span> |
| <span data-ttu-id="555cc-2102">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-2102">compression</span></span> | <span data-ttu-id="555cc-2103">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-2104">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce).</span><span class="sxs-lookup"><span data-stu-id="555cc-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-2105">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-2106">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2106">No</span></span> |
| <span data-ttu-id="555cc-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="555cc-2107">useBinaryTransfer</span></span> |<span data-ttu-id="555cc-2108">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="555cc-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="555cc-2109">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="555cc-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="555cc-2110">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="555cc-2110">Default value: True.</span></span> <span data-ttu-id="555cc-2111">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="555cc-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="555cc-2112">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="555cc-2113">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-2114">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="555cc-2115">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="555cc-2116">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2117">Se si copiano dati da un server FTP, impostare il **tipo di origine** dell'attività di copia su **FileSystemSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2118">Property</span></span> | <span data-ttu-id="555cc-2119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2119">Description</span></span> | <span data-ttu-id="555cc-2120">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2120">Allowed values</span></span> | <span data-ttu-id="555cc-2121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2122">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-2122">recursive</span></span> |<span data-ttu-id="555cc-2123">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-2124">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-2124">True, False (default)</span></span> |<span data-ttu-id="555cc-2125">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2126">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="555cc-2127">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="555cc-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="555cc-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-2129">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2129">Linked service</span></span>
<span data-ttu-id="555cc-2130">Per definire un servizio collegato di HDFS, impostare il **tipo** di servizio collegato su **Hdfs** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2131">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2131">Property</span></span> | <span data-ttu-id="555cc-2132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2132">Description</span></span> | <span data-ttu-id="555cc-2133">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2134">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2134">type</span></span> |<span data-ttu-id="555cc-2135">La proprietà type deve essere impostata su: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="555cc-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="555cc-2136">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2136">Yes</span></span> |
| <span data-ttu-id="555cc-2137">Url</span><span class="sxs-lookup"><span data-stu-id="555cc-2137">Url</span></span> |<span data-ttu-id="555cc-2138">URL di HDFS</span><span class="sxs-lookup"><span data-stu-id="555cc-2138">URL to the HDFS</span></span> |<span data-ttu-id="555cc-2139">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2139">Yes</span></span> |
| <span data-ttu-id="555cc-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2140">authenticationType</span></span> |<span data-ttu-id="555cc-2141">Anonima o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="555cc-2142">Per usare l'**autenticazione Kerberos** per il connettore HDFS, fare riferimento a [questa sezione](#use-kerberos-authentication-for-hdfs-connector) per impostare correttamente l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="555cc-2143">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2143">Yes</span></span> |
| <span data-ttu-id="555cc-2144">userName</span><span class="sxs-lookup"><span data-stu-id="555cc-2144">userName</span></span> |<span data-ttu-id="555cc-2145">Nome utente per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="555cc-2146">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="555cc-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="555cc-2147">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2147">password</span></span> |<span data-ttu-id="555cc-2148">Password per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="555cc-2149">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="555cc-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="555cc-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2150">gatewayName</span></span> |<span data-ttu-id="555cc-2151">Nome del gateway che il servizio Data Factory deve usare per connettersi a HDFS.</span><span class="sxs-lookup"><span data-stu-id="555cc-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="555cc-2152">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2152">Yes</span></span> |
| <span data-ttu-id="555cc-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-2153">encryptedCredential</span></span> |<span data-ttu-id="555cc-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) delle credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="555cc-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="555cc-2155">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="555cc-2156">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="555cc-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="555cc-2157">Esempio: uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="555cc-2158">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-2159">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2159">Dataset</span></span>
<span data-ttu-id="555cc-2160">Per definire un set di dati di HDFS, impostare il **tipo** di set di dati su **FileShare**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2161">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2161">Property</span></span> | <span data-ttu-id="555cc-2162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2162">Description</span></span> | <span data-ttu-id="555cc-2163">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-2164">folderPath</span></span> |<span data-ttu-id="555cc-2165">Percorso della cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2165">Path to the folder.</span></span> <span data-ttu-id="555cc-2166">Esempio: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="555cc-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="555cc-2167">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="555cc-2168">Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.</span><span class="sxs-lookup"><span data-stu-id="555cc-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="555cc-2169">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="555cc-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="555cc-2170">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2170">Yes</span></span> |
| <span data-ttu-id="555cc-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-2171">fileName</span></span> |<span data-ttu-id="555cc-2172">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="555cc-2173">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="555cc-2174">Quando fileName non viene specificato per un set di dati di output, il nome del file generato sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="555cc-2175">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="555cc-2176">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2176">No</span></span> |
| <span data-ttu-id="555cc-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-2177">partitionedBy</span></span> |<span data-ttu-id="555cc-2178">partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="555cc-2179">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-2180">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2180">No</span></span> |
| <span data-ttu-id="555cc-2181">format</span><span class="sxs-lookup"><span data-stu-id="555cc-2181">format</span></span> | <span data-ttu-id="555cc-2182">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-2183">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-2184">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-2185">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-2186">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2186">No</span></span> |
| <span data-ttu-id="555cc-2187">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-2187">compression</span></span> | <span data-ttu-id="555cc-2188">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-2189">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-2190">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-2191">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-2192">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="555cc-2193">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-2194">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="555cc-2195">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="555cc-2196">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2197">Se si copiano dati da HDFS, impostare il **tipo di origine** dell'attività di copia su **FileSystemSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="555cc-2198">**FileSystemSource** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="555cc-2199">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2199">Property</span></span> | <span data-ttu-id="555cc-2200">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2200">Description</span></span> | <span data-ttu-id="555cc-2201">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2201">Allowed values</span></span> | <span data-ttu-id="555cc-2202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2203">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-2203">recursive</span></span> |<span data-ttu-id="555cc-2204">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-2205">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-2205">True, False (default)</span></span> |<span data-ttu-id="555cc-2206">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2207">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="555cc-2208">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="555cc-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-2210">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2210">Linked service</span></span>
<span data-ttu-id="555cc-2211">Per definire un servizio collegato di SFTP, impostare il **tipo** di servizio collegato su **Sftp** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2212">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2212">Property</span></span> | <span data-ttu-id="555cc-2213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2213">Description</span></span> | <span data-ttu-id="555cc-2214">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2215">host</span><span class="sxs-lookup"><span data-stu-id="555cc-2215">host</span></span> | <span data-ttu-id="555cc-2216">Nome o indirizzo IP del server SFTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="555cc-2217">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2217">Yes</span></span> |
| <span data-ttu-id="555cc-2218">port</span><span class="sxs-lookup"><span data-stu-id="555cc-2218">port</span></span> |<span data-ttu-id="555cc-2219">Porta su cui è in ascolto il server SFTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="555cc-2220">Il valore predefinito è 21</span><span class="sxs-lookup"><span data-stu-id="555cc-2220">The default value is: 21</span></span> |<span data-ttu-id="555cc-2221">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2221">No</span></span> |
| <span data-ttu-id="555cc-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2222">authenticationType</span></span> |<span data-ttu-id="555cc-2223">Specificare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2223">Specify authentication type.</span></span> <span data-ttu-id="555cc-2224">Valori consentiti: **Base**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="555cc-2225">Fare riferimento alle sezioni [Uso dell'autenticazione di base](#using-basic-authentication) e [Uso dell'autenticazione con chiave pubblica SSH](#using-ssh-public-key-authentication) rispettivamente per vedere altre proprietà ed esempi JSON.</span><span class="sxs-lookup"><span data-stu-id="555cc-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="555cc-2226">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2226">Yes</span></span> |
| <span data-ttu-id="555cc-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="555cc-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="555cc-2228">Specificare se si desidera ignorare la convalida tramite della chiave host.</span><span class="sxs-lookup"><span data-stu-id="555cc-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="555cc-2229">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2229">No.</span></span> <span data-ttu-id="555cc-2230">Il valore predefinito è: falso</span><span class="sxs-lookup"><span data-stu-id="555cc-2230">The default value: false</span></span> |
| <span data-ttu-id="555cc-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="555cc-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="555cc-2232">Specificare le impronte digitali della chiave host.</span><span class="sxs-lookup"><span data-stu-id="555cc-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="555cc-2233">Sì se `skipHostKeyValidation` è impostato su falso.</span><span class="sxs-lookup"><span data-stu-id="555cc-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="555cc-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2234">gatewayName</span></span> |<span data-ttu-id="555cc-2235">Nome del gateway di gestione dati per connettersi a un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="555cc-2236">Sì se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="555cc-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-2237">encryptedCredential</span></span> | <span data-ttu-id="555cc-2238">Credenziali crittografate per accedere al server SFTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="555cc-2239">Generato automaticamente quando si specifica l'autenticazione di base (nome utente e password) o l'autenticazione SshPublicKey (nome utente e percorso della chiave privato o contenuto) nella copia guidata o nella finestra di dialogo popup ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="555cc-2240">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2240">No.</span></span> <span data-ttu-id="555cc-2241">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="555cc-2242">Esempio: uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="555cc-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="555cc-2243">Per usare l'autenticazione di base, impostare `authenticationType` come `Basic` e specificare le proprietà seguenti oltre a quelle generiche del connettore SFTP introdotte nell'ultima sezione:</span><span class="sxs-lookup"><span data-stu-id="555cc-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="555cc-2244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2244">Property</span></span> | <span data-ttu-id="555cc-2245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2245">Description</span></span> | <span data-ttu-id="555cc-2246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2247">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2247">username</span></span> | <span data-ttu-id="555cc-2248">Utente che ha accesso al server SFTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="555cc-2249">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2249">Yes</span></span> |
| <span data-ttu-id="555cc-2250">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2250">password</span></span> | <span data-ttu-id="555cc-2251">Password per l'utente (nome utente).</span><span class="sxs-lookup"><span data-stu-id="555cc-2251">Password for the user (username).</span></span> | <span data-ttu-id="555cc-2252">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="555cc-2253">Esempio: autenticazione di base con credenziali crittografate**</span><span class="sxs-lookup"><span data-stu-id="555cc-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="555cc-2254">Esempio: uso dell'autenticazione con chiave pubblica SSH:**</span><span class="sxs-lookup"><span data-stu-id="555cc-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="555cc-2255">Per usare l'autenticazione di base, impostare `authenticationType` come `SshPublicKey` e specificare le proprietà seguenti oltre a quelle generiche del connettore SFTP introdotte nell'ultima sezione:</span><span class="sxs-lookup"><span data-stu-id="555cc-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="555cc-2256">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2256">Property</span></span> | <span data-ttu-id="555cc-2257">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2257">Description</span></span> | <span data-ttu-id="555cc-2258">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2259">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2259">username</span></span> |<span data-ttu-id="555cc-2260">Utente che ha accesso al server SFTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="555cc-2261">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2261">Yes</span></span> |
| <span data-ttu-id="555cc-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="555cc-2262">privateKeyPath</span></span> | <span data-ttu-id="555cc-2263">Specificare un percorso assoluto al file di chiave privato a cui il gateway può accedere.</span><span class="sxs-lookup"><span data-stu-id="555cc-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="555cc-2264">Specificare `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="555cc-2265">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="555cc-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="555cc-2266">privateKeyContent</span></span> | <span data-ttu-id="555cc-2267">Una stringa serializzata del contenuto di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="555cc-2268">La copia guidata può leggere il file di chiave privata ed estrarre automaticamente il contenuto della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="555cc-2269">Se si usa un qualsiasi altro strumento/SDK, usare la proprietà privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="555cc-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="555cc-2270">Specificare `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="555cc-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="555cc-2271">passPhrase</span></span> | <span data-ttu-id="555cc-2272">Specificare la passphrase o la password per decrittografare la chiave privata se il file della chiave è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="555cc-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="555cc-2273">Sì se il file della chiave privata è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="555cc-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="555cc-2274">Esempio: autenticazione SshPublicKey con contenuto della chiave privata**</span><span class="sxs-lookup"><span data-stu-id="555cc-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="555cc-2275">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-2276">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2276">Dataset</span></span>
<span data-ttu-id="555cc-2277">Per definire un set di dati di SFTP, impostare il **tipo** di set di dati su **FileShare**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2278">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2278">Property</span></span> | <span data-ttu-id="555cc-2279">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2279">Description</span></span> | <span data-ttu-id="555cc-2280">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="555cc-2281">folderPath</span></span> |<span data-ttu-id="555cc-2282">Sottopercorso alla cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2282">Sub path to the folder.</span></span> <span data-ttu-id="555cc-2283">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="555cc-2284">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="555cc-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="555cc-2285">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="555cc-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="555cc-2286">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2286">Yes</span></span> |
| <span data-ttu-id="555cc-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="555cc-2287">fileName</span></span> |<span data-ttu-id="555cc-2288">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="555cc-2289">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="555cc-2290">Quando fileName non viene specificato per un set di dati di output, il nome del file generato sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="555cc-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="555cc-2291">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="555cc-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="555cc-2292">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2292">No</span></span> |
| <span data-ttu-id="555cc-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="555cc-2293">fileFilter</span></span> |<span data-ttu-id="555cc-2294">Specificare un filtro da usare per selezionare un sottoinsieme di file in folderPath anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="555cc-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="555cc-2295">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="555cc-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="555cc-2296">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="555cc-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="555cc-2297">Esempio 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="555cc-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="555cc-2298">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="555cc-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="555cc-2299">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="555cc-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="555cc-2300">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2300">No</span></span> |
| <span data-ttu-id="555cc-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="555cc-2301">partitionedBy</span></span> |<span data-ttu-id="555cc-2302">partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="555cc-2303">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="555cc-2304">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2304">No</span></span> |
| <span data-ttu-id="555cc-2305">format</span><span class="sxs-lookup"><span data-stu-id="555cc-2305">format</span></span> | <span data-ttu-id="555cc-2306">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-2307">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="555cc-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="555cc-2308">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="555cc-2309">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="555cc-2310">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2310">No</span></span> |
| <span data-ttu-id="555cc-2311">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-2311">compression</span></span> | <span data-ttu-id="555cc-2312">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-2313">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-2314">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-2315">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-2316">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2316">No</span></span> |
| <span data-ttu-id="555cc-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="555cc-2317">useBinaryTransfer</span></span> |<span data-ttu-id="555cc-2318">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="555cc-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="555cc-2319">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="555cc-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="555cc-2320">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="555cc-2320">Default value: True.</span></span> <span data-ttu-id="555cc-2321">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="555cc-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="555cc-2322">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="555cc-2323">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-2324">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="555cc-2325">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="555cc-2326">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2327">Se si copiano dati da un'origine SFTP, impostare il **tipo di origine** dell'attività di copia su **FileSystemSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2328">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2328">Property</span></span> | <span data-ttu-id="555cc-2329">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2329">Description</span></span> | <span data-ttu-id="555cc-2330">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2330">Allowed values</span></span> | <span data-ttu-id="555cc-2331">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2332">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="555cc-2332">recursive</span></span> |<span data-ttu-id="555cc-2333">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="555cc-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="555cc-2334">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-2334">True, False (default)</span></span> |<span data-ttu-id="555cc-2335">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="555cc-2336">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="555cc-2337">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="555cc-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="555cc-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-2339">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2339">Linked service</span></span>
<span data-ttu-id="555cc-2340">Per definire un servizio collegato di HTTP, impostare il **tipo** di servizio collegato su **Http** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2341">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2341">Property</span></span> | <span data-ttu-id="555cc-2342">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2342">Description</span></span> | <span data-ttu-id="555cc-2343">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2344">URL</span><span class="sxs-lookup"><span data-stu-id="555cc-2344">url</span></span> | <span data-ttu-id="555cc-2345">URL di base al server Web</span><span class="sxs-lookup"><span data-stu-id="555cc-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="555cc-2346">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2346">Yes</span></span> |
| <span data-ttu-id="555cc-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2347">authenticationType</span></span> | <span data-ttu-id="555cc-2348">Specifica il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2348">Specifies the authentication type.</span></span> <span data-ttu-id="555cc-2349">I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="555cc-2350">Fare riferimento alle sezioni sotto questa tabella per altre proprietà e altri esempi JSON per questi tipi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="555cc-2351">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2351">Yes</span></span> |
| <span data-ttu-id="555cc-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="555cc-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="555cc-2353">Specificare se abilitare la convalida del certificato SSL del server se l'origine è un server Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="555cc-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="555cc-2354">No, il valore predefinito è true</span><span class="sxs-lookup"><span data-stu-id="555cc-2354">No, default is true</span></span> |
| <span data-ttu-id="555cc-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2355">gatewayName</span></span> | <span data-ttu-id="555cc-2356">Nome del gateway di gestione dati per connettersi a un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="555cc-2357">Sì se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="555cc-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-2358">encryptedCredential</span></span> | <span data-ttu-id="555cc-2359">Credenziali crittografate per accedere all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="555cc-2360">Generate automaticamente quando si configurano le informazioni di autenticazione nella procedura di copia guidata o nella finestra di dialogo popup ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="555cc-2361">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2361">No.</span></span> <span data-ttu-id="555cc-2362">Applicare solo se si copiano i dati da un server HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="555cc-2363">Esempio: uso dell'autenticazione di base, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="555cc-2364">Impostare `authenticationType` come `Basic`, `Digest`, o `Windows` e specificare le proprietà seguenti oltre a quelle generiche del connettore HTTP illustrate in precedenza:</span><span class="sxs-lookup"><span data-stu-id="555cc-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="555cc-2365">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2365">Property</span></span> | <span data-ttu-id="555cc-2366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2366">Description</span></span> | <span data-ttu-id="555cc-2367">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2368">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2368">username</span></span> | <span data-ttu-id="555cc-2369">Nome utente per accedere all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="555cc-2370">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2370">Yes</span></span> |
| <span data-ttu-id="555cc-2371">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2371">password</span></span> | <span data-ttu-id="555cc-2372">Password per l'utente (nome utente).</span><span class="sxs-lookup"><span data-stu-id="555cc-2372">Password for the user (username).</span></span> | <span data-ttu-id="555cc-2373">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="555cc-2374">Esempio: uso dell'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="555cc-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="555cc-2375">Per usare l'autenticazione di base, impostare `authenticationType` come `ClientCertificate` e specificare le proprietà seguenti oltre a quelle generiche del connettore HTTP introdotte in precedenza:</span><span class="sxs-lookup"><span data-stu-id="555cc-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="555cc-2376">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2376">Property</span></span> | <span data-ttu-id="555cc-2377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2377">Description</span></span> | <span data-ttu-id="555cc-2378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="555cc-2379">embeddedCertData</span></span> | <span data-ttu-id="555cc-2380">Contenuto con codifica Base 64 dei dati binari del file di scambio di informazioni personali (PFX, Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="555cc-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="555cc-2381">Specificare `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="555cc-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="555cc-2382">certThumbprint</span></span> | <span data-ttu-id="555cc-2383">L'identificazione personale del certificato installato nell'archivio certificati del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="555cc-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="555cc-2384">Applicare solo se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="555cc-2385">Specificare `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="555cc-2386">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2386">password</span></span> | <span data-ttu-id="555cc-2387">Password associata al certificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="555cc-2388">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2388">No</span></span> |

<span data-ttu-id="555cc-2389">Se si usa `certThumbprint` per l'autenticazione e il certificato è installato nell'archivio personale del computer locale, è necessario concedere l'autorizzazione di lettura per il servizio gateway:</span><span class="sxs-lookup"><span data-stu-id="555cc-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="555cc-2390">Avviare Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="555cc-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="555cc-2391">Aggiungere lo snap-in **Certificati** con il **Computer locale** come destinazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="555cc-2392">Espandere **Certificati**, **Personali** e fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="555cc-2393">Fare clic con il tasto destro del mouse sul certificato dall'archivio personale, quindi selezionare **Tutte le attività**->**Gestisci chiavi private...**</span><span class="sxs-lookup"><span data-stu-id="555cc-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="555cc-2394">Nella scheda **Sicurezza** aggiungere l'account utente in cui è in esecuzione il Servizio host di Gateway di gestione dati con l'accesso in lettura al certificato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="555cc-2395">**Esempio: uso del certificato client:** questo servizio collegato collega la data factory a un server Web HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="555cc-2396">Usa un file del certificato client installato nel computer che dispone del Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="555cc-2397">Esempio: utilizzo di un certificato client in un file</span><span class="sxs-lookup"><span data-stu-id="555cc-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="555cc-2398">Questo servizio collegato collega la data factory a un server Web HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="555cc-2399">Usa un file del certificato client nel computer con installato il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="555cc-2400">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-2401">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2401">Dataset</span></span>
<span data-ttu-id="555cc-2402">Per definire un set di dati di HTTP, impostare il **tipo** di set di dati su **Http**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2403">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2403">Property</span></span> | <span data-ttu-id="555cc-2404">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2404">Description</span></span> | <span data-ttu-id="555cc-2405">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="555cc-2406">relativeUrl</span></span> | <span data-ttu-id="555cc-2407">URL relativo della risorsa che contiene i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="555cc-2408">Quando non è specificato alcun percorso, viene usato solo l'URL specificato nella definizione del servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="555cc-2409">Per creare un URL dinamico, è possibile usare le [unzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md), ad esempio: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="555cc-2410">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2410">No</span></span> |
| <span data-ttu-id="555cc-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="555cc-2411">requestMethod</span></span> | <span data-ttu-id="555cc-2412">Metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2412">Http method.</span></span> <span data-ttu-id="555cc-2413">I valori consentiti sono **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="555cc-2414">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2414">No.</span></span> <span data-ttu-id="555cc-2415">Il valore predefinito è `GET`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="555cc-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="555cc-2416">additionalHeaders</span></span> | <span data-ttu-id="555cc-2417">Intestazioni richiesta HTTP aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="555cc-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="555cc-2418">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2418">No</span></span> |
| <span data-ttu-id="555cc-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="555cc-2419">requestBody</span></span> | <span data-ttu-id="555cc-2420">Il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="555cc-2420">Body for HTTP request.</span></span> | <span data-ttu-id="555cc-2421">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2421">No</span></span> |
| <span data-ttu-id="555cc-2422">format</span><span class="sxs-lookup"><span data-stu-id="555cc-2422">format</span></span> | <span data-ttu-id="555cc-2423">Se si desidera semplicemente **recuperare i dati dall'endpoint HTTP così come sono** senza analizzarli, ignorare questa impostazione di formato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="555cc-2424">Se si desidera analizzare i contenuti di risposta HTTP durante la copia, sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="555cc-2425">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="555cc-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="555cc-2426">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2426">No</span></span> |
| <span data-ttu-id="555cc-2427">compressione</span><span class="sxs-lookup"><span data-stu-id="555cc-2427">compression</span></span> | <span data-ttu-id="555cc-2428">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="555cc-2429">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="555cc-2430">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="555cc-2431">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="555cc-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="555cc-2432">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="555cc-2433">Esempio: usando il metodo GET (predefinito)</span><span class="sxs-lookup"><span data-stu-id="555cc-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="555cc-2434">Esempio: usando il metodo POST</span><span class="sxs-lookup"><span data-stu-id="555cc-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="555cc-2435">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="555cc-2436">Origine HTTP nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2437">Se si copiano dati da un'origine HTTP, impostare il **tipo di origine** dell'attività di copia su **HttpSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2438">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2438">Property</span></span> | <span data-ttu-id="555cc-2439">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2439">Description</span></span> | <span data-ttu-id="555cc-2440">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="555cc-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="555cc-2441">httpRequestTimeout</span></span> | <span data-ttu-id="555cc-2442">Il timeout (TimeSpan) durante il quale la richiesta HTTP attende una risposta.</span><span class="sxs-lookup"><span data-stu-id="555cc-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="555cc-2443">Si tratta del timeout per ottenere una risposta, non per leggere i dati della risposta stessa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="555cc-2444">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2444">No.</span></span> <span data-ttu-id="555cc-2445">Valore predefinito: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="555cc-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-2446">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-2447">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="555cc-2448">OData</span><span class="sxs-lookup"><span data-stu-id="555cc-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-2449">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2449">Linked service</span></span>
<span data-ttu-id="555cc-2450">Per definire un servizio collegato di OData, impostare il **tipo** di servizio collegato su **OData** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2451">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2451">Property</span></span> | <span data-ttu-id="555cc-2452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2452">Description</span></span> | <span data-ttu-id="555cc-2453">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2454">URL</span><span class="sxs-lookup"><span data-stu-id="555cc-2454">url</span></span> |<span data-ttu-id="555cc-2455">URL del servizio OData.</span><span class="sxs-lookup"><span data-stu-id="555cc-2455">Url of the OData service.</span></span> |<span data-ttu-id="555cc-2456">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2456">Yes</span></span> |
| <span data-ttu-id="555cc-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2457">authenticationType</span></span> |<span data-ttu-id="555cc-2458">Tipo di autenticazione usato per connettersi all'origine OData.</span><span class="sxs-lookup"><span data-stu-id="555cc-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="555cc-2459">Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="555cc-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="555cc-2460">Per OData locale, i valori possibili sono Anonima, Di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="555cc-2461">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2461">Yes</span></span> |
| <span data-ttu-id="555cc-2462">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2462">username</span></span> |<span data-ttu-id="555cc-2463">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="555cc-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="555cc-2464">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="555cc-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="555cc-2465">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2465">password</span></span> |<span data-ttu-id="555cc-2466">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-2467">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="555cc-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="555cc-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="555cc-2468">authorizedCredential</span></span> |<span data-ttu-id="555cc-2469">Se si usa OAuth, fare clic sul pulsante **Autorizza** nella procedura guidata di copia di Data Factory o nell'Editor e immettere le credenziali. Il valore di questa proprietà viene quindi generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="555cc-2470">Sì (solo se si usa l'autenticazione OAuth)</span><span class="sxs-lookup"><span data-stu-id="555cc-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="555cc-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2471">gatewayName</span></span> |<span data-ttu-id="555cc-2472">Nome del gateway che il servizio Data Factory deve usare per connettersi al servizio OData locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="555cc-2473">Specificare solo se si copiano dati da un'origine OData locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="555cc-2474">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="555cc-2475">Esempio - Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="555cc-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="555cc-2476">Esempio - Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="555cc-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="555cc-2477">Esempio - Uso dell'autenticazione Windows per accedere all'origine OData locale</span><span class="sxs-lookup"><span data-stu-id="555cc-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="555cc-2478">Esempio - Uso dell'autenticazione OAuth per accedere all'origine OData cloud</span><span class="sxs-lookup"><span data-stu-id="555cc-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="555cc-2479">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="555cc-2480">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2480">Dataset</span></span>
<span data-ttu-id="555cc-2481">Per definire un set di dati di OData, impostare il **tipo** di set di dati su **ODataResource**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2482">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2482">Property</span></span> | <span data-ttu-id="555cc-2483">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2483">Description</span></span> | <span data-ttu-id="555cc-2484">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2485">path</span><span class="sxs-lookup"><span data-stu-id="555cc-2485">path</span></span> |<span data-ttu-id="555cc-2486">Percorso della risorsa OData</span><span class="sxs-lookup"><span data-stu-id="555cc-2486">Path to the OData resource</span></span> |<span data-ttu-id="555cc-2487">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2488">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="555cc-2489">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-2490">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2491">Se si copiano dati da un'origine OData, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2492">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2492">Property</span></span> | <span data-ttu-id="555cc-2493">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2493">Description</span></span> | <span data-ttu-id="555cc-2494">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2494">Example</span></span> | <span data-ttu-id="555cc-2495">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2496">query</span><span class="sxs-lookup"><span data-stu-id="555cc-2496">query</span></span> |<span data-ttu-id="555cc-2497">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="555cc-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="555cc-2499">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2500">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="555cc-2501">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="555cc-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="555cc-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-2503">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2503">Linked service</span></span>
<span data-ttu-id="555cc-2504">Per definire un servizio collegato di ODBC, impostare il **tipo** di servizio collegato su **OnPremisesOdbc** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2505">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2505">Property</span></span> | <span data-ttu-id="555cc-2506">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2506">Description</span></span> | <span data-ttu-id="555cc-2507">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-2508">connectionString</span></span> |<span data-ttu-id="555cc-2509">La parte delle credenziali non di accesso della stringa di connessione e una credenziale crittografata facoltativa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="555cc-2510">Vedere gli esempi nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2510">See examples in the following sections.</span></span> |<span data-ttu-id="555cc-2511">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2511">Yes</span></span> |
| <span data-ttu-id="555cc-2512">credential</span><span class="sxs-lookup"><span data-stu-id="555cc-2512">credential</span></span> |<span data-ttu-id="555cc-2513">La parte delle credenziali di accesso della stringa di connessione specificata nel formato di valore della proprietà specifico del driver.</span><span class="sxs-lookup"><span data-stu-id="555cc-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="555cc-2514">Esempio: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="555cc-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="555cc-2515">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2515">No</span></span> |
| <span data-ttu-id="555cc-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2516">authenticationType</span></span> |<span data-ttu-id="555cc-2517">Tipo di autenticazione usato per connettersi all'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="555cc-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="555cc-2518">I valori possibili sono: anonima e di base.</span><span class="sxs-lookup"><span data-stu-id="555cc-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="555cc-2519">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2519">Yes</span></span> |
| <span data-ttu-id="555cc-2520">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2520">username</span></span> |<span data-ttu-id="555cc-2521">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="555cc-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="555cc-2522">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2522">No</span></span> |
| <span data-ttu-id="555cc-2523">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2523">password</span></span> |<span data-ttu-id="555cc-2524">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-2525">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2525">No</span></span> |
| <span data-ttu-id="555cc-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2526">gatewayName</span></span> |<span data-ttu-id="555cc-2527">Nome del gateway che il servizio Data Factory deve usare per connettersi all'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="555cc-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="555cc-2528">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="555cc-2529">Esempio - Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="555cc-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="555cc-2530">Esempio - Uso dell'autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="555cc-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="555cc-2531">È possibile crittografare le credenziali usando il cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx), in Azure PowerShell versione 1.0, oppure [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx), in Azure PowerShell versione 0.9 o precedente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="555cc-2532">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="555cc-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="555cc-2533">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-2534">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2534">Dataset</span></span>
<span data-ttu-id="555cc-2535">Per definire un set di dati di ODBC, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2536">Property</span></span> | <span data-ttu-id="555cc-2537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2537">Description</span></span> | <span data-ttu-id="555cc-2538">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-2539">tableName</span></span> |<span data-ttu-id="555cc-2540">Nome della tabella nell'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="555cc-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="555cc-2541">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="555cc-2542">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-2543">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-2544">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2545">Se si copiano dati da un archivio dati ODBC, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2546">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2546">Property</span></span> | <span data-ttu-id="555cc-2547">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2547">Description</span></span> | <span data-ttu-id="555cc-2548">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2548">Allowed values</span></span> | <span data-ttu-id="555cc-2549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2550">query</span><span class="sxs-lookup"><span data-stu-id="555cc-2550">query</span></span> |<span data-ttu-id="555cc-2551">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-2552">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-2552">SQL query string.</span></span> <span data-ttu-id="555cc-2553">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="555cc-2554">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2555">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="555cc-2556">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="555cc-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="555cc-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="555cc-2558">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2558">Linked service</span></span>
<span data-ttu-id="555cc-2559">Per definire un servizio collegato di Salesforce, impostare il **tipo** di servizio collegato su **Salesforce** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2560">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2560">Property</span></span> | <span data-ttu-id="555cc-2561">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2561">Description</span></span> | <span data-ttu-id="555cc-2562">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="555cc-2563">environmentUrl</span></span> | <span data-ttu-id="555cc-2564">Specificare l'URL dell'istanza di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="555cc-2565">- Il valore predefinito è "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="555cc-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="555cc-2566">- Per copiare i dati dalla sandbox, specificare "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="555cc-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="555cc-2567">- Per copiare i dati dal dominio personalizzato, specificare ad esempio "https://[dominio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="555cc-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="555cc-2568">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2568">No</span></span> |
| <span data-ttu-id="555cc-2569">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2569">username</span></span> |<span data-ttu-id="555cc-2570">Specificare un nome utente per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="555cc-2571">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2571">Yes</span></span> |
| <span data-ttu-id="555cc-2572">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2572">password</span></span> |<span data-ttu-id="555cc-2573">Specificare la password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="555cc-2574">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2574">Yes</span></span> |
| <span data-ttu-id="555cc-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="555cc-2575">securityToken</span></span> |<span data-ttu-id="555cc-2576">Specificare un token di sicurezza per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="555cc-2577">Per istruzioni su come ottenere o reimpostare un token di sicurezza, vedere [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Ottenere un token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="555cc-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="555cc-2578">Per informazioni generali sui token di sicurezza, vedere [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Sicurezza e API).</span><span class="sxs-lookup"><span data-stu-id="555cc-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="555cc-2579">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2580">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="555cc-2581">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-2582">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2582">Dataset</span></span>
<span data-ttu-id="555cc-2583">Per definire un set di dati di Salesforce, impostare il **tipo** di set di dati su **RelationalTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2584">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2584">Property</span></span> | <span data-ttu-id="555cc-2585">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2585">Description</span></span> | <span data-ttu-id="555cc-2586">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="555cc-2587">tableName</span></span> |<span data-ttu-id="555cc-2588">Nome della tabella in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="555cc-2589">No, se è specificata una **query** di **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="555cc-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2590">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="555cc-2591">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="555cc-2592">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2593">Se si copiano dati da Salesforce, impostare il **tipo di origine** dell'attività di copia su **RelationalSource**e specificare le proprietà seguenti nella sezione **source**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="555cc-2594">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2594">Property</span></span> | <span data-ttu-id="555cc-2595">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2595">Description</span></span> | <span data-ttu-id="555cc-2596">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="555cc-2596">Allowed values</span></span> | <span data-ttu-id="555cc-2597">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555cc-2598">query</span><span class="sxs-lookup"><span data-stu-id="555cc-2598">query</span></span> |<span data-ttu-id="555cc-2599">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="555cc-2600">Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="555cc-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="555cc-2601">Ad esempio: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="555cc-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="555cc-2602">No, se è specificato **tableName** per il **set di dati**</span><span class="sxs-lookup"><span data-stu-id="555cc-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2603">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="555cc-2604">La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="555cc-2605">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="555cc-2606">Dati Web</span><span class="sxs-lookup"><span data-stu-id="555cc-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2607">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2607">Linked service</span></span>
<span data-ttu-id="555cc-2608">Per definire un servizio collegato Web, impostare il **tipo** di servizio collegato su **Web** e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2609">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2609">Property</span></span> | <span data-ttu-id="555cc-2610">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2610">Description</span></span> | <span data-ttu-id="555cc-2611">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2612">Url</span><span class="sxs-lookup"><span data-stu-id="555cc-2612">Url</span></span> |<span data-ttu-id="555cc-2613">URL dell'origine Web</span><span class="sxs-lookup"><span data-stu-id="555cc-2613">URL to the Web source</span></span> |<span data-ttu-id="555cc-2614">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2614">Yes</span></span> |
| <span data-ttu-id="555cc-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="555cc-2615">authenticationType</span></span> |<span data-ttu-id="555cc-2616">Anonimo.</span><span class="sxs-lookup"><span data-stu-id="555cc-2616">Anonymous.</span></span> |<span data-ttu-id="555cc-2617">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="555cc-2618">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="555cc-2619">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="555cc-2620">Set di dati</span><span class="sxs-lookup"><span data-stu-id="555cc-2620">Dataset</span></span>
<span data-ttu-id="555cc-2621">Per definire un set di dati Web, impostare il **tipo** di set di dati su **WebTable**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="555cc-2622">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2622">Property</span></span> | <span data-ttu-id="555cc-2623">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2623">Description</span></span> | <span data-ttu-id="555cc-2624">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-2625">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2625">type</span></span> |<span data-ttu-id="555cc-2626">Tipo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2626">type of the dataset.</span></span> <span data-ttu-id="555cc-2627">Deve essere impostato su **WebTable**</span><span class="sxs-lookup"><span data-stu-id="555cc-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="555cc-2628">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2628">Yes</span></span> |
| <span data-ttu-id="555cc-2629">path</span><span class="sxs-lookup"><span data-stu-id="555cc-2629">path</span></span> |<span data-ttu-id="555cc-2630">URL relativo della risorsa che contiene la tabella.</span><span class="sxs-lookup"><span data-stu-id="555cc-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="555cc-2631">No.</span><span class="sxs-lookup"><span data-stu-id="555cc-2631">No.</span></span> <span data-ttu-id="555cc-2632">Quando non è specificato alcun percorso, viene usato solo l'URL specificato nella definizione del servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="555cc-2633">index</span><span class="sxs-lookup"><span data-stu-id="555cc-2633">index</span></span> |<span data-ttu-id="555cc-2634">Indice della tabella nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="555cc-2634">The index of the table in the resource.</span></span> <span data-ttu-id="555cc-2635">Per i passaggi per ottenere l'indice di una tabella in una pagina HTML, vedere la sezione [Ottenere l'indice di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="555cc-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="555cc-2636">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="555cc-2637">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="555cc-2638">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="555cc-2639">Origine Web nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="555cc-2640">Se si copiano dati da una tabella Web, impostare il **tipo di origine** dell'attività di copia su **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="555cc-2641">Quando l'origine nell'attività di copia è di tipo **WebSource**non sono attualmente supportate altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="555cc-2642">Esempio</span><span class="sxs-lookup"><span data-stu-id="555cc-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="555cc-2643">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="555cc-2644">Ambienti di calcolo</span><span class="sxs-lookup"><span data-stu-id="555cc-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="555cc-2645">La tabella seguente elenca gli ambienti di calcolo supportati da Data Factory e le attività di trasformazione eseguibili in tali ambienti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="555cc-2646">Fare clic sul collegamento al calcolo al quale si è interessati per visualizzare gli schemi JSON per il servizio collegato per eseguirne il collegamento a una data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="555cc-2647">Ambiente di calcolo</span><span class="sxs-lookup"><span data-stu-id="555cc-2647">Compute environment</span></span> | <span data-ttu-id="555cc-2648">Attività</span><span class="sxs-lookup"><span data-stu-id="555cc-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="555cc-2649">[Cluster HDInsight su richiesta](#on-demand-azure-hdinsight-cluster) o [il proprio cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="555cc-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="555cc-2650">[Attività personalizzata .NET ](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig](#hdinsight-pig-activity, [attività MapReduce](#hdinsight-mapreduce-activity), [attività di Hadoop Streaming](#hdinsight-streaming-activityd), [attività Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="555cc-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="555cc-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="555cc-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="555cc-2652">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="555cc-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="555cc-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="555cc-2654">[Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="555cc-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="555cc-2655">Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="555cc-2656">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="555cc-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="555cc-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="555cc-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="555cc-2658">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="555cc-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="555cc-2659">Cluster HDInsight di Azure su richiesta</span><span class="sxs-lookup"><span data-stu-id="555cc-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="555cc-2660">Il servizio Data factory di Azure può creare automaticamente un cluster HDInsight su richiesta basato su Windows o Linux per elaborare i dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="555cc-2661">La creazione del cluster avviene nella stessa area dell'account di archiviazione (proprietà linkedServiceName in JSON) associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="555cc-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="555cc-2662">Su questo servizio collegato è possibile eseguire le attività di trasformazione seguenti: [attività personalizzata .NET](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig] (#hdinsight-pig-activity, [attività MapReduce](#hdinsight-mapreduce-activity), [attività di Hadoop Streaming](#hdinsight-streaming-activityd), [attività Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="555cc-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2663">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2663">Linked service</span></span> 
<span data-ttu-id="555cc-2664">La tabella seguente fornisce le descrizioni delle proprietà usate nella definizione JSON di Azure per un servizio collegato HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="555cc-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="555cc-2665">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2665">Property</span></span> | <span data-ttu-id="555cc-2666">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2666">Description</span></span> | <span data-ttu-id="555cc-2667">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2668">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2668">type</span></span> |<span data-ttu-id="555cc-2669">La proprietà type deve essere impostata su **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="555cc-2670">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2670">Yes</span></span> |
| <span data-ttu-id="555cc-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="555cc-2671">clusterSize</span></span> |<span data-ttu-id="555cc-2672">Numero di nodi del ruolo di lavoro/nodi dati nel cluster.</span><span class="sxs-lookup"><span data-stu-id="555cc-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="555cc-2673">Il cluster HDInsight viene creato con 2 nodi head e il numero di nodi del ruolo di lavoro specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="555cc-2674">I nodi sono di dimensione Standard_D3, con 4 core, quindi un cluster di 4 nodi del ruolo di lavoro ha 24 core, ossia 4\*4 = 16 core per i nodi del ruolo di lavoro + 2\*4 = 8 core per i nodi head.</span><span class="sxs-lookup"><span data-stu-id="555cc-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="555cc-2675">Vedere [Creare cluster Hadoop basati su Linux in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) per i dettagli sul livello Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="555cc-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="555cc-2676">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2676">Yes</span></span> |
| <span data-ttu-id="555cc-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="555cc-2677">timetolive</span></span> |<span data-ttu-id="555cc-2678">Il tempo di inattività consentito per il cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="555cc-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="555cc-2679">Specifica per quanto tempo il cluster HDInsight su richiesta rimane attivo dopo il completamento di un'attività eseguita se non sono presenti altri processi attivi del cluster.</span><span class="sxs-lookup"><span data-stu-id="555cc-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="555cc-2680">Ad esempio, se un'esecuzione di attività accetta 6 minuti e timetolive è impostato su 5 minuti, il cluster rimane attivo per altri 5 minuti dopo i 6 minuti di elaborazione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="555cc-2681">Se un'altra attività viene eseguita entro i 6 minuti consentiti, verrà elaborata dal cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="555cc-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="555cc-2682">Poiché la creazione di un cluster HDInsight su richiesta è un'operazione che usa un numero elevato di risorse e potrebbe richiedere alcuni minuti, usare questa impostazione a seconda delle necessità per migliorare le prestazioni di una data factory riutilizzando un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="555cc-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="555cc-2683">Se si imposta il valore della proprietà timetolive su 0, il cluster viene eliminato non appena l'attività in elaborazione termina.</span><span class="sxs-lookup"><span data-stu-id="555cc-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="555cc-2684">D'altra parte, se si imposta un valore elevato, il cluster può rimanere inattivo inutilmente causando costi elevati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="555cc-2685">È quindi importante impostare il valore appropriato in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="555cc-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="555cc-2686">Più pipeline possono condividere la stessa istanza del cluster HDInsight su richiesta se il valore della proprietà timetolive è impostato in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="555cc-2687">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2687">Yes</span></span> |
| <span data-ttu-id="555cc-2688">version</span><span class="sxs-lookup"><span data-stu-id="555cc-2688">version</span></span> |<span data-ttu-id="555cc-2689">Versione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="555cc-2690">Per informazioni dettagliate vedere le [versioni supportate di HDInsight in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="555cc-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="555cc-2691">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2691">No</span></span> |
| <span data-ttu-id="555cc-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="555cc-2692">linkedServiceName</span></span> |<span data-ttu-id="555cc-2693">Servizio collegato Archiviazione di Azure che il cluster su richiesta deve usare per l'archiviazione e l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="555cc-2694">Non è attualmente possibile creare un cluster HDInsight su richiesta che usa Azure Data Lake Store come risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="555cc-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="555cc-2695">Per archiviare i dati dei risultati dell'elaborazione di HDInsight in un'istanza di Azure Data Lake Store, usare un'attività di copia per copiare i dati dall'archivio BLOB di Azure in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="555cc-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="555cc-2696">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2696">Yes</span></span> |
| <span data-ttu-id="555cc-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="555cc-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="555cc-2698">Specifica account di archiviazione aggiuntivi per il servizio collegato HDInsight in modo che il servizio Data Factory possa registrarli per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="555cc-2699">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2699">No</span></span> |
| <span data-ttu-id="555cc-2700">osType</span><span class="sxs-lookup"><span data-stu-id="555cc-2700">osType</span></span> |<span data-ttu-id="555cc-2701">Tipo di sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-2701">Type of operating system.</span></span> <span data-ttu-id="555cc-2702">I valori consentiti sono: Windows (impostazione predefinita) e Linux</span><span class="sxs-lookup"><span data-stu-id="555cc-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="555cc-2703">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2703">No</span></span> |
| <span data-ttu-id="555cc-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="555cc-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="555cc-2705">Il nome del servizio collegato di Azure SQL che fa riferimento al database HCatalog.</span><span class="sxs-lookup"><span data-stu-id="555cc-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="555cc-2706">Viene creato il cluster HDInsight su richiesta usando il database SQL di Azure come metastore.</span><span class="sxs-lookup"><span data-stu-id="555cc-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="555cc-2707">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="555cc-2708">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2708">JSON example</span></span>
<span data-ttu-id="555cc-2709">Il codice JSON seguente definisce un servizio collegato HDInsight su richiesta basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="555cc-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="555cc-2710">Il servizio Data factory crea automaticamente un cluster HDInsight **basato su Linux** durante l'elaborazione di una sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="555cc-2711">Per altre informazioni, vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="555cc-2712">Cluster HDInsight di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="555cc-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="555cc-2713">È possibile creare un servizio collegato Azure HDInsight per registrare il proprio cluster HDInsight con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="555cc-2714">Su questo servizio collegato è possibile eseguire le attività di trasformazione seguenti:[attività personalizzate .NET ](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig](#hdinsight-pig-activity, [attività MapReduce](#hdinsight-mapreduce-activity), [attività di Hadoop Streaming](#hdinsight-streaming-activityd), [attività Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="555cc-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2715">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2715">Linked service</span></span>
<span data-ttu-id="555cc-2716">La tabella seguente fornisce le descrizioni delle proprietà usate nella definizione JSON di Azure di un servizio collegato HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="555cc-2717">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2717">Property</span></span> | <span data-ttu-id="555cc-2718">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2718">Description</span></span> | <span data-ttu-id="555cc-2719">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2720">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2720">type</span></span> |<span data-ttu-id="555cc-2721">La proprietà type deve essere impostata su **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="555cc-2722">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2722">Yes</span></span> |
| <span data-ttu-id="555cc-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="555cc-2723">clusterUri</span></span> |<span data-ttu-id="555cc-2724">L'URI del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="555cc-2725">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2725">Yes</span></span> |
| <span data-ttu-id="555cc-2726">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2726">username</span></span> |<span data-ttu-id="555cc-2727">Specifica il nome dell'utente da utilizzare per connettersi a un cluster HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="555cc-2728">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2728">Yes</span></span> |
| <span data-ttu-id="555cc-2729">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2729">password</span></span> |<span data-ttu-id="555cc-2730">Specifica la password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2730">Specify password for the user account.</span></span> |<span data-ttu-id="555cc-2731">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2731">Yes</span></span> |
| <span data-ttu-id="555cc-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="555cc-2732">linkedServiceName</span></span> | <span data-ttu-id="555cc-2733">Nome del servizio collegato all'archiviazione di Azure che fa riferimento all'archiviazione BLOB di Azure usata dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="555cc-2734">Attualmente non è possibile specificare un servizio collegato di Azure Data Lake Store per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="555cc-2735">È possibile accedere ai dati in Azure Data Lake Store da script Hive/Pig se il cluster HDInsight dispone di accesso a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="555cc-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="555cc-2736">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2736">Yes</span></span> |

<span data-ttu-id="555cc-2737">Per le versioni dei cluster di HDInsight, vedere le [versioni supportate di HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="555cc-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="555cc-2738">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="555cc-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="555cc-2739">Azure Batch</span></span>
<span data-ttu-id="555cc-2740">È possibile creare un servizio collegato di Azure Batch per registrare un pool di Batch di macchine virtuali in una data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="555cc-2741">È possibile eseguire le attività .NET personalizzate utilizzando Batch Azure o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="555cc-2742">Su questo servizio collegato è possibile eseguire un' [attività personalizzata .NET](#net-custom-activity).</span><span class="sxs-lookup"><span data-stu-id="555cc-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2743">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2743">Linked service</span></span>
<span data-ttu-id="555cc-2744">La tabella seguente fornisce le descrizioni delle proprietà usate nella definizione JSON di Azure di un servizio collegato Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="555cc-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="555cc-2745">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2745">Property</span></span> | <span data-ttu-id="555cc-2746">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2746">Description</span></span> | <span data-ttu-id="555cc-2747">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2748">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2748">type</span></span> |<span data-ttu-id="555cc-2749">La proprietà type deve essere impostata su **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="555cc-2750">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2750">Yes</span></span> |
| <span data-ttu-id="555cc-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="555cc-2751">accountName</span></span> |<span data-ttu-id="555cc-2752">Nome dell'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="555cc-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="555cc-2753">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2753">Yes</span></span> |
| <span data-ttu-id="555cc-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="555cc-2754">accessKey</span></span> |<span data-ttu-id="555cc-2755">Chiave di accesso per l'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="555cc-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="555cc-2756">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2756">Yes</span></span> |
| <span data-ttu-id="555cc-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="555cc-2757">poolName</span></span> |<span data-ttu-id="555cc-2758">Nome del pool di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="555cc-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="555cc-2759">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2759">Yes</span></span> |
| <span data-ttu-id="555cc-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="555cc-2760">linkedServiceName</span></span> |<span data-ttu-id="555cc-2761">Nome dello spazio di archiviazione del servizio collegato Azure associato al servizio collegato Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="555cc-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="555cc-2762">Questo servizio collegato viene utilizzato per organizzare i file necessari per eseguire l'attività e archiviare i log di esecuzione dell’attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="555cc-2763">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="555cc-2764">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="555cc-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-2765">Azure Machine Learning</span></span>
<span data-ttu-id="555cc-2766">Creare un servizio collegato di Azure Machine Learning per registrare un endpoint di punteggio batch Machine Learning in una data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="555cc-2767">Su questo servizio collegato è possibile eseguire due attività di trasformazione dati: [Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="555cc-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2768">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2768">Linked service</span></span>
<span data-ttu-id="555cc-2769">La tabella seguente fornisce le descrizioni delle proprietà usate nella definizione JSON di Azure di un servizio collegato Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="555cc-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="555cc-2770">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2770">Property</span></span> | <span data-ttu-id="555cc-2771">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2771">Description</span></span> | <span data-ttu-id="555cc-2772">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2773">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2773">Type</span></span> |<span data-ttu-id="555cc-2774">La proprietà type deve essere impostata su **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="555cc-2775">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2775">Yes</span></span> |
| <span data-ttu-id="555cc-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="555cc-2776">mlEndpoint</span></span> |<span data-ttu-id="555cc-2777">L’URL del batch punteggio.</span><span class="sxs-lookup"><span data-stu-id="555cc-2777">The batch scoring URL.</span></span> |<span data-ttu-id="555cc-2778">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2778">Yes</span></span> |
| <span data-ttu-id="555cc-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="555cc-2779">apiKey</span></span> |<span data-ttu-id="555cc-2780">Modello dell'area di lavoro pubblicato di API.</span><span class="sxs-lookup"><span data-stu-id="555cc-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="555cc-2781">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="555cc-2782">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="555cc-2783">Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="555cc-2784">Creare un servizio collegato di **Azure Data Lake Analytics** per collegare un servizio di calcolo di Azure Data Lake Analytics a una Data factory di Azure prima di usare l' [attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md) in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="555cc-2785">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2785">Linked service</span></span>

<span data-ttu-id="555cc-2786">La tabella seguente fornisce le descrizioni delle proprietà usate nella definizione JSON di un servizio collegato Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="555cc-2787">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2787">Property</span></span> | <span data-ttu-id="555cc-2788">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2788">Description</span></span> | <span data-ttu-id="555cc-2789">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="555cc-2790">Type</span></span> |<span data-ttu-id="555cc-2791">La proprietà type deve essere impostata su **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="555cc-2792">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2792">Yes</span></span> |
| <span data-ttu-id="555cc-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="555cc-2793">accountName</span></span> |<span data-ttu-id="555cc-2794">Nome dell'account di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="555cc-2795">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2795">Yes</span></span> |
| <span data-ttu-id="555cc-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="555cc-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="555cc-2797">URI di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="555cc-2798">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2798">No</span></span> |
| <span data-ttu-id="555cc-2799">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="555cc-2799">authorization</span></span> |<span data-ttu-id="555cc-2800">Il codice di autorizzazione viene recuperato automaticamente dopo aver fatto clic sul pulsante **Autorizza** nell'editor di Data factory e aver completato l'accesso OAuth.</span><span class="sxs-lookup"><span data-stu-id="555cc-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="555cc-2801">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2801">Yes</span></span> |
| <span data-ttu-id="555cc-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="555cc-2802">subscriptionId</span></span> |<span data-ttu-id="555cc-2803">ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-2803">Azure subscription id</span></span> |<span data-ttu-id="555cc-2804">No (se non specificata, viene usata la sottoscrizione della Data factory).</span><span class="sxs-lookup"><span data-stu-id="555cc-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="555cc-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="555cc-2805">resourceGroupName</span></span> |<span data-ttu-id="555cc-2806">Nome del gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-2806">Azure resource group name</span></span> |<span data-ttu-id="555cc-2807">No (se non specificata, viene usato il gruppo di risorse di Data Factory).</span><span class="sxs-lookup"><span data-stu-id="555cc-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="555cc-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="555cc-2808">sessionId</span></span> |<span data-ttu-id="555cc-2809">ID di sessione dalla sessione di autorizzazione OAuth.</span><span class="sxs-lookup"><span data-stu-id="555cc-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="555cc-2810">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="555cc-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="555cc-2811">L'ID viene generato automaticamente nell'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="555cc-2812">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="555cc-2813">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2813">JSON example</span></span>
<span data-ttu-id="555cc-2814">Nell'esempio seguente viene fornita la definizione JSON per un servizio collegato di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="555cc-2815">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-2815">Azure SQL Database</span></span>
<span data-ttu-id="555cc-2816">Si crea un servizio collegato di Azure SQL e lo si utilizza con l’ [Attività di stored procedure](#stored-procedure-activity) per richiamare una procedura stored da una pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2817">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2817">Linked service</span></span>
<span data-ttu-id="555cc-2818">Per definire un servizio collegato di Database SQL di Azure, impostare il **tipo** di servizio collegato su **AzureSqlDatabase**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2819">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2819">Property</span></span> | <span data-ttu-id="555cc-2820">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2820">Description</span></span> | <span data-ttu-id="555cc-2821">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-2822">connectionString</span></span> |<span data-ttu-id="555cc-2823">Specificare le informazioni necessarie per connettersi all'istanza di database SQL di Azure per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="555cc-2824">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="555cc-2825">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="555cc-2826">Vedere l’articolo [Connettore di Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="555cc-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="555cc-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="555cc-2828">Si crea un servizio collegato di Azure SQL Data Warehouse e lo si usa con l' [attività di stored procedure](data-factory-stored-proc-activity.md) per richiamare una stored procedure da una pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2829">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2829">Linked service</span></span>
<span data-ttu-id="555cc-2830">Per definire un servizio collegato di Azure SQL Data Warehouse, impostare il **tipo** di servizio collegato su **AzureSqlDW**e specificare le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="555cc-2831">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2831">Property</span></span> | <span data-ttu-id="555cc-2832">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2832">Description</span></span> | <span data-ttu-id="555cc-2833">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-2834">connectionString</span></span> |<span data-ttu-id="555cc-2835">Specificare le informazioni necessarie per connettersi all'istanza di Azure SQL Data Warehouse per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="555cc-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="555cc-2836">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="555cc-2837">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="555cc-2838">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="555cc-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="555cc-2839">SQL Server</span></span> 
<span data-ttu-id="555cc-2840">Si crea un servizio collegato di SQL Server e lo si usa con l' [attività di stored procedure](data-factory-stored-proc-activity.md) per richiamare una stored procedure da una pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="555cc-2841">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="555cc-2841">Linked service</span></span>
<span data-ttu-id="555cc-2842">È stato creato un servizio collegato di tipo **OnPremisesSqlServer** per collegare un database di SQL Server locale a una data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="555cc-2843">La tabella seguente contiene le descrizioni degli elementi JSON specifici per il servizio collegato di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="555cc-2844">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato SQL Server.</span><span class="sxs-lookup"><span data-stu-id="555cc-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="555cc-2845">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2845">Property</span></span> | <span data-ttu-id="555cc-2846">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2846">Description</span></span> | <span data-ttu-id="555cc-2847">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2848">type</span><span class="sxs-lookup"><span data-stu-id="555cc-2848">type</span></span> |<span data-ttu-id="555cc-2849">La proprietà type deve essere impostata su **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="555cc-2850">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2850">Yes</span></span> |
| <span data-ttu-id="555cc-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="555cc-2851">connectionString</span></span> |<span data-ttu-id="555cc-2852">Specificare le informazioni di connectionString necessarie per connettersi al database di SQL Server locale usando l'autenticazione di SQL o Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="555cc-2853">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2853">Yes</span></span> |
| <span data-ttu-id="555cc-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="555cc-2854">gatewayName</span></span> |<span data-ttu-id="555cc-2855">Nome del gateway che il servizio Data factory deve usare per connettersi al database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="555cc-2856">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2856">Yes</span></span> |
| <span data-ttu-id="555cc-2857">username</span><span class="sxs-lookup"><span data-stu-id="555cc-2857">username</span></span> |<span data-ttu-id="555cc-2858">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="555cc-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="555cc-2859">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="555cc-2860">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2860">No</span></span> |
| <span data-ttu-id="555cc-2861">password</span><span class="sxs-lookup"><span data-stu-id="555cc-2861">password</span></span> |<span data-ttu-id="555cc-2862">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="555cc-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="555cc-2863">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2863">No</span></span> |

<span data-ttu-id="555cc-2864">È possibile crittografare le credenziali usando il cmdlet **New-AzureRmDataFactoryEncryptValue** e usarle nella stringa di connessione, come illustrato nell'esempio seguente (proprietà **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="555cc-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="555cc-2865">Esempio: JSON per l'uso dell'autenticazione SQL</span><span class="sxs-lookup"><span data-stu-id="555cc-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="555cc-2866">Esempio: JSON per l'uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="555cc-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="555cc-2867">Se vengono specificati nome utente e password, il gateway li usa per rappresentare l'account utente specificato per la connessione al database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="555cc-2868">In caso contrario, il gateway si connette a SQL Server direttamente con il contesto di sicurezza del gateway (l'account di avvio).</span><span class="sxs-lookup"><span data-stu-id="555cc-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="555cc-2869">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="555cc-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="555cc-2870">ATTIVITÀ DI TRASFORMAZIONE DEI DATI</span><span class="sxs-lookup"><span data-stu-id="555cc-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="555cc-2871">Attività</span><span class="sxs-lookup"><span data-stu-id="555cc-2871">Activity</span></span> | <span data-ttu-id="555cc-2872">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="555cc-2873">Attività Hive di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="555cc-2874">L'attività Hive di HDInsight in una pipeline di Data factory esegue query Hive sul proprio cluster HDInsight o sul cluster HDInsight su richiesta basato su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="555cc-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="555cc-2875">Attività Pig di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="555cc-2876">L'attività Pig di HDInsight in una pipeline di Data factory esegue query Pig sul proprio cluster HDInsight o sul cluster HDInsight su richiesta basato su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="555cc-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="555cc-2877">Attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="555cc-2878">L'attività HDInsight MapReduce in una pipeline di Data Factory esegue i programmi di MapReduce nei cluster HDInsight personalizzati o su richiesta basati su Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="555cc-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="555cc-2879">Attività di streaming di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="555cc-2880">L'attività HDInsight Streaming Activity in una pipeline di Data Factory esegue i programmi di Hadoop Streaming nei cluster HDInsight personalizzati o su richiesta basati su Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="555cc-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="555cc-2881">Attività HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="555cc-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="555cc-2882">L'attività Spark di HDInsight in una pipeline di Data Factory esegue programmi Spark nel cluster HDInsight personale.</span><span class="sxs-lookup"><span data-stu-id="555cc-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="555cc-2883">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="555cc-2884">Azure Data Factory consente di creare facilmente pipeline che usano un servizio Web pubblicato di Azure Machine Learning per l'analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="555cc-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="555cc-2885">Con Attività di esecuzione Batch in una pipeline di Azure Data Factory è possibile richiamare un servizio Web di Machine Learning per eseguire stime dei dati in batch.</span><span class="sxs-lookup"><span data-stu-id="555cc-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="555cc-2886">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="555cc-2887">Nel corso del tempo è necessario ripetere il training dei modelli predittivi negli esperimenti di assegnazione dei punteggi di Machine Learning usando nuovi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="555cc-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="555cc-2888">Una volta ripetuto il training, aggiornare il servizio Web di assegnazione dei punteggi con il modello Machine Learning di cui è stato ripetuto il training.</span><span class="sxs-lookup"><span data-stu-id="555cc-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="555cc-2889">È possibile usare l'attività di aggiornamento risorse per aggiornare il servizio Web con il nuovo modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="555cc-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="555cc-2890">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="555cc-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="555cc-2891">È possibile usare l'attività stored procedure in una pipeline di Data Factory per richiamare una stored procedure in uno dei seguenti archivi dati: database SQL di Azure, Azure SQL Data Warehouse, database di SQL Server in azienda o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="555cc-2892">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="555cc-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="555cc-2893">L'attività U-SQL di Data Lake Analytics esegue uno script U-SQL in un cluster di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="555cc-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="555cc-2894">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="555cc-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="555cc-2895">Se è necessario trasformare i dati in una modalità non supportata da Data Factory, è possibile creare un'attività personalizzata contenente la logica di elaborazione dei dati richiesta e usarla nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="555cc-2896">È possibile configurare l'attività .NET personalizzata da eseguire usando il servizio Azure Batch o un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="555cc-2897">Attività Hive di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="555cc-2898">In una definizione JSON di attività Hive è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="555cc-2899">Il tipo di proprietà dell'attività deve essere impostato su **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="555cc-2900">È necessario creare innanzitutto un servizio collegato di HDInsight e quindi specificarne il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-2901">Quando si imposta il tipo di attività HDInsightHive vengono le proprietà seguenti sono supportate nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="555cc-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="555cc-2902">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2902">Property</span></span> | <span data-ttu-id="555cc-2903">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2903">Description</span></span> | <span data-ttu-id="555cc-2904">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2905">script</span><span class="sxs-lookup"><span data-stu-id="555cc-2905">script</span></span> |<span data-ttu-id="555cc-2906">Specificare lo script Hive inline</span><span class="sxs-lookup"><span data-stu-id="555cc-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="555cc-2907">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2907">No</span></span> |
| <span data-ttu-id="555cc-2908">script path</span><span class="sxs-lookup"><span data-stu-id="555cc-2908">script path</span></span> |<span data-ttu-id="555cc-2909">Archiviare lo script Hive in un archivio BLOB di Azure e immettere il percorso del file.</span><span class="sxs-lookup"><span data-stu-id="555cc-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="555cc-2910">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="555cc-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="555cc-2911">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2911">Both cannot be used together.</span></span> <span data-ttu-id="555cc-2912">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="555cc-2913">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2913">No</span></span> |
| <span data-ttu-id="555cc-2914">defines</span><span class="sxs-lookup"><span data-stu-id="555cc-2914">defines</span></span> |<span data-ttu-id="555cc-2915">Specificare i parametri come coppie chiave/valore per fare riferimento ad essi nello script Hive usando "hiveconf"</span><span class="sxs-lookup"><span data-stu-id="555cc-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="555cc-2916">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2916">No</span></span> |

<span data-ttu-id="555cc-2917">Questi tipi di proprietà sono specifiche per l'attività Hive.</span><span class="sxs-lookup"><span data-stu-id="555cc-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="555cc-2918">Altre proprietà (esterne alla sezione typeProperties) sono supportate per tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="555cc-2919">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2919">JSON example</span></span>
<span data-ttu-id="555cc-2920">Il codice JSON seguente definisce un'attività Hive di HDInsight in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="555cc-2921">Per altre informazioni, vedere [Attività Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="555cc-2922">Attività Pig di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="555cc-2923">In una definizione JSON di attività Pig è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="555cc-2924">Il tipo di proprietà dell'attività deve essere impostato su **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="555cc-2925">È necessario creare innanzitutto un servizio collegato di HDInsight e quindi specificarne il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-2926">Quando il tipo di attività è impostato su HDInsightPig, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="555cc-2927">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2927">Property</span></span> | <span data-ttu-id="555cc-2928">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2928">Description</span></span> | <span data-ttu-id="555cc-2929">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2930">script</span><span class="sxs-lookup"><span data-stu-id="555cc-2930">script</span></span> |<span data-ttu-id="555cc-2931">Specificare lo script Pig inline</span><span class="sxs-lookup"><span data-stu-id="555cc-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="555cc-2932">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2932">No</span></span> |
| <span data-ttu-id="555cc-2933">script path</span><span class="sxs-lookup"><span data-stu-id="555cc-2933">script path</span></span> |<span data-ttu-id="555cc-2934">Archiviare lo script Pig in un archivio BLOB di Azure e immettere il percorso del file.</span><span class="sxs-lookup"><span data-stu-id="555cc-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="555cc-2935">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="555cc-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="555cc-2936">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2936">Both cannot be used together.</span></span> <span data-ttu-id="555cc-2937">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="555cc-2938">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2938">No</span></span> |
| <span data-ttu-id="555cc-2939">defines</span><span class="sxs-lookup"><span data-stu-id="555cc-2939">defines</span></span> |<span data-ttu-id="555cc-2940">Specificare i parametri come coppie chiave/valore per fare riferimento ad essi nello script Pig</span><span class="sxs-lookup"><span data-stu-id="555cc-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="555cc-2941">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2941">No</span></span> |

<span data-ttu-id="555cc-2942">Questi tipi di proprietà sono specifiche per l'attività Pig.</span><span class="sxs-lookup"><span data-stu-id="555cc-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="555cc-2943">Altre proprietà (esterne alla sezione typeProperties) sono supportate per tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="555cc-2944">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="555cc-2945">Per altre informazioni, vedere [Attività Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="555cc-2946">Attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="555cc-2947">In una definizione JSON di attività MapReduce è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="555cc-2948">Il tipo di proprietà dell'attività deve essere impostato su **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="555cc-2949">È necessario creare innanzitutto un servizio collegato di HDInsight e quindi specificarne il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-2950">Quando il tipo di attività è impostato su HDInsightMapReduce, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="555cc-2951">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2951">Property</span></span> | <span data-ttu-id="555cc-2952">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2952">Description</span></span> | <span data-ttu-id="555cc-2953">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="555cc-2954">jarLinkedService</span></span> | <span data-ttu-id="555cc-2955">Nome del servizio collegato di Archiviazione di Azure che contiene il file JAR.</span><span class="sxs-lookup"><span data-stu-id="555cc-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="555cc-2956">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2956">Yes</span></span> |
| <span data-ttu-id="555cc-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="555cc-2957">jarFilePath</span></span> | <span data-ttu-id="555cc-2958">Percorso del file JAR nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="555cc-2959">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2959">Yes</span></span> | 
| <span data-ttu-id="555cc-2960">className</span><span class="sxs-lookup"><span data-stu-id="555cc-2960">className</span></span> | <span data-ttu-id="555cc-2961">Nome della classe principale nel file JAR.</span><span class="sxs-lookup"><span data-stu-id="555cc-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="555cc-2962">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-2962">Yes</span></span> | 
| <span data-ttu-id="555cc-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="555cc-2963">arguments</span></span> | <span data-ttu-id="555cc-2964">Un elenco di argomenti delimitati da virgole per il programma MapReduce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="555cc-2965">In fase di esecuzione, vengono visualizzati alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="555cc-2966">Per differenziare gli argomenti con gli argomenti di MapReduce, è consigliabile usare sia l'opzione che il valore come argomenti, come illustrato nell'esempio seguente (- s, --input - output e così via sono opzioni immediatamente seguite dai valori).</span><span class="sxs-lookup"><span data-stu-id="555cc-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="555cc-2967">No</span><span class="sxs-lookup"><span data-stu-id="555cc-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="555cc-2968">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="555cc-2969">Per altre informazioni, vedere [Attività MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="555cc-2970">Attività di streaming di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="555cc-2971">In una definizione JSON di attività Hadoop Streaming è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="555cc-2972">Il tipo di proprietà dell'attività deve essere impostato su **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="555cc-2973">È necessario creare innanzitutto un servizio collegato di HDInsight e quindi specificarne il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-2974">Quando il tipo di attività è impostato su HDInsightStreaming, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="555cc-2975">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-2975">Property</span></span> | <span data-ttu-id="555cc-2976">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="555cc-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="555cc-2977">mapper</span></span> | <span data-ttu-id="555cc-2978">Nome del mapper eseguibile.</span><span class="sxs-lookup"><span data-stu-id="555cc-2978">Name of the mapper executable.</span></span> <span data-ttu-id="555cc-2979">Nell'esempio cat.exe è l'eseguibile del mapper.</span><span class="sxs-lookup"><span data-stu-id="555cc-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="555cc-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="555cc-2980">reducer</span></span> | <span data-ttu-id="555cc-2981">Nome del reducer eseguibile.</span><span class="sxs-lookup"><span data-stu-id="555cc-2981">Name of the reducer executable.</span></span> <span data-ttu-id="555cc-2982">Nell'esempio wc.exe è l'eseguibile del mapper.</span><span class="sxs-lookup"><span data-stu-id="555cc-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="555cc-2983">input</span><span class="sxs-lookup"><span data-stu-id="555cc-2983">input</span></span> | <span data-ttu-id="555cc-2984">File di input (incluso percorso) del mapper.</span><span class="sxs-lookup"><span data-stu-id="555cc-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="555cc-2985">Nell'esempio "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt" adfsample è il contenitore BLOB, example/data/Gutenberg è la cartella e davinci.txt è il BLOB.</span><span class="sxs-lookup"><span data-stu-id="555cc-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="555cc-2986">output</span><span class="sxs-lookup"><span data-stu-id="555cc-2986">output</span></span> | <span data-ttu-id="555cc-2987">File di output (incluso percorso) del reducer.</span><span class="sxs-lookup"><span data-stu-id="555cc-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="555cc-2988">L'output del processo di Hadoop Streaming viene scritto nel percorso specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="555cc-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="555cc-2989">filePaths</span></span> | <span data-ttu-id="555cc-2990">Percorsi dei file eseguibili del mapper e del reducer.</span><span class="sxs-lookup"><span data-stu-id="555cc-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="555cc-2991">Nell'esempio: "adfsample/example/apps/wc.exe", adfsample è il contenitore BLOB, example/apps è la cartella e wc.exe è l'eseguibile.</span><span class="sxs-lookup"><span data-stu-id="555cc-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="555cc-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="555cc-2992">fileLinkedService</span></span> | <span data-ttu-id="555cc-2993">Servizio collegato di Archiviazione di Azure che rappresenta l'archivio di Azure contenente i file specificati nella sezione filePaths.</span><span class="sxs-lookup"><span data-stu-id="555cc-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="555cc-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="555cc-2994">arguments</span></span> | <span data-ttu-id="555cc-2995">Un elenco di argomenti delimitati da virgole per il programma MapReduce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="555cc-2996">In fase di esecuzione, vengono visualizzati alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="555cc-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="555cc-2997">Per differenziare gli argomenti con gli argomenti di MapReduce, è consigliabile usare sia l'opzione che il valore come argomenti, come illustrato nell'esempio seguente (- s, --input - output e così via sono opzioni immediatamente seguite dai valori).</span><span class="sxs-lookup"><span data-stu-id="555cc-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="555cc-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="555cc-2998">getDebugInfo</span></span> | <span data-ttu-id="555cc-2999">Un elemento facoltativo.</span><span class="sxs-lookup"><span data-stu-id="555cc-2999">An optional element.</span></span> <span data-ttu-id="555cc-3000">Quando viene impostata su Failure, i log vengono scaricati solo in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="555cc-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="555cc-3001">Quando viene impostata su All, i log vengono sempre scaricati indipendentemente dallo stato dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="555cc-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="555cc-3002">È necessario specificare un set di dati di output per l'attività di Hadoop Streaming per la proprietà **output** .</span><span class="sxs-lookup"><span data-stu-id="555cc-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="555cc-3003">Questo set di dati fittizio è necessario per la pianificazione della pipeline (oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="555cc-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="555cc-3004">Se l'attività non accetta un input, è possibile evitare di specificare il set di dati di input dell'attività per la proprietà **input**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="555cc-3005">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="555cc-3006">Per altre informazioni, vedere l'argomento relativo all'[attività Hadoop Streaming](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="555cc-3007">Attività Spark di HDInsight</span><span class="sxs-lookup"><span data-stu-id="555cc-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="555cc-3008">In una definizione JSON di attività Spark è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="555cc-3009">Il tipo di proprietà dell'attività deve essere impostato su **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="555cc-3010">È necessario creare innanzitutto un servizio collegato di HDInsight e quindi specificarne il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-3011">Quando il tipo di attività è impostato su HDInsightSpark, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="555cc-3012">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3012">Property</span></span> | <span data-ttu-id="555cc-3013">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3013">Description</span></span> | <span data-ttu-id="555cc-3014">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="555cc-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="555cc-3015">rootPath</span></span> | <span data-ttu-id="555cc-3016">Contenitore BLOB di Azure e cartella che contiene il file Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="555cc-3017">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="555cc-3018">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3018">Yes</span></span> |
| <span data-ttu-id="555cc-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="555cc-3019">entryFilePath</span></span> | <span data-ttu-id="555cc-3020">Percorso relativo alla cartella radice del pacchetto/codice Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="555cc-3021">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3021">Yes</span></span> |
| <span data-ttu-id="555cc-3022">className</span><span class="sxs-lookup"><span data-stu-id="555cc-3022">className</span></span> | <span data-ttu-id="555cc-3023">Classe principale Java/Spark dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="555cc-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="555cc-3024">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3024">No</span></span> | 
| <span data-ttu-id="555cc-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="555cc-3025">arguments</span></span> | <span data-ttu-id="555cc-3026">Elenco di argomenti della riga di comando del programma Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="555cc-3027">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3027">No</span></span> | 
| <span data-ttu-id="555cc-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="555cc-3028">proxyUser</span></span> | <span data-ttu-id="555cc-3029">Account utente da rappresentare per eseguire il programma Spark</span><span class="sxs-lookup"><span data-stu-id="555cc-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="555cc-3030">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3030">No</span></span> | 
| <span data-ttu-id="555cc-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="555cc-3031">sparkConfig</span></span> | <span data-ttu-id="555cc-3032">Proprietà di configurazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3032">Spark configuration properties.</span></span> | <span data-ttu-id="555cc-3033">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3033">No</span></span> | 
| <span data-ttu-id="555cc-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="555cc-3034">getDebugInfo</span></span> | <span data-ttu-id="555cc-3035">Specifica quando i file di log di Spark vengono copiati nell'archiviazione di Azure usata dal cluster HDInsight (o) specificata da sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="555cc-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="555cc-3036">Valori consentiti: None, Always o Failure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="555cc-3037">Valore predefinito: None.</span><span class="sxs-lookup"><span data-stu-id="555cc-3037">Default value: None.</span></span> | <span data-ttu-id="555cc-3038">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3038">No</span></span> | 
| <span data-ttu-id="555cc-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="555cc-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="555cc-3040">Il servizio collegato di archiviazione di Azure che contiene il file di processo, le dipendenze e i log di Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="555cc-3041">Se non si specifica un valore per questa proprietà, viene usato lo spazio di archiviazione associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="555cc-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="555cc-3042">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="555cc-3043">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="555cc-3044">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="555cc-3044">Note the following points:</span></span> 

- <span data-ttu-id="555cc-3045">La proprietà **type** è impostata su **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="555cc-3046">Il **rootPath** è impostato su **adfspark\\pyFiles**, dove adfspark è il contenitore BLOB di Azure e pyFiles è la cartella di file nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="555cc-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="555cc-3047">In questo esempio, l'archivio BLOB di Azure è quello associato al cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="555cc-3048">È possibile caricare il file in un archivio di Azure diverso.</span><span class="sxs-lookup"><span data-stu-id="555cc-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="555cc-3049">In tal caso, creare un servizio collegato Archiviazione di Azure per collegare l'account di archiviazione alla data factory.</span><span class="sxs-lookup"><span data-stu-id="555cc-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="555cc-3050">Quindi, specificare il nome del servizio collegato come valore per la proprietà **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="555cc-3051">Vedere [Proprietà dell'attività Spark](#spark-activity-properties) per informazioni dettagliate su questa e altre proprietà supportate dall'attività Spark.</span><span class="sxs-lookup"><span data-stu-id="555cc-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="555cc-3052">La proprietà **entryFilePath** è impostata su **test.py**, ovvero il file python.</span><span class="sxs-lookup"><span data-stu-id="555cc-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="555cc-3053">La proprietà **getDebugInfo** è impostata su **Sempre** e indica che i file di log vengono sempre generati (con esito positivo o negativo).</span><span class="sxs-lookup"><span data-stu-id="555cc-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="555cc-3054">Non è consigliabile impostare questa proprietà su Sempre in un ambiente di produzione a meno che non si stia tentando di risolvere un problema.</span><span class="sxs-lookup"><span data-stu-id="555cc-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="555cc-3055">La sezione **outputs** presenta un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="555cc-3056">Anche se il programma Spark non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="555cc-3057">Il set di dati di output è ciò su cui si basa la pianificazione della pipeline (oraria, giornaliera e così via).</span><span class="sxs-lookup"><span data-stu-id="555cc-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="555cc-3058">Per altre informazioni sull'attività, vedere l'argomento relativo all'[attività Spark](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="555cc-3059">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="555cc-3060">In una definizione JSON di attività di esecuzione batch di Machine Learning è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="555cc-3061">Il tipo di proprietà dell'attività deve essere impostato su **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="555cc-3062">È necessario creare innanzitutto un servizio collegato di Azure Machine Learning e quindi specificare il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-3063">Quando il tipo di attività è impostato su AzureMLBatchExecution, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="555cc-3064">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3064">Property</span></span> | <span data-ttu-id="555cc-3065">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3065">Description</span></span> | <span data-ttu-id="555cc-3066">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="555cc-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="555cc-3067">webServiceInput</span></span> | <span data-ttu-id="555cc-3068">Il set di dati da passare come input del servizio Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="555cc-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="555cc-3069">Questo set di dati deve essere incluso anche nella sezione inputs dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="555cc-3070">Usare webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="555cc-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="555cc-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="555cc-3071">webServiceInputs</span></span> | <span data-ttu-id="555cc-3072">I set di dati specifici da passare come input del servizio Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="555cc-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="555cc-3073">Se il servizio Web accetta più input, usare la proprietà webServiceInputs invece di webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="555cc-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="555cc-3074">Includere anche i set di dati a cui **webServiceInputs** fa riferimento negli **input** dell'attività.</span><span class="sxs-lookup"><span data-stu-id="555cc-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="555cc-3075">Usare webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="555cc-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="555cc-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="555cc-3076">webServiceOutputs</span></span> | <span data-ttu-id="555cc-3077">I set di dati assegnati come output del servizio Web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="555cc-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="555cc-3078">Il servizio Web restituisce i dati di output in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="555cc-3079">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3079">Yes</span></span> | 
<span data-ttu-id="555cc-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-3080">globalParameters</span></span> | <span data-ttu-id="555cc-3081">Specificare i valori dei parametri del servizio Web in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="555cc-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="555cc-3082">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="555cc-3083">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3083">JSON example</span></span>
<span data-ttu-id="555cc-3084">In questo esempio, l'attività ha il set di dati **MLSqlInput** come input e **MLSqlOutput** come output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="555cc-3085">Il set di dati **MLSqlInput** viene passato come input al servizio Web usando la proprietà JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="555cc-3086">Il set di dati **MLSqlOutput** viene passato come output al servizio Web usando la proprietà JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="555cc-3087">Nell'esempio JSON, il servizio Web di Azure Machine Learning distribuito usa un modulo Reader e un modulo Writer per leggere e scrivere i dati da e in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="555cc-3088">Il servizio Web espone i quattro parametri seguenti: Database server name, Database name, Server user account name e Server user account password.</span><span class="sxs-lookup"><span data-stu-id="555cc-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="555cc-3089">Possono essere passati come parametri per il servizio Web solo input e output dell'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="555cc-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="555cc-3090">Nel precedente snippet JSON, ad esempio, MLSqlInput è un input per l'attività AzureMLBatchExecution e viene passato come input al servizio Web tramite il parametro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="555cc-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="555cc-3091">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="555cc-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="555cc-3092">In una definizione JSON di attività della risorsa di aggiornamento di Machine Learning è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="555cc-3093">Il tipo di proprietà dell'attività deve essere impostato su **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="555cc-3094">È necessario creare innanzitutto un servizio collegato di Azure Machine Learning e quindi specificare il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-3095">Quando il tipo di attività è impostato su AzureMLUpdateResource, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="555cc-3096">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3096">Property</span></span> | <span data-ttu-id="555cc-3097">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3097">Description</span></span> | <span data-ttu-id="555cc-3098">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="555cc-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="555cc-3099">trainedModelName</span></span> | <span data-ttu-id="555cc-3100">Nome del modello sottoposto nuovamente a training.</span><span class="sxs-lookup"><span data-stu-id="555cc-3100">Name of the retrained model.</span></span> | <span data-ttu-id="555cc-3101">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3101">Yes</span></span> |  
<span data-ttu-id="555cc-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="555cc-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="555cc-3103">Set di dati che punta al file iLearner restituito dall'operazione di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="555cc-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="555cc-3104">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="555cc-3105">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3105">JSON example</span></span>
<span data-ttu-id="555cc-3106">La pipeline include due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="555cc-3107">Attività di esecuzione batch di Azure ML accetta i dati di training come input e genera il file con estensione iLearner come output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="555cc-3108">L'attività richiama il servizio Web di training, l'esperimento di training esposto come servizio Web, con i dati di training di input e riceve il file iLearner dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="555cc-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="555cc-3109">placeholderBlob è solo un set di dati di output fittizio richiesto dal servizio Data factory di Azure per eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="555cc-3110">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="555cc-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="555cc-3111">In una definizione JSON di attività U-SQL è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="555cc-3112">Il tipo di proprietà dell'attività deve essere impostato su **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="555cc-3113">È necessario creare innanzitutto un servizio collegato di Azure Data Lake Analytics e quindi specificare il nome come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-3114">Quando il tipo di attività è impostato su DataLakeAnalyticsU-SQL, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="555cc-3115">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3115">Property</span></span> | <span data-ttu-id="555cc-3116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3116">Description</span></span> | <span data-ttu-id="555cc-3117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="555cc-3118">scriptPath</span></span> |<span data-ttu-id="555cc-3119">Percorso della cartella contenente lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="555cc-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="555cc-3120">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="555cc-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="555cc-3121">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="555cc-3121">No (if you use script)</span></span> |
| <span data-ttu-id="555cc-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="555cc-3122">scriptLinkedService</span></span> |<span data-ttu-id="555cc-3123">Servizi collegati che collegano la risorsa di archiviazione contenente lo script alla Data factory</span><span class="sxs-lookup"><span data-stu-id="555cc-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="555cc-3124">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="555cc-3124">No (if you use script)</span></span> |
| <span data-ttu-id="555cc-3125">script</span><span class="sxs-lookup"><span data-stu-id="555cc-3125">script</span></span> |<span data-ttu-id="555cc-3126">Specificare lo script inline anziché scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="555cc-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="555cc-3127">Ad esempio: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="555cc-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="555cc-3128">No (se si usano le proprietà scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="555cc-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="555cc-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="555cc-3129">degreeOfParallelism</span></span> |<span data-ttu-id="555cc-3130">Il numero massimo di nodi usati contemporaneamente per eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="555cc-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="555cc-3131">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3131">No</span></span> |
| <span data-ttu-id="555cc-3132">priority</span><span class="sxs-lookup"><span data-stu-id="555cc-3132">priority</span></span> |<span data-ttu-id="555cc-3133">Determina quali processi rispetto a tutti gli altri disponibili nella coda devono essere selezionati per essere eseguiti per primi.</span><span class="sxs-lookup"><span data-stu-id="555cc-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="555cc-3134">Più è basso il numero, maggiore sarà la priorità.</span><span class="sxs-lookup"><span data-stu-id="555cc-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="555cc-3135">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3135">No</span></span> |
| <span data-ttu-id="555cc-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="555cc-3136">parameters</span></span> |<span data-ttu-id="555cc-3137">Parametri per lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="555cc-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="555cc-3138">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="555cc-3139">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="555cc-3140">Per altre informazioni, vedere [Attività Data Lake Analytics U-SQL](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="555cc-3141">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="555cc-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="555cc-3142">In una definizione JSON di attività stored procedure è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="555cc-3143">Il tipo di proprietà dell'attività deve essere impostato su **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="555cc-3144">È necessario creare uno dei seguenti servizi collegati e specificare il nome del servizio collegato come valore della proprietà **linkedServiceName**:</span><span class="sxs-lookup"><span data-stu-id="555cc-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="555cc-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="555cc-3145">SQL Server</span></span> 
- <span data-ttu-id="555cc-3146">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="555cc-3146">Azure SQL Database</span></span>
- <span data-ttu-id="555cc-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="555cc-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="555cc-3148">Quando il tipo di attività è impostato su SqlServerStoredProcedure, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="555cc-3149">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3149">Property</span></span> | <span data-ttu-id="555cc-3150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3150">Description</span></span> | <span data-ttu-id="555cc-3151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555cc-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="555cc-3152">storedProcedureName</span></span> |<span data-ttu-id="555cc-3153">Specificare il nome della stored procedure nel database SQL di Azure o Azure SQL Data Warehouse rappresentato dal servizio collegato che usa la tabella di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="555cc-3154">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3154">Yes</span></span> |
| <span data-ttu-id="555cc-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="555cc-3155">storedProcedureParameters</span></span> |<span data-ttu-id="555cc-3156">Specificare i valori dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="555cc-3157">Se è necessario passare null per un parametro, usare la sintassi "param1": null (tutte lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="555cc-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="555cc-3158">Vedere l'esempio seguente per informazioni sull'uso di questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="555cc-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="555cc-3159">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3159">No</span></span> |

<span data-ttu-id="555cc-3160">Se si specifica un set di dati di input, questo dovrà essere disponibile (in stato 'Ready') per l'esecuzione dell'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="555cc-3161">Il set di dati di input non può essere usato nella stored procedure come parametro.</span><span class="sxs-lookup"><span data-stu-id="555cc-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="555cc-3162">Viene usato solo per verificare la dipendenza prima di iniziare l'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="555cc-3163">È necessario specificare un set di dati di output per un'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="555cc-3164">Il set di dati di output specifica la **pianificazione** per le attività della stored procedure (ogni ora, ogni settimana, ogni mese e così via).</span><span class="sxs-lookup"><span data-stu-id="555cc-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="555cc-3165">Il set di dati di output deve usare un **servizio collegato** che faccia riferimento a un database SQL di Azure, a un Azure SQL Data Warehouse o a un database SQL Server in cui si vuole che venga eseguita la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="555cc-3166">Il set di dati di output può essere usato per passare il risultato della stored procedure per la successiva elaborazione da parte di un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="555cc-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="555cc-3167">Data Factory non scrive tuttavia automaticamente l'output di una stored procedure in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="555cc-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="555cc-3168">È la stored procedure a scrivere dati in una tabella SQL cui punta il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="555cc-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="555cc-3169">In alcuni casi, il set di dati di output può essere un **set di dati fittizio**che viene usato solo per specificare la pianificazione per l'esecuzione dell'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="555cc-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="555cc-3170">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="555cc-3171">Per altre informazioni, vedere [Attività stored procedure](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="555cc-3172">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="555cc-3172">.NET custom activity</span></span>
<span data-ttu-id="555cc-3173">In una definizione JSON di attività personalizzata .NET è possibile specificare le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="555cc-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="555cc-3174">Il tipo di proprietà dell'attività deve essere impostato su **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="555cc-3175">È necessario creare un servizio collegato Azure HDInsight o Azure Batch e specificare il nome del servizio collegato come valore della proprietà **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="555cc-3176">Quando il tipo di attività è impostato su DotNetActivity, nella sezione **typeProperties** sono supportate le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="555cc-3177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="555cc-3177">Property</span></span> | <span data-ttu-id="555cc-3178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="555cc-3178">Description</span></span> | <span data-ttu-id="555cc-3179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="555cc-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="555cc-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="555cc-3180">AssemblyName</span></span> | <span data-ttu-id="555cc-3181">Nome dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="555cc-3181">Name of the assembly.</span></span> <span data-ttu-id="555cc-3182">Nell'esempio è: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="555cc-3183">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3183">Yes</span></span> |
| <span data-ttu-id="555cc-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="555cc-3184">EntryPoint</span></span> |<span data-ttu-id="555cc-3185">Nome della classe che implementa l'interfaccia IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="555cc-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="555cc-3186">Nell'esempio è: **MyDotNetActivityNS.MyDotNetActivity** dove MyDotNetActivityNS è lo spazio dei nomi e MyDotNetActivity è la classe.</span><span class="sxs-lookup"><span data-stu-id="555cc-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="555cc-3187">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3187">Yes</span></span> | 
| <span data-ttu-id="555cc-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="555cc-3188">PackageLinkedService</span></span> | <span data-ttu-id="555cc-3189">None del servizio collegato di Archiviazione di Azure che punta all'archivio BLOB contenente il file con estensione zip dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="555cc-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="555cc-3190">Nell'esempio è: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="555cc-3191">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3191">Yes</span></span> |
| <span data-ttu-id="555cc-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="555cc-3192">PackageFile</span></span> | <span data-ttu-id="555cc-3193">Nome del file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="555cc-3193">Name of the zip file.</span></span> <span data-ttu-id="555cc-3194">Nell'esempio è: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="555cc-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="555cc-3195">Sì</span><span class="sxs-lookup"><span data-stu-id="555cc-3195">Yes</span></span> |
| <span data-ttu-id="555cc-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="555cc-3196">extendedProperties</span></span> | <span data-ttu-id="555cc-3197">Proprietà estese che è possibile definire e passare al codice .NET.</span><span class="sxs-lookup"><span data-stu-id="555cc-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="555cc-3198">In questo esempio, la variabile **SliceStart** è impostata su un valore basato sulla variabile di sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="555cc-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="555cc-3199">No</span><span class="sxs-lookup"><span data-stu-id="555cc-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="555cc-3200">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="555cc-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="555cc-3201">Per altre informazioni, vedere l'articolo relativo all'[uso delle attività personalizzate in Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="555cc-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="555cc-3202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="555cc-3202">Next Steps</span></span>
<span data-ttu-id="555cc-3203">Vedere le esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="555cc-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="555cc-3204">Esercitazione: Creare una pipeline con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="555cc-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="555cc-3205">Esercitazione: Creare una pipeline con un'attività di Hive</span><span class="sxs-lookup"><span data-stu-id="555cc-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)