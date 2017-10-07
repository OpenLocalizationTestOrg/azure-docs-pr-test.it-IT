---
title: Mappa in Azure Application Insights aaaApplication | Documenti Microsoft
description: Rappresentazione grafica delle dipendenze di hello tra i componenti dell'app, etichettata con avvisi e gli indicatori KPI.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="9d741-103">Mappa delle applicazioni in Application Insights</span><span class="sxs-lookup"><span data-stu-id="9d741-103">Application Map in Application Insights</span></span>
<span data-ttu-id="9d741-104">In [Azure Application Insights](app-insights-overview.md), mapping di applicazioni è un layout visivo hello relazioni di dipendenza dei componenti di applicazione.</span><span class="sxs-lookup"><span data-stu-id="9d741-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="9d741-105">Ogni componente mostra gli indicatori KPI, ad esempio toohelp carico, prestazioni, errori e avvisi, che si scopre di qualsiasi componente che causa un errore o un problema di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9d741-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="9d741-106">È possibile fare clic su tramite toomore qualsiasi componente dettagliate di diagnostica, ad esempio gli eventi di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9d741-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="9d741-107">Se l'app Usa i servizi di Azure, è anche possibile fare clic tramite diagnostica tooAzure, ad esempio indicazioni guidata Database SQL.</span><span class="sxs-lookup"><span data-stu-id="9d741-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="9d741-108">Come altri tipi di grafico, è possibile aggiungere un toohello mappa applicazione dashboard di Azure, in cui è completamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="9d741-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="9d741-109">Mappa delle applicazioni hello aperto</span><span class="sxs-lookup"><span data-stu-id="9d741-109">Open hello application map</span></span>
<span data-ttu-id="9d741-110">Mappa di hello aperto dal pannello della panoramica hello per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="9d741-110">Open hello map from hello overview blade for your application:</span></span>

![aprire la mappa delle app](./media/app-insights-app-map/01.png)

![mappa delle app](./media/app-insights-app-map/02.png)

<span data-ttu-id="9d741-113">Mostra mappa Hello:</span><span class="sxs-lookup"><span data-stu-id="9d741-113">hello map shows:</span></span>

* <span data-ttu-id="9d741-114">Test della disponibilità</span><span class="sxs-lookup"><span data-stu-id="9d741-114">Availability tests</span></span>
* <span data-ttu-id="9d741-115">Componente lato client (controllato con hello SDK per JavaScript)</span><span class="sxs-lookup"><span data-stu-id="9d741-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="9d741-116">Componente lato server</span><span class="sxs-lookup"><span data-stu-id="9d741-116">Server-side component</span></span>
* <span data-ttu-id="9d741-117">Dipendenze dei componenti client e server hello</span><span class="sxs-lookup"><span data-stu-id="9d741-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="9d741-118">È possibile espandere e comprimere i gruppi di collegamento di dipendenza:</span><span class="sxs-lookup"><span data-stu-id="9d741-118">You can expand and collapse dependency link groups:</span></span>

![comprimere](./media/app-insights-app-map/03.png)

<span data-ttu-id="9d741-120">Se si dispone di numerose dipendenze di un tipo (SQL, HTTP e così via), possono essere visualizzate raggruppate.</span><span class="sxs-lookup"><span data-stu-id="9d741-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dipendenze raggruppate](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="9d741-122">Individuazione di problemi</span><span class="sxs-lookup"><span data-stu-id="9d741-122">Spot problems</span></span>
<span data-ttu-id="9d741-123">Ogni nodo dispone di indicatori di prestazioni rilevanti, ad esempio tassi hello di carico, prestazioni ed errori per il componente.</span><span class="sxs-lookup"><span data-stu-id="9d741-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="9d741-124">Le icone di avviso evidenziano possibili problemi.</span><span class="sxs-lookup"><span data-stu-id="9d741-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="9d741-125">Un avviso di colore arancione indica che si verificano errori nelle richieste, visualizzazioni di pagina o chiamate di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="9d741-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="9d741-126">Il rosso indica una percentuale di errore superiore al 5%.</span><span class="sxs-lookup"><span data-stu-id="9d741-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="9d741-127">Se si desidera tooadjust queste soglie, aprire Opzioni.</span><span class="sxs-lookup"><span data-stu-id="9d741-127">If you want tooadjust these thresholds, open Options.</span></span>

![icone di errore](./media/app-insights-app-map/04.png)

<span data-ttu-id="9d741-129">Vengono visualizzati anche avvisi attivi:</span><span class="sxs-lookup"><span data-stu-id="9d741-129">Active alerts also show up:</span></span> 

![avvisi attivi](./media/app-insights-app-map/05.png)

<span data-ttu-id="9d741-131">Se si usa SQL Azure, è presente un'icona che indica quando sono disponibili consigli su come è possibile migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9d741-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Suggerimento di Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="9d741-133">Fare clic su qualsiasi icona tooget ulteriori dettagli:</span><span class="sxs-lookup"><span data-stu-id="9d741-133">Click any icon tooget more details:</span></span>

![Suggerimento di Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="9d741-135">Diagnostica tramite clic</span><span class="sxs-lookup"><span data-stu-id="9d741-135">Diagnostic click through</span></span>
<span data-ttu-id="9d741-136">Ogni nodo hello nella mappa hello offre destinazione click-through per la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="9d741-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="9d741-137">opzioni di Hello variano a seconda di tipo hello del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-137">hello options vary depending on hello type of hello node.</span></span>

![opzioni server](./media/app-insights-app-map/09.png)

<span data-ttu-id="9d741-139">Per i componenti sono ospitati in Azure, le opzioni di hello includono toothem collegamenti diretti.</span><span class="sxs-lookup"><span data-stu-id="9d741-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="9d741-140">Filtri e intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="9d741-140">Filters and time range</span></span>
<span data-ttu-id="9d741-141">Per impostazione predefinita, la mappa hello riepiloga i dati di hello tutti disponibili per l'intervallo di tempo scelto hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="9d741-142">Ma è possibile filtrare i nomi delle operazioni solo a specifici di tooinclude o dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d741-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="9d741-143">Nome dell'operazione: include sia le visualizzazioni pagina che i tipi di richiesta lato server.</span><span class="sxs-lookup"><span data-stu-id="9d741-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="9d741-144">Con questa opzione, hello mappa Mostra hello KPI nel nodo di hello client/server-side per le operazioni di hello selezionato solo.</span><span class="sxs-lookup"><span data-stu-id="9d741-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="9d741-145">Mostra dipendenze hello chiamate nel contesto di hello di tali operazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="9d741-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="9d741-146">Nome di base della dipendenza: sono incluse le dipendenze di browser AJAX hello e le dipendenze sul lato server.</span><span class="sxs-lookup"><span data-stu-id="9d741-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="9d741-147">Se si segnala telemetria dipendenza personalizzata con hello TrackDependency API, verranno visualizzate anche qui.</span><span class="sxs-lookup"><span data-stu-id="9d741-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="9d741-148">È possibile selezionare hello dipendenze tooshow nella mappa hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="9d741-149">Attualmente questa selezione non filtra richieste sul lato server hello o visualizzazioni di pagina sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![impostare i filtri](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="9d741-151">Salvare i filtri</span><span class="sxs-lookup"><span data-stu-id="9d741-151">Save filters</span></span>
<span data-ttu-id="9d741-152">toosave hello i filtri applicati, hello pin filtrati visualizzazione su un [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="9d741-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="9d741-154">Riquadro dell'errore</span><span class="sxs-lookup"><span data-stu-id="9d741-154">Error pane</span></span>
<span data-ttu-id="9d741-155">Quando si fa clic su un nodo nella mappa hello, un riquadro di errore viene visualizzato sul lato destro di hello Riepilogo errori relativi a tale nodo.</span><span class="sxs-lookup"><span data-stu-id="9d741-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="9d741-156">Gli errori vengono prima raggruppati per ID operazione e quindi per ID del problema.</span><span class="sxs-lookup"><span data-stu-id="9d741-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Riquadro dell'errore](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="9d741-158">Facendo clic su un errore accetta toohello istanza più recente di questo tipo di errore.</span><span class="sxs-lookup"><span data-stu-id="9d741-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="9d741-159">Integrità delle risorse</span><span class="sxs-lookup"><span data-stu-id="9d741-159">Resource health</span></span>
<span data-ttu-id="9d741-160">Per alcuni tipi di risorsa, l'integrità delle risorse viene visualizzato nella parte superiore di hello del riquadro errore hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="9d741-161">Ad esempio, facendo clic su un nodo SQL verranno visualizzati integrità database hello e eventuali avvisi che sono stati attivati.</span><span class="sxs-lookup"><span data-stu-id="9d741-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Integrità delle risorse](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="9d741-163">È possibile scegliere le metriche hello risorsa nome tooview Panoramica standard per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="9d741-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="9d741-164">Mappe delle app del sistema end-to-end</span><span class="sxs-lookup"><span data-stu-id="9d741-164">End-to-end system app maps</span></span>

<span data-ttu-id="9d741-165">*È necessaria la versione 2.3 o successive di SDK*</span><span class="sxs-lookup"><span data-stu-id="9d741-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="9d741-166">Se l'applicazione dispone di diversi componenti, ad esempio, un servizio back-end inoltre toohello web app, quindi si può visualizzare tutte nel mapping di un'applicazione integrata.</span><span class="sxs-lookup"><span data-stu-id="9d741-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![impostare i filtri](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="9d741-168">mappa app Hello consente di trovare i nodi del server seguendo le chiamate di dipendenza HTTP inviate tra i server con hello che Application Insights SDK installato.</span><span class="sxs-lookup"><span data-stu-id="9d741-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="9d741-169">Ogni risorsa di Application Insights presuppone toocontain un server.</span><span class="sxs-lookup"><span data-stu-id="9d741-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="9d741-170">Mappa con app multi-ruolo (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9d741-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="9d741-171">Hello anteprima app Multiruolo mappa consente toouse hello app mappa con più server, l'invio di dati toohello stessa risorsa di Application Insights / chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="9d741-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="9d741-172">I server nella mappa hello sono segmentati per proprietà cloud_RoleName hello sugli elementi di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="9d741-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="9d741-173">Impostare *con più ruoli applicazione mappa* troppo*su* da hello anteprime pannello tooenable questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="9d741-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="9d741-174">Questo approccio è preferibile in un'applicazione di micro-services o in altri scenari in cui si desidera che gli eventi toocorrelate tra più server all'interno di una singola risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9d741-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="9d741-175">Video</span><span class="sxs-lookup"><span data-stu-id="9d741-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="9d741-176">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9d741-176">Feedback</span></span>
<span data-ttu-id="9d741-177">Fornire commenti e suggerimenti tramite l'opzione commenti e suggerimenti portale hello.</span><span class="sxs-lookup"><span data-stu-id="9d741-177">Please provide feedback through hello portal feedback option.</span></span>

![Immagine MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="9d741-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d741-179">Next steps</span></span>

* [<span data-ttu-id="9d741-180">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9d741-180">Azure portal</span></span>](https://portal.azure.com)
