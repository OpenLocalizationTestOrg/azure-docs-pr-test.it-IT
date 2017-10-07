---
title: esempi di aaaQuery per i modelli di utilizzo comune in flusso Analitica | Documenti Microsoft
description: Modelli di query comuni di Analisi di flusso di Azure
keywords: esempi di query
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="dbbc4-104">Esempi di query per modelli di uso comune di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="dbbc4-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="dbbc4-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="dbbc4-105">Introduction</span></span>
<span data-ttu-id="dbbc4-106">Le query in Analisi di flusso di Azure sono espresse in un linguaggio di query di tipo SQL.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="dbbc4-107">Queste query sono documentate in hello [flusso Analitica riferimenti al linguaggio di query](https://msdn.microsoft.com/library/azure/dn834998.aspx) Guida.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="dbbc4-108">Questo articolo vengono illustrati soluzioni tooseveral comuni modelli di query, in base a scenari reali.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="dbbc4-109">È un lavoro in corso e continua toobe aggiornato con nuovi modelli in maniera continuativa.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="dbbc4-110">Esempio di query: convertire tipi di dati</span><span class="sxs-lookup"><span data-stu-id="dbbc4-110">Query example: Convert data types</span></span>
<span data-ttu-id="dbbc4-111">**Descrizione**: definire i tipi di hello di proprietà nel flusso di input hello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="dbbc4-112">Ad esempio, peso car hello proviene nel flusso di input hello come stringhe e deve toobe convertito è troppo**INT** tooperform **somma** , configurarlo.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="dbbc4-113">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-113">**Input**:</span></span>

| <span data-ttu-id="dbbc4-114">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-114">Make</span></span> | <span data-ttu-id="dbbc4-115">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-115">Time</span></span> | <span data-ttu-id="dbbc4-116">Peso</span><span class="sxs-lookup"><span data-stu-id="dbbc4-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-117">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-117">Honda</span></span> |<span data-ttu-id="dbbc4-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="dbbc4-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-119">"1000"</span></span> |
| <span data-ttu-id="dbbc4-120">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-120">Honda</span></span> |<span data-ttu-id="dbbc4-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="dbbc4-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-122">"2000"</span></span> |

<span data-ttu-id="dbbc4-123">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-123">**Output**:</span></span>

| <span data-ttu-id="dbbc4-124">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-124">Make</span></span> | <span data-ttu-id="dbbc4-125">Peso</span><span class="sxs-lookup"><span data-stu-id="dbbc4-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-126">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-126">Honda</span></span> |<span data-ttu-id="dbbc4-127">3000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-127">3000</span></span> |

<span data-ttu-id="dbbc4-128">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="dbbc4-129">**SPIEGAZIONE**: utilizzare un **CAST** istruzione hello **peso** campo toospecify il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="dbbc4-130">Vedere hello elenco dei tipi di dati supportati in [tipi di dati (Analitica del flusso di Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbbc4-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="dbbc4-131">Esempio di query: utilizzare Like o Not like toodo criteri di ricerca</span><span class="sxs-lookup"><span data-stu-id="dbbc4-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="dbbc4-132">**Descrizione**: verificare che il valore di un campo evento hello corrisponde a un determinato modello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="dbbc4-133">Ad esempio, verificare che il risultato di hello restituisca targa che iniziare con una lettera e terminare con 9.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="dbbc4-134">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-134">**Input**:</span></span>

| <span data-ttu-id="dbbc4-135">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-135">Make</span></span> | <span data-ttu-id="dbbc4-136">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-136">LicensePlate</span></span> | <span data-ttu-id="dbbc4-137">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-138">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-138">Honda</span></span> |<span data-ttu-id="dbbc4-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="dbbc4-139">ABC-123</span></span> |<span data-ttu-id="dbbc4-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-141">Toyota</span></span> |<span data-ttu-id="dbbc4-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="dbbc4-142">AAA-999</span></span> |<span data-ttu-id="dbbc4-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="dbbc4-144">Nissan</span></span> |<span data-ttu-id="dbbc4-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="dbbc4-145">ABC-369</span></span> |<span data-ttu-id="dbbc4-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-147">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-147">**Output**:</span></span>

| <span data-ttu-id="dbbc4-148">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-148">Make</span></span> | <span data-ttu-id="dbbc4-149">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-149">LicensePlate</span></span> | <span data-ttu-id="dbbc4-150">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-151">Toyota</span></span> |<span data-ttu-id="dbbc4-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="dbbc4-152">AAA-999</span></span> |<span data-ttu-id="dbbc4-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="dbbc4-154">Nissan</span></span> |<span data-ttu-id="dbbc4-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="dbbc4-155">ABC-369</span></span> |<span data-ttu-id="dbbc4-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-157">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="dbbc4-158">**SPIEGAZIONE**: hello utilizzare **come** hello toocheck istruzione **LicensePlate** valore del campo.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="dbbc4-159">inizi con la lettera A, contenga una stringa di zeri o altri caratteri e termini con 9.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="dbbc4-160">Esempio di query: Specificare la logica per i diversi casi/valori (istruzioni CASE)</span><span class="sxs-lookup"><span data-stu-id="dbbc4-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="dbbc4-161">**Descrizione**: fornire un calcolo diverso per un campo in base un determinato criterio.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="dbbc4-162">Ad esempio, fornire una descrizione della stringa per automobili quanti di hello stesso rendere passato, con un caso speciale di 1.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="dbbc4-163">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-163">**Input**:</span></span>

| <span data-ttu-id="dbbc4-164">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-164">Make</span></span> | <span data-ttu-id="dbbc4-165">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-166">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-166">Honda</span></span> |<span data-ttu-id="dbbc4-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-168">Toyota</span></span> |<span data-ttu-id="dbbc4-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-170">Toyota</span></span> |<span data-ttu-id="dbbc4-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-172">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-172">**Output**:</span></span>

| <span data-ttu-id="dbbc4-173">Auto passate</span><span class="sxs-lookup"><span data-stu-id="dbbc4-173">CarsPassed</span></span> | <span data-ttu-id="dbbc4-174">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-175">1 Honda</span></span> |<span data-ttu-id="dbbc4-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-177">2 Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-177">2 Toyotas</span></span> |<span data-ttu-id="dbbc4-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="dbbc4-179">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="dbbc4-180">**SPIEGAZIONE**: hello **CASE** clausola consente tooprovide un calcolo diversi, in base ad alcuni criteri (in questo caso, il conteggio di hello di automobili hello nella finestra di aggregazione hello).</span><span class="sxs-lookup"><span data-stu-id="dbbc4-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="dbbc4-181">Esempio di query: inviare dati toomultiple restituisce</span><span class="sxs-lookup"><span data-stu-id="dbbc4-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="dbbc4-182">**Descrizione**: trasmissione dati toomultiple output destinazioni da un singolo processo.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="dbbc4-183">Ad esempio, analizzare i dati per un avviso in base a soglie e spazio di archiviazione di tooblob tutti gli eventi.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="dbbc4-184">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-184">**Input**:</span></span>

| <span data-ttu-id="dbbc4-185">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-185">Make</span></span> | <span data-ttu-id="dbbc4-186">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-187">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-187">Honda</span></span> |<span data-ttu-id="dbbc4-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-189">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-189">Honda</span></span> |<span data-ttu-id="dbbc4-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-191">Toyota</span></span> |<span data-ttu-id="dbbc4-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-193">Toyota</span></span> |<span data-ttu-id="dbbc4-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-195">Toyota</span></span> |<span data-ttu-id="dbbc4-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-197">**Output1**:</span></span>

| <span data-ttu-id="dbbc4-198">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-198">Make</span></span> | <span data-ttu-id="dbbc4-199">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-200">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-200">Honda</span></span> |<span data-ttu-id="dbbc4-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-202">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-202">Honda</span></span> |<span data-ttu-id="dbbc4-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-204">Toyota</span></span> |<span data-ttu-id="dbbc4-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-206">Toyota</span></span> |<span data-ttu-id="dbbc4-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-208">Toyota</span></span> |<span data-ttu-id="dbbc4-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-210">**Output2**:</span></span>

| <span data-ttu-id="dbbc4-211">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-211">Make</span></span> | <span data-ttu-id="dbbc4-212">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-212">Time</span></span> | <span data-ttu-id="dbbc4-213">Conteggio</span><span class="sxs-lookup"><span data-stu-id="dbbc4-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-214">Toyota</span></span> |<span data-ttu-id="dbbc4-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="dbbc4-216">3</span><span class="sxs-lookup"><span data-stu-id="dbbc4-216">3</span></span> |

<span data-ttu-id="dbbc4-217">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="dbbc4-218">**SPIEGAZIONE**: hello **INTO** clausola indica Analitica flusso quali hello restituisce toowrite hello dati toofrom questa istruzione.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="dbbc4-219">Hello prima query è pass-through dei dati di hello è pervenuta tooan output è denominato **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="dbbc4-220">funzionamento di una query secondo Hello alcune semplici aggregazioni e il filtro, quindi invia i risultati di hello tooa sistema di avvisi a valle.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="dbbc4-221">Si noti che è anche possibile riutilizzare i risultati di hello delle espressioni di tabella comuni hello (CTE) (ad esempio **WITH** istruzioni) in più istruzioni di output.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="dbbc4-222">Questa opzione è hello ulteriore vantaggio di apertura di un numero inferiore lettori toohello l'origine di input.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="dbbc4-223">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="dbbc4-224">Esempio di query: contare valori univoci</span><span class="sxs-lookup"><span data-stu-id="dbbc4-224">Query example: Count unique values</span></span>
<span data-ttu-id="dbbc4-225">**Descrizione**: contare il numero di hello di valori di campo univoco che vengono visualizzati nel flusso di hello all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="dbbc4-226">Ad esempio, il numero univoco consente di automobili passate casello hello in una finestra di 2 secondi?</span><span class="sxs-lookup"><span data-stu-id="dbbc4-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="dbbc4-227">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-227">**Input**:</span></span>

| <span data-ttu-id="dbbc4-228">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-228">Make</span></span> | <span data-ttu-id="dbbc4-229">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-230">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-230">Honda</span></span> |<span data-ttu-id="dbbc4-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-232">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-232">Honda</span></span> |<span data-ttu-id="dbbc4-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-234">Toyota</span></span> |<span data-ttu-id="dbbc4-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-236">Toyota</span></span> |<span data-ttu-id="dbbc4-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-238">Toyota</span></span> |<span data-ttu-id="dbbc4-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="dbbc4-240">**Output:**</span><span class="sxs-lookup"><span data-stu-id="dbbc4-240">**Output:**</span></span>

| <span data-ttu-id="dbbc4-241">Conteggio</span><span class="sxs-lookup"><span data-stu-id="dbbc4-241">Count</span></span> | <span data-ttu-id="dbbc4-242">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-243">2</span><span class="sxs-lookup"><span data-stu-id="dbbc4-243">2</span></span> |<span data-ttu-id="dbbc4-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="dbbc4-245">1</span><span class="sxs-lookup"><span data-stu-id="dbbc4-245">1</span></span> |<span data-ttu-id="dbbc4-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="dbbc4-247">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="dbbc4-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="dbbc4-248">**Spiegazione:**
**COUNT (DISTINCT rendere)** restituisce hello numero di valori distinct in hello **rendere** colonna all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="dbbc4-249">Esempio di query: Determinare la potenziale variazione di un valore</span><span class="sxs-lookup"><span data-stu-id="dbbc4-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="dbbc4-250">**Descrizione**: esaminare un toodetermine valore precedente se è diverso dal valore corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="dbbc4-251">Ad esempio, è Auto precedente hello in hello di strada casello hello che stesso rendere car corrente hello?</span><span class="sxs-lookup"><span data-stu-id="dbbc4-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="dbbc4-252">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-252">**Input**:</span></span>

| <span data-ttu-id="dbbc4-253">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-253">Make</span></span> | <span data-ttu-id="dbbc4-254">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-255">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-255">Honda</span></span> |<span data-ttu-id="dbbc4-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-257">Toyota</span></span> |<span data-ttu-id="dbbc4-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="dbbc4-259">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-259">**Output**:</span></span>

| <span data-ttu-id="dbbc4-260">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-260">Make</span></span> | <span data-ttu-id="dbbc4-261">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-262">Toyota</span></span> |<span data-ttu-id="dbbc4-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="dbbc4-264">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="dbbc4-265">**SPIEGAZIONE**: utilizzare **LAG** toopeek in hello nuovamente un evento flusso di input e ottenere hello **rendere** valore.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="dbbc4-266">Confrontare quindi toohello **rendere** valore hello corrente ed evento output hello se sono diversi.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="dbbc4-267">Esempio di query: primo evento hello trova in una finestra</span><span class="sxs-lookup"><span data-stu-id="dbbc4-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="dbbc4-268">**Descrizione**: auto prima di trovare hello in ogni intervallo di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="dbbc4-269">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-269">**Input**:</span></span>

| <span data-ttu-id="dbbc4-270">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-270">LicensePlate</span></span> | <span data-ttu-id="dbbc4-271">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-271">Make</span></span> | <span data-ttu-id="dbbc4-272">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="dbbc4-273">DXE 5291</span></span> |<span data-ttu-id="dbbc4-274">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-274">Honda</span></span> |<span data-ttu-id="dbbc4-275">27-07-2015T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="dbbc4-276">YZK 5704</span></span> |<span data-ttu-id="dbbc4-277">Ford</span><span class="sxs-lookup"><span data-stu-id="dbbc4-277">Ford</span></span> |<span data-ttu-id="dbbc4-278">27-07-2015T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="dbbc4-279">RMV 8282</span></span> |<span data-ttu-id="dbbc4-280">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-280">Honda</span></span> |<span data-ttu-id="dbbc4-281">27-07-2015T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="dbbc4-282">YHN 6970</span></span> |<span data-ttu-id="dbbc4-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-283">Toyota</span></span> |<span data-ttu-id="dbbc4-284">27-07-2015T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="dbbc4-285">VFE 1616</span></span> |<span data-ttu-id="dbbc4-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-286">Toyota</span></span> |<span data-ttu-id="dbbc4-287">27-07-2015T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="dbbc4-288">QYF 9358</span></span> |<span data-ttu-id="dbbc4-289">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-289">Honda</span></span> |<span data-ttu-id="dbbc4-290">27-07-2015T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="dbbc4-291">MDR 6128</span></span> |<span data-ttu-id="dbbc4-292">BMW</span><span class="sxs-lookup"><span data-stu-id="dbbc4-292">BMW</span></span> |<span data-ttu-id="dbbc4-293">27-07-2015T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="dbbc4-294">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-294">**Output**:</span></span>

| <span data-ttu-id="dbbc4-295">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-295">LicensePlate</span></span> | <span data-ttu-id="dbbc4-296">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-296">Make</span></span> | <span data-ttu-id="dbbc4-297">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="dbbc4-298">DXE 5291</span></span> |<span data-ttu-id="dbbc4-299">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-299">Honda</span></span> |<span data-ttu-id="dbbc4-300">27-07-2015T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="dbbc4-301">QYF 9358</span></span> |<span data-ttu-id="dbbc4-302">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-302">Honda</span></span> |<span data-ttu-id="dbbc4-303">27-07-2015T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="dbbc4-304">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="dbbc4-305">Ora verifichiamo modifica hello problema e individuare hello prima Auto di un particolare in ogni intervallo di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="dbbc4-306">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-306">LicensePlate</span></span> | <span data-ttu-id="dbbc4-307">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-307">Make</span></span> | <span data-ttu-id="dbbc4-308">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="dbbc4-309">DXE 5291</span></span> |<span data-ttu-id="dbbc4-310">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-310">Honda</span></span> |<span data-ttu-id="dbbc4-311">27-07-2015T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="dbbc4-312">YZK 5704</span></span> |<span data-ttu-id="dbbc4-313">Ford</span><span class="sxs-lookup"><span data-stu-id="dbbc4-313">Ford</span></span> |<span data-ttu-id="dbbc4-314">27-07-2015T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="dbbc4-315">YHN 6970</span></span> |<span data-ttu-id="dbbc4-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-316">Toyota</span></span> |<span data-ttu-id="dbbc4-317">27-07-2015T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="dbbc4-318">QYF 9358</span></span> |<span data-ttu-id="dbbc4-319">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-319">Honda</span></span> |<span data-ttu-id="dbbc4-320">27-07-2015T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="dbbc4-321">MDR 6128</span></span> |<span data-ttu-id="dbbc4-322">BMW</span><span class="sxs-lookup"><span data-stu-id="dbbc4-322">BMW</span></span> |<span data-ttu-id="dbbc4-323">27-07-2015T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="dbbc4-324">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="dbbc4-325">Esempio di query: ultimo evento hello trova in una finestra</span><span class="sxs-lookup"><span data-stu-id="dbbc4-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="dbbc4-326">**Descrizione**: auto ultima ricerca di hello in ogni intervallo di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="dbbc4-327">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-327">**Input**:</span></span>

| <span data-ttu-id="dbbc4-328">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-328">LicensePlate</span></span> | <span data-ttu-id="dbbc4-329">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-329">Make</span></span> | <span data-ttu-id="dbbc4-330">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="dbbc4-331">DXE 5291</span></span> |<span data-ttu-id="dbbc4-332">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-332">Honda</span></span> |<span data-ttu-id="dbbc4-333">27-07-2015T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="dbbc4-334">YZK 5704</span></span> |<span data-ttu-id="dbbc4-335">Ford</span><span class="sxs-lookup"><span data-stu-id="dbbc4-335">Ford</span></span> |<span data-ttu-id="dbbc4-336">27-07-2015T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="dbbc4-337">RMV 8282</span></span> |<span data-ttu-id="dbbc4-338">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-338">Honda</span></span> |<span data-ttu-id="dbbc4-339">27-07-2015T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="dbbc4-340">YHN 6970</span></span> |<span data-ttu-id="dbbc4-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-341">Toyota</span></span> |<span data-ttu-id="dbbc4-342">27-07-2015T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="dbbc4-343">VFE 1616</span></span> |<span data-ttu-id="dbbc4-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-344">Toyota</span></span> |<span data-ttu-id="dbbc4-345">27-07-2015T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="dbbc4-346">QYF 9358</span></span> |<span data-ttu-id="dbbc4-347">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-347">Honda</span></span> |<span data-ttu-id="dbbc4-348">27-07-2015T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="dbbc4-349">MDR 6128</span></span> |<span data-ttu-id="dbbc4-350">BMW</span><span class="sxs-lookup"><span data-stu-id="dbbc4-350">BMW</span></span> |<span data-ttu-id="dbbc4-351">27-07-2015T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="dbbc4-352">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-352">**Output**:</span></span>

| <span data-ttu-id="dbbc4-353">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-353">LicensePlate</span></span> | <span data-ttu-id="dbbc4-354">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-354">Make</span></span> | <span data-ttu-id="dbbc4-355">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="dbbc4-356">VFE 1616</span></span> |<span data-ttu-id="dbbc4-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-357">Toyota</span></span> |<span data-ttu-id="dbbc4-358">27-07-2015T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="dbbc4-359">MDR 6128</span></span> |<span data-ttu-id="dbbc4-360">BMW</span><span class="sxs-lookup"><span data-stu-id="dbbc4-360">BMW</span></span> |<span data-ttu-id="dbbc4-361">27-07-2015T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="dbbc4-362">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="dbbc4-363">**SPIEGAZIONE**: sono disponibili due passaggi nella query hello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="dbbc4-364">Hello prima rileva uno hello più recente timestamp in windows 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="dbbc4-365">join di Hello secondo passaggio hello risultati di query prima di hello con hello originale flusso toofind hello eventi che corrispondono ultimo timestamp hello in ogni finestra.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="dbbc4-366">Esempio di query: rilevare l'assenza di hello di eventi</span><span class="sxs-lookup"><span data-stu-id="dbbc4-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="dbbc4-367">**Descrizione**: verificare che un flusso non abbia un valore corrispondente a determinati criteri.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="dbbc4-368">Ad esempio, 2 automobili consecutive da hello che stesso rendere immesse road casello hello all'interno di hello 90 secondi ultimo?</span><span class="sxs-lookup"><span data-stu-id="dbbc4-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="dbbc4-369">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-369">**Input**:</span></span>

| <span data-ttu-id="dbbc4-370">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-370">Make</span></span> | <span data-ttu-id="dbbc4-371">Targa</span><span class="sxs-lookup"><span data-stu-id="dbbc4-371">LicensePlate</span></span> | <span data-ttu-id="dbbc4-372">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-373">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-373">Honda</span></span> |<span data-ttu-id="dbbc4-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="dbbc4-374">ABC-123</span></span> |<span data-ttu-id="dbbc4-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-376">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-376">Honda</span></span> |<span data-ttu-id="dbbc4-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="dbbc4-377">AAA-999</span></span> |<span data-ttu-id="dbbc4-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-379">Toyota</span></span> |<span data-ttu-id="dbbc4-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="dbbc4-380">DEF-987</span></span> |<span data-ttu-id="dbbc4-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="dbbc4-382">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-382">Honda</span></span> |<span data-ttu-id="dbbc4-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="dbbc4-383">GHI-345</span></span> |<span data-ttu-id="dbbc4-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="dbbc4-385">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-385">**Output**:</span></span>

| <span data-ttu-id="dbbc4-386">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-386">Make</span></span> | <span data-ttu-id="dbbc4-387">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-387">Time</span></span> | <span data-ttu-id="dbbc4-388">Targa auto corrente</span><span class="sxs-lookup"><span data-stu-id="dbbc4-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="dbbc4-389">Targa prima auto</span><span class="sxs-lookup"><span data-stu-id="dbbc4-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="dbbc4-390">Tempo prima auto</span><span class="sxs-lookup"><span data-stu-id="dbbc4-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="dbbc4-391">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-391">Honda</span></span> |<span data-ttu-id="dbbc4-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="dbbc4-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="dbbc4-393">AAA-999</span></span> |<span data-ttu-id="dbbc4-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="dbbc4-394">ABC-123</span></span> |<span data-ttu-id="dbbc4-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="dbbc4-396">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="dbbc4-397">**SPIEGAZIONE**: utilizzare **LAG** toopeek in hello nuovamente un evento flusso di input e ottenere hello **rendere** valore.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="dbbc4-398">Confrontarlo toohello **rendere** hello corrente eventi e output hello se essi sono hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="dbbc4-399">È inoltre possibile utilizzare **LAG** dati tooget su Auto precedente hello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="dbbc4-400">Esempio di query: rilevare la durata di hello tra gli eventi</span><span class="sxs-lookup"><span data-stu-id="dbbc4-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="dbbc4-401">**Descrizione**: trovare hello durata di un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="dbbc4-402">Ad esempio, dato un clickstream web, determinare tempo hello dedicato a una funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="dbbc4-403">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-403">**Input**:</span></span>  

| <span data-ttu-id="dbbc4-404">Utente</span><span class="sxs-lookup"><span data-stu-id="dbbc4-404">User</span></span> | <span data-ttu-id="dbbc4-405">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="dbbc4-405">Feature</span></span> | <span data-ttu-id="dbbc4-406">Evento</span><span class="sxs-lookup"><span data-stu-id="dbbc4-406">Event</span></span> | <span data-ttu-id="dbbc4-407">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="dbbc4-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="dbbc4-408">RightMenu</span></span> |<span data-ttu-id="dbbc4-409">Inizia</span><span class="sxs-lookup"><span data-stu-id="dbbc4-409">Start</span></span> |<span data-ttu-id="dbbc4-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="dbbc4-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="dbbc4-411">RightMenu</span></span> |<span data-ttu-id="dbbc4-412">End</span><span class="sxs-lookup"><span data-stu-id="dbbc4-412">End</span></span> |<span data-ttu-id="dbbc4-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="dbbc4-414">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-414">**Output**:</span></span>  

| <span data-ttu-id="dbbc4-415">Utente</span><span class="sxs-lookup"><span data-stu-id="dbbc4-415">User</span></span> | <span data-ttu-id="dbbc4-416">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="dbbc4-416">Feature</span></span> | <span data-ttu-id="dbbc4-417">Durata</span><span class="sxs-lookup"><span data-stu-id="dbbc4-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="dbbc4-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="dbbc4-418">RightMenu</span></span> |<span data-ttu-id="dbbc4-419">7</span><span class="sxs-lookup"><span data-stu-id="dbbc4-419">7</span></span> |

<span data-ttu-id="dbbc4-420">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="dbbc4-421">**SPIEGAZIONE**: hello utilizzare **ultimo** funzione hello tooretrieve ultima **ora** valore quando il tipo di evento hello **avviare**.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="dbbc4-422">Hello **ultimo** funzione Usa **PARTITION BY [user]** tooindicate che hello risultato viene calcolato per ogni utente univoco.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="dbbc4-423">query Hello dispone di una soglia massima di 1 ora per la differenza di orario hello tra **avviare** e **arrestare** eventi, ma può essere configurato in base alle esigenze **(limite DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="dbbc4-424">Esempio di query: rilevare la durata di hello di una condizione</span><span class="sxs-lookup"><span data-stu-id="dbbc4-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="dbbc4-425">**Descrizione**: individuare la durata di una condizione.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="dbbc4-426">Si supponga, ad esempio, che un bug abbia generato un peso errato per tutte le automobili (oltre 20.000 libbre, pari a 9 tonnellate)</span><span class="sxs-lookup"><span data-stu-id="dbbc4-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="dbbc4-427">Si vuole che la durata di hello toocompute bug hello.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="dbbc4-428">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-428">**Input**:</span></span>

| <span data-ttu-id="dbbc4-429">Casa automobilistica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-429">Make</span></span> | <span data-ttu-id="dbbc4-430">Tempo</span><span class="sxs-lookup"><span data-stu-id="dbbc4-430">Time</span></span> | <span data-ttu-id="dbbc4-431">Peso</span><span class="sxs-lookup"><span data-stu-id="dbbc4-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-432">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-432">Honda</span></span> |<span data-ttu-id="dbbc4-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="dbbc4-434">2000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-434">2000</span></span> |
| <span data-ttu-id="dbbc4-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-435">Toyota</span></span> |<span data-ttu-id="dbbc4-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="dbbc4-437">25000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-437">25000</span></span> |
| <span data-ttu-id="dbbc4-438">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-438">Honda</span></span> |<span data-ttu-id="dbbc4-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="dbbc4-440">26000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-440">26000</span></span> |
| <span data-ttu-id="dbbc4-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-441">Toyota</span></span> |<span data-ttu-id="dbbc4-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="dbbc4-443">25000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-443">25000</span></span> |
| <span data-ttu-id="dbbc4-444">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-444">Honda</span></span> |<span data-ttu-id="dbbc4-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="dbbc4-446">26000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-446">26000</span></span> |
| <span data-ttu-id="dbbc4-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-447">Toyota</span></span> |<span data-ttu-id="dbbc4-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="dbbc4-449">25000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-449">25000</span></span> |
| <span data-ttu-id="dbbc4-450">Honda</span><span class="sxs-lookup"><span data-stu-id="dbbc4-450">Honda</span></span> |<span data-ttu-id="dbbc4-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="dbbc4-452">26000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-452">26000</span></span> |
| <span data-ttu-id="dbbc4-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="dbbc4-453">Toyota</span></span> |<span data-ttu-id="dbbc4-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="dbbc4-455">2000</span><span class="sxs-lookup"><span data-stu-id="dbbc4-455">2000</span></span> |

<span data-ttu-id="dbbc4-456">**Output**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-456">**Output**:</span></span>

| <span data-ttu-id="dbbc4-457">Inizio errore</span><span class="sxs-lookup"><span data-stu-id="dbbc4-457">StartFault</span></span> | <span data-ttu-id="dbbc4-458">Fine errore</span><span class="sxs-lookup"><span data-stu-id="dbbc4-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="dbbc4-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="dbbc4-461">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="dbbc4-462">**SPIEGAZIONE**: utilizzare **LAG** flusso di input hello tooview per 24 ore e cercare istanze where **StartFault** e **StopFault** sono occupati da hello peso < 20000.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="dbbc4-463">Esempio di query: immettere i valori mancanti</span><span class="sxs-lookup"><span data-stu-id="dbbc4-463">Query example: Fill missing values</span></span>
<span data-ttu-id="dbbc4-464">**Descrizione**: per il flusso di hello di eventi con i valori mancanti, generare un flusso di eventi con intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="dbbc4-465">Ad esempio, generare un evento ogni 5 secondi che segnala punto dati hello visualizzato più di recente.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="dbbc4-466">**Input**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-466">**Input**:</span></span>

| <span data-ttu-id="dbbc4-467">t</span><span class="sxs-lookup"><span data-stu-id="dbbc4-467">t</span></span> | <span data-ttu-id="dbbc4-468">value</span><span class="sxs-lookup"><span data-stu-id="dbbc4-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="dbbc4-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="dbbc4-470">1</span><span class="sxs-lookup"><span data-stu-id="dbbc4-470">1</span></span> |
| <span data-ttu-id="dbbc4-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="dbbc4-472">2</span><span class="sxs-lookup"><span data-stu-id="dbbc4-472">2</span></span> |
| <span data-ttu-id="dbbc4-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="dbbc4-474">3</span><span class="sxs-lookup"><span data-stu-id="dbbc4-474">3</span></span> |
| <span data-ttu-id="dbbc4-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="dbbc4-476">4</span><span class="sxs-lookup"><span data-stu-id="dbbc4-476">4</span></span> |
| <span data-ttu-id="dbbc4-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="dbbc4-478">5</span><span class="sxs-lookup"><span data-stu-id="dbbc4-478">5</span></span> |
| <span data-ttu-id="dbbc4-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="dbbc4-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="dbbc4-480">6</span><span class="sxs-lookup"><span data-stu-id="dbbc4-480">6</span></span> |

<span data-ttu-id="dbbc4-481">**Output (prime 10 righe)**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="dbbc4-482">windowend</span><span class="sxs-lookup"><span data-stu-id="dbbc4-482">windowend</span></span> | <span data-ttu-id="dbbc4-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="dbbc4-483">lastevent.t</span></span> | <span data-ttu-id="dbbc4-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="dbbc4-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbbc4-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="dbbc4-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="dbbc4-487">1</span><span class="sxs-lookup"><span data-stu-id="dbbc4-487">1</span></span> |
| <span data-ttu-id="dbbc4-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="dbbc4-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="dbbc4-490">2</span><span class="sxs-lookup"><span data-stu-id="dbbc4-490">2</span></span> |
| <span data-ttu-id="dbbc4-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="dbbc4-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="dbbc4-493">3</span><span class="sxs-lookup"><span data-stu-id="dbbc4-493">3</span></span> |
| <span data-ttu-id="dbbc4-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="dbbc4-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="dbbc4-496">4</span><span class="sxs-lookup"><span data-stu-id="dbbc4-496">4</span></span> |
| <span data-ttu-id="dbbc4-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="dbbc4-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="dbbc4-499">4</span><span class="sxs-lookup"><span data-stu-id="dbbc4-499">4</span></span> |
| <span data-ttu-id="dbbc4-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="dbbc4-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="dbbc4-502">4</span><span class="sxs-lookup"><span data-stu-id="dbbc4-502">4</span></span> |
| <span data-ttu-id="dbbc4-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="dbbc4-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="dbbc4-505">5</span><span class="sxs-lookup"><span data-stu-id="dbbc4-505">5</span></span> |
| <span data-ttu-id="dbbc4-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="dbbc4-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="dbbc4-508">6</span><span class="sxs-lookup"><span data-stu-id="dbbc4-508">6</span></span> |
| <span data-ttu-id="dbbc4-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="dbbc4-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="dbbc4-511">6</span><span class="sxs-lookup"><span data-stu-id="dbbc4-511">6</span></span> |
| <span data-ttu-id="dbbc4-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="dbbc4-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="dbbc4-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="dbbc4-514">6</span><span class="sxs-lookup"><span data-stu-id="dbbc4-514">6</span></span> |

<span data-ttu-id="dbbc4-515">**Soluzione**:</span><span class="sxs-lookup"><span data-stu-id="dbbc4-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="dbbc4-516">**SPIEGAZIONE**: la query seguente genera gli eventi ogni 5 secondi e l'output di hello ultimo evento ricevuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dbbc4-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="dbbc4-517">Hello [finestra Hopping](https://msdn.microsoft.com/library/dn835041.aspx "finestra Hopping - Azure flusso Analitica") durata determina la distanza query hello Indietro Cerca toofind evento più recente di hello (300 secondi in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="dbbc4-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="dbbc4-518">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="dbbc4-518">Get help</span></span>
<span data-ttu-id="dbbc4-519">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="dbbc4-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbbc4-520">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbbc4-520">Next steps</span></span>
* [<span data-ttu-id="dbbc4-521">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="dbbc4-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="dbbc4-522">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbbc4-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="dbbc4-523">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbbc4-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="dbbc4-524">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbbc4-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="dbbc4-525">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="dbbc4-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

