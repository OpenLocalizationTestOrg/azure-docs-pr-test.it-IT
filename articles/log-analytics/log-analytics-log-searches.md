---
title: dati aaaFind con ricerche nei log in Azure Log Analitica | Documenti Microsoft
description: "Ricerche nei log consentono toocombine e correlare i dati dei computer da più origini all'interno dell'ambiente."
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
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="1429d-103">Trovare dati con ricerche nei log in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1429d-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="1429d-104">Questo articolo descrive l'utilizzo del linguaggio di query corrente hello in Log Analitica ricerche nei log.</span><span class="sxs-lookup"><span data-stu-id="1429d-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="1429d-105">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è consigliabile consultare troppo[Understanding log eseguire ricerche nei Log Analitica (nuovo)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="1429d-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="1429d-106">Base hello di Log Analitica è funzionalità di ricerca log hello, che consente toocombine e correlare i dati dei computer da più origini all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="1429d-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="1429d-107">Le soluzioni sono inoltre basate toobring di ricerca di log è metriche specifiche per una particolare area problematica.</span><span class="sxs-lookup"><span data-stu-id="1429d-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="1429d-108">Nella pagina di ricerca hello, è possibile creare una query e quindi quando esegue la ricerca, è possibile filtrare hello risultati usando controlli facet.</span><span class="sxs-lookup"><span data-stu-id="1429d-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="1429d-109">È anche possibile creare query avanzate tootransform, filtro e report sui risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="1429d-110">Le query di ricerca log più comuni sono visualizzate nella maggior parte delle pagine delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="1429d-111">Nella console di OMS hello, è possibile fare clic su riquadri o analizzare elementi tooother tooview dettagli sull'elemento hello utilizzando la ricerca di log.</span><span class="sxs-lookup"><span data-stu-id="1429d-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="1429d-112">In questa esercitazione verranno esaminati esempi toocover tutti elementi fondamentali di hello quando si usa la ricerca di log.</span><span class="sxs-lookup"><span data-stu-id="1429d-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="1429d-113">Viene iniziano con esempi semplici e pratici e quindi compilare su di essi in modo che è possibile ottenere la comprensione di casi d'uso pratici sulla modalità di insights di toouse hello sintassi tooextract hello dai dati hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="1429d-114">Dopo avere acquisito familiarità con le tecniche di ricerca, è possibile esaminare hello [riferimento alla ricerca di log Log Analitica](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1429d-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="1429d-115">Usare filtri di base</span><span class="sxs-lookup"><span data-stu-id="1429d-115">Use basic filters</span></span>
<span data-ttu-id="1429d-116">Hello in primo luogo tooknow è tale hello prima parte di una query di ricerca, prima di qualsiasi "|" carattere di barra verticale, è sempre un *filtro*.</span><span class="sxs-lookup"><span data-stu-id="1429d-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="1429d-117">Si può considerare come una clausola WHERE in TSQL: determina *cosa* subset di dati toopull dall'archivio dati OMS di hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="1429d-118">Ricerca nell'archivio dati hello è importante specificare caratteristiche hello dei dati di hello che si desidera tooextract, pertanto è normale che una query inizi con hello clausola WHERE.</span><span class="sxs-lookup"><span data-stu-id="1429d-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="1429d-119">Hello filtri più semplici è possibile utilizzare sono *parole chiave*, ad esempio 'error' o 'timeout' o un nome di computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="1429d-120">Questi tipi di query semplici restituiscono in genere diverse forme di dati all'interno di hello stesso set di risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="1429d-121">Infatti Log Analitica presenta diversi *tipi* dei dati nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="1429d-122">tooconduct una ricerca semplice</span><span class="sxs-lookup"><span data-stu-id="1429d-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="1429d-123">Nel portale OMS hello, fare clic su **ricerca nei Log**.</span><span class="sxs-lookup"><span data-stu-id="1429d-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="1429d-124">![riquadro di ricerca](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="1429d-125">Nel campo della query hello digitare `error` e quindi fare clic su **ricerca**.</span><span class="sxs-lookup"><span data-stu-id="1429d-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="1429d-126">![errore di ricerca](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="1429d-127">Ad esempio, query di hello per `error` in hello immagine seguente ha restituito 100.000 **evento** record (raccolti da Log Management), 18 **ConfigurationAlert** record (generato dalla configurazione Assessment) e 12 **ConfigurationChange** record (acquisiti da Change Tracking hello).</span><span class="sxs-lookup"><span data-stu-id="1429d-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="1429d-128">![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="1429d-129">Questi filtri non sono realmente tipi o classi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="1429d-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="1429d-130">*Tipo* è semplicemente un tag o una proprietà o una stringa/nome/categoria, che è collegato tooa parte dei dati.</span><span class="sxs-lookup"><span data-stu-id="1429d-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="1429d-131">Alcuni documenti nel sistema hello vengono contrassegnati come **Type: ConfigurationAlert** e alcuni vengono contrassegnati come **tipo: prestazioni**, o **Type: Event**e così via.</span><span class="sxs-lookup"><span data-stu-id="1429d-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="1429d-132">Ogni risultato della ricerca, documento, record o voce vengono visualizzate tutte le proprietà non elaborato di hello e i relativi valori per ciascuno di tali dati, e utilizzare tali toospecify di nomi di campo nel filtro hello quando si desidera che solo i record hello tooretrieve cui campo hello presenta specificato valore.</span><span class="sxs-lookup"><span data-stu-id="1429d-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="1429d-133">*Type* è in realtà solo un campo che contiene tutti i record, non è diverso dagli altri campi.</span><span class="sxs-lookup"><span data-stu-id="1429d-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="1429d-134">Ciò è stato stabilito in base al valore di hello hello del campo di tipo.</span><span class="sxs-lookup"><span data-stu-id="1429d-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="1429d-135">Quel record avrà una forma o un formato diversi.</span><span class="sxs-lookup"><span data-stu-id="1429d-135">That record will have a different shape or form.</span></span> <span data-ttu-id="1429d-136">Tra l'altro, **tipo = Perf**, o **tipo di evento =** è anche hello sintassi che è necessario toolearn tooquery per gli eventi o dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="1429d-137">È possibile utilizzare i due punti (:) o un segno di uguale (=) dopo il nome di campo hello e prima del valore hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="1429d-138">**Type: Event** e **tipo di evento =** sono equivalenti nel significato, è possibile scegliere hello stile desiderato.</span><span class="sxs-lookup"><span data-stu-id="1429d-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="1429d-139">In tal caso, se hello digitare = Perf record hanno un campo denominato 'CounterName', quindi è possibile scrivere una query simile a `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="1429d-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="1429d-140">Questa query fornirà solo i dati sulle prestazioni hello in cui il nome del contatore delle prestazioni di hello è "% Processor Time".</span><span class="sxs-lookup"><span data-stu-id="1429d-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="1429d-141">toosearch per i dati sulle prestazioni di tempo processore</span><span class="sxs-lookup"><span data-stu-id="1429d-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="1429d-142">Nel campo di query di ricerca hello, digitare`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="1429d-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="1429d-143">È anche possibile essere più specifici e usare **InstanceName = _ 'Total'** nella query hello, che rappresenta un contatore delle prestazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="1429d-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="1429d-144">È possibile anche selezionare un facet e un altro **field:value**.</span><span class="sxs-lookup"><span data-stu-id="1429d-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="1429d-145">filtro Hello viene automaticamente aggiunto tooyour filtro nella barra di query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="1429d-146">È possibile vedere questo nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-146">You can see this in hello following image.</span></span> <span data-ttu-id="1429d-147">Viene illustrato dove tooclick tooadd **InstanceName: Total'** toohello query senza digitare nulla.</span><span class="sxs-lookup"><span data-stu-id="1429d-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![facet di ricerca](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="1429d-149">La query diventa `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="1429d-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="1429d-150">In questo esempio, non si dispone di toospecify **tipo = Perf** tooget toothis risultato.</span><span class="sxs-lookup"><span data-stu-id="1429d-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="1429d-151">Poiché hello campi CounterName e InstanceName esistono solo per i record di tipo = Perf, query hello è abbastanza specifico tooreturn hello stessi risultati come hello precedente, più lunga:</span><span class="sxs-lookup"><span data-stu-id="1429d-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="1429d-152">In questo modo tutti i filtri nella query hello hello vengono valutati come in *AND* tra loro.</span><span class="sxs-lookup"><span data-stu-id="1429d-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="1429d-153">In effetti, hello ulteriori campi aggiunti toohello criteri, si ottiene minore, risultati più specifici e complessi.</span><span class="sxs-lookup"><span data-stu-id="1429d-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="1429d-154">Ad esempio, query di hello `Type=Event EventLog="Windows PowerShell"` è identico troppo`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="1429d-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="1429d-155">Restituisce tutti gli eventi che sono stati registrati nel e raccolti dal registro eventi di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="1429d-156">Se si aggiunge un filtro più volte selezionando ripetutamente hello stesso facet, quindi problema hello è puramente descrittivo, potrebbe creare confusione barra di ricerca hello, ma restituisce comunque hello stessi risultati perché l'operatore AND implicito hello è sempre presente.</span><span class="sxs-lookup"><span data-stu-id="1429d-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="1429d-157">È possibile invertire facilmente l'operatore AND implicito hello usando un operatore NOT in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="1429d-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="1429d-158">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-158">For example:</span></span>

<span data-ttu-id="1429d-159">`Type:Event NOT(EventLog:"Windows PowerShell")`o l'equivalente `Type=Event EventLog!="Windows PowerShell"` restituiscono tutti gli eventi da tutti gli altri log che non sono il log di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="1429d-160">In alternativa, è possibile usare altri operatori booleani, ad esempio 'OR'.</span><span class="sxs-lookup"><span data-stu-id="1429d-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="1429d-161">esempio Hello query restituisce i record per cui hello EventLog è Application OR System.</span><span class="sxs-lookup"><span data-stu-id="1429d-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="1429d-162">Utilizza hello di sopra di query, si otterranno le voci per entrambi i log in hello stesso set di risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="1429d-163">Tuttavia, se rimuove hello o lasciando hello operatore implicito AND, quindi hello nella query seguente non produrrà alcun risultato perché non è una voce del registro eventi che appartiene tooBOTH log.</span><span class="sxs-lookup"><span data-stu-id="1429d-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="1429d-164">Ogni voce del registro eventi è stato scritto tooonly uno dei due log hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="1429d-165">Usare filtri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="1429d-165">Use additional filters</span></span>
<span data-ttu-id="1429d-166">Hello nella query seguente restituisce le voci per 2 registri eventi per tutti i computer hello che hanno inviato dati.</span><span class="sxs-lookup"><span data-stu-id="1429d-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="1429d-168">Se si seleziona uno dei campi hello o filtri restringerà hello query tooa computer specifico, escludendo tutti gli altri.</span><span class="sxs-lookup"><span data-stu-id="1429d-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="1429d-169">la query risultante Hello è simile al seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="1429d-170">Che è equivalente toohello seguenti, a causa di hello operatore AND implicito.</span><span class="sxs-lookup"><span data-stu-id="1429d-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="1429d-171">Ogni query viene considerata nell'ordine esplicito seguente hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="1429d-172">Parentesi hello nota.</span><span class="sxs-lookup"><span data-stu-id="1429d-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="1429d-173">Come campo hello del registro eventi, è possibile recuperare i dati solo per un set di computer specifici aggiungendo o.</span><span class="sxs-lookup"><span data-stu-id="1429d-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="1429d-174">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="1429d-175">Analogamente, questa hello seguenti restituiscono query **% CPU Time** per hello selezionato solo due computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="1429d-176">Tipi di campo</span><span class="sxs-lookup"><span data-stu-id="1429d-176">Field types</span></span>
<span data-ttu-id="1429d-177">Quando si creano filtri, è necessario comprendere le differenze di hello durante l'utilizzo di tipi diversi di campi restituiti nelle ricerche di log.</span><span class="sxs-lookup"><span data-stu-id="1429d-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="1429d-178">**I campi ricercabili** sono in blu nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="1429d-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="1429d-179">È possibile utilizzare i campi ricercabili nel campo toohello specifiche condizioni di ricerca come illustrato di seguito hello:</span><span class="sxs-lookup"><span data-stu-id="1429d-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="1429d-180">**I campi ricercabili a testo libero** vengono visualizzati in grigio nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="1429d-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="1429d-181">Non possono essere utilizzate con campo toohello specifiche condizioni di ricerca come campi ricercabili.</span><span class="sxs-lookup"><span data-stu-id="1429d-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="1429d-182">Ricerca solo quando si esegue una query per tutti i campi come illustrato di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="1429d-183">Operatori booleani</span><span class="sxs-lookup"><span data-stu-id="1429d-183">Boolean operators</span></span>
<span data-ttu-id="1429d-184">Con i campi di data/ora e numerici, è possibile cercare i valori usando *maggiore di*, *minore di* e *minore o uguale a*.</span><span class="sxs-lookup"><span data-stu-id="1429d-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="1429d-185">È possibile usare operatori semplici come >, <>, =, < =,! = nella barra di ricerca di query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="1429d-186">È possibile eseguire una query su un registro eventi specifico per uno specifico periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="1429d-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="1429d-187">Ad esempio, hello ultime 24 ore viene espresso con hello seguente espressione mnemonica.</span><span class="sxs-lookup"><span data-stu-id="1429d-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="1429d-188">toosearch usando un operatore booleano</span><span class="sxs-lookup"><span data-stu-id="1429d-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="1429d-189">Nel campo di query di ricerca hello, digitare`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="1429d-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="1429d-190">![ricerca con valore booleano](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="1429d-191">Anche se è possibile controllare hello graficamente l'intervallo di tempo e la maggior parte delle volte in cui è possibile toodo, vi sono vantaggi tooincluding un filtro temporale direttamente nella query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="1429d-192">Ad esempio, è efficace con i dashboard in cui è possibile eseguire l'override di tempo hello per ogni riquadro, indipendentemente dal hello *globale* selettore ora nella pagina dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="1429d-193">Per altre informazioni, vedere l'argomento relativo alle [questioni di tempo nel dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="1429d-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="1429d-194">Quando si Filtra per volta, tenere presente che si ottengano risultati per hello *intersezione* di hello due periodi di tempo: quello specificato nel portale OMS hello (S1) hello e hello quello specificato nella query hello (S2).</span><span class="sxs-lookup"><span data-stu-id="1429d-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![intersezione](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="1429d-196">Ciò significa che, se hello periodi di tempo non si intersecano, ad esempio nel portale OMS hello è stata scelta **questa settimana** e nella query hello in cui si definisce **ultima settimana**, non esiste alcuna intersezione e non è visualizzato alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="1429d-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="1429d-197">Gli operatori di confronto utilizzati per il campo TimeGenerated hello sono utili anche in altre situazioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="1429d-198">Ad esempio, con i campi numerici.</span><span class="sxs-lookup"><span data-stu-id="1429d-198">For example, with numeric fields.</span></span>

<span data-ttu-id="1429d-199">Ad esempio, poiché gli avvisi di Configuration Assessment presentano hello i valori di gravità seguenti:</span><span class="sxs-lookup"><span data-stu-id="1429d-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="1429d-200">0 = Informazioni</span><span class="sxs-lookup"><span data-stu-id="1429d-200">0 = Information</span></span>
* <span data-ttu-id="1429d-201">1 = Avviso</span><span class="sxs-lookup"><span data-stu-id="1429d-201">1 = Warning</span></span>
* <span data-ttu-id="1429d-202">2 = Avviso critico</span><span class="sxs-lookup"><span data-stu-id="1429d-202">2 = Critical</span></span>

<span data-ttu-id="1429d-203">È possibile eseguire una query per gli avvisi critici o avvisi e informativi con hello seguenti query di escludere anche:</span><span class="sxs-lookup"><span data-stu-id="1429d-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="1429d-204">È inoltre possibile usare le query di intervallo.</span><span class="sxs-lookup"><span data-stu-id="1429d-204">You can also use range queries.</span></span> <span data-ttu-id="1429d-205">Ciò significa che è possibile fornire hello inizio e fine dell'intervallo di valori in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="1429d-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="1429d-206">Ad esempio, se si desidera che gli eventi dal registro eventi di Operations Manager hello dove hello EventID è maggiore o uguale too2100 ma non maggiore di 2199, quindi hello query seguente restituirà tali eventi.</span><span class="sxs-lookup"><span data-stu-id="1429d-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="1429d-207">è necessario utilizzare sintassi dell'intervallo hello è separatore: valore del campo di due punti (:) hello e *non* hello segno di uguale (=).</span><span class="sxs-lookup"><span data-stu-id="1429d-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="1429d-208">Estremità di hello inferiore e superiore dell'intervallo di hello di racchiudere tra parentesi quadre e separarle con due punti (.).</span><span class="sxs-lookup"><span data-stu-id="1429d-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="1429d-209">Modificare i risultati della ricerca</span><span class="sxs-lookup"><span data-stu-id="1429d-209">Manipulate search results</span></span>
<span data-ttu-id="1429d-210">Quando si esegue una ricerca per i dati, verranno desidera toorefine query di ricerca e avere un buon livello di controllo sui risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="1429d-211">Quando vengono recuperati i risultati, è possibile applicare comandi tootransform li.</span><span class="sxs-lookup"><span data-stu-id="1429d-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="1429d-212">I comandi nelle ricerche Log Analitica *deve* seguire hello carattere di barra verticale (|).</span><span class="sxs-lookup"><span data-stu-id="1429d-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="1429d-213">Un filtro deve essere sempre prima parte di hello di una stringa di query.</span><span class="sxs-lookup"><span data-stu-id="1429d-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="1429d-214">Definisce il set di dati hello in uso e quindi "Invia" i risultati in un comando.</span><span class="sxs-lookup"><span data-stu-id="1429d-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="1429d-215">È quindi possibile utilizzare comandi aggiuntivi di hello pipe tooadd.</span><span class="sxs-lookup"><span data-stu-id="1429d-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="1429d-216">Si tratta della pipeline di Windows PowerShell toohello simile a regime di controllo libero.</span><span class="sxs-lookup"><span data-stu-id="1429d-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="1429d-217">In generale, il linguaggio di ricerca Log Analitica hello Cerca toomake di stile e le linee guida di PowerShell toofollow it simili toohello IT Pro e tooease hello curva di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="1429d-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="1429d-218">I comandi hanno nomi di verbi, pertanto è possibile stabilire facilmente quali azioni eseguono.</span><span class="sxs-lookup"><span data-stu-id="1429d-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="1429d-219">Ordina</span><span class="sxs-lookup"><span data-stu-id="1429d-219">Sort</span></span>
<span data-ttu-id="1429d-220">comando sort Hello consente hello toodefine ordinamento da uno o più campi.</span><span class="sxs-lookup"><span data-stu-id="1429d-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="1429d-221">Anche se non viene usato, per impostazione predefinita, viene applicato un ordine decrescente di tempo.</span><span class="sxs-lookup"><span data-stu-id="1429d-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="1429d-222">risultati più recenti Hello sono sempre nella parte superiore di hello dei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="1429d-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="1429d-223">Ciò significa che quando si esegue una ricerca con `Type=Event EventID=1234`, in realtà la query che viene eseguita automaticamente è:</span><span class="sxs-lookup"><span data-stu-id="1429d-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="1429d-224">Ciò avviene perché è il tipo di hello di esperienza con che cui si ha familiarità nei log.</span><span class="sxs-lookup"><span data-stu-id="1429d-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="1429d-225">Ad esempio, nel Visualizzatore eventi di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="1429d-226">È possibile utilizzare l'ordinamento toochange hello modo risultati vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="1429d-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="1429d-227">Hello esempi seguenti viene illustrato il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="1429d-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="1429d-228">Hello esempi semplici sopra illustrano il funzionano dei comandi - cambiano la forma hello dei risultati hello hello filtro restituito.</span><span class="sxs-lookup"><span data-stu-id="1429d-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="1429d-229">Limit e top</span><span class="sxs-lookup"><span data-stu-id="1429d-229">Limit and top</span></span>
<span data-ttu-id="1429d-230">Un altro comando meno noto è LIMIT.</span><span class="sxs-lookup"><span data-stu-id="1429d-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="1429d-231">Limit è un verbo di tipo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1429d-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="1429d-232">Limite è comando TOP toohello funzionalmente identico.</span><span class="sxs-lookup"><span data-stu-id="1429d-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="1429d-233">Hello query seguenti restituiscono hello stessi risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="1429d-234">utilizzo di top toosearch</span><span class="sxs-lookup"><span data-stu-id="1429d-234">toosearch using top</span></span>
* <span data-ttu-id="1429d-235">Nel campo di query di ricerca hello, digitare`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="1429d-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="1429d-236">![top di ricerca](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="1429d-237">Nell'immagine hello precedente, sono presenti migliaia di 358 record con EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="1429d-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="1429d-238">Hello campi e facet filtri su hello lasciato sempre mostrano informazioni sui risultati di hello *dalla parte filtro hello* di query hello, che fa parte di hello prima di qualsiasi carattere di barra verticale.</span><span class="sxs-lookup"><span data-stu-id="1429d-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="1429d-239">Hello **risultati** riquadro restituisce solo il risultato di hello 1 più recente, perché il comando di esempio hello ha definito e trasformato i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="1429d-240">Selezionare</span><span class="sxs-lookup"><span data-stu-id="1429d-240">Select</span></span>
<span data-ttu-id="1429d-241">comando SELECT Hello si comporta come Select-Object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1429d-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="1429d-242">Restituisce i risultati filtrati che non presentano tutte le relative proprietà originali.</span><span class="sxs-lookup"><span data-stu-id="1429d-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="1429d-243">Al contrario, seleziona solo le proprietà hello specificate.</span><span class="sxs-lookup"><span data-stu-id="1429d-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="1429d-244">toorun una ricerca usando il comando select hello</span><span class="sxs-lookup"><span data-stu-id="1429d-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="1429d-245">Nella ricerca, digitare `Type=Event` e quindi fare clic su **Search**.</span><span class="sxs-lookup"><span data-stu-id="1429d-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="1429d-246">Fare clic su **+ Mostra altre** in uno dei tooview risultati hello tutte le proprietà di hello che hello risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="1429d-247">Selezionandone alcune in modo esplicito e hello le modifiche alle query troppo`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="1429d-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="1429d-248">![select di ricerca](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="1429d-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="1429d-249">Questo comando è particolarmente utile quando si desidera toocontrol output di ricerca e scegliere hello porzioni di dati davvero importanti per l'esplorazione, che spesso non record completo hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="1429d-250">Il comando è utile anche quando record di tipo diverso hanno *alcune* proprietà comuni, ma non *tutte*.</span><span class="sxs-lookup"><span data-stu-id="1429d-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="1429d-251">È possibile generare un output simile a una tabella o funziona bene quando esportato file CSV tooa e quindi modificato in Excel.</span><span class="sxs-lookup"><span data-stu-id="1429d-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="1429d-252">Usare il comando di measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-252">Use hello measure command</span></span>
<span data-ttu-id="1429d-253">MEASURE è uno dei comandi più versatili di hello nelle ricerche Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="1429d-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="1429d-254">Consente di tooapply statistica *funzioni* tooyour dati e aggregare i risultati raggruppati in base a un determinato campo.</span><span class="sxs-lookup"><span data-stu-id="1429d-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="1429d-255">Esistono più funzioni statistiche supportate dal comando Measure.</span><span class="sxs-lookup"><span data-stu-id="1429d-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="1429d-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="1429d-256">Measure count()</span></span>
<span data-ttu-id="1429d-257">Hello prima funzione statistica toowork con, e uno di toounderstand più semplice hello è hello *Count ()* (funzione).</span><span class="sxs-lookup"><span data-stu-id="1429d-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="1429d-258">Nei risultati di una query di ricerca, ad esempio `Type=Event`, i filtri, denominati anche facet su hello il lato sinistro di risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="1429d-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="1429d-259">Hello filtri visualizzano una distribuzione di valori da un determinato campo, per risultati hello hello ricerca eseguita.</span><span class="sxs-lookup"><span data-stu-id="1429d-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="1429d-261">Ad esempio, nei hello immagine sopra si noterà hello **Computer** campo indica che in hello quasi 739 migliaia di eventi nei risultati di hello, esistono 68 valori univoci e distinti per hello **Computer** campo in questi record.</span><span class="sxs-lookup"><span data-stu-id="1429d-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="1429d-262">Hello riquadro vengono visualizzati solo hello i primi 5, che sono hello 5 i valori più comuni che vengono scritti in hello **Computer** campi), ordinati in base al numero di hello di documenti che contengono quel valore specifico in quel campo.</span><span class="sxs-lookup"><span data-stu-id="1429d-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="1429d-263">Nell'immagine hello si noterà che, quasi 369 migliaia di eventi, delle migliaia 90 provengono dal computer OpsInsights04.contoso.com hello, mille 83 dal computer DB03.contoso.com hello e così via.</span><span class="sxs-lookup"><span data-stu-id="1429d-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="1429d-264">Cosa accade se si desidera toosee tutti i valori, poiché hello riquadro vengono visualizzati solo hello solo i primi 5?</span><span class="sxs-lookup"><span data-stu-id="1429d-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="1429d-265">Ovvero le misure hello comando è possibile eseguire con funzione di hello Count ().</span><span class="sxs-lookup"><span data-stu-id="1429d-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="1429d-266">Per questa funzione non viene usato alcun parametro.</span><span class="sxs-lookup"><span data-stu-id="1429d-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="1429d-267">È sufficiente specificare il campo hello mediante il quale si desidera toogroup da – hello **Computer** in questo caso:</span><span class="sxs-lookup"><span data-stu-id="1429d-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="1429d-269">Tuttavia, **Computer** è semplicemente un campo usato *in* tutti i dati: non è coinvolto alcun database relazionale e non esiste alcun oggetto **Computer** separato altrove.</span><span class="sxs-lookup"><span data-stu-id="1429d-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="1429d-270">Hello solo valori *in* hello dati possono descrivere quale entità ha generato e un numero di altre caratteristiche e aspetti dei dati hello: hello pertanto termine *facet*.</span><span class="sxs-lookup"><span data-stu-id="1429d-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="1429d-271">Tuttavia, è possibile eseguire il raggruppamento anche in base ad altri campi.</span><span class="sxs-lookup"><span data-stu-id="1429d-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="1429d-272">Poiché i risultati originali di hello di quasi 739 migliaia di eventi inviati comando measure hello presentano anche un campo denominato **EventID**, è possibile applicare hello stessa tecnica toogroup base a tale campo e ottenere un conteggio di eventi per EventID:</span><span class="sxs-lookup"><span data-stu-id="1429d-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="1429d-273">Se non si è interessati Conteggio record effettivo hello che contengono un valore specifico, ma invece se si vuole solo un elenco di hello gli stessi valori, è possibile aggiungere un *selezionare* comando alla fine hello e nella prima colonna hello basta selezionare:</span><span class="sxs-lookup"><span data-stu-id="1429d-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="1429d-274">È quindi possibile ottenere risultati più complessi e ordinare in precedenza hello risultati query hello oppure è possibile fare semplicemente clic colonne hello nella griglia hello troppo.</span><span class="sxs-lookup"><span data-stu-id="1429d-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="1429d-275">toosearch con measure count</span><span class="sxs-lookup"><span data-stu-id="1429d-275">toosearch using measure count</span></span>
* <span data-ttu-id="1429d-276">Nel campo di query di ricerca hello, digitare`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="1429d-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="1429d-277">Aggiungere `| Select EventID` toohello fine della query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="1429d-278">Infine, aggiungere `| Sort EventID asc` toohello fine della query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="1429d-279">Esistono due aspetti importanti toonotice e mettere in evidenza:</span><span class="sxs-lookup"><span data-stu-id="1429d-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="1429d-280">In primo luogo, hello risultati visualizzati non sono risultati originali non elaborati di hello più.</span><span class="sxs-lookup"><span data-stu-id="1429d-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="1429d-281">Sono invece risultati aggregati, essenzialmente gruppi di risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="1429d-282">Ciò non rappresenta un problema, ma è importante comprendere che si interagisce con una forma di dati che è molto diversa da hello forma originale non elaborata che viene creata in tempo reale di hello come risultato di funzione di aggregazione/statistica hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="1429d-283">In secondo luogo, **misura Conteggio** attualmente restituisce hello solo primi 100 risultati distinti.</span><span class="sxs-lookup"><span data-stu-id="1429d-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="1429d-284">Questo limite non si applica toohello altre funzioni statistiche.</span><span class="sxs-lookup"><span data-stu-id="1429d-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="1429d-285">In tal caso, in genere è necessario toouse un toosearch prima di filtro più preciso per elementi specifici prima di applicare measure Count ().</span><span class="sxs-lookup"><span data-stu-id="1429d-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="1429d-286">Utilizzare le funzioni max e min hello con il comando measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="1429d-287">Esistono vari scenari in cui è utile usare **Measure Max()** e **Measure Min()**.</span><span class="sxs-lookup"><span data-stu-id="1429d-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="1429d-288">Tuttavia, poiché ciascuna funzione è opposta all'altra, verrà illustrata la funzione Max() e l'utente sperimenterà autonomamente la funzione Min().</span><span class="sxs-lookup"><span data-stu-id="1429d-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="1429d-289">Se si esegue una query per gli eventi di sicurezza, tali eventi hanno una proprietà **Livello** che può variare.</span><span class="sxs-lookup"><span data-stu-id="1429d-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="1429d-290">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-290">For example:</span></span>

```
Type=SecurityEvent
```

![measure count start di ricerca](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="1429d-292">Se si desidera valore più alto di hello tooview per sicurezza hello tutti gli eventi di un determinato Computer comune, hello campo Raggruppa per, è possibile utilizzare</span><span class="sxs-lookup"><span data-stu-id="1429d-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![measure max computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="1429d-294">Che verrà visualizzato per i computer che avevano hello **livello** record, la maggior parte di essi hanno almeno 8, a livello molti ha un livello di 16.</span><span class="sxs-lookup"><span data-stu-id="1429d-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![measure max time generated computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="1429d-296">Questa funzione è adatta ad essere usata con i numeri, ma può essere usata anche con i campi di data/ora.</span><span class="sxs-lookup"><span data-stu-id="1429d-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="1429d-297">È utile toocheck per hello ultimo o timestamp più recente per tutti i dati indicizzati per ciascun computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="1429d-298">Ad esempio: quando è stato evento di sicurezza più recente di hello segnalato per ciascuna macchina?</span><span class="sxs-lookup"><span data-stu-id="1429d-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="1429d-299">Funzione avg hello con il comando measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="1429d-300">valore medio di hello toocalculate per alcuni campi consente Hello utilizzata con misura la funzione statistica AVG () e gruppo di risultati da hello stesso o un altro campo.</span><span class="sxs-lookup"><span data-stu-id="1429d-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="1429d-301">Questa funzione è utile in diversi casi, ad esempio con i dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="1429d-302">Si inizierà con i dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-302">We'll start with performance data.</span></span> <span data-ttu-id="1429d-303">Si noti che OMS attualmente raccoglie i contatori delle prestazioni sia per i computer Windows che Linux.</span><span class="sxs-lookup"><span data-stu-id="1429d-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="1429d-304">toosearch per *tutti* dati sulle prestazioni, la query più semplice di hello è:</span><span class="sxs-lookup"><span data-stu-id="1429d-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="1429d-306">Hello prima cosa da notare è che Analitica Log mostra tre prospettive: elenco che mostra che mostra i record effettivi hello dietro i grafici hello; Tabella che mostra una vista tabulare di dati del contatore delle prestazioni. e la metrica che mostra i grafici per hello contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="1429d-307">Nell'immagine hello sopra, sono disponibili due set di campi contrassegnati che indicano l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="1429d-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="1429d-308">Hello primo set identifica nome contatore delle prestazioni di Windows, il nome di oggetto e nome dell'istanza nel filtro di query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="1429d-309">Questi sono campi hello è probabilmente verranno in genere utilizzato come facet/filtri</span><span class="sxs-lookup"><span data-stu-id="1429d-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="1429d-310">**CounterValue** è hello valore effettivo del contatore hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="1429d-311">In questo esempio, il valore di hello è *75*.</span><span class="sxs-lookup"><span data-stu-id="1429d-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="1429d-312">**TimeGenerated** è 12:51, nel formato 24 ore.</span><span class="sxs-lookup"><span data-stu-id="1429d-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="1429d-313">Di seguito è riportata una visualizzazione delle metriche hello in un grafico.</span><span class="sxs-lookup"><span data-stu-id="1429d-313">Here's a view of hello metrics in a graph.</span></span>

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="1429d-315">Dopo la lettura di informazioni sulla forma di record prestazioni hello e, con informazioni sulle altre tecniche di ricerca, è possibile utilizzare questo tipo di dati numerici misura tooaggregate AVG ().</span><span class="sxs-lookup"><span data-stu-id="1429d-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="1429d-316">Un semplice esempio viene riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1429d-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue di ricerca](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="1429d-318">In questo esempio si seleziona contatore delle prestazioni CPU Total Time hello e Media dal Computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="1429d-319">Se si desidera toonarrow verso il basso il hello tooonly risultati ultima 6 ore, è possibile utilizzare il controllo di filtro ora hello o specificare la query come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1429d-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="1429d-320">funzione avg hello con il comando measure hello toosearch</span><span class="sxs-lookup"><span data-stu-id="1429d-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="1429d-321">Nella casella Search hello, digitare `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="1429d-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="1429d-322">È possibile aggregare e correlare i dati *tra* computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="1429d-323">Ad esempio, si supponga di disporre di un set di host in un certo tipo di farm in cui ogni nodo è uguale tooany altro e avviene solo hello tutti stesso tipo di lavoro e il carico è approssimativamente bilanciato.</span><span class="sxs-lookup"><span data-stu-id="1429d-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="1429d-324">È possibile ottenere i contatori che tutti contemporaneamente con hello seguente query e ottenere le medie per l'intera farm hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="1429d-325">È possibile iniziare scegliendo i computer hello con hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1429d-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="1429d-326">Ora che sono presenti computer hello, si desidera anche solo tooselect due gli indicatori delle prestazioni chiave (KPI): % CPU Usage e % spazio libero su disco.</span><span class="sxs-lookup"><span data-stu-id="1429d-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="1429d-327">In tal caso, quella parte della query hello diventa:</span><span class="sxs-lookup"><span data-stu-id="1429d-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="1429d-328">È ora possibile aggiungere computer e contatori con hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1429d-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="1429d-329">Poiché si dispone di una selezione molto specifica, hello **misurare AVG ()** comando può restituire hello Media non dal computer, ma la farm di hello, eseguendo il raggruppamento per CounterName.</span><span class="sxs-lookup"><span data-stu-id="1429d-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="1429d-330">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="1429d-331">Ciò consente una visualizzazione utile e compatta di un paio di indicatori di prestazioni chiave dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="1429d-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![avg grouping di ricerca](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="1429d-333">In un dashboard, è possibile utilizzare facilmente query di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="1429d-334">Ad esempio, è possibile salvare la query di ricerca hello e creare un dashboard da esso denominato *gli indicatori KPI di Web Farm*.</span><span class="sxs-lookup"><span data-stu-id="1429d-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="1429d-335">toolearn ulteriori informazioni sull'utilizzo di dashboard, vedere [creare un dashboard personalizzato in Log Analitica](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="1429d-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![avg dashboard di ricerca](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="1429d-337">Utilizzare la funzione di somma hello con il comando measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="1429d-338">Funzione sum Hello è simile tooother funzioni del comando measure hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="1429d-339">È possibile visualizzare un esempio su come toouse hello funzione sum [ricerca nei log di IIS W3C in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="1429d-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="1429d-340">È possibile usare Max() e Min() con numeri, intervalli di data/ora e stringhe di testo.</span><span class="sxs-lookup"><span data-stu-id="1429d-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="1429d-341">Le stringhe di testo sono ordinate in ordine alfabetico e vengono visualizzate la prima e l'ultima.</span><span class="sxs-lookup"><span data-stu-id="1429d-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="1429d-342">Tuttavia, è possibile usare Sum() con elementi diversi dai campi numerici.</span><span class="sxs-lookup"><span data-stu-id="1429d-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="1429d-343">Questo vale anche tooAvg().</span><span class="sxs-lookup"><span data-stu-id="1429d-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="1429d-344">Utilizzare la funzione di percentile hello con il comando measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="1429d-345">funzione percentile Hello è simile tooAvg() e SUM () in quanto è possibile utilizzare solo per i campi numerici.</span><span class="sxs-lookup"><span data-stu-id="1429d-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="1429d-346">È possibile utilizzare qualsiasi percentile tra 1 too99 in un campo numerico.</span><span class="sxs-lookup"><span data-stu-id="1429d-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="1429d-347">È possibile usare sia il comando**percentile** che il comando **pct**.</span><span class="sxs-lookup"><span data-stu-id="1429d-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="1429d-348">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="1429d-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="1429d-349">Utilizzare hello dove comando</span><span class="sxs-lookup"><span data-stu-id="1429d-349">Use hello where command</span></span>
<span data-ttu-id="1429d-350">Hello in cui funziona come un filtro, ma può essere applicato nel filtro di hello pipeline toofurther aggregati i risultati prodotti da un comando Measure, come tooraw anziché i risultati vengono filtrati all'inizio di hello di una query.</span><span class="sxs-lookup"><span data-stu-id="1429d-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="1429d-351">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="1429d-352">È possibile aggiungere un'altra barra verticale "|" hello e carattere comando tooonly dove ottenere i computer il cui utilizzo medio della CPU è superiore all'80%, con hello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="1429d-353">Se si ha familiarità con Microsoft System Center - Operations Manager, è possibile pensare di hello dove comando in termini di management pack.</span><span class="sxs-lookup"><span data-stu-id="1429d-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="1429d-354">Se l'esempio hello fosse una regola, hello prima parte della query hello sarebbe hello e origine dati hello in cui comando sarebbe rilevamento della condizione hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="1429d-355">È possibile utilizzare query hello come un riquadro in **My Dashboard**, come un monitoraggio di ordinamento, toosee quando computer CPU è sovrautilizzato.</span><span class="sxs-lookup"><span data-stu-id="1429d-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="1429d-356">toolearn altre informazioni sui dashboard, vedere [creare un dashboard personalizzato in Log Analitica](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="1429d-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="1429d-357">È anche possibile creare e utilizzare i dashboard con hello app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="1429d-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="1429d-358">Per altre informazioni, vedere la pagina relativa all'[app OMS per dispositivi mobili ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="1429d-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="1429d-359">Nei riquadri di inferiore due hello di hello seguente immagine, è possibile vedere Monitoraggio hello visualizzati un elenco e come un numero.</span><span class="sxs-lookup"><span data-stu-id="1429d-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="1429d-360">In pratica, sempre necessario hello numero toobe zero e hello toobe elenco vuoto.</span><span class="sxs-lookup"><span data-stu-id="1429d-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="1429d-361">In caso contrario, indica una condizione di avviso.</span><span class="sxs-lookup"><span data-stu-id="1429d-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="1429d-362">Se necessario, è possibile utilizzare tootake esaminare quali computer sono sotto pressione.</span><span class="sxs-lookup"><span data-stu-id="1429d-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![dashboard mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="1429d-364">Utilizzare hello in (operatore)</span><span class="sxs-lookup"><span data-stu-id="1429d-364">Use hello in operator</span></span>
<span data-ttu-id="1429d-365">Hello *IN* (operatore), insieme a *NOT IN* consente le ricerche secondarie toouse, ovvero ricerche che includono un'altra ricerca come argomento.</span><span class="sxs-lookup"><span data-stu-id="1429d-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="1429d-366">Sono racchiuse tra parentesi graffe {} all'interno di un'altra ricerca *primaria* o *esterna*.</span><span class="sxs-lookup"><span data-stu-id="1429d-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="1429d-367">il risultato di Hello di una ricerca secondaria, spesso un elenco di risultati distinti, viene quindi usato come argomento nella ricerca primaria.</span><span class="sxs-lookup"><span data-stu-id="1429d-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="1429d-368">È possibile utilizzare le ricerche secondarie toomatch subset di dati che non è possibile descrivere direttamente in un'espressione di ricerca, ma che possono essere generati da una ricerca.</span><span class="sxs-lookup"><span data-stu-id="1429d-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="1429d-369">Ad esempio, se si è interessati all'uso di tutti gli eventi da una ricerca toofind *computer privi di aggiornamenti della sicurezza*, è necessario toodesign una ricerca secondaria che identifichi *computer privi di aggiornamenti della sicurezza*  prima di trovare gli eventi appartenenti toothose host.</span><span class="sxs-lookup"><span data-stu-id="1429d-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="1429d-370">In tal caso, è possibile esprimere *computer attualmente privi di necessari aggiornamenti della sicurezza* con hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="1429d-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="1429d-372">Dopo aver creato elenco hello, è possibile utilizzare ricerca hello come un elenco di hello toofeed ricerca interna dei computer in una ricerca esterna (primaria) che cercherà gli eventi per tali computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="1429d-373">Questo caso, racchiudere la ricerca interna hello tra parentesi graffe e inserire i risultati come possibili valori per un filtro/campo nella ricerca esterna di hello utilizzando l'operatore IN hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="1429d-374">query Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1429d-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="1429d-376">Anche tempo hello notifica filtro usato nella ricerca interna hello perché hello System Update Assessment esegue uno snapshot di tutti i computer ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="1429d-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="1429d-377">È possibile rendere la query interna di hello più leggera e precisa cercando solo un giorno.</span><span class="sxs-lookup"><span data-stu-id="1429d-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="1429d-378">ricerca esterna Hello Usa invece la selezione di tempo hello nell'interfaccia utente di hello, recuperando gli eventi da hello ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="1429d-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="1429d-379">Per altre informazioni sugli operatori temporali, vedere la sezione [Operatori booleani](#boolean-operators) .</span><span class="sxs-lookup"><span data-stu-id="1429d-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="1429d-380">Perché si usa solo hello i risultati della ricerca interna di hello come un valore di filtro per hello esterno, è comunque possibile applicare i comandi nella ricerca esterna hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="1429d-381">Ad esempio, è comunque possibile hello gruppo sopra gli eventi con un altro comando measure:</span><span class="sxs-lookup"><span data-stu-id="1429d-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="1429d-383">In genere, si desidera tooexecute la query interna rapidamente perché in Log Analitica timeout lato servizio, nonché tooreturn una piccola quantità di risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="1429d-384">Se la query interna hello restituisce più risultati, viene troncato elenco risultati hello, che possono provocare hello ricerca esterna tooreturn risultati non corretti.</span><span class="sxs-lookup"><span data-stu-id="1429d-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="1429d-385">Un'altra regola prevede che ricerca interna hello attualmente tooprovide *aggregati* risultati.</span><span class="sxs-lookup"><span data-stu-id="1429d-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="1429d-386">In altre parole deve contenere un comando *measure* , perché attualmente non è possibile inserire risultati non elaborati in una ricerca esterna.</span><span class="sxs-lookup"><span data-stu-id="1429d-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="1429d-387">Inoltre, può esistere un solo operatore IN, e che deve essere hello l'ultimo filtro nella query hello.</span><span class="sxs-lookup"><span data-stu-id="1429d-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="1429d-388">Non possono essere più operatori IN o sarebbe: ciò che impedisce essenzialmente l'esecuzione di più ricerche secondarie: hello importante punto è che una sola ricerca secondaria/interna, è possibile per ogni ricerca esterna.</span><span class="sxs-lookup"><span data-stu-id="1429d-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="1429d-389">Anche con questi limiti, IN consente diverse tipologie di ricerche correlate e permette toodefine toogroups simile, ad esempio computer, utenti o file, tutti gli eventuali campi hello nei dati contengono.</span><span class="sxs-lookup"><span data-stu-id="1429d-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="1429d-390">Di seguito sono riportati altri esempi:</span><span class="sxs-lookup"><span data-stu-id="1429d-390">Here are more examples:</span></span>

<span data-ttu-id="1429d-391">**Tutti gli aggiornamenti mancanti nei computer in cui è disabilitato l'aggiornamento automatico**</span><span class="sxs-lookup"><span data-stu-id="1429d-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="1429d-392">**Tutti gli eventi di errore dai computer che eseguono SQL Server, in cui viene eseguito SQL Assessment**</span><span class="sxs-lookup"><span data-stu-id="1429d-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="1429d-393">**Tutti gli eventi di sicurezza dai computer che sono controller di dominio, in cui viene eseguito AD Assessment**</span><span class="sxs-lookup"><span data-stu-id="1429d-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="1429d-394">**Quali altri account hanno effettuato toohello stesso computer in cui si è connesso l'account BACONLAND\jochan?**</span><span class="sxs-lookup"><span data-stu-id="1429d-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="1429d-395">Comando distinti hello</span><span class="sxs-lookup"><span data-stu-id="1429d-395">Use hello distinct command</span></span>
<span data-ttu-id="1429d-396">Come suggerisce il nome di hello, questo comando fornisce un elenco di valori distinct per un campo.</span><span class="sxs-lookup"><span data-stu-id="1429d-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="1429d-397">È estremamente semplice ma molto utile.</span><span class="sxs-lookup"><span data-stu-id="1429d-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="1429d-398">Hello che stesso può essere ottenuto anche, come illustrato di seguito con il comando measure Count ().</span><span class="sxs-lookup"><span data-stu-id="1429d-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="1429d-400">Tuttavia, se si è interessati solo a un elenco di valori distinti e non hello conteggio dei documenti che contengono che i valori, quindi DISTINCT può fornire tooread più semplice e leggibile di output e una sintassi più breve, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1429d-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="1429d-402">Funzione countdistinct hello con il comando measure hello</span><span class="sxs-lookup"><span data-stu-id="1429d-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="1429d-403">funzione countdistinct Hello hello conteggio di valori distinti in ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="1429d-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="1429d-404">Ad esempio, potrebbe essere utilizzato toocount hello numero di computer univoci per ogni tipo:</span><span class="sxs-lookup"><span data-stu-id="1429d-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="1429d-406">Comando hello misura intervallo</span><span class="sxs-lookup"><span data-stu-id="1429d-406">Use hello measure interval command</span></span>
<span data-ttu-id="1429d-407">La raccolta di dati sulle prestazioni quasi in tempo reale permette di raccogliere e visualizzare qualsiasi contatore delle prestazioni in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1429d-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="1429d-408">Semplicemente immettere query hello **tipo: prestazioni** restituirà migliaia di grafici metrica in base al numero di hello di contatori e i server nell'ambiente Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="1429d-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="1429d-409">Con l'aggregazione di metrica su richiesta, è possibile esaminare hello complessive metriche nell'ambiente a un livello elevato e approfondimento di dati più granulari che è necessario.</span><span class="sxs-lookup"><span data-stu-id="1429d-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="1429d-410">Si supponga che si desidera tooknow hello utilizzo medio della CPU tra tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="1429d-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="1429d-411">Esaminando hello utilizzo medio della CPU per tutti i computer potrebbe non essere utile in quanto i risultati possono ottenere smussati. toolook in ulteriori dettagli, è possibile aggregare i risultati in un momento più piccolo blocchi di finestra e cercare in una serie temporale tra diverse dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1429d-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="1429d-412">Ad esempio, è possibile eseguire hello oraria circa l'utilizzo della CPU tra tutti i computer come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1429d-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![misura intervallo medio](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="1429d-414">Per impostazione predefinita, questi risultati vengono visualizzati in un grafico a linee interattivo a più serie.</span><span class="sxs-lookup"><span data-stu-id="1429d-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="1429d-415">Il grafico supporta l'attivazione e la disattivazione delle serie con ridimensionamento dell'asse Y, lo zoom e il passaggio del puntatore.</span><span class="sxs-lookup"><span data-stu-id="1429d-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="1429d-416">opzione di visualizzazione tabella Hello è ancora disponibile per la visualizzazione dei dati non elaborati hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="1429d-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="1429d-417">È anche possibile raggruppare in base ad altri campi.</span><span class="sxs-lookup"><span data-stu-id="1429d-417">You can also group by other fields.</span></span> <span data-ttu-id="1429d-418">In questo esempio, ricerca di tutti i contatori % hello per un computer specifico e desidera tooknow i percentili oraria 70 hello di ogni contatore:</span><span class="sxs-lookup"><span data-stu-id="1429d-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="1429d-419">Una cosa toonote è che queste query non sono limitate tooperformance contatori.</span><span class="sxs-lookup"><span data-stu-id="1429d-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="1429d-420">È possibile applicarle tooany metrica.</span><span class="sxs-lookup"><span data-stu-id="1429d-420">You can apply them tooany metric.</span></span> <span data-ttu-id="1429d-421">In questo esempio si esaminano i log di IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="1429d-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="1429d-422">Desidera tooknow hello massimo tempo su un intervallo di 5 minuti per l'elaborazione di ogni richiesta:</span><span class="sxs-lookup"><span data-stu-id="1429d-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="1429d-423">Usare più aggregazioni in una query</span><span class="sxs-lookup"><span data-stu-id="1429d-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="1429d-424">È possibile specificare più clausole di aggregazione in un comando measure.</span><span class="sxs-lookup"><span data-stu-id="1429d-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="1429d-425">Ognuna di esse può essere associata a un alias in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1429d-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="1429d-426">Se non viene assegnato un alias di hello risultante il nome del campo sarà la funzione di aggregazione hello che è stata utilizzata (ad esempio "avg(CounterValue)" per avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="1429d-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="1429d-428">Di seguito è riportato un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="1429d-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="1429d-429">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1429d-429">Next steps</span></span>
<span data-ttu-id="1429d-430">Per altre informazioni sulle ricerche nei log:</span><span class="sxs-lookup"><span data-stu-id="1429d-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="1429d-431">Utilizzare [campi personalizzati nel registro Analitica](log-analytics-custom-fields.md) tooextend ricerche nei log.</span><span class="sxs-lookup"><span data-stu-id="1429d-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="1429d-432">Hello revisione [riferimento alla ricerca di log Log Analitica](log-analytics-search-reference.md) tooview tutti hello cerca i campi e facet disponibile nel Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="1429d-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
