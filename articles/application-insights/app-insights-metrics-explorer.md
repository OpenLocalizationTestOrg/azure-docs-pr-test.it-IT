---
title: aaaExploring metriche in Azure Application Insights | Documenti Microsoft
description: Come Esplora metrica dai grafici toointerpret e come toocustomize pannelli di Esplora metriche.
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
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="7c82a-103">Esaminare le metriche in Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c82a-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="7c82a-104">Le metriche in [Application Insights][start] sono valori e conteggi di eventi misurati, inviati nei dati di telemetria dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c82a-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="7c82a-105">Consentono di rilevare problemi di prestazioni e osservare le tendenze nella modalità di uso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c82a-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="7c82a-106">Esiste una vasta gamma di metriche standard ed è anche possibile creare metriche ed eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7c82a-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="7c82a-107">Il conteggio delle metriche e degli eventi viene visualizzato nei grafici dei valori aggregati, ad esempio somme, medie o conteggi.</span><span class="sxs-lookup"><span data-stu-id="7c82a-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="7c82a-108">Ecco un esempio di set di grafici:</span><span class="sxs-lookup"><span data-stu-id="7c82a-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="7c82a-109">Disponibili ovunque grafici delle metriche nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="7c82a-110">Nella maggior parte dei casi, possono essere personalizzate ed è possibile aggiungere ulteriori pannello toohello di grafici.</span><span class="sxs-lookup"><span data-stu-id="7c82a-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="7c82a-111">Dal pannello della panoramica hello, fare clic sulle toomore dettagliate grafici (che dispone di titoli, ad esempio "Server"), oppure fare clic su **Esplora metriche** tooopen un nuovo pannello in cui è possibile creare grafici personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7c82a-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="7c82a-112">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="7c82a-112">Time range</span></span>
<span data-ttu-id="7c82a-113">È possibile modificare l'intervallo di tempo coperto da grafici hello o griglie in qualsiasi pannello hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Pannello della panoramica hello aperti dell'applicazione nel portale di Azure hello](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="7c82a-115">Se si è in attesa di alcuni dati non ancora visualizzati, fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="7c82a-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="7c82a-116">Aggiornamento grafici a intervalli, ma sono più tempi per intervalli di tempo più ampi intervalli hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="7c82a-117">Può richiedere un po' di tempo per dati toocome tramite pipeline di analisi hello in un grafico.</span><span class="sxs-lookup"><span data-stu-id="7c82a-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="7c82a-118">toozoom nella parte di un grafico, trascinare su di essa:</span><span class="sxs-lookup"><span data-stu-id="7c82a-118">toozoom into part of a chart, drag over it:</span></span>

![Trascinare il puntatore su una parte di un grafico.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="7c82a-120">Fare clic su toorestore di pulsante Annulla Zoom hello è.</span><span class="sxs-lookup"><span data-stu-id="7c82a-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="7c82a-121">Granularità e valori dei punti</span><span class="sxs-lookup"><span data-stu-id="7c82a-121">Granularity and point values</span></span>
<span data-ttu-id="7c82a-122">A questo punto, posiziona il mouse su valori hello toodisplay di hello del grafico delle metriche hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Posizionare il mouse di hello su un grafico](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="7c82a-124">valore di Hello della metrica hello in un particolare punto è aggregato in hello precedente intervallo di campionamento.</span><span class="sxs-lookup"><span data-stu-id="7c82a-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="7c82a-125">intervallo di campionamento Hello o "granularità" viene visualizzata nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![intestazione Hello di un pannello.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="7c82a-127">È possibile regolare la granularità hello nel Pannello di intervallo di tempo hello:</span><span class="sxs-lookup"><span data-stu-id="7c82a-127">You can adjust hello granularity in hello Time range blade:</span></span>

![intestazione Hello di un pannello.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="7c82a-129">granularità Hello disponibili dipendono dall'intervallo di tempo hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="7c82a-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="7c82a-130">granularità esplicita Hello sono alternative toohello la granularità "automatico" per l'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="7c82a-131">Modifica di grafici e griglie</span><span class="sxs-lookup"><span data-stu-id="7c82a-131">Editing charts and grids</span></span>
<span data-ttu-id="7c82a-132">tooadd un nuovo pannello toohello grafico:</span><span class="sxs-lookup"><span data-stu-id="7c82a-132">tooadd a new chart toohello blade:</span></span>

![In Esplora metriche scegliere Aggiungi grafico](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="7c82a-134">Selezionare **modificare** in tooedit un grafico esistente o nuovo cosa viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="7c82a-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Selezionare una o più metriche](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="7c82a-136">È possibile visualizzare più di una metrica in un grafico, anche se sono presenti restrizioni sulle combinazioni di hello che possono essere visualizzate insieme.</span><span class="sxs-lookup"><span data-stu-id="7c82a-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="7c82a-137">Non appena si sceglie una metrica, alcune delle hello che altri è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="7c82a-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="7c82a-138">Se è stata codificata [metriche personalizzate] [ track] nell'app (chiamate tooTrackMetric e TrackEvent) questi verranno elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="7c82a-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="7c82a-139">Segmentare i dati</span><span class="sxs-lookup"><span data-stu-id="7c82a-139">Segment your data</span></span>
<span data-ttu-id="7c82a-140">È possibile dividere una metrica dalla proprietà, ad esempio, le visualizzazioni pagina toocompare nei client con sistemi operativi diversi.</span><span class="sxs-lookup"><span data-stu-id="7c82a-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="7c82a-141">Selezionare un diagramma o griglia, attivare il raggruppamento e scegliere un toogroup di proprietà da:</span><span class="sxs-lookup"><span data-stu-id="7c82a-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Attivare il raggruppamento e poi selezionare una proprietà in Raggruppa per](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="7c82a-143">Quando si utilizza il raggruppamento, i tipi di Area e di grafico a barre hello forniscono una visualizzazione in pila.</span><span class="sxs-lookup"><span data-stu-id="7c82a-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="7c82a-144">È adatto in cui il metodo di aggregazione hello è Sum.</span><span class="sxs-lookup"><span data-stu-id="7c82a-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="7c82a-145">Tuttavia, in cui il tipo di aggregazione hello Media, scegliere tipi di visualizzazione di riga o una griglia hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="7c82a-146">Se è stata codificata [metriche personalizzate] [ track] nell'app e includono i valori delle proprietà, sarà in grado di tooselect proprietà hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="7c82a-147">È troppo piccolo per i dati segmentati grafico hello?</span><span class="sxs-lookup"><span data-stu-id="7c82a-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="7c82a-148">modificarne l'altezza:</span><span class="sxs-lookup"><span data-stu-id="7c82a-148">Adjust its height:</span></span>

![Regolare il dispositivo di scorrimento hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="7c82a-150">Tipi di aggregazione</span><span class="sxs-lookup"><span data-stu-id="7c82a-150">Aggregation types</span></span>
<span data-ttu-id="7c82a-151">legenda Hello sul lato di hello per impostazione predefinita in genere viene visualizzato il valore aggregato hello periodo hello del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="7c82a-152">Se si passa il mouse sopra il grafico di hello, verrà visualizzato il valore di hello a questo punto.</span><span class="sxs-lookup"><span data-stu-id="7c82a-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="7c82a-153">Ogni punto dati nel grafico hello è un'aggregazione di valori di dati hello ricevuti nel precedente intervallo di campionamento "granularità" hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="7c82a-154">viene visualizzata nella parte superiore di hello del pannello hello granularità Hello e varia in base alla hello complessiva della scala cronologica del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="7c82a-155">Le metriche possono essere aggregate in modi diversi:</span><span class="sxs-lookup"><span data-stu-id="7c82a-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="7c82a-156">**Conteggio** è un numero di eventi di hello ricevuti nell'intervallo di campionamento hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="7c82a-157">Viene utilizzato per gli eventi come le richieste.</span><span class="sxs-lookup"><span data-stu-id="7c82a-157">It is used for events such as requests.</span></span> <span data-ttu-id="7c82a-158">Variazioni del grafico hello altezza hello indica le variazioni nel numero hello che si verificano gli eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="7c82a-159">Ma si noti che il valore numerico di hello cambia quando si modifica l'intervallo di campionamento hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="7c82a-160">**Somma** aggiunge i valori hello di tutti i punti dati hello ricevuti tramite l'intervallo di campionamento hello o periodo hello del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="7c82a-161">**Media** divide hello somma tramite un numero di punti dati ricevuti in intervallo hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="7c82a-162">**Unica** : i conteggi vengono usati per contare gli utenti e gli account.</span><span class="sxs-lookup"><span data-stu-id="7c82a-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="7c82a-163">Intervallo di campionamento hello o periodo hello del grafico hello, hello figura conteggio hello dei diversi utenti visualizzati in quel momento.</span><span class="sxs-lookup"><span data-stu-id="7c82a-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="7c82a-164">**%** - le versioni in percentuale di ogni aggregazione vengono utilizzate solo con i grafici segmentati.</span><span class="sxs-lookup"><span data-stu-id="7c82a-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="7c82a-165">Totale Hello aggiunge sempre % too100 grafico hello Mostra contributo relativo di hello dei diversi componenti di un totale.</span><span class="sxs-lookup"><span data-stu-id="7c82a-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Aggregazione in percentuale](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="7c82a-167">Modificare il tipo di aggregazione hello</span><span class="sxs-lookup"><span data-stu-id="7c82a-167">Change hello aggregation type</span></span>

![Modificare il grafico hello e quindi selezionare aggregazione](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="7c82a-169">il metodo predefinito Hello per ogni metrica viene visualizzato quando si crea un nuovo grafico o quando vengono deselezionate tutte le metriche:</span><span class="sxs-lookup"><span data-stu-id="7c82a-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Deselezionare tutte le metriche toosee hello le impostazioni predefinite](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="7c82a-171">Bloccare l'asse Y</span><span class="sxs-lookup"><span data-stu-id="7c82a-171">Pin Y-axis</span></span> 
<span data-ttu-id="7c82a-172">Per impostazione predefinita un grafico mostra i valori dell'asse Y a partire da zero fino a: i valori massimi nell'intervallo di dati hello, toogive una rappresentazione visiva del quantum di valori hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="7c82a-173">Ma in alcuni casi più quantum hello potrebbe essere interessante toovisually controllare piccole modifiche nei valori.</span><span class="sxs-lookup"><span data-stu-id="7c82a-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="7c82a-174">Per le personalizzazioni come questo utilizzo hello asse y intervallo modifica funzionalità toopin hello valore dell'asse y minimo o massimo nella posizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="7c82a-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="7c82a-175">Fare clic su "Impostazioni" casella di controllo toobring backup hello intervallo dell'asse y impostazioni</span><span class="sxs-lookup"><span data-stu-id="7c82a-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Fare clic su Impostazioni avanzate, selezionare l'intervallo Personalizzato e specificare i valori minino e massimo](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="7c82a-177">Filtrare i dati</span><span class="sxs-lookup"><span data-stu-id="7c82a-177">Filter your data</span></span>
<span data-ttu-id="7c82a-178">metrica di toosee hello solo per un set di valori di proprietà selezionato:</span><span class="sxs-lookup"><span data-stu-id="7c82a-178">toosee just hello metrics for a selected set of property values:</span></span>

![Fare clic su Filtro, espandere una proprietà e selezionare alcuni valori](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="7c82a-180">Se non si seleziona tutti i valori per una particolare proprietà, dispone di hello stesso come selezionarle tutte: non sono presenti filtri su questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="7c82a-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="7c82a-181">Hello notare i conteggi di eventi insieme a ogni valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="7c82a-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="7c82a-182">Quando si selezionano i valori di una proprietà, hello conta insieme ad altre proprietà vengono modificati i valori.</span><span class="sxs-lookup"><span data-stu-id="7c82a-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="7c82a-183">I filtri vengono applicati i grafici di hello tooall in un pannello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="7c82a-184">Se si desidera grafici toodifferent filtri diversi, creare e salvare blade metriche.</span><span class="sxs-lookup"><span data-stu-id="7c82a-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="7c82a-185">Se si desidera, è possibile aggiungere grafici dal dashboard toohello diversi pannelli, in modo che possano vederli uno accanto a altro.</span><span class="sxs-lookup"><span data-stu-id="7c82a-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="7c82a-186">Rimuovere il traffico di bot e test Web</span><span class="sxs-lookup"><span data-stu-id="7c82a-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="7c82a-187">Usa filtro hello **traffico reale o sintetico** e controllare **reale**.</span><span class="sxs-lookup"><span data-stu-id="7c82a-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="7c82a-188">È possibile anche filtrare in base a **Origine del traffico sintetico**.</span><span class="sxs-lookup"><span data-stu-id="7c82a-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="7c82a-189">elenco di filtri tooadd proprietà toohello</span><span class="sxs-lookup"><span data-stu-id="7c82a-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="7c82a-190">Si desidera telemetria toofilter su una categoria di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="7c82a-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="7c82a-191">Ad esempio, è possibile che si dividano gli utenti in categorie diverse e si voglia segmentare i dati in base a queste categorie.</span><span class="sxs-lookup"><span data-stu-id="7c82a-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="7c82a-192">[Creare proprietà personalizzate](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="7c82a-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="7c82a-193">Impostare la proprietà in un [telemetria inizializzatore](app-insights-api-custom-events-metrics.md#defaults) toohave appare in tutti i dati di telemetria, inclusi i dati di telemetria standard hello inviato da diversi moduli SDK.</span><span class="sxs-lookup"><span data-stu-id="7c82a-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="7c82a-194">Modificare il tipo di grafico hello</span><span class="sxs-lookup"><span data-stu-id="7c82a-194">Edit hello chart type</span></span>
<span data-ttu-id="7c82a-195">Si noti che è possibile passare dalle griglie ai grafici e viceversa:</span><span class="sxs-lookup"><span data-stu-id="7c82a-195">Notice that you can switch between grids and graphs:</span></span>

![Selezionare una griglia o un grafico e quindi scegliere un tipo di grafico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="7c82a-197">Salvare il pannello delle metriche</span><span class="sxs-lookup"><span data-stu-id="7c82a-197">Save your metrics blade</span></span>
<span data-ttu-id="7c82a-198">Dopo aver creato alcuni grafici, è possibile salvarli come preferiti.</span><span class="sxs-lookup"><span data-stu-id="7c82a-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="7c82a-199">È possibile scegliere se tooshare con altri membri del team, se si utilizza un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="7c82a-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Scegliere Preferito](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="7c82a-201">nuovo pannello con hello toosee **pannello della panoramica passare toohello** e aprire Preferiti:</span><span class="sxs-lookup"><span data-stu-id="7c82a-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Nel pannello della panoramica hello, scegliere Preferiti](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="7c82a-203">Se si sceglie l'intervallo di tempo relativo al momento del salvataggio, pannello hello verrà aggiornato con le metriche più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="7c82a-204">Se si sceglie l'intervallo di tempo assoluto, verrà visualizzato hello stessi dati ogni volta.</span><span class="sxs-lookup"><span data-stu-id="7c82a-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="7c82a-205">Reimpostazione hello pannello</span><span class="sxs-lookup"><span data-stu-id="7c82a-205">Reset hello blade</span></span>
<span data-ttu-id="7c82a-206">Se si modifica un pannello ma quindi cui si desidera che i set di backup toohello originale salvato tooget, semplicemente fare clic su Reimposta.</span><span class="sxs-lookup"><span data-stu-id="7c82a-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![Nei pulsanti di hello nella parte superiore di hello di Esplora metriche](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="7c82a-208">Flusso metriche attive</span><span class="sxs-lookup"><span data-stu-id="7c82a-208">Live metrics stream</span></span>

<span data-ttu-id="7c82a-209">Per una visualizzazione molto più immediata dei dati di telemetria, aprire [flusso live](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="7c82a-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="7c82a-210">La maggior parte delle metriche accettano pochi minuti tooappear, a causa del processo di hello di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="7c82a-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="7c82a-211">Al contrario, le metriche attive sono ottimizzate per bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="7c82a-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="7c82a-212">Impostazione di avvisi</span><span class="sxs-lookup"><span data-stu-id="7c82a-212">Set alerts</span></span>
<span data-ttu-id="7c82a-213">toobe una notifica tramite posta elettronica di valori insoliti per le metriche, aggiungere un avviso.</span><span class="sxs-lookup"><span data-stu-id="7c82a-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="7c82a-214">È possibile scegliere gli amministratori degli account toohello toosend hello posta elettronica o toospecific indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7c82a-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![In Esplora metriche scegliere Regole di avviso, Aggiungi avviso](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="7c82a-216">[Altre informazioni sugli avvisi][alerts].</span><span class="sxs-lookup"><span data-stu-id="7c82a-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="7c82a-217">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="7c82a-217">Continuous Export</span></span>
<span data-ttu-id="7c82a-218">Se si vuole che i dati vengano esportati in modo continuo per poterli elaborare esternamente, considerare la possibilità di usare l' [esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="7c82a-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="7c82a-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="7c82a-219">Power BI</span></span>
<span data-ttu-id="7c82a-220">Se si desidera arricchire la visualizzazione dei dati, è possibile [esportare tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c82a-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="7c82a-221">Analytics</span><span class="sxs-lookup"><span data-stu-id="7c82a-221">Analytics</span></span>
<span data-ttu-id="7c82a-222">[Analitica](app-insights-analytics.md) è un esempio di modalità più versatile tooanalyze dati di telemetria utilizzando un linguaggio di query avanzate.</span><span class="sxs-lookup"><span data-stu-id="7c82a-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="7c82a-223">Usarlo se si desidera toocombine risultati di metriche di calcolo o eseguire un'analisi approfondita del prestazioni recente dell'app.</span><span class="sxs-lookup"><span data-stu-id="7c82a-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="7c82a-224">In un grafico di metrica, è possibile scegliere hello Analitica icona tooget direttamente toohello Analitica query equivalente.</span><span class="sxs-lookup"><span data-stu-id="7c82a-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7c82a-225">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7c82a-225">Troubleshooting</span></span>
<span data-ttu-id="7c82a-226">*All'interno del grafico non vengono visualizzati dati.*</span><span class="sxs-lookup"><span data-stu-id="7c82a-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="7c82a-227">I filtri vengono applicati i grafici di hello tooall nel pannello hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="7c82a-228">Assicurarsi che, mentre sta porre l'attenzione su un grafico, non è stato impostato un filtro che escluda tutti i dati di hello in un altro.</span><span class="sxs-lookup"><span data-stu-id="7c82a-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="7c82a-229">Se si desidera tooset filtri diversi nei grafici diversi, crearli in diversi pannelli, salvare i Preferiti come separate.</span><span class="sxs-lookup"><span data-stu-id="7c82a-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="7c82a-230">Se si desidera, è possibile aggiungerli toohello dashboard in modo che possano vederli uno accanto a altro.</span><span class="sxs-lookup"><span data-stu-id="7c82a-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="7c82a-231">Se si raggruppa un grafico da una proprietà che non è definita nella metrica hello, quindi verrà nulla sul grafico hello.</span><span class="sxs-lookup"><span data-stu-id="7c82a-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="7c82a-232">Provare a lasciare il campo "Raggruppa in base a" vuoto o scegliere una proprietà di raggruppamento diversa.</span><span class="sxs-lookup"><span data-stu-id="7c82a-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="7c82a-233">I dati sulle prestazioni (CPU, velocità di IO e così via) sono disponibili per servizi Web Java, app desktop di Windows, [app Web IIS se si installa Status Monitor](app-insights-monitor-performance-live-website-now.md) e [servizi cloud di Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="7c82a-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="7c82a-234">I dati non sono disponibili per i siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c82a-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="7c82a-235">Video</span><span class="sxs-lookup"><span data-stu-id="7c82a-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="7c82a-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c82a-236">Next steps</span></span>
* [<span data-ttu-id="7c82a-237">Monitoraggio dell'utilizzo con Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c82a-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="7c82a-238">Uso di Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="7c82a-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
