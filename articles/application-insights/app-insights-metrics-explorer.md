---
title: Esaminare le metriche in Azure Application Insights | Microsoft Docs
description: Come interpretare i grafici in Esplora metriche e come personalizzare i pannelli di Esplora metriche.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="73091-103">Esaminare le metriche in Application Insights</span><span class="sxs-lookup"><span data-stu-id="73091-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="73091-104">Le metriche in [Application Insights][start] sono valori e conteggi di eventi misurati, inviati nei dati di telemetria dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73091-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="73091-105">Consentono di rilevare problemi di prestazioni e osservare le tendenze nella modalità di uso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73091-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="73091-106">Esiste una vasta gamma di metriche standard ed è anche possibile creare metriche ed eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="73091-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="73091-107">Il conteggio delle metriche e degli eventi viene visualizzato nei grafici dei valori aggregati, ad esempio somme, medie o conteggi.</span><span class="sxs-lookup"><span data-stu-id="73091-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="73091-108">Ecco un esempio di set di grafici:</span><span class="sxs-lookup"><span data-stu-id="73091-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="73091-109">I grafici delle metriche sono disponibili ovunque nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="73091-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="73091-110">Nella maggior parte dei casi possono essere personalizzati ed è possibile aggiungere altri grafici al pannello.</span><span class="sxs-lookup"><span data-stu-id="73091-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="73091-111">Nel pannello Panoramica fare clic per visualizzare grafici più dettagliati (con titoli come "Server") oppure fare clic su **Esplora metriche** per aprire un nuovo pannello in cui è possibile creare grafici personalizzati.</span><span class="sxs-lookup"><span data-stu-id="73091-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="73091-112">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="73091-112">Time range</span></span>
<span data-ttu-id="73091-113">È possibile modificare l'intervallo di tempo coperto dai grafici o dalle griglie in tutti i pannelli.</span><span class="sxs-lookup"><span data-stu-id="73091-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Aprire il pannello Panoramica dell'applicazione nel portale di Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="73091-115">Se si è in attesa di alcuni dati non ancora visualizzati, fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="73091-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="73091-116">I grafici si aggiornano a intervalli regolari, ma gli intervalli sono più lunghi per gli intervalli di tempo maggiori.</span><span class="sxs-lookup"><span data-stu-id="73091-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="73091-117">Ai dati potrebbe essere necessario un po' di tempo per superare la pipeline di analisi in un grafico.</span><span class="sxs-lookup"><span data-stu-id="73091-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="73091-118">Per ingrandire una parte di un grafico, trascinare sulla parte:</span><span class="sxs-lookup"><span data-stu-id="73091-118">To zoom into part of a chart, drag over it:</span></span>

![Trascinare il puntatore su una parte di un grafico.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="73091-120">Fare clic sul pulsante Annulla zoom per ripristinarlo.</span><span class="sxs-lookup"><span data-stu-id="73091-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="73091-121">Granularità e valori dei punti</span><span class="sxs-lookup"><span data-stu-id="73091-121">Granularity and point values</span></span>
<span data-ttu-id="73091-122">Posizionare il mouse sul grafico per visualizzare i valori delle metriche in quel punto.</span><span class="sxs-lookup"><span data-stu-id="73091-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Posizionare il mouse su un grafico](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="73091-124">Il valore della metrica in un punto particolare viene aggregato in base all'intervallo di campionamento precedente.</span><span class="sxs-lookup"><span data-stu-id="73091-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="73091-125">L'intervallo di campionamento o "granularità" è visibile nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="73091-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![Intestazione di un pannello.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="73091-127">È possibile modificare la granularità nel pannello Intervallo di tempo:</span><span class="sxs-lookup"><span data-stu-id="73091-127">You can adjust the granularity in the Time range blade:</span></span>

![Intestazione di un pannello.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="73091-129">Le granularità disponibili dipendono dall'intervallo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="73091-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="73091-130">Le granularità esplicite costituiscono alternative alla granularità "automatica" per l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="73091-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="73091-131">Modifica di grafici e griglie</span><span class="sxs-lookup"><span data-stu-id="73091-131">Editing charts and grids</span></span>
<span data-ttu-id="73091-132">Per aggiungere un nuovo grafico al pannello:</span><span class="sxs-lookup"><span data-stu-id="73091-132">To add a new chart to the blade:</span></span>

![In Esplora metriche scegliere Aggiungi grafico](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="73091-134">Selezionare **Modifica** su un grafico nuovo o esistente per modificare il contenuto visualizzato:</span><span class="sxs-lookup"><span data-stu-id="73091-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Selezionare una o più metriche](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="73091-136">È possibile visualizzare più metriche in un grafico, anche se sono presenti restrizioni sulle combinazioni che è possibile visualizzare insieme.</span><span class="sxs-lookup"><span data-stu-id="73091-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="73091-137">Non appena si sceglie una metrica, alcune vengono disabilitate.</span><span class="sxs-lookup"><span data-stu-id="73091-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="73091-138">Eventuali [metriche personalizzate][track] codificate nell'app (chiamate a TrackMetric e TrackEvent) vengono elencate qui.</span><span class="sxs-lookup"><span data-stu-id="73091-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="73091-139">Segmentare i dati</span><span class="sxs-lookup"><span data-stu-id="73091-139">Segment your data</span></span>
<span data-ttu-id="73091-140">È possibile suddividere una metrica per la proprietà, ad esempio eseguire un confronto delle visualizzazioni di una pagina sui client con sistemi operativi differenti.</span><span class="sxs-lookup"><span data-stu-id="73091-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="73091-141">Selezionare un grafico o una griglia, attivare il raggruppamento e scegliere una proprietà in base a cui eseguire il raggruppamento:</span><span class="sxs-lookup"><span data-stu-id="73091-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Attivare il raggruppamento e poi selezionare una proprietà in Raggruppa per](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="73091-143">Quando si utilizza la funzione di raggruppamento, i grafici ad area e a barre forniscono una visualizzazione in pila,</span><span class="sxs-lookup"><span data-stu-id="73091-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="73091-144">che risulta ottimale se il metodo di aggregazione selezionato è Somma.</span><span class="sxs-lookup"><span data-stu-id="73091-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="73091-145">Ma se il tipo di aggregazione selezionato è Media, è consigliabile scegliere i tipi di visualizzazione a righe o a griglia.</span><span class="sxs-lookup"><span data-stu-id="73091-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="73091-146">Se si codificano [metriche personalizzate][track] nell'app e si includono valori di proprietà, sarà possibile selezionare le proprietà da questo elenco.</span><span class="sxs-lookup"><span data-stu-id="73091-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="73091-147">Il grafico è troppo piccolo per dati segmentati?</span><span class="sxs-lookup"><span data-stu-id="73091-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="73091-148">modificarne l'altezza:</span><span class="sxs-lookup"><span data-stu-id="73091-148">Adjust its height:</span></span>

![Regolare il dispositivo di scorrimento](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="73091-150">Tipi di aggregazione</span><span class="sxs-lookup"><span data-stu-id="73091-150">Aggregation types</span></span>
<span data-ttu-id="73091-151">La legenda sul lato mostra di solito per impostazione predefinita il valore aggregato per il periodo del grafico.</span><span class="sxs-lookup"><span data-stu-id="73091-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="73091-152">Se si passa il mouse sul grafico, viene visualizzato il valore in questo punto.</span><span class="sxs-lookup"><span data-stu-id="73091-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="73091-153">Ogni punto dati del grafico è una funzione di aggregazione dei valori di dati ricevuti nell'intervallo di campionamento o nella "granularità" precedente.</span><span class="sxs-lookup"><span data-stu-id="73091-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="73091-154">La granularità viene visualizzata nella parte superiore del pannello e varia in base alla scala cronologica complessiva del grafico.</span><span class="sxs-lookup"><span data-stu-id="73091-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="73091-155">Le metriche possono essere aggregate in modi diversi:</span><span class="sxs-lookup"><span data-stu-id="73091-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="73091-156">**Conteggio** è un conteggio degli eventi ricevuti nell'intervallo di campionamento.</span><span class="sxs-lookup"><span data-stu-id="73091-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="73091-157">Viene utilizzato per gli eventi come le richieste.</span><span class="sxs-lookup"><span data-stu-id="73091-157">It is used for events such as requests.</span></span> <span data-ttu-id="73091-158">Le variazioni in altezza del grafico indicano variazioni della frequenza con cui si verificano gli eventi.</span><span class="sxs-lookup"><span data-stu-id="73091-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="73091-159">Ma si noti che il valore numerico cambia quando si modifica l'intervallo di campionamento.</span><span class="sxs-lookup"><span data-stu-id="73091-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="73091-160">**Somma** : esegue la somma dei valori dei punti dati ricevuti tramite l'intervallo di campionamento o il periodo del grafico.</span><span class="sxs-lookup"><span data-stu-id="73091-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="73091-161">**Media** : divide la somma per il numero di punti dati ricevuti tramite l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="73091-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="73091-162">**Unica** : i conteggi vengono usati per contare gli utenti e gli account.</span><span class="sxs-lookup"><span data-stu-id="73091-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="73091-163">Per tutto l'intervallo di campionamento, o per il periodo del grafico, la cifra mostra il numero di utenti diversi visualizzato in quel momento.</span><span class="sxs-lookup"><span data-stu-id="73091-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="73091-164">**%** - le versioni in percentuale di ogni aggregazione vengono utilizzate solo con i grafici segmentati.</span><span class="sxs-lookup"><span data-stu-id="73091-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="73091-165">Il totale raggiunge sempre il 100% e il grafico mostra il contributo relativo dei diversi componenti di un totale.</span><span class="sxs-lookup"><span data-stu-id="73091-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Aggregazione in percentuale](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="73091-167">Modificare il tipo di aggregazione</span><span class="sxs-lookup"><span data-stu-id="73091-167">Change the aggregation type</span></span>

![Modificare il grafico, quindi selezionare Aggregazione](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="73091-169">Il metodo predefinito per ciascuna metrica viene visualizzato quando si crea un nuovo grafico o quando si deselezionano tutte le metriche:</span><span class="sxs-lookup"><span data-stu-id="73091-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Deselezionare tutte le metriche per visualizzare le impostazioni predefinite](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="73091-171">Bloccare l'asse Y</span><span class="sxs-lookup"><span data-stu-id="73091-171">Pin Y-axis</span></span> 
<span data-ttu-id="73091-172">Per impostazione predefinita, in un grafico i valori dell'asse Y sono visualizzati a partire da zero fino ai valori massimi dell'intervallo di dati, per offrire una rappresentazione visiva del quantum dei valori.</span><span class="sxs-lookup"><span data-stu-id="73091-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="73091-173">In alcuni casi tuttavia, più che il quantum, può essere interessante esaminare le modifiche secondarie ai valori.</span><span class="sxs-lookup"><span data-stu-id="73091-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="73091-174">Per personalizzazioni di questo tipo, usare la funzionalità di modifica dell'intervallo dell'asse Y per bloccare il valore minimo o massimo dell'asse Y nel punto desiderato.</span><span class="sxs-lookup"><span data-stu-id="73091-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="73091-175">Fare clic sulla casella di controllo "Impostazioni avanzate" per visualizzare le impostazioni dell'intervallo dell'asse Y.</span><span class="sxs-lookup"><span data-stu-id="73091-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Fare clic su Impostazioni avanzate, selezionare l'intervallo Personalizzato e specificare i valori minino e massimo](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="73091-177">Filtrare i dati</span><span class="sxs-lookup"><span data-stu-id="73091-177">Filter your data</span></span>
<span data-ttu-id="73091-178">Per visualizzare solo le metriche per un set di valori di proprietà selezionati:</span><span class="sxs-lookup"><span data-stu-id="73091-178">To see just the metrics for a selected set of property values:</span></span>

![Fare clic su Filtro, espandere una proprietà e selezionare alcuni valori](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="73091-180">Se non si seleziona alcun valore per una determinata proprietà, è come se si selezionassero tutti i valori, ovvero alla proprietà non verrà applicato alcun filtro.</span><span class="sxs-lookup"><span data-stu-id="73091-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="73091-181">Si noti il numero di eventi vicino a ogni valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="73091-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="73091-182">Quando si selezionano i valori di una proprietà, i conteggi vicino ad altri valori di proprietà vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="73091-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="73091-183">I filtri si applicano a tutti i grafici in un pannello.</span><span class="sxs-lookup"><span data-stu-id="73091-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="73091-184">Se si desidera applicare filtri diversi a grafici differenti, creare e salvare pannelli di metriche diversi.</span><span class="sxs-lookup"><span data-stu-id="73091-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="73091-185">Se si desidera, è possibile aggiungere sul dashboard grafici di pannelli diversi, in modo da visualizzarli uno accanto all'altro.</span><span class="sxs-lookup"><span data-stu-id="73091-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="73091-186">Rimuovere il traffico di bot e test Web</span><span class="sxs-lookup"><span data-stu-id="73091-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="73091-187">Usare il filtro **Traffico reale o sintetico** e selezionare **Reale**.</span><span class="sxs-lookup"><span data-stu-id="73091-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="73091-188">È possibile anche filtrare in base a **Origine del traffico sintetico**.</span><span class="sxs-lookup"><span data-stu-id="73091-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="73091-189">Per aggiungere proprietà all'elenco di filtri</span><span class="sxs-lookup"><span data-stu-id="73091-189">To add properties to the filter list</span></span>
<span data-ttu-id="73091-190">È possibile che si voglia filtrare i dati di telemetria in base a una categoria personalizzata.</span><span class="sxs-lookup"><span data-stu-id="73091-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="73091-191">Ad esempio, è possibile che si dividano gli utenti in categorie diverse e si voglia segmentare i dati in base a queste categorie.</span><span class="sxs-lookup"><span data-stu-id="73091-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="73091-192">[Creare proprietà personalizzate](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="73091-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="73091-193">Impostazione in un [Inizializzatore di telemetria](app-insights-api-custom-events-metrics.md#defaults) affinché venga visualizzato in tutti i dati di telemetria - compresa la telemetria standard inviata dai diversi moduli SDK.</span><span class="sxs-lookup"><span data-stu-id="73091-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="73091-194">Modificare il tipo di grafico</span><span class="sxs-lookup"><span data-stu-id="73091-194">Edit the chart type</span></span>
<span data-ttu-id="73091-195">Si noti che è possibile passare dalle griglie ai grafici e viceversa:</span><span class="sxs-lookup"><span data-stu-id="73091-195">Notice that you can switch between grids and graphs:</span></span>

![Selezionare una griglia o un grafico e quindi scegliere un tipo di grafico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="73091-197">Salvare il pannello delle metriche</span><span class="sxs-lookup"><span data-stu-id="73091-197">Save your metrics blade</span></span>
<span data-ttu-id="73091-198">Dopo aver creato alcuni grafici, è possibile salvarli come preferiti.</span><span class="sxs-lookup"><span data-stu-id="73091-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="73091-199">È possibile scegliere se condividerlo con altri membri del team, se si usa un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="73091-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Scegliere Preferito](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="73091-201">Per visualizzare nuovamente il pannello, **andare al pannello** e aprire Preferiti:</span><span class="sxs-lookup"><span data-stu-id="73091-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![Nel pannello Panoramica scegliere Preferiti](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="73091-203">Se si è scelto l'intervallo di tempo Relativo al momento del salvataggio, il pannello verrà aggiornato con le metriche più recenti.</span><span class="sxs-lookup"><span data-stu-id="73091-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="73091-204">Se si è scelto l'intervallo di tempo Assoluto, verranno visualizzati gli stessi dati ogni volta.</span><span class="sxs-lookup"><span data-stu-id="73091-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="73091-205">Reimpostare il pannello</span><span class="sxs-lookup"><span data-stu-id="73091-205">Reset the blade</span></span>
<span data-ttu-id="73091-206">Se si modifica un pannello ma poi si vuole tornare a quello salvato in origine, fare clic su Reimposta.</span><span class="sxs-lookup"><span data-stu-id="73091-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![Nei pulsanti nella parte superiore di Esplora metriche](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="73091-208">Flusso metriche attive</span><span class="sxs-lookup"><span data-stu-id="73091-208">Live metrics stream</span></span>

<span data-ttu-id="73091-209">Per una visualizzazione molto più immediata dei dati di telemetria, aprire [flusso live](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="73091-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="73091-210">La visualizzazione della maggior parte delle metriche richiede alcuni minuti, a causa del processo di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="73091-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="73091-211">Al contrario, le metriche attive sono ottimizzate per bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="73091-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="73091-212">Impostazione di avvisi</span><span class="sxs-lookup"><span data-stu-id="73091-212">Set alerts</span></span>
<span data-ttu-id="73091-213">Per ricevere tramite posta elettronica una notifica relativa a valori insoliti di una metrica, aggiungere un avviso.</span><span class="sxs-lookup"><span data-stu-id="73091-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="73091-214">È possibile scegliere di inviare il messaggio di posta elettronica agli amministratori di account o a indirizzi di posta elettronica specifici.</span><span class="sxs-lookup"><span data-stu-id="73091-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![In Esplora metriche scegliere Regole di avviso, Aggiungi avviso](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="73091-216">[Altre informazioni sugli avvisi][alerts].</span><span class="sxs-lookup"><span data-stu-id="73091-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="73091-217">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="73091-217">Continuous Export</span></span>
<span data-ttu-id="73091-218">Se si vuole che i dati vengano esportati in modo continuo per poterli elaborare esternamente, considerare la possibilità di usare l' [esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="73091-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="73091-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="73091-219">Power BI</span></span>
<span data-ttu-id="73091-220">Per visualizzazione dei dati ancora più avanzate, è possibile [esportare in Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="73091-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="73091-221">Analytics</span><span class="sxs-lookup"><span data-stu-id="73091-221">Analytics</span></span>
<span data-ttu-id="73091-222">[Analytics](app-insights-analytics.md) è un modo più versatile per analizzare i dati di telemetria usando un linguaggio di query avanzato.</span><span class="sxs-lookup"><span data-stu-id="73091-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="73091-223">Usare l'opzione per combinare o calcolare i risultati delle metriche oppure per eseguire un'analisi approfondita delle prestazioni recenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73091-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="73091-224">Da un grafico di metriche è possibile fare clic sull'icona di Analytics per passare direttamente alla query di Analytics equivalente.</span><span class="sxs-lookup"><span data-stu-id="73091-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="73091-225">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="73091-225">Troubleshooting</span></span>
<span data-ttu-id="73091-226">*All'interno del grafico non vengono visualizzati dati.*</span><span class="sxs-lookup"><span data-stu-id="73091-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="73091-227">I filtri si applicano a tutti i grafici del pannello.</span><span class="sxs-lookup"><span data-stu-id="73091-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="73091-228">Assicurarsi che, mentre ci si concentra su un grafico, non sia stato impostato un filtro che escluda tutti i dati di un altro grafico.</span><span class="sxs-lookup"><span data-stu-id="73091-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="73091-229">Se si desidera impostare filtri diversi nei vari grafici, creare grafici in diversi pannelli e salvarli come Preferiti separati.</span><span class="sxs-lookup"><span data-stu-id="73091-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="73091-230">Se si desidera, è possibile impostarli sul dashboard in modo da visualizzarli uno accanto all'altro.</span><span class="sxs-lookup"><span data-stu-id="73091-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="73091-231">Se si raggruppa un grafico per una proprietà non definita sulla metrica, il grafico sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="73091-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="73091-232">Provare a lasciare il campo "Raggruppa in base a" vuoto o scegliere una proprietà di raggruppamento diversa.</span><span class="sxs-lookup"><span data-stu-id="73091-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="73091-233">I dati sulle prestazioni (CPU, velocità di IO e così via) sono disponibili per servizi Web Java, app desktop di Windows, [app Web IIS se si installa Status Monitor](app-insights-monitor-performance-live-website-now.md) e [servizi cloud di Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="73091-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="73091-234">I dati non sono disponibili per i siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73091-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="73091-235">Video</span><span class="sxs-lookup"><span data-stu-id="73091-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="73091-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73091-236">Next steps</span></span>
* [<span data-ttu-id="73091-237">Monitoraggio dell'utilizzo con Application Insights</span><span class="sxs-lookup"><span data-stu-id="73091-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="73091-238">Uso di Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="73091-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
