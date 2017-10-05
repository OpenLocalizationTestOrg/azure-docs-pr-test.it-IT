---
title: Uso del portale per la ricerca log in Azure Log Analytics | Microsoft Docs
description: Questo articolo include un'esercitazione che descrive come creare ricerche log e analizzare i dati archiviati nell'area di lavoro di Log Analytics tramite il portale per la ricerca log.  L'esercitazione include l'esecuzione di alcune semplici query per restituire diversi tipi di dati e l'analisi dei risultati.
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
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="7e0f6-104">Creare ricerche log in Azure Log Analytics tramite il portale per la ricerca log</span><span class="sxs-lookup"><span data-stu-id="7e0f6-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="7e0f6-105">Questo articolo descrive il portale per la ricerca log in Azure Log Analytics e l'uso del nuovo linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="7e0f6-106">In [Aggiornare l'area di lavoro di Azure Log Analytics alla nuova ricerca log](log-analytics-log-search-upgrade.md) sono disponibili altre informazioni sul nuovo linguaggio e istruzioni per l'aggiornamento dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="7e0f6-107">Se l'area di lavoro non è stata aggiornata al nuovo linguaggio di query, è consigliabile consultare [Trovare dati tramite ricerche nei log in Log Analytics](log-analytics-log-searches.md) per informazioni sulla versione corrente del portale per la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="7e0f6-108">Questo articolo include un'esercitazione che descrive come creare ricerche log e analizzare i dati archiviati nell'area di lavoro di Log Analytics tramite il portale per la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="7e0f6-109">L'esercitazione include l'esecuzione di alcune semplici query per restituire diversi tipi di dati e l'analisi dei risultati.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="7e0f6-110">È incentrata sulle funzionalità del portale per la ricerca log per la modifica della query, anziché sulla modifica diretta.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="7e0f6-111">Per informazioni dettagliate su come modificare direttamente la query, vedere [Informazioni di riferimento sul linguaggio di query](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="7e0f6-112">Per creare ricerche nel portale Advanced Analytics anziché nel portale per la ricerca log, vedere [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587) (Introduzione al portale di Analytics).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="7e0f6-113">Entrambi i portali utilizzano lo stesso linguaggio di query per accedere agli stessi dati nell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e0f6-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e0f6-114">Prerequisites</span></span>
<span data-ttu-id="7e0f6-115">In questa esercitazione si presuppone che sia già disponibile un'area di lavoro di Log Analytics con almeno un'origine connessa che genera dati analizzabili tramite le query.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="7e0f6-116">Se l'area di lavoro non è disponibile, è possibile crearne una gratuitamente seguendo la procedura in [Introduzione a un'area di lavoro di Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="7e0f6-117">Connettere almeno un [agente Windows](log-analytics-windows-agents.md) o un [agente Linux](log-analytics-linux-agents.md) all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="7e0f6-118">Aprire il portale per la ricerca log</span><span class="sxs-lookup"><span data-stu-id="7e0f6-118">Open the Log Search portal</span></span>
<span data-ttu-id="7e0f6-119">Per iniziare, aprire il portale per la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="7e0f6-120">È possibile accedervi dal portale di Azure o dal portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="7e0f6-121">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="7e0f6-122">Passare a Log Analytics e selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="7e0f6-123">Selezionare **Ricerca log** per rimanere nel portale di Azure o avviare il portale di OMS selezionando **Portale di OMS** e facendo quindi clic sul pulsante Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Pulsante di ricerca log](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="7e0f6-125">Creare una ricerca semplice</span><span class="sxs-lookup"><span data-stu-id="7e0f6-125">Create a simple search</span></span>
<span data-ttu-id="7e0f6-126">Il modo più rapido per recuperare alcuni dati da utilizzare è una query semplice che restituisce tutti i record in una tabella.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="7e0f6-127">In presenza di client Windows o Linux connessi all'area di lavoro, saranno disponibili dati nella tabella Event (Windows) o nella tabella Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="7e0f6-128">Digitare una delle query seguenti nella casella di ricerca e fare clic sul pulsante di ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="7e0f6-129">I dati vengono restituiti nella visualizzazione elenco predefinita ed è possibile vedere il numero totale di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Query semplice](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="7e0f6-131">Vengono visualizzate alcune delle prime proprietà di ogni record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="7e0f6-132">Fare clic su **Mostra più** per visualizzare tutte le proprietà per un record specifico.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-132">Click **show more** to display all properties for a particular record.</span></span>

![Dettagli sui record](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="7e0f6-134">Impostare l'intervallo temporale</span><span class="sxs-lookup"><span data-stu-id="7e0f6-134">Set the time scope</span></span>
<span data-ttu-id="7e0f6-135">Per ogni record raccolto da Log Analytics esiste una proprietà **TimeGenerated** che contiene la data e ora di creazione del record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="7e0f6-136">Una query nel portale per la ricerca log restituisce solo i record con **TimeGenerated** incluso nell'intervallo temporale visualizzato sul lato sinistro della schermata.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="7e0f6-137">È possibile modificare il filtro temporale selezionando il valore desiderato nell'elenco a discesa oppure modificando il dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="7e0f6-138">Il dispositivo di scorrimento visualizza un grafico a barre che mostra il numero relativo di record per ogni segmento di tempo all'interno dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="7e0f6-139">Questo segmento può variare a seconda dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="7e0f6-140">L'intervallo temporale predefinito è **1 giorno**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="7e0f6-141">Se si modifica il valore impostando **7 giorni** il numero totale di record dovrebbe aumentare.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Intervallo temporale](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="7e0f6-143">Filtrare i risultati della query</span><span class="sxs-lookup"><span data-stu-id="7e0f6-143">Filter results of the query</span></span>
<span data-ttu-id="7e0f6-144">Sul lato sinistro della schermata è disponibile il riquadro di filtro che consente di aggiungere filtri alla query senza modificarla direttamente.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="7e0f6-145">Varie proprietà dei record restituiti vengono visualizzate con i relativi primi dieci valori e il numero di record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="7e0f6-146">Se si sta usando la tabella **Event**, selezionare la casella di controllo accanto a **Error** in **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="7e0f6-147">Se si sta usando la tabella **Syslog**, selezionare la casella di controllo accanto a **err** in **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="7e0f6-148">La query viene modificata come segue per limitare i risultati agli eventi di errore.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="7e0f6-150">Aggiungere proprietà al riquadro di filtro scegliendo **Aggiungi ai filtri** dal menu della proprietà in uno dei record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Menu Aggiungi ai filtri](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="7e0f6-152">È possibile impostare lo stesso filtro selezionando **Filtra** dal menu della proprietà per un record con il valore in base al quale si vogliono filtrare i risultati.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="7e0f6-153">L'opzione **Filtra** è disponibile solo per le proprietà con il nome in blu.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="7e0f6-154">Si tratta di campi *disponibili per la ricerca* che vengono indicizzati per le condizioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="7e0f6-155">I campi in grigio sono campi *disponibili per la ricerca a testo libero* per i quali è disponibile solo l'opzione **Mostra riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="7e0f6-156">Questa opzione restituisce i record con il valore specificato in qualsiasi proprietà.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-156">This option returns records that have that value in any property.</span></span>

![Menu di filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="7e0f6-158">È possibile raggruppare i risultati in base a una singola proprietà selezionando l'opzione **Raggruppa per** nel menu del record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="7e0f6-159">Verrà aggiunto un operatore [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) alla query, che visualizza i risultati in un grafico.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="7e0f6-160">È possibile effettuare il raggruppamento in base a una o più proprietà, ma in questo caso occorre modificare direttamente la query.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="7e0f6-161">Selezionare il menu del record accanto alla proprietà **Computer** e scegliere **Raggruppa per 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Raggruppare in base alla proprietà Computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="7e0f6-163">Usare i risultati</span><span class="sxs-lookup"><span data-stu-id="7e0f6-163">Work with results</span></span>
<span data-ttu-id="7e0f6-164">Il portale per la ricerca log offre un'ampia gamma di funzionalità per l'utilizzo dei risultati di una query.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="7e0f6-165">È possibile ordinare, filtrare e raggruppare i risultati per analizzare i dati senza modificare la query effettiva.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="7e0f6-166">I risultati di una query non sono ordinati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="7e0f6-167">Per visualizzare i dati in formato di tabella e avere così a disposizione ulteriori opzioni di filtro e ordinamento, fare clic su **Tabella**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Visualizzazione tabella](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="7e0f6-169">Fare clic sulla freccia accanto a un record per visualizzare i dettagli di tale record.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-169">Click the arrow by a record to view the details for that record.</span></span>

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="7e0f6-171">È possibile ordinare i risultati in base a qualsiasi campo facendo clic sulla relativa intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-171">Sort on any field by clicking on its column header.</span></span>

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="7e0f6-173">Per filtrare i risultati in base a un valore specifico nella colonna, fare clic sul pulsante di filtro e specificare una condizione di filtro.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filtrare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="7e0f6-175">Per raggruppare i risultati in base a una colonna, trascinare l'intestazione della colonna nella parte superiore dei risultati.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="7e0f6-176">È possibile effettuare il raggruppamento in base a più campi trascinando più colonne nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Raggruppare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="7e0f6-178">Utilizzare i dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7e0f6-178">Work with performance data</span></span>
<span data-ttu-id="7e0f6-179">I dati sulle delle prestazioni per gli agenti Windows e Linux sono archiviati nell'area di lavoro di Log Analytics nella tabella **Perf**.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="7e0f6-180">I record sulle prestazioni hanno lo stesso aspetto di qualsiasi altro record ed è possibile scrivere una query semplice che restituisce tutti i record sulle prestazioni esattamente come per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="7e0f6-182">La restituzione di milioni di record per tutti i contatori e gli oggetti prestazioni non è molto utile.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="7e0f6-183">È possibile usare gli stessi metodi descritti in precedenza per filtrare i dati oppure digitare la query seguente direttamente nella casella di ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="7e0f6-184">Vengono restituiti solo i record relativi all'utilizzo del processore per i computer Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilizzo del processore](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="7e0f6-186">I dati vengono così limitati a un particolare contatore, ma sono ancora presentati in una forma non particolarmente utile.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="7e0f6-187">È possibile visualizzare i dati in un grafico a linee, ma è prima necessario raggrupparli in base a Computer e TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="7e0f6-188">Per effettuare il raggruppamento in base a più campi, è necessario modificare direttamente la query, quindi modificarla come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="7e0f6-189">Questa query usa la funzione [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) sulla proprietà **CounterValue** per calcolare il valore medio ogni ora.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Grafico dei dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="7e0f6-191">Ora che i dati sono raggruppati in modo adeguato, è possibile visualizzarli in un grafico aggiungendo l'operatore [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Grafico a linee](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="7e0f6-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e0f6-193">Next steps</span></span>

- <span data-ttu-id="7e0f6-194">Altre informazioni sul linguaggio di query di Log Analytics sono disponibili in [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079) (Introduzione al portale di Analytics).</span><span class="sxs-lookup"><span data-stu-id="7e0f6-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="7e0f6-195">Eseguire un'esercitazione con il [portale Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) che consente di eseguire le stesse query e accedere agli stessi dati del portale per la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="7e0f6-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
