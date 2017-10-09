---
title: le funzioni definite dall'utente flusso Analitica JavaScript aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="3a77a-104">Funzioni JavaScript definite dall'utente in Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="3a77a-105">L'Analisi di flusso di Azure supporta le funzioni definite dall'utente nel linguaggio JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3a77a-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="3a77a-106">Ampia gamma di hello di **stringa**, **RegExp**, **matematiche**, **matrice**, e **data** metodi che JavaScript fornisce, le trasformazioni di dati complessi con i processi di flusso Analitica diventano toocreate più semplice.</span><span class="sxs-lookup"><span data-stu-id="3a77a-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="3a77a-107">Funzioni JavaScript definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="3a77a-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="3a77a-108">Le funzioni JavaScript definite dall'utente supportano funzioni senza stato e di solo calcolo che non richiedono connettività esterna.</span><span class="sxs-lookup"><span data-stu-id="3a77a-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="3a77a-109">Hello restituiscono valore di una funzione può essere solo un valore scalare (singolo).</span><span class="sxs-lookup"><span data-stu-id="3a77a-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="3a77a-110">Dopo aver aggiunto un processo di tooa JavaScript funzione definita dall'utente, è possibile utilizzare la funzione hello in qualsiasi punto nella query hello, ad esempio una funzione scalare predefinita.</span><span class="sxs-lookup"><span data-stu-id="3a77a-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="3a77a-111">Ecco alcuni scenari in cui potrebbero essere utili le funzioni JavaScript definite dall'utente:</span><span class="sxs-lookup"><span data-stu-id="3a77a-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="3a77a-112">Analisi e manipolazione delle stringhe con funzioni di espressione regolare, ad esempio **Regexp_Replace()** e **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="3a77a-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="3a77a-113">Decodifica e codifica dati, ad esempio conversione dal formato binario al formato esadecimale</span><span class="sxs-lookup"><span data-stu-id="3a77a-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="3a77a-114">Esecuzione di calcoli matematici con funzioni JavaScript **Math**</span><span class="sxs-lookup"><span data-stu-id="3a77a-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="3a77a-115">Esecuzione di operazioni di matrice come ordinamento, aggiunta, ricerca e riempimento</span><span class="sxs-lookup"><span data-stu-id="3a77a-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="3a77a-116">Ecco alcune operazioni non eseguibili con una funzione JavaScript definita dall'utente in Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="3a77a-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="3a77a-117">Chiamate agli endpoint REST esterni, ad esempio per l'esecuzione di una ricerca inversa degli indirizzi IP o per la raccolta di dati di riferimento da un'origine esterna</span><span class="sxs-lookup"><span data-stu-id="3a77a-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="3a77a-118">Esecuzione della serializzazione o deserializzazione negli input e output di un formato evento personalizzato</span><span class="sxs-lookup"><span data-stu-id="3a77a-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="3a77a-119">Creazione di aggregazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="3a77a-119">Create custom aggregates</span></span>

<span data-ttu-id="3a77a-120">Sebbene le funzioni come **Date.GetDate()** o **Math.random()** non sono bloccate nella definizione di funzioni hello, è consigliabile evitare di utilizzarle.</span><span class="sxs-lookup"><span data-stu-id="3a77a-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="3a77a-121">Queste funzioni **non** hello restituito stesso risultato ogni volta che vengono chiamati e hello servizio Analitica di flusso di Azure non mantiene una registrazione di chiamate di funzione e ha restituito risultati.</span><span class="sxs-lookup"><span data-stu-id="3a77a-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="3a77a-122">Se una funzione restituisce risultati diversi in hello stessi eventi, ripetibilità non è garantito quando un processo viene riavviato dall'utente o dal servizio di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="3a77a-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="3a77a-123">Aggiungere una funzione definita dall'utente di JavaScript nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3a77a-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="3a77a-124">toocreate una funzione definita dall'utente JavaScript semplice in un processo di flusso Analitica esistente, eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3a77a-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="3a77a-125">Nel portale di Azure hello, trovare il processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="3a77a-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="3a77a-126">In **TOPOLOGIA PROCESSO** selezionare la funzione.</span><span class="sxs-lookup"><span data-stu-id="3a77a-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="3a77a-127">Viene visualizzato un elenco vuoto di funzioni.</span><span class="sxs-lookup"><span data-stu-id="3a77a-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="3a77a-128">Selezionare una nuova funzione definita dall'utente, toocreate **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="3a77a-129">In hello **nuova funzione** pannello per **tipo di funzione**selezionare **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="3a77a-130">Un modello di funzione predefinita viene visualizzata nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="3a77a-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="3a77a-131">Per hello **alias funzione definita dall'utente**, immettere **hex2Int**e modifica di implementazione della funzione hello come segue:</span><span class="sxs-lookup"><span data-stu-id="3a77a-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="3a77a-132">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-132">Select **Save**.</span></span> <span data-ttu-id="3a77a-133">La funzione viene visualizzato nell'elenco di hello di funzioni.</span><span class="sxs-lookup"><span data-stu-id="3a77a-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="3a77a-134">Seleziona hello nuovo **hex2Int** funzione e controllare la definizione di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="3a77a-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="3a77a-135">Tutte le funzioni hanno un **funzione definita dall'utente** alias di funzione di prefisso toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="3a77a-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="3a77a-136">È necessario troppo*includere il prefisso hello* quando si chiama la funzione hello nella query Analitica di flusso.</span><span class="sxs-lookup"><span data-stu-id="3a77a-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="3a77a-137">In questo caso, si chiama **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="3a77a-138">Chiamare una funzione JavaScript definita dall'utente nella query</span><span class="sxs-lookup"><span data-stu-id="3a77a-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="3a77a-139">In hello editor di query, in **processo TOPOLOGIA**selezionare **Query**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="3a77a-140">Modificare la query e quindi chiamare hello-funzione definita dall'utente, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3a77a-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="3a77a-141">file di dati di esempio hello tooupload, rapida hello processo input.</span><span class="sxs-lookup"><span data-stu-id="3a77a-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="3a77a-142">tootest della query, seleziona **Test**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="3a77a-143">Oggetti JavaScript supportati</span><span class="sxs-lookup"><span data-stu-id="3a77a-143">Supported JavaScript objects</span></span>
<span data-ttu-id="3a77a-144">Le funzioni JavaScript definite dall'utente in Analisi di flusso di Azure supportano oggetti JavaScript standard e incorporati.</span><span class="sxs-lookup"><span data-stu-id="3a77a-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="3a77a-145">Per un elenco di questi oggetti, vedere [Oggetti globali](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="3a77a-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="3a77a-146">Conversione dei tipi di Analisi di flusso e JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a77a-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="3a77a-147">Esistono differenze nei tipi di hello che supportano il linguaggio di query flusso Analitica hello e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3a77a-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="3a77a-148">Questa tabella elenca i mapping di conversione hello tra hello due:</span><span class="sxs-lookup"><span data-stu-id="3a77a-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="3a77a-149">Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="3a77a-149">Stream Analytics</span></span> | <span data-ttu-id="3a77a-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a77a-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="3a77a-151">bigint</span><span class="sxs-lookup"><span data-stu-id="3a77a-151">bigint</span></span> | <span data-ttu-id="3a77a-152">Numero (JavaScript possono rappresentare solo valori interi di tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="3a77a-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="3a77a-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="3a77a-153">DateTime</span></span> | <span data-ttu-id="3a77a-154">Data (JavaScript supporta solo millisecondi)</span><span class="sxs-lookup"><span data-stu-id="3a77a-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="3a77a-155">double</span><span class="sxs-lookup"><span data-stu-id="3a77a-155">double</span></span> | <span data-ttu-id="3a77a-156">Number</span><span class="sxs-lookup"><span data-stu-id="3a77a-156">Number</span></span>
<span data-ttu-id="3a77a-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="3a77a-157">nvarchar(MAX)</span></span> | <span data-ttu-id="3a77a-158">string</span><span class="sxs-lookup"><span data-stu-id="3a77a-158">String</span></span>
<span data-ttu-id="3a77a-159">Record</span><span class="sxs-lookup"><span data-stu-id="3a77a-159">Record</span></span> | <span data-ttu-id="3a77a-160">Oggetto</span><span class="sxs-lookup"><span data-stu-id="3a77a-160">Object</span></span>
<span data-ttu-id="3a77a-161">Array</span><span class="sxs-lookup"><span data-stu-id="3a77a-161">Array</span></span> | <span data-ttu-id="3a77a-162">Array</span><span class="sxs-lookup"><span data-stu-id="3a77a-162">Array</span></span>
<span data-ttu-id="3a77a-163">NULL</span><span class="sxs-lookup"><span data-stu-id="3a77a-163">NULL</span></span> | <span data-ttu-id="3a77a-164">Null</span><span class="sxs-lookup"><span data-stu-id="3a77a-164">Null</span></span>


<span data-ttu-id="3a77a-165">Ecco le conversioni da JavaScript ad Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="3a77a-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="3a77a-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a77a-166">JavaScript</span></span> | <span data-ttu-id="3a77a-167">Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="3a77a-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="3a77a-168">Number</span><span class="sxs-lookup"><span data-stu-id="3a77a-168">Number</span></span> | <span data-ttu-id="3a77a-169">Bigint (se il numero di hello è arrotondamento e tra long. MinValue e long. MaxValue; in caso contrario, viene applicato il doppio)</span><span class="sxs-lookup"><span data-stu-id="3a77a-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="3a77a-170">Date</span><span class="sxs-lookup"><span data-stu-id="3a77a-170">Date</span></span> | <span data-ttu-id="3a77a-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="3a77a-171">DateTime</span></span>
<span data-ttu-id="3a77a-172">String</span><span class="sxs-lookup"><span data-stu-id="3a77a-172">String</span></span> | <span data-ttu-id="3a77a-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="3a77a-173">nvarchar(MAX)</span></span>
<span data-ttu-id="3a77a-174">Oggetto</span><span class="sxs-lookup"><span data-stu-id="3a77a-174">Object</span></span> | <span data-ttu-id="3a77a-175">Record</span><span class="sxs-lookup"><span data-stu-id="3a77a-175">Record</span></span>
<span data-ttu-id="3a77a-176">Array</span><span class="sxs-lookup"><span data-stu-id="3a77a-176">Array</span></span> | <span data-ttu-id="3a77a-177">Array</span><span class="sxs-lookup"><span data-stu-id="3a77a-177">Array</span></span>
<span data-ttu-id="3a77a-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="3a77a-178">Null, Undefined</span></span> | <span data-ttu-id="3a77a-179">NULL</span><span class="sxs-lookup"><span data-stu-id="3a77a-179">NULL</span></span>
<span data-ttu-id="3a77a-180">Qualsiasi altro tipo (ad esempio, una funzione o un errore)</span><span class="sxs-lookup"><span data-stu-id="3a77a-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="3a77a-181">Non supportato (risultati nell'errore di runtime)</span><span class="sxs-lookup"><span data-stu-id="3a77a-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3a77a-182">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3a77a-182">Troubleshooting</span></span>
<span data-ttu-id="3a77a-183">Errori di runtime di JavaScript sono considerati irreversibili e resi visibili tramite log attività hello.</span><span class="sxs-lookup"><span data-stu-id="3a77a-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="3a77a-184">log hello tooretrieve, nel portale di Azure hello, andare tooyour processo e scegliere **log attività**.</span><span class="sxs-lookup"><span data-stu-id="3a77a-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="3a77a-185">Altri modelli della funzione JavaScript definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="3a77a-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="3a77a-186">Scrivere toooutput JSON nidificata</span><span class="sxs-lookup"><span data-stu-id="3a77a-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="3a77a-187">Se si dispone di un passaggio di completamento di elaborazione che utilizza un processo Analitica di flusso di output come input, ed è necessario un formato JSON, è possibile scrivere un toooutput stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="3a77a-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="3a77a-188">esempio Hello chiama hello **JSON.stringify()** funzione toopack tutte le coppie nome/valore di hello di input e quindi li scrivono come un singolo valore stringa nell'output.</span><span class="sxs-lookup"><span data-stu-id="3a77a-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="3a77a-189">**Definizione della funzione JavaScript definita dall'utente:**</span><span class="sxs-lookup"><span data-stu-id="3a77a-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="3a77a-190">**Query di esempio:**</span><span class="sxs-lookup"><span data-stu-id="3a77a-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="3a77a-191">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="3a77a-191">Get help</span></span>
<span data-ttu-id="3a77a-192">Per ulteriore assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="3a77a-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a77a-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a77a-193">Next steps</span></span>
* [<span data-ttu-id="3a77a-194">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="3a77a-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3a77a-195">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3a77a-196">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3a77a-197">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3a77a-198">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
