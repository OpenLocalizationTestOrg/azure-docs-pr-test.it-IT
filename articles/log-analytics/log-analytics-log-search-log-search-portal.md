---
title: portale di ricerca nei Log aaaUsing hello in Azure Log Analitica | Documenti Microsoft
description: In questo articolo include un'esercitazione che illustra come toocreate log ricerche e analisi dei dati memorizzati nell'area di lavoro Analitica Log tramite il portale di ricerca nei Log hello.  esercitazione di Hello include eseguire alcune semplici query tooreturn diversi tipi di dati e analizzare i risultati.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="20910-104">Creare ricerche nei log in Analitica di Log di Azure tramite il portale di ricerca nei Log hello</span><span class="sxs-lookup"><span data-stu-id="20910-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="20910-105">Questo articolo descrive il portale di ricerca nei Log hello in Analitica di Log di Azure utilizzando il nuovo linguaggio di query hello.</span><span class="sxs-lookup"><span data-stu-id="20910-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="20910-106">È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="20910-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="20910-107">Se l'area di lavoro non è stato aggiornato toohello nuovo linguaggio di query, è consigliabile consultare troppo[trovare i dati tramite ricerche nei log nel Log Analitica](log-analytics-log-searches.md) per informazioni sulla versione corrente di hello del portale di ricerca nei Log hello.</span><span class="sxs-lookup"><span data-stu-id="20910-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="20910-108">In questo articolo include un'esercitazione che illustra come toocreate log ricerche e analisi dei dati memorizzati nell'area di lavoro Analitica Log tramite il portale di ricerca nei Log hello.</span><span class="sxs-lookup"><span data-stu-id="20910-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="20910-109">esercitazione di Hello include eseguire alcune semplici query tooreturn diversi tipi di dati e analizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="20910-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="20910-110">Si concentra sulle funzionalità nel portale di ricerca nei Log hello per modificare la query hello anziché modificarlo direttamente.</span><span class="sxs-lookup"><span data-stu-id="20910-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="20910-111">Per informazioni dettagliate sulla modifica direttamente la query hello, vedere hello [riferimenti al linguaggio di Query](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="20910-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="20910-112">vedere toocreate ricerche nel portale di Advanced Analitica hello anziché portale ricerca nei Log di hello [Introduzione al portale Analitica hello](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="20910-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="20910-113">Entrambi i portali utilizzano hello stessa query language tooaccess hello stessi dati nell'area di lavoro Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="20910-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20910-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20910-114">Prerequisites</span></span>
<span data-ttu-id="20910-115">In questa esercitazione si presuppone che si disponga già di un'area di lavoro Log Analitica con almeno un'origine connessa che genera i dati per tooanalyze query hello.</span><span class="sxs-lookup"><span data-stu-id="20910-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="20910-116">Se non si dispone di un'area di lavoro, è possibile creare uno disponibile nella procedura hello in [Introduzione a un'area di lavoro Log Analitica](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="20910-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="20910-117">Connettere almeno una [dell'agente di Windows](log-analytics-windows-agents.md) o uno [agente Linux](log-analytics-linux-agents.md) toohello dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="20910-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="20910-118">Portale di hello aprire ricerca dei registri</span><span class="sxs-lookup"><span data-stu-id="20910-118">Open hello Log Search portal</span></span>
<span data-ttu-id="20910-119">Avvia aprendo il portale di ricerca nei Log hello.</span><span class="sxs-lookup"><span data-stu-id="20910-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="20910-120">È possibile accedervi in hello portale di Azure o il portale di OMS hello.</span><span class="sxs-lookup"><span data-stu-id="20910-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="20910-121">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="20910-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="20910-122">Passare tooLog Analitica e selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="20910-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="20910-123">Selezionare **ricerca nei Log** toostay in hello Azure portal o avviare hello portale OMS selezionando **portale OMS** e quindi fare clic sul pulsante ricerca dei registri hello.</span><span class="sxs-lookup"><span data-stu-id="20910-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Pulsante di ricerca log](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="20910-125">Creare una ricerca semplice</span><span class="sxs-lookup"><span data-stu-id="20910-125">Create a simple search</span></span>
<span data-ttu-id="20910-126">tooretrieve modo più rapido Hello toowork alcuni dati con è una query semplice che restituisce tutti i record nella tabella.</span><span class="sxs-lookup"><span data-stu-id="20910-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="20910-127">Se si dispone di qualsiasi area di tooyour connessi i client Windows o Linux, quindi sarà necessario dati hello di eventi (Windows) o una tabella Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="20910-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="20910-128">Digitare uno hello seguente query nella casella di ricerca hello e fare clic sul pulsante ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="20910-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="20910-129">Vengono restituiti dati nella visualizzazione elenco predefinito di hello ed è possibile visualizzare il numero totale di record sono stati restituiti.</span><span class="sxs-lookup"><span data-stu-id="20910-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Query semplice](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="20910-131">Solo hello prima alcune proprietà di ogni record vengono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="20910-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="20910-132">Fare clic su **Mostra altre** toodisplay tutte le proprietà per un record specifico.</span><span class="sxs-lookup"><span data-stu-id="20910-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Dettagli sui record](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="20910-134">Impostare l'ambito di hello ora</span><span class="sxs-lookup"><span data-stu-id="20910-134">Set hello time scope</span></span>
<span data-ttu-id="20910-135">Ogni record raccolti da Log Analitica con un **TimeGenerated** proprietà contenente hello data e ora in cui è stato creato il record di hello.</span><span class="sxs-lookup"><span data-stu-id="20910-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="20910-136">Una query nel portale di ricerca nei Log hello restituisce solo i record con un **TimeGenerated** ambito hello ora che viene visualizzato sul lato sinistro di schermata Ciao hello.</span><span class="sxs-lookup"><span data-stu-id="20910-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="20910-137">È possibile modificare filtro temporale hello selezionando l'elenco a discesa hello o modificando il dispositivo di scorrimento hello.</span><span class="sxs-lookup"><span data-stu-id="20910-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="20910-138">dispositivo di scorrimento Hello Visualizza un grafico a barre che mostra i numero di record per ogni segmento di tempo compreso hello relativo hello.</span><span class="sxs-lookup"><span data-stu-id="20910-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="20910-139">Questo segmento dipenderà dall'intervallo hello.</span><span class="sxs-lookup"><span data-stu-id="20910-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="20910-140">ambito di tempo predefinito Hello è **1 giorno**.</span><span class="sxs-lookup"><span data-stu-id="20910-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="20910-141">Modificare questo valore troppo**7 giorni**, e hello il numero totale di record aumenta.</span><span class="sxs-lookup"><span data-stu-id="20910-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Intervallo temporale](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="20910-143">Filtrare i risultati della query hello</span><span class="sxs-lookup"><span data-stu-id="20910-143">Filter results of hello query</span></span>
<span data-ttu-id="20910-144">In hello lato sinistro dello schermo hello è riquadro filtri hello consente tooadd filtro query toohello senza modificarlo direttamente.</span><span class="sxs-lookup"><span data-stu-id="20910-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="20910-145">Diverse proprietà di hello record restituiti vengono visualizzate con i relativi dieci valori superiore al numero di record.</span><span class="sxs-lookup"><span data-stu-id="20910-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="20910-146">Se si lavora con **evento**, selezionare hello casella di controllo accanto troppo**errore** in **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="20910-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="20910-147">Se si lavora con **Syslog**, selezionare hello casella di controllo accanto troppo**err** in **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="20910-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="20910-148">In questo caso query hello tooone di hello seguente hello toolimit risultati tooerror eventi.</span><span class="sxs-lookup"><span data-stu-id="20910-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="20910-150">Aggiungi riquadro filtro toohello di proprietà selezionando **aggiungere toofilters** dal menu di proprietà hello in uno dei record di hello.</span><span class="sxs-lookup"><span data-stu-id="20910-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Aggiungere menu toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="20910-152">È possibile impostare hello allo stesso filtro selezionando **filtro** dal menu di proprietà hello per un record con valore hello desiderato toofilter.</span><span class="sxs-lookup"><span data-stu-id="20910-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="20910-153">È sufficiente hello **filtro** opzione per le proprietà con il relativo nome in blu.</span><span class="sxs-lookup"><span data-stu-id="20910-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="20910-154">Si tratta di campi *disponibili per la ricerca* che vengono indicizzati per le condizioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="20910-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="20910-155">I campi in grigio sono *disponibile per la ricerca di testo libero* campi che dispongono solo delle hello **Mostra riferimenti** opzione.</span><span class="sxs-lookup"><span data-stu-id="20910-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="20910-156">Questa opzione restituisce i record con il valore specificato in qualsiasi proprietà.</span><span class="sxs-lookup"><span data-stu-id="20910-156">This option returns records that have that value in any property.</span></span>

![Menu di filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="20910-158">È possibile raggruppare i risultati di hello in una singola proprietà selezionando hello **raggruppare** opzione nel menu record hello.</span><span class="sxs-lookup"><span data-stu-id="20910-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="20910-159">Verrà aggiunta una [riepilogare](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) query tooyour operatore che visualizza i risultati di hello in un grafico.</span><span class="sxs-lookup"><span data-stu-id="20910-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="20910-160">È possibile raggruppare in più di una proprietà, ma è necessario query hello tooedit direttamente.</span><span class="sxs-lookup"><span data-stu-id="20910-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="20910-161">Selezionare prova menu record successivo hello prova **Computer** proprietà e selezionare **Group by 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="20910-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Raggruppare in base alla proprietà Computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="20910-163">Usare i risultati</span><span class="sxs-lookup"><span data-stu-id="20910-163">Work with results</span></span>
<span data-ttu-id="20910-164">portale di ricerca nei Log Hello dispone di una serie di funzionalità per l'utilizzo dei risultati di hello di una query.</span><span class="sxs-lookup"><span data-stu-id="20910-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="20910-165">È possibile ordinare, filtrare e raggruppare dati hello tooanalyze dei risultati senza modificare la query effettiva hello.</span><span class="sxs-lookup"><span data-stu-id="20910-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="20910-166">I risultati di una query non sono ordinati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="20910-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="20910-167">dati hello tooview in forma di tabella che fornisce ulteriori opzioni di filtro e ordinamento, fare clic su **tabella**.</span><span class="sxs-lookup"><span data-stu-id="20910-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Visualizzazione tabella](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="20910-169">Fare clic sulla freccia di hello da un dettagli hello tooview record per tale record.</span><span class="sxs-lookup"><span data-stu-id="20910-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="20910-171">È possibile ordinare i risultati in base a qualsiasi campo facendo clic sulla relativa intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="20910-171">Sort on any field by clicking on its column header.</span></span>

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="20910-173">Filtrare i risultati di hello su un valore specifico nella colonna hello facendo clic sul pulsante filtro hello e fornendo una condizione di filtro.</span><span class="sxs-lookup"><span data-stu-id="20910-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Filtrare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="20910-175">Raggruppare in una colonna, trascinare la parte superiore toohello di intestazione di colonna dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="20910-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="20910-176">È possibile raggruppare in più campi mediante il trascinamento di più colonne toohello dall'alto.</span><span class="sxs-lookup"><span data-stu-id="20910-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Raggruppare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="20910-178">Utilizzare i dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="20910-178">Work with performance data</span></span>
<span data-ttu-id="20910-179">Dati sulle prestazioni per Windows e Linux gli agenti vengono archiviati nell'area di lavoro Log Analitica hello in hello **prestazioni** tabella.</span><span class="sxs-lookup"><span data-stu-id="20910-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="20910-180">I record sulle prestazioni hanno lo stesso aspetto di qualsiasi altro record ed è possibile scrivere una query semplice che restituisce tutti i record sulle prestazioni esattamente come per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="20910-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="20910-182">La restituzione di milioni di record per tutti i contatori e gli oggetti prestazioni non è molto utile.</span><span class="sxs-lookup"><span data-stu-id="20910-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="20910-183">È possibile utilizzare hello è utilizzato in precedenza dati hello toofilter o semplicemente digitare hello seguente stessi metodi di query direttamente nella casella di ricerca log hello.</span><span class="sxs-lookup"><span data-stu-id="20910-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="20910-184">Vengono restituiti solo i record relativi all'utilizzo del processore per i computer Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="20910-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilizzo del processore](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="20910-186">Questo limita particolare contatore tooa dati hello, ma ancora non inserirlo in un form che risulta particolarmente utile.</span><span class="sxs-lookup"><span data-stu-id="20910-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="20910-187">È possibile visualizzare i dati di hello in un grafico a linee, ma prima di tutto necessario toogroup da Computer e TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="20910-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="20910-188">toogroup in più campi, è necessario query hello toomodify modificare direttamente, pertanto seguente toohello di hello query.</span><span class="sxs-lookup"><span data-stu-id="20910-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="20910-189">Questo metodo utilizza hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) funzione su hello **CounterValue** valore medio hello toocalculate della proprietà di ogni ora.</span><span class="sxs-lookup"><span data-stu-id="20910-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Grafico dei dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="20910-191">Ora che i dati di hello adeguatamente raggruppati, è possibile visualizzarlo in un grafico visual aggiungendo hello [rendering](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operatore.</span><span class="sxs-lookup"><span data-stu-id="20910-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Grafico a linee](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="20910-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20910-193">Next steps</span></span>

- <span data-ttu-id="20910-194">Altre informazioni sul linguaggio di query Log Analitica hello in [Introduzione al portale Analitica hello](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="20910-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="20910-195">Scorrere un'esercitazione utilizzando hello [portale avanzate Analitica](https://go.microsoft.com/fwlink/?linkid=856587) che consentono di hello toorun stessa query e accesso hello portale ricerca nei Log hello stessi dati.</span><span class="sxs-lookup"><span data-stu-id="20910-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
