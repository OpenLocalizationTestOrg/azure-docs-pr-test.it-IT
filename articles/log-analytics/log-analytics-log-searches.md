---
title: Trovare dati con ricerche nei log in Log Analytics di Azure | Documentazione Microsoft
description: "Le ricerche nei log permettono di combinare e correlare i dati del computer provenienti da più origini nell'ambiente corrente."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="d0473-103">Trovare dati con ricerche nei log in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d0473-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="d0473-104">Questo articolo descrive le ricerche nei log con l'attuale linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0473-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="d0473-105">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), è consigliabile vedere [Informazioni sulle ricerche log in Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="d0473-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="d0473-106">Un elemento fondamentale di Log Analytics è la funzionalità di ricerca nei log, che permette di combinare e correlare i dati del computer da più origini all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d0473-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="d0473-107">Anche le soluzioni sono basate sulla ricerca log, per offrire metriche specifiche per una particolare area problematica.</span><span class="sxs-lookup"><span data-stu-id="d0473-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="d0473-108">Nella pagina Search è possibile creare una query e quindi, durante la ricerca, filtrare i risultati usando controlli facet.</span><span class="sxs-lookup"><span data-stu-id="d0473-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="d0473-109">È anche possibile creare query avanzate per trasformare, filtrare e creare report sui risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="d0473-110">Le query di ricerca log più comuni sono visualizzate nella maggior parte delle pagine delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="d0473-111">In tutta la console OMS è possibile fare clic sui riquadri o analizzare altri elementi per visualizzarne i dettagli usando la funzionalità di ricerca nei log.</span><span class="sxs-lookup"><span data-stu-id="d0473-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="d0473-112">In questa esercitazione verranno esaminati alcuni esempi per analizzare tutti gli elementi di base quando si usa la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="d0473-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="d0473-113">Si inizierà con esempi semplici e pratici, tali esempi verranno quindi compilati in modo da acquisire informazioni sui casi d'uso pratici relativi all'uso della sintassi per estrarre le informazioni desiderate dai dati.</span><span class="sxs-lookup"><span data-stu-id="d0473-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="d0473-114">Dopo aver acquisito familiarità con le tecniche di ricerca, vedere il [riferimento alla ricerca nei log di Log Analytics](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d0473-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="d0473-115">Usare filtri di base</span><span class="sxs-lookup"><span data-stu-id="d0473-115">Use basic filters</span></span>
<span data-ttu-id="d0473-116">La prima parte di una query di ricerca, quella prima di un carattere di barra verticale "|", è sempre un *filtro*.</span><span class="sxs-lookup"><span data-stu-id="d0473-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="d0473-117">Può essere considerata come una clausola WHERE in TSQL, perché determina *quale* subset di dati estrarre dall'archivio dati di OMS.</span><span class="sxs-lookup"><span data-stu-id="d0473-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="d0473-118">Per la ricerca in un archivio dati è importante specificare le caratteristiche dei dati da estrarre, è quindi normale che una query inizi con la clausola WHERE.</span><span class="sxs-lookup"><span data-stu-id="d0473-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="d0473-119">I filtri più semplici che è possibile usare sono *parole chiave*, ad esempio 'error' o 'timeout' o un nome di computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="d0473-120">Questi tipi di query semplici restituiscono in genere diverse forme di dati all'interno dello stesso set di risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="d0473-121">Questo perché Log Analytics include diversi *tipi* di dati nel sistema.</span><span class="sxs-lookup"><span data-stu-id="d0473-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="d0473-122">Per eseguire una ricerca semplice</span><span class="sxs-lookup"><span data-stu-id="d0473-122">To conduct a simple search</span></span>
1. <span data-ttu-id="d0473-123">Nel portale di OMS, fare clic su **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="d0473-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="d0473-124">![riquadro di ricerca](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="d0473-125">Nel campo delle query digitare `error` e quindi fare clic su **Search**.</span><span class="sxs-lookup"><span data-stu-id="d0473-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="d0473-126">![errore di ricerca](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="d0473-127">Ad esempio, la query per `error` nell'immagine seguente ha restituito 100.000 record **Event** (raccolti da Log Management), 18 record **ConfigurationAlert** (generati da Configuration Assessment) e 12 record **ConfigurationChange** (acquisiti da Change Tracking).</span><span class="sxs-lookup"><span data-stu-id="d0473-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="d0473-128">![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="d0473-129">Questi filtri non sono realmente tipi o classi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="d0473-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="d0473-130">*Type* è semplicemente un tag o una proprietà o una stringa/nome/categoria, collegata a una parte dei dati.</span><span class="sxs-lookup"><span data-stu-id="d0473-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="d0473-131">Alcuni documenti nel sistema vengono contrassegnati come **Type:ConfigurationAlert** e alcuni vengono contrassegnati come **Type:Perf** o **Type:Event** e così via.</span><span class="sxs-lookup"><span data-stu-id="d0473-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="d0473-132">In ogni risultato della ricerca, documento, record o voce vengono visualizzate tutte le proprietà non elaborate e i relativi valori per ciascuno di tali dati ed è possibile usare i nomi dei campi per specificare nel filtro quando si desidera recuperare solo i record il cui campo presenta il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="d0473-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="d0473-133">*Type* è in realtà solo un campo che contiene tutti i record, non è diverso dagli altri campi.</span><span class="sxs-lookup"><span data-stu-id="d0473-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="d0473-134">Ciò è stato stabilito in base al valore del campo Type.</span><span class="sxs-lookup"><span data-stu-id="d0473-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="d0473-135">Quel record avrà una forma o un formato diversi.</span><span class="sxs-lookup"><span data-stu-id="d0473-135">That record will have a different shape or form.</span></span> <span data-ttu-id="d0473-136">Tra l'altro, **Type=Perf** o **Type=Event** è anche la sintassi necessaria per eseguire una query su eventi o dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="d0473-137">È possibile usare i due punti (:) o un segno di uguale (=) dopo il nome del campo e prima del valore.</span><span class="sxs-lookup"><span data-stu-id="d0473-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="d0473-138">**Type:Event** and **Type=Event** hanno un significato equivalente ed è possibile scegliere lo stile preferito.</span><span class="sxs-lookup"><span data-stu-id="d0473-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="d0473-139">Se i record Type=Perf hanno un campo denominato "CounterName", è quindi possibile scrivere una query simile a `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="d0473-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="d0473-140">Questa query fornirà solo i dati sulle prestazioni in cui il nome del contatore delle prestazioni è "% Processor Time".</span><span class="sxs-lookup"><span data-stu-id="d0473-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="d0473-141">Per ricercare i dati sulle prestazioni del tempo del processore</span><span class="sxs-lookup"><span data-stu-id="d0473-141">To search for processor time performance data</span></span>
* <span data-ttu-id="d0473-142">Nel campo della query di ricerca, digitare `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="d0473-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="d0473-143">È inoltre possibile essere più specifici e usare **InstanceName=_'Total'** nella query, che rappresenta un contatore delle prestazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="d0473-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="d0473-144">È possibile anche selezionare un facet e un altro **field:value**.</span><span class="sxs-lookup"><span data-stu-id="d0473-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="d0473-145">Il filtro viene aggiunto automaticamente al filtro dell'utente nella barra di query.</span><span class="sxs-lookup"><span data-stu-id="d0473-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="d0473-146">È possibile visualizzare il risultato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="d0473-146">You can see this in the following image.</span></span> <span data-ttu-id="d0473-147">Viene indicato dove è possibile fare clic per aggiungere **InstanceName:'_Total'** alla query senza digitare nulla.</span><span class="sxs-lookup"><span data-stu-id="d0473-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![facet di ricerca](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="d0473-149">La query diventa `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="d0473-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="d0473-150">In questo esempio non è necessario specificare **Type=Perf** per ottenere questo risultato.</span><span class="sxs-lookup"><span data-stu-id="d0473-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="d0473-151">Dato che i campi CounterName e InstanceName esistono solo per record di Type=Perf, la query è abbastanza specifica per restituire gli stessi risultati della query precedente, più lunga:</span><span class="sxs-lookup"><span data-stu-id="d0473-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="d0473-152">Questo perché tutti i filtri nella query vengono considerati come se fossero collegati dall'operatore *AND* .</span><span class="sxs-lookup"><span data-stu-id="d0473-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="d0473-153">In effetti, quanti più campi vengono aggiunti ai criteri, tanto più i risultati saranno di numero inferiore ma più specifici e complessi.</span><span class="sxs-lookup"><span data-stu-id="d0473-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="d0473-154">Ad esempio, la query `Type=Event EventLog="Windows PowerShell"` è identica a `Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="d0473-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="d0473-155">Restituisce tutti gli eventi a cui è stato effettuato l'accesso e che sono stati raccolti dal registro eventi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0473-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="d0473-156">Se si aggiunge un filtro più volte selezionando ripetutamente lo stesso facet, il problema è puramente descrittivo, potrebbe creare confusione nella barra di ricerca, ma restituisce comunque gli stessi risultati perché l'operatore AND implicito è sempre presente.</span><span class="sxs-lookup"><span data-stu-id="d0473-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="d0473-157">È possibile invertire facilmente l'operatore AND implicito usando un operatore NOT in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="d0473-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="d0473-158">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-158">For example:</span></span>

<span data-ttu-id="d0473-159">`Type:Event NOT(EventLog:"Windows PowerShell")` o l'equivalente `Type=Event EventLog!="Windows PowerShell"` restituisce tutti gli eventi di tutti gli altri log DIVERSI dal log di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0473-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="d0473-160">In alternativa, è possibile usare altri operatori booleani, ad esempio 'OR'.</span><span class="sxs-lookup"><span data-stu-id="d0473-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="d0473-161">La query seguente restituisce i record per cui EventLog è Application OR System.</span><span class="sxs-lookup"><span data-stu-id="d0473-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="d0473-162">Usando la query precedente, si otterranno le voci per entrambi i log nello stesso set di risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="d0473-163">Tuttavia, se si rimuove l'operatore OR lasciando l'operatore implicito AND, la query seguente non produrrà alcun risultato perché non è presente una voce del registro eventi che appartiene a entrambi i log.</span><span class="sxs-lookup"><span data-stu-id="d0473-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="d0473-164">Ogni voce del registro eventi è stata scritta solo in uno dei due log.</span><span class="sxs-lookup"><span data-stu-id="d0473-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="d0473-165">Usare filtri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="d0473-165">Use additional filters</span></span>
<span data-ttu-id="d0473-166">La query seguente restituisce le voci per 2 registri eventi per tutti i computer che hanno inviato dati.</span><span class="sxs-lookup"><span data-stu-id="d0473-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="d0473-168">Se si seleziona uno dei campi o filtri la query viene limitata a un computer specifico, escludendo tutti gli altri.</span><span class="sxs-lookup"><span data-stu-id="d0473-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="d0473-169">La query risultante sarà simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="d0473-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="d0473-170">Questa query equivale alla seguente, a causa dell'operatore AND implicito.</span><span class="sxs-lookup"><span data-stu-id="d0473-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="d0473-171">Ogni query viene considerata nell'ordine esplicito seguente.</span><span class="sxs-lookup"><span data-stu-id="d0473-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="d0473-172">Notare le parentesi.</span><span class="sxs-lookup"><span data-stu-id="d0473-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="d0473-173">Come il campo del registro eventi, è possibile recuperare i dati solo per un set di computer specifici aggiungendo OR.</span><span class="sxs-lookup"><span data-stu-id="d0473-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="d0473-174">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="d0473-175">Analogamente ,la query seguente restituisce **% CPU Time** solo per i due computer selezionati.</span><span class="sxs-lookup"><span data-stu-id="d0473-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="d0473-176">Tipi di campo</span><span class="sxs-lookup"><span data-stu-id="d0473-176">Field types</span></span>
<span data-ttu-id="d0473-177">Quando si creano filtri, è importante comprendere le differenze di utilizzo dei diversi tipi di campi restituiti nelle ricerche di log.</span><span class="sxs-lookup"><span data-stu-id="d0473-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="d0473-178">**I campi ricercabili** sono in blu nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="d0473-179">È possibile usare i campi ricercabili in condizioni di ricerca specifiche per il campo, ad esempio le seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0473-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="d0473-180">**I campi ricercabili a testo libero** vengono visualizzati in grigio nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="d0473-181">Non possono essere usati con le condizioni di ricerca specifiche per il campo come i campi ricercabili.</span><span class="sxs-lookup"><span data-stu-id="d0473-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="d0473-182">La ricerca viene eseguita qui solo quando si esegue una query su tutti i campi, ad esempio nei casi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d0473-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="d0473-183">Operatori booleani</span><span class="sxs-lookup"><span data-stu-id="d0473-183">Boolean operators</span></span>
<span data-ttu-id="d0473-184">Con i campi di data/ora e numerici, è possibile cercare i valori usando *maggiore di*, *minore di* e *minore o uguale a*.</span><span class="sxs-lookup"><span data-stu-id="d0473-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="d0473-185">È possibile usare operatori semplici come >, < , >=, <= , != nella barra di ricerca della query.</span><span class="sxs-lookup"><span data-stu-id="d0473-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="d0473-186">È possibile eseguire una query su un registro eventi specifico per uno specifico periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d0473-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="d0473-187">Ad esempio, le ultime 24 ore viene espresso con la seguente espressione mnemonica.</span><span class="sxs-lookup"><span data-stu-id="d0473-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="d0473-188">Per eseguire la ricerca usando un operatore booleano</span><span class="sxs-lookup"><span data-stu-id="d0473-188">To search using a boolean operator</span></span>
* <span data-ttu-id="d0473-189">Nel campo della query di ricerca, digitare `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="d0473-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="d0473-190">![ricerca con valore booleano](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="d0473-191">Nonostante sia possibile controllare graficamente l'intervallo di tempo, e la maggior parte delle volte si desideri farlo, l'inclusione di un filtro temporale direttamente nella query presenta dei vantaggi.</span><span class="sxs-lookup"><span data-stu-id="d0473-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="d0473-192">Ad esempio, è efficace con i dashboard, in cui è possibile sostituire l'intervallo di tempo per ogni riquadro, indipendentemente dal selettore temporale *globale* nella pagina del dashboard.</span><span class="sxs-lookup"><span data-stu-id="d0473-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="d0473-193">Per altre informazioni, vedere l'argomento relativo alle [questioni di tempo nel dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="d0473-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="d0473-194">Quando si filtra in base al tempo si ottengono risultati per l' *intersezione* dei due periodi di tempo: quello specificato nel portale di OMS (S1) e quello specificato nella query (S2).</span><span class="sxs-lookup"><span data-stu-id="d0473-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![intersezione](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="d0473-196">Ciò significa che se non c'è intersezione tra i periodi di tempo, ad esempio se nel portale di OMS è stata scelta la **settimana corrente** e nella query è stata definita l'**ultima settimana**, non viene visualizzato alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="d0473-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="d0473-197">Gli operatori di confronto usati per il campo TimeGenerated sono utili anche in altre situazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="d0473-198">Ad esempio, con i campi numerici.</span><span class="sxs-lookup"><span data-stu-id="d0473-198">For example, with numeric fields.</span></span>

<span data-ttu-id="d0473-199">Ad esempio, poiché gli avvisi di Configuration Assessment presentano i seguenti valori di gravità:</span><span class="sxs-lookup"><span data-stu-id="d0473-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="d0473-200">0 = Informazioni</span><span class="sxs-lookup"><span data-stu-id="d0473-200">0 = Information</span></span>
* <span data-ttu-id="d0473-201">1 = Avviso</span><span class="sxs-lookup"><span data-stu-id="d0473-201">1 = Warning</span></span>
* <span data-ttu-id="d0473-202">2 = Avviso critico</span><span class="sxs-lookup"><span data-stu-id="d0473-202">2 = Critical</span></span>

<span data-ttu-id="d0473-203">È possibile eseguire una query per avvisi e avvisi critici ed escludere gli avvisi informativi con la query seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="d0473-204">È inoltre possibile usare le query di intervallo.</span><span class="sxs-lookup"><span data-stu-id="d0473-204">You can also use range queries.</span></span> <span data-ttu-id="d0473-205">Ciò significa che è possibile specificare l'inizio e la fine dell'intervallo dei valori in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="d0473-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="d0473-206">Ad esempio, se si desidera conoscere gli eventi del registro eventi di Operations Manager dove EventID è maggiore o uguale a 2100 ma non maggiore di 2199, la query seguente restituirà tali eventi.</span><span class="sxs-lookup"><span data-stu-id="d0473-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="d0473-207">La sintassi dell'intervallo da usare è il separatore di due punti (:), field:value, e *non* il segno di uguale (=).</span><span class="sxs-lookup"><span data-stu-id="d0473-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="d0473-208">Racchiudere le estremità inferiore e superiore dell'intervallo tra parentesi quadre e separarle con due punti (..).</span><span class="sxs-lookup"><span data-stu-id="d0473-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="d0473-209">Modificare i risultati della ricerca</span><span class="sxs-lookup"><span data-stu-id="d0473-209">Manipulate search results</span></span>
<span data-ttu-id="d0473-210">Quando si esegue una ricerca di dati, è opportuno ridefinire la query di ricerca e avere un buon livello di controllo sui risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="d0473-211">Quando i risultati vengono recuperati, è possibile applicare comandi per trasformarli.</span><span class="sxs-lookup"><span data-stu-id="d0473-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="d0473-212">I comandi nelle ricerche di Log Analytics *devono* seguire il carattere di barra verticale (|).</span><span class="sxs-lookup"><span data-stu-id="d0473-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="d0473-213">Un filtro deve essere sempre la prima parte di una stringa di query.</span><span class="sxs-lookup"><span data-stu-id="d0473-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="d0473-214">Definisce il set di dati che si sta usando e quindi "invia" i risultati in un comando.</span><span class="sxs-lookup"><span data-stu-id="d0473-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="d0473-215">È quindi possibile usare il carattere di barra verticale per aggiungere altri comandi.</span><span class="sxs-lookup"><span data-stu-id="d0473-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="d0473-216">Il funzionamento è simile a quello della pipeline di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0473-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="d0473-217">Il linguaggio di ricerca di Log Analytics segue in genere lo stile e le linee guida di PowerShell per semplificare la curva di apprendimento dei professionisti IT grazie a tale somiglianza.</span><span class="sxs-lookup"><span data-stu-id="d0473-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="d0473-218">I comandi hanno nomi di verbi, pertanto è possibile stabilire facilmente quali azioni eseguono.</span><span class="sxs-lookup"><span data-stu-id="d0473-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="d0473-219">Ordina</span><span class="sxs-lookup"><span data-stu-id="d0473-219">Sort</span></span>
<span data-ttu-id="d0473-220">Il comando sort consente di definire l'ordinamento in base a uno o più campi.</span><span class="sxs-lookup"><span data-stu-id="d0473-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="d0473-221">Anche se non viene usato, per impostazione predefinita, viene applicato un ordine decrescente di tempo.</span><span class="sxs-lookup"><span data-stu-id="d0473-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="d0473-222">I risultati più recenti sono sempre nella parte superiore dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="d0473-223">Ciò significa che quando si esegue una ricerca con `Type=Event EventID=1234`, in realtà la query che viene eseguita automaticamente è:</span><span class="sxs-lookup"><span data-stu-id="d0473-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="d0473-224">Questo perché si tratta del tipo di esperienza con cui si ha familiarità nei log,</span><span class="sxs-lookup"><span data-stu-id="d0473-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="d0473-225">ad esempio, nel Visualizzatore eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="d0473-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="d0473-226">È possibile usare il comando Sort per modificare il modo in cui vengono restituiti i risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="d0473-227">Negli esempi riportati di seguito viene illustrato il funzionamento di questo comando.</span><span class="sxs-lookup"><span data-stu-id="d0473-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="d0473-228">Gli esempi semplici sopra riportati illustrano il funzionamento dei comandi: i comandi cambiano la forma dei risultati restituiti dal filtro.</span><span class="sxs-lookup"><span data-stu-id="d0473-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="d0473-229">Limit e top</span><span class="sxs-lookup"><span data-stu-id="d0473-229">Limit and top</span></span>
<span data-ttu-id="d0473-230">Un altro comando meno noto è LIMIT.</span><span class="sxs-lookup"><span data-stu-id="d0473-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="d0473-231">Limit è un verbo di tipo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0473-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="d0473-232">Il comando Limit è, dal punto di vista funzionale, identico al comando TOP.</span><span class="sxs-lookup"><span data-stu-id="d0473-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="d0473-233">Le query seguenti restituiscono gli stessi risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="d0473-234">Per eseguire la ricerca usando il comando top</span><span class="sxs-lookup"><span data-stu-id="d0473-234">To search using top</span></span>
* <span data-ttu-id="d0473-235">Nel campo della query di ricerca, digitare `Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="d0473-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="d0473-236">![top di ricerca](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="d0473-237">Nell'immagine precedente, sono presenti 358.000 record con EventID=600.</span><span class="sxs-lookup"><span data-stu-id="d0473-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="d0473-238">I campi, i facet e i filtri a sinistra mostrano sempre informazioni sui risultati restituiti *dalla parte filtro* della query, ovvero la parte prima di qualsiasi carattere di barra verticale.</span><span class="sxs-lookup"><span data-stu-id="d0473-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="d0473-239">Il riquadro **Risultati** restituisce il risultato più recente, in quanto il comando di esempio ha dato una forma e trasformato i risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="d0473-240">Selezionare</span><span class="sxs-lookup"><span data-stu-id="d0473-240">Select</span></span>
<span data-ttu-id="d0473-241">Il comando SELECT si comporta come Select-Object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0473-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="d0473-242">Restituisce i risultati filtrati che non presentano tutte le relative proprietà originali.</span><span class="sxs-lookup"><span data-stu-id="d0473-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="d0473-243">Al contrario, seleziona solo le proprietà specificate.</span><span class="sxs-lookup"><span data-stu-id="d0473-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="d0473-244">Per eseguire una ricerca usando il comando select</span><span class="sxs-lookup"><span data-stu-id="d0473-244">To run a search using the select command</span></span>
1. <span data-ttu-id="d0473-245">Nella ricerca, digitare `Type=Event` e quindi fare clic su **Search**.</span><span class="sxs-lookup"><span data-stu-id="d0473-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="d0473-246">Fare clic su **+ show more** in uno dei risultati per visualizzare tutte le proprietà dei risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="d0473-247">Selezionare alcune proprietà in modo esplicito, la query viene modificata in `Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="d0473-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="d0473-248">![selezione della ricerca](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="d0473-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="d0473-249">Si tratta di comando particolarmente utile quando si vuole controllare l'output di ricerca e scegliere solo le parti di dati davvero importanti per l'esplorazione, che spesso non corrispondono al record completo.</span><span class="sxs-lookup"><span data-stu-id="d0473-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="d0473-250">Il comando è utile anche quando record di tipo diverso hanno *alcune* proprietà comuni, ma non *tutte*.</span><span class="sxs-lookup"><span data-stu-id="d0473-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="d0473-251">È possibile generare un output simile a una tabella o che funziona bene quando esportato in un file CSV e quindi modificato in Excel.</span><span class="sxs-lookup"><span data-stu-id="d0473-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="d0473-252">Usare il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-252">Use the measure command</span></span>
<span data-ttu-id="d0473-253">MEASURE è uno dei comandi più versatili nelle ricerche di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0473-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="d0473-254">Consente di applicare *funzioni* statistiche ai dati e di aggregare i risultati raggruppati in base a un determinato campo.</span><span class="sxs-lookup"><span data-stu-id="d0473-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="d0473-255">Esistono più funzioni statistiche supportate dal comando Measure.</span><span class="sxs-lookup"><span data-stu-id="d0473-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="d0473-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="d0473-256">Measure count()</span></span>
<span data-ttu-id="d0473-257">La prima funzione statistica da usare e una delle più semplici da comprendere è la funzione *count()* .</span><span class="sxs-lookup"><span data-stu-id="d0473-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="d0473-258">Nei risultati di una query di ricerca, ad esempio `Type=Event`, i filtri, anche denominati facet, vengono visualizzati sul lato sinistro dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="d0473-259">I filtri visualizzano una distribuzione di valori in base a un determinato campo, per i risultati della ricerca eseguita.</span><span class="sxs-lookup"><span data-stu-id="d0473-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="d0473-261">Ad esempio, nell'immagine precedente viene visualizzato il campo **Computer**. Tale campo indica che in quasi 739.000 eventi nei risultati sono presenti 68 valori univoci e distinti per il campo **Computer** in questi record.</span><span class="sxs-lookup"><span data-stu-id="d0473-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="d0473-262">Nel riquadro vengono visualizzati solo i primi 5 valori, che corrispondono ai 5 valori più comuni scritti nel campo **Computer**, ordinati in base al numero di documenti che contengono quel valore specifico in quel campo.</span><span class="sxs-lookup"><span data-stu-id="d0473-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="d0473-263">Nell'immagine è possibile vedere che, di quasi 369.000 eventi, 90.000 provengono dal computer OpsInsights04.contoso.com, 83.000 dal computer DB03.contoso.com e così via.</span><span class="sxs-lookup"><span data-stu-id="d0473-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="d0473-264">Poiché nel riquadro vengono visualizzati solo i primi 5 valori, in che modo è possibile visualizzare tutti i valori?</span><span class="sxs-lookup"><span data-stu-id="d0473-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="d0473-265">Per visualizzare tutti i valori è possibile usare il comando measure con la funzione count().</span><span class="sxs-lookup"><span data-stu-id="d0473-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="d0473-266">Per questa funzione non viene usato alcun parametro.</span><span class="sxs-lookup"><span data-stu-id="d0473-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="d0473-267">È sufficiente specificare il campo in base al quale si desidera eseguire il raggruppamento: in questo caso il campo **Computer** :</span><span class="sxs-lookup"><span data-stu-id="d0473-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="d0473-269">Tuttavia, **Computer** è semplicemente un campo usato *in* tutti i dati: non è coinvolto alcun database relazionale e non esiste alcun oggetto **Computer** separato altrove.</span><span class="sxs-lookup"><span data-stu-id="d0473-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="d0473-270">Solo i valori presenti *nei* dati possono descrivere quale entità ha generato i dati e altre caratteristiche e aspetti dei dati, da qui il termine *facet*.</span><span class="sxs-lookup"><span data-stu-id="d0473-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="d0473-271">Tuttavia, è possibile eseguire il raggruppamento anche in base ad altri campi.</span><span class="sxs-lookup"><span data-stu-id="d0473-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="d0473-272">Poiché i risultati originali di quasi 739.000 eventi inviati al comando measure presentano anche un campo denominato **EventID**, è possibile applicare la stessa tecnica per eseguire il raggruppamento in base a tale campo e ottenere un conteggio di eventi per EventID:</span><span class="sxs-lookup"><span data-stu-id="d0473-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="d0473-273">Se non si è interessati al conteggio record effettivo che contiene un valore specifico, ma si desidera invece solo un elenco di valori, è possibile aggiungere un comando *Select* alla fine e selezionare la prima colonna:</span><span class="sxs-lookup"><span data-stu-id="d0473-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="d0473-274">Quindi, è possibile ottenere risultati più complessi e ordinare in precedenza i risultati nella query o semplicemente selezionare le colonne nella griglia.</span><span class="sxs-lookup"><span data-stu-id="d0473-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="d0473-275">Per eseguire la ricerca con measure count</span><span class="sxs-lookup"><span data-stu-id="d0473-275">To search using measure count</span></span>
* <span data-ttu-id="d0473-276">Nel campo della query di ricerca, digitare `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="d0473-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="d0473-277">Aggiungere `| Select EventID` alla fine della query.</span><span class="sxs-lookup"><span data-stu-id="d0473-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="d0473-278">Infine, aggiungere `| Sort EventID asc` alla fine della query.</span><span class="sxs-lookup"><span data-stu-id="d0473-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="d0473-279">Esistono due aspetti importanti da notare e mettere in evidenza:</span><span class="sxs-lookup"><span data-stu-id="d0473-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="d0473-280">In primo luogo, i risultati visualizzati non sono più i risultati originali non elaborati.</span><span class="sxs-lookup"><span data-stu-id="d0473-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="d0473-281">Sono invece risultati aggregati, essenzialmente gruppi di risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="d0473-282">Questo non è un problema, ma è importante sapere che si interagisce con una forma di dati che è molto diversa dalla forma originale non elaborata che viene creata in tempo reale come risultato della funzione di statistica o di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="d0473-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="d0473-283">In secondo luogo, **Measure count** restituisce attualmente solo i primi 100 risultati distinti.</span><span class="sxs-lookup"><span data-stu-id="d0473-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="d0473-284">Questo limite non si applica alle altre funzioni statistiche.</span><span class="sxs-lookup"><span data-stu-id="d0473-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="d0473-285">Pertanto, in genere è necessario usare un filtro più preciso per cercare elementi specifici, prima di applicare measure count().</span><span class="sxs-lookup"><span data-stu-id="d0473-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="d0473-286">Usare le funzioni max e min con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="d0473-287">Esistono vari scenari in cui è utile usare **Measure Max()** e **Measure Min()**.</span><span class="sxs-lookup"><span data-stu-id="d0473-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="d0473-288">Tuttavia, poiché ciascuna funzione è opposta all'altra, verrà illustrata la funzione Max() e l'utente sperimenterà autonomamente la funzione Min().</span><span class="sxs-lookup"><span data-stu-id="d0473-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="d0473-289">Se si esegue una query per gli eventi di sicurezza, tali eventi hanno una proprietà **Livello** che può variare.</span><span class="sxs-lookup"><span data-stu-id="d0473-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="d0473-290">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-290">For example:</span></span>

```
Type=SecurityEvent
```

![measure count start di ricerca](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="d0473-292">Se si desidera visualizzare il valore massimo per tutti gli eventi di sicurezza di un determinato computer comune, quindi raggrupparli per campo, è possibile usare</span><span class="sxs-lookup"><span data-stu-id="d0473-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![measure max computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="d0473-294">Mostrerà che per i computer che avevano record **Livello**, la maggior parte ha almeno il livello 8, mentre molti avevano un livello 16.</span><span class="sxs-lookup"><span data-stu-id="d0473-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![measure max time generated computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="d0473-296">Questa funzione è adatta ad essere usata con i numeri, ma può essere usata anche con i campi di data/ora.</span><span class="sxs-lookup"><span data-stu-id="d0473-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="d0473-297">È utile per verificare l'ultima data/ora o la data/ora più recente relativa a tutti i dati indicizzati per ciascun computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="d0473-298">Ad esempio: quando è stato segnalato l'evento di sicurezza più recente?</span><span class="sxs-lookup"><span data-stu-id="d0473-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="d0473-299">Usare la funzione avg con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="d0473-300">La funzione statistica Avg() usata con il comando measure consente di calcolare il valore medio per alcuni campi e di raggruppare i risultati in base allo stesso campo o ad un campo diverso.</span><span class="sxs-lookup"><span data-stu-id="d0473-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="d0473-301">Questa funzione è utile in diversi casi, ad esempio con i dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="d0473-302">Si inizierà con i dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-302">We'll start with performance data.</span></span> <span data-ttu-id="d0473-303">Si noti che OMS attualmente raccoglie i contatori delle prestazioni sia per i computer Windows che Linux.</span><span class="sxs-lookup"><span data-stu-id="d0473-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="d0473-304">Per la ricerca di *tutti* i dati sulle prestazioni, la query più semplice è:</span><span class="sxs-lookup"><span data-stu-id="d0473-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="d0473-306">La prima cosa che si noterà è che Log Analytics mostra tre prospettive: Elenco, che mostra i record effettivi dietro i grafici; Tabella, che mostra una vista tabulare dei dati del contatore delle prestazioni; Metriche, che mostra i grafici per i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="d0473-307">Nell'immagine precedente, sono presenti due set di campi contrassegnati che indicano quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d0473-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="d0473-308">Il primo set identifica il nome del contatore delle prestazioni di Windows, il nome dell'oggetto e il nome dell'istanza nel filtro della query.</span><span class="sxs-lookup"><span data-stu-id="d0473-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="d0473-309">Questi sono i campi che probabilmente verranno usati in genere come facet/filtri</span><span class="sxs-lookup"><span data-stu-id="d0473-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="d0473-310">**CounterValue** è il valore effettivo del contatore.</span><span class="sxs-lookup"><span data-stu-id="d0473-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="d0473-311">In questo esempio, il valore è *75*.</span><span class="sxs-lookup"><span data-stu-id="d0473-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="d0473-312">**TimeGenerated** è 12:51, nel formato 24 ore.</span><span class="sxs-lookup"><span data-stu-id="d0473-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="d0473-313">Questa è una visualizzazione delle metriche in un grafico.</span><span class="sxs-lookup"><span data-stu-id="d0473-313">Here's a view of the metrics in a graph.</span></span>

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="d0473-315">Dopo aver acquisito informazioni sulla forma del record Perf e su altre tecniche di ricerca, è possibile usare il comando measure Avg() per aggregare questo tipo di dati numerici.</span><span class="sxs-lookup"><span data-stu-id="d0473-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="d0473-316">Un semplice esempio viene riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0473-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue di ricerca](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="d0473-318">In questo esempio, viene selezionato il contatore delle prestazioni CPU Total Time e la media viene calcolata in base a Computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="d0473-319">Per limitare i risultati alle ultime sei ore, è possibile usare il controllo del filtro temporale o specificarlo nella query come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0473-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="d0473-320">Per eseguire la ricerca tramite la funzione avg con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="d0473-321">Nella casella della query di ricerca, digitare `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`</span><span class="sxs-lookup"><span data-stu-id="d0473-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="d0473-322">È possibile aggregare e correlare i dati *tra* computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="d0473-323">Ad esempio, si supponga di disporre di un set di host in un certo tipo di farm in cui ogni nodo è uguale a qualsiasi altro nodo, tutti i nodi eseguono lo stesso tipo di lavoro e il carico è approssimativamente bilanciato.</span><span class="sxs-lookup"><span data-stu-id="d0473-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="d0473-324">È possibile ottenere tutti i contatori contemporaneamente con la query seguente e ottenere le medie per l'intera farm.</span><span class="sxs-lookup"><span data-stu-id="d0473-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="d0473-325">È possibile iniziare scegliendo i computer con l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="d0473-326">Ora che si dispone dei computer, è possibile selezionare due indicatori delle prestazioni chiave (KPI): % CPU Usage e % Free Disk Space.</span><span class="sxs-lookup"><span data-stu-id="d0473-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="d0473-327">Quindi, quella parte della query diventa:</span><span class="sxs-lookup"><span data-stu-id="d0473-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="d0473-328">Ora è possibile aggiungere computer e contatori con l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="d0473-329">Poiché è stata effettuata una selezione molto specifica, il comando **measure Avg()** può restituire la media non in base al computer ma, all'interno della farm, eseguendo il raggruppamento per CounterName.</span><span class="sxs-lookup"><span data-stu-id="d0473-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="d0473-330">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="d0473-331">Ciò consente una visualizzazione utile e compatta di un paio di indicatori di prestazioni chiave dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d0473-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![avg grouping di ricerca](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="d0473-333">È possibile usare facilmente la query di ricerca in un dashboard.</span><span class="sxs-lookup"><span data-stu-id="d0473-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="d0473-334">Ad esempio, è possibile salvare la query di ricerca e creare un dashboard chiamato *Web Farm KPIs*.</span><span class="sxs-lookup"><span data-stu-id="d0473-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="d0473-335">Per altre informazioni sull'uso dei dashboard, vedere l'articolo relativo alla [creazione di un dashboard personalizzato in Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="d0473-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![avg dashboard di ricerca](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="d0473-337">Usare la funzione sum con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="d0473-338">La funzione sum è simile ad altre funzioni del comando measure.</span><span class="sxs-lookup"><span data-stu-id="d0473-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="d0473-339">È possibile vedere un esempio su come usare la funzione sum nell'argomento relativo alla [ricerca di Log W3C IIS in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0473-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="d0473-340">È possibile usare Max() e Min() con numeri, intervalli di data/ora e stringhe di testo.</span><span class="sxs-lookup"><span data-stu-id="d0473-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="d0473-341">Le stringhe di testo sono ordinate in ordine alfabetico e vengono visualizzate la prima e l'ultima.</span><span class="sxs-lookup"><span data-stu-id="d0473-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="d0473-342">Tuttavia, è possibile usare Sum() con elementi diversi dai campi numerici.</span><span class="sxs-lookup"><span data-stu-id="d0473-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="d0473-343">Questo vale anche per Avg().</span><span class="sxs-lookup"><span data-stu-id="d0473-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="d0473-344">Usare la funzione percentile con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="d0473-345">La funzione percentile è simile a Avg() e Sum() perché può essere usata unicamente per i campi numerici.</span><span class="sxs-lookup"><span data-stu-id="d0473-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="d0473-346">In un campo numerico è possibile usare qualsiasi percentile compreso tra 1 e 99.</span><span class="sxs-lookup"><span data-stu-id="d0473-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="d0473-347">È possibile usare sia il comando**percentile** che il comando **pct**.</span><span class="sxs-lookup"><span data-stu-id="d0473-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="d0473-348">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="d0473-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="d0473-349">Usare il comando where</span><span class="sxs-lookup"><span data-stu-id="d0473-349">Use the where command</span></span>
<span data-ttu-id="d0473-350">Il comando where funziona come un filtro, ma può essere applicato nella pipeline per filtrare ulteriormente i risultati aggregati prodotti da un comando Measure, differentemente dai risultati non elaborati che vengono filtrati all'inizio di una query.</span><span class="sxs-lookup"><span data-stu-id="d0473-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="d0473-351">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="d0473-352">È possibile aggiungere un altro carattere di barra verticale "|" e il comando where per visualizzare solo i computer il cui utilizzo medio della CPU è superiore all'80%, con l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="d0473-353">Se si ha familiarità con Microsoft System Center - Operations Manager, è possibile considerare il comando where in termini di Management Pack.</span><span class="sxs-lookup"><span data-stu-id="d0473-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="d0473-354">Se l'esempio fosse una regola, la prima parte della query sarebbe l'origine dati e il comando where sarebbe il rilevamento della condizione.</span><span class="sxs-lookup"><span data-stu-id="d0473-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="d0473-355">È possibile usare la query come un riquadro in **My Dashboard**, come un monitoraggio di ordinamenti, per verificare se sono presenti CPU di computer sovrautilizzate.</span><span class="sxs-lookup"><span data-stu-id="d0473-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="d0473-356">Per altre informazioni sui dashboard, vedere l'articolo relativo alla [creazione di un dashboard personalizzato in Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="d0473-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="d0473-357">È possibile creare e usare i dashboard anche tramite l'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="d0473-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="d0473-358">Per altre informazioni, vedere la pagina relativa all'[app OMS per dispositivi mobili ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="d0473-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="d0473-359">Nei due riquadri in basso dell'immagine seguente, il monitoraggio viene visualizzato come un elenco e come un numero.</span><span class="sxs-lookup"><span data-stu-id="d0473-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="d0473-360">Essenzialmente, è auspicabile che il numero sia sempre zero e l'elenco sia sempre vuoto.</span><span class="sxs-lookup"><span data-stu-id="d0473-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="d0473-361">In caso contrario, indica una condizione di avviso.</span><span class="sxs-lookup"><span data-stu-id="d0473-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="d0473-362">Se necessario, è possibile usarlo per individuare quali computer sono sotto pressione.</span><span class="sxs-lookup"><span data-stu-id="d0473-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![dashboard mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="d0473-364">Usare l'operatore IN</span><span class="sxs-lookup"><span data-stu-id="d0473-364">Use the in operator</span></span>
<span data-ttu-id="d0473-365">Gli operatori *IN* e *NOT IN* permettono di usare le sottoricerche, ovvero ricerche che includono un'altra ricerca come argomento.</span><span class="sxs-lookup"><span data-stu-id="d0473-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="d0473-366">Sono racchiuse tra parentesi graffe {} all'interno di un'altra ricerca *primaria* o *esterna*.</span><span class="sxs-lookup"><span data-stu-id="d0473-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="d0473-367">Il risultato di una sottoricerca, costituito spesso da un elenco di risultati distinti, viene quindi usato come argomento nella ricerca primaria.</span><span class="sxs-lookup"><span data-stu-id="d0473-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="d0473-368">È possibile usare le sottoricerche per la corrispondenza con subset di dati che non è possibile descrivere direttamente in un'espressione di ricerca, ma che possono essere generati da una ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="d0473-369">Ad esempio, se si vuole usare una sola ricerca per trovare tutti gli eventi da *computer privi di aggiornamenti della sicurezza*, è necessario progettare prima di tutto una sottoricerca che identifichi i *computer privi di aggiornamenti della sicurezza* per poi trovare gli eventi appartenenti a tali host.</span><span class="sxs-lookup"><span data-stu-id="d0473-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="d0473-370">Per specificare i *computer attualmente privi dei necessari aggiornamenti della sicurezza* è possibile usare la query seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="d0473-372">Dopo aver ottenuto l'elenco, la ricerca può essere usata come ricerca interna per inserire l'elenco dei computer in una ricerca esterna, o primaria, che cerca gli eventi relativi a tali computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="d0473-373">A questo scopo, racchiudere tra parentesi la ricerca interna e inserire i risultati come possibili valori per un filtro o un campo nella ricerca esterna usando l'operatore IN.</span><span class="sxs-lookup"><span data-stu-id="d0473-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="d0473-374">La query sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="d0473-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="d0473-376">Si noti anche il filtro temporale usato nella ricerca interna perché System Update Assessment acquisisce uno snapshot di tutti i computer ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="d0473-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="d0473-377">È possibile rendere più leggera e precisa la query interna cercando soltanto un giorno.</span><span class="sxs-lookup"><span data-stu-id="d0473-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="d0473-378">La ricerca esterna usa invece la selezione della data/ora nell'interfaccia utente e recupera gli eventi degli ultimi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="d0473-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="d0473-379">Per altre informazioni sugli operatori temporali, vedere la sezione [Operatori booleani](#boolean-operators) .</span><span class="sxs-lookup"><span data-stu-id="d0473-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="d0473-380">Dato che i risultati della ricerca interna vengono usati solo come valore filtro per quella esterna, è comunque possibile applicare i comandi alla ricerca esterna.</span><span class="sxs-lookup"><span data-stu-id="d0473-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="d0473-381">Ad esempio, è ancora possibile raggruppare gli eventi mostrati sopra con un altro comando measure:</span><span class="sxs-lookup"><span data-stu-id="d0473-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="d0473-383">In genere, la query interna deve essere eseguita rapidamente perché Log Analytics prevede timeout sul lato servizio e anche per ottenere una quantità ridotta di risultati.</span><span class="sxs-lookup"><span data-stu-id="d0473-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="d0473-384">Se la query interna restituisce più risultati, l'elenco dei risultati viene troncato e questo può portare a risultati non corretti restituiti dalla ricerca esterna.</span><span class="sxs-lookup"><span data-stu-id="d0473-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="d0473-385">La ricerca interna attualmente deve fornire risultati *aggregati* .</span><span class="sxs-lookup"><span data-stu-id="d0473-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="d0473-386">In altre parole deve contenere un comando *measure* , perché attualmente non è possibile inserire risultati non elaborati in una ricerca esterna.</span><span class="sxs-lookup"><span data-stu-id="d0473-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="d0473-387">Può essere presente un solo operatore IN e deve essere l'ultimo filtro nella query.</span><span class="sxs-lookup"><span data-stu-id="d0473-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="d0473-388">Non è possibile usare gli operatori OR con più operatori IN. Questo di fatto impedisce l'esecuzione di più sottoricerche. Tenere quindi presente che per ogni ricerca esterna può essere presente una sola ricerca interna o sottoricerca.</span><span class="sxs-lookup"><span data-stu-id="d0473-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="d0473-389">Nonostante queste limitazioni, l'operatore IN permette di eseguire molti tipi di ricerche correlate e consente di definire qualcosa di simile ai gruppi, ad esempio computer, utenti, file o qualunque cosa contengano i campi dei dati.</span><span class="sxs-lookup"><span data-stu-id="d0473-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="d0473-390">Di seguito sono riportati altri esempi:</span><span class="sxs-lookup"><span data-stu-id="d0473-390">Here are more examples:</span></span>

<span data-ttu-id="d0473-391">**Tutti gli aggiornamenti mancanti nei computer in cui è disabilitato l'aggiornamento automatico**</span><span class="sxs-lookup"><span data-stu-id="d0473-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="d0473-392">**Tutti gli eventi di errore dai computer che eseguono SQL Server, in cui viene eseguito SQL Assessment**</span><span class="sxs-lookup"><span data-stu-id="d0473-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="d0473-393">**Tutti gli eventi di sicurezza dai computer che sono controller di dominio, in cui viene eseguito AD Assessment**</span><span class="sxs-lookup"><span data-stu-id="d0473-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="d0473-394">**Quali altri account hanno eseguito l'accesso agli stessi computer a cui si è connesso l'account BACONLAND\jochan?**</span><span class="sxs-lookup"><span data-stu-id="d0473-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="d0473-395">Usare il comando distinct</span><span class="sxs-lookup"><span data-stu-id="d0473-395">Use the distinct command</span></span>
<span data-ttu-id="d0473-396">Come suggerisce il nome, questo comando restituisce un elenco di valori distinct per un campo.</span><span class="sxs-lookup"><span data-stu-id="d0473-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="d0473-397">È estremamente semplice ma molto utile.</span><span class="sxs-lookup"><span data-stu-id="d0473-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="d0473-398">È possibile ottenere lo stesso risultato con il comando measure count(), come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d0473-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="d0473-400">Tuttavia, per ottenere semplicemente un elenco di valori distinct e non il conteggio dei documenti che li contengono, il comando distinct fornisce un output più chiaro e leggibile con una sintassi più breve, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d0473-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="d0473-402">Usare la funzione countdistinct con il comando measure</span><span class="sxs-lookup"><span data-stu-id="d0473-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="d0473-403">La funzione countdistinct conta il numero di valori distinct in ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="d0473-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="d0473-404">Può essere usata, ad esempio, per contare il numero di computer univoci che creano report per ogni tipo:</span><span class="sxs-lookup"><span data-stu-id="d0473-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="d0473-406">Usare il comando measure interval</span><span class="sxs-lookup"><span data-stu-id="d0473-406">Use the measure interval command</span></span>
<span data-ttu-id="d0473-407">La raccolta di dati sulle prestazioni quasi in tempo reale permette di raccogliere e visualizzare qualsiasi contatore delle prestazioni in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0473-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="d0473-408">La semplice query **Type:Perf** restituisce migliaia di grafici delle metriche basati sul numero di contatori e server nell'ambiente di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0473-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="d0473-409">L'aggregazione delle metriche su richiesta permette di esaminare tutte le metriche nell'ambiente a livello generale e di approfondire i dati più granulari in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d0473-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="d0473-410">Si supponga di voler conoscere l'utilizzo medio della CPU in tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="d0473-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="d0473-411">Esaminare l'utilizzo medio della CPU di ogni computer potrebbe non essere utile perché i risultati potrebbero essere livellati.</span><span class="sxs-lookup"><span data-stu-id="d0473-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="d0473-412">Per ottenere informazioni più dettagliate, è possibile aggregare il risultato in blocchi di intervalli di tempo più piccoli ed esaminare una serie temporale da varie dimensioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="d0473-413">Ad esempio, per calcolare la media oraria di utilizzo della CPU tra tutti i computer, è possibile procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0473-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![misura intervallo medio](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="d0473-415">Per impostazione predefinita, questi risultati vengono visualizzati in un grafico a linee interattivo a più serie.</span><span class="sxs-lookup"><span data-stu-id="d0473-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="d0473-416">Il grafico supporta l'attivazione e la disattivazione delle serie con ridimensionamento dell'asse Y, lo zoom e il passaggio del puntatore.</span><span class="sxs-lookup"><span data-stu-id="d0473-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="d0473-417">L'opzione di visualizzazione tabella è ancora disponibile per visualizzare i dati non elaborati, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d0473-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="d0473-418">È anche possibile raggruppare in base ad altri campi.</span><span class="sxs-lookup"><span data-stu-id="d0473-418">You can also group by other fields.</span></span> <span data-ttu-id="d0473-419">In questo esempio vengono esaminati tutti i contatori % per un computer specifico e si vuole conoscere il percentile 70 orario di ogni contatore:</span><span class="sxs-lookup"><span data-stu-id="d0473-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="d0473-420">Un aspetto da sottolineare è che queste query non sono limitate ai contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0473-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="d0473-421">Possono essere applicate a qualsiasi metrica.</span><span class="sxs-lookup"><span data-stu-id="d0473-421">You can apply them to any metric.</span></span> <span data-ttu-id="d0473-422">In questo esempio si esaminano i log di IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="d0473-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="d0473-423">Si vuole conoscere il tempo massimo impiegato in un intervallo di cinque minuti per l'elaborazione di ogni richiesta:</span><span class="sxs-lookup"><span data-stu-id="d0473-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="d0473-424">Usare più aggregazioni in una query</span><span class="sxs-lookup"><span data-stu-id="d0473-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="d0473-425">È possibile specificare più clausole di aggregazione in un comando measure.</span><span class="sxs-lookup"><span data-stu-id="d0473-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="d0473-426">Ognuna di esse può essere associata a un alias in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="d0473-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="d0473-427">Se non viene associata a un alias, il nome del campo risultante sarà la funzione di aggregazione che è stata usata, ad esempio "avg(CounterValue)" per avg(CounterValue).</span><span class="sxs-lookup"><span data-stu-id="d0473-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="d0473-429">Di seguito è riportato un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="d0473-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="d0473-430">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0473-430">Next steps</span></span>
<span data-ttu-id="d0473-431">Per altre informazioni sulle ricerche nei log:</span><span class="sxs-lookup"><span data-stu-id="d0473-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="d0473-432">Usare [Campi personalizzati in Log Analytics](log-analytics-custom-fields.md) per estendere le ricerche nei log.</span><span class="sxs-lookup"><span data-stu-id="d0473-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="d0473-433">Vedere il [riferimento alla ricerca nei log di Log Analytics](log-analytics-search-reference.md) per visualizzare tutti i campi di ricerca e i facet disponibili in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0473-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
