---
title: aaaAzure Data Factory - riferimento agli script JSON | Documenti Microsoft
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="54475-103">Azure Data Factory - Informazioni di riferimento sugli script JSON</span><span class="sxs-lookup"><span data-stu-id="54475-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="54475-104">Questo articolo fornisce gli schemi JSON ed esempi per la definizione di entità di Azure Data Factory (pipeline, attività, set di dati e servizi collegati).</span><span class="sxs-lookup"><span data-stu-id="54475-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="54475-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="54475-105">Pipeline</span></span> 
<span data-ttu-id="54475-106">struttura di alto livello per una definizione di pipeline Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="54475-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="54475-107">Nella tabella seguente vengono descritte le proprietà di hello all'interno della pipeline hello definizione JSON:</span><span class="sxs-lookup"><span data-stu-id="54475-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="54475-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-108">Property</span></span> | <span data-ttu-id="54475-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-109">Description</span></span> | <span data-ttu-id="54475-110">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="54475-111">name</span><span class="sxs-lookup"><span data-stu-id="54475-111">name</span></span> | <span data-ttu-id="54475-112">Nome della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="54475-112">Name of hello pipeline.</span></span> <span data-ttu-id="54475-113">Specificare un nome che rappresenta l'azione di hello che hello attività o pipeline è toodo configurato</span><span class="sxs-lookup"><span data-stu-id="54475-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="54475-114">Numero massimo di caratteri: 260</span><span class="sxs-lookup"><span data-stu-id="54475-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="54475-115">Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</span><span class="sxs-lookup"><span data-stu-id="54475-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="54475-116">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</span><span class="sxs-lookup"><span data-stu-id="54475-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="54475-117">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-117">Yes</span></span> |
| <span data-ttu-id="54475-118">description</span><span class="sxs-lookup"><span data-stu-id="54475-118">description</span></span> |<span data-ttu-id="54475-119">Testo che descrive le attività hello o una pipeline viene utilizzata per</span><span class="sxs-lookup"><span data-stu-id="54475-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="54475-120">No</span><span class="sxs-lookup"><span data-stu-id="54475-120">No</span></span> |
| <span data-ttu-id="54475-121">attività</span><span class="sxs-lookup"><span data-stu-id="54475-121">activities</span></span> | <span data-ttu-id="54475-122">Contiene un elenco di attività.</span><span class="sxs-lookup"><span data-stu-id="54475-122">Contains a list of activities.</span></span> | <span data-ttu-id="54475-123">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-123">Yes</span></span> |
| <span data-ttu-id="54475-124">start</span><span class="sxs-lookup"><span data-stu-id="54475-124">start</span></span> |<span data-ttu-id="54475-125">Data-ora di inizio per la pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="54475-126">Devono essere nel [formato ISO](http://en.wikipedia.org/wiki/ISO_8601),</span><span class="sxs-lookup"><span data-stu-id="54475-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="54475-127">ad esempio: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="54475-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="54475-128">È possibile toospecify un'ora locale, ad esempio un'ora EST.</span><span class="sxs-lookup"><span data-stu-id="54475-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="54475-129">Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.</span><span class="sxs-lookup"><span data-stu-id="54475-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="54475-130">Hello proprietà start ed end insieme specificano il periodo attivo per la pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="54475-131">Le sezioni di output vengono generate solo in questo periodo attivo.</span><span class="sxs-lookup"><span data-stu-id="54475-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="54475-132">No</span><span class="sxs-lookup"><span data-stu-id="54475-132">No</span></span><br/><br/><span data-ttu-id="54475-133">Se si specifica un valore per la proprietà di fine hello, è necessario specificare una valore per la proprietà di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="54475-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="54475-134">Hello ora di inizio e fine può essere entrambi vuoti toocreate una pipeline.</span><span class="sxs-lookup"><span data-stu-id="54475-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="54475-135">È necessario specificare entrambi i valori tooset un periodo attivo per hello pipeline toorun.</span><span class="sxs-lookup"><span data-stu-id="54475-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="54475-136">Se non si specifica l'ora di inizio e fine durante la creazione di una pipeline, è possibile impostare utilizzando il cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="54475-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="54475-137">end</span><span class="sxs-lookup"><span data-stu-id="54475-137">end</span></span> |<span data-ttu-id="54475-138">Data-ora di fine per la pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="54475-139">Se specificate, devono essere in formato ISO.</span><span class="sxs-lookup"><span data-stu-id="54475-139">If specified must be in ISO format.</span></span> <span data-ttu-id="54475-140">Ad esempio: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="54475-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="54475-141">È possibile toospecify un'ora locale, ad esempio un'ora EST.</span><span class="sxs-lookup"><span data-stu-id="54475-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="54475-142">Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.</span><span class="sxs-lookup"><span data-stu-id="54475-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="54475-143">pipeline hello toorun specificare in modo indefinito, 9999-09-09 come valore di hello per la proprietà di fine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="54475-144">No</span><span class="sxs-lookup"><span data-stu-id="54475-144">No</span></span> <br/><br/><span data-ttu-id="54475-145">Se si specifica un valore per la proprietà di avvio hello, è necessario specificare una valore per la proprietà di fine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="54475-146">Vedere le note per hello **avviare** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="54475-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="54475-147">isPaused</span></span> |<span data-ttu-id="54475-148">Se set tootrue hello pipeline non viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="54475-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="54475-149">Valore predefinito = false.</span><span class="sxs-lookup"><span data-stu-id="54475-149">Default value = false.</span></span> <span data-ttu-id="54475-150">È possibile utilizzare questa proprietà tooenable o disabilitare.</span><span class="sxs-lookup"><span data-stu-id="54475-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="54475-151">No</span><span class="sxs-lookup"><span data-stu-id="54475-151">No</span></span> |
| <span data-ttu-id="54475-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="54475-152">pipelineMode</span></span> |<span data-ttu-id="54475-153">metodo Hello per la pianificazione viene eseguita per la pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="54475-154">I valori consentiti sono scheduled (predefinito) e onetime.</span><span class="sxs-lookup"><span data-stu-id="54475-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="54475-155">'Pianificata' indica che pipeline hello viene eseguita in un intervallo di tempo specificato in base tooits periodo attivo (ora di inizio e fine).</span><span class="sxs-lookup"><span data-stu-id="54475-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="54475-156">'Unica' indica che pipeline hello viene eseguito una sola volta.</span><span class="sxs-lookup"><span data-stu-id="54475-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="54475-157">Al momento, dopo aver creato una pipeline monouso non è possibile modificarla o aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="54475-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="54475-158">Per informazioni dettagliate sull'impostazione onetime, vedere la sezione [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="54475-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="54475-159">No</span><span class="sxs-lookup"><span data-stu-id="54475-159">No</span></span> |
| <span data-ttu-id="54475-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="54475-160">expirationTime</span></span> |<span data-ttu-id="54475-161">Periodo di tempo dopo la creazione per i quali hello pipeline sia valido e deve rimanere disponibile.</span><span class="sxs-lookup"><span data-stu-id="54475-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="54475-162">Se non è attiva qualsiasi, non è riuscita, o in attesa di esecuzione, la pipeline di hello viene eliminata automaticamente una volta raggiunta l'ora di scadenza hello.</span><span class="sxs-lookup"><span data-stu-id="54475-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="54475-163">No</span><span class="sxs-lookup"><span data-stu-id="54475-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="54475-164">Attività</span><span class="sxs-lookup"><span data-stu-id="54475-164">Activity</span></span> 
<span data-ttu-id="54475-165">struttura di alto livello Hello per un'attività all'interno di una definizione di pipeline (elemento di attività) è il seguente:</span><span class="sxs-lookup"><span data-stu-id="54475-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="54475-166">Seguente tabella vengono descritti proprietà hello all'interno di attività hello definizione JSON:</span><span class="sxs-lookup"><span data-stu-id="54475-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="54475-167">Tag</span><span class="sxs-lookup"><span data-stu-id="54475-167">Tag</span></span> | <span data-ttu-id="54475-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-168">Description</span></span> | <span data-ttu-id="54475-169">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-170">name</span><span class="sxs-lookup"><span data-stu-id="54475-170">name</span></span> |<span data-ttu-id="54475-171">Nome dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-171">Name of hello activity.</span></span> <span data-ttu-id="54475-172">Specificare un nome che rappresenta l'azione di hello che attività hello è configurato toodo</span><span class="sxs-lookup"><span data-stu-id="54475-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="54475-173">Numero massimo di caratteri: 260</span><span class="sxs-lookup"><span data-stu-id="54475-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="54475-174">Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</span><span class="sxs-lookup"><span data-stu-id="54475-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="54475-175">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</span><span class="sxs-lookup"><span data-stu-id="54475-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="54475-176">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-176">Yes</span></span> |
| <span data-ttu-id="54475-177">description</span><span class="sxs-lookup"><span data-stu-id="54475-177">description</span></span> |<span data-ttu-id="54475-178">Testo che descrive le attività di hello viene utilizzato per.</span><span class="sxs-lookup"><span data-stu-id="54475-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="54475-179">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-179">Yes</span></span> |
| <span data-ttu-id="54475-180">type</span><span class="sxs-lookup"><span data-stu-id="54475-180">type</span></span> |<span data-ttu-id="54475-181">Specifica il tipo di hello di attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="54475-182">Vedere hello [archivi dati](#data-stores) e [le attività di trasformazione dati](#data-transformation-activities) sezioni per diversi tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="54475-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="54475-183">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-183">Yes</span></span> |
| <span data-ttu-id="54475-184">inputs</span><span class="sxs-lookup"><span data-stu-id="54475-184">inputs</span></span> |<span data-ttu-id="54475-185">Tabelle di input utilizzate dall'attività hello</span><span class="sxs-lookup"><span data-stu-id="54475-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="54475-186">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-186">Yes</span></span> |
| <span data-ttu-id="54475-187">outputs</span><span class="sxs-lookup"><span data-stu-id="54475-187">outputs</span></span> |<span data-ttu-id="54475-188">Tabelle di output utilizzate dall'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="54475-189">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-189">Yes</span></span> |
| <span data-ttu-id="54475-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54475-190">linkedServiceName</span></span> |<span data-ttu-id="54475-191">Nome del servizio hello collegato usato dall'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="54475-192">Un'attività potrebbe essere necessario specificare il servizio collegato hello che collega l'ambiente di calcolo necessarie toohello.</span><span class="sxs-lookup"><span data-stu-id="54475-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="54475-193">Sì per attività di HDInsight, attività di Azure Machine Learning e attività delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="54475-194">No per tutto il resto</span><span class="sxs-lookup"><span data-stu-id="54475-194">No for all others</span></span> |
| <span data-ttu-id="54475-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="54475-195">typeProperties</span></span> |<span data-ttu-id="54475-196">Le proprietà nella sezione typeProperties hello dipendono dal tipo di attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="54475-197">No</span><span class="sxs-lookup"><span data-stu-id="54475-197">No</span></span> |
| <span data-ttu-id="54475-198">policy</span><span class="sxs-lookup"><span data-stu-id="54475-198">policy</span></span> |<span data-ttu-id="54475-199">Criteri che influiscono sul comportamento di hello in fase di esecuzione dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="54475-200">Se vengono omessi, vengono usati i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="54475-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="54475-201">No</span><span class="sxs-lookup"><span data-stu-id="54475-201">No</span></span> |
| <span data-ttu-id="54475-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="54475-202">scheduler</span></span> |<span data-ttu-id="54475-203">proprietà "utilità di pianificazione" è utilizzato toodefine desiderato pianificazione per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="54475-204">Le sottoproprietà sono hello stesso hello quelle nella hello [proprietà disponibilità in un set di dati](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="54475-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="54475-205">No</span><span class="sxs-lookup"><span data-stu-id="54475-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="54475-206">Criteri</span><span class="sxs-lookup"><span data-stu-id="54475-206">Policies</span></span>
<span data-ttu-id="54475-207">Criteri influiscono sul comportamento di hello in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione hello di una tabella.</span><span class="sxs-lookup"><span data-stu-id="54475-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="54475-208">Hello nella tabella seguente fornisce dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="54475-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="54475-209">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-209">Property</span></span> | <span data-ttu-id="54475-210">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-210">Permitted values</span></span> | <span data-ttu-id="54475-211">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="54475-211">Default Value</span></span> | <span data-ttu-id="54475-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-213">Concorrenza</span><span class="sxs-lookup"><span data-stu-id="54475-213">concurrency</span></span> |<span data-ttu-id="54475-214">Integer </span><span class="sxs-lookup"><span data-stu-id="54475-214">Integer</span></span> <br/><br/><span data-ttu-id="54475-215">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="54475-215">Max value: 10</span></span> |<span data-ttu-id="54475-216">1</span><span class="sxs-lookup"><span data-stu-id="54475-216">1</span></span> |<span data-ttu-id="54475-217">Numero di esecuzioni simultanee dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="54475-218">Determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse.</span><span class="sxs-lookup"><span data-stu-id="54475-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="54475-219">Ad esempio, se un'attività deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="54475-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="54475-220">executionPriorityOrder</span></span> |<span data-ttu-id="54475-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="54475-221">NewestFirst</span></span><br/><br/><span data-ttu-id="54475-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="54475-222">OldestFirst</span></span> |<span data-ttu-id="54475-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="54475-223">OldestFirst</span></span> |<span data-ttu-id="54475-224">Determina hello ordinamento delle sezioni di dati che vengono elaborate.</span><span class="sxs-lookup"><span data-stu-id="54475-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="54475-225">Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="54475-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="54475-226">Se si imposta executionPriorityOrder di hello toobe NewestFirst, slice hello 17: 00 viene elaborata per prima.</span><span class="sxs-lookup"><span data-stu-id="54475-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="54475-227">Allo stesso modo se si imposta executionPriorityORder di hello toobe OldestFIrst, viene elaborato sezione hello 4 ore.</span><span class="sxs-lookup"><span data-stu-id="54475-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="54475-228">retry</span><span class="sxs-lookup"><span data-stu-id="54475-228">retry</span></span> |<span data-ttu-id="54475-229">Integer </span><span class="sxs-lookup"><span data-stu-id="54475-229">Integer</span></span><br/><br/><span data-ttu-id="54475-230">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="54475-230">Max value can be 10</span></span> |<span data-ttu-id="54475-231">0</span><span class="sxs-lookup"><span data-stu-id="54475-231">0</span></span> |<span data-ttu-id="54475-232">Numero di tentativi prima dell'elaborazione dei dati di hello per sezione hello è contrassegnato come errore.</span><span class="sxs-lookup"><span data-stu-id="54475-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="54475-233">Esecuzione di attività per una sezione di dati viene ripetuta backup toohello specificato numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="54475-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="54475-234">Riprova Hello viene eseguito appena possibile dopo l'errore hello.</span><span class="sxs-lookup"><span data-stu-id="54475-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="54475-235">timeout</span><span class="sxs-lookup"><span data-stu-id="54475-235">timeout</span></span> |<span data-ttu-id="54475-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="54475-236">TimeSpan</span></span> |<span data-ttu-id="54475-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="54475-237">00:00:00</span></span> |<span data-ttu-id="54475-238">Timeout per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-238">Timeout for hello activity.</span></span> <span data-ttu-id="54475-239">Esempio: 00:10:00 (implica un timeout di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="54475-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="54475-240">Se un valore viene omesso o è 0, hello timeout è infinito.</span><span class="sxs-lookup"><span data-stu-id="54475-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="54475-241">Se il tempo di elaborazione di dati hello in una sezione supera il valore di timeout di hello, viene annullata e sistema hello tenta l'elaborazione di hello tooretry.</span><span class="sxs-lookup"><span data-stu-id="54475-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="54475-242">numero di tentativi di Hello dipende dalla proprietà retry hello.</span><span class="sxs-lookup"><span data-stu-id="54475-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="54475-243">Quando si verifica il timeout, hello stato tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="54475-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="54475-244">delay</span><span class="sxs-lookup"><span data-stu-id="54475-244">delay</span></span> |<span data-ttu-id="54475-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="54475-245">TimeSpan</span></span> |<span data-ttu-id="54475-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="54475-246">00:00:00</span></span> |<span data-ttu-id="54475-247">Specificare il ritardo di hello prima dell'elaborazione di dati di hello sezione inizia.</span><span class="sxs-lookup"><span data-stu-id="54475-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="54475-248">esecuzione di Hello dell'attività per una sezione di dati viene avviata dopo hello ritardo passato hello previsto tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="54475-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="54475-249">Esempio: 00:10:00 (implica un ritardo di 10 minuti)</span><span class="sxs-lookup"><span data-stu-id="54475-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="54475-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="54475-250">longRetry</span></span> |<span data-ttu-id="54475-251">Integer </span><span class="sxs-lookup"><span data-stu-id="54475-251">Integer</span></span><br/><br/><span data-ttu-id="54475-252">Valore massimo: 10</span><span class="sxs-lookup"><span data-stu-id="54475-252">Max value: 10</span></span> |<span data-ttu-id="54475-253">1</span><span class="sxs-lookup"><span data-stu-id="54475-253">1</span></span> |<span data-ttu-id="54475-254">numero di Hello di long tentativi prima dell'esecuzione della sezione hello è non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="54475-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="54475-255">I tentativi longRetry sono distanziati da longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="54475-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="54475-256">Pertanto, se è necessario toospecify un intervallo tra tentativi, usare quindi longRetry.</span><span class="sxs-lookup"><span data-stu-id="54475-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="54475-257">Se vengono specificati Retry e longRetry, ogni tentativo longRetry include nuovi tentativi e numero massimo di tentativi di hello è Riprova * longRetry.</span><span class="sxs-lookup"><span data-stu-id="54475-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="54475-258">Ad esempio, se si dispone delle seguenti impostazioni in criteri attività hello hello:</span><span class="sxs-lookup"><span data-stu-id="54475-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="54475-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="54475-259">Retry: 3</span></span><br/><span data-ttu-id="54475-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="54475-260">longRetry: 2</span></span><br/><span data-ttu-id="54475-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="54475-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="54475-262">Si supponga che sia presente solo una sezione tooexecute (lo stato è in attesa) e l'esecuzione dell'attività hello ha esito negativo di ogni volta.</span><span class="sxs-lookup"><span data-stu-id="54475-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="54475-263">All’inizio vi saranno tre tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="54475-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="54475-264">Dopo ogni tentativo, lo stato della sezione hello sarà Retry.</span><span class="sxs-lookup"><span data-stu-id="54475-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="54475-265">Dopo aver innanzitutto 3 tentativi di failover, lo stato della sezione hello sarebbe LongRetry.</span><span class="sxs-lookup"><span data-stu-id="54475-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="54475-266">Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi.</span><span class="sxs-lookup"><span data-stu-id="54475-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="54475-267">Successivamente, lo stato della sezione hello sarà Failed e non più necessario tentativi.</span><span class="sxs-lookup"><span data-stu-id="54475-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="54475-268">Quindi, sono stati eseguiti 6 tentativi.</span><span class="sxs-lookup"><span data-stu-id="54475-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="54475-269">Se qualsiasi esecuzione ha esito positivo, lo stato della sezione hello sarà Ready e non più tentativi.</span><span class="sxs-lookup"><span data-stu-id="54475-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="54475-270">longRetry possono essere utilizzati in situazioni in cui dipendenti dati arrivano a volte non deterministica o hello ambiente generale non è affidabile in cui l'elaborazione dei dati si verifica.</span><span class="sxs-lookup"><span data-stu-id="54475-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="54475-271">In questi casi, potrebbe non aiutare eseguire tentativi uno dopo l'altro e in questo modo, dopo un intervallo di risultati in fase di hello desiderato output.</span><span class="sxs-lookup"><span data-stu-id="54475-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="54475-272">Attenzione: non impostare valori elevati per longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="54475-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="54475-273">In genere, valori più elevati comportano altri problemi sistemici.</span><span class="sxs-lookup"><span data-stu-id="54475-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="54475-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="54475-274">longRetryInterval</span></span> |<span data-ttu-id="54475-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="54475-275">TimeSpan</span></span> |<span data-ttu-id="54475-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="54475-276">00:00:00</span></span> |<span data-ttu-id="54475-277">ritardo Hello tra nuovi tentativi lunghi</span><span class="sxs-lookup"><span data-stu-id="54475-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="54475-278">sezione typeProperties</span><span class="sxs-lookup"><span data-stu-id="54475-278">typeProperties section</span></span>
<span data-ttu-id="54475-279">sezione typeProperties Hello è diverso per ogni attività.</span><span class="sxs-lookup"><span data-stu-id="54475-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="54475-280">Le attività di trasformazione dispongono solo le proprietà del tipo hello.</span><span class="sxs-lookup"><span data-stu-id="54475-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="54475-281">Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="54475-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="54475-282">**Attività di copia** contiene due sottosezioni nella sezione typeProperties hello: **origine** e **sink**.</span><span class="sxs-lookup"><span data-stu-id="54475-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="54475-283">Vedere [archivi dati](#data-stores) sezione in questo articolo per esempi che mostrano come toouse dati memorizzati come origine e/o un sink di JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="54475-284">Esempio di una pipeline di copia</span><span class="sxs-lookup"><span data-stu-id="54475-284">Sample copy pipeline</span></span>
<span data-ttu-id="54475-285">In hello seguente della pipeline di esempio, un'attività di tipo è **copia** in hello **attività** sezione.</span><span class="sxs-lookup"><span data-stu-id="54475-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="54475-286">In questo esempio, hello [attività di copia](data-factory-data-movement-activities.md) copia i dati da un database di SQL Azure tooan di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="54475-287">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="54475-287">Note hello following points:</span></span>

* <span data-ttu-id="54475-288">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="54475-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="54475-289">Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="54475-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="54475-290">In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.</span><span class="sxs-lookup"><span data-stu-id="54475-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="54475-291">Vedere [archivi dati](#data-stores) sezione in questo articolo per esempi che mostrano come toouse dati memorizzati come origine e/o un sink di JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="54475-292">Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="54475-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="54475-293">Esempio di una pipeline di trasformazione</span><span class="sxs-lookup"><span data-stu-id="54475-293">Sample transformation pipeline</span></span>
<span data-ttu-id="54475-294">In hello seguente della pipeline di esempio, un'attività di tipo è **HDInsightHive** in hello **attività** sezione.</span><span class="sxs-lookup"><span data-stu-id="54475-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="54475-295">In questo esempio, hello [attività Hive di HDInsight](data-factory-hive-activity.md) Trasforma i dati da un archivio Blob di Azure eseguendo un file di script Hive in un cluster Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54475-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="54475-296">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="54475-296">Note hello following points:</span></span> 

* <span data-ttu-id="54475-297">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="54475-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="54475-298">file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **AzureStorageLinkedService**) e in  **script** cartella nel contenitore hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="54475-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="54475-299">Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="54475-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="54475-300">Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="54475-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="54475-301">Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: creare i primi dati tooprocess pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="54475-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="54475-302">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-302">Linked service</span></span>
<span data-ttu-id="54475-303">struttura di alto livello per una definizione di servizio collegato Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="54475-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="54475-304">Seguente tabella vengono descritti proprietà hello all'interno di attività hello definizione JSON:</span><span class="sxs-lookup"><span data-stu-id="54475-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="54475-305">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-305">Property</span></span> | <span data-ttu-id="54475-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-306">Description</span></span> | <span data-ttu-id="54475-307">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="54475-308">name</span><span class="sxs-lookup"><span data-stu-id="54475-308">name</span></span> | <span data-ttu-id="54475-309">Nome del servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-309">Name of hello linked service.</span></span> | <span data-ttu-id="54475-310">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-310">Yes</span></span> | 
| <span data-ttu-id="54475-311">proprietà - tipo</span><span class="sxs-lookup"><span data-stu-id="54475-311">properties - type</span></span> | <span data-ttu-id="54475-312">Tipo di servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-312">Type of hello linked service.</span></span> <span data-ttu-id="54475-313">Ad esempio: archiviazione di Azure, database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="54475-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="54475-314">typeProperties</span></span> | <span data-ttu-id="54475-315">sezione typeProperties Hello dispone degli elementi che sono diverse per ogni archivio dati o l'ambiente di calcolo.</span><span class="sxs-lookup"><span data-stu-id="54475-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="54475-316">Vedere [archivi dati](#datastores) sezione per tutti i dati di hello servizi collegati dell'archivio e [calcolo ambienti](#compute-environments) per hello tutti i servizi collegati di calcolo</span><span class="sxs-lookup"><span data-stu-id="54475-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="54475-317">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-317">Dataset</span></span> 
<span data-ttu-id="54475-318">Un set di dati in Azure Data Factory viene definito come segue:</span><span class="sxs-lookup"><span data-stu-id="54475-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="54475-319">Hello nella tabella seguente vengono descritte le proprietà in hello sopra JSON:</span><span class="sxs-lookup"><span data-stu-id="54475-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="54475-320">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-320">Property</span></span> | <span data-ttu-id="54475-321">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-321">Description</span></span> | <span data-ttu-id="54475-322">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-322">Required</span></span> | <span data-ttu-id="54475-323">Default</span><span class="sxs-lookup"><span data-stu-id="54475-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-324">name</span><span class="sxs-lookup"><span data-stu-id="54475-324">name</span></span> | <span data-ttu-id="54475-325">Nome del set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-325">Name of hello dataset.</span></span> <span data-ttu-id="54475-326">Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="54475-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="54475-327">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-327">Yes</span></span> |<span data-ttu-id="54475-328">ND</span><span class="sxs-lookup"><span data-stu-id="54475-328">NA</span></span> |
| <span data-ttu-id="54475-329">type</span><span class="sxs-lookup"><span data-stu-id="54475-329">type</span></span> | <span data-ttu-id="54475-330">tipo di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-330">Type of hello dataset.</span></span> <span data-ttu-id="54475-331">Specificare uno dei tipi di hello supportati da Data Factory di Azure (ad esempio: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="54475-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="54475-332">Vedere [archivi dati](#data-stores) sezione per tutti hello archivi dati e i tipi di set di dati supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="54475-333">structure</span><span class="sxs-lookup"><span data-stu-id="54475-333">structure</span></span> | <span data-ttu-id="54475-334">Schema di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-334">Schema of hello dataset.</span></span> <span data-ttu-id="54475-335">Contiene le colonne, i tipi e così via.</span><span class="sxs-lookup"><span data-stu-id="54475-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="54475-336">No</span><span class="sxs-lookup"><span data-stu-id="54475-336">No</span></span> |<span data-ttu-id="54475-337">ND</span><span class="sxs-lookup"><span data-stu-id="54475-337">NA</span></span> |
| <span data-ttu-id="54475-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="54475-338">typeProperties</span></span> | <span data-ttu-id="54475-339">Le proprietà corrispondenti toohello tipo selezionato.</span><span class="sxs-lookup"><span data-stu-id="54475-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="54475-340">Vedere la sezione [Archivi dati](#data-stores) per i tipi supportati e le rispettive proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="54475-341">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-341">Yes</span></span> |<span data-ttu-id="54475-342">ND</span><span class="sxs-lookup"><span data-stu-id="54475-342">NA</span></span> |
| <span data-ttu-id="54475-343">external</span><span class="sxs-lookup"><span data-stu-id="54475-343">external</span></span> | <span data-ttu-id="54475-344">Valore booleano flag toospecify se un set di dati generata in modo esplicito tramite una pipeline di factory di dati o non.</span><span class="sxs-lookup"><span data-stu-id="54475-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="54475-345">No</span><span class="sxs-lookup"><span data-stu-id="54475-345">No</span></span> |<span data-ttu-id="54475-346">false</span><span class="sxs-lookup"><span data-stu-id="54475-346">false</span></span> |
| <span data-ttu-id="54475-347">disponibilità</span><span class="sxs-lookup"><span data-stu-id="54475-347">availability</span></span> | <span data-ttu-id="54475-348">Definisce l'elaborazione di finestra o sezionamento modello per la produzione di set di dati hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="54475-349">Per informazioni dettagliate sul set di dati hello sezionamento modello, vedere [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="54475-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="54475-350">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-350">Yes</span></span> |<span data-ttu-id="54475-351">ND</span><span class="sxs-lookup"><span data-stu-id="54475-351">NA</span></span> |
| <span data-ttu-id="54475-352">policy</span><span class="sxs-lookup"><span data-stu-id="54475-352">policy</span></span> |<span data-ttu-id="54475-353">Definisce i criteri di hello o condizione hello che devono soddisfare le sezioni di hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="54475-354">Per informazioni dettagliate, vedere la sezione [Criteri di set di dati](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="54475-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="54475-355">No</span><span class="sxs-lookup"><span data-stu-id="54475-355">No</span></span> |<span data-ttu-id="54475-356">ND</span><span class="sxs-lookup"><span data-stu-id="54475-356">NA</span></span> |

<span data-ttu-id="54475-357">Ogni colonna hello **struttura** sezione contiene hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="54475-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="54475-358">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-358">Property</span></span> | <span data-ttu-id="54475-359">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-359">Description</span></span> | <span data-ttu-id="54475-360">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-361">name</span><span class="sxs-lookup"><span data-stu-id="54475-361">name</span></span> |<span data-ttu-id="54475-362">Nome della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="54475-362">Name of hello column.</span></span> |<span data-ttu-id="54475-363">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-363">Yes</span></span> |
| <span data-ttu-id="54475-364">type</span><span class="sxs-lookup"><span data-stu-id="54475-364">type</span></span> |<span data-ttu-id="54475-365">Tipo di dati della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="54475-365">Data type of hello column.</span></span>  |<span data-ttu-id="54475-366">No</span><span class="sxs-lookup"><span data-stu-id="54475-366">No</span></span> |
| <span data-ttu-id="54475-367">culture</span><span class="sxs-lookup"><span data-stu-id="54475-367">culture</span></span> |<span data-ttu-id="54475-368">Impostazioni cultura toobe utilizzato quando il tipo specificato e il tipo .NET basato su .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="54475-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="54475-369">Il valore predefinito è `en-us`.</span><span class="sxs-lookup"><span data-stu-id="54475-369">Default is `en-us`.</span></span> |<span data-ttu-id="54475-370">No</span><span class="sxs-lookup"><span data-stu-id="54475-370">No</span></span> |
| <span data-ttu-id="54475-371">format</span><span class="sxs-lookup"><span data-stu-id="54475-371">format</span></span> |<span data-ttu-id="54475-372">Formato stringa toobe utilizzato quando il tipo specificato e il tipo .NET `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="54475-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="54475-373">No</span><span class="sxs-lookup"><span data-stu-id="54475-373">No</span></span> |

<span data-ttu-id="54475-374">Nell'esempio seguente di hello, set di dati hello ha tre colonne `slicetimestamp`, `projectname`, e `pageviews` e sono di tipo: String, String e decimali rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="54475-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="54475-375">Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **disponibilità** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="54475-376">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-376">Property</span></span> | <span data-ttu-id="54475-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-377">Description</span></span> | <span data-ttu-id="54475-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-378">Required</span></span> | <span data-ttu-id="54475-379">Default</span><span class="sxs-lookup"><span data-stu-id="54475-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-380">frequency</span><span class="sxs-lookup"><span data-stu-id="54475-380">frequency</span></span> |<span data-ttu-id="54475-381">Specifica l'unità di tempo hello per la produzione di sezione set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="54475-382"><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese</span><span class="sxs-lookup"><span data-stu-id="54475-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="54475-383">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-383">Yes</span></span> |<span data-ttu-id="54475-384">ND</span><span class="sxs-lookup"><span data-stu-id="54475-384">NA</span></span> |
| <span data-ttu-id="54475-385">interval</span><span class="sxs-lookup"><span data-stu-id="54475-385">interval</span></span> |<span data-ttu-id="54475-386">Specifica un moltiplicatore per la frequenza.</span><span class="sxs-lookup"><span data-stu-id="54475-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="54475-387">"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta.</span><span class="sxs-lookup"><span data-stu-id="54475-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="54475-388">Se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="54475-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="54475-389"><b>Nota</b>: se si specifica Frequency come Minute, si consiglia di impostare hello intervallo toono inferiore a 15</span><span class="sxs-lookup"><span data-stu-id="54475-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="54475-390">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-390">Yes</span></span> |<span data-ttu-id="54475-391">ND</span><span class="sxs-lookup"><span data-stu-id="54475-391">NA</span></span> |
| <span data-ttu-id="54475-392">style</span><span class="sxs-lookup"><span data-stu-id="54475-392">style</span></span> |<span data-ttu-id="54475-393">Specifica se la sezione hello deve essere prodotta all'hello inizio/fine dell'intervallo "hello".</span><span class="sxs-lookup"><span data-stu-id="54475-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="54475-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="54475-394">StartOfInterval</span></span></li><li><span data-ttu-id="54475-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="54475-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="54475-396">Se Frequency è impostato tooMonth e style è impostato tooEndOfInterval, hello sezione viene prodotta hello ultimo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="54475-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="54475-397">Se lo stile di hello è impostato tooStartOfInterval, hello sezione viene prodotta hello primo giorno del mese.</span><span class="sxs-lookup"><span data-stu-id="54475-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="54475-398">Se Frequency è impostato tooDay e style è impostato tooEndOfInterval, sezione hello viene prodotta nell'ultima ora del giorno hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="54475-399">Se Frequency è impostato tooHour e style è impostato tooEndOfInterval, sezione hello viene prodotta alla fine hello ora hello.</span><span class="sxs-lookup"><span data-stu-id="54475-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="54475-400">Ad esempio, per una sezione per periodo 1 PM – 2 PM, sezione di hello viene prodotta alle 14.00.</span><span class="sxs-lookup"><span data-stu-id="54475-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="54475-401">No</span><span class="sxs-lookup"><span data-stu-id="54475-401">No</span></span> |<span data-ttu-id="54475-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="54475-402">EndOfInterval</span></span> |
| <span data-ttu-id="54475-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="54475-403">anchorDateTime</span></span> |<span data-ttu-id="54475-404">Definisce una posizione assoluta di hello in utilizzata dai limiti di sezione dell'utilità di pianificazione toocompute set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="54475-405"><b>Nota</b>: se hello AnchorDateTime ha parti di date più granulari frequenza hello in hello parti più granulari verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="54475-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="54475-406">Ad esempio, se hello <b>intervallo</b> è <b>oraria</b> (frequenza: ora e intervallo: 1) e hello <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>quindi hello <b>minuti e secondi</b> parti di hello AnchorDateTime verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="54475-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="54475-407">No</span><span class="sxs-lookup"><span data-stu-id="54475-407">No</span></span> |<span data-ttu-id="54475-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="54475-408">01/01/0001</span></span> |
| <span data-ttu-id="54475-409">offset</span><span class="sxs-lookup"><span data-stu-id="54475-409">offset</span></span> |<span data-ttu-id="54475-410">Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati.</span><span class="sxs-lookup"><span data-stu-id="54475-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="54475-411"><b>Nota</b>: se vengono specificati sia anchorDateTime che offset, il risultato di hello è MAIUSC hello combinato.</span><span class="sxs-lookup"><span data-stu-id="54475-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="54475-412">No</span><span class="sxs-lookup"><span data-stu-id="54475-412">No</span></span> |<span data-ttu-id="54475-413">ND</span><span class="sxs-lookup"><span data-stu-id="54475-413">NA</span></span> |

<span data-ttu-id="54475-414">Hello seguente sezione di disponibilità specifica il set di dati di output di hello è creati ogni ora (o) input set di dati è disponibile ogni ora:</span><span class="sxs-lookup"><span data-stu-id="54475-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="54475-415">Hello **criteri** sezione nella definizione di set di dati definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare.</span><span class="sxs-lookup"><span data-stu-id="54475-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="54475-416">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="54475-416">Policy Name</span></span> | <span data-ttu-id="54475-417">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-417">Description</span></span> | <span data-ttu-id="54475-418">Troppo applicato</span><span class="sxs-lookup"><span data-stu-id="54475-418">Applied too</span></span>| <span data-ttu-id="54475-419">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-419">Required</span></span> | <span data-ttu-id="54475-420">Default</span><span class="sxs-lookup"><span data-stu-id="54475-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="54475-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="54475-421">minimumSizeMB</span></span> |<span data-ttu-id="54475-422">Convalida i dati di hello un **blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte).</span><span class="sxs-lookup"><span data-stu-id="54475-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="54475-423">BLOB Azure</span><span class="sxs-lookup"><span data-stu-id="54475-423">Azure Blob</span></span> |<span data-ttu-id="54475-424">No</span><span class="sxs-lookup"><span data-stu-id="54475-424">No</span></span> |<span data-ttu-id="54475-425">ND</span><span class="sxs-lookup"><span data-stu-id="54475-425">NA</span></span> |
| <span data-ttu-id="54475-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="54475-426">minimumRows</span></span> |<span data-ttu-id="54475-427">Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe.</span><span class="sxs-lookup"><span data-stu-id="54475-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="54475-428">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-428">Azure SQL Database</span></span></li><li><span data-ttu-id="54475-429">tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-429">Azure Table</span></span></li></ul> |<span data-ttu-id="54475-430">No</span><span class="sxs-lookup"><span data-stu-id="54475-430">No</span></span> |<span data-ttu-id="54475-431">ND</span><span class="sxs-lookup"><span data-stu-id="54475-431">NA</span></span> |

<span data-ttu-id="54475-432">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="54475-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="54475-433">A meno che un set di dati non sia generato da Azure Data Factory, deve essere contrassegnato come **external**.</span><span class="sxs-lookup"><span data-stu-id="54475-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="54475-434">Questa impostazione si applica in genere input toohello della prima attività in una pipeline, a meno che l'attività o il concatenamento della pipeline in uso.</span><span class="sxs-lookup"><span data-stu-id="54475-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="54475-435">Nome</span><span class="sxs-lookup"><span data-stu-id="54475-435">Name</span></span> | <span data-ttu-id="54475-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-436">Description</span></span> | <span data-ttu-id="54475-437">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-437">Required</span></span> | <span data-ttu-id="54475-438">Default Value</span><span class="sxs-lookup"><span data-stu-id="54475-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="54475-439">dataDelay</span></span> |<span data-ttu-id="54475-440">Tempo toodelay hello controllo disponibilità hello di dati esterni di hello di hello dato sezione.</span><span class="sxs-lookup"><span data-stu-id="54475-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="54475-441">Ad esempio, se hello i dati sono disponibili ogni ora, hello controllo toosee hello i dati esterni sono disponibili e la sezione corrispondente di hello sia Ready può essere posticipato utilizzando dataDelay.</span><span class="sxs-lookup"><span data-stu-id="54475-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="54475-442">Si applica solo toohello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="54475-442">Only applies toohello present time.</span></span>  <span data-ttu-id="54475-443">Ad esempio, se è 1:00 PM subito e questo valore è 10 minuti, convalida hello inizia alle ore 1:10.</span><span class="sxs-lookup"><span data-stu-id="54475-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="54475-444">Questa impostazione influisce sulle sezioni in hello precedente (sezioni con ora di fine sezione + dataDelay < ora) vengono elaborati senza alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="54475-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="54475-445">Periodo di tempo maggiore di 23:59 ore necessario toospecified utilizzando hello `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="54475-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="54475-446">Ad esempio, toospecify 24 ore, non utilizzare 24:00:00; Utilizzare invece 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="54475-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="54475-447">Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="54475-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="54475-448">Per 1 giorno e 4 ore, specificare 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="54475-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="54475-449">No</span><span class="sxs-lookup"><span data-stu-id="54475-449">No</span></span> |<span data-ttu-id="54475-450">0</span><span class="sxs-lookup"><span data-stu-id="54475-450">0</span></span> |
| <span data-ttu-id="54475-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="54475-451">retryInterval</span></span> |<span data-ttu-id="54475-452">tempo di attesa Hello tra un errore e hello successivo tentativo.</span><span class="sxs-lookup"><span data-stu-id="54475-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="54475-453">Se un tentativo non riesce, il successivo tentativo di hello è dopo retryInterval.</span><span class="sxs-lookup"><span data-stu-id="54475-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="54475-454">Se è 1:00 PM al momento, iniziamo hello primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="54475-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="54475-455">Se hello durata toocomplete hello primo controllo di convalida è 1 minuto e operazione hello non riuscita, tentativo successivo di hello è 1:00 + 1 min (durata) + 1 minuto (intervallo tra tentativi) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="54475-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="54475-456">Per le sezioni hello precedente, non si verifica alcun ritardo.</span><span class="sxs-lookup"><span data-stu-id="54475-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="54475-457">Riprova Hello si verifica immediatamente.</span><span class="sxs-lookup"><span data-stu-id="54475-457">hello retry happens immediately.</span></span> |<span data-ttu-id="54475-458">No</span><span class="sxs-lookup"><span data-stu-id="54475-458">No</span></span> |<span data-ttu-id="54475-459">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="54475-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="54475-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-460">retryTimeout</span></span> |<span data-ttu-id="54475-461">timeout di Hello per ogni nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="54475-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="54475-462">Se questa proprietà è impostata too10 minuti, hello toobe esigenze convalida completata entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="54475-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="54475-463">Se impiega più tempo rispetto alla convalida hello tooperform di 10 minuti, hello ripetere verifica il timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="54475-464">Se tutti i tentativi per la convalida di hello scade, sezione hello è contrassegnata come TimedOut.</span><span class="sxs-lookup"><span data-stu-id="54475-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="54475-465">No</span><span class="sxs-lookup"><span data-stu-id="54475-465">No</span></span> |<span data-ttu-id="54475-466">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="54475-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="54475-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="54475-467">maximumRetry</span></span> |<span data-ttu-id="54475-468">Numero di volte in cui toocheck per la disponibilità di dati esterni hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="54475-469">Hello consentito valore massimo è 10.</span><span class="sxs-lookup"><span data-stu-id="54475-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="54475-470">No</span><span class="sxs-lookup"><span data-stu-id="54475-470">No</span></span> |<span data-ttu-id="54475-471">3</span><span class="sxs-lookup"><span data-stu-id="54475-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="54475-472">Archivi dati</span><span class="sxs-lookup"><span data-stu-id="54475-472">DATA STORES</span></span>
<span data-ttu-id="54475-473">Hello [servizio collegato](#linked-service) descrizioni sezione forniti per gli elementi JSON che sono tipi di servizi collegati tooall comuni.</span><span class="sxs-lookup"><span data-stu-id="54475-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="54475-474">Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati tooeach specifico.</span><span class="sxs-lookup"><span data-stu-id="54475-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="54475-475">Hello [Dataset](#dataset) descrizioni sezione forniti per gli elementi JSON che sono tipi di set di dati tooall comuni.</span><span class="sxs-lookup"><span data-stu-id="54475-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="54475-476">Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati tooeach specifico.</span><span class="sxs-lookup"><span data-stu-id="54475-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="54475-477">Hello [attività](#activity) descrizioni sezione forniti per gli elementi JSON che sono tipi tooall comuni di attività.</span><span class="sxs-lookup"><span data-stu-id="54475-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="54475-478">Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati specifico tooeach quando viene utilizzata come origine/sink in un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="54475-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="54475-479">Fare clic sul collegamento hello per archivio hello si è interessati negli schemi JSON hello toosee per il servizio collegato, set di dati e hello origine/sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="54475-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="54475-480">Categoria</span><span class="sxs-lookup"><span data-stu-id="54475-480">Category</span></span> | <span data-ttu-id="54475-481">Archivio dati</span><span class="sxs-lookup"><span data-stu-id="54475-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="54475-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="54475-482">**Azure**</span></span> |[<span data-ttu-id="54475-483">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="54475-484">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="54475-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="54475-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="54475-486">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="54475-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="54475-488">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="54475-489">Archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="54475-490">**Database**</span><span class="sxs-lookup"><span data-stu-id="54475-490">**Databases**</span></span> |[<span data-ttu-id="54475-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="54475-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="54475-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="54475-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="54475-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="54475-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="54475-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="54475-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="54475-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="54475-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="54475-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="54475-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54475-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="54475-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="54475-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="54475-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="54475-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="54475-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="54475-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="54475-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="54475-501">**NoSQL**</span></span> |[<span data-ttu-id="54475-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="54475-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="54475-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="54475-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="54475-504">**File**</span><span class="sxs-lookup"><span data-stu-id="54475-504">**File**</span></span> |[<span data-ttu-id="54475-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="54475-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="54475-506">File system</span><span class="sxs-lookup"><span data-stu-id="54475-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="54475-507">FTP</span><span class="sxs-lookup"><span data-stu-id="54475-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="54475-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="54475-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="54475-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="54475-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="54475-510">**Altro**</span><span class="sxs-lookup"><span data-stu-id="54475-510">**Others**</span></span> |[<span data-ttu-id="54475-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="54475-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="54475-512">OData</span><span class="sxs-lookup"><span data-stu-id="54475-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="54475-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="54475-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="54475-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="54475-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="54475-515">Tabella Web</span><span class="sxs-lookup"><span data-stu-id="54475-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="54475-516">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-517">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-517">Linked service</span></span>
<span data-ttu-id="54475-518">Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="54475-519">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="54475-520">toolink la data factory tooa account di archiviazione di Azure tramite hello **chiave dell'account**, creare un servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="54475-521">il set hello servizio collegato di toodefine una risorsa di archiviazione di Azure **tipo** di hello servizio collegato troppo**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="54475-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="54475-522">Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-523">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-523">Property</span></span> | <span data-ttu-id="54475-524">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-524">Description</span></span> | <span data-ttu-id="54475-525">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-526">connectionString</span></span> |<span data-ttu-id="54475-527">Specificare le informazioni necessarie tooconnect tooAzure archiviazione per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="54475-528">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="54475-529">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="54475-530">Servizio collegato di firma di accesso condiviso Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="54475-531">servizio sa di archiviazione di Azure collegati Hello consente toolink un Account di archiviazione Azure tooan data factory di Azure tramite una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="54475-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="54475-532">Fornisce data factory di hello con accesso limitato/scadenza tooall/specifiche risorse (blob/contenitore) nell'archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="54475-533">toolink la data factory tooa account di archiviazione di Azure tramite la firma di accesso condiviso, creare un servizio sa di archiviazione di Azure collegati.</span><span class="sxs-lookup"><span data-stu-id="54475-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="54475-534">il servizio hello set toodefine un SAS di archiviazione di Azure collegato **tipo** di hello servizio collegato troppo**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="54475-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="54475-535">Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="54475-536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-536">Property</span></span> | <span data-ttu-id="54475-537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-537">Description</span></span> | <span data-ttu-id="54475-538">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="54475-539">sasUri</span></span> |<span data-ttu-id="54475-540">Specificare le risorse di archiviazione di Azure toohello URI firma di accesso condiviso, ad esempio una tabella, contenitore o blob.</span><span class="sxs-lookup"><span data-stu-id="54475-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="54475-541">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="54475-542">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-542">Example</span></span>

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

<span data-ttu-id="54475-543">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione BLOB di Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-544">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-544">Dataset</span></span>
<span data-ttu-id="54475-545">toodefine un set di dati Blob di Azure, hello set **tipo** del set di dati hello troppo**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="54475-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="54475-546">Quindi, specificare le proprietà specifiche di Blob di Azure in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-547">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-547">Property</span></span> | <span data-ttu-id="54475-548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-548">Description</span></span> | <span data-ttu-id="54475-549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-550">folderPath</span></span> |<span data-ttu-id="54475-551">Percorso toohello contenitore e della cartella nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="54475-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="54475-552">Esempio: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="54475-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="54475-553">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-553">Yes</span></span> |
| <span data-ttu-id="54475-554">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-554">fileName</span></span> |<span data-ttu-id="54475-555">Nome del blob hello.</span><span class="sxs-lookup"><span data-stu-id="54475-555">Name of hello blob.</span></span> <span data-ttu-id="54475-556">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="54475-557">Se si specifica un nome di file, hello attività (incluso copia) funziona su hello Blob specifico.</span><span class="sxs-lookup"><span data-stu-id="54475-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="54475-558">Quando non è stato specificato il nome del file, copia include tutti i BLOB in folderPath hello per input set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="54475-559">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: dati. <Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="54475-560">No</span><span class="sxs-lookup"><span data-stu-id="54475-560">No</span></span> |
| <span data-ttu-id="54475-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-561">partitionedBy</span></span> |<span data-ttu-id="54475-562">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="54475-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="54475-563">È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54475-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="54475-564">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="54475-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-565">No</span><span class="sxs-lookup"><span data-stu-id="54475-565">No</span></span> |
| <span data-ttu-id="54475-566">format</span><span class="sxs-lookup"><span data-stu-id="54475-566">format</span></span> | <span data-ttu-id="54475-567">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-568">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-569">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-570">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-571">No</span><span class="sxs-lookup"><span data-stu-id="54475-571">No</span></span> |
| <span data-ttu-id="54475-572">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-572">compression</span></span> | <span data-ttu-id="54475-573">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-574">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-575">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="54475-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-576">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-577">No</span><span class="sxs-lookup"><span data-stu-id="54475-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-578">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-578">Example</span></span>

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


<span data-ttu-id="54475-579">Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="54475-580">BlobSource in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="54475-581">Se si copiano dati da un archivio Blob di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**BlobSource**e specificare le seguenti proprietà in hello * * origine * * sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="54475-582">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-582">Property</span></span> | <span data-ttu-id="54475-583">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-583">Description</span></span> | <span data-ttu-id="54475-584">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-584">Allowed values</span></span> | <span data-ttu-id="54475-585">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-586">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-586">recursive</span></span> |<span data-ttu-id="54475-587">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-588">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="54475-588">True (default value), False</span></span> |<span data-ttu-id="54475-589">No</span><span class="sxs-lookup"><span data-stu-id="54475-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="54475-590">Esempio: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="54475-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="54475-591">BlobSink in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="54475-592">Se si copiano dati tooan archiviazione Blob di Azure, impostare hello **tipo di sink** di hello attività di copia troppo**BlobSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-593">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-593">Property</span></span> | <span data-ttu-id="54475-594">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-594">Description</span></span> | <span data-ttu-id="54475-595">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-595">Allowed values</span></span> | <span data-ttu-id="54475-596">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="54475-597">copyBehavior</span></span> |<span data-ttu-id="54475-598">Definisce il comportamento di copia hello quando origine hello è BlobSource o file System.</span><span class="sxs-lookup"><span data-stu-id="54475-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="54475-599"><b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="54475-600">percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="54475-601"><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello presenti hello primo livelli della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="54475-602">i file di destinazione Hello hanno nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="54475-603"><b>Oggetto (impostazione predefinita):</b> unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="54475-604">Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="54475-605">No</span><span class="sxs-lookup"><span data-stu-id="54475-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="54475-606">Esempio: BlobSink</span><span class="sxs-lookup"><span data-stu-id="54475-606">Example: BlobSink</span></span>

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

<span data-ttu-id="54475-607">Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="54475-608">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="54475-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-609">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-609">Linked service</span></span>
<span data-ttu-id="54475-610">un servizio collegato archivio Azure Data Lake toodefine, imposta il tipo di hello hello servizio collegato troppo**AzureDataLakeStore**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-611">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-611">Property</span></span> | <span data-ttu-id="54475-612">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-612">Description</span></span> | <span data-ttu-id="54475-613">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-614">type</span><span class="sxs-lookup"><span data-stu-id="54475-614">type</span></span> | <span data-ttu-id="54475-615">proprietà di tipo Hello deve essere impostata su: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="54475-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="54475-616">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-616">Yes</span></span> |
| <span data-ttu-id="54475-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="54475-617">dataLakeStoreUri</span></span> | <span data-ttu-id="54475-618">Specificare le informazioni su hello account archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="54475-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="54475-619">È presente nel seguente formato hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="54475-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="54475-620">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-620">Yes</span></span> |
| <span data-ttu-id="54475-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="54475-621">subscriptionId</span></span> | <span data-ttu-id="54475-622">Sottoscrizione di Azure toowhich Id archivio Data Lake appartiene.</span><span class="sxs-lookup"><span data-stu-id="54475-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="54475-623">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="54475-623">Required for sink</span></span> |
| <span data-ttu-id="54475-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="54475-624">resourceGroupName</span></span> | <span data-ttu-id="54475-625">Toowhich di nome gruppo di risorse di Azure archivio Data Lake appartiene.</span><span class="sxs-lookup"><span data-stu-id="54475-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="54475-626">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="54475-626">Required for sink</span></span> |
| <span data-ttu-id="54475-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="54475-627">servicePrincipalId</span></span> | <span data-ttu-id="54475-628">Specificare un ID client. dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="54475-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="54475-629">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="54475-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="54475-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="54475-630">servicePrincipalKey</span></span> | <span data-ttu-id="54475-631">Specificare la chiave dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-631">Specify hello application's key.</span></span> | <span data-ttu-id="54475-632">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="54475-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="54475-633">tenant</span><span class="sxs-lookup"><span data-stu-id="54475-633">tenant</span></span> | <span data-ttu-id="54475-634">Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="54475-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="54475-635">È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="54475-636">Sì (per l'autenticazione di un'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="54475-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="54475-637">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="54475-637">authorization</span></span> | <span data-ttu-id="54475-638">Fare clic su **Authorize** pulsante hello **Editor delle Data Factory** e immettere le credenziali dell'utente che assegna hello autogenerati autorizzazione URL toothis proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="54475-639">Sì (per l'autenticazione basata su credenziali utente)</span><span class="sxs-lookup"><span data-stu-id="54475-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="54475-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="54475-640">sessionId</span></span> | <span data-ttu-id="54475-641">Id di sessione OAuth della sessione di autorizzazione OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="54475-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="54475-642">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="54475-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="54475-643">Questa impostazione viene generata automaticamente quando si usa l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="54475-644">Sì (per l'autenticazione basata su credenziali utente)</span><span class="sxs-lookup"><span data-stu-id="54475-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="54475-645">Esempio: uso dell'autenticazione basata su entità servizio</span><span class="sxs-lookup"><span data-stu-id="54475-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="54475-646">Esempio: uso dell'autenticazione basata su credenziali utente</span><span class="sxs-lookup"><span data-stu-id="54475-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="54475-647">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-648">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-648">Dataset</span></span>
<span data-ttu-id="54475-649">toodefine un set di dati di archivio Azure Data Lake, hello set **tipo** del set di dati hello troppo**AzureDataLakeStore**e specificare le proprietà in hello seguenti hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-650">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-650">Property</span></span> | <span data-ttu-id="54475-651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-651">Description</span></span> | <span data-ttu-id="54475-652">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-653">folderPath</span></span> |<span data-ttu-id="54475-654">Percorso toohello contenitore e della cartella in hello Azure Data Lake archiviare.</span><span class="sxs-lookup"><span data-stu-id="54475-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="54475-655">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-655">Yes</span></span> |
| <span data-ttu-id="54475-656">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-656">fileName</span></span> |<span data-ttu-id="54475-657">Nome del file hello nell'archivio Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="54475-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="54475-658">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="54475-659">Se si specifica un nome di file, attività hello (inclusi copia) funziona su file specifiche hello.</span><span class="sxs-lookup"><span data-stu-id="54475-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="54475-660">Quando non è stato specificato il nome del file, copia include tutti i file in folderPath hello per input set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="54475-661">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: dati. <Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="54475-662">No</span><span class="sxs-lookup"><span data-stu-id="54475-662">No</span></span> |
| <span data-ttu-id="54475-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-663">partitionedBy</span></span> |<span data-ttu-id="54475-664">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="54475-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="54475-665">È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54475-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="54475-666">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="54475-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-667">No</span><span class="sxs-lookup"><span data-stu-id="54475-667">No</span></span> |
| <span data-ttu-id="54475-668">format</span><span class="sxs-lookup"><span data-stu-id="54475-668">format</span></span> | <span data-ttu-id="54475-669">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-670">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-671">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-672">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-673">No</span><span class="sxs-lookup"><span data-stu-id="54475-673">No</span></span> |
| <span data-ttu-id="54475-674">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-674">compression</span></span> | <span data-ttu-id="54475-675">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-676">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-677">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="54475-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-678">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-679">No</span><span class="sxs-lookup"><span data-stu-id="54475-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-680">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-680">Example</span></span>
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

<span data-ttu-id="54475-681">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="54475-682">Origine Azure Data Lake Store in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="54475-683">Se si copiano dati da un archivio Azure Data Lake, impostare hello **tipo di origine** di hello attività di copia troppo**AzureDataLakeStoreSource**e specificare le seguenti proprietà in hello **origine**  sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="54475-684">**AzureDataLakeStoreSource** supporta le proprietà seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="54475-685">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-685">Property</span></span> | <span data-ttu-id="54475-686">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-686">Description</span></span> | <span data-ttu-id="54475-687">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-687">Allowed values</span></span> | <span data-ttu-id="54475-688">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-689">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-689">recursive</span></span> |<span data-ttu-id="54475-690">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-691">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="54475-691">True (default value), False</span></span> |<span data-ttu-id="54475-692">No</span><span class="sxs-lookup"><span data-stu-id="54475-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="54475-693">Esempio: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="54475-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="54475-694">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="54475-695">Sink Azure Data Lake Store in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="54475-696">Se si copia un archivio dati tooan Azure Data Lake, impostare hello **tipo di sink** di hello attività di copia troppo**AzureDataLakeStoreSink**e specificare le seguenti proprietà in hello **sink**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-697">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-697">Property</span></span> | <span data-ttu-id="54475-698">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-698">Description</span></span> | <span data-ttu-id="54475-699">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-699">Allowed values</span></span> | <span data-ttu-id="54475-700">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="54475-701">copyBehavior</span></span> |<span data-ttu-id="54475-702">Specifica il comportamento di copia hello.</span><span class="sxs-lookup"><span data-stu-id="54475-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="54475-703"><b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="54475-704">percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="54475-705"><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="54475-706">file di destinazione Hello vengono creati con il nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="54475-707"><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="54475-708">Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="54475-709">No</span><span class="sxs-lookup"><span data-stu-id="54475-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="54475-710">Esempio: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="54475-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="54475-711">Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="54475-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="54475-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="54475-713">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-713">Linked service</span></span>
<span data-ttu-id="54475-714">il servizio hello set toodefine un database di Azure Cosmos collegato **tipo** di hello servizio collegato troppo**DocumentDb**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-715">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="54475-715">**Property**</span></span> | <span data-ttu-id="54475-716">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="54475-716">**Description**</span></span> | <span data-ttu-id="54475-717">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="54475-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-718">connectionString</span></span> |<span data-ttu-id="54475-719">Specificare le informazioni necessarie tooconnect tooAzure DB Cosmos database.</span><span class="sxs-lookup"><span data-stu-id="54475-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="54475-720">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-721">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-721">Example</span></span>

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
<span data-ttu-id="54475-722">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-723">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-723">Dataset</span></span>
<span data-ttu-id="54475-724">toodefine un set di dati di Azure Cosmos DB hello set **tipo** del set di dati hello troppo**DocumentDbCollection**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-725">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="54475-725">**Property**</span></span> | <span data-ttu-id="54475-726">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="54475-726">**Description**</span></span> | <span data-ttu-id="54475-727">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="54475-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="54475-728">collectionName</span></span> |<span data-ttu-id="54475-729">Nome della raccolta di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="54475-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="54475-730">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-731">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-731">Example</span></span>

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
<span data-ttu-id="54475-732">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="54475-733">Origine della raccolta Azure Cosmos DB in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="54475-734">Se si copiano dati da un database di Azure Cosmos, impostare hello **tipo di origine** di hello attività di copia troppo**DocumentDbCollectionSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-735">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="54475-735">**Property**</span></span> | <span data-ttu-id="54475-736">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="54475-736">**Description**</span></span> | <span data-ttu-id="54475-737">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="54475-737">**Allowed values**</span></span> | <span data-ttu-id="54475-738">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="54475-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-739">query</span><span class="sxs-lookup"><span data-stu-id="54475-739">query</span></span> |<span data-ttu-id="54475-740">Specificare i dati di tooread query hello.</span><span class="sxs-lookup"><span data-stu-id="54475-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="54475-741">Stringa di query supportata da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="54475-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="54475-742">Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="54475-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="54475-743">No</span><span class="sxs-lookup"><span data-stu-id="54475-743">No</span></span> <br/><br/><span data-ttu-id="54475-744">Se non specificato, hello istruzione SQL eseguita:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="54475-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="54475-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="54475-745">nestingSeparator</span></span> |<span data-ttu-id="54475-746">Carattere speciale tooindicate che hello documento nidificato</span><span class="sxs-lookup"><span data-stu-id="54475-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="54475-747">Qualsiasi carattere.</span><span class="sxs-lookup"><span data-stu-id="54475-747">Any character.</span></span> <br/><br/><span data-ttu-id="54475-748">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="54475-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="54475-749">Data Factory di Azure consente gerarchia toodenote utente tramite nestingSeparator, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="54475-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="54475-750">in hello esempi sopra riportati.</span><span class="sxs-lookup"><span data-stu-id="54475-750">in hello above examples.</span></span> <span data-ttu-id="54475-751">Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella.</span><span class="sxs-lookup"><span data-stu-id="54475-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="54475-752">No</span><span class="sxs-lookup"><span data-stu-id="54475-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-753">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="54475-754">Sink della raccolta Azure Cosmos DB in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="54475-755">Se si copiano dati tooAzure DB Cosmos, impostare hello **tipo di sink** di hello attività di copia troppo**DocumentDbCollectionSink**e specificare le seguenti proprietà in hello **sink**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-756">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="54475-756">**Property**</span></span> | <span data-ttu-id="54475-757">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="54475-757">**Description**</span></span> | <span data-ttu-id="54475-758">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="54475-758">**Allowed values**</span></span> | <span data-ttu-id="54475-759">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="54475-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="54475-760">nestingSeparator</span></span> |<span data-ttu-id="54475-761">È necessario un carattere speciale nel hello origine colonna nome tooindicate annidati di documento.</span><span class="sxs-lookup"><span data-stu-id="54475-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="54475-762">Ad esempio sopra: `Name.First` nell'output di hello tabella produce hello seguente struttura JSON nel documento Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="54475-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="54475-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="54475-763">"Name": {</span></span><br/>    <span data-ttu-id="54475-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="54475-764">"First": "John"</span></span><br/><span data-ttu-id="54475-765">},</span><span class="sxs-lookup"><span data-stu-id="54475-765">},</span></span> |<span data-ttu-id="54475-766">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="54475-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="54475-767">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="54475-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="54475-768">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="54475-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="54475-769">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="54475-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="54475-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-770">writeBatchSize</span></span> |<span data-ttu-id="54475-771">Numero parallelo di richieste di documenti di toocreate tooAzure DB Cosmos del servizio.</span><span class="sxs-lookup"><span data-stu-id="54475-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="54475-772">È possibile ottimizzare le prestazioni di hello quando si copiano dati da e verso Azure Cosmos DB usando questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="54475-773">È possibile prevedere prestazioni migliori quando si aumenta viene raggiunto writeBatchSize poiché vengono inviate altre richieste in parallelo tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54475-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="54475-774">Tuttavia, occorre tooavoid la limitazione delle richieste che possono generare il messaggio di errore hello: "Richiesta frequenza è grande".</span><span class="sxs-lookup"><span data-stu-id="54475-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="54475-775">La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile utilizzare un migliore hello toohave raccolta (ad esempio, S3) la maggior parte delle velocità effettiva disponibile (2.500 richiesta unità al secondo).</span><span class="sxs-lookup"><span data-stu-id="54475-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="54475-776">Integer</span><span class="sxs-lookup"><span data-stu-id="54475-776">Integer</span></span> |<span data-ttu-id="54475-777">No (valore predefinito: 5)</span><span class="sxs-lookup"><span data-stu-id="54475-777">No (default: 5)</span></span> |
| <span data-ttu-id="54475-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-778">writeBatchTimeout</span></span> |<span data-ttu-id="54475-779">Tempo di attesa per hello operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="54475-780">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-780">timespan</span></span><br/><br/> <span data-ttu-id="54475-781">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="54475-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="54475-782">No</span><span class="sxs-lookup"><span data-stu-id="54475-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-783">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="54475-784">Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="54475-785">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-786">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-786">Linked service</span></span>
<span data-ttu-id="54475-787">il set hello servizio collegato di toodefine un Database di SQL Azure **tipo** di hello servizio collegato troppo**AzureSqlDatabase**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-788">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-788">Property</span></span> | <span data-ttu-id="54475-789">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-789">Description</span></span> | <span data-ttu-id="54475-790">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-791">connectionString</span></span> |<span data-ttu-id="54475-792">Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="54475-793">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-794">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-794">Example</span></span>
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

<span data-ttu-id="54475-795">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-796">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-796">Dataset</span></span>
<span data-ttu-id="54475-797">toodefine un set di dati di Database SQL di Azure, hello set **tipo** del set di dati hello troppo**AzureSqlTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-798">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-798">Property</span></span> | <span data-ttu-id="54475-799">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-799">Description</span></span> | <span data-ttu-id="54475-800">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-801">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-801">tableName</span></span> |<span data-ttu-id="54475-802">Nome della tabella hello o della vista nell'istanza di Database SQL di Azure hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="54475-803">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-804">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-804">Example</span></span>

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
<span data-ttu-id="54475-805">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="54475-806">Origine SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="54475-807">Se si copiano dati da un Database SQL di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**SqlSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-808">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-808">Property</span></span> | <span data-ttu-id="54475-809">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-809">Description</span></span> | <span data-ttu-id="54475-810">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-810">Allowed values</span></span> | <span data-ttu-id="54475-811">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="54475-812">sqlReaderQuery</span></span> |<span data-ttu-id="54475-813">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-814">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-814">SQL query string.</span></span> <span data-ttu-id="54475-815">Esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-816">No</span><span class="sxs-lookup"><span data-stu-id="54475-816">No</span></span> |
| <span data-ttu-id="54475-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="54475-818">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="54475-819">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="54475-820">No</span><span class="sxs-lookup"><span data-stu-id="54475-820">No</span></span> |
| <span data-ttu-id="54475-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-821">storedProcedureParameters</span></span> |<span data-ttu-id="54475-822">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="54475-823">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="54475-823">Name/value pairs.</span></span> <span data-ttu-id="54475-824">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="54475-825">No</span><span class="sxs-lookup"><span data-stu-id="54475-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-826">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-826">Example</span></span>

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
<span data-ttu-id="54475-827">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="54475-828">Sink SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="54475-829">Se si copiano dati tooAzure Database SQL, impostare hello **tipo di sink** di hello attività di copia troppo**SqlSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-830">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-830">Property</span></span> | <span data-ttu-id="54475-831">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-831">Description</span></span> | <span data-ttu-id="54475-832">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-832">Allowed values</span></span> | <span data-ttu-id="54475-833">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-834">writeBatchTimeout</span></span> |<span data-ttu-id="54475-835">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="54475-836">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-836">timespan</span></span><br/><br/> <span data-ttu-id="54475-837">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="54475-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="54475-838">No</span><span class="sxs-lookup"><span data-stu-id="54475-838">No</span></span> |
| <span data-ttu-id="54475-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-839">writeBatchSize</span></span> |<span data-ttu-id="54475-840">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="54475-841">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="54475-841">Integer (number of rows)</span></span> |<span data-ttu-id="54475-842">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="54475-842">No (default: 10000)</span></span> |
| <span data-ttu-id="54475-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="54475-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="54475-844">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="54475-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="54475-845">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="54475-845">A query statement.</span></span> |<span data-ttu-id="54475-846">No</span><span class="sxs-lookup"><span data-stu-id="54475-846">No</span></span> |
| <span data-ttu-id="54475-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="54475-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="54475-848">Specificare un nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="54475-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="54475-849">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="54475-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="54475-850">No</span><span class="sxs-lookup"><span data-stu-id="54475-850">No</span></span> |
| <span data-ttu-id="54475-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="54475-852">Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="54475-853">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="54475-854">No</span><span class="sxs-lookup"><span data-stu-id="54475-854">No</span></span> |
| <span data-ttu-id="54475-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-855">storedProcedureParameters</span></span> |<span data-ttu-id="54475-856">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="54475-857">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="54475-857">Name/value pairs.</span></span> <span data-ttu-id="54475-858">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="54475-859">No</span><span class="sxs-lookup"><span data-stu-id="54475-859">No</span></span> |
| <span data-ttu-id="54475-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="54475-860">sqlWriterTableType</span></span> |<span data-ttu-id="54475-861">Specificare un toobe nome tipo di tabella utilizzati in hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="54475-862">Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati.</span><span class="sxs-lookup"><span data-stu-id="54475-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="54475-863">Codice della stored procedure può unire dati hello copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="54475-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="54475-864">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="54475-864">A table type name.</span></span> |<span data-ttu-id="54475-865">No</span><span class="sxs-lookup"><span data-stu-id="54475-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-866">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-866">Example</span></span>

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

<span data-ttu-id="54475-867">Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="54475-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-869">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-869">Linked service</span></span>
<span data-ttu-id="54475-870">il servizio hello set toodefine un Data Warehouse di SQL Azure collegato **tipo** di hello servizio collegato troppo**AzureSqlDW**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-871">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-871">Property</span></span> | <span data-ttu-id="54475-872">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-872">Description</span></span> | <span data-ttu-id="54475-873">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-874">connectionString</span></span> |<span data-ttu-id="54475-875">Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="54475-876">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="54475-877">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-877">Example</span></span>

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

<span data-ttu-id="54475-878">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-879">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-879">Dataset</span></span>
<span data-ttu-id="54475-880">toodefine un set di dati di Azure SQL Data Warehouse, hello set **tipo** del set di dati hello troppo**AzureSqlDWTable**e specificare le proprietà in hello seguenti hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-881">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-881">Property</span></span> | <span data-ttu-id="54475-882">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-882">Description</span></span> | <span data-ttu-id="54475-883">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-884">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-884">tableName</span></span> |<span data-ttu-id="54475-885">Nome della tabella hello o della vista nel database di Azure SQL Data Warehouse hello che hello servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="54475-886">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-887">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-887">Example</span></span>

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

<span data-ttu-id="54475-888">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="54475-889">Origine SQL DW nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="54475-890">Se si copiano dati da Azure SQL Data Warehouse, impostare hello **tipo di origine** di hello attività di copia troppo**SqlDWSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-891">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-891">Property</span></span> | <span data-ttu-id="54475-892">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-892">Description</span></span> | <span data-ttu-id="54475-893">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-893">Allowed values</span></span> | <span data-ttu-id="54475-894">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="54475-895">sqlReaderQuery</span></span> |<span data-ttu-id="54475-896">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-897">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-897">SQL query string.</span></span> <span data-ttu-id="54475-898">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-899">No</span><span class="sxs-lookup"><span data-stu-id="54475-899">No</span></span> |
| <span data-ttu-id="54475-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="54475-901">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="54475-902">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="54475-903">No</span><span class="sxs-lookup"><span data-stu-id="54475-903">No</span></span> |
| <span data-ttu-id="54475-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-904">storedProcedureParameters</span></span> |<span data-ttu-id="54475-905">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="54475-906">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="54475-906">Name/value pairs.</span></span> <span data-ttu-id="54475-907">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="54475-908">No</span><span class="sxs-lookup"><span data-stu-id="54475-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-909">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-909">Example</span></span>

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

<span data-ttu-id="54475-910">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="54475-911">Sink SQL DW nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="54475-912">Se si copiano dati tooAzure SQL Data Warehouse, impostare hello **tipo di sink** di hello attività di copia troppo**SqlDWSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-913">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-913">Property</span></span> | <span data-ttu-id="54475-914">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-914">Description</span></span> | <span data-ttu-id="54475-915">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-915">Allowed values</span></span> | <span data-ttu-id="54475-916">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="54475-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="54475-918">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="54475-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="54475-919">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="54475-919">A query statement.</span></span> |<span data-ttu-id="54475-920">No</span><span class="sxs-lookup"><span data-stu-id="54475-920">No</span></span> |
| <span data-ttu-id="54475-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="54475-921">allowPolyBase</span></span> |<span data-ttu-id="54475-922">Indica se toouse PolyBase (se applicabile) anziché meccanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="54475-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="54475-923">**Utilizzo di PolyBase è hello consigliato dei dati tooload in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="54475-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="54475-924">True </span><span class="sxs-lookup"><span data-stu-id="54475-924">True</span></span> <br/><span data-ttu-id="54475-925">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="54475-925">False (default)</span></span> |<span data-ttu-id="54475-926">No</span><span class="sxs-lookup"><span data-stu-id="54475-926">No</span></span> |
| <span data-ttu-id="54475-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="54475-927">polyBaseSettings</span></span> |<span data-ttu-id="54475-928">Un gruppo di proprietà che possono essere specificati quando hello **allowPolybase** impostata troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="54475-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="54475-929">No</span><span class="sxs-lookup"><span data-stu-id="54475-929">No</span></span> |
| <span data-ttu-id="54475-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="54475-930">rejectValue</span></span> |<span data-ttu-id="54475-931">Specifica il numero di hello o la percentuale di righe che può essere rifiutata prima di hello query ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="54475-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="54475-932">Informazioni su ulteriori informazioni su del PolyBase hello rifiutare le opzioni di hello **argomenti** sezione [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="54475-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="54475-933">0 (impostazione predefinita), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="54475-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="54475-934">No</span><span class="sxs-lookup"><span data-stu-id="54475-934">No</span></span> |
| <span data-ttu-id="54475-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="54475-935">rejectType</span></span> |<span data-ttu-id="54475-936">Specifica se l'opzione rejectValue hello è specificato come valore letterale o percentuale.</span><span class="sxs-lookup"><span data-stu-id="54475-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="54475-937">Value (impostazione predefinita), Percentage</span><span class="sxs-lookup"><span data-stu-id="54475-937">Value (default), Percentage</span></span> |<span data-ttu-id="54475-938">No</span><span class="sxs-lookup"><span data-stu-id="54475-938">No</span></span> |
| <span data-ttu-id="54475-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="54475-939">rejectSampleValue</span></span> |<span data-ttu-id="54475-940">Determina il numero di hello di tooretrieve righe prima di hello PolyBase Ricalcola percentuale hello di righe rifiutate.</span><span class="sxs-lookup"><span data-stu-id="54475-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="54475-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="54475-941">1, 2, …</span></span> |<span data-ttu-id="54475-942">Sì se **rejectType** è **percentage**</span><span class="sxs-lookup"><span data-stu-id="54475-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="54475-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="54475-943">useTypeDefault</span></span> |<span data-ttu-id="54475-944">Specifica la modalità toohandle mancano i valori nel file di testo delimitati quando PolyBase recupera i dati da file di testo hello.</span><span class="sxs-lookup"><span data-stu-id="54475-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="54475-945">Altre informazioni su questa proprietà dalla sezione argomenti hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="54475-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="54475-946">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="54475-946">True, False (default)</span></span> |<span data-ttu-id="54475-947">No</span><span class="sxs-lookup"><span data-stu-id="54475-947">No</span></span> |
| <span data-ttu-id="54475-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-948">writeBatchSize</span></span> |<span data-ttu-id="54475-949">Inserisce i dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello</span><span class="sxs-lookup"><span data-stu-id="54475-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="54475-950">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="54475-950">Integer (number of rows)</span></span> |<span data-ttu-id="54475-951">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="54475-951">No (default: 10000)</span></span> |
| <span data-ttu-id="54475-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-952">writeBatchTimeout</span></span> |<span data-ttu-id="54475-953">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="54475-954">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-954">timespan</span></span><br/><br/> <span data-ttu-id="54475-955">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="54475-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="54475-956">No</span><span class="sxs-lookup"><span data-stu-id="54475-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-957">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-957">Example</span></span>

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

<span data-ttu-id="54475-958">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="54475-959">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-960">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-960">Linked service</span></span>
<span data-ttu-id="54475-961">il servizio hello set toodefine una ricerca di Azure collegato **tipo** di hello servizio collegato troppo**AzureSearch**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-962">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-962">Property</span></span> | <span data-ttu-id="54475-963">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-963">Description</span></span> | <span data-ttu-id="54475-964">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="54475-965">URL</span><span class="sxs-lookup"><span data-stu-id="54475-965">url</span></span> | <span data-ttu-id="54475-966">URL per il servizio di ricerca di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54475-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="54475-967">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-967">Yes</span></span> |
| <span data-ttu-id="54475-968">key</span><span class="sxs-lookup"><span data-stu-id="54475-968">key</span></span> | <span data-ttu-id="54475-969">Chiave di amministrazione per hello del servizio di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="54475-970">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-971">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-971">Example</span></span>

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

<span data-ttu-id="54475-972">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-973">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-973">Dataset</span></span>
<span data-ttu-id="54475-974">toodefine un set di dati di ricerca di Azure, hello set **tipo** del set di dati hello troppo**AzureSearchIndex**e specificare le proprietà in hello seguenti hello **typeProperties** sezione :</span><span class="sxs-lookup"><span data-stu-id="54475-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-975">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-975">Property</span></span> | <span data-ttu-id="54475-976">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-976">Description</span></span> | <span data-ttu-id="54475-977">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="54475-978">type</span><span class="sxs-lookup"><span data-stu-id="54475-978">type</span></span> | <span data-ttu-id="54475-979">proprietà di tipo Hello deve essere impostata troppo**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="54475-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="54475-980">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-980">Yes</span></span> |
| <span data-ttu-id="54475-981">indexName</span><span class="sxs-lookup"><span data-stu-id="54475-981">indexName</span></span> | <span data-ttu-id="54475-982">Nome dell'indice di ricerca di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54475-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="54475-983">Data Factory di creare l'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="54475-984">indice di Hello deve esistere in ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="54475-985">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-986">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-986">Example</span></span>

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

<span data-ttu-id="54475-987">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="54475-988">Sink Indice di Ricerca di Azure in attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="54475-989">Se si sta copiando l'indice di ricerca di Azure tooan dati, impostare hello **tipo di sink** di hello attività di copia troppo**AzureSearchIndexSink**e specificare le seguenti proprietà in hello **sink**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-990">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-990">Property</span></span> | <span data-ttu-id="54475-991">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-991">Description</span></span> | <span data-ttu-id="54475-992">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-992">Allowed values</span></span> | <span data-ttu-id="54475-993">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="54475-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="54475-994">WriteBehavior</span></span> | <span data-ttu-id="54475-995">Specifica se toomerge o Sostituisci quando un documento già presente nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="54475-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="54475-996">Merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="54475-996">Merge (default)</span></span><br/><span data-ttu-id="54475-997">Carica</span><span class="sxs-lookup"><span data-stu-id="54475-997">Upload</span></span>| <span data-ttu-id="54475-998">No</span><span class="sxs-lookup"><span data-stu-id="54475-998">No</span></span> |
| <span data-ttu-id="54475-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-999">WriteBatchSize</span></span> | <span data-ttu-id="54475-1000">Carica i dati nell'indice di ricerca di Azure hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="54475-1001">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="54475-1001">1 too1,000.</span></span> <span data-ttu-id="54475-1002">Il valore predefinito è 1000.</span><span class="sxs-lookup"><span data-stu-id="54475-1002">Default value is 1000.</span></span> | <span data-ttu-id="54475-1003">No</span><span class="sxs-lookup"><span data-stu-id="54475-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1004">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1004">Example</span></span>

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

<span data-ttu-id="54475-1005">Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="54475-1006">Archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1007">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1007">Linked service</span></span>
<span data-ttu-id="54475-1008">Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="54475-1009">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="54475-1010">toolink la data factory tooa account di archiviazione di Azure tramite hello **chiave dell'account**, creare un servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="54475-1011">il set hello servizio collegato di toodefine una risorsa di archiviazione di Azure **tipo** di hello servizio collegato troppo**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="54475-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="54475-1012">Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1013">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1013">Property</span></span> | <span data-ttu-id="54475-1014">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1014">Description</span></span> | <span data-ttu-id="54475-1015">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-1016">type</span><span class="sxs-lookup"><span data-stu-id="54475-1016">type</span></span> |<span data-ttu-id="54475-1017">proprietà di tipo Hello deve essere impostata su: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="54475-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="54475-1018">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1018">Yes</span></span> |
| <span data-ttu-id="54475-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-1019">connectionString</span></span> |<span data-ttu-id="54475-1020">Specificare le informazioni necessarie tooconnect tooAzure archiviazione per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="54475-1021">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1021">Yes</span></span> |

<span data-ttu-id="54475-1022">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="54475-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="54475-1023">Servizio collegato di firma di accesso condiviso Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="54475-1024">servizio sa di archiviazione di Azure collegati Hello consente toolink un Account di archiviazione Azure tooan data factory di Azure tramite una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="54475-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="54475-1025">Fornisce data factory di hello con accesso limitato/scadenza tooall/specifiche risorse (blob/contenitore) nell'archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="54475-1026">toolink la data factory tooa account di archiviazione di Azure tramite la firma di accesso condiviso, creare un servizio sa di archiviazione di Azure collegati.</span><span class="sxs-lookup"><span data-stu-id="54475-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="54475-1027">il servizio hello set toodefine un SAS di archiviazione di Azure collegato **tipo** di hello servizio collegato troppo**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="54475-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="54475-1028">Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="54475-1029">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1029">Property</span></span> | <span data-ttu-id="54475-1030">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1030">Description</span></span> | <span data-ttu-id="54475-1031">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-1032">type</span><span class="sxs-lookup"><span data-stu-id="54475-1032">type</span></span> |<span data-ttu-id="54475-1033">proprietà di tipo Hello deve essere impostata su: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="54475-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="54475-1034">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1034">Yes</span></span> |
| <span data-ttu-id="54475-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="54475-1035">sasUri</span></span> |<span data-ttu-id="54475-1036">Specificare le risorse di archiviazione di Azure toohello URI firma di accesso condiviso, ad esempio una tabella, contenitore o blob.</span><span class="sxs-lookup"><span data-stu-id="54475-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="54475-1037">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1037">Yes</span></span> |

<span data-ttu-id="54475-1038">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="54475-1038">**Example:**</span></span>

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

<span data-ttu-id="54475-1039">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1040">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1040">Dataset</span></span>
<span data-ttu-id="54475-1041">toodefine un set di dati di tabelle di Azure, hello set **tipo** del set di dati hello troppo**AzureTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1042">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1042">Property</span></span> | <span data-ttu-id="54475-1043">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1043">Description</span></span> | <span data-ttu-id="54475-1044">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1045">tableName</span></span> |<span data-ttu-id="54475-1046">Nome della tabella hello nell'istanza di Database della tabella di Azure hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="54475-1047">Sì.</span><span class="sxs-lookup"><span data-stu-id="54475-1047">Yes.</span></span> <span data-ttu-id="54475-1048">Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="54475-1049">Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="54475-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1050">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1050">Example</span></span>

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

<span data-ttu-id="54475-1051">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="54475-1052">Origine Tabella di Azure nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="54475-1053">Se si copiano dati da Archiviazione tabelle di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**AzureTableSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1054">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1054">Property</span></span> | <span data-ttu-id="54475-1055">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1055">Description</span></span> | <span data-ttu-id="54475-1056">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1056">Allowed values</span></span> | <span data-ttu-id="54475-1057">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="54475-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="54475-1059">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1060">Stringa di query della tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-1060">Azure table query string.</span></span> <span data-ttu-id="54475-1061">Vedere gli esempi nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1061">See examples in hello next section.</span></span> |<span data-ttu-id="54475-1062">No.</span><span class="sxs-lookup"><span data-stu-id="54475-1062">No.</span></span> <span data-ttu-id="54475-1063">Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="54475-1064">Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="54475-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="54475-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="54475-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="54475-1066">Indica se ignorare hello eccezione della tabella non esiste.</span><span class="sxs-lookup"><span data-stu-id="54475-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="54475-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="54475-1067">TRUE</span></span><br/><span data-ttu-id="54475-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="54475-1068">FALSE</span></span> |<span data-ttu-id="54475-1069">No</span><span class="sxs-lookup"><span data-stu-id="54475-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1070">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1070">Example</span></span>

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

<span data-ttu-id="54475-1071">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="54475-1072">Sink Tabella di Azure nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="54475-1073">Se si copiano dati tooAzure archiviazione tabelle, impostare hello **tipo di sink** di hello attività di copia troppo**AzureTableSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-1074">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1074">Property</span></span> | <span data-ttu-id="54475-1075">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1075">Description</span></span> | <span data-ttu-id="54475-1076">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1076">Allowed values</span></span> | <span data-ttu-id="54475-1077">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="54475-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="54475-1079">Partizione chiave valore predefinito che può essere usato dal sink hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="54475-1080">Valore stringa.</span><span class="sxs-lookup"><span data-stu-id="54475-1080">A string value.</span></span> |<span data-ttu-id="54475-1081">No</span><span class="sxs-lookup"><span data-stu-id="54475-1081">No</span></span> |
| <span data-ttu-id="54475-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="54475-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="54475-1083">Nome della colonna hello i cui valori vengono utilizzati come chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="54475-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="54475-1084">Se non specificato, AzureTableDefaultPartitionKeyValue viene utilizzato come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="54475-1085">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="54475-1085">A column name.</span></span> |<span data-ttu-id="54475-1086">No</span><span class="sxs-lookup"><span data-stu-id="54475-1086">No</span></span> |
| <span data-ttu-id="54475-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="54475-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="54475-1088">Nome della colonna hello i cui valori di colonna vengono utilizzati come chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="54475-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="54475-1089">Se non specificato, usare un GUID per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="54475-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="54475-1090">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="54475-1090">A column name.</span></span> |<span data-ttu-id="54475-1091">No</span><span class="sxs-lookup"><span data-stu-id="54475-1091">No</span></span> |
| <span data-ttu-id="54475-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="54475-1092">azureTableInsertType</span></span> |<span data-ttu-id="54475-1093">Hello modalità tooinsert i dati in tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="54475-1094">Questa proprietà controlla se le righe esistenti nella tabella di output di hello con le chiavi di riga e di partizione corrispondenti hanno valori di sostituzione o unione.</span><span class="sxs-lookup"><span data-stu-id="54475-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="54475-1095">toolearn sul funzionano di queste impostazioni (merge e la sostituzione), vedere [Insert o l'entità di tipo Merge](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Insert o sostituire entità](https://msdn.microsoft.com/library/azure/hh452242.aspx) argomenti.</span><span class="sxs-lookup"><span data-stu-id="54475-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="54475-1096">Questa impostazione si applica a livello di riga hello, non a livello tabella hello, e nessuna delle due opzioni consente di eliminare le righe nella tabella di output di hello che non esistono nell'input hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="54475-1097">merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="54475-1097">merge (default)</span></span><br/><span data-ttu-id="54475-1098">replace</span><span class="sxs-lookup"><span data-stu-id="54475-1098">replace</span></span> |<span data-ttu-id="54475-1099">No</span><span class="sxs-lookup"><span data-stu-id="54475-1099">No</span></span> |
| <span data-ttu-id="54475-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-1100">writeBatchSize</span></span> |<span data-ttu-id="54475-1101">Inserisce dati nella tabella di Azure hello quando hello di viene raggiunto writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="54475-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="54475-1102">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="54475-1102">Integer (number of rows)</span></span> |<span data-ttu-id="54475-1103">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="54475-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="54475-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-1104">writeBatchTimeout</span></span> |<span data-ttu-id="54475-1105">Inserisce i dati in tabelle di Azure hello quando viene raggiunto writeBatchSize hello o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="54475-1106">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-1106">timespan</span></span><br/><br/><span data-ttu-id="54475-1107">Ad esempio: "00:20:00" (20 minuti)</span><span class="sxs-lookup"><span data-stu-id="54475-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="54475-1108">No (valore di timeout predefinito del client predefinito toostorage 90 secondi)</span><span class="sxs-lookup"><span data-stu-id="54475-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1109">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1109">Example</span></span>

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
<span data-ttu-id="54475-1110">Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="54475-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="54475-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1112">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1112">Linked service</span></span>
<span data-ttu-id="54475-1113">toodefine un Amazon Redshift collegato del servizio, hello set **tipo** di hello servizio collegato troppo**AmazonRedshift**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1114">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1114">Property</span></span> | <span data-ttu-id="54475-1115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1115">Description</span></span> | <span data-ttu-id="54475-1116">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1117">server</span><span class="sxs-lookup"><span data-stu-id="54475-1117">server</span></span> |<span data-ttu-id="54475-1118">IP il nome host o indirizzo del server di Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="54475-1119">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1119">Yes</span></span> |
| <span data-ttu-id="54475-1120">port</span><span class="sxs-lookup"><span data-stu-id="54475-1120">port</span></span> |<span data-ttu-id="54475-1121">numero di Hello di porta TCP hello hello server Amazon Redshift utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="54475-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="54475-1122">No, valore predefinito: 5439</span><span class="sxs-lookup"><span data-stu-id="54475-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="54475-1123">database</span><span class="sxs-lookup"><span data-stu-id="54475-1123">database</span></span> |<span data-ttu-id="54475-1124">Nome del database Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="54475-1125">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1125">Yes</span></span> |
| <span data-ttu-id="54475-1126">username</span><span class="sxs-lookup"><span data-stu-id="54475-1126">username</span></span> |<span data-ttu-id="54475-1127">Nome dell'utente che dispone di accesso toohello database.</span><span class="sxs-lookup"><span data-stu-id="54475-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="54475-1128">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1128">Yes</span></span> |
| <span data-ttu-id="54475-1129">password</span><span class="sxs-lookup"><span data-stu-id="54475-1129">password</span></span> |<span data-ttu-id="54475-1130">Password dell'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1130">Password for hello user account.</span></span> |<span data-ttu-id="54475-1131">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1132">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1132">Example</span></span>

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

<span data-ttu-id="54475-1133">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1134">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1134">Dataset</span></span>
<span data-ttu-id="54475-1135">toodefine un set di dati di Amazon Redshift set hello **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1136">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1136">Property</span></span> | <span data-ttu-id="54475-1137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1137">Description</span></span> | <span data-ttu-id="54475-1138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1139">tableName</span></span> |<span data-ttu-id="54475-1140">Nome della tabella hello hello Amazon Redshift in database in cui il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="54475-1141">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="54475-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-1142">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1142">Example</span></span>

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
<span data-ttu-id="54475-1143">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1144">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="54475-1145">Se si copiano dati da Amazon Redshift, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1146">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1146">Property</span></span> | <span data-ttu-id="54475-1147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1147">Description</span></span> | <span data-ttu-id="54475-1148">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1148">Allowed values</span></span> | <span data-ttu-id="54475-1149">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1150">query</span><span class="sxs-lookup"><span data-stu-id="54475-1150">query</span></span> |<span data-ttu-id="54475-1151">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1152">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1152">SQL query string.</span></span> <span data-ttu-id="54475-1153">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-1154">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1155">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1155">Example</span></span>

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
<span data-ttu-id="54475-1156">Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="54475-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="54475-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1158">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1158">Linked service</span></span>
<span data-ttu-id="54475-1159">il set hello servizio collegato di toodefine un IBM DB2 **tipo** di hello servizio collegato troppo**OnPremisesDB2**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1160">Property</span></span> | <span data-ttu-id="54475-1161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1161">Description</span></span> | <span data-ttu-id="54475-1162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1163">server</span><span class="sxs-lookup"><span data-stu-id="54475-1163">server</span></span> |<span data-ttu-id="54475-1164">Nome del server DB2 hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="54475-1165">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1165">Yes</span></span> |
| <span data-ttu-id="54475-1166">database</span><span class="sxs-lookup"><span data-stu-id="54475-1166">database</span></span> |<span data-ttu-id="54475-1167">Nome del database DB2 hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="54475-1168">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1168">Yes</span></span> |
| <span data-ttu-id="54475-1169">schema</span><span class="sxs-lookup"><span data-stu-id="54475-1169">schema</span></span> |<span data-ttu-id="54475-1170">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="54475-1171">nome dello schema Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="54475-1172">No</span><span class="sxs-lookup"><span data-stu-id="54475-1172">No</span></span> |
| <span data-ttu-id="54475-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1173">authenticationType</span></span> |<span data-ttu-id="54475-1174">Tipo di autenticazione usato tooconnect toohello DB2 database.</span><span class="sxs-lookup"><span data-stu-id="54475-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="54475-1175">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54475-1176">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1176">Yes</span></span> |
| <span data-ttu-id="54475-1177">username</span><span class="sxs-lookup"><span data-stu-id="54475-1177">username</span></span> |<span data-ttu-id="54475-1178">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="54475-1179">No</span><span class="sxs-lookup"><span data-stu-id="54475-1179">No</span></span> |
| <span data-ttu-id="54475-1180">password</span><span class="sxs-lookup"><span data-stu-id="54475-1180">password</span></span> |<span data-ttu-id="54475-1181">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-1182">No</span><span class="sxs-lookup"><span data-stu-id="54475-1182">No</span></span> |
| <span data-ttu-id="54475-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1183">gatewayName</span></span> |<span data-ttu-id="54475-1184">Nome del gateway hello hello servizio Data Factory deve usare database di DB2 tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="54475-1185">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1186">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1186">Example</span></span>
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
<span data-ttu-id="54475-1187">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1188">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1188">Dataset</span></span>
<span data-ttu-id="54475-1189">set di dati toodefine un DB2, set hello **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="54475-1190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1190">Property</span></span> | <span data-ttu-id="54475-1191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1191">Description</span></span> | <span data-ttu-id="54475-1192">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1193">tableName</span></span> |<span data-ttu-id="54475-1194">Nome della tabella hello nell'istanza di Database DB2 hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="54475-1195">tableName Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="54475-1196">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="54475-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="54475-1197">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1197">Example</span></span>
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

<span data-ttu-id="54475-1198">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1199">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1200">Se si copiano dati da IBM DB2, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1201">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1201">Property</span></span> | <span data-ttu-id="54475-1202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1202">Description</span></span> | <span data-ttu-id="54475-1203">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1203">Allowed values</span></span> | <span data-ttu-id="54475-1204">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1205">query</span><span class="sxs-lookup"><span data-stu-id="54475-1205">query</span></span> |<span data-ttu-id="54475-1206">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1207">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1207">SQL query string.</span></span> <span data-ttu-id="54475-1208">Ad esempio: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="54475-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="54475-1209">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1210">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1210">Example</span></span>
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
<span data-ttu-id="54475-1211">Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="54475-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="54475-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1213">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1213">Linked service</span></span>
<span data-ttu-id="54475-1214">il servizio hello set toodefine MySQL collegato **tipo** di hello servizio collegato troppo**OnPremisesMySql**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1215">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1215">Property</span></span> | <span data-ttu-id="54475-1216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1216">Description</span></span> | <span data-ttu-id="54475-1217">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1218">server</span><span class="sxs-lookup"><span data-stu-id="54475-1218">server</span></span> |<span data-ttu-id="54475-1219">Nome del server MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="54475-1220">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1220">Yes</span></span> |
| <span data-ttu-id="54475-1221">database</span><span class="sxs-lookup"><span data-stu-id="54475-1221">database</span></span> |<span data-ttu-id="54475-1222">Nome del database MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="54475-1223">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1223">Yes</span></span> |
| <span data-ttu-id="54475-1224">schema</span><span class="sxs-lookup"><span data-stu-id="54475-1224">schema</span></span> |<span data-ttu-id="54475-1225">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="54475-1226">No</span><span class="sxs-lookup"><span data-stu-id="54475-1226">No</span></span> |
| <span data-ttu-id="54475-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1227">authenticationType</span></span> |<span data-ttu-id="54475-1228">Tipo di autenticazione usato toohello tooconnect di database MySQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="54475-1229">I valori possibili sono:`Basic`.</span><span class="sxs-lookup"><span data-stu-id="54475-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="54475-1230">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1230">Yes</span></span> |
| <span data-ttu-id="54475-1231">username</span><span class="sxs-lookup"><span data-stu-id="54475-1231">username</span></span> |<span data-ttu-id="54475-1232">Specificare i database di MySQL toohello tooconnect nome utente.</span><span class="sxs-lookup"><span data-stu-id="54475-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="54475-1233">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1233">Yes</span></span> |
| <span data-ttu-id="54475-1234">password</span><span class="sxs-lookup"><span data-stu-id="54475-1234">password</span></span> |<span data-ttu-id="54475-1235">Specificare la password per l'account utente di hello specificato.</span><span class="sxs-lookup"><span data-stu-id="54475-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="54475-1236">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1236">Yes</span></span> |
| <span data-ttu-id="54475-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1237">gatewayName</span></span> |<span data-ttu-id="54475-1238">Nome del gateway hello hello servizio Data Factory deve utilizzare database MySQL di tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="54475-1239">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1240">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1240">Example</span></span>

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

<span data-ttu-id="54475-1241">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1242">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1242">Dataset</span></span>
<span data-ttu-id="54475-1243">toodefine un set di dati di MySQL, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1244">Property</span></span> | <span data-ttu-id="54475-1245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1245">Description</span></span> | <span data-ttu-id="54475-1246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1247">tableName</span></span> |<span data-ttu-id="54475-1248">Nome della tabella hello nell'istanza di MySQL Database che fa riferimento il servizio collegato a hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="54475-1249">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="54475-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1250">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1250">Example</span></span>

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
<span data-ttu-id="54475-1251">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1252">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1253">Se si copiano dati da un database MySQL, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1254">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1254">Property</span></span> | <span data-ttu-id="54475-1255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1255">Description</span></span> | <span data-ttu-id="54475-1256">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1256">Allowed values</span></span> | <span data-ttu-id="54475-1257">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1258">query</span><span class="sxs-lookup"><span data-stu-id="54475-1258">query</span></span> |<span data-ttu-id="54475-1259">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1260">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1260">SQL query string.</span></span> <span data-ttu-id="54475-1261">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-1262">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-1263">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1263">Example</span></span>
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

<span data-ttu-id="54475-1264">Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="54475-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="54475-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-1266">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1266">Linked service</span></span>
<span data-ttu-id="54475-1267">il servizio hello set toodefine Oracle collegato **tipo** di hello servizio collegato troppo**OnPremisesOracle**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1268">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1268">Property</span></span> | <span data-ttu-id="54475-1269">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1269">Description</span></span> | <span data-ttu-id="54475-1270">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="54475-1271">driverType</span></span> | <span data-ttu-id="54475-1272">Specificare i dati del driver toouse toocopy da / tooOracle Database.</span><span class="sxs-lookup"><span data-stu-id="54475-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="54475-1273">I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="54475-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="54475-1274">Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="54475-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="54475-1275">No</span><span class="sxs-lookup"><span data-stu-id="54475-1275">No</span></span> |
| <span data-ttu-id="54475-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-1276">connectionString</span></span> | <span data-ttu-id="54475-1277">Specificare l'istanza di Oracle Database toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="54475-1278">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1278">Yes</span></span> |
| <span data-ttu-id="54475-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1279">gatewayName</span></span> | <span data-ttu-id="54475-1280">Nome del gateway hello che viene utilizzato tooconnect toohello server Oracle locale</span><span class="sxs-lookup"><span data-stu-id="54475-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="54475-1281">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1282">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1282">Example</span></span>
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

<span data-ttu-id="54475-1283">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1284">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1284">Dataset</span></span>
<span data-ttu-id="54475-1285">toodefine un set di dati Oracle, hello set **tipo** del set di dati hello troppo**OracleTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1286">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1286">Property</span></span> | <span data-ttu-id="54475-1287">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1287">Description</span></span> | <span data-ttu-id="54475-1288">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1289">tableName</span></span> |<span data-ttu-id="54475-1290">Nome della tabella hello nel Database Oracle per il servizio collegato di hello hello fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="54475-1291">No, se **oracleReaderQuery** di **OracleSource** è specificato</span><span class="sxs-lookup"><span data-stu-id="54475-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1292">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1292">Example</span></span>

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
<span data-ttu-id="54475-1293">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="54475-1294">Origine Oracle nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="54475-1295">Se si copiano dati da un database Oracle, impostare hello **tipo di origine** di hello attività di copia troppo**OracleSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1296">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1296">Property</span></span> | <span data-ttu-id="54475-1297">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1297">Description</span></span> | <span data-ttu-id="54475-1298">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1298">Allowed values</span></span> | <span data-ttu-id="54475-1299">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="54475-1300">oracleReaderQuery</span></span> |<span data-ttu-id="54475-1301">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1302">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1302">SQL query string.</span></span> <span data-ttu-id="54475-1303">Ad esempio: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="54475-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="54475-1304">Se non specificato, hello istruzione SQL eseguita:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="54475-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="54475-1305">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1306">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1306">Example</span></span>

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

<span data-ttu-id="54475-1307">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="54475-1308">Sink Oracle nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="54475-1309">Se si copia database Oracle tooam di dati, impostare hello **tipo di sink** di hello attività di copia troppo**OracleSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-1310">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1310">Property</span></span> | <span data-ttu-id="54475-1311">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1311">Description</span></span> | <span data-ttu-id="54475-1312">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1312">Allowed values</span></span> | <span data-ttu-id="54475-1313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-1314">writeBatchTimeout</span></span> |<span data-ttu-id="54475-1315">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="54475-1316">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-1316">timespan</span></span><br/><br/> <span data-ttu-id="54475-1317">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="54475-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="54475-1318">No</span><span class="sxs-lookup"><span data-stu-id="54475-1318">No</span></span> |
| <span data-ttu-id="54475-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-1319">writeBatchSize</span></span> |<span data-ttu-id="54475-1320">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="54475-1321">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="54475-1321">Integer (number of rows)</span></span> |<span data-ttu-id="54475-1322">No (valore predefinito: 100)</span><span class="sxs-lookup"><span data-stu-id="54475-1322">No (default: 100)</span></span> |
| <span data-ttu-id="54475-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="54475-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="54475-1324">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="54475-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="54475-1325">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="54475-1325">A query statement.</span></span> |<span data-ttu-id="54475-1326">No</span><span class="sxs-lookup"><span data-stu-id="54475-1326">No</span></span> |
| <span data-ttu-id="54475-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="54475-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="54475-1328">Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="54475-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="54475-1329">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="54475-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="54475-1330">No</span><span class="sxs-lookup"><span data-stu-id="54475-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1331">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1331">Example</span></span>
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
<span data-ttu-id="54475-1332">Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="54475-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="54475-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1334">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1334">Linked service</span></span>
<span data-ttu-id="54475-1335">toodefine un PostgreSQL collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesPostgreSql**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1336">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1336">Property</span></span> | <span data-ttu-id="54475-1337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1337">Description</span></span> | <span data-ttu-id="54475-1338">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1339">server</span><span class="sxs-lookup"><span data-stu-id="54475-1339">server</span></span> |<span data-ttu-id="54475-1340">Nome del server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="54475-1341">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1341">Yes</span></span> |
| <span data-ttu-id="54475-1342">database</span><span class="sxs-lookup"><span data-stu-id="54475-1342">database</span></span> |<span data-ttu-id="54475-1343">Nome del database PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="54475-1344">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1344">Yes</span></span> |
| <span data-ttu-id="54475-1345">schema</span><span class="sxs-lookup"><span data-stu-id="54475-1345">schema</span></span> |<span data-ttu-id="54475-1346">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="54475-1347">nome dello schema Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="54475-1348">No</span><span class="sxs-lookup"><span data-stu-id="54475-1348">No</span></span> |
| <span data-ttu-id="54475-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1349">authenticationType</span></span> |<span data-ttu-id="54475-1350">Tipo di autenticazione usato tooconnect toohello PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="54475-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="54475-1351">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54475-1352">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1352">Yes</span></span> |
| <span data-ttu-id="54475-1353">username</span><span class="sxs-lookup"><span data-stu-id="54475-1353">username</span></span> |<span data-ttu-id="54475-1354">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="54475-1355">No</span><span class="sxs-lookup"><span data-stu-id="54475-1355">No</span></span> |
| <span data-ttu-id="54475-1356">password</span><span class="sxs-lookup"><span data-stu-id="54475-1356">password</span></span> |<span data-ttu-id="54475-1357">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-1358">No</span><span class="sxs-lookup"><span data-stu-id="54475-1358">No</span></span> |
| <span data-ttu-id="54475-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1359">gatewayName</span></span> |<span data-ttu-id="54475-1360">Nome del gateway hello hello servizio Data Factory deve utilizzare database PostgreSQL locale di tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="54475-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="54475-1361">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1362">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1362">Example</span></span>

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
<span data-ttu-id="54475-1363">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1364">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1364">Dataset</span></span>
<span data-ttu-id="54475-1365">toodefine un set di dati, PostgreSQL hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1366">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1366">Property</span></span> | <span data-ttu-id="54475-1367">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1367">Description</span></span> | <span data-ttu-id="54475-1368">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1369">tableName</span></span> |<span data-ttu-id="54475-1370">Nome della tabella hello in hello istanza PostgreSQL Database riferito al servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="54475-1371">tableName Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="54475-1372">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="54475-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1373">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1373">Example</span></span>
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
<span data-ttu-id="54475-1374">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1375">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1376">Se si copiano dati da un database PostgreSQL, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1377">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1377">Property</span></span> | <span data-ttu-id="54475-1378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1378">Description</span></span> | <span data-ttu-id="54475-1379">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1379">Allowed values</span></span> | <span data-ttu-id="54475-1380">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1381">query</span><span class="sxs-lookup"><span data-stu-id="54475-1381">query</span></span> |<span data-ttu-id="54475-1382">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1383">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1383">SQL query string.</span></span> <span data-ttu-id="54475-1384">Ad esempio: "query": "select * from \"Schema\".\"Tabella\"".</span><span class="sxs-lookup"><span data-stu-id="54475-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="54475-1385">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1386">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1386">Example</span></span>

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

<span data-ttu-id="54475-1387">Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="54475-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-1389">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1389">Linked service</span></span>
<span data-ttu-id="54475-1390">il set hello servizio collegato di toodefine un SAP Business Warehouse (BW) **tipo** di hello servizio collegato troppo**SapBw**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="54475-1391">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1391">Property</span></span> | <span data-ttu-id="54475-1392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1392">Description</span></span> | <span data-ttu-id="54475-1393">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1393">Allowed values</span></span> | <span data-ttu-id="54475-1394">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="54475-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="54475-1395">server</span><span class="sxs-lookup"><span data-stu-id="54475-1395">server</span></span> | <span data-ttu-id="54475-1396">Nome del server di hello in SAP BW che hello si trova l'istanza.</span><span class="sxs-lookup"><span data-stu-id="54475-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="54475-1397">string</span><span class="sxs-lookup"><span data-stu-id="54475-1397">string</span></span> | <span data-ttu-id="54475-1398">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1398">Yes</span></span>
<span data-ttu-id="54475-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="54475-1399">systemNumber</span></span> | <span data-ttu-id="54475-1400">Numero di sistema di hello sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="54475-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="54475-1401">Numero decimale a due cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="54475-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="54475-1402">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1402">Yes</span></span>
<span data-ttu-id="54475-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="54475-1403">clientId</span></span> | <span data-ttu-id="54475-1404">ID client di client hello in hello sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="54475-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="54475-1405">Numero decimale a tre cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="54475-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="54475-1406">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1406">Yes</span></span>
<span data-ttu-id="54475-1407">username</span><span class="sxs-lookup"><span data-stu-id="54475-1407">username</span></span> | <span data-ttu-id="54475-1408">Nome dell'utente di hello con server di accesso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="54475-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="54475-1409">string</span><span class="sxs-lookup"><span data-stu-id="54475-1409">string</span></span> | <span data-ttu-id="54475-1410">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1410">Yes</span></span>
<span data-ttu-id="54475-1411">password</span><span class="sxs-lookup"><span data-stu-id="54475-1411">password</span></span> | <span data-ttu-id="54475-1412">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1412">Password for hello user.</span></span> | <span data-ttu-id="54475-1413">string</span><span class="sxs-lookup"><span data-stu-id="54475-1413">string</span></span> | <span data-ttu-id="54475-1414">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1414">Yes</span></span>
<span data-ttu-id="54475-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1415">gatewayName</span></span> | <span data-ttu-id="54475-1416">Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP BW tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="54475-1417">string</span><span class="sxs-lookup"><span data-stu-id="54475-1417">string</span></span> | <span data-ttu-id="54475-1418">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1418">Yes</span></span>
<span data-ttu-id="54475-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-1419">encryptedCredential</span></span> | <span data-ttu-id="54475-1420">stringa di credenziale crittografato Hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="54475-1421">string</span><span class="sxs-lookup"><span data-stu-id="54475-1421">string</span></span> | <span data-ttu-id="54475-1422">No</span><span class="sxs-lookup"><span data-stu-id="54475-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="54475-1423">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1423">Example</span></span>

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

<span data-ttu-id="54475-1424">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1425">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1425">Dataset</span></span>
<span data-ttu-id="54475-1426">toodefine un set di dati SAP BW, hello set **tipo** del set di dati hello troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54475-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="54475-1427">Non esistono proprietà specifiche del tipo supportato per il set di dati di hello SAP BW di tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54475-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="54475-1428">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1428">Example</span></span>

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
<span data-ttu-id="54475-1429">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1430">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1431">Se si copiano dati da SAP Business Warehouse, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1432">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1432">Property</span></span> | <span data-ttu-id="54475-1433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1433">Description</span></span> | <span data-ttu-id="54475-1434">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1434">Allowed values</span></span> | <span data-ttu-id="54475-1435">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1436">query</span><span class="sxs-lookup"><span data-stu-id="54475-1436">query</span></span> | <span data-ttu-id="54475-1437">Specifica i dati di tooread query MDX hello dall'istanza di SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="54475-1438">Query MDX.</span><span class="sxs-lookup"><span data-stu-id="54475-1438">MDX query.</span></span> | <span data-ttu-id="54475-1439">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1440">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1440">Example</span></span>

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

<span data-ttu-id="54475-1441">Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="54475-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54475-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1443">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1443">Linked service</span></span>
<span data-ttu-id="54475-1444">il set hello servizio collegato di toodefine un SAP HANA **tipo** di hello servizio collegato troppo**SapHana**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="54475-1445">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1445">Property</span></span> | <span data-ttu-id="54475-1446">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1446">Description</span></span> | <span data-ttu-id="54475-1447">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1447">Allowed values</span></span> | <span data-ttu-id="54475-1448">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="54475-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="54475-1449">server</span><span class="sxs-lookup"><span data-stu-id="54475-1449">server</span></span> | <span data-ttu-id="54475-1450">Nome del server di hello in SAP HANA quali hello si trova l'istanza.</span><span class="sxs-lookup"><span data-stu-id="54475-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="54475-1451">Se il server usa una porta personalizzata, specificare `server:port`.</span><span class="sxs-lookup"><span data-stu-id="54475-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="54475-1452">string</span><span class="sxs-lookup"><span data-stu-id="54475-1452">string</span></span> | <span data-ttu-id="54475-1453">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1453">Yes</span></span>
<span data-ttu-id="54475-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1454">authenticationType</span></span> | <span data-ttu-id="54475-1455">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54475-1455">Type of authentication.</span></span> | <span data-ttu-id="54475-1456">string.</span><span class="sxs-lookup"><span data-stu-id="54475-1456">string.</span></span> <span data-ttu-id="54475-1457">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="54475-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="54475-1458">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1458">Yes</span></span> 
<span data-ttu-id="54475-1459">username</span><span class="sxs-lookup"><span data-stu-id="54475-1459">username</span></span> | <span data-ttu-id="54475-1460">Nome dell'utente di hello con server di accesso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="54475-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="54475-1461">string</span><span class="sxs-lookup"><span data-stu-id="54475-1461">string</span></span> | <span data-ttu-id="54475-1462">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1462">Yes</span></span>
<span data-ttu-id="54475-1463">password</span><span class="sxs-lookup"><span data-stu-id="54475-1463">password</span></span> | <span data-ttu-id="54475-1464">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1464">Password for hello user.</span></span> | <span data-ttu-id="54475-1465">string</span><span class="sxs-lookup"><span data-stu-id="54475-1465">string</span></span> | <span data-ttu-id="54475-1466">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1466">Yes</span></span>
<span data-ttu-id="54475-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1467">gatewayName</span></span> | <span data-ttu-id="54475-1468">Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP HANA tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="54475-1469">string</span><span class="sxs-lookup"><span data-stu-id="54475-1469">string</span></span> | <span data-ttu-id="54475-1470">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1470">Yes</span></span>
<span data-ttu-id="54475-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-1471">encryptedCredential</span></span> | <span data-ttu-id="54475-1472">stringa di credenziale crittografato Hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="54475-1473">string</span><span class="sxs-lookup"><span data-stu-id="54475-1473">string</span></span> | <span data-ttu-id="54475-1474">No</span><span class="sxs-lookup"><span data-stu-id="54475-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="54475-1475">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1475">Example</span></span>

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
<span data-ttu-id="54475-1476">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="54475-1477">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1477">Dataset</span></span>
<span data-ttu-id="54475-1478">toodefine un set di dati SAP HANA, hello set **tipo** del set di dati hello troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54475-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="54475-1479">Non esistono proprietà specifiche del tipo supportato per i set di dati SAP HANA hello di tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54475-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="54475-1480">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1480">Example</span></span>

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
<span data-ttu-id="54475-1481">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1482">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1483">Se si copiano dati da un archivio dati SAP HANA, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1484">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1484">Property</span></span> | <span data-ttu-id="54475-1485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1485">Description</span></span> | <span data-ttu-id="54475-1486">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1486">Allowed values</span></span> | <span data-ttu-id="54475-1487">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1488">query</span><span class="sxs-lookup"><span data-stu-id="54475-1488">query</span></span> | <span data-ttu-id="54475-1489">Specifica i dati di tooread query SQL hello dall'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="54475-1490">Query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1490">SQL query.</span></span> | <span data-ttu-id="54475-1491">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-1492">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1492">Example</span></span>


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

<span data-ttu-id="54475-1493">Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="54475-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="54475-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1495">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1495">Linked service</span></span>
<span data-ttu-id="54475-1496">Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="54475-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="54475-1497">Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="54475-1498">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="54475-1499">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1499">Property</span></span> | <span data-ttu-id="54475-1500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1500">Description</span></span> | <span data-ttu-id="54475-1501">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1502">type</span><span class="sxs-lookup"><span data-stu-id="54475-1502">type</span></span> |<span data-ttu-id="54475-1503">proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="54475-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="54475-1504">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1504">Yes</span></span> |
| <span data-ttu-id="54475-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-1505">connectionString</span></span> |<span data-ttu-id="54475-1506">Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="54475-1507">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1507">Yes</span></span> |
| <span data-ttu-id="54475-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1508">gatewayName</span></span> |<span data-ttu-id="54475-1509">Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="54475-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="54475-1510">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1510">Yes</span></span> |
| <span data-ttu-id="54475-1511">username</span><span class="sxs-lookup"><span data-stu-id="54475-1511">username</span></span> |<span data-ttu-id="54475-1512">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="54475-1513">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="54475-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="54475-1514">No</span><span class="sxs-lookup"><span data-stu-id="54475-1514">No</span></span> |
| <span data-ttu-id="54475-1515">password</span><span class="sxs-lookup"><span data-stu-id="54475-1515">password</span></span> |<span data-ttu-id="54475-1516">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-1517">No</span><span class="sxs-lookup"><span data-stu-id="54475-1517">No</span></span> |

<span data-ttu-id="54475-1518">È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):</span><span class="sxs-lookup"><span data-stu-id="54475-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="54475-1519">Esempio: JSON per l'uso dell'autenticazione SQL</span><span class="sxs-lookup"><span data-stu-id="54475-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="54475-1520">Esempio: JSON per l'uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="54475-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="54475-1521">Se vengono specificati nome utente e password, gateway li utilizza hello tooimpersonate database di SQL Server on-premise toohello tooconnect account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="54475-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="54475-1522">In caso contrario, gateway si connetta toohello SQL Server direttamente con il contesto di sicurezza hello del Gateway (il relativo account di avvio).</span><span class="sxs-lookup"><span data-stu-id="54475-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="54475-1523">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1524">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1524">Dataset</span></span>
<span data-ttu-id="54475-1525">toodefine un set di dati di SQL Server, hello set **tipo** del set di dati hello troppo**SqlServerTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1526">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1526">Property</span></span> | <span data-ttu-id="54475-1527">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1527">Description</span></span> | <span data-ttu-id="54475-1528">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1529">tableName</span></span> |<span data-ttu-id="54475-1530">Nome della tabella hello o della vista nell'istanza di Database di SQL Server hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="54475-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="54475-1531">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1532">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1532">Example</span></span>
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

<span data-ttu-id="54475-1533">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="54475-1534">Origine SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="54475-1535">Se si copiano dati da un database di SQL Server, impostare hello **tipo di origine** di hello attività di copia troppo**SqlSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1536">Property</span></span> | <span data-ttu-id="54475-1537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1537">Description</span></span> | <span data-ttu-id="54475-1538">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1538">Allowed values</span></span> | <span data-ttu-id="54475-1539">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="54475-1540">sqlReaderQuery</span></span> |<span data-ttu-id="54475-1541">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1542">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1542">SQL query string.</span></span> <span data-ttu-id="54475-1543">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="54475-1544">Può fare riferimento a più tabelle dal database hello hello di un set di dati dell'input a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="54475-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="54475-1545">Se non specificato, hello istruzione SQL eseguita: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="54475-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="54475-1546">No</span><span class="sxs-lookup"><span data-stu-id="54475-1546">No</span></span> |
| <span data-ttu-id="54475-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="54475-1548">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="54475-1549">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="54475-1550">No</span><span class="sxs-lookup"><span data-stu-id="54475-1550">No</span></span> |
| <span data-ttu-id="54475-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-1551">storedProcedureParameters</span></span> |<span data-ttu-id="54475-1552">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="54475-1553">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="54475-1553">Name/value pairs.</span></span> <span data-ttu-id="54475-1554">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="54475-1555">No</span><span class="sxs-lookup"><span data-stu-id="54475-1555">No</span></span> |

<span data-ttu-id="54475-1556">Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database di SQL Server tooget hello dati.</span><span class="sxs-lookup"><span data-stu-id="54475-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="54475-1557">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="54475-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="54475-1558">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54475-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="54475-1559">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="54475-1560">Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="54475-1561">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="54475-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="54475-1562">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1562">Example</span></span>
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

<span data-ttu-id="54475-1563">In questo esempio, **sqlReaderQuery** specificato per hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="54475-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="54475-1564">Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54475-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="54475-1565">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="54475-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="54475-1566">Hello sqlReaderQuery può fare riferimento a più tabelle all'interno del database hello hello di un set di dati dell'input a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="54475-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="54475-1567">Non è limitato tooonly hello tabella impostata come hello typeProperty tableName del set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="54475-1568">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54475-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="54475-1569">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="54475-1570">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="54475-1571">Sink SQL nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="54475-1572">Se si desidera copiare i database di SQL Server tooa di dati, impostare hello **tipo di sink** di hello attività di copia troppo**SqlSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-1573">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1573">Property</span></span> | <span data-ttu-id="54475-1574">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1574">Description</span></span> | <span data-ttu-id="54475-1575">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1575">Allowed values</span></span> | <span data-ttu-id="54475-1576">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-1577">writeBatchTimeout</span></span> |<span data-ttu-id="54475-1578">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="54475-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="54475-1579">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="54475-1579">timespan</span></span><br/><br/> <span data-ttu-id="54475-1580">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="54475-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="54475-1581">No</span><span class="sxs-lookup"><span data-stu-id="54475-1581">No</span></span> |
| <span data-ttu-id="54475-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="54475-1582">writeBatchSize</span></span> |<span data-ttu-id="54475-1583">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="54475-1584">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="54475-1584">Integer (number of rows)</span></span> |<span data-ttu-id="54475-1585">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="54475-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="54475-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="54475-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="54475-1587">Specificare query per l'attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="54475-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="54475-1588">Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="54475-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="54475-1589">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="54475-1589">A query statement.</span></span> |<span data-ttu-id="54475-1590">No</span><span class="sxs-lookup"><span data-stu-id="54475-1590">No</span></span> |
| <span data-ttu-id="54475-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="54475-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="54475-1592">Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="54475-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="54475-1593">Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="54475-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="54475-1594">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="54475-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="54475-1595">No</span><span class="sxs-lookup"><span data-stu-id="54475-1595">No</span></span> |
| <span data-ttu-id="54475-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="54475-1597">Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="54475-1598">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="54475-1599">No</span><span class="sxs-lookup"><span data-stu-id="54475-1599">No</span></span> |
| <span data-ttu-id="54475-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-1600">storedProcedureParameters</span></span> |<span data-ttu-id="54475-1601">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="54475-1602">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="54475-1602">Name/value pairs.</span></span> <span data-ttu-id="54475-1603">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="54475-1604">No</span><span class="sxs-lookup"><span data-stu-id="54475-1604">No</span></span> |
| <span data-ttu-id="54475-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="54475-1605">sqlWriterTableType</span></span> |<span data-ttu-id="54475-1606">Specificare toobe nome tipo di tabella utilizzati in hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="54475-1607">Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati.</span><span class="sxs-lookup"><span data-stu-id="54475-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="54475-1608">Codice della stored procedure può unire dati hello copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="54475-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="54475-1609">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="54475-1609">A table type name.</span></span> |<span data-ttu-id="54475-1610">No</span><span class="sxs-lookup"><span data-stu-id="54475-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1611">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1611">Example</span></span>
<span data-ttu-id="54475-1612">pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora.</span><span class="sxs-lookup"><span data-stu-id="54475-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="54475-1613">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="54475-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="54475-1614">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="54475-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="54475-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1616">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1616">Linked service</span></span>
<span data-ttu-id="54475-1617">toodefine un Sybase collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesSybase**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1618">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1618">Property</span></span> | <span data-ttu-id="54475-1619">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1619">Description</span></span> | <span data-ttu-id="54475-1620">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1621">server</span><span class="sxs-lookup"><span data-stu-id="54475-1621">server</span></span> |<span data-ttu-id="54475-1622">Nome del server di Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="54475-1623">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1623">Yes</span></span> |
| <span data-ttu-id="54475-1624">database</span><span class="sxs-lookup"><span data-stu-id="54475-1624">database</span></span> |<span data-ttu-id="54475-1625">Nome del database di Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="54475-1626">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1626">Yes</span></span> |
| <span data-ttu-id="54475-1627">schema</span><span class="sxs-lookup"><span data-stu-id="54475-1627">schema</span></span> |<span data-ttu-id="54475-1628">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="54475-1629">No</span><span class="sxs-lookup"><span data-stu-id="54475-1629">No</span></span> |
| <span data-ttu-id="54475-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1630">authenticationType</span></span> |<span data-ttu-id="54475-1631">Tipo di autenticazione usato tooconnect toohello database di Sybase.</span><span class="sxs-lookup"><span data-stu-id="54475-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="54475-1632">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54475-1633">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1633">Yes</span></span> |
| <span data-ttu-id="54475-1634">username</span><span class="sxs-lookup"><span data-stu-id="54475-1634">username</span></span> |<span data-ttu-id="54475-1635">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="54475-1636">No</span><span class="sxs-lookup"><span data-stu-id="54475-1636">No</span></span> |
| <span data-ttu-id="54475-1637">password</span><span class="sxs-lookup"><span data-stu-id="54475-1637">password</span></span> |<span data-ttu-id="54475-1638">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-1639">No</span><span class="sxs-lookup"><span data-stu-id="54475-1639">No</span></span> |
| <span data-ttu-id="54475-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1640">gatewayName</span></span> |<span data-ttu-id="54475-1641">Nome del gateway hello hello servizio Data Factory deve usare database di Sybase tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="54475-1642">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1643">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1643">Example</span></span>
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

<span data-ttu-id="54475-1644">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1645">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1645">Dataset</span></span>
<span data-ttu-id="54475-1646">toodefine un set di dati, Sybase hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1647">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1647">Property</span></span> | <span data-ttu-id="54475-1648">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1648">Description</span></span> | <span data-ttu-id="54475-1649">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1650">tableName</span></span> |<span data-ttu-id="54475-1651">Nome della tabella hello in hello istanza del Database di Sybase riferito al servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="54475-1652">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="54475-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1653">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1653">Example</span></span>

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

<span data-ttu-id="54475-1654">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1655">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1656">Se si copiano dati da un database di Sybase, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1657">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1657">Property</span></span> | <span data-ttu-id="54475-1658">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1658">Description</span></span> | <span data-ttu-id="54475-1659">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1659">Allowed values</span></span> | <span data-ttu-id="54475-1660">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1661">query</span><span class="sxs-lookup"><span data-stu-id="54475-1661">query</span></span> |<span data-ttu-id="54475-1662">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1663">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1663">SQL query string.</span></span> <span data-ttu-id="54475-1664">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-1665">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1666">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1666">Example</span></span>

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

<span data-ttu-id="54475-1667">Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="54475-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="54475-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1669">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1669">Linked service</span></span>
<span data-ttu-id="54475-1670">il servizio hello set toodefine un Teradata collegato **tipo** di hello servizio collegato troppo**OnPremisesTeradata**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1671">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1671">Property</span></span> | <span data-ttu-id="54475-1672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1672">Description</span></span> | <span data-ttu-id="54475-1673">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1674">server</span><span class="sxs-lookup"><span data-stu-id="54475-1674">server</span></span> |<span data-ttu-id="54475-1675">Nome del server Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="54475-1676">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1676">Yes</span></span> |
| <span data-ttu-id="54475-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1677">authenticationType</span></span> |<span data-ttu-id="54475-1678">Tipo di autenticazione usato tooconnect toohello Teradata database.</span><span class="sxs-lookup"><span data-stu-id="54475-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="54475-1679">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54475-1680">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1680">Yes</span></span> |
| <span data-ttu-id="54475-1681">username</span><span class="sxs-lookup"><span data-stu-id="54475-1681">username</span></span> |<span data-ttu-id="54475-1682">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="54475-1683">No</span><span class="sxs-lookup"><span data-stu-id="54475-1683">No</span></span> |
| <span data-ttu-id="54475-1684">password</span><span class="sxs-lookup"><span data-stu-id="54475-1684">password</span></span> |<span data-ttu-id="54475-1685">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-1686">No</span><span class="sxs-lookup"><span data-stu-id="54475-1686">No</span></span> |
| <span data-ttu-id="54475-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1687">gatewayName</span></span> |<span data-ttu-id="54475-1688">Nome del gateway hello hello servizio Data Factory deve usare database di Teradata tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="54475-1689">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1690">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1690">Example</span></span>
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

<span data-ttu-id="54475-1691">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1692">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1692">Dataset</span></span>
<span data-ttu-id="54475-1693">toodefine un set di dati Teradata Blob hello set **tipo** del set di dati hello troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54475-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="54475-1694">Non sono attualmente presenti proprietà del tipo non supportato per i set di dati Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="54475-1695">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1695">Example</span></span>
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

<span data-ttu-id="54475-1696">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-1697">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-1698">Se si copiano dati da un database Teradata, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1699">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1699">Property</span></span> | <span data-ttu-id="54475-1700">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1700">Description</span></span> | <span data-ttu-id="54475-1701">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1701">Allowed values</span></span> | <span data-ttu-id="54475-1702">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1703">query</span><span class="sxs-lookup"><span data-stu-id="54475-1703">query</span></span> |<span data-ttu-id="54475-1704">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1705">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1705">SQL query string.</span></span> <span data-ttu-id="54475-1706">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-1707">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1708">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1708">Example</span></span>

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

<span data-ttu-id="54475-1709">Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="54475-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="54475-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-1711">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1711">Linked service</span></span>
<span data-ttu-id="54475-1712">toodefine un Cassandra collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesCassandra**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1713">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1713">Property</span></span> | <span data-ttu-id="54475-1714">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1714">Description</span></span> | <span data-ttu-id="54475-1715">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1716">host</span><span class="sxs-lookup"><span data-stu-id="54475-1716">host</span></span> |<span data-ttu-id="54475-1717">Uno o più indirizzi IP o nomi host di server Cassandra.</span><span class="sxs-lookup"><span data-stu-id="54475-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="54475-1718">Specificare un elenco delimitato da virgole di indirizzi IP o host nomi tooconnect tooall server contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="54475-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="54475-1719">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1719">Yes</span></span> |
| <span data-ttu-id="54475-1720">port</span><span class="sxs-lookup"><span data-stu-id="54475-1720">port</span></span> |<span data-ttu-id="54475-1721">la porta TCP che hello server Cassandra Hello utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="54475-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="54475-1722">No, valore predefinito: 9042</span><span class="sxs-lookup"><span data-stu-id="54475-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="54475-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1723">authenticationType</span></span> |<span data-ttu-id="54475-1724">Di base o anonima</span><span class="sxs-lookup"><span data-stu-id="54475-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="54475-1725">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1725">Yes</span></span> |
| <span data-ttu-id="54475-1726">username</span><span class="sxs-lookup"><span data-stu-id="54475-1726">username</span></span> |<span data-ttu-id="54475-1727">Specificare nome utente per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="54475-1728">Sì, se authenticationType impostata tooBasic.</span><span class="sxs-lookup"><span data-stu-id="54475-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="54475-1729">password</span><span class="sxs-lookup"><span data-stu-id="54475-1729">password</span></span> |<span data-ttu-id="54475-1730">Specificare la password per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="54475-1731">Sì, se authenticationType impostata tooBasic.</span><span class="sxs-lookup"><span data-stu-id="54475-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="54475-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1732">gatewayName</span></span> |<span data-ttu-id="54475-1733">nome Hello del gateway hello tooconnect utilizzati toohello Cassandra database locale.</span><span class="sxs-lookup"><span data-stu-id="54475-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="54475-1734">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1734">Yes</span></span> |
| <span data-ttu-id="54475-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-1735">encryptedCredential</span></span> |<span data-ttu-id="54475-1736">Credenziali crittografate dal gateway hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="54475-1737">No</span><span class="sxs-lookup"><span data-stu-id="54475-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1738">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1738">Example</span></span>

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

<span data-ttu-id="54475-1739">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-1740">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1740">Dataset</span></span>
<span data-ttu-id="54475-1741">toodefine un set di dati Cassandra hello set **tipo** del set di dati hello troppo**CassandraTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1742">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1742">Property</span></span> | <span data-ttu-id="54475-1743">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1743">Description</span></span> | <span data-ttu-id="54475-1744">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="54475-1745">keyspace</span></span> |<span data-ttu-id="54475-1746">Nome di schema nel database Cassandra o di spazio delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="54475-1747">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="54475-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="54475-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-1748">tableName</span></span> |<span data-ttu-id="54475-1749">Nome della tabella hello Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="54475-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="54475-1750">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="54475-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1751">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1751">Example</span></span>

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

<span data-ttu-id="54475-1752">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="54475-1753">Origine Cassandra nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="54475-1754">Se si copiano dati da Cassandra, impostare hello **tipo di origine** di hello attività di copia troppo**CassandraSource**e specificare le seguenti proprietà in hello **origine** sezione :</span><span class="sxs-lookup"><span data-stu-id="54475-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1755">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1755">Property</span></span> | <span data-ttu-id="54475-1756">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1756">Description</span></span> | <span data-ttu-id="54475-1757">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1757">Allowed values</span></span> | <span data-ttu-id="54475-1758">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1759">query</span><span class="sxs-lookup"><span data-stu-id="54475-1759">query</span></span> |<span data-ttu-id="54475-1760">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1761">Query SQL-92 o query CQL.</span><span class="sxs-lookup"><span data-stu-id="54475-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="54475-1762">Vedere il [riferimento a CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="54475-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="54475-1763">Quando si utilizza una query SQL, specificare **spazio delle chiavi name.table nome** toorepresent hello tabella tooquery.</span><span class="sxs-lookup"><span data-stu-id="54475-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="54475-1764">No (se tableName e keyspace sul set di dati sono definiti).</span><span class="sxs-lookup"><span data-stu-id="54475-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="54475-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="54475-1765">consistencyLevel</span></span> |<span data-ttu-id="54475-1766">livello di coerenza Hello specifica il numero di repliche deve rispondere tooa richiesta di lettura prima della restituzione dell'applicazione client toohello di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="54475-1767">Controlli Cassandra hello specificato numero di repliche per hello toosatisfy dati richiesta di lettura.</span><span class="sxs-lookup"><span data-stu-id="54475-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="54475-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="54475-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="54475-1769">Per informazioni dettagliate, vedere [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configurazione della coerenza dei dati).</span><span class="sxs-lookup"><span data-stu-id="54475-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="54475-1770">No.</span><span class="sxs-lookup"><span data-stu-id="54475-1770">No.</span></span> <span data-ttu-id="54475-1771">Il valore predefinito è ONE.</span><span class="sxs-lookup"><span data-stu-id="54475-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1772">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="54475-1773">Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="54475-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="54475-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-1775">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1775">Linked service</span></span>
<span data-ttu-id="54475-1776">toodefine un MongoDB collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesMongoDB**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1777">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1777">Property</span></span> | <span data-ttu-id="54475-1778">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1778">Description</span></span> | <span data-ttu-id="54475-1779">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1780">server</span><span class="sxs-lookup"><span data-stu-id="54475-1780">server</span></span> |<span data-ttu-id="54475-1781">IP il nome host o indirizzo del server di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="54475-1782">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1782">Yes</span></span> |
| <span data-ttu-id="54475-1783">port</span><span class="sxs-lookup"><span data-stu-id="54475-1783">port</span></span> |<span data-ttu-id="54475-1784">La porta TCP che hello MongoDB server utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="54475-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="54475-1785">Facoltativo, valore predefinito: 27017</span><span class="sxs-lookup"><span data-stu-id="54475-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="54475-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-1786">authenticationType</span></span> |<span data-ttu-id="54475-1787">Di base o anonima.</span><span class="sxs-lookup"><span data-stu-id="54475-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="54475-1788">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1788">Yes</span></span> |
| <span data-ttu-id="54475-1789">username</span><span class="sxs-lookup"><span data-stu-id="54475-1789">username</span></span> |<span data-ttu-id="54475-1790">Utente account tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="54475-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="54475-1791">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="54475-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="54475-1792">password</span><span class="sxs-lookup"><span data-stu-id="54475-1792">password</span></span> |<span data-ttu-id="54475-1793">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1793">Password for hello user.</span></span> |<span data-ttu-id="54475-1794">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="54475-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="54475-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="54475-1795">authSource</span></span> |<span data-ttu-id="54475-1796">Nome del database MongoDB hello che si desidera toouse toocheck le credenziali per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54475-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="54475-1797">Facoltativo (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="54475-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="54475-1798">impostazione predefinita: Usa l'account amministratore hello e database hello specificato utilizzando la proprietà databaseName.</span><span class="sxs-lookup"><span data-stu-id="54475-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="54475-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="54475-1799">databaseName</span></span> |<span data-ttu-id="54475-1800">Nome del database MongoDB hello che si desidera tooaccess.</span><span class="sxs-lookup"><span data-stu-id="54475-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="54475-1801">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1801">Yes</span></span> |
| <span data-ttu-id="54475-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1802">gatewayName</span></span> |<span data-ttu-id="54475-1803">Nome del gateway hello che accede a hello archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="54475-1804">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1804">Yes</span></span> |
| <span data-ttu-id="54475-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-1805">encryptedCredential</span></span> |<span data-ttu-id="54475-1806">Credenziali crittografate in base al gateway.</span><span class="sxs-lookup"><span data-stu-id="54475-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="54475-1807">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="54475-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1808">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="54475-1809">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1810">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1810">Dataset</span></span>
<span data-ttu-id="54475-1811">toodefine un set di dati, MongoDB hello set **tipo** del set di dati hello troppo**MongoDbCollection**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1812">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1812">Property</span></span> | <span data-ttu-id="54475-1813">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1813">Description</span></span> | <span data-ttu-id="54475-1814">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="54475-1815">collectionName</span></span> |<span data-ttu-id="54475-1816">Nome dell'insieme di hello nel database di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="54475-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="54475-1817">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1818">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1818">Example</span></span>

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

<span data-ttu-id="54475-1819">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="54475-1820">Origine MongoDB nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="54475-1821">Se si copiano dati da MongoDB, impostare hello **tipo di origine** di hello attività di copia troppo**MongoDbSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1822">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1822">Property</span></span> | <span data-ttu-id="54475-1823">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1823">Description</span></span> | <span data-ttu-id="54475-1824">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1824">Allowed values</span></span> | <span data-ttu-id="54475-1825">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1826">query</span><span class="sxs-lookup"><span data-stu-id="54475-1826">query</span></span> |<span data-ttu-id="54475-1827">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-1828">Stringa di query SQL-92.</span><span class="sxs-lookup"><span data-stu-id="54475-1828">SQL-92 query string.</span></span> <span data-ttu-id="54475-1829">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-1830">No, se **collectionName** di **set di dati** è specificato</span><span class="sxs-lookup"><span data-stu-id="54475-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1831">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1831">Example</span></span>

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

<span data-ttu-id="54475-1832">Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="54475-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="54475-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-1834">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1834">Linked service</span></span>
<span data-ttu-id="54475-1835">toodefine un S3 Amazon collegato del servizio, hello set **tipo** di hello servizio collegato troppo**AwsAccessKey**e specificare le seguenti proprietà in hello **typeProperties** sezione :</span><span class="sxs-lookup"><span data-stu-id="54475-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-1836">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1836">Property</span></span> | <span data-ttu-id="54475-1837">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1837">Description</span></span> | <span data-ttu-id="54475-1838">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1838">Allowed values</span></span> | <span data-ttu-id="54475-1839">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="54475-1840">accessKeyID</span></span> |<span data-ttu-id="54475-1841">ID della chiave di accesso privata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="54475-1842">string</span><span class="sxs-lookup"><span data-stu-id="54475-1842">string</span></span> |<span data-ttu-id="54475-1843">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1843">Yes</span></span> |
| <span data-ttu-id="54475-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="54475-1844">secretAccessKey</span></span> |<span data-ttu-id="54475-1845">chiave di accesso per i segreti Hello stessa.</span><span class="sxs-lookup"><span data-stu-id="54475-1845">hello secret access key itself.</span></span> |<span data-ttu-id="54475-1846">La stringa segreta crittografata</span><span class="sxs-lookup"><span data-stu-id="54475-1846">Encrypted secret string</span></span> |<span data-ttu-id="54475-1847">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-1848">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1848">Example</span></span>
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

<span data-ttu-id="54475-1849">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1850">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1850">Dataset</span></span>
<span data-ttu-id="54475-1851">set di dati toodefine un S3 Amazon, hello set **tipo** del set di dati hello troppo**AmazonS3**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1852">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1852">Property</span></span> | <span data-ttu-id="54475-1853">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1853">Description</span></span> | <span data-ttu-id="54475-1854">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1854">Allowed values</span></span> | <span data-ttu-id="54475-1855">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="54475-1856">bucketName</span></span> |<span data-ttu-id="54475-1857">nome di bucket Hello S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="54475-1858">String</span><span class="sxs-lookup"><span data-stu-id="54475-1858">String</span></span> |<span data-ttu-id="54475-1859">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1859">Yes</span></span> |
| <span data-ttu-id="54475-1860">key</span><span class="sxs-lookup"><span data-stu-id="54475-1860">key</span></span> |<span data-ttu-id="54475-1861">chiave dell'oggetto Hello S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1861">hello S3 object key.</span></span> |<span data-ttu-id="54475-1862">String</span><span class="sxs-lookup"><span data-stu-id="54475-1862">String</span></span> |<span data-ttu-id="54475-1863">No</span><span class="sxs-lookup"><span data-stu-id="54475-1863">No</span></span> |
| <span data-ttu-id="54475-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="54475-1864">prefix</span></span> |<span data-ttu-id="54475-1865">Prefisso per la chiave dell'oggetto hello S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="54475-1866">Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="54475-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="54475-1867">Si applica solo quando la chiave è vuota.</span><span class="sxs-lookup"><span data-stu-id="54475-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="54475-1868">string</span><span class="sxs-lookup"><span data-stu-id="54475-1868">String</span></span> |<span data-ttu-id="54475-1869">No</span><span class="sxs-lookup"><span data-stu-id="54475-1869">No</span></span> |
| <span data-ttu-id="54475-1870">version</span><span class="sxs-lookup"><span data-stu-id="54475-1870">version</span></span> |<span data-ttu-id="54475-1871">versione di Hello dell'oggetto S3 se è abilitato il controllo delle versioni S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="54475-1872">String</span><span class="sxs-lookup"><span data-stu-id="54475-1872">String</span></span> |<span data-ttu-id="54475-1873">No</span><span class="sxs-lookup"><span data-stu-id="54475-1873">No</span></span> |
| <span data-ttu-id="54475-1874">format</span><span class="sxs-lookup"><span data-stu-id="54475-1874">format</span></span> | <span data-ttu-id="54475-1875">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-1876">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-1877">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-1878">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-1879">No</span><span class="sxs-lookup"><span data-stu-id="54475-1879">No</span></span> | |
| <span data-ttu-id="54475-1880">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-1880">compression</span></span> | <span data-ttu-id="54475-1881">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-1882">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-1883">livelli di Hello supportato sono: **ottimale** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="54475-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-1884">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-1885">No</span><span class="sxs-lookup"><span data-stu-id="54475-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="54475-1886">bucketName + tasto specifica il percorso di hello dell'oggetto hello S3 in bucket è il contenitore radice hello per gli oggetti S3 e la chiave è oggetto di tooS3 hello percorso completo.</span><span class="sxs-lookup"><span data-stu-id="54475-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="54475-1887">Esempio: set di dati di esempio con prefisso</span><span class="sxs-lookup"><span data-stu-id="54475-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="54475-1888">Esempio: set di dati di esempio con versione</span><span class="sxs-lookup"><span data-stu-id="54475-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="54475-1889">Esempio: percorsi dinamici per S3</span><span class="sxs-lookup"><span data-stu-id="54475-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="54475-1890">Nell'esempio hello, utilizziamo valori fissi per le proprietà di chiave e bucketName nel set di dati hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="54475-1891">È possibile avere Data Factory di calcolare la chiave di hello e bucketName dinamicamente in fase di esecuzione tramite variabili di sistema, ad esempio SliceStart.</span><span class="sxs-lookup"><span data-stu-id="54475-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="54475-1892">È possibile eseguire stesso hello per le proprietà prefix hello di un set di dati di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="54475-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="54475-1893">Per un elenco delle funzioni e delle variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="54475-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="54475-1894">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="54475-1895">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="54475-1896">Se si copiano dati da S3 Amazon, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione :</span><span class="sxs-lookup"><span data-stu-id="54475-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="54475-1897">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1897">Property</span></span> | <span data-ttu-id="54475-1898">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1898">Description</span></span> | <span data-ttu-id="54475-1899">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1899">Allowed values</span></span> | <span data-ttu-id="54475-1900">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1901">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-1901">recursive</span></span> |<span data-ttu-id="54475-1902">Specifica se l'elenco toorecursively S3 oggetti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="54475-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="54475-1903">true/false</span></span> |<span data-ttu-id="54475-1904">No</span><span class="sxs-lookup"><span data-stu-id="54475-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-1905">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1905">Example</span></span>


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

<span data-ttu-id="54475-1906">Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="54475-1907">File system</span><span class="sxs-lookup"><span data-stu-id="54475-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-1908">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1908">Linked service</span></span>
<span data-ttu-id="54475-1909">È possibile collegare una locale file system tooan data factory di Azure con hello **Server File locale** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="54475-1910">Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON toohello specifico servizio locale di File Server collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="54475-1911">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1911">Property</span></span> | <span data-ttu-id="54475-1912">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1912">Description</span></span> | <span data-ttu-id="54475-1913">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1914">type</span><span class="sxs-lookup"><span data-stu-id="54475-1914">type</span></span> |<span data-ttu-id="54475-1915">Verificare che la proprietà di tipo hello sia impostata troppo**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="54475-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="54475-1916">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1916">Yes</span></span> |
| <span data-ttu-id="54475-1917">host</span><span class="sxs-lookup"><span data-stu-id="54475-1917">host</span></span> |<span data-ttu-id="54475-1918">Specifica il percorso radice hello della cartella hello che si desidera toocopy.</span><span class="sxs-lookup"><span data-stu-id="54475-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="54475-1919">Utilizzare il carattere di escape hello ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="54475-1920">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="54475-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="54475-1921">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1921">Yes</span></span> |
| <span data-ttu-id="54475-1922">userid</span><span class="sxs-lookup"><span data-stu-id="54475-1922">userid</span></span> |<span data-ttu-id="54475-1923">Specificare ID utente hello con server di accesso toohello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="54475-1924">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="54475-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="54475-1925">password</span><span class="sxs-lookup"><span data-stu-id="54475-1925">password</span></span> |<span data-ttu-id="54475-1926">Specificare la password hello per utente hello (userid).</span><span class="sxs-lookup"><span data-stu-id="54475-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="54475-1927">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="54475-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="54475-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-1928">encryptedCredential</span></span> |<span data-ttu-id="54475-1929">Specificare le credenziali crittografato hello che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="54475-1930">No (se si sceglie toospecify userid e password in testo normale)</span><span class="sxs-lookup"><span data-stu-id="54475-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="54475-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-1931">gatewayName</span></span> |<span data-ttu-id="54475-1932">Specifica il nome di hello del gateway hello che Data Factory deve usare tooconnect toohello ai file server locali.</span><span class="sxs-lookup"><span data-stu-id="54475-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="54475-1933">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="54475-1934">Definizioni del percorso della cartella di esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="54475-1935">Scenario</span><span class="sxs-lookup"><span data-stu-id="54475-1935">Scenario</span></span> | <span data-ttu-id="54475-1936">Host nella definizione del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-1936">Host in linked service definition</span></span> | <span data-ttu-id="54475-1937">folderPath nella definizione del set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1938">Cartella locale nel computer del gateway di gestione dati: </span><span class="sxs-lookup"><span data-stu-id="54475-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="54475-1939">Esempi: D:\\\* o D:\cartella\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="54475-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="54475-1940">D:\\\\ (per Gateway di gestione dati versione 2.0 e successive)</span><span class="sxs-lookup"><span data-stu-id="54475-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="54475-1941">localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati)</span><span class="sxs-lookup"><span data-stu-id="54475-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="54475-1942">.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="54475-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="54475-1943">D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0)</span><span class="sxs-lookup"><span data-stu-id="54475-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="54475-1944">Cartella condivisa remota: </span><span class="sxs-lookup"><span data-stu-id="54475-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="54475-1945">Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="54475-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="54475-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="54475-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="54475-1947">.\\\\ o cartella\\\\sottocartella</span><span class="sxs-lookup"><span data-stu-id="54475-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="54475-1948">Esempio: Uso di nome utente e password in testo normale</span><span class="sxs-lookup"><span data-stu-id="54475-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="54475-1949">Esempio: Uso di encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="54475-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="54475-1950">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-1951">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-1951">Dataset</span></span>
<span data-ttu-id="54475-1952">toodefine un set di dati di File System, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-1953">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1953">Property</span></span> | <span data-ttu-id="54475-1954">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1954">Description</span></span> | <span data-ttu-id="54475-1955">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-1956">folderPath</span></span> |<span data-ttu-id="54475-1957">Specifica hello sottopercorso toohello cartella.</span><span class="sxs-lookup"><span data-stu-id="54475-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="54475-1958">Utilizzare il carattere di escape hello ' \' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="54475-1959">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="54475-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="54475-1960">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="54475-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="54475-1961">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-1961">Yes</span></span> |
| <span data-ttu-id="54475-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-1962">fileName</span></span> |<span data-ttu-id="54475-1963">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="54475-1964">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="54475-1965">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato è in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="54475-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="54475-1966">`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="54475-1967">No</span><span class="sxs-lookup"><span data-stu-id="54475-1967">No</span></span> |
| <span data-ttu-id="54475-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="54475-1968">fileFilter</span></span> |<span data-ttu-id="54475-1969">Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="54475-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="54475-1970">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="54475-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="54475-1971">Esempio 1: "fileFilter": "*. log"</span><span class="sxs-lookup"><span data-stu-id="54475-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="54475-1972">Esempio 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="54475-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="54475-1973">Si noti che fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="54475-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="54475-1974">No</span><span class="sxs-lookup"><span data-stu-id="54475-1974">No</span></span> |
| <span data-ttu-id="54475-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-1975">partitionedBy</span></span> |<span data-ttu-id="54475-1976">È possibile utilizzare partitionedBy toospecify dinamica folderPath/nome di file per i dati delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="54475-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="54475-1977">Un esempio è folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-1978">No</span><span class="sxs-lookup"><span data-stu-id="54475-1978">No</span></span> |
| <span data-ttu-id="54475-1979">format</span><span class="sxs-lookup"><span data-stu-id="54475-1979">format</span></span> | <span data-ttu-id="54475-1980">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-1981">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-1982">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-1983">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-1984">No</span><span class="sxs-lookup"><span data-stu-id="54475-1984">No</span></span> |
| <span data-ttu-id="54475-1985">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-1985">compression</span></span> | <span data-ttu-id="54475-1986">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-1987">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce).</span><span class="sxs-lookup"><span data-stu-id="54475-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-1988">vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-1989">No</span><span class="sxs-lookup"><span data-stu-id="54475-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="54475-1990">Non è possibile usare fileName e fileFilter contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="54475-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="54475-1991">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-1991">Example</span></span>

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

<span data-ttu-id="54475-1992">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="54475-1993">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="54475-1994">Se si siano copiando i dati dal File System, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-1995">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-1995">Property</span></span> | <span data-ttu-id="54475-1996">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-1996">Description</span></span> | <span data-ttu-id="54475-1997">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-1997">Allowed values</span></span> | <span data-ttu-id="54475-1998">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-1999">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-1999">recursive</span></span> |<span data-ttu-id="54475-2000">Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-2001">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="54475-2001">True, False (default)</span></span> |<span data-ttu-id="54475-2002">No</span><span class="sxs-lookup"><span data-stu-id="54475-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2003">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2003">Example</span></span>

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
<span data-ttu-id="54475-2004">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="54475-2005">Sink File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="54475-2006">Se si copiano dati tooFile sistema, impostare hello **tipo di sink** di hello attività di copia troppo**FileSystemSink**e specificare le seguenti proprietà in hello **sink** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="54475-2007">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2007">Property</span></span> | <span data-ttu-id="54475-2008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2008">Description</span></span> | <span data-ttu-id="54475-2009">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2009">Allowed values</span></span> | <span data-ttu-id="54475-2010">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="54475-2011">copyBehavior</span></span> |<span data-ttu-id="54475-2012">Definisce il comportamento di copia hello quando origine hello è BlobSource o file System.</span><span class="sxs-lookup"><span data-stu-id="54475-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="54475-2013">**PreserveHierarchy:** mantiene la gerarchia di file hello nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="54475-2014">Percorso relativo di hello hello origine toohello origine della cartella dei file, ovvero è hello come percorso relativo di hello hello file toohello destinazione della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="54475-2015">**FlattenHierarchy:** tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="54475-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="54475-2016">file di destinazione Hello vengono creati con un nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="54475-2017">**Oggetto:** unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="54475-2018">Se viene specificato nome di nome/blob file hello, nome di file uniti hello è nome specificato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="54475-2019">In caso contrario, verrà usato un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="54475-2020">No</span><span class="sxs-lookup"><span data-stu-id="54475-2020">No</span></span> |
<span data-ttu-id="54475-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="54475-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="54475-2022">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2022">Example</span></span>

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

<span data-ttu-id="54475-2023">Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="54475-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="54475-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-2025">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2025">Linked service</span></span>
<span data-ttu-id="54475-2026">il set hello servizio collegato di toodefine un FTP **tipo** di hello servizio collegato troppo**server FTP**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2027">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2027">Property</span></span> | <span data-ttu-id="54475-2028">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2028">Description</span></span> | <span data-ttu-id="54475-2029">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2029">Required</span></span> | <span data-ttu-id="54475-2030">Default</span><span class="sxs-lookup"><span data-stu-id="54475-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2031">host</span><span class="sxs-lookup"><span data-stu-id="54475-2031">host</span></span> |<span data-ttu-id="54475-2032">Nome o indirizzo IP del FTP Server hello</span><span class="sxs-lookup"><span data-stu-id="54475-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="54475-2033">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="54475-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2034">authenticationType</span></span> |<span data-ttu-id="54475-2035">Specificare il tipo di autenticazione</span><span class="sxs-lookup"><span data-stu-id="54475-2035">Specify authentication type</span></span> |<span data-ttu-id="54475-2036">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2036">Yes</span></span> |<span data-ttu-id="54475-2037">Di base, anonimo</span><span class="sxs-lookup"><span data-stu-id="54475-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="54475-2038">username</span><span class="sxs-lookup"><span data-stu-id="54475-2038">username</span></span> |<span data-ttu-id="54475-2039">Utente che dispone di server di accesso FTP toohello</span><span class="sxs-lookup"><span data-stu-id="54475-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="54475-2040">No</span><span class="sxs-lookup"><span data-stu-id="54475-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="54475-2041">password</span><span class="sxs-lookup"><span data-stu-id="54475-2041">password</span></span> |<span data-ttu-id="54475-2042">Password per l'utente di hello (nomeutente)</span><span class="sxs-lookup"><span data-stu-id="54475-2042">Password for hello user (username)</span></span> |<span data-ttu-id="54475-2043">No</span><span class="sxs-lookup"><span data-stu-id="54475-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="54475-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-2044">encryptedCredential</span></span> |<span data-ttu-id="54475-2045">Server FTP di credenziali crittografate tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="54475-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="54475-2046">No</span><span class="sxs-lookup"><span data-stu-id="54475-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="54475-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2047">gatewayName</span></span> |<span data-ttu-id="54475-2048">Nome di hello Gateway di gestione dati gateway tooconnect tooan locale server FTP</span><span class="sxs-lookup"><span data-stu-id="54475-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="54475-2049">No</span><span class="sxs-lookup"><span data-stu-id="54475-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="54475-2050">port</span><span class="sxs-lookup"><span data-stu-id="54475-2050">port</span></span> |<span data-ttu-id="54475-2051">Porta su cui hello FTP è in attesa server</span><span class="sxs-lookup"><span data-stu-id="54475-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="54475-2052">No</span><span class="sxs-lookup"><span data-stu-id="54475-2052">No</span></span> |<span data-ttu-id="54475-2053">21</span><span class="sxs-lookup"><span data-stu-id="54475-2053">21</span></span> |
| <span data-ttu-id="54475-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="54475-2054">enableSsl</span></span> |<span data-ttu-id="54475-2055">Specificare se toouse FTP attraverso il canale SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="54475-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="54475-2056">No</span><span class="sxs-lookup"><span data-stu-id="54475-2056">No</span></span> |<span data-ttu-id="54475-2057">true</span><span class="sxs-lookup"><span data-stu-id="54475-2057">true</span></span> |
| <span data-ttu-id="54475-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="54475-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="54475-2059">Specificare se il server tooenable SSL la convalida del certificato quando si utilizza FTP su canale SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="54475-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="54475-2060">No</span><span class="sxs-lookup"><span data-stu-id="54475-2060">No</span></span> |<span data-ttu-id="54475-2061">true</span><span class="sxs-lookup"><span data-stu-id="54475-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="54475-2062">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="54475-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="54475-2063">Esempio: uso di nome utente e password in testo normale per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="54475-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="54475-2064">Esempio: uso di porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="54475-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="54475-2065">Esempio: uso di encryptedCredential per autenticazione e gateway</span><span class="sxs-lookup"><span data-stu-id="54475-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="54475-2066">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-2067">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2067">Dataset</span></span>
<span data-ttu-id="54475-2068">set di dati toodefine un FTP, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2069">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2069">Property</span></span> | <span data-ttu-id="54475-2070">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2070">Description</span></span> | <span data-ttu-id="54475-2071">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-2072">folderPath</span></span> |<span data-ttu-id="54475-2073">Toohello sottocartella percorso.</span><span class="sxs-lookup"><span data-stu-id="54475-2073">Sub path toohello folder.</span></span> <span data-ttu-id="54475-2074">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="54475-2075">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="54475-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="54475-2076">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="54475-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="54475-2077">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2077">Yes</span></span> 
| <span data-ttu-id="54475-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-2078">fileName</span></span> |<span data-ttu-id="54475-2079">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="54475-2080">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="54475-2081">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato:</span><span class="sxs-lookup"><span data-stu-id="54475-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="54475-2082">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="54475-2083">No</span><span class="sxs-lookup"><span data-stu-id="54475-2083">No</span></span> |
| <span data-ttu-id="54475-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="54475-2084">fileFilter</span></span> |<span data-ttu-id="54475-2085">Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="54475-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="54475-2086">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="54475-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="54475-2087">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="54475-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="54475-2088">Esempio 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="54475-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="54475-2089">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="54475-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="54475-2090">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="54475-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="54475-2091">No</span><span class="sxs-lookup"><span data-stu-id="54475-2091">No</span></span> |
| <span data-ttu-id="54475-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-2092">partitionedBy</span></span> |<span data-ttu-id="54475-2093">partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54475-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="54475-2094">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-2095">No</span><span class="sxs-lookup"><span data-stu-id="54475-2095">No</span></span> |
| <span data-ttu-id="54475-2096">format</span><span class="sxs-lookup"><span data-stu-id="54475-2096">format</span></span> | <span data-ttu-id="54475-2097">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-2098">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-2099">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-2100">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-2101">No</span><span class="sxs-lookup"><span data-stu-id="54475-2101">No</span></span> |
| <span data-ttu-id="54475-2102">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-2102">compression</span></span> | <span data-ttu-id="54475-2103">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-2104">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce).</span><span class="sxs-lookup"><span data-stu-id="54475-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-2105">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-2106">No</span><span class="sxs-lookup"><span data-stu-id="54475-2106">No</span></span> |
| <span data-ttu-id="54475-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="54475-2107">useBinaryTransfer</span></span> |<span data-ttu-id="54475-2108">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="54475-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="54475-2109">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="54475-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="54475-2110">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="54475-2110">Default value: True.</span></span> <span data-ttu-id="54475-2111">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="54475-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="54475-2112">No</span><span class="sxs-lookup"><span data-stu-id="54475-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="54475-2113">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="54475-2114">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="54475-2115">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="54475-2116">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="54475-2117">Se si copiano dati da un server FTP, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2118">Property</span></span> | <span data-ttu-id="54475-2119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2119">Description</span></span> | <span data-ttu-id="54475-2120">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2120">Allowed values</span></span> | <span data-ttu-id="54475-2121">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2122">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-2122">recursive</span></span> |<span data-ttu-id="54475-2123">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-2124">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="54475-2124">True, False (default)</span></span> |<span data-ttu-id="54475-2125">No</span><span class="sxs-lookup"><span data-stu-id="54475-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2126">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2126">Example</span></span>

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

<span data-ttu-id="54475-2127">Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="54475-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="54475-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-2129">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2129">Linked service</span></span>
<span data-ttu-id="54475-2130">il set hello servizio collegato di toodefine un HDFS **tipo** di hello servizio collegato troppo**Hdfs**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2131">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2131">Property</span></span> | <span data-ttu-id="54475-2132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2132">Description</span></span> | <span data-ttu-id="54475-2133">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2134">type</span><span class="sxs-lookup"><span data-stu-id="54475-2134">type</span></span> |<span data-ttu-id="54475-2135">proprietà di tipo Hello deve essere impostata su: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="54475-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="54475-2136">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2136">Yes</span></span> |
| <span data-ttu-id="54475-2137">Url</span><span class="sxs-lookup"><span data-stu-id="54475-2137">Url</span></span> |<span data-ttu-id="54475-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="54475-2138">URL toohello HDFS</span></span> |<span data-ttu-id="54475-2139">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2139">Yes</span></span> |
| <span data-ttu-id="54475-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2140">authenticationType</span></span> |<span data-ttu-id="54475-2141">Anonima o Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="54475-2142">toouse **l'autenticazione Kerberos** per connettore HDFS, fare riferimento troppo[in questa sezione](#use-kerberos-authentication-for-hdfs-connector) tooset l'ambiente locale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="54475-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="54475-2143">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2143">Yes</span></span> |
| <span data-ttu-id="54475-2144">userName</span><span class="sxs-lookup"><span data-stu-id="54475-2144">userName</span></span> |<span data-ttu-id="54475-2145">Nome utente per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="54475-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="54475-2146">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="54475-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="54475-2147">password</span><span class="sxs-lookup"><span data-stu-id="54475-2147">password</span></span> |<span data-ttu-id="54475-2148">Password per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="54475-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="54475-2149">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="54475-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="54475-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2150">gatewayName</span></span> |<span data-ttu-id="54475-2151">Nome del gateway hello hello servizio Data Factory deve usare tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="54475-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="54475-2152">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2152">Yes</span></span> |
| <span data-ttu-id="54475-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-2153">encryptedCredential</span></span> |<span data-ttu-id="54475-2154">[Nuovo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output delle credenziali di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="54475-2155">No</span><span class="sxs-lookup"><span data-stu-id="54475-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="54475-2156">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="54475-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="54475-2157">Esempio: uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="54475-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="54475-2158">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-2159">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2159">Dataset</span></span>
<span data-ttu-id="54475-2160">toodefine un set di dati HDFS set hello **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2161">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2161">Property</span></span> | <span data-ttu-id="54475-2162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2162">Description</span></span> | <span data-ttu-id="54475-2163">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-2164">folderPath</span></span> |<span data-ttu-id="54475-2165">Cartella toohello percorso.</span><span class="sxs-lookup"><span data-stu-id="54475-2165">Path toohello folder.</span></span> <span data-ttu-id="54475-2166">Esempio: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="54475-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="54475-2167">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="54475-2168">Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.</span><span class="sxs-lookup"><span data-stu-id="54475-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="54475-2169">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="54475-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="54475-2170">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2170">Yes</span></span> |
| <span data-ttu-id="54475-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-2171">fileName</span></span> |<span data-ttu-id="54475-2172">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="54475-2173">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="54475-2174">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato:</span><span class="sxs-lookup"><span data-stu-id="54475-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="54475-2175">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="54475-2176">No</span><span class="sxs-lookup"><span data-stu-id="54475-2176">No</span></span> |
| <span data-ttu-id="54475-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-2177">partitionedBy</span></span> |<span data-ttu-id="54475-2178">partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54475-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="54475-2179">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-2180">No</span><span class="sxs-lookup"><span data-stu-id="54475-2180">No</span></span> |
| <span data-ttu-id="54475-2181">format</span><span class="sxs-lookup"><span data-stu-id="54475-2181">format</span></span> | <span data-ttu-id="54475-2182">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-2183">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-2184">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-2185">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-2186">No</span><span class="sxs-lookup"><span data-stu-id="54475-2186">No</span></span> |
| <span data-ttu-id="54475-2187">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-2187">compression</span></span> | <span data-ttu-id="54475-2188">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-2189">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-2190">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="54475-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-2191">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-2192">No</span><span class="sxs-lookup"><span data-stu-id="54475-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="54475-2193">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="54475-2194">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2194">Example</span></span>

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

<span data-ttu-id="54475-2195">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="54475-2196">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="54475-2197">Se si copiano dati da HDFS, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="54475-2198">**FileSystemSource** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="54475-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="54475-2199">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2199">Property</span></span> | <span data-ttu-id="54475-2200">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2200">Description</span></span> | <span data-ttu-id="54475-2201">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2201">Allowed values</span></span> | <span data-ttu-id="54475-2202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2203">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-2203">recursive</span></span> |<span data-ttu-id="54475-2204">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-2205">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="54475-2205">True, False (default)</span></span> |<span data-ttu-id="54475-2206">No</span><span class="sxs-lookup"><span data-stu-id="54475-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2207">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2207">Example</span></span>

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

<span data-ttu-id="54475-2208">Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="54475-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="54475-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-2210">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2210">Linked service</span></span>
<span data-ttu-id="54475-2211">il set hello servizio collegato di toodefine un SFTP **tipo** di hello servizio collegato troppo**Sftp**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2212">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2212">Property</span></span> | <span data-ttu-id="54475-2213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2213">Description</span></span> | <span data-ttu-id="54475-2214">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2215">host</span><span class="sxs-lookup"><span data-stu-id="54475-2215">host</span></span> | <span data-ttu-id="54475-2216">Nome o indirizzo IP del server SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="54475-2217">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2217">Yes</span></span> |
| <span data-ttu-id="54475-2218">port</span><span class="sxs-lookup"><span data-stu-id="54475-2218">port</span></span> |<span data-ttu-id="54475-2219">Porta su cui hello SFTP server è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="54475-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="54475-2220">valore predefinito di Hello è: 21</span><span class="sxs-lookup"><span data-stu-id="54475-2220">hello default value is: 21</span></span> |<span data-ttu-id="54475-2221">No</span><span class="sxs-lookup"><span data-stu-id="54475-2221">No</span></span> |
| <span data-ttu-id="54475-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2222">authenticationType</span></span> |<span data-ttu-id="54475-2223">Specificare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54475-2223">Specify authentication type.</span></span> <span data-ttu-id="54475-2224">Valori consentiti: **Base**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="54475-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="54475-2225">Fare riferimento troppo[tramite l'autenticazione di base](#using-basic-authentication) e [tramite SSH autenticazione a chiave pubblica](#using-ssh-public-key-authentication) sezioni su altre proprietà e gli esempi JSON rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="54475-2226">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2226">Yes</span></span> |
| <span data-ttu-id="54475-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="54475-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="54475-2228">Specificare se tooskip chiave convalida dell'host.</span><span class="sxs-lookup"><span data-stu-id="54475-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="54475-2229">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2229">No.</span></span> <span data-ttu-id="54475-2230">Hello valore predefinito: false</span><span class="sxs-lookup"><span data-stu-id="54475-2230">hello default value: false</span></span> |
| <span data-ttu-id="54475-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="54475-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="54475-2232">Specificare impronte digitali hello della chiave host hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="54475-2233">Sì se hello `skipHostKeyValidation` è impostato toofalse.</span><span class="sxs-lookup"><span data-stu-id="54475-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="54475-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2234">gatewayName</span></span> |<span data-ttu-id="54475-2235">Nome di hello Gateway di gestione dati tooconnect tooan locale server SFTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="54475-2236">Sì se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="54475-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-2237">encryptedCredential</span></span> | <span data-ttu-id="54475-2238">Server SFTP hello tooaccess credenziali crittografate.</span><span class="sxs-lookup"><span data-stu-id="54475-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="54475-2239">Generati automaticamente quando si specifica l'autenticazione di base (password e nome utente) o parametri SshPublicKey (nome utente + percorso della chiave privata o contenuto) nella copia guidata o hello ClickOnce finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="54475-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="54475-2240">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2240">No.</span></span> <span data-ttu-id="54475-2241">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="54475-2242">Esempio: uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="54475-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="54475-2243">impostare l'autenticazione di base toouse, `authenticationType` come `Basic`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:</span><span class="sxs-lookup"><span data-stu-id="54475-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="54475-2244">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2244">Property</span></span> | <span data-ttu-id="54475-2245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2245">Description</span></span> | <span data-ttu-id="54475-2246">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2247">username</span><span class="sxs-lookup"><span data-stu-id="54475-2247">username</span></span> | <span data-ttu-id="54475-2248">Utente che dispone di server di accesso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="54475-2249">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2249">Yes</span></span> |
| <span data-ttu-id="54475-2250">password</span><span class="sxs-lookup"><span data-stu-id="54475-2250">password</span></span> | <span data-ttu-id="54475-2251">Password per l'utente di hello (nomeutente).</span><span class="sxs-lookup"><span data-stu-id="54475-2251">Password for hello user (username).</span></span> | <span data-ttu-id="54475-2252">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="54475-2253">Esempio: autenticazione di base con credenziali crittografate**</span><span class="sxs-lookup"><span data-stu-id="54475-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="54475-2254">Esempio: uso dell'autenticazione con chiave pubblica SSH:**</span><span class="sxs-lookup"><span data-stu-id="54475-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="54475-2255">impostare l'autenticazione di base toouse, `authenticationType` come `SshPublicKey`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:</span><span class="sxs-lookup"><span data-stu-id="54475-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="54475-2256">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2256">Property</span></span> | <span data-ttu-id="54475-2257">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2257">Description</span></span> | <span data-ttu-id="54475-2258">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2259">username</span><span class="sxs-lookup"><span data-stu-id="54475-2259">username</span></span> |<span data-ttu-id="54475-2260">Utente che dispone di server di accesso toohello SFTP</span><span class="sxs-lookup"><span data-stu-id="54475-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="54475-2261">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2261">Yes</span></span> |
| <span data-ttu-id="54475-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="54475-2262">privateKeyPath</span></span> | <span data-ttu-id="54475-2263">Specificare un percorso assoluto toohello file di chiave privata accessibile tale gateway.</span><span class="sxs-lookup"><span data-stu-id="54475-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="54475-2264">Specificare entrambi hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="54475-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="54475-2265">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="54475-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="54475-2266">privateKeyContent</span></span> | <span data-ttu-id="54475-2267">Una stringa serializzata del contenuto di chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="54475-2268">Hello Copia guidata è possibile leggere il file di chiave privata di hello ed estrarre automaticamente il contenuto di chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="54475-2269">Se si utilizza qualsiasi altro strumento o SDK, è possibile utilizzare proprietà privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="54475-2270">Specificare entrambi hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="54475-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="54475-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="54475-2271">passPhrase</span></span> | <span data-ttu-id="54475-2272">Specificare hello frase/password toodecrypt hello privati passkey se i file di chiave hello è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="54475-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="54475-2273">Sì se il file di chiave privata di hello è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="54475-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="54475-2274">Esempio: autenticazione SshPublicKey con contenuto della chiave privata**</span><span class="sxs-lookup"><span data-stu-id="54475-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="54475-2275">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-2276">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2276">Dataset</span></span>
<span data-ttu-id="54475-2277">toodefine un set di dati, SFTP, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2278">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2278">Property</span></span> | <span data-ttu-id="54475-2279">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2279">Description</span></span> | <span data-ttu-id="54475-2280">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="54475-2281">folderPath</span></span> |<span data-ttu-id="54475-2282">Toohello sottocartella percorso.</span><span class="sxs-lookup"><span data-stu-id="54475-2282">Sub path toohello folder.</span></span> <span data-ttu-id="54475-2283">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="54475-2284">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="54475-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="54475-2285">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="54475-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="54475-2286">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2286">Yes</span></span> |
| <span data-ttu-id="54475-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="54475-2287">fileName</span></span> |<span data-ttu-id="54475-2288">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="54475-2289">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="54475-2290">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato:</span><span class="sxs-lookup"><span data-stu-id="54475-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="54475-2291">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="54475-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="54475-2292">No</span><span class="sxs-lookup"><span data-stu-id="54475-2292">No</span></span> |
| <span data-ttu-id="54475-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="54475-2293">fileFilter</span></span> |<span data-ttu-id="54475-2294">Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="54475-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="54475-2295">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="54475-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="54475-2296">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="54475-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="54475-2297">Esempio 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="54475-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="54475-2298">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="54475-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="54475-2299">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="54475-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="54475-2300">No</span><span class="sxs-lookup"><span data-stu-id="54475-2300">No</span></span> |
| <span data-ttu-id="54475-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="54475-2301">partitionedBy</span></span> |<span data-ttu-id="54475-2302">partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54475-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="54475-2303">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="54475-2304">No</span><span class="sxs-lookup"><span data-stu-id="54475-2304">No</span></span> |
| <span data-ttu-id="54475-2305">format</span><span class="sxs-lookup"><span data-stu-id="54475-2305">format</span></span> | <span data-ttu-id="54475-2306">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-2307">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="54475-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="54475-2308">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="54475-2309">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="54475-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="54475-2310">No</span><span class="sxs-lookup"><span data-stu-id="54475-2310">No</span></span> |
| <span data-ttu-id="54475-2311">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-2311">compression</span></span> | <span data-ttu-id="54475-2312">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-2313">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-2314">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="54475-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-2315">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-2316">No</span><span class="sxs-lookup"><span data-stu-id="54475-2316">No</span></span> |
| <span data-ttu-id="54475-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="54475-2317">useBinaryTransfer</span></span> |<span data-ttu-id="54475-2318">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="54475-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="54475-2319">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="54475-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="54475-2320">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="54475-2320">Default value: True.</span></span> <span data-ttu-id="54475-2321">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="54475-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="54475-2322">No</span><span class="sxs-lookup"><span data-stu-id="54475-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="54475-2323">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="54475-2324">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="54475-2325">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="54475-2326">Origine File System nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="54475-2327">Se si copiano dati da un'origine SFTP, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2328">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2328">Property</span></span> | <span data-ttu-id="54475-2329">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2329">Description</span></span> | <span data-ttu-id="54475-2330">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2330">Allowed values</span></span> | <span data-ttu-id="54475-2331">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2332">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="54475-2332">recursive</span></span> |<span data-ttu-id="54475-2333">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="54475-2334">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="54475-2334">True, False (default)</span></span> |<span data-ttu-id="54475-2335">No</span><span class="sxs-lookup"><span data-stu-id="54475-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="54475-2336">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2336">Example</span></span>

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

<span data-ttu-id="54475-2337">Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="54475-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="54475-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-2339">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2339">Linked service</span></span>
<span data-ttu-id="54475-2340">il set hello servizio collegato di toodefine un HTTP **tipo** di hello servizio collegato troppo**Http**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2341">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2341">Property</span></span> | <span data-ttu-id="54475-2342">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2342">Description</span></span> | <span data-ttu-id="54475-2343">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2344">URL</span><span class="sxs-lookup"><span data-stu-id="54475-2344">url</span></span> | <span data-ttu-id="54475-2345">URL toohello Server Web di base</span><span class="sxs-lookup"><span data-stu-id="54475-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="54475-2346">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2346">Yes</span></span> |
| <span data-ttu-id="54475-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2347">authenticationType</span></span> | <span data-ttu-id="54475-2348">Specifica il tipo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="54475-2349">I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="54475-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="54475-2350">Vedere rispettivamente toosections riportata sotto questa tabella in più proprietà e gli esempi JSON per i tipi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54475-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="54475-2351">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2351">Yes</span></span> |
| <span data-ttu-id="54475-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="54475-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="54475-2353">Specificare se il server tooenable SSL la convalida del certificato se l'origine è il Server Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="54475-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="54475-2354">No, il valore predefinito è true</span><span class="sxs-lookup"><span data-stu-id="54475-2354">No, default is true</span></span> |
| <span data-ttu-id="54475-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2355">gatewayName</span></span> | <span data-ttu-id="54475-2356">Nome di hello Gateway di gestione dati tooconnect tooan locale origine HTTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="54475-2357">Sì se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="54475-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-2358">encryptedCredential</span></span> | <span data-ttu-id="54475-2359">Credenziali crittografate tooaccess hello endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="54475-2360">Generati automaticamente quando si configurano le informazioni di autenticazione hello in copia guidata o hello ClickOnce finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="54475-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="54475-2361">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2361">No.</span></span> <span data-ttu-id="54475-2362">Applicare solo se si copiano i dati da un server HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="54475-2363">Esempio: uso dell'autenticazione di base, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="54475-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="54475-2364">Impostare `authenticationType` come `Basic`, `Digest`, o `Windows`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:</span><span class="sxs-lookup"><span data-stu-id="54475-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="54475-2365">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2365">Property</span></span> | <span data-ttu-id="54475-2366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2366">Description</span></span> | <span data-ttu-id="54475-2367">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2368">username</span><span class="sxs-lookup"><span data-stu-id="54475-2368">username</span></span> | <span data-ttu-id="54475-2369">Nome utente tooaccess hello endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="54475-2370">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2370">Yes</span></span> |
| <span data-ttu-id="54475-2371">password</span><span class="sxs-lookup"><span data-stu-id="54475-2371">password</span></span> | <span data-ttu-id="54475-2372">Password per l'utente di hello (nomeutente).</span><span class="sxs-lookup"><span data-stu-id="54475-2372">Password for hello user (username).</span></span> | <span data-ttu-id="54475-2373">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="54475-2374">Esempio: uso dell'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="54475-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="54475-2375">impostare l'autenticazione di base toouse, `authenticationType` come `ClientCertificate`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:</span><span class="sxs-lookup"><span data-stu-id="54475-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="54475-2376">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2376">Property</span></span> | <span data-ttu-id="54475-2377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2377">Description</span></span> | <span data-ttu-id="54475-2378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="54475-2379">embeddedCertData</span></span> | <span data-ttu-id="54475-2380">Hello contenuto con codifica Base64 di dati binari del file di scambio di informazioni personali (PFX) hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="54475-2381">Specificare entrambi hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="54475-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="54475-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="54475-2382">certThumbprint</span></span> | <span data-ttu-id="54475-2383">Hello identificazione personale del certificato hello che è stata installata nell'archivio certificati del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="54475-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="54475-2384">Applicare solo se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="54475-2385">Specificare entrambi hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="54475-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="54475-2386">password</span><span class="sxs-lookup"><span data-stu-id="54475-2386">password</span></span> | <span data-ttu-id="54475-2387">Password associata al certificato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="54475-2388">No</span><span class="sxs-lookup"><span data-stu-id="54475-2388">No</span></span> |

<span data-ttu-id="54475-2389">Se si utilizza `certThumbprint` per hello e autenticazione il certificato è installato nell'archivio personale di hello del computer locale hello, è necessario che il servizio gateway toogrant hello autorizzazione di lettura toohello:</span><span class="sxs-lookup"><span data-stu-id="54475-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="54475-2390">Avviare Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="54475-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="54475-2391">Aggiungere hello **certificati** snap-in tale hello destinazioni **Computer locale**.</span><span class="sxs-lookup"><span data-stu-id="54475-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="54475-2392">Espandere **Certificati**, **Personali** e fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="54475-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="54475-2393">Certificato hello dall'archivio personale hello e scegliere **tutte le attività**->**Gestisci chiavi Private...**</span><span class="sxs-lookup"><span data-stu-id="54475-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="54475-2394">In hello **sicurezza** scheda, aggiungere l'account utente di hello in cui è in esecuzione servizio Host di Gateway di gestione di dati con certificato toohello di hello accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="54475-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="54475-2395">**Esempio: utilizzo del certificato client:** questo collegato collegamenti al servizio data factory tooan locale HTTP server web.</span><span class="sxs-lookup"><span data-stu-id="54475-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="54475-2396">Usa un certificato client è installato nel computer di hello con Gateway di gestione di dati installati.</span><span class="sxs-lookup"><span data-stu-id="54475-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="54475-2397">Esempio: utilizzo di un certificato client in un file</span><span class="sxs-lookup"><span data-stu-id="54475-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="54475-2398">Questo collegato collegamenti al servizio data factory tooan locale HTTP server web.</span><span class="sxs-lookup"><span data-stu-id="54475-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="54475-2399">Usa un file del certificato client nel computer di hello con Gateway di gestione di dati installati.</span><span class="sxs-lookup"><span data-stu-id="54475-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="54475-2400">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-2401">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2401">Dataset</span></span>
<span data-ttu-id="54475-2402">set di dati toodefine un HTTP, hello set **tipo** del set di dati hello troppo**Http**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2403">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2403">Property</span></span> | <span data-ttu-id="54475-2404">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2404">Description</span></span> | <span data-ttu-id="54475-2405">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="54475-2406">relativeUrl</span></span> | <span data-ttu-id="54475-2407">Una risorsa relativa di URL toohello che contiene dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="54475-2408">Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="54475-2409">tooconstruct URL dinamico, è possibile utilizzare [funzioni di Data Factory e le variabili di sistema](data-factory-functions-variables.md), esempio: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="54475-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="54475-2410">No</span><span class="sxs-lookup"><span data-stu-id="54475-2410">No</span></span> |
| <span data-ttu-id="54475-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="54475-2411">requestMethod</span></span> | <span data-ttu-id="54475-2412">Metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2412">Http method.</span></span> <span data-ttu-id="54475-2413">I valori consentiti sono **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="54475-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="54475-2414">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2414">No.</span></span> <span data-ttu-id="54475-2415">Il valore predefinito è `GET`.</span><span class="sxs-lookup"><span data-stu-id="54475-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="54475-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="54475-2416">additionalHeaders</span></span> | <span data-ttu-id="54475-2417">Intestazioni richiesta HTTP aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="54475-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="54475-2418">No</span><span class="sxs-lookup"><span data-stu-id="54475-2418">No</span></span> |
| <span data-ttu-id="54475-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="54475-2419">requestBody</span></span> | <span data-ttu-id="54475-2420">Il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="54475-2420">Body for HTTP request.</span></span> | <span data-ttu-id="54475-2421">No</span><span class="sxs-lookup"><span data-stu-id="54475-2421">No</span></span> |
| <span data-ttu-id="54475-2422">format</span><span class="sxs-lookup"><span data-stu-id="54475-2422">format</span></span> | <span data-ttu-id="54475-2423">Se si desidera toosimply **recuperare i dati di hello da endpoint HTTP come-è** senza analizzarlo, ignorare questa impostazione di formato.</span><span class="sxs-lookup"><span data-stu-id="54475-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="54475-2424">Se si desidera tooparse hello HTTP risposta contenuto durante la copia, è supportato i seguenti tipi di formato hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="54475-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="54475-2425">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="54475-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="54475-2426">No</span><span class="sxs-lookup"><span data-stu-id="54475-2426">No</span></span> |
| <span data-ttu-id="54475-2427">compressione</span><span class="sxs-lookup"><span data-stu-id="54475-2427">compression</span></span> | <span data-ttu-id="54475-2428">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="54475-2429">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="54475-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="54475-2430">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="54475-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="54475-2431">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="54475-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="54475-2432">No</span><span class="sxs-lookup"><span data-stu-id="54475-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="54475-2433">Esempio: hello metodo GET (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="54475-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="54475-2434">Esempio: utilizzo di metodo POST hello</span><span class="sxs-lookup"><span data-stu-id="54475-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="54475-2435">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="54475-2436">Origine HTTP nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="54475-2437">Se si copiano dati da un'origine HTTP, impostare hello **tipo di origine** di hello attività di copia troppo**HttpSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2438">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2438">Property</span></span> | <span data-ttu-id="54475-2439">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2439">Description</span></span> | <span data-ttu-id="54475-2440">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="54475-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="54475-2441">httpRequestTimeout</span></span> | <span data-ttu-id="54475-2442">Hello timeout (TimeSpan) per hello HTTP richiesta tooget una risposta.</span><span class="sxs-lookup"><span data-stu-id="54475-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="54475-2443">È hello timeout tooget una risposta, dati di risposta non hello timeout tooread.</span><span class="sxs-lookup"><span data-stu-id="54475-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="54475-2444">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2444">No.</span></span> <span data-ttu-id="54475-2445">Valore predefinito: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="54475-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-2446">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="54475-2447">Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="54475-2448">OData</span><span class="sxs-lookup"><span data-stu-id="54475-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-2449">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2449">Linked service</span></span>
<span data-ttu-id="54475-2450">il servizio hello set toodefine OData collegato **tipo** di hello servizio collegato troppo**OData**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2451">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2451">Property</span></span> | <span data-ttu-id="54475-2452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2452">Description</span></span> | <span data-ttu-id="54475-2453">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2454">URL</span><span class="sxs-lookup"><span data-stu-id="54475-2454">url</span></span> |<span data-ttu-id="54475-2455">URL del servizio OData hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2455">Url of hello OData service.</span></span> |<span data-ttu-id="54475-2456">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2456">Yes</span></span> |
| <span data-ttu-id="54475-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2457">authenticationType</span></span> |<span data-ttu-id="54475-2458">Tipo di autenticazione usato tooconnect toohello un'origine OData.</span><span class="sxs-lookup"><span data-stu-id="54475-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="54475-2459">Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="54475-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="54475-2460">Per OData locale, i valori possibili sono Anonima, Di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54475-2461">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2461">Yes</span></span> |
| <span data-ttu-id="54475-2462">username</span><span class="sxs-lookup"><span data-stu-id="54475-2462">username</span></span> |<span data-ttu-id="54475-2463">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="54475-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="54475-2464">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="54475-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="54475-2465">password</span><span class="sxs-lookup"><span data-stu-id="54475-2465">password</span></span> |<span data-ttu-id="54475-2466">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-2467">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="54475-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="54475-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="54475-2468">authorizedCredential</span></span> |<span data-ttu-id="54475-2469">Se si utilizza OAuth, fare clic su **Authorize** pulsante nell'Editor o hello Data Factory Copia guidata e immettere le credenziali, il valore di hello di questa proprietà verrà generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="54475-2470">Sì (solo se si usa l'autenticazione OAuth)</span><span class="sxs-lookup"><span data-stu-id="54475-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="54475-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2471">gatewayName</span></span> |<span data-ttu-id="54475-2472">Nome del gateway hello hello servizio Data Factory deve usare servizio OData di tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="54475-2473">Specificare solo se si copiano dati da un'origine OData locale.</span><span class="sxs-lookup"><span data-stu-id="54475-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="54475-2474">No</span><span class="sxs-lookup"><span data-stu-id="54475-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="54475-2475">Esempio - Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="54475-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="54475-2476">Esempio - Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="54475-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="54475-2477">Esempio - Uso dell'autenticazione Windows per accedere all'origine OData locale</span><span class="sxs-lookup"><span data-stu-id="54475-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="54475-2478">Esempio - Uso dell'autenticazione OAuth per accedere all'origine OData cloud</span><span class="sxs-lookup"><span data-stu-id="54475-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="54475-2479">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="54475-2480">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2480">Dataset</span></span>
<span data-ttu-id="54475-2481">toodefine un set di dati OData, hello set **tipo** del set di dati hello troppo**ODataResource**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2482">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2482">Property</span></span> | <span data-ttu-id="54475-2483">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2483">Description</span></span> | <span data-ttu-id="54475-2484">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2485">path</span><span class="sxs-lookup"><span data-stu-id="54475-2485">path</span></span> |<span data-ttu-id="54475-2486">Percorso toohello risorse OData</span><span class="sxs-lookup"><span data-stu-id="54475-2486">Path toohello OData resource</span></span> |<span data-ttu-id="54475-2487">No</span><span class="sxs-lookup"><span data-stu-id="54475-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2488">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2488">Example</span></span>

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

<span data-ttu-id="54475-2489">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-2490">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-2491">Se si copiano dati da un'origine OData, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2492">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2492">Property</span></span> | <span data-ttu-id="54475-2493">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2493">Description</span></span> | <span data-ttu-id="54475-2494">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2494">Example</span></span> | <span data-ttu-id="54475-2495">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2496">query</span><span class="sxs-lookup"><span data-stu-id="54475-2496">query</span></span> |<span data-ttu-id="54475-2497">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="54475-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="54475-2499">No</span><span class="sxs-lookup"><span data-stu-id="54475-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2500">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2500">Example</span></span>

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

<span data-ttu-id="54475-2501">Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="54475-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="54475-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-2503">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2503">Linked service</span></span>
<span data-ttu-id="54475-2504">il set hello servizio collegato di toodefine un ODBC **tipo** di hello servizio collegato troppo**OnPremisesOdbc**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2505">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2505">Property</span></span> | <span data-ttu-id="54475-2506">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2506">Description</span></span> | <span data-ttu-id="54475-2507">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-2508">connectionString</span></span> |<span data-ttu-id="54475-2509">credenziale è crittografata da parte di credenziali di accesso non Hello di stringa di connessione hello e un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="54475-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="54475-2510">Vedere esempi in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="54475-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="54475-2511">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2511">Yes</span></span> |
| <span data-ttu-id="54475-2512">credential</span><span class="sxs-lookup"><span data-stu-id="54475-2512">credential</span></span> |<span data-ttu-id="54475-2513">parte delle credenziali di accesso Hello hello della stringa di connessione specificato nel formato valore della proprietà specifiche del driver.</span><span class="sxs-lookup"><span data-stu-id="54475-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="54475-2514">Esempio: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="54475-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="54475-2515">No</span><span class="sxs-lookup"><span data-stu-id="54475-2515">No</span></span> |
| <span data-ttu-id="54475-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2516">authenticationType</span></span> |<span data-ttu-id="54475-2517">Tipo di autenticazione utilizzato l'archivio di dati ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="54475-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="54475-2518">I valori possibili sono: anonima e di base.</span><span class="sxs-lookup"><span data-stu-id="54475-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="54475-2519">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2519">Yes</span></span> |
| <span data-ttu-id="54475-2520">username</span><span class="sxs-lookup"><span data-stu-id="54475-2520">username</span></span> |<span data-ttu-id="54475-2521">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="54475-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="54475-2522">No</span><span class="sxs-lookup"><span data-stu-id="54475-2522">No</span></span> |
| <span data-ttu-id="54475-2523">password</span><span class="sxs-lookup"><span data-stu-id="54475-2523">password</span></span> |<span data-ttu-id="54475-2524">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-2525">No</span><span class="sxs-lookup"><span data-stu-id="54475-2525">No</span></span> |
| <span data-ttu-id="54475-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2526">gatewayName</span></span> |<span data-ttu-id="54475-2527">Nome del gateway hello hello servizio Data Factory deve utilizzare l'archivio di dati ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="54475-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="54475-2528">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="54475-2529">Esempio - Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="54475-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="54475-2530">Esempio - Uso dell'autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="54475-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="54475-2531">È possibile crittografare le credenziali di hello utilizzando hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versione di Azure PowerShell) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 o versioni precedenti di hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="54475-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="54475-2532">Esempio: uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="54475-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="54475-2533">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-2534">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2534">Dataset</span></span>
<span data-ttu-id="54475-2535">toodefine un set di dati ODBC, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2536">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2536">Property</span></span> | <span data-ttu-id="54475-2537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2537">Description</span></span> | <span data-ttu-id="54475-2538">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-2539">tableName</span></span> |<span data-ttu-id="54475-2540">Nome della tabella hello nell'archivio di dati ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="54475-2541">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="54475-2542">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2542">Example</span></span>

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

<span data-ttu-id="54475-2543">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-2544">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-2545">Se si copiano dati da un archivio di dati ODBC, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2546">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2546">Property</span></span> | <span data-ttu-id="54475-2547">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2547">Description</span></span> | <span data-ttu-id="54475-2548">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2548">Allowed values</span></span> | <span data-ttu-id="54475-2549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2550">query</span><span class="sxs-lookup"><span data-stu-id="54475-2550">query</span></span> |<span data-ttu-id="54475-2551">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-2552">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-2552">SQL query string.</span></span> <span data-ttu-id="54475-2553">Ad esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="54475-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="54475-2554">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2555">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2555">Example</span></span>

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

<span data-ttu-id="54475-2556">Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="54475-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="54475-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="54475-2558">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2558">Linked service</span></span>
<span data-ttu-id="54475-2559">il set hello servizio collegato di Salesforce toodefine **tipo** di hello servizio collegato troppo**Salesforce**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2560">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2560">Property</span></span> | <span data-ttu-id="54475-2561">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2561">Description</span></span> | <span data-ttu-id="54475-2562">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="54475-2563">environmentUrl</span></span> | <span data-ttu-id="54475-2564">Specificare l'istanza di URL di Salesforce hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="54475-2565">- Il valore predefinito è "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="54475-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="54475-2566">-toocopy dati dalla sandbox, specificare "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="54475-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="54475-2567">-toocopy dati da un dominio personalizzato, specificare, ad esempio, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="54475-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="54475-2568">No</span><span class="sxs-lookup"><span data-stu-id="54475-2568">No</span></span> |
| <span data-ttu-id="54475-2569">username</span><span class="sxs-lookup"><span data-stu-id="54475-2569">username</span></span> |<span data-ttu-id="54475-2570">Specificare un nome utente per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="54475-2571">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2571">Yes</span></span> |
| <span data-ttu-id="54475-2572">password</span><span class="sxs-lookup"><span data-stu-id="54475-2572">password</span></span> |<span data-ttu-id="54475-2573">Specificare una password per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="54475-2574">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2574">Yes</span></span> |
| <span data-ttu-id="54475-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="54475-2575">securityToken</span></span> |<span data-ttu-id="54475-2576">Specificare un token di sicurezza per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="54475-2577">Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come un token di sicurezza tooreset/get.</span><span class="sxs-lookup"><span data-stu-id="54475-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="54475-2578">in generale, vedere toolearn sui token di sicurezza [API di protezione e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="54475-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="54475-2579">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2580">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2580">Example</span></span>

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

<span data-ttu-id="54475-2581">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-2582">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2582">Dataset</span></span>
<span data-ttu-id="54475-2583">toodefine un set di dati di Salesforce, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2584">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2584">Property</span></span> | <span data-ttu-id="54475-2585">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2585">Description</span></span> | <span data-ttu-id="54475-2586">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="54475-2587">tableName</span></span> |<span data-ttu-id="54475-2588">Nome della tabella hello in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="54475-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="54475-2589">No, se è specificata una **query** di **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="54475-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2590">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2590">Example</span></span>

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

<span data-ttu-id="54475-2591">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="54475-2592">Origine relazionale nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="54475-2593">Se si copiano dati da Salesforce, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="54475-2594">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2594">Property</span></span> | <span data-ttu-id="54475-2595">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2595">Description</span></span> | <span data-ttu-id="54475-2596">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54475-2596">Allowed values</span></span> | <span data-ttu-id="54475-2597">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54475-2598">query</span><span class="sxs-lookup"><span data-stu-id="54475-2598">query</span></span> |<span data-ttu-id="54475-2599">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54475-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="54475-2600">Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="54475-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="54475-2601">Ad esempio: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="54475-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="54475-2602">No (se hello **tableName** di hello **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="54475-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2603">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="54475-2604">parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="54475-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="54475-2605">Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="54475-2606">Dati Web</span><span class="sxs-lookup"><span data-stu-id="54475-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2607">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2607">Linked service</span></span>
<span data-ttu-id="54475-2608">il servizio hello set toodefine Web collegato **tipo** di hello servizio collegato troppo**Web**e specificare le seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2609">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2609">Property</span></span> | <span data-ttu-id="54475-2610">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2610">Description</span></span> | <span data-ttu-id="54475-2611">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2612">Url</span><span class="sxs-lookup"><span data-stu-id="54475-2612">Url</span></span> |<span data-ttu-id="54475-2613">Origine di URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="54475-2613">URL toohello Web source</span></span> |<span data-ttu-id="54475-2614">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2614">Yes</span></span> |
| <span data-ttu-id="54475-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="54475-2615">authenticationType</span></span> |<span data-ttu-id="54475-2616">Anonimo.</span><span class="sxs-lookup"><span data-stu-id="54475-2616">Anonymous.</span></span> |<span data-ttu-id="54475-2617">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="54475-2618">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2618">Example</span></span>


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

<span data-ttu-id="54475-2619">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="54475-2620">Set di dati</span><span class="sxs-lookup"><span data-stu-id="54475-2620">Dataset</span></span>
<span data-ttu-id="54475-2621">toodefine un set di dati Web hello set **tipo** del set di dati hello troppo**tabella Web**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="54475-2622">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2622">Property</span></span> | <span data-ttu-id="54475-2623">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2623">Description</span></span> | <span data-ttu-id="54475-2624">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-2625">type</span><span class="sxs-lookup"><span data-stu-id="54475-2625">type</span></span> |<span data-ttu-id="54475-2626">tipo di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2626">type of hello dataset.</span></span> <span data-ttu-id="54475-2627">deve essere impostato troppo**tabella Web**</span><span class="sxs-lookup"><span data-stu-id="54475-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="54475-2628">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2628">Yes</span></span> |
| <span data-ttu-id="54475-2629">path</span><span class="sxs-lookup"><span data-stu-id="54475-2629">path</span></span> |<span data-ttu-id="54475-2630">Una risorsa relativa di URL toohello che contiene la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="54475-2631">No.</span><span class="sxs-lookup"><span data-stu-id="54475-2631">No.</span></span> <span data-ttu-id="54475-2632">Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="54475-2633">index</span><span class="sxs-lookup"><span data-stu-id="54475-2633">index</span></span> |<span data-ttu-id="54475-2634">indice di Hello della tabella hello nella risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="54475-2635">Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML.</span><span class="sxs-lookup"><span data-stu-id="54475-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="54475-2636">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="54475-2637">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2637">Example</span></span>

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

<span data-ttu-id="54475-2638">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="54475-2639">Origine Web nell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="54475-2640">Se si copiano dati da una tabella, impostare hello **tipo di origine** di hello attività di copia troppo**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="54475-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="54475-2641">Attualmente, quando origine hello in attività di copia è di tipo **WebSource**, non sono supportate proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="54475-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="54475-2642">Esempio</span><span class="sxs-lookup"><span data-stu-id="54475-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="54475-2643">Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="54475-2644">Ambienti di calcolo</span><span class="sxs-lookup"><span data-stu-id="54475-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="54475-2645">Hello nella tabella seguente elenca gli ambienti di calcolo hello è supportati da Data Factory e hello attività di trasformazione che è possibile eseguire su di essi.</span><span class="sxs-lookup"><span data-stu-id="54475-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="54475-2646">Fare clic sul collegamento hello per il calcolo hello si è interessati negli schemi JSON hello toosee per toolink servizio collegato data factory di tooa.</span><span class="sxs-lookup"><span data-stu-id="54475-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="54475-2647">Ambiente di calcolo</span><span class="sxs-lookup"><span data-stu-id="54475-2647">Compute environment</span></span> | <span data-ttu-id="54475-2648">Attività</span><span class="sxs-lookup"><span data-stu-id="54475-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="54475-2649">[Cluster HDInsight su richiesta](#on-demand-azure-hdinsight-cluster) o [il proprio cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="54475-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="54475-2650">[Attività personalizzata .NET ](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig](#hdinsight-pig-activity, [attività MapReduce](#hdinsight-mapreduce-activity), [attività di Hadoop Streaming](#hdinsight-streaming-activityd), [attività Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="54475-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="54475-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54475-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="54475-2652">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="54475-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="54475-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="54475-2654">[Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="54475-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="54475-2655">Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="54475-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="54475-2656">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="54475-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="54475-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="54475-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="54475-2658">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="54475-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="54475-2659">Cluster HDInsight di Azure su richiesta</span><span class="sxs-lookup"><span data-stu-id="54475-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="54475-2660">Hello servizio Azure Data Factory può creare automaticamente un dati di tooprocess di basati su Windows o Linux su richiesta HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54475-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="54475-2661">Hello cluster viene creato nella stessa area dell'account di archiviazione hello (proprietà linkedServiceName in JSON hello) associata a cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="54475-2662">È possibile eseguire hello seguire le attività di trasformazione di questo servizio collegato: [attività personalizzate .NET](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig] (#hdinsight--attività pig, [attività MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming attività](#hdinsight-streaming-activityd), [nascita attività](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="54475-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2663">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2663">Linked service</span></span> 
<span data-ttu-id="54475-2664">Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="54475-2665">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2665">Property</span></span> | <span data-ttu-id="54475-2666">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2666">Description</span></span> | <span data-ttu-id="54475-2667">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2668">type</span><span class="sxs-lookup"><span data-stu-id="54475-2668">type</span></span> |<span data-ttu-id="54475-2669">proprietà tipo Hello deve essere impostato troppo**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="54475-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="54475-2670">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2670">Yes</span></span> |
| <span data-ttu-id="54475-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="54475-2671">clusterSize</span></span> |<span data-ttu-id="54475-2672">Numero di nodi di lavoro o dati in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="54475-2673">cluster HDInsight Hello viene creato con 2 nodi head e il numero di hello di nodi di lavoro che è specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="54475-2674">nodi Hello sono di dimensioni Standard_D3 con 4 core, pertanto un cluster di nodi di 4 lavoro accetta 24 core (4\*4 = 16 core per i nodi di lavoro, più 2\*4 = 8 core per i nodi head).</span><span class="sxs-lookup"><span data-stu-id="54475-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="54475-2675">Vedere [cluster basati su Linux creare Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) per informazioni dettagliate su livello hello Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="54475-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="54475-2676">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2676">Yes</span></span> |
| <span data-ttu-id="54475-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="54475-2677">timetolive</span></span> |<span data-ttu-id="54475-2678">Hello consentito tempo di inattività per il cluster HDInsight su richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="54475-2679">Specifica quanto tempo rimarrà attivo cluster HDInsight su richiesta di hello dopo il completamento di un'attività eseguita se non sono disponibili altri processi attivi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="54475-2680">Ad esempio, se un'attività eseguita richiede 6 minuti e la proprietà timetolive è impostato too5 minuti, hello cluster rimane attivo per 5 minuti dopo hello 6 minuti di elaborazione di esecuzione dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="54475-2681">Se l'esecuzione di un'altra attività viene eseguita con finestra 6 minuti hello, che viene elaborato dalla hello dello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="54475-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="54475-2682">Creazione di un cluster di HDInsight su richiesta è un'operazione dispendiosa (potrebbe richiedere un po' di tempo), quindi utilizzare questa impostazione prestazioni tooimprove necessari per una data factory riutilizzando un cluster di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="54475-2683">Se si imposta la proprietà timetolive valore too0, cluster hello viene eliminato non appena l'esecuzione di attività hello in elaborato.</span><span class="sxs-lookup"><span data-stu-id="54475-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="54475-2684">In hello invece se si imposta un valore elevato, cluster hello può rimanere inattivo inutilmente risultante in costi elevati.</span><span class="sxs-lookup"><span data-stu-id="54475-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="54475-2685">Pertanto, è importante impostare hello di valore appropriato in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="54475-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="54475-2686">Più pipeline possono condividere hello stessa istanza del cluster HDInsight su richiesta di hello se il valore della proprietà timetolive hello è impostato in modo appropriato</span><span class="sxs-lookup"><span data-stu-id="54475-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="54475-2687">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2687">Yes</span></span> |
| <span data-ttu-id="54475-2688">version</span><span class="sxs-lookup"><span data-stu-id="54475-2688">version</span></span> |<span data-ttu-id="54475-2689">Versione del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="54475-2690">Per informazioni dettagliate vedere le [versioni supportate di HDInsight in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="54475-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="54475-2691">No</span><span class="sxs-lookup"><span data-stu-id="54475-2691">No</span></span> |
| <span data-ttu-id="54475-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54475-2692">linkedServiceName</span></span> |<span data-ttu-id="54475-2693">Servizio collegato di archiviazione Azure: toobe utilizzato dal cluster di hello su richiesta per l'archiviazione e l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="54475-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="54475-2694">Attualmente, è possibile creare un cluster HDInsight su richiesta che utilizza un archivio Azure Data Lake come archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="54475-2695">Se si desiderano dati del risultato hello toostore dal HDInsight l'elaborazione in un archivio Azure Data Lake, utilizzare un attività di copia toocopy hello dati dall'archiviazione Blob di Azure di hello toohello archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="54475-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="54475-2696">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2696">Yes</span></span> |
| <span data-ttu-id="54475-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="54475-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="54475-2698">Specifica l'account di archiviazione aggiuntivi per hello HDInsight servizio collegato in modo che il servizio di Data Factory hello può registrare per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="54475-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="54475-2699">No</span><span class="sxs-lookup"><span data-stu-id="54475-2699">No</span></span> |
| <span data-ttu-id="54475-2700">osType</span><span class="sxs-lookup"><span data-stu-id="54475-2700">osType</span></span> |<span data-ttu-id="54475-2701">Tipo di sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="54475-2701">Type of operating system.</span></span> <span data-ttu-id="54475-2702">I valori consentiti sono: Windows (impostazione predefinita) e Linux</span><span class="sxs-lookup"><span data-stu-id="54475-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="54475-2703">No</span><span class="sxs-lookup"><span data-stu-id="54475-2703">No</span></span> |
| <span data-ttu-id="54475-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54475-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="54475-2705">nome Hello del collegato SQL Azure database HCatalog toohello punto del servizio.</span><span class="sxs-lookup"><span data-stu-id="54475-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="54475-2706">cluster di HDInsight su richiesta Hello viene creato utilizzando il database di SQL Azure hello come metastore hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="54475-2707">No</span><span class="sxs-lookup"><span data-stu-id="54475-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="54475-2708">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2708">JSON example</span></span>
<span data-ttu-id="54475-2709">Hello JSON seguente definisce un servizio di collegato di HDInsight su richiesta basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="54475-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="54475-2710">Hello servizio Data Factory crea automaticamente un **basati su Linux** cluster HDInsight durante l'elaborazione di una sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="54475-2711">Per altre informazioni, vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="54475-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="54475-2712">Cluster HDInsight di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="54475-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="54475-2713">È possibile creare cluster HDInsight un tooregister di servizio collegato di HDInsight di Azure con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="54475-2714">È possibile eseguire hello seguente attività di trasformazione dei dati in questo servizio collegato: [attività personalizzate .NET](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig] (#hdinsight--attività pig, [MapReduce attività](#hdinsight-mapreduce-activity), [Hadoop streaming attività](#hdinsight-streaming-activityd), [nascita attività](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="54475-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2715">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2715">Linked service</span></span>
<span data-ttu-id="54475-2716">Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="54475-2717">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2717">Property</span></span> | <span data-ttu-id="54475-2718">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2718">Description</span></span> | <span data-ttu-id="54475-2719">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2720">type</span><span class="sxs-lookup"><span data-stu-id="54475-2720">type</span></span> |<span data-ttu-id="54475-2721">proprietà tipo Hello deve essere impostato troppo**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="54475-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="54475-2722">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2722">Yes</span></span> |
| <span data-ttu-id="54475-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="54475-2723">clusterUri</span></span> |<span data-ttu-id="54475-2724">URI del cluster HDInsight hello Hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="54475-2725">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2725">Yes</span></span> |
| <span data-ttu-id="54475-2726">username</span><span class="sxs-lookup"><span data-stu-id="54475-2726">username</span></span> |<span data-ttu-id="54475-2727">Specificare nome hello di hello utente toobe utilizzata cluster di HDInsight tooconnect tooan esistente.</span><span class="sxs-lookup"><span data-stu-id="54475-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="54475-2728">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2728">Yes</span></span> |
| <span data-ttu-id="54475-2729">password</span><span class="sxs-lookup"><span data-stu-id="54475-2729">password</span></span> |<span data-ttu-id="54475-2730">Specificare la password per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="54475-2731">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2731">Yes</span></span> |
| <span data-ttu-id="54475-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54475-2732">linkedServiceName</span></span> | <span data-ttu-id="54475-2733">Nome di servizio collegato di archiviazione di Azure che fa riferimento nell'archiviazione blob di Azure toohello hello utilizzato da hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54475-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="54475-2734">Attualmente non è possibile specificare un servizio collegato di Azure Data Lake Store per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="54475-2735">È possibile accedere ai dati hello archivio Azure Data Lake dagli script Hive o Pig se il cluster di HDInsight hello dispone di accesso toohello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="54475-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="54475-2736">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2736">Yes</span></span> |

<span data-ttu-id="54475-2737">Per le versioni dei cluster di HDInsight, vedere le [versioni supportate di HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="54475-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="54475-2738">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="54475-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54475-2739">Azure Batch</span></span>
<span data-ttu-id="54475-2740">È possibile creare un pool di Batch di macchine virtuali (VM) di un tooregister di servizio collegato di Azure Batch con una data factory.</span><span class="sxs-lookup"><span data-stu-id="54475-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="54475-2741">È possibile eseguire le attività .NET personalizzate utilizzando Batch Azure o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54475-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="54475-2742">Su questo servizio collegato è possibile eseguire un' [attività personalizzata .NET](#net-custom-activity).</span><span class="sxs-lookup"><span data-stu-id="54475-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2743">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2743">Linked service</span></span>
<span data-ttu-id="54475-2744">Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="54475-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="54475-2745">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2745">Property</span></span> | <span data-ttu-id="54475-2746">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2746">Description</span></span> | <span data-ttu-id="54475-2747">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2748">type</span><span class="sxs-lookup"><span data-stu-id="54475-2748">type</span></span> |<span data-ttu-id="54475-2749">proprietà tipo Hello deve essere impostato troppo**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="54475-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="54475-2750">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2750">Yes</span></span> |
| <span data-ttu-id="54475-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="54475-2751">accountName</span></span> |<span data-ttu-id="54475-2752">Nome dell'account Azure Batch hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="54475-2753">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2753">Yes</span></span> |
| <span data-ttu-id="54475-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="54475-2754">accessKey</span></span> |<span data-ttu-id="54475-2755">Chiave di accesso per account Azure Batch hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="54475-2756">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2756">Yes</span></span> |
| <span data-ttu-id="54475-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="54475-2757">poolName</span></span> |<span data-ttu-id="54475-2758">Nome del pool di hello delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="54475-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="54475-2759">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2759">Yes</span></span> |
| <span data-ttu-id="54475-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54475-2760">linkedServiceName</span></span> |<span data-ttu-id="54475-2761">Nome del servizio collegato di archiviazione di Azure associato a questo servizio collegato di Azure Batch hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="54475-2762">Questo servizio collegato viene utilizzato per i file di gestione temporanea attività hello toorun e l'archiviazione dei log di esecuzione di attività hello obbligatori.</span><span class="sxs-lookup"><span data-stu-id="54475-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="54475-2763">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="54475-2764">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="54475-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-2765">Azure Machine Learning</span></span>
<span data-ttu-id="54475-2766">Creare un tooregister di servizio collegato di Azure Machine Learning punteggio endpoint con una data factory di un batch di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="54475-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="54475-2767">Su questo servizio collegato è possibile eseguire due attività di trasformazione dati: [Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="54475-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2768">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2768">Linked service</span></span>
<span data-ttu-id="54475-2769">Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="54475-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="54475-2770">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2770">Property</span></span> | <span data-ttu-id="54475-2771">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2771">Description</span></span> | <span data-ttu-id="54475-2772">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2773">Tipo</span><span class="sxs-lookup"><span data-stu-id="54475-2773">Type</span></span> |<span data-ttu-id="54475-2774">proprietà di tipo Hello deve essere impostata su: **Azure ml**.</span><span class="sxs-lookup"><span data-stu-id="54475-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="54475-2775">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2775">Yes</span></span> |
| <span data-ttu-id="54475-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="54475-2776">mlEndpoint</span></span> |<span data-ttu-id="54475-2777">URL di punteggio batch di Hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="54475-2778">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2778">Yes</span></span> |
| <span data-ttu-id="54475-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="54475-2779">apiKey</span></span> |<span data-ttu-id="54475-2780">Hello pubblicati API del modello di area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="54475-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="54475-2781">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="54475-2782">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="54475-2783">Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="54475-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="54475-2784">Si crea un **Azure Data Lake Analitica** collegati toolink servizio una factory di dati di Azure tooan del servizio di calcolo di Azure Data Lake Analitica prima di utilizzare hello [attività Data Lake Analitica U-SQL](data-factory-usql-activity.md) in una pipeline .</span><span class="sxs-lookup"><span data-stu-id="54475-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="54475-2785">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2785">Linked service</span></span>

<span data-ttu-id="54475-2786">Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione JSON hello di un servizio di Azure Data Lake Analitica collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="54475-2787">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2787">Property</span></span> | <span data-ttu-id="54475-2788">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2788">Description</span></span> | <span data-ttu-id="54475-2789">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="54475-2790">Type</span></span> |<span data-ttu-id="54475-2791">proprietà di tipo Hello deve essere impostata su: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="54475-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="54475-2792">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2792">Yes</span></span> |
| <span data-ttu-id="54475-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="54475-2793">accountName</span></span> |<span data-ttu-id="54475-2794">Nome dell'account di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="54475-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="54475-2795">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2795">Yes</span></span> |
| <span data-ttu-id="54475-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="54475-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="54475-2797">URI di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="54475-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="54475-2798">No</span><span class="sxs-lookup"><span data-stu-id="54475-2798">No</span></span> |
| <span data-ttu-id="54475-2799">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="54475-2799">authorization</span></span> |<span data-ttu-id="54475-2800">Codice di autorizzazione viene recuperato automaticamente dopo aver fatto clic **Authorize** pulsante hello Editor delle Data Factory e completamento dell'account di accesso hello OAuth.</span><span class="sxs-lookup"><span data-stu-id="54475-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="54475-2801">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2801">Yes</span></span> |
| <span data-ttu-id="54475-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="54475-2802">subscriptionId</span></span> |<span data-ttu-id="54475-2803">ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-2803">Azure subscription id</span></span> |<span data-ttu-id="54475-2804">No (se non specificato, sottoscrizione di hello viene utilizzata una data factory).</span><span class="sxs-lookup"><span data-stu-id="54475-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="54475-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="54475-2805">resourceGroupName</span></span> |<span data-ttu-id="54475-2806">Nome del gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-2806">Azure resource group name</span></span> |<span data-ttu-id="54475-2807">No (se non specificato, il gruppo di risorse di hello viene utilizzata una data factory).</span><span class="sxs-lookup"><span data-stu-id="54475-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="54475-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="54475-2808">sessionId</span></span> |<span data-ttu-id="54475-2809">id di sessione dalla sessione di autorizzazione OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="54475-2810">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="54475-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="54475-2811">Quando si utilizza l'Editor delle Data Factory di hello, questo ID viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54475-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="54475-2812">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="54475-2813">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2813">JSON example</span></span>
<span data-ttu-id="54475-2814">Hello di esempio seguente fornisce una definizione JSON per un servizio di Azure Data Lake Analitica collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="54475-2815">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-2815">Azure SQL Database</span></span>
<span data-ttu-id="54475-2816">È possibile creare un servizio collegato SQL Azure e usarlo con hello [attività Stored Procedure](#stored-procedure-activity) tooinvoke una stored procedure da una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2817">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2817">Linked service</span></span>
<span data-ttu-id="54475-2818">il set hello servizio collegato di toodefine un Database di SQL Azure **tipo** di hello servizio collegato troppo**AzureSqlDatabase**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2819">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2819">Property</span></span> | <span data-ttu-id="54475-2820">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2820">Description</span></span> | <span data-ttu-id="54475-2821">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-2822">connectionString</span></span> |<span data-ttu-id="54475-2823">Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="54475-2824">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="54475-2825">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2825">JSON example</span></span>

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

<span data-ttu-id="54475-2826">Vedere l’articolo [Connettore di Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="54475-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="54475-2828">È possibile creare un servizio collegato di Azure SQL Data Warehouse e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2829">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2829">Linked service</span></span>
<span data-ttu-id="54475-2830">il servizio hello set toodefine un Data Warehouse di SQL Azure collegato **tipo** di hello servizio collegato troppo**AzureSqlDW**e specificare le seguenti proprietà in hello **typeProperties**sezione:</span><span class="sxs-lookup"><span data-stu-id="54475-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="54475-2831">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2831">Property</span></span> | <span data-ttu-id="54475-2832">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2832">Description</span></span> | <span data-ttu-id="54475-2833">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-2834">connectionString</span></span> |<span data-ttu-id="54475-2835">Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="54475-2836">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="54475-2837">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2837">JSON example</span></span>

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

<span data-ttu-id="54475-2838">Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="54475-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="54475-2839">SQL Server</span></span> 
<span data-ttu-id="54475-2840">Creare un servizio collegato SQL Server e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54475-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="54475-2841">Servizio collegato</span><span class="sxs-lookup"><span data-stu-id="54475-2841">Linked service</span></span>
<span data-ttu-id="54475-2842">Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="54475-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="54475-2843">Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="54475-2844">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.</span><span class="sxs-lookup"><span data-stu-id="54475-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="54475-2845">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2845">Property</span></span> | <span data-ttu-id="54475-2846">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2846">Description</span></span> | <span data-ttu-id="54475-2847">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2848">type</span><span class="sxs-lookup"><span data-stu-id="54475-2848">type</span></span> |<span data-ttu-id="54475-2849">proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="54475-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="54475-2850">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2850">Yes</span></span> |
| <span data-ttu-id="54475-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="54475-2851">connectionString</span></span> |<span data-ttu-id="54475-2852">Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="54475-2853">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2853">Yes</span></span> |
| <span data-ttu-id="54475-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="54475-2854">gatewayName</span></span> |<span data-ttu-id="54475-2855">Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="54475-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="54475-2856">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2856">Yes</span></span> |
| <span data-ttu-id="54475-2857">username</span><span class="sxs-lookup"><span data-stu-id="54475-2857">username</span></span> |<span data-ttu-id="54475-2858">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="54475-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="54475-2859">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="54475-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="54475-2860">No</span><span class="sxs-lookup"><span data-stu-id="54475-2860">No</span></span> |
| <span data-ttu-id="54475-2861">password</span><span class="sxs-lookup"><span data-stu-id="54475-2861">password</span></span> |<span data-ttu-id="54475-2862">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="54475-2863">No</span><span class="sxs-lookup"><span data-stu-id="54475-2863">No</span></span> |

<span data-ttu-id="54475-2864">È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):</span><span class="sxs-lookup"><span data-stu-id="54475-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="54475-2865">Esempio: JSON per l'uso dell'autenticazione SQL</span><span class="sxs-lookup"><span data-stu-id="54475-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="54475-2866">Esempio: JSON per l'uso dell'autenticazione Windows</span><span class="sxs-lookup"><span data-stu-id="54475-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="54475-2867">Se vengono specificati nome utente e password, gateway li utilizza hello tooimpersonate database di SQL Server on-premise toohello tooconnect account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="54475-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="54475-2868">In caso contrario, gateway si connetta toohello SQL Server direttamente con il contesto di sicurezza hello del Gateway (il relativo account di avvio).</span><span class="sxs-lookup"><span data-stu-id="54475-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="54475-2869">Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="54475-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="54475-2870">ATTIVITÀ DI TRASFORMAZIONE DEI DATI</span><span class="sxs-lookup"><span data-stu-id="54475-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="54475-2871">Attività</span><span class="sxs-lookup"><span data-stu-id="54475-2871">Activity</span></span> | <span data-ttu-id="54475-2872">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="54475-2873">Attività Hive di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="54475-2874">attività Hive di HDInsight in una pipeline di Data Factory Hello esegue query Hive per proprio conto o il cluster HDInsight basati su Windows o Linux su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="54475-2875">Attività Pig di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="54475-2876">attività Pig di HDInsight in una pipeline di Data Factory Hello esegue query Pig autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="54475-2877">Attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="54475-2878">attività MapReduce di HDInsight in una pipeline di Data Factory Hello esegue i programmi MapReduce autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="54475-2879">Attività di streaming di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="54475-2880">Hello attività Streaming di HDInsight in una pipeline di Data Factory esegue i programmi di Hadoop Streaming autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.</span><span class="sxs-lookup"><span data-stu-id="54475-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="54475-2881">Attività HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="54475-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="54475-2882">attività HDInsight Spark in una pipeline di Data Factory Hello esegue programmi Spark nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54475-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="54475-2883">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="54475-2884">Servizio per analitica predittiva web di Azure consente di Data Factory è tooeasily creare pipeline che utilizzano una versione pubblicata di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="54475-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="54475-2885">Utilizza hello attività di esecuzione del Batch in una pipeline di Data Factory di Azure, è possibile richiamare un stime di toomake servizio web Machine Learning sui dati hello in batch.</span><span class="sxs-lookup"><span data-stu-id="54475-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="54475-2886">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="54475-2887">Nel corso del tempo, modelli predittivi di hello in hello Machine Learning esperimenti punteggio necessario toobe ripetere il training utilizzando il nuovo set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="54475-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="54475-2888">Dopo avere completato con ripetizione di training, si desidera hello tooupdate punteggio servizio web con hello Training modello di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="54475-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="54475-2889">È possibile utilizzare servizio web di attività di aggiornamento risorsa tooupdate hello hello con hello appena training del modello.</span><span class="sxs-lookup"><span data-stu-id="54475-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="54475-2890">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="54475-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="54475-2891">È possibile utilizzare l'attività di Stored Procedure hello in tooinvoke di pipeline una stored procedure in uno dei seguenti archivi dati hello una Data Factory: Database SQL di Azure, Azure SQL Data Warehouse, il Database di SQL Server nell'organizzazione o una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="54475-2892">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="54475-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="54475-2893">L'attività U-SQL di Data Lake Analytics esegue uno script U-SQL in un cluster di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="54475-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="54475-2894">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="54475-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="54475-2895">Se è necessario tootransform dati in modo che non è supportato da Data Factory, è possibile creare un'attività personalizzata con la logica di elaborazione dei dati e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="54475-2896">È possibile configurare hello personalizzato .NET attività toorun utilizzando un servizio Azure Batch o un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54475-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="54475-2897">Attività Hive di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="54475-2898">È possibile specificare le proprietà in una definizione del formato JSON dell'attività Hive seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="54475-2899">deve essere di proprietà del tipo Hello attività hello: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="54475-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="54475-2900">È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-2901">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightHive attività:</span><span class="sxs-lookup"><span data-stu-id="54475-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="54475-2902">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2902">Property</span></span> | <span data-ttu-id="54475-2903">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2903">Description</span></span> | <span data-ttu-id="54475-2904">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2905">script</span><span class="sxs-lookup"><span data-stu-id="54475-2905">script</span></span> |<span data-ttu-id="54475-2906">Specificare hello Hive script inline</span><span class="sxs-lookup"><span data-stu-id="54475-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="54475-2907">No</span><span class="sxs-lookup"><span data-stu-id="54475-2907">No</span></span> |
| <span data-ttu-id="54475-2908">script path</span><span class="sxs-lookup"><span data-stu-id="54475-2908">script path</span></span> |<span data-ttu-id="54475-2909">Hello archivio Hive script in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file.</span><span class="sxs-lookup"><span data-stu-id="54475-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="54475-2910">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="54475-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="54475-2911">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2911">Both cannot be used together.</span></span> <span data-ttu-id="54475-2912">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="54475-2913">No</span><span class="sxs-lookup"><span data-stu-id="54475-2913">No</span></span> |
| <span data-ttu-id="54475-2914">defines</span><span class="sxs-lookup"><span data-stu-id="54475-2914">defines</span></span> |<span data-ttu-id="54475-2915">Specificare i parametri come coppie chiave/valore per il riferimento all'interno dello script Hive hello utilizzando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="54475-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="54475-2916">No</span><span class="sxs-lookup"><span data-stu-id="54475-2916">No</span></span> |

<span data-ttu-id="54475-2917">Queste proprietà sono toohello specifica attività Hive.</span><span class="sxs-lookup"><span data-stu-id="54475-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="54475-2918">Altre proprietà (all'esterno di sezione typeProperties hello) sono supportati per tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="54475-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="54475-2919">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2919">JSON example</span></span>
<span data-ttu-id="54475-2920">Hello JSON seguente definisce un'attività Hive di HDInsight in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="54475-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="54475-2921">Per altre informazioni, vedere [Attività Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="54475-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="54475-2922">Attività Pig di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="54475-2923">È possibile specificare le proprietà in una definizione del formato JSON dell'attività Pig seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="54475-2924">deve essere di proprietà del tipo Hello attività hello: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="54475-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="54475-2925">È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-2926">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightPig attività:</span><span class="sxs-lookup"><span data-stu-id="54475-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="54475-2927">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2927">Property</span></span> | <span data-ttu-id="54475-2928">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2928">Description</span></span> | <span data-ttu-id="54475-2929">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2930">script</span><span class="sxs-lookup"><span data-stu-id="54475-2930">script</span></span> |<span data-ttu-id="54475-2931">Specificare hello Pig script inline</span><span class="sxs-lookup"><span data-stu-id="54475-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="54475-2932">No</span><span class="sxs-lookup"><span data-stu-id="54475-2932">No</span></span> |
| <span data-ttu-id="54475-2933">script path</span><span class="sxs-lookup"><span data-stu-id="54475-2933">script path</span></span> |<span data-ttu-id="54475-2934">Archiviare lo script Pig hello in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file.</span><span class="sxs-lookup"><span data-stu-id="54475-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="54475-2935">Usare la proprietà "script" o "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="54475-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="54475-2936">Non è possibile usare entrambe le proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2936">Both cannot be used together.</span></span> <span data-ttu-id="54475-2937">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="54475-2938">No</span><span class="sxs-lookup"><span data-stu-id="54475-2938">No</span></span> |
| <span data-ttu-id="54475-2939">defines</span><span class="sxs-lookup"><span data-stu-id="54475-2939">defines</span></span> |<span data-ttu-id="54475-2940">Specificare i parametri come coppie chiave/valore per il riferimento all'interno di uno script Pig hello</span><span class="sxs-lookup"><span data-stu-id="54475-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="54475-2941">No</span><span class="sxs-lookup"><span data-stu-id="54475-2941">No</span></span> |

<span data-ttu-id="54475-2942">Queste proprietà sono toohello specifica attività Pig.</span><span class="sxs-lookup"><span data-stu-id="54475-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="54475-2943">Altre proprietà (all'esterno di sezione typeProperties hello) sono supportati per tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="54475-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="54475-2944">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2944">JSON example</span></span>

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

<span data-ttu-id="54475-2945">Per altre informazioni, vedere [Attività Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="54475-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="54475-2946">Attività MapReduce di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="54475-2947">È possibile specificare hello seguenti proprietà in una definizione del formato JSON dell'attività MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54475-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="54475-2948">deve essere di proprietà del tipo Hello attività hello: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="54475-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="54475-2949">È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-2950">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightMapReduce attività:</span><span class="sxs-lookup"><span data-stu-id="54475-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="54475-2951">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2951">Property</span></span> | <span data-ttu-id="54475-2952">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2952">Description</span></span> | <span data-ttu-id="54475-2953">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="54475-2954">jarLinkedService</span></span> | <span data-ttu-id="54475-2955">Nome di hello collegato del servizio di archiviazione di Azure che contiene i file JAR hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="54475-2956">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2956">Yes</span></span> |
| <span data-ttu-id="54475-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="54475-2957">jarFilePath</span></span> | <span data-ttu-id="54475-2958">Percorso file JAR di toohello in hello archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="54475-2959">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2959">Yes</span></span> | 
| <span data-ttu-id="54475-2960">className</span><span class="sxs-lookup"><span data-stu-id="54475-2960">className</span></span> | <span data-ttu-id="54475-2961">Nome della classe principale di hello in file JAR hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="54475-2962">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-2962">Yes</span></span> | 
| <span data-ttu-id="54475-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="54475-2963">arguments</span></span> | <span data-ttu-id="54475-2964">Un elenco di argomenti delimitato da virgole per il programma MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="54475-2965">In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="54475-2966">toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni)</span><span class="sxs-lookup"><span data-stu-id="54475-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="54475-2967">No</span><span class="sxs-lookup"><span data-stu-id="54475-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="54475-2968">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="54475-2969">Per altre informazioni, vedere [Attività MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="54475-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="54475-2970">Attività di streaming di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="54475-2971">È possibile specificare le proprietà in una definizione del formato JSON dell'attività di Streaming Hadoop seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="54475-2972">deve essere di proprietà del tipo Hello attività hello: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="54475-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="54475-2973">È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-2974">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightStreaming attività:</span><span class="sxs-lookup"><span data-stu-id="54475-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="54475-2975">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-2975">Property</span></span> | <span data-ttu-id="54475-2976">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="54475-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="54475-2977">mapper</span></span> | <span data-ttu-id="54475-2978">Nome del mapper hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="54475-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="54475-2979">Nell'esempio hello cat.exe è mapper hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="54475-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="54475-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="54475-2980">reducer</span></span> | <span data-ttu-id="54475-2981">Nome del file eseguibile del reducer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="54475-2982">Nell'esempio hello wc.exe è file eseguibile del reducer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="54475-2983">input</span><span class="sxs-lookup"><span data-stu-id="54475-2983">input</span></span> | <span data-ttu-id="54475-2984">File di input (incluso percorso) per il mapper hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="54475-2985">Nell'esempio hello: "//adfsample @<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample è il contenitore di blob hello, esempio/data/Gutenberg è la cartella hello e davinci.txt è blob hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="54475-2986">output</span><span class="sxs-lookup"><span data-stu-id="54475-2986">output</span></span> | <span data-ttu-id="54475-2987">File di output (incluso percorso) per riduttore hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="54475-2988">output di Hello del processo Hadoop Streaming hello viene scritto toohello percorso specificato per questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="54475-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="54475-2989">filePaths</span></span> | <span data-ttu-id="54475-2990">Percorsi per gli eseguibili del mapper e del reducer hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="54475-2991">Nell'esempio hello: "adfsample/example/apps/wc.exe", adfsample è il contenitore di blob hello, example/apps è la cartella hello e wc.exe è hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="54475-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="54475-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="54475-2992">fileLinkedService</span></span> | <span data-ttu-id="54475-2993">Servizio collegato di archiviazione Azure che rappresenta l'archiviazione di Azure che contiene file hello specificati nella sezione filePaths hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="54475-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="54475-2994">arguments</span></span> | <span data-ttu-id="54475-2995">Un elenco di argomenti delimitato da virgole per il programma MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="54475-2996">In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="54475-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="54475-2997">toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni)</span><span class="sxs-lookup"><span data-stu-id="54475-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="54475-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="54475-2998">getDebugInfo</span></span> | <span data-ttu-id="54475-2999">Un elemento facoltativo.</span><span class="sxs-lookup"><span data-stu-id="54475-2999">An optional element.</span></span> <span data-ttu-id="54475-3000">Quando si imposta tooFailure, hello registri vengono scaricati solo in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="54475-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="54475-3001">Quando si imposta tooAll, i log vengono sempre scaricati indipendentemente lo stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="54475-3002">È necessario specificare un set di dati di output di hello attività di Streaming di Hadoop per hello **restituisce** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="54475-3003">Questo set di dati può essere solo un dummy set di dati è necessario toodrive hello pipeline pianificazione (oraria, giornaliera, e così via.).</span><span class="sxs-lookup"><span data-stu-id="54475-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="54475-3004">Se l'attività hello non accetta un input, è possibile ignorare specificando un set di dati di input per l'attività hello per hello **input** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="54475-3005">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3005">JSON example</span></span>

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

<span data-ttu-id="54475-3006">Per altre informazioni, vedere l'argomento relativo all'[attività Hadoop Streaming](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="54475-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="54475-3007">Attività Spark di HDInsight</span><span class="sxs-lookup"><span data-stu-id="54475-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="54475-3008">È possibile specificare le proprietà in una definizione del formato JSON dell'attività Spark seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="54475-3009">deve essere di proprietà del tipo Hello attività hello: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="54475-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="54475-3010">È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-3011">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightSpark attività:</span><span class="sxs-lookup"><span data-stu-id="54475-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="54475-3012">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3012">Property</span></span> | <span data-ttu-id="54475-3013">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3013">Description</span></span> | <span data-ttu-id="54475-3014">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="54475-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="54475-3015">rootPath</span></span> | <span data-ttu-id="54475-3016">contenitore di Blob di Azure Hello e della cartella che contiene file Spark hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="54475-3017">nome del file Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="54475-3018">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3018">Yes</span></span> |
| <span data-ttu-id="54475-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="54475-3019">entryFilePath</span></span> | <span data-ttu-id="54475-3020">Cartella radice di percorso relativo toohello di hello Spark codice o del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="54475-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="54475-3021">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3021">Yes</span></span> |
| <span data-ttu-id="54475-3022">className</span><span class="sxs-lookup"><span data-stu-id="54475-3022">className</span></span> | <span data-ttu-id="54475-3023">Classe principale Java/Spark dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="54475-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="54475-3024">No</span><span class="sxs-lookup"><span data-stu-id="54475-3024">No</span></span> | 
| <span data-ttu-id="54475-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="54475-3025">arguments</span></span> | <span data-ttu-id="54475-3026">Un elenco di programmi di Spark toohello gli argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="54475-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="54475-3027">No</span><span class="sxs-lookup"><span data-stu-id="54475-3027">No</span></span> | 
| <span data-ttu-id="54475-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="54475-3028">proxyUser</span></span> | <span data-ttu-id="54475-3029">programma di Hello utente account tooimpersonate tooexecute hello Spark</span><span class="sxs-lookup"><span data-stu-id="54475-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="54475-3030">No</span><span class="sxs-lookup"><span data-stu-id="54475-3030">No</span></span> | 
| <span data-ttu-id="54475-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="54475-3031">sparkConfig</span></span> | <span data-ttu-id="54475-3032">Proprietà di configurazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="54475-3032">Spark configuration properties.</span></span> | <span data-ttu-id="54475-3033">No</span><span class="sxs-lookup"><span data-stu-id="54475-3033">No</span></span> | 
| <span data-ttu-id="54475-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="54475-3034">getDebugInfo</span></span> | <span data-ttu-id="54475-3035">Specifica quando i file di log Spark hello toohello copiato archiviazione di Azure usati dal cluster HDInsight (o) specificato da sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="54475-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="54475-3036">Valori consentiti: None, Always o Failure.</span><span class="sxs-lookup"><span data-stu-id="54475-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="54475-3037">Valore predefinito: None.</span><span class="sxs-lookup"><span data-stu-id="54475-3037">Default value: None.</span></span> | <span data-ttu-id="54475-3038">No</span><span class="sxs-lookup"><span data-stu-id="54475-3038">No</span></span> | 
| <span data-ttu-id="54475-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="54475-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="54475-3040">servizio collegato di archiviazione di Azure che contiene i registri, le dipendenze e hello Spark processo file Hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="54475-3041">Se non si specifica un valore per questa proprietà, viene utilizzata l'archiviazione di hello associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54475-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="54475-3042">No</span><span class="sxs-lookup"><span data-stu-id="54475-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="54475-3043">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3043">JSON example</span></span>

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
<span data-ttu-id="54475-3044">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="54475-3044">Note hello following points:</span></span> 

- <span data-ttu-id="54475-3045">Hello **tipo** impostata troppo**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="54475-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="54475-3046">Hello **rootPath** è troppo**adfspark\\pyFiles** dove adfspark è il contenitore di Blob di Azure hello e pyFiles è cartella correttamente in tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="54475-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="54475-3047">In questo esempio hello archiviazione Blob di Azure è hello uno associato al cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="54475-3048">È possibile caricare tooa file hello archiviazione di Azure diversi.</span><span class="sxs-lookup"><span data-stu-id="54475-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="54475-3049">In tal caso, creare un toolink di servizio collegato di archiviazione di Azure che data factory toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="54475-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="54475-3050">Quindi, specificare il nome di hello del servizio hello collegato come valore per hello **sparkJobLinkedService** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="54475-3051">Vedere [le proprietà dell'attività di Spark](#spark-activity-properties) per informazioni dettagliate su questa proprietà e altre proprietà supportate dall'attività Spark hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="54475-3052">Hello **entryFilePath** è impostato toohello **test.py**, ossia file python hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="54475-3053">Hello **getDebugInfo** impostata troppo**sempre**, ovvero i file di log hello vengono sempre generati (esito positivo o negativo).</span><span class="sxs-lookup"><span data-stu-id="54475-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="54475-3054">È consigliabile non impostare tooAlways questa proprietà in un ambiente di produzione a meno che non si sta risolvendo un problema.</span><span class="sxs-lookup"><span data-stu-id="54475-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="54475-3055">Hello **restituisce** sezione ha un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="54475-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="54475-3056">Anche se il programma di spark hello non genera alcun output, è necessario specificare un set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="54475-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="54475-3057">pianificazione di hello unità per set di dati di output Hello per pipeline hello (oraria, giornaliera, e così via.).</span><span class="sxs-lookup"><span data-stu-id="54475-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="54475-3058">Per ulteriori informazioni sulle attività hello, vedere [attività Spark](data-factory-spark.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="54475-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="54475-3059">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="54475-3060">È possibile specificare le proprietà in una definizione di Azure ML Batch esecuzione attività JSON seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="54475-3061">deve essere di proprietà del tipo Hello attività hello: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="54475-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="54475-3062">È necessario creare un Azure Machine Learning innanzitutto il servizio collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-3063">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooAzureMLBatchExecution attività:</span><span class="sxs-lookup"><span data-stu-id="54475-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="54475-3064">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3064">Property</span></span> | <span data-ttu-id="54475-3065">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3065">Description</span></span> | <span data-ttu-id="54475-3066">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="54475-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="54475-3067">webServiceInput</span></span> | <span data-ttu-id="54475-3068">Hello toobe di set di dati passato come input per hello servizio web di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="54475-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="54475-3069">Questo set di dati deve essere incluso anche in input hello per attività hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="54475-3070">Usare webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="54475-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="54475-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="54475-3071">webServiceInputs</span></span> | <span data-ttu-id="54475-3072">Specificare i set di dati toobe passate come input per hello servizio web di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="54475-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="54475-3073">Se il servizio web hello accetta più input, è possibile utilizzare proprietà webServiceInputs hello anziché proprietà WebServiceInputActivity hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="54475-3074">Set di dati che fanno riferimento hello **webServiceInputs** deve essere incluso anche in attività hello **input**.</span><span class="sxs-lookup"><span data-stu-id="54475-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="54475-3075">Usare webServiceInput o webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="54475-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="54475-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="54475-3076">webServiceOutputs</span></span> | <span data-ttu-id="54475-3077">Hello set di dati che vengono assegnati come output per il servizio web di Azure ML hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="54475-3078">servizio web Hello restituisce i dati di output in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="54475-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="54475-3079">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3079">Yes</span></span> | 
<span data-ttu-id="54475-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="54475-3080">globalParameters</span></span> | <span data-ttu-id="54475-3081">Specificare i valori per parametri del servizio web hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="54475-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="54475-3082">No</span><span class="sxs-lookup"><span data-stu-id="54475-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="54475-3083">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3083">JSON example</span></span>
<span data-ttu-id="54475-3084">In questo esempio, attività hello presenta dataset hello **MLSqlInput** come input e **MLSqlOutput** come output di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="54475-3085">Hello **MLSqlInput** viene passato come un servizio web di input toohello da utilizzando hello **WebServiceInputActivity** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="54475-3086">Hello **MLSqlOutput** viene passato come un servizio Web toohello di output da utilizzando hello **webserviceoutputs della** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="54475-3087">Nell'esempio hello JSON hello distribuito Azure Machine Learning Web servizio utilizza un lettore e un writer modulo tooread/scrittura di dati da / tooan Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="54475-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="54475-3088">Questo servizio Web espone hello seguenti quattro parametri: nome del server, nome del Database, nome Server dell'account utente e password dell'account utente Server di Database.</span><span class="sxs-lookup"><span data-stu-id="54475-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="54475-3089">Solo input e output dell'attività AzureMLBatchExecution hello possono essere passati come parametri toohello servizio Web.</span><span class="sxs-lookup"><span data-stu-id="54475-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="54475-3090">Ad esempio, in hello sopra frammento di codice JSON, MLSqlInput è un input toohello AzureMLBatchExecution attività, che viene passato come un input toohello servizio Web tramite un parametro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="54475-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="54475-3091">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54475-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="54475-3092">È possibile specificare hello seguenti proprietà in una definizione di Azure ML aggiornamento risorsa attività JSON.</span><span class="sxs-lookup"><span data-stu-id="54475-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="54475-3093">deve essere di proprietà del tipo Hello attività hello: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="54475-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="54475-3094">È necessario creare un Azure Machine Learning innanzitutto il servizio collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-3095">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooAzureMLUpdateResource attività:</span><span class="sxs-lookup"><span data-stu-id="54475-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="54475-3096">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3096">Property</span></span> | <span data-ttu-id="54475-3097">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3097">Description</span></span> | <span data-ttu-id="54475-3098">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="54475-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="54475-3099">trainedModelName</span></span> | <span data-ttu-id="54475-3100">Nome di hello ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="54475-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="54475-3101">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3101">Yes</span></span> |  
<span data-ttu-id="54475-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="54475-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="54475-3103">Set di dati puntamento toohello iLearner file restituito dall'operazione di ripetizione di training hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="54475-3104">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="54475-3105">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3105">JSON example</span></span>
<span data-ttu-id="54475-3106">Hello pipeline dispone di due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="54475-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="54475-3107">l'attività di esecuzione Batch di Azure ML Hello accetta i dati di training hello come input e genera un file iLearner come output.</span><span class="sxs-lookup"><span data-stu-id="54475-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="54475-3108">attività Hello richiama il servizio web di formazione hello (esperimento di training esposta come servizio web) con input hello i dati di training e riceve file ilearner hello dal servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="54475-3109">placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.</span><span class="sxs-lookup"><span data-stu-id="54475-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="54475-3110">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="54475-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="54475-3111">È possibile specificare le proprietà in una definizione del formato JSON dell'attività U-SQL seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="54475-3112">deve essere di proprietà del tipo Hello attività hello: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="54475-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="54475-3113">È necessario creare un servizio di Azure Data Lake Analitica collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-3114">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di attività tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="54475-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="54475-3115">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3115">Property</span></span> | <span data-ttu-id="54475-3116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3116">Description</span></span> | <span data-ttu-id="54475-3117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="54475-3118">scriptPath</span></span> |<span data-ttu-id="54475-3119">Toofolder percorso che contiene lo script hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="54475-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="54475-3120">Nome del file hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54475-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="54475-3121">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="54475-3121">No (if you use script)</span></span> |
| <span data-ttu-id="54475-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="54475-3122">scriptLinkedService</span></span> |<span data-ttu-id="54475-3123">Servizio collegato che si collega archiviazione hello che contiene una data factory di hello script toohello</span><span class="sxs-lookup"><span data-stu-id="54475-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="54475-3124">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="54475-3124">No (if you use script)</span></span> |
| <span data-ttu-id="54475-3125">script</span><span class="sxs-lookup"><span data-stu-id="54475-3125">script</span></span> |<span data-ttu-id="54475-3126">Specificare lo script inline anziché scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="54475-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="54475-3127">Ad esempio: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="54475-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="54475-3128">No (se si usano le proprietà scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="54475-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="54475-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="54475-3129">degreeOfParallelism</span></span> |<span data-ttu-id="54475-3130">numero massimo di Hello di nodi utilizzati contemporaneamente processo hello toorun.</span><span class="sxs-lookup"><span data-stu-id="54475-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="54475-3131">No</span><span class="sxs-lookup"><span data-stu-id="54475-3131">No</span></span> |
| <span data-ttu-id="54475-3132">priority</span><span class="sxs-lookup"><span data-stu-id="54475-3132">priority</span></span> |<span data-ttu-id="54475-3133">Determina innanzitutto quali processi, tra tutti quelli accodati devono essere toorun selezionato.</span><span class="sxs-lookup"><span data-stu-id="54475-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="54475-3134">Hello hello numero inferiore, priorità più alta hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="54475-3135">No</span><span class="sxs-lookup"><span data-stu-id="54475-3135">No</span></span> |
| <span data-ttu-id="54475-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="54475-3136">parameters</span></span> |<span data-ttu-id="54475-3137">Parametri per hello U-SQL script</span><span class="sxs-lookup"><span data-stu-id="54475-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="54475-3138">No</span><span class="sxs-lookup"><span data-stu-id="54475-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="54475-3139">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3139">JSON example</span></span>

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

<span data-ttu-id="54475-3140">Per altre informazioni, vedere [Attività Data Lake Analytics U-SQL](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="54475-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="54475-3141">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="54475-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="54475-3142">È possibile specificare hello seguenti proprietà in una definizione di Stored Procedure formato JSON dell'attività.</span><span class="sxs-lookup"><span data-stu-id="54475-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="54475-3143">deve essere di proprietà del tipo Hello attività hello: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="54475-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="54475-3144">È necessario creare un uno dei seguenti servizi collegati hello e specificare il nome di hello del servizio hello collegato come un valore per hello **linkedServiceName** proprietà:</span><span class="sxs-lookup"><span data-stu-id="54475-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="54475-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="54475-3145">SQL Server</span></span> 
- <span data-ttu-id="54475-3146">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="54475-3146">Azure SQL Database</span></span>
- <span data-ttu-id="54475-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="54475-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="54475-3148">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooSqlServerStoredProcedure attività:</span><span class="sxs-lookup"><span data-stu-id="54475-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="54475-3149">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3149">Property</span></span> | <span data-ttu-id="54475-3150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3150">Description</span></span> | <span data-ttu-id="54475-3151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54475-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="54475-3152">storedProcedureName</span></span> |<span data-ttu-id="54475-3153">Specificare il nome di hello della routine di hello archiviato nel database di SQL Azure hello o Azure SQL Data Warehouse è rappresentato dal servizio hello collegato che Usa tabella di output di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="54475-3154">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3154">Yes</span></span> |
| <span data-ttu-id="54475-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="54475-3155">storedProcedureParameters</span></span> |<span data-ttu-id="54475-3156">Specificare i valori dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="54475-3157">Se è necessario toopass null per un parametro, utilizzare la sintassi di hello: "param1": null (lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="54475-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="54475-3158">Vedere hello seguente toolearn esempio sull'utilizzo di questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="54475-3159">No</span><span class="sxs-lookup"><span data-stu-id="54475-3159">No</span></span> |

<span data-ttu-id="54475-3160">Se si specifica un set di dati di input, deve essere disponibile (in stato "Pronto") per hello stored procedure toorun di attività.</span><span class="sxs-lookup"><span data-stu-id="54475-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="54475-3161">set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro.</span><span class="sxs-lookup"><span data-stu-id="54475-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="54475-3162">È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="54475-3163">È necessario specificare un set di dati di output per un'attività della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="54475-3164">Set di dati di output specifica hello **pianificazione** per hello attività stored procedure (ogni ora, settimanale, mensile, ecc.).</span><span class="sxs-lookup"><span data-stu-id="54475-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="54475-3165">Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="54475-3166">Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="54475-3167">Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="54475-3168">È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="54475-3169">In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio**, che viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure.</span><span class="sxs-lookup"><span data-stu-id="54475-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="54475-3170">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3170">JSON example</span></span>

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

<span data-ttu-id="54475-3171">Per altre informazioni, vedere [Attività stored procedure](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="54475-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="54475-3172">Attività personalizzata .NET</span><span class="sxs-lookup"><span data-stu-id="54475-3172">.NET custom activity</span></span>
<span data-ttu-id="54475-3173">È possibile specificare le proprietà in un'attività personalizzata .NET definizione JSON seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="54475-3174">deve essere di proprietà del tipo Hello attività hello: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="54475-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="54475-3175">È necessario creare un servizio collegato di HDInsight di Azure o un Batch di Azure collegato del servizio e specificare il nome di hello del servizio collegato hello come valore per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="54475-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="54475-3176">salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooDotNetActivity attività:</span><span class="sxs-lookup"><span data-stu-id="54475-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="54475-3177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54475-3177">Property</span></span> | <span data-ttu-id="54475-3178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54475-3178">Description</span></span> | <span data-ttu-id="54475-3179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54475-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="54475-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="54475-3180">AssemblyName</span></span> | <span data-ttu-id="54475-3181">Nome dell'assembly hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3181">Name of hello assembly.</span></span> <span data-ttu-id="54475-3182">Nell'esempio hello è: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="54475-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="54475-3183">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3183">Yes</span></span> |
| <span data-ttu-id="54475-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="54475-3184">EntryPoint</span></span> |<span data-ttu-id="54475-3185">Nome della classe hello che implementa l'interfaccia IDotNetActivity hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="54475-3186">Nell'esempio hello è: **MyDotNetActivityNS.MyDotNetActivity** dove MyDotNetActivityNS è lo spazio dei nomi hello e MyDotNetActivity è la classe hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="54475-3187">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3187">Yes</span></span> | 
| <span data-ttu-id="54475-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="54475-3188">PackageLinkedService</span></span> | <span data-ttu-id="54475-3189">Nome del servizio collegato di archiviazione di Azure che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="54475-3190">Nell'esempio hello è: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="54475-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="54475-3191">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3191">Yes</span></span> |
| <span data-ttu-id="54475-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="54475-3192">PackageFile</span></span> | <span data-ttu-id="54475-3193">Nome del file zip hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3193">Name of hello zip file.</span></span> <span data-ttu-id="54475-3194">Nell'esempio hello è: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="54475-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="54475-3195">Sì</span><span class="sxs-lookup"><span data-stu-id="54475-3195">Yes</span></span> |
| <span data-ttu-id="54475-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="54475-3196">extendedProperties</span></span> | <span data-ttu-id="54475-3197">Proprietà estese che è possibile definire e passare al codice .NET toohello.</span><span class="sxs-lookup"><span data-stu-id="54475-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="54475-3198">In questo esempio hello **SliceStart** variabile è impostata un valore tooa in base alla variabile di sistema SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="54475-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="54475-3199">No</span><span class="sxs-lookup"><span data-stu-id="54475-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="54475-3200">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="54475-3200">JSON example</span></span>

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

<span data-ttu-id="54475-3201">Per altre informazioni, vedere l'articolo relativo all'[uso delle attività personalizzate in Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="54475-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54475-3202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54475-3202">Next Steps</span></span>
<span data-ttu-id="54475-3203">Vedere hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="54475-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="54475-3204">Esercitazione: Creare una pipeline con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54475-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="54475-3205">Esercitazione: Creare una pipeline con un'attività di Hive</span><span class="sxs-lookup"><span data-stu-id="54475-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)