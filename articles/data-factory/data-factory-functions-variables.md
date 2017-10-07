---
title: aaaData Factory funzioni e variabili di sistema | Documenti Microsoft
description: Fornisce un elenco delle funzioni e delle variabili di sistema di Azure Data Factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="e9ae9-103">Azure Data Factory - Funzioni e variabili di sistema</span><span class="sxs-lookup"><span data-stu-id="e9ae9-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="e9ae9-104">In questo articolo vengono fornite informazioni sulle funzioni e le variabili supportate da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="e9ae9-105">Variabili di sistema di Data Factory</span><span class="sxs-lookup"><span data-stu-id="e9ae9-105">Data Factory system variables</span></span>
| <span data-ttu-id="e9ae9-106">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="e9ae9-106">Variable Name</span></span> | <span data-ttu-id="e9ae9-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9ae9-107">Description</span></span> | <span data-ttu-id="e9ae9-108">Ambito dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="e9ae9-108">Object Scope</span></span> | <span data-ttu-id="e9ae9-109">Ambito JSON e casi d'uso</span><span class="sxs-lookup"><span data-stu-id="e9ae9-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9ae9-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="e9ae9-110">WindowStart</span></span> |<span data-ttu-id="e9ae9-111">Inizio dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="e9ae9-112">attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-112">activity</span></span> |<ol><li><span data-ttu-id="e9ae9-113">Definizione delle query di selezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-113">Specify data selection queries.</span></span> <span data-ttu-id="e9ae9-114">Vedere connettore articoli a cui fa riferimento in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="e9ae9-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="e9ae9-115">WindowEnd</span></span> |<span data-ttu-id="e9ae9-116">Fine dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="e9ae9-117">attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-117">activity</span></span> |<span data-ttu-id="e9ae9-118">uguale a WindowStart.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-118">same as WindowStart.</span></span> |
| <span data-ttu-id="e9ae9-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="e9ae9-119">SliceStart</span></span> |<span data-ttu-id="e9ae9-120">Inizio dell'intervallo di tempo relativo alla sezione di dati in fase di produzione</span><span class="sxs-lookup"><span data-stu-id="e9ae9-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="e9ae9-121">attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-121">activity</span></span><br/><span data-ttu-id="e9ae9-122">attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-122">dataset</span></span> |<ol><li><span data-ttu-id="e9ae9-123">Definizione di nomi di file e percorsi di cartelle dinamici durante l'uso dell'[archivio BLOB di Azure](data-factory-azure-blob-connector.md) e dei [set di dati del file system](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="e9ae9-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="e9ae9-124">Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="e9ae9-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="e9ae9-125">SliceEnd</span></span> |<span data-ttu-id="e9ae9-126">Fine dell'intervallo di tempo relativo alla sezione di dati corrente.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="e9ae9-127">attività</span><span class="sxs-lookup"><span data-stu-id="e9ae9-127">activity</span></span><br/><span data-ttu-id="e9ae9-128">dataset</span><span class="sxs-lookup"><span data-stu-id="e9ae9-128">dataset</span></span> |<span data-ttu-id="e9ae9-129">uguale a SliceStart.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="e9ae9-130">Attualmente è necessario tale hello pianificare hello specificato nella data factory di attività corrisponde esattamente alla pianificazione di hello specificata nella disponibilità di dataset di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="e9ae9-131">Pertanto, WindowStart, WindowEnd e SliceStart e SliceEnd sempre eseguito il mapping toohello stesso tempo periodo e una sezione singolo output.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="e9ae9-132">Esempio di uso di una variabile di sistema</span><span class="sxs-lookup"><span data-stu-id="e9ae9-132">Example for using a system variable</span></span>
<span data-ttu-id="e9ae9-133">Nel seguente esempio, anno, mese, giorno e ora di hello **SliceStart** vengono estratti in variabili distinte che vengono utilizzate da **folderPath** e **fileName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="e9ae9-134">Funzioni di Data Factory</span><span class="sxs-lookup"><span data-stu-id="e9ae9-134">Data Factory functions</span></span>
<span data-ttu-id="e9ae9-135">È possibile utilizzare funzioni nella data factory e le variabili di sistema per hello seguenti scopi:</span><span class="sxs-lookup"><span data-stu-id="e9ae9-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="e9ae9-136">Specifica di query di selezione dei dati (vedere connettore articoli a cui fa riferimento hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="e9ae9-137">Hello tooinvoke sintassi è una funzione di data factory:  **$$ <function>**  per query di selezione dei dati e altre proprietà in attività hello e set di dati.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="e9ae9-138">Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="e9ae9-139">La sintassi $$ non è necessaria per definire le espressioni delle dipendenze di input.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="e9ae9-140">Nel seguente esempio, hello **sqlReaderQuery** proprietà in un file JSON viene assegnato il valore di tooa restituito da hello `Text.Format` (funzione).</span><span class="sxs-lookup"><span data-stu-id="e9ae9-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="e9ae9-141">In questo esempio utilizza inoltre una variabile di sistema denominata **WindowStart**, che rappresenta l'ora di inizio hello della finestra di esecuzione dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="e9ae9-142">Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: aa e aaaa.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="e9ae9-143">Funzioni</span><span class="sxs-lookup"><span data-stu-id="e9ae9-143">Functions</span></span>
<span data-ttu-id="e9ae9-144">le tabelle seguenti Hello Elenca tutte le funzioni hello nella Data Factory di Azure:</span><span class="sxs-lookup"><span data-stu-id="e9ae9-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="e9ae9-145">Categoria</span><span class="sxs-lookup"><span data-stu-id="e9ae9-145">Category</span></span> | <span data-ttu-id="e9ae9-146">Funzione</span><span class="sxs-lookup"><span data-stu-id="e9ae9-146">Function</span></span> | <span data-ttu-id="e9ae9-147">Parametri</span><span class="sxs-lookup"><span data-stu-id="e9ae9-147">Parameters</span></span> | <span data-ttu-id="e9ae9-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9ae9-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9ae9-149">Time</span><span class="sxs-lookup"><span data-stu-id="e9ae9-149">Time</span></span> |<span data-ttu-id="e9ae9-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-150">AddHours(X,Y)</span></span> |<span data-ttu-id="e9ae9-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="e9ae9-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-152">Y: int</span></span> |<span data-ttu-id="e9ae9-153">Aggiunge Y ore toohello momento X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="e9ae9-154">Esempio: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e9ae9-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="e9ae9-155">Time</span><span class="sxs-lookup"><span data-stu-id="e9ae9-155">Time</span></span> |<span data-ttu-id="e9ae9-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="e9ae9-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="e9ae9-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-158">Y: int</span></span> |<span data-ttu-id="e9ae9-159">Aggiunge Y minuti tooX.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="e9ae9-160">Esempio: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e9ae9-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="e9ae9-161">Time</span><span class="sxs-lookup"><span data-stu-id="e9ae9-161">Time</span></span> |<span data-ttu-id="e9ae9-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-162">StartOfHour(X)</span></span> |<span data-ttu-id="e9ae9-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-163">X: Datetime</span></span> |<span data-ttu-id="e9ae9-164">Ottiene hello avvio per ora hello rappresentato dal componente di ora hello di X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="e9ae9-165">Esempio: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e9ae9-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="e9ae9-166">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-166">Date</span></span> |<span data-ttu-id="e9ae9-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-167">AddDays(X,Y)</span></span> |<span data-ttu-id="e9ae9-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-168">X: DateTime</span></span><br/><br/><span data-ttu-id="e9ae9-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-169">Y: int</span></span> |<span data-ttu-id="e9ae9-170">Aggiunge Y giorni tooX.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="e9ae9-171">Esempio: 9/15/2013 12:00:00 PM + 2 giorni = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="e9ae9-172">È possibile anche sottrarre giorni specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e9ae9-173">Esempio: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e9ae9-174">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-174">Date</span></span> |<span data-ttu-id="e9ae9-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="e9ae9-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-176">X: DateTime</span></span><br/><br/><span data-ttu-id="e9ae9-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-177">Y: int</span></span> |<span data-ttu-id="e9ae9-178">Aggiunge Y mesi tooX.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="e9ae9-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="e9ae9-180">È possibile anche sottrarre mesi specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e9ae9-181">Esempio: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="e9ae9-182">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-182">Date</span></span> |<span data-ttu-id="e9ae9-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="e9ae9-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="e9ae9-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-185">Y: int</span></span> |<span data-ttu-id="e9ae9-186">Aggiunge Y * 3 mesi tooX.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="e9ae9-187">Esempio: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e9ae9-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="e9ae9-188">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-188">Date</span></span> |<span data-ttu-id="e9ae9-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="e9ae9-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-190">X: DateTime</span></span><br/><br/><span data-ttu-id="e9ae9-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-191">Y: int</span></span> |<span data-ttu-id="e9ae9-192">Aggiunge Y * 7 giorni tooX</span><span class="sxs-lookup"><span data-stu-id="e9ae9-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="e9ae9-193">Esempio: 15/09/2013 12:00:00 + 1 settimana = 22/09/2013 12:00:00</span><span class="sxs-lookup"><span data-stu-id="e9ae9-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="e9ae9-194">È possibile anche sottrarre settimane specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e9ae9-195">Esempio: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e9ae9-196">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-196">Date</span></span> |<span data-ttu-id="e9ae9-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-197">AddYears(X,Y)</span></span> |<span data-ttu-id="e9ae9-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="e9ae9-198">X: DateTime</span></span><br/><br/><span data-ttu-id="e9ae9-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="e9ae9-199">Y: int</span></span> |<span data-ttu-id="e9ae9-200">Aggiunge Y anni tooX.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="e9ae9-201">È possibile anche sottrarre anni specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e9ae9-202">Esempio: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e9ae9-203">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-203">Date</span></span> |<span data-ttu-id="e9ae9-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-204">Day(X)</span></span> |<span data-ttu-id="e9ae9-205">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-205">X: DateTime</span></span> |<span data-ttu-id="e9ae9-206">Ottiene il componente giorno hello di X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="e9ae9-207">Esempio: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="e9ae9-208">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-208">Date</span></span> |<span data-ttu-id="e9ae9-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-209">DayOfWeek(X)</span></span> |<span data-ttu-id="e9ae9-210">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-210">X: DateTime</span></span> |<span data-ttu-id="e9ae9-211">Ottiene hello componente giorno della settimana di X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="e9ae9-212">Esempio: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="e9ae9-213">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-213">Date</span></span> |<span data-ttu-id="e9ae9-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-214">DayOfYear(X)</span></span> |<span data-ttu-id="e9ae9-215">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-215">X: DateTime</span></span> |<span data-ttu-id="e9ae9-216">Ottiene il giorno hello nell'anno hello rappresentato dal componente anno hello di X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="e9ae9-217">Esempi:</span><span class="sxs-lookup"><span data-stu-id="e9ae9-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="e9ae9-218">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-218">Date</span></span> |<span data-ttu-id="e9ae9-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-219">DaysInMonth(X)</span></span> |<span data-ttu-id="e9ae9-220">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-220">X: DateTime</span></span> |<span data-ttu-id="e9ae9-221">Ottiene i giorni hello nel mese di hello rappresentato dal componente di mese di hello del parametro X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="e9ae9-222">Esempio: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="e9ae9-223">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-223">Date</span></span> |<span data-ttu-id="e9ae9-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-224">EndOfDay(X)</span></span> |<span data-ttu-id="e9ae9-225">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-225">X: DateTime</span></span> |<span data-ttu-id="e9ae9-226">Ottiene data e ora di hello che rappresenta la fine del giorno hello (componente giorno) x hello.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="e9ae9-227">Esempio: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="e9ae9-228">Data</span><span class="sxs-lookup"><span data-stu-id="e9ae9-228">Date</span></span> |<span data-ttu-id="e9ae9-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-229">EndOfMonth(X)</span></span> |<span data-ttu-id="e9ae9-230">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-230">X: DateTime</span></span> |<span data-ttu-id="e9ae9-231">Ottiene hello fine del mese hello rappresentato dal componente di mese del parametro X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="e9ae9-232">Esempio: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data e ora che rappresenta la fine del mese di settembre hello)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="e9ae9-233">Date</span><span class="sxs-lookup"><span data-stu-id="e9ae9-233">Date</span></span> |<span data-ttu-id="e9ae9-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-234">StartOfDay(X)</span></span> |<span data-ttu-id="e9ae9-235">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-235">X: DateTime</span></span> |<span data-ttu-id="e9ae9-236">Ottiene l'inizio di hello del giorno hello rappresentato dal componente giorno hello del parametro X.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="e9ae9-237">Esempio: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="e9ae9-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-238">DateTime</span></span> |<span data-ttu-id="e9ae9-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-239">From(X)</span></span> |<span data-ttu-id="e9ae9-240">X: String</span><span class="sxs-lookup"><span data-stu-id="e9ae9-240">X: String</span></span> |<span data-ttu-id="e9ae9-241">Analizzare la stringa X tooa data ora.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="e9ae9-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-242">DateTime</span></span> |<span data-ttu-id="e9ae9-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-243">Ticks(X)</span></span> |<span data-ttu-id="e9ae9-244">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="e9ae9-244">X: DateTime</span></span> |<span data-ttu-id="e9ae9-245">Ottiene i segni di graduazione hello proprietà del parametro hello X. Un tick è uguale a 100 nanosecondi.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="e9ae9-246">il valore di Hello di questa proprietà rappresenta il numero di hello di segni di graduazione che sono trascorsi dalla mezzanotte 12:00:00 del 1 ° gennaio 0001.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="e9ae9-247">Text</span><span class="sxs-lookup"><span data-stu-id="e9ae9-247">Text</span></span> |<span data-ttu-id="e9ae9-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="e9ae9-248">Format(X)</span></span> |<span data-ttu-id="e9ae9-249">X: variabile stringa</span><span class="sxs-lookup"><span data-stu-id="e9ae9-249">X: String variable</span></span> |<span data-ttu-id="e9ae9-250">Formati di testo di hello (utilizzare `\\'` tooescape combinazione `'` carattere).</span><span class="sxs-lookup"><span data-stu-id="e9ae9-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="e9ae9-251">Quando si utilizza una funzione all'interno di un'altra funzione, non è necessario toouse  **$$**  prefisso per la funzione interna hello.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="e9ae9-252">Ad esempio: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="e9ae9-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="e9ae9-253">In questo esempio, si noti che  **$$**  prefisso non viene utilizzato per hello **Time.AddHours** (funzione).</span><span class="sxs-lookup"><span data-stu-id="e9ae9-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="e9ae9-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9ae9-254">Example</span></span>
<span data-ttu-id="e9ae9-255">In hello vengono determinati i seguenti parametri di esempio di input e output per l'attività Hive hello utilizzando hello `Text.Format` SliceStart variabili di sistema e di funzione.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="e9ae9-256">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="e9ae9-256">Example 2</span></span>

<span data-ttu-id="e9ae9-257">Nell'esempio seguente di hello, hello parametro DateTime per l'attività Stored Procedure viene determinato tramite hello testo hello.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="e9ae9-258">Formattare la funzione e hello SliceStart variabile.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-258">Format function and hello SliceStart variable.</span></span> 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="e9ae9-259">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="e9ae9-259">Example 3</span></span>
<span data-ttu-id="e9ae9-260">dati tooread dal giorno precedente anziché giorno rappresentato dal hello SliceStart, funzione hello AddDays come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e9ae9-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

<span data-ttu-id="e9ae9-261">Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: AA e aaaa.</span><span class="sxs-lookup"><span data-stu-id="e9ae9-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

