---
title: diagnostica aaaSmart delle modifiche delle prestazioni di app web in Azure Application Insights | Documenti Microsoft
description: Diagnosi automatica di modifiche improvvise nella telemetria delle prestazioni da parte di un'app web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="d514c-103">Diagnosticare modifiche improvvise nella telemetria dell'app</span><span class="sxs-lookup"><span data-stu-id="d514c-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="d514c-104">*Questa funzionalità è in anteprima.*</span><span class="sxs-lookup"><span data-stu-id="d514c-104">*This feature is in preview.*</span></span>

<span data-ttu-id="d514c-105">Diagnosticare modifiche improvvise delle prestazioni e dell'uso dell'app Web con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="d514c-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="d514c-106">funzionalità di diagnostica Smart Hello è disponibile quando si crea un grafico temporale nella [Analitica](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d514c-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d514c-107">In caso di una modifica insolita dalla tendenza hello dei risultati, ad esempio un picco o un dip, diagnostica Smart identifica il pattern di dimensioni e i valori correlati che potrebbero spiegare modifica hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="d514c-108">Ciò consente di diagnosticare il problema di hello rapidamente.</span><span class="sxs-lookup"><span data-stu-id="d514c-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="d514c-109">In questo esempio, diagnostica Smart ha identificato un modello di valori di proprietà associato modifica hello e viene evidenziata hello differenza tra i risultati con e senza tale modello:</span><span class="sxs-lookup"><span data-stu-id="d514c-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![Risultato di esempio della diagnostica di Analytics](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="d514c-111">Diagnosticare le modifiche ai dati</span><span class="sxs-lookup"><span data-stu-id="d514c-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="d514c-112">Eseguire una query in Analytics e creare un grafico del tempo.</span><span class="sxs-lookup"><span data-stu-id="d514c-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="d514c-113">Fare clic su qualsiasi punto di picco evidenziato, se presente.</span><span class="sxs-lookup"><span data-stu-id="d514c-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![Punto di picco](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="d514c-115">Diagnostica richiede pochi secondi toodiscover un modello.</span><span class="sxs-lookup"><span data-stu-id="d514c-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="d514c-116">scheda dei risultati diagnostica Hello Mostra un modello che può spiegare i discontinuità di dati.</span><span class="sxs-lookup"><span data-stu-id="d514c-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![risultato](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="d514c-118">testo Hello Mostra i valori delle dimensioni hello visualizzati toocorrelate con il tasto MAIUSC hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="d514c-119">In questo esempio, lo spostamento è associato a una determinata richiesta e a una versione particolare del browser.</span><span class="sxs-lookup"><span data-stu-id="d514c-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="d514c-120">Si noti inoltre componenti hello due grafico hello, con hello filtro true e false.</span><span class="sxs-lookup"><span data-stu-id="d514c-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="d514c-121">componente false Hello Mostra una tendenza subisce modifica.</span><span class="sxs-lookup"><span data-stu-id="d514c-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="d514c-122">In altre parole, è invariato nei risultati di telemetria hello, se si esclude hello problematico combinazione dimensioni identificati diagnostica.</span><span class="sxs-lookup"><span data-stu-id="d514c-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="d514c-123">Al contrario, i risultati di hello all'interno di tale combinazione mostrano notevoli modifiche nell'area di hello evidenziato di analisi.</span><span class="sxs-lookup"><span data-stu-id="d514c-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="d514c-124">Questo indica che la diagnostica è disponibile una combinazione di proprietà che spiega modifica hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="d514c-125">Se il modello di hello è complesso, è necessario toohover su **Mostra tutto** dimensioni hello toosee.</span><span class="sxs-lookup"><span data-stu-id="d514c-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![Mostra tutto](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="d514c-127">In caso di diagnostica consente di trovare alcun toonotify modello significativo su, verrà visualizzata la pagina "Nessun risultato" hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="d514c-128">A questo punto, è possibile modificare la query.</span><span class="sxs-lookup"><span data-stu-id="d514c-128">At this point, you may change your query.</span></span> <span data-ttu-id="d514c-129">Ad esempio, è possibile limitare l'ambito intervallo di tempo hello e binning nella query Analitica, per un'ulteriore analisi e potenzialmente migliori risultati.</span><span class="sxs-lookup"><span data-stu-id="d514c-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="d514c-130">Grazie a informazioni hello che una determinata pagina del sito Web disponga di un problema in un determinato browser, è possibile passare pagina problema toohello retta e provare a utilizzare le modifiche recenti.</span><span class="sxs-lookup"><span data-stu-id="d514c-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="d514c-131">Provare la demo hello</span><span class="sxs-lookup"><span data-stu-id="d514c-131">Try hello demo</span></span>

<span data-ttu-id="d514c-132">[Fare clic qui toosee una dimostrazione](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) su dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="d514c-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d514c-133">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="d514c-133">How it works</span></span>

<span data-ttu-id="d514c-134">Diagnostica smart utilizza un algoritmo di apprendimento non supervisionato avanzato basato su hello [DiffPatterns](app-insights-analytics-reference.md) operazione.</span><span class="sxs-lookup"><span data-stu-id="d514c-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="d514c-135">La ricerca di modelli candidati che potrebbero spiegare hello modifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="d514c-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="d514c-136">Analizza l'impatto di hello di ciascun candidato metrica hello e Mostra il modello di hello che mette in correlazione migliore con modifica hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="d514c-137">Nessun punto di diagnostica?</span><span class="sxs-lookup"><span data-stu-id="d514c-137">No diagnostic points?</span></span>

<span data-ttu-id="d514c-138">Diagnostica smart funziona solo quando viene soddisfatte hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="d514c-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="d514c-139">L'impostazione Smart Diagnostics è attivata.</span><span class="sxs-lookup"><span data-stu-id="d514c-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="d514c-140">Guarda sotto l'icona di impostazioni hello in Analitica.</span><span class="sxs-lookup"><span data-stu-id="d514c-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="d514c-141">opzione Smart diagnostica nelle impostazioni Analitica Hello è selezionata.</span><span class="sxs-lookup"><span data-stu-id="d514c-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="d514c-142">Asse temporale: hello asse x del grafico hello deve essere di tipo `datetime`.</span><span class="sxs-lookup"><span data-stu-id="d514c-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="d514c-143">Grafico a linee o ad area: la diagnostica funziona solo con questi tipi di grafico.</span><span class="sxs-lookup"><span data-stu-id="d514c-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="d514c-144">Utilizzare `| render timechart` o `| render areachart` alla fine della query; hello o selezionare grafico a linee o Area dal selettore di hello elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="d514c-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="d514c-145">Discontinuità: Deve esistere una discontinuità significativa nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="d514c-146">Tooanalyze di punti sufficiente.</span><span class="sxs-lookup"><span data-stu-id="d514c-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="d514c-147">Non più di un riepilogo di clausola di query hello.</span><span class="sxs-lookup"><span data-stu-id="d514c-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="d514c-148">Nessuna clausola del progetto che contiene una definizione di nome prima di hello riepilogare clausola.</span><span class="sxs-lookup"><span data-stu-id="d514c-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="d514c-149">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="d514c-149">Related articles</span></span>

 * [<span data-ttu-id="d514c-150">Esercitazione su Analisi</span><span class="sxs-lookup"><span data-stu-id="d514c-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="d514c-151">[Rilevamento smart](app-insights-proactive-diagnostics.md) utente viene avvisato automaticamente tooperformance problemi.</span><span class="sxs-lookup"><span data-stu-id="d514c-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
