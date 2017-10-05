---
title: Funzioni e variabili di sistema di Data Factory | Microsoft Docs
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
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="1be58-103">Azure Data Factory - Funzioni e variabili di sistema</span><span class="sxs-lookup"><span data-stu-id="1be58-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="1be58-104">In questo articolo vengono fornite informazioni sulle funzioni e le variabili supportate da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1be58-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="1be58-105">Variabili di sistema di Data Factory</span><span class="sxs-lookup"><span data-stu-id="1be58-105">Data Factory system variables</span></span>
| <span data-ttu-id="1be58-106">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="1be58-106">Variable Name</span></span> | <span data-ttu-id="1be58-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1be58-107">Description</span></span> | <span data-ttu-id="1be58-108">Ambito dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="1be58-108">Object Scope</span></span> | <span data-ttu-id="1be58-109">Ambito JSON e casi d'uso</span><span class="sxs-lookup"><span data-stu-id="1be58-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1be58-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="1be58-110">WindowStart</span></span> |<span data-ttu-id="1be58-111">Inizio dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività</span><span class="sxs-lookup"><span data-stu-id="1be58-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="1be58-112">attività</span><span class="sxs-lookup"><span data-stu-id="1be58-112">activity</span></span> |<ol><li><span data-ttu-id="1be58-113">Definizione delle query di selezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="1be58-113">Specify data selection queries.</span></span> <span data-ttu-id="1be58-114">Vedere gli articoli connettore a cui fa riferimento l'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="1be58-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="1be58-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="1be58-115">WindowEnd</span></span> |<span data-ttu-id="1be58-116">Fine dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività</span><span class="sxs-lookup"><span data-stu-id="1be58-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="1be58-117">attività</span><span class="sxs-lookup"><span data-stu-id="1be58-117">activity</span></span> |<span data-ttu-id="1be58-118">uguale a WindowStart.</span><span class="sxs-lookup"><span data-stu-id="1be58-118">same as WindowStart.</span></span> |
| <span data-ttu-id="1be58-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="1be58-119">SliceStart</span></span> |<span data-ttu-id="1be58-120">Inizio dell'intervallo di tempo relativo alla sezione di dati in fase di produzione</span><span class="sxs-lookup"><span data-stu-id="1be58-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="1be58-121">attività</span><span class="sxs-lookup"><span data-stu-id="1be58-121">activity</span></span><br/><span data-ttu-id="1be58-122">attività</span><span class="sxs-lookup"><span data-stu-id="1be58-122">dataset</span></span> |<ol><li><span data-ttu-id="1be58-123">Definizione di nomi di file e percorsi di cartelle dinamici durante l'uso dell'[archivio BLOB di Azure](data-factory-azure-blob-connector.md) e dei [set di dati del file system](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="1be58-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="1be58-124">Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.</span><span class="sxs-lookup"><span data-stu-id="1be58-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="1be58-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="1be58-125">SliceEnd</span></span> |<span data-ttu-id="1be58-126">Fine dell'intervallo di tempo relativo alla sezione di dati corrente.</span><span class="sxs-lookup"><span data-stu-id="1be58-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="1be58-127">attività</span><span class="sxs-lookup"><span data-stu-id="1be58-127">activity</span></span><br/><span data-ttu-id="1be58-128">dataset</span><span class="sxs-lookup"><span data-stu-id="1be58-128">dataset</span></span> |<span data-ttu-id="1be58-129">uguale a SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1be58-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="1be58-130">Attualmente Data Factory richiede che la pianificazione specificata nell'attività corrisponda esattamente alla pianificazione specificata nella sezione relativa alla disponibilità del set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="1be58-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="1be58-131">Il mapping delle variabili WindowStart, WindowEnd, SliceStart e SliceEnd viene quindi sempre eseguito allo stesso periodo di tempo e a un'unica sezione di output.</span><span class="sxs-lookup"><span data-stu-id="1be58-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="1be58-132">Esempio di uso di una variabile di sistema</span><span class="sxs-lookup"><span data-stu-id="1be58-132">Example for using a system variable</span></span>
<span data-ttu-id="1be58-133">Nell'esempio seguente l'anno, il mese, il giorno e l'ora di **SliceStart** vengono estratti in variabili separate usate dalle proprietà **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="1be58-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="1be58-134">Funzioni di Data Factory</span><span class="sxs-lookup"><span data-stu-id="1be58-134">Data Factory functions</span></span>
<span data-ttu-id="1be58-135">È possibile combinare le funzioni della data factory con le variabili di sistema per gli scopi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1be58-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="1be58-136">Definizione delle query di selezione dei dati (vedere gli articoli connettore a cui fa riferimento l'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="1be58-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="1be58-137">La sintassi per chiamare una funzione della data factory è **$$<function>** per le query di selezione dei dati e altre proprietà dell'attività e del set di dati.</span><span class="sxs-lookup"><span data-stu-id="1be58-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="1be58-138">Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.</span><span class="sxs-lookup"><span data-stu-id="1be58-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="1be58-139">La sintassi $$ non è necessaria per definire le espressioni delle dipendenze di input.</span><span class="sxs-lookup"><span data-stu-id="1be58-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="1be58-140">Nell'esempio seguente la proprietà **sqlReaderQuery** di un file JSON è assegnata a un valore restituito dalla funzione `Text.Format`.</span><span class="sxs-lookup"><span data-stu-id="1be58-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="1be58-141">Questo esempio usa anche una variabile di sistema denominata **WindowStart**, che rappresenta l'ora di inizio della finestra di esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="1be58-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="1be58-142">Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: aa e aaaa.</span><span class="sxs-lookup"><span data-stu-id="1be58-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="1be58-143">Funzioni</span><span class="sxs-lookup"><span data-stu-id="1be58-143">Functions</span></span>
<span data-ttu-id="1be58-144">Le tabelle seguenti elencano tutte le funzioni di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="1be58-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="1be58-145">Categoria</span><span class="sxs-lookup"><span data-stu-id="1be58-145">Category</span></span> | <span data-ttu-id="1be58-146">Funzione</span><span class="sxs-lookup"><span data-stu-id="1be58-146">Function</span></span> | <span data-ttu-id="1be58-147">Parametri</span><span class="sxs-lookup"><span data-stu-id="1be58-147">Parameters</span></span> | <span data-ttu-id="1be58-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1be58-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1be58-149">Time</span><span class="sxs-lookup"><span data-stu-id="1be58-149">Time</span></span> |<span data-ttu-id="1be58-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-150">AddHours(X,Y)</span></span> |<span data-ttu-id="1be58-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="1be58-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-152">Y: int</span></span> |<span data-ttu-id="1be58-153">Aggiunge Y ore all'ora X specificata.</span><span class="sxs-lookup"><span data-stu-id="1be58-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="1be58-154">Esempio: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1be58-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="1be58-155">Time</span><span class="sxs-lookup"><span data-stu-id="1be58-155">Time</span></span> |<span data-ttu-id="1be58-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="1be58-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="1be58-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-158">Y: int</span></span> |<span data-ttu-id="1be58-159">Aggiunge Y minuti a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="1be58-160">Esempio: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1be58-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="1be58-161">Time</span><span class="sxs-lookup"><span data-stu-id="1be58-161">Time</span></span> |<span data-ttu-id="1be58-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-162">StartOfHour(X)</span></span> |<span data-ttu-id="1be58-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-163">X: Datetime</span></span> |<span data-ttu-id="1be58-164">Ottiene l'ora di inizio per l'ora rappresentata dal componente ora di X.</span><span class="sxs-lookup"><span data-stu-id="1be58-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="1be58-165">Esempio: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1be58-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="1be58-166">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-166">Date</span></span> |<span data-ttu-id="1be58-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-167">AddDays(X,Y)</span></span> |<span data-ttu-id="1be58-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-168">X: DateTime</span></span><br/><br/><span data-ttu-id="1be58-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-169">Y: int</span></span> |<span data-ttu-id="1be58-170">Aggiunge Y giorni a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="1be58-171">Esempio: 9/15/2013 12:00:00 PM + 2 giorni = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="1be58-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="1be58-172">È possibile anche sottrarre giorni specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="1be58-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1be58-173">Esempio: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1be58-174">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-174">Date</span></span> |<span data-ttu-id="1be58-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="1be58-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-176">X: DateTime</span></span><br/><br/><span data-ttu-id="1be58-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-177">Y: int</span></span> |<span data-ttu-id="1be58-178">Aggiunge Y mesi a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="1be58-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="1be58-180">È possibile anche sottrarre mesi specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="1be58-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1be58-181">Esempio: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="1be58-182">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-182">Date</span></span> |<span data-ttu-id="1be58-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="1be58-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="1be58-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-185">Y: int</span></span> |<span data-ttu-id="1be58-186">Aggiunge Y * 3 mesi a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="1be58-187">Esempio: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1be58-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="1be58-188">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-188">Date</span></span> |<span data-ttu-id="1be58-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="1be58-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-190">X: DateTime</span></span><br/><br/><span data-ttu-id="1be58-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-191">Y: int</span></span> |<span data-ttu-id="1be58-192">Aggiunge Y * 7 giorni a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="1be58-193">Esempio: 15/09/2013 12:00:00 + 1 settimana = 22/09/2013 12:00:00</span><span class="sxs-lookup"><span data-stu-id="1be58-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="1be58-194">È possibile anche sottrarre settimane specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="1be58-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1be58-195">Esempio: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1be58-196">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-196">Date</span></span> |<span data-ttu-id="1be58-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1be58-197">AddYears(X,Y)</span></span> |<span data-ttu-id="1be58-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-198">X: DateTime</span></span><br/><br/><span data-ttu-id="1be58-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="1be58-199">Y: int</span></span> |<span data-ttu-id="1be58-200">Aggiunge Y anni a X.</span><span class="sxs-lookup"><span data-stu-id="1be58-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="1be58-201">È possibile anche sottrarre anni specificando Y come un numero negativo.</span><span class="sxs-lookup"><span data-stu-id="1be58-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1be58-202">Esempio: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1be58-203">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-203">Date</span></span> |<span data-ttu-id="1be58-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-204">Day(X)</span></span> |<span data-ttu-id="1be58-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-205">X: DateTime</span></span> |<span data-ttu-id="1be58-206">Ottiene il componente giorno di X.</span><span class="sxs-lookup"><span data-stu-id="1be58-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="1be58-207">Esempio: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="1be58-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="1be58-208">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-208">Date</span></span> |<span data-ttu-id="1be58-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-209">DayOfWeek(X)</span></span> |<span data-ttu-id="1be58-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-210">X: DateTime</span></span> |<span data-ttu-id="1be58-211">Ottiene il giorno del componente settimana di X.</span><span class="sxs-lookup"><span data-stu-id="1be58-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="1be58-212">Esempio: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="1be58-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="1be58-213">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-213">Date</span></span> |<span data-ttu-id="1be58-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-214">DayOfYear(X)</span></span> |<span data-ttu-id="1be58-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-215">X: DateTime</span></span> |<span data-ttu-id="1be58-216">Ottiene il giorno dell'anno rappresentato dal componente anno di X.</span><span class="sxs-lookup"><span data-stu-id="1be58-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="1be58-217">Esempi:</span><span class="sxs-lookup"><span data-stu-id="1be58-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="1be58-218">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-218">Date</span></span> |<span data-ttu-id="1be58-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-219">DaysInMonth(X)</span></span> |<span data-ttu-id="1be58-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-220">X: DateTime</span></span> |<span data-ttu-id="1be58-221">Ottiene i giorni del mese rappresentati dal componente mese del parametro X.</span><span class="sxs-lookup"><span data-stu-id="1be58-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="1be58-222">Esempio: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="1be58-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="1be58-223">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-223">Date</span></span> |<span data-ttu-id="1be58-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-224">EndOfDay(X)</span></span> |<span data-ttu-id="1be58-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-225">X: DateTime</span></span> |<span data-ttu-id="1be58-226">Ottiene la data e ora che rappresenta la fine del giorno (componente giorno) X.</span><span class="sxs-lookup"><span data-stu-id="1be58-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="1be58-227">Esempio: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="1be58-228">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-228">Date</span></span> |<span data-ttu-id="1be58-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-229">EndOfMonth(X)</span></span> |<span data-ttu-id="1be58-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-230">X: DateTime</span></span> |<span data-ttu-id="1be58-231">Ottiene la fine del mese rappresentato dal componente mese del parametro X.</span><span class="sxs-lookup"><span data-stu-id="1be58-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="1be58-232">Esempio: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data e ora che rappresentano la fine del mese di settembre)</span><span class="sxs-lookup"><span data-stu-id="1be58-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="1be58-233">Data</span><span class="sxs-lookup"><span data-stu-id="1be58-233">Date</span></span> |<span data-ttu-id="1be58-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-234">StartOfDay(X)</span></span> |<span data-ttu-id="1be58-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="1be58-235">X: DateTime</span></span> |<span data-ttu-id="1be58-236">Ottiene l'inizio del giorno rappresentato dal componente giorno del parametro X.</span><span class="sxs-lookup"><span data-stu-id="1be58-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="1be58-237">Esempio: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="1be58-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="1be58-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="1be58-238">DateTime</span></span> |<span data-ttu-id="1be58-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-239">From(X)</span></span> |<span data-ttu-id="1be58-240">X: String</span><span class="sxs-lookup"><span data-stu-id="1be58-240">X: String</span></span> |<span data-ttu-id="1be58-241">Analizza la stringa X fino a una data/ora.</span><span class="sxs-lookup"><span data-stu-id="1be58-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="1be58-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="1be58-242">DateTime</span></span> |<span data-ttu-id="1be58-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-243">Ticks(X)</span></span> |<span data-ttu-id="1be58-244">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="1be58-244">X: DateTime</span></span> |<span data-ttu-id="1be58-245">Ottiene la proprietà dei tick del parametro X. Un tick equivale a 100 nanosecondi.</span><span class="sxs-lookup"><span data-stu-id="1be58-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="1be58-246">Il valore di questa proprietà rappresenta il numero di tick trascorsi dalla mezzanotte 12:00:00 del 1 gennaio 0001.</span><span class="sxs-lookup"><span data-stu-id="1be58-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="1be58-247">Text</span><span class="sxs-lookup"><span data-stu-id="1be58-247">Text</span></span> |<span data-ttu-id="1be58-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="1be58-248">Format(X)</span></span> |<span data-ttu-id="1be58-249">X: variabile stringa</span><span class="sxs-lookup"><span data-stu-id="1be58-249">X: String variable</span></span> |<span data-ttu-id="1be58-250">Formatta il testo (usare la combinazione `\\'` per il carattere di escape `'`).</span><span class="sxs-lookup"><span data-stu-id="1be58-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="1be58-251">Quando si usa una funzione all'interno di un'altra funzione, non è necessario usare il prefisso **$$** per la funzione interna.</span><span class="sxs-lookup"><span data-stu-id="1be58-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="1be58-252">Ad esempio: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="1be58-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="1be58-253">In questo esempio il prefisso **$$** non viene usato per la funzione **Time.AddHours**.</span><span class="sxs-lookup"><span data-stu-id="1be58-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="1be58-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="1be58-254">Example</span></span>
<span data-ttu-id="1be58-255">Nell'esempio seguente, i parametri di input e output per l'attività Hive vengono determinati usando la funzione `Text.Format` e la variabile di sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1be58-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="1be58-256">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="1be58-256">Example 2</span></span>

<span data-ttu-id="1be58-257">Nell'esempio seguente, il parametro DateTime per l'attività Stored Procedure viene determinato usando la funzione Text.</span><span class="sxs-lookup"><span data-stu-id="1be58-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="1be58-258">Format e la variabile di SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1be58-258">Format function and the SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="1be58-259">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="1be58-259">Example 3</span></span>
<span data-ttu-id="1be58-260">Per leggere i dati del giorno precedente anziché del giorno rappresentato da SliceStart, usare la funzione AddDays, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1be58-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

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

<span data-ttu-id="1be58-261">Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: AA e aaaa.</span><span class="sxs-lookup"><span data-stu-id="1be58-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

