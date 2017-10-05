---
title: Mappa delle applicazioni in Azure Application Insights | Microsoft Docs
description: Una rappresentazione visiva delle dipendenze tra i componenti di app, contrassegnati con avvisi e indicatori KPI.
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
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="cf219-103">Mappa delle applicazioni in Application Insights</span><span class="sxs-lookup"><span data-stu-id="cf219-103">Application Map in Application Insights</span></span>
<span data-ttu-id="cf219-104">In [Azure Application Insights](app-insights-overview.md), Mappa delle applicazioni è un layout visivo delle relazioni di dipendenza dei componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cf219-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="cf219-105">Ogni componente mostra gli indicatori KPI, ad esempio carico, prestazioni, errori e avvisi per individuare eventuali componenti che generano un errore o un problema di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cf219-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="cf219-106">È possibile fare clic da qualsiasi componente per ottenere una diagnostica più dettagliata, ad esempio sugli eventi di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cf219-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="cf219-107">Se l'app usa i servizi di Azure, è possibile anche fare clic sulla diagnostica di Azure, ad esempio per consigli di Advisor su database SQL.</span><span class="sxs-lookup"><span data-stu-id="cf219-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="cf219-108">Come altri tipi di grafico, è possibile aggiungere una mappa delle applicazioni al dashboard di Azure, in cui è completamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="cf219-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="cf219-109">Aprire la mappa delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="cf219-109">Open the application map</span></span>
<span data-ttu-id="cf219-110">Aprire la mappa nel pannello di panoramica dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="cf219-110">Open the map from the overview blade for your application:</span></span>

![aprire la mappa delle app](./media/app-insights-app-map/01.png)

![mappa delle app](./media/app-insights-app-map/02.png)

<span data-ttu-id="cf219-113">La mappa mostra:</span><span class="sxs-lookup"><span data-stu-id="cf219-113">The map shows:</span></span>

* <span data-ttu-id="cf219-114">Test della disponibilità</span><span class="sxs-lookup"><span data-stu-id="cf219-114">Availability tests</span></span>
* <span data-ttu-id="cf219-115">Componente lato client (monitorato con JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="cf219-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="cf219-116">Componente lato server</span><span class="sxs-lookup"><span data-stu-id="cf219-116">Server-side component</span></span>
* <span data-ttu-id="cf219-117">Dipendenze dei componenti client e server</span><span class="sxs-lookup"><span data-stu-id="cf219-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="cf219-118">È possibile espandere e comprimere i gruppi di collegamento di dipendenza:</span><span class="sxs-lookup"><span data-stu-id="cf219-118">You can expand and collapse dependency link groups:</span></span>

![comprimere](./media/app-insights-app-map/03.png)

<span data-ttu-id="cf219-120">Se si dispone di numerose dipendenze di un tipo (SQL, HTTP e così via), possono essere visualizzate raggruppate.</span><span class="sxs-lookup"><span data-stu-id="cf219-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dipendenze raggruppate](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="cf219-122">Individuazione di problemi</span><span class="sxs-lookup"><span data-stu-id="cf219-122">Spot problems</span></span>
<span data-ttu-id="cf219-123">Ogni nodo dispone di indicatori di prestazioni rilevanti, ad esempio tassi di carico, prestazioni ed errori per il componente.</span><span class="sxs-lookup"><span data-stu-id="cf219-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="cf219-124">Le icone di avviso evidenziano possibili problemi.</span><span class="sxs-lookup"><span data-stu-id="cf219-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="cf219-125">Un avviso di colore arancione indica che si verificano errori nelle richieste, visualizzazioni di pagina o chiamate di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="cf219-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="cf219-126">Il rosso indica una percentuale di errore superiore al 5%.</span><span class="sxs-lookup"><span data-stu-id="cf219-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="cf219-127">Se si vuole modificare queste soglie, aprire Opzioni.</span><span class="sxs-lookup"><span data-stu-id="cf219-127">If you want to adjust these thresholds, open Options.</span></span>

![icone di errore](./media/app-insights-app-map/04.png)

<span data-ttu-id="cf219-129">Vengono visualizzati anche avvisi attivi:</span><span class="sxs-lookup"><span data-stu-id="cf219-129">Active alerts also show up:</span></span> 

![avvisi attivi](./media/app-insights-app-map/05.png)

<span data-ttu-id="cf219-131">Se si usa SQL Azure, è presente un'icona che indica quando sono disponibili consigli su come è possibile migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cf219-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Suggerimento di Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="cf219-133">Per ottenere altri dettagli, fare clic su qualsiasi icona:</span><span class="sxs-lookup"><span data-stu-id="cf219-133">Click any icon to get more details:</span></span>

![Suggerimento di Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="cf219-135">Diagnostica tramite clic</span><span class="sxs-lookup"><span data-stu-id="cf219-135">Diagnostic click through</span></span>
<span data-ttu-id="cf219-136">Ciascun nodo della mappa permette una diagnostica tramite clic mirati.</span><span class="sxs-lookup"><span data-stu-id="cf219-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="cf219-137">Le opzioni variano a seconda del tipo del nodo.</span><span class="sxs-lookup"><span data-stu-id="cf219-137">The options vary depending on the type of the node.</span></span>

![opzioni server](./media/app-insights-app-map/09.png)

<span data-ttu-id="cf219-139">Per i componenti ospitati in Azure, le opzioni includono collegamenti diretti a essi.</span><span class="sxs-lookup"><span data-stu-id="cf219-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="cf219-140">Filtri e intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="cf219-140">Filters and time range</span></span>
<span data-ttu-id="cf219-141">Per impostazione predefinita, la mappa riepiloga tutti i dati disponibili per l'intervallo di tempo scelto.</span><span class="sxs-lookup"><span data-stu-id="cf219-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="cf219-142">è possibile filtrarlo in modo da includere solo i nomi di operazioni o dipendenze specifici.</span><span class="sxs-lookup"><span data-stu-id="cf219-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="cf219-143">Nome dell'operazione: include sia le visualizzazioni pagina che i tipi di richiesta lato server.</span><span class="sxs-lookup"><span data-stu-id="cf219-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="cf219-144">Con questa opzione, la mappa mostra l'indicatore KPI nel nodo lato server/client solo per le operazioni selezionate.</span><span class="sxs-lookup"><span data-stu-id="cf219-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="cf219-145">Mostra le dipendenze chiamate nel contesto di tali operazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="cf219-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="cf219-146">Nome di base delle dipendenze: include le dipendenze del browser AJAX e lato server.</span><span class="sxs-lookup"><span data-stu-id="cf219-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="cf219-147">Se si segnalano dati di telemetria di dipendenza personalizzati con l'API TrackDependency, questi vengono visualizzati anche qui.</span><span class="sxs-lookup"><span data-stu-id="cf219-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="cf219-148">È possibile selezionare le dipendenze da mostrare sulla mappa.</span><span class="sxs-lookup"><span data-stu-id="cf219-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="cf219-149">Attualmente, questa selezione non filtra le richieste lato server o le visualizzazioni di pagina lato client.</span><span class="sxs-lookup"><span data-stu-id="cf219-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![impostare i filtri](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="cf219-151">Salvare i filtri</span><span class="sxs-lookup"><span data-stu-id="cf219-151">Save filters</span></span>
<span data-ttu-id="cf219-152">Per salvare i filtri applicati, bloccare la visualizzazione filtrata su un [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="cf219-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Aggiungi al dashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="cf219-154">Riquadro dell'errore</span><span class="sxs-lookup"><span data-stu-id="cf219-154">Error pane</span></span>
<span data-ttu-id="cf219-155">Quando si fa clic su un nodo nella mappa, viene visualizzato un riquadro dell'errore sul lato destro che riassume i problemi relativi a tale nodo.</span><span class="sxs-lookup"><span data-stu-id="cf219-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="cf219-156">Gli errori vengono prima raggruppati per ID operazione e quindi per ID del problema.</span><span class="sxs-lookup"><span data-stu-id="cf219-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Riquadro dell'errore](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="cf219-158">Per passare all'istanza più recente dell'errore fare clic sull'errore stesso.</span><span class="sxs-lookup"><span data-stu-id="cf219-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="cf219-159">Integrità delle risorse</span><span class="sxs-lookup"><span data-stu-id="cf219-159">Resource health</span></span>
<span data-ttu-id="cf219-160">Per alcuni tipi di risorsa, l'integrità delle risorse viene visualizzata nella parte superiore del riquadro dell'errore.</span><span class="sxs-lookup"><span data-stu-id="cf219-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="cf219-161">Ad esempio, facendo clic su un nodo SQL verranno visualizzati l'integrità del database ed eventuali avvisi che sono stati attivati.</span><span class="sxs-lookup"><span data-stu-id="cf219-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![Integrità delle risorse](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="cf219-163">È possibile fare clic sul nome della risorsa per visualizzare le metriche di panoramica standard per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="cf219-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="cf219-164">Mappe delle app del sistema end-to-end</span><span class="sxs-lookup"><span data-stu-id="cf219-164">End-to-end system app maps</span></span>

<span data-ttu-id="cf219-165">*È necessaria la versione 2.3 o successive di SDK*</span><span class="sxs-lookup"><span data-stu-id="cf219-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="cf219-166">Se l'applicazione include diversi componenti, ad esempio un servizio back-end oltre all'App Web, è anche possibile visualizzarli tutti in una mappa integrata delle app.</span><span class="sxs-lookup"><span data-stu-id="cf219-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![impostare i filtri](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="cf219-168">La mappa dell'app consente di trovare i nodi del server seguendo le chiamate di dipendenza HTTP inviate tra i server con Application Insights SDK installato.</span><span class="sxs-lookup"><span data-stu-id="cf219-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="cf219-169">Si presuppone che ogni risorsa di Application Insights contenga un server.</span><span class="sxs-lookup"><span data-stu-id="cf219-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="cf219-170">Mappa con app multi-ruolo (anteprima)</span><span class="sxs-lookup"><span data-stu-id="cf219-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="cf219-171">La funzionalità di anteprima della mappa dell'app multi-ruolo consente di usare la mappa dell'app con più server che inviano dati alla stessa risorsa o alla stessa chiave di strumentazione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cf219-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="cf219-172">I server nella mappa vengono segmentati in base alla proprietà cloud_RoleName negli elementi di telemetria.</span><span class="sxs-lookup"><span data-stu-id="cf219-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="cf219-173">Impostare *Multi-role Application Map* (Mappa dell'applicazione multi-ruolo) su *On* (Attivo) nel pannello Anteprime per abilitare questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="cf219-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="cf219-174">Questo approccio potrebbe essere necessario in un'applicazione di micro-servizi o in altri scenari in cui si desidera correlare gli eventi tra più server all'interno di una singola risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cf219-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="cf219-175">Video</span><span class="sxs-lookup"><span data-stu-id="cf219-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="cf219-176">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cf219-176">Feedback</span></span>
<span data-ttu-id="cf219-177">Inviare commenti e suggerimenti tramite l'apposita opzione del portale.</span><span class="sxs-lookup"><span data-stu-id="cf219-177">Please provide feedback through the portal feedback option.</span></span>

![Immagine MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="cf219-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf219-179">Next steps</span></span>

* [<span data-ttu-id="cf219-180">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cf219-180">Azure portal</span></span>](https://portal.azure.com)
