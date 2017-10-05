---
title: Funzioni JavaScript definite dall'utente in Analisi di flusso di Azure | Microsoft Docs
description: Eseguire i meccanismi di query avanzate con funzioni JavaScript definite dall'utente
keywords: javascript, funzioni definite dall'utente, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="1a9cb-104">Funzioni JavaScript definite dall'utente in Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="1a9cb-105">L'Analisi di flusso di Azure supporta le funzioni definite dall'utente nel linguaggio JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="1a9cb-106">Con il vasto set di metodi **String**, **RegExp**, **Math**, **Array** e **Date** offerti da JavaScript, risulta più facile creare trasformazioni di dati complessi con processi di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="1a9cb-107">Funzioni JavaScript definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="1a9cb-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="1a9cb-108">Le funzioni JavaScript definite dall'utente supportano funzioni senza stato e di solo calcolo che non richiedono connettività esterna.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="1a9cb-109">Il valore restituito di una funzione può essere solo un valore scalare singolo.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="1a9cb-110">Dopo aver aggiunto una funzione JavaScript definita dall'utente a un processo, è possibile utilizzare la funzione in un punto qualsiasi nella query, ad esempio una funzione scalare incorporata.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="1a9cb-111">Ecco alcuni scenari in cui potrebbero essere utili le funzioni JavaScript definite dall'utente:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="1a9cb-112">Analisi e manipolazione delle stringhe con funzioni di espressione regolare, ad esempio **Regexp_Replace()** e **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="1a9cb-113">Decodifica e codifica dati, ad esempio conversione dal formato binario al formato esadecimale</span><span class="sxs-lookup"><span data-stu-id="1a9cb-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="1a9cb-114">Esecuzione di calcoli matematici con funzioni JavaScript **Math**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="1a9cb-115">Esecuzione di operazioni di matrice come ordinamento, aggiunta, ricerca e riempimento</span><span class="sxs-lookup"><span data-stu-id="1a9cb-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="1a9cb-116">Ecco alcune operazioni non eseguibili con una funzione JavaScript definita dall'utente in Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="1a9cb-117">Chiamate agli endpoint REST esterni, ad esempio per l'esecuzione di una ricerca inversa degli indirizzi IP o per la raccolta di dati di riferimento da un'origine esterna</span><span class="sxs-lookup"><span data-stu-id="1a9cb-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="1a9cb-118">Esecuzione della serializzazione o deserializzazione negli input e output di un formato evento personalizzato</span><span class="sxs-lookup"><span data-stu-id="1a9cb-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="1a9cb-119">Creazione di aggregazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="1a9cb-119">Create custom aggregates</span></span>

<span data-ttu-id="1a9cb-120">Sebbene le funzioni come **Date.GetDate()** o **Math.random()** non sono bloccate nella definizione delle funzioni, è consigliabile evitare di utilizzarle.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="1a9cb-121">Queste funzioni, infatti, **non** restituiscono lo stesso risultato ogni volta che vengono chiamate e Analisi di flusso di Azure non conserva un giornale di chiamate di funzione e dei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="1a9cb-122">Se una funzione restituisce risultati diversi per gli stessi eventi, non viene garantita la ripetibilità in caso di processo riavviato dall'utente o dal servizio di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="1a9cb-123">Aggiungere una funzione JavaScript definita dall'utente nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="1a9cb-124">I passaggi seguenti illustrano come creare una semplice funzione JavaScript definita dall'utente in un processo esistente di Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="1a9cb-125">Nel portale di Azure individuare il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="1a9cb-126">In **TOPOLOGIA PROCESSO** selezionare la funzione.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="1a9cb-127">Viene visualizzato un elenco vuoto di funzioni.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="1a9cb-128">Per creare una nuova funzione definita dall'utente, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="1a9cb-129">Sul pannello **Nuova funzione** selezionare **JavaScript** per **Tipo funzione**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="1a9cb-130">Nell'editor viene visualizzato un modello di funzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="1a9cb-131">Per l'**alias della funzione definita dall'utente**, inserire **hex2Int** e modificare l'implementazione della funzione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="1a9cb-132">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-132">Select **Save**.</span></span> <span data-ttu-id="1a9cb-133">La funzione viene visualizzata nell'elenco delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="1a9cb-134">Selezionare la nuova funzione **hex2Int** e controllare la definizione di funzione.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="1a9cb-135">Per ogni funzione, all'alias della funzione viene aggiunto un prefisso della **funzione definita dall'utente**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="1a9cb-136">È necessario *includere il prefisso* quando si chiama la funzione nella query Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="1a9cb-137">In questo caso, si chiama **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="1a9cb-138">Chiamare una funzione JavaScript definita dall'utente nella query</span><span class="sxs-lookup"><span data-stu-id="1a9cb-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="1a9cb-139">Nell'editor di query, in **TOPOLOGIA PROCESSO**, selezionare **Query**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="1a9cb-140">Modificare la query e quindi chiamare la funzione definita dall'utente, simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="1a9cb-141">Per caricare un file di dati di esempio, fare clic con il tasto destro del mouse sull'input del processo.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="1a9cb-142">Per testare la query, selezionare **Test**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="1a9cb-143">Oggetti JavaScript supportati</span><span class="sxs-lookup"><span data-stu-id="1a9cb-143">Supported JavaScript objects</span></span>
<span data-ttu-id="1a9cb-144">Le funzioni JavaScript definite dall'utente in Analisi di flusso di Azure supportano oggetti JavaScript standard e incorporati.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="1a9cb-145">Per un elenco di questi oggetti, vedere [Oggetti globali](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="1a9cb-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="1a9cb-146">Conversione dei tipi di Analisi di flusso e JavaScript</span><span class="sxs-lookup"><span data-stu-id="1a9cb-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="1a9cb-147">Esistono delle differenze tra i tipi supportati da JavaScript e dal linguaggio di query di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="1a9cb-148">Questa tabella elenca i mapping di conversione tra i due:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="1a9cb-149">Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="1a9cb-149">Stream Analytics</span></span> | <span data-ttu-id="1a9cb-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1a9cb-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="1a9cb-151">bigint</span><span class="sxs-lookup"><span data-stu-id="1a9cb-151">bigint</span></span> | <span data-ttu-id="1a9cb-152">Numero (per la precisione, JavaScript può rappresentare solo numeri interi fino a 2^53)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="1a9cb-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="1a9cb-153">DateTime</span></span> | <span data-ttu-id="1a9cb-154">Data (JavaScript supporta solo millisecondi)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="1a9cb-155">double</span><span class="sxs-lookup"><span data-stu-id="1a9cb-155">double</span></span> | <span data-ttu-id="1a9cb-156">Number</span><span class="sxs-lookup"><span data-stu-id="1a9cb-156">Number</span></span>
<span data-ttu-id="1a9cb-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-157">nvarchar(MAX)</span></span> | <span data-ttu-id="1a9cb-158">string</span><span class="sxs-lookup"><span data-stu-id="1a9cb-158">String</span></span>
<span data-ttu-id="1a9cb-159">Record</span><span class="sxs-lookup"><span data-stu-id="1a9cb-159">Record</span></span> | <span data-ttu-id="1a9cb-160">Oggetto</span><span class="sxs-lookup"><span data-stu-id="1a9cb-160">Object</span></span>
<span data-ttu-id="1a9cb-161">Array</span><span class="sxs-lookup"><span data-stu-id="1a9cb-161">Array</span></span> | <span data-ttu-id="1a9cb-162">Array</span><span class="sxs-lookup"><span data-stu-id="1a9cb-162">Array</span></span>
<span data-ttu-id="1a9cb-163">NULL</span><span class="sxs-lookup"><span data-stu-id="1a9cb-163">NULL</span></span> | <span data-ttu-id="1a9cb-164">Null</span><span class="sxs-lookup"><span data-stu-id="1a9cb-164">Null</span></span>


<span data-ttu-id="1a9cb-165">Ecco le conversioni da JavaScript ad Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="1a9cb-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="1a9cb-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1a9cb-166">JavaScript</span></span> | <span data-ttu-id="1a9cb-167">Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="1a9cb-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="1a9cb-168">Number</span><span class="sxs-lookup"><span data-stu-id="1a9cb-168">Number</span></span> | <span data-ttu-id="1a9cb-169">Bigint (se il numero è arrotondato e compreso tra long.MinValue e long.MaxValue, in caso contrario è doppio)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="1a9cb-170">Date</span><span class="sxs-lookup"><span data-stu-id="1a9cb-170">Date</span></span> | <span data-ttu-id="1a9cb-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="1a9cb-171">DateTime</span></span>
<span data-ttu-id="1a9cb-172">String</span><span class="sxs-lookup"><span data-stu-id="1a9cb-172">String</span></span> | <span data-ttu-id="1a9cb-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-173">nvarchar(MAX)</span></span>
<span data-ttu-id="1a9cb-174">Oggetto</span><span class="sxs-lookup"><span data-stu-id="1a9cb-174">Object</span></span> | <span data-ttu-id="1a9cb-175">Record</span><span class="sxs-lookup"><span data-stu-id="1a9cb-175">Record</span></span>
<span data-ttu-id="1a9cb-176">Array</span><span class="sxs-lookup"><span data-stu-id="1a9cb-176">Array</span></span> | <span data-ttu-id="1a9cb-177">Array</span><span class="sxs-lookup"><span data-stu-id="1a9cb-177">Array</span></span>
<span data-ttu-id="1a9cb-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="1a9cb-178">Null, Undefined</span></span> | <span data-ttu-id="1a9cb-179">NULL</span><span class="sxs-lookup"><span data-stu-id="1a9cb-179">NULL</span></span>
<span data-ttu-id="1a9cb-180">Qualsiasi altro tipo (ad esempio, una funzione o un errore)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="1a9cb-181">Non supportato (risultati nell'errore di runtime)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1a9cb-182">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1a9cb-182">Troubleshooting</span></span>
<span data-ttu-id="1a9cb-183">Gli errori di runtime in JavaScript sono considerati irreversibili ed esposti tramite il log attività.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="1a9cb-184">Per recuperare il log, nel portale di Azure passare al processo e selezionare **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="1a9cb-185">Altri modelli della funzione JavaScript definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="1a9cb-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="1a9cb-186">Scrivere una stringa JSON nidificata in output</span><span class="sxs-lookup"><span data-stu-id="1a9cb-186">Write nested JSON to output</span></span>
<span data-ttu-id="1a9cb-187">In caso di passaggi di elaborazione successivi che utilizzano un output di un processo di Analisi di flusso come input e l'output richiede un formato JSON, è possibile scrivere una stringa JSON in output.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="1a9cb-188">L'esempio successivo chiama la funzione **JSON.stringify()** per raccogliere tutte le coppie nome/valore dell'input e quindi scriverle come valore di stringa singola nell'output.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="1a9cb-189">**Definizione della funzione JavaScript definita dall'utente:**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="1a9cb-190">**Query di esempio:**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="1a9cb-191">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="1a9cb-191">Get help</span></span>
<span data-ttu-id="1a9cb-192">Per ulteriore assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1a9cb-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a9cb-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a9cb-193">Next steps</span></span>
* [<span data-ttu-id="1a9cb-194">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1a9cb-195">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1a9cb-196">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1a9cb-197">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1a9cb-198">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9cb-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
