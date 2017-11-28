---
title: Panoramica della soluzione di connected factory di Azure IoT Suite | Microsoft Docs
description: Descrizione della soluzione preconfigurata di connected factory di Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="99b5a-103">Introduzione alla soluzione preconfigurata di connected factory</span><span class="sxs-lookup"><span data-stu-id="99b5a-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="99b5a-104">Le [soluzioni preconfigurate][lnk-preconfigured-solutions] di Azure IoT Suite combinano più servizi IoT di Azure per fornire soluzioni end-to-end che implementano scenari aziendali IoT comuni.</span><span class="sxs-lookup"><span data-stu-id="99b5a-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="99b5a-105">La soluzione preconfigurata di *connected factory* si connette ai dispositivi industriali e li monitora.</span><span class="sxs-lookup"><span data-stu-id="99b5a-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="99b5a-106">È possibile usare la soluzione per analizzare il flusso di dati dei dispositivi e ottimizzare la produttività e la redditività operativa.</span><span class="sxs-lookup"><span data-stu-id="99b5a-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="99b5a-107">Questa esercitazione illustra come effettuare il provisioning della soluzione preconfigurata di connected factory.</span><span class="sxs-lookup"><span data-stu-id="99b5a-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="99b5a-108">Ne descrive anche le funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="99b5a-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="99b5a-109">È possibile accedere a molte di queste funzionalità dal *dashboard* distribuito come parte della soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="99b5a-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Dashboard della soluzione preconfigurata di connected factory][img-cf-home]

<span data-ttu-id="99b5a-111">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="99b5a-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="99b5a-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="99b5a-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="99b5a-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="99b5a-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="99b5a-114">Effettuare il provisioning della soluzione</span><span class="sxs-lookup"><span data-stu-id="99b5a-114">Provision the solution</span></span>

1. <span data-ttu-id="99b5a-115">Accedere ad azureiotsuite.com con le credenziali dell'account Azure e fare clic su "**+**" per creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="99b5a-116">Fare clic su **Seleziona** e sul riquadro **Connected factory**.</span><span class="sxs-lookup"><span data-stu-id="99b5a-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="99b5a-117">Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di connected factory.</span><span class="sxs-lookup"><span data-stu-id="99b5a-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="99b5a-118">Selezionare la **sottoscrizione** e l'**area** da usare per il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="99b5a-119">Fare clic su **Crea soluzione** per iniziare il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="99b5a-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="99b5a-120">In genere il processo richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="99b5a-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="99b5a-121">In attesa del completamento del provisioning</span><span class="sxs-lookup"><span data-stu-id="99b5a-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="99b5a-122">Fare clic sul riquadro della soluzione con stato **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="99b5a-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="99b5a-123">Notare gli stati **Provisioning** man mano che i servizi di Azure vengono distribuiti nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="99b5a-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="99b5a-124">Al termine del provisioning, lo stato cambierà in **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="99b5a-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="99b5a-125">Fare clic sul riquadro per visualizzare i dettagli della soluzione nel riquadro di destra.</span><span class="sxs-lookup"><span data-stu-id="99b5a-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="99b5a-126">In caso di problemi nella distribuzione della soluzione preconfigurata, vedere [Autorizzazioni per il sito azureiotsuite.com][lnk-permissions] e le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="99b5a-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="99b5a-127">Se i problemi persistono, creare un ticket di servizio nel [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="99b5a-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="99b5a-128">Se ci sono dettagli importanti non elencati per la soluzione,</span><span class="sxs-lookup"><span data-stu-id="99b5a-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="99b5a-129">è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="99b5a-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="99b5a-130">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="99b5a-130">Scenario overview</span></span>

<span data-ttu-id="99b5a-131">Nel momento in cui viene distribuita, la soluzione preconfigurata di connected factory viene prepopolata con risorse che consentono di eseguire uno scenario industriale comune.</span><span class="sxs-lookup"><span data-stu-id="99b5a-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="99b5a-132">In questo scenario, diversi stabilimenti connessi alla soluzione generano report con i valori dei dati necessari per calcolare l'OEE (Overall Equipment Efficiency) e gli indicatori di prestazioni chiave (KPI).</span><span class="sxs-lookup"><span data-stu-id="99b5a-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="99b5a-133">Le sezioni seguenti mostrano come:</span><span class="sxs-lookup"><span data-stu-id="99b5a-133">The following sections show you how to:</span></span>

* <span data-ttu-id="99b5a-134">Monitorare stabilimenti, linee di produzione, OEE delle postazioni e valori KPI</span><span class="sxs-lookup"><span data-stu-id="99b5a-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="99b5a-135">Analizzare i dati di telemetria generati da questi dispositivi usando Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="99b5a-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="99b5a-136">Intervenire in caso di avviso per risolvere i problemi</span><span class="sxs-lookup"><span data-stu-id="99b5a-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="99b5a-137">Una particolarità di questo scenario consiste nella possibilità di eseguire tutte queste azioni in remoto dal dashboard della soluzione,</span><span class="sxs-lookup"><span data-stu-id="99b5a-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="99b5a-138">senza dover accedere fisicamente ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="99b5a-139">Visualizzare il dashboard della soluzione</span><span class="sxs-lookup"><span data-stu-id="99b5a-139">View the solution dashboard</span></span>

<span data-ttu-id="99b5a-140">Il dashboard della soluzione consente di gestire la soluzione distribuita.</span><span class="sxs-lookup"><span data-stu-id="99b5a-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="99b5a-141">Si tratta di una rappresentazione gerarchica della configurazione globale degli stabilimenti.</span><span class="sxs-lookup"><span data-stu-id="99b5a-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="99b5a-142">È ad esempio possibile visualizzare OEE e KPI, pubblicare nuovi nodi per la telemetria e attivare avvisi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="99b5a-143">Al termine del provisioning, quando il riquadro della soluzione preconfigurata indica **Pronto**, scegliere **Avvia** per aprire il portale della soluzione di connected factory in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="99b5a-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![Avviare la soluzione preconfigurata][img-launch-solution]

1. <span data-ttu-id="99b5a-145">Per impostazione predefinita, il portale della soluzione visualizza il *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="99b5a-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="99b5a-146">Per passare ad altre aree del portale, usare il menu a sinistra della pagina.</span><span class="sxs-lookup"><span data-stu-id="99b5a-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Dashboard della soluzione preconfigurata di connected factory][cf-img-menu]

<span data-ttu-id="99b5a-148">Il dashboard visualizza le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="99b5a-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="99b5a-149">Un pannello con l'**elenco degli stabilimenti** che visualizza stato, località e configurazione di produzione corrente nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="99b5a-150">Quando si esegue la soluzione per la prima volta, sono disponibili alcuni dispositivi simulati.</span><span class="sxs-lookup"><span data-stu-id="99b5a-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="99b5a-151">La simulazione delle linee di produzione è costituita da tre server OPC UA reali per ogni linea di produzione che eseguono attività simulate e condividono i dati.</span><span class="sxs-lookup"><span data-stu-id="99b5a-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="99b5a-152">Per altre informazioni su OPC UA, vedere le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="99b5a-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="99b5a-153">Una **mappa** che visualizza la posizione di ogni dispositivo connesso alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="99b5a-154">La soluzione può usare l'API di Bing Mappe per tracciare le informazioni sulla mappa.</span><span class="sxs-lookup"><span data-stu-id="99b5a-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="99b5a-155">Se la sottoscrizione è abilitata per l'API di Bing Mappe per le aziende, questa funzionalità viene usata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="99b5a-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="99b5a-156">In caso contrario, vedere le [domande frequenti][lnk-faq] per informazioni su come rendere dinamica la mappa.</span><span class="sxs-lookup"><span data-stu-id="99b5a-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="99b5a-157">Un pannello degli **avvisi** che visualizza gli avvisi generati quando un valore OEE/KPI o di telemetria supera una soglia specifica.</span><span class="sxs-lookup"><span data-stu-id="99b5a-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="99b5a-158">Un pannello **Overall Equipment Efficiency** che visualizza i valori OEE per l'intera azienda o per lo stabilimento, la linea di produzione o la postazione in esame.</span><span class="sxs-lookup"><span data-stu-id="99b5a-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="99b5a-159">Questo valore viene aggregato dalla vista della postazione fino al livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="99b5a-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="99b5a-160">Il valore OEE e i relativi elementi costitutivi possono essere analizzati nei dettagli.</span><span class="sxs-lookup"><span data-stu-id="99b5a-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="99b5a-161">Un pannello **Key Performance Indicators** (Indicatori di prestazioni chiave) che visualizza il numero di unità prodotte e l'energia usata dall'intera azienda o dallo stabilimento, dalla linea di produzione o dalla postazione in esame.</span><span class="sxs-lookup"><span data-stu-id="99b5a-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="99b5a-162">Questi valori vengono aggregati dalla vista della postazione fino al livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="99b5a-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="99b5a-163">Visualizzare gli stabilimenti</span><span class="sxs-lookup"><span data-stu-id="99b5a-163">View factories</span></span>

<span data-ttu-id="99b5a-164">Il pannello degli *stabilimenti* visualizza la posizione geografica di tutti gli stabilimenti presenti nella soluzione, con lo stato e la configurazione di produzione corrente.</span><span class="sxs-lookup"><span data-stu-id="99b5a-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="99b5a-165">Dall'elenco delle località è possibile passare agli altri livelli della gerarchia della soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="99b5a-166">Le righe nell'elenco sono collegamenti ipertestuali che consentono di visualizzare i dettagli delle linee di produzione di tale località.</span><span class="sxs-lookup"><span data-stu-id="99b5a-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="99b5a-167">È quindi possibile esaminare i dettagli delle linee di produzione fino al livello della postazione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="99b5a-168">È anche possibile applicare un filtro all'elenco.</span><span class="sxs-lookup"><span data-stu-id="99b5a-168">You can also apply a filter to the list.</span></span>

![Stabilimenti della soluzione preconfigurata di connected factory][cf-img-factories] 

1. <span data-ttu-id="99b5a-170">Il **pannello degli stabilimenti** visualizza l'elenco di stabilimenti presenti in questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="99b5a-171">L'elenco degli stabilimenti visualizza inizialmente sei stabilimenti creati dal processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="99b5a-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="99b5a-172">È possibile aggiungere altri dispositivi fisici e simulati alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="99b5a-173">Per visualizzare i dettagli di uno stabilimento, fare clic sulla riga corrispondente nell'elenco degli stabilimenti.</span><span class="sxs-lookup"><span data-stu-id="99b5a-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="99b5a-174">Per visualizzare i dettagli di una linea di produzione, fare clic sulla riga corrispondente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="99b5a-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="99b5a-175">Per visualizzare i nodi OPC UA pubblicati di una postazione nella linea di produzione, fare clic sulla riga corrispondente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="99b5a-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="99b5a-176">Per visualizzare i dettagli in un nodo specifico nella postazione, fare clic sulla riga corrispondente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="99b5a-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="99b5a-177">Questa azione consente di avviare il pannello contestuale con visualizzazioni di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99b5a-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="99b5a-178">Fare clic su questi grafici per eseguire altre analisi nell'ambiente di esplorazione di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99b5a-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="99b5a-179">Visualizzare la mappa</span><span class="sxs-lookup"><span data-stu-id="99b5a-179">View map</span></span>

<span data-ttu-id="99b5a-180">Se la sottoscrizione ha accesso all'API di Bing Mappe, la mappa degli *stabilimenti* visualizza la posizione geografica e lo stato di tutti gli stabilimenti presenti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="99b5a-181">Per esaminare i dettagli, fare clic sulle località visualizzate sulla mappa.</span><span class="sxs-lookup"><span data-stu-id="99b5a-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Mappa della soluzione preconfigurata di connected factory][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="99b5a-183">Visualizzare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="99b5a-183">View alerts</span></span>

<span data-ttu-id="99b5a-184">Il pannello **Alert** (Avvisi) indica gli avvisi generati a causa di un valore segnalato o un valore OEE/KPI calcolato superiore alla soglia configurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="99b5a-185">Questo pannello visualizza gli avvisi per ogni livello della gerarchia, dalla vista a livello di postazione fino alla vista globale.</span><span class="sxs-lookup"><span data-stu-id="99b5a-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="99b5a-186">Gli avvisi contengono descrizione dell'avviso, data, ora, località e numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="99b5a-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="99b5a-187">È possibile ottenere informazioni dettagliate sulle cause dell'avviso usando i dati di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99b5a-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="99b5a-188">I dati di Time Series Insights vengono visualizzati negli avvisi, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="99b5a-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="99b5a-189">Gli amministratori possono eseguire azioni predefinite sugli avvisi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="99b5a-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="99b5a-190">Chiudere l'avviso.</span><span class="sxs-lookup"><span data-stu-id="99b5a-190">Close the alert.</span></span>
* <span data-ttu-id="99b5a-191">Confermare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="99b5a-191">Acknowledge the alert.</span></span>

<span data-ttu-id="99b5a-192">È anche possibile eseguire operazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="99b5a-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="99b5a-193">Ad esempio, per il nodo OPC UA relativo alla pressione del gruppo di componenti è possibile:</span><span class="sxs-lookup"><span data-stu-id="99b5a-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="99b5a-194">Visualizzare informazioni di supporto in una pagina Web in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="99b5a-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="99b5a-195">Attenuare la causa dell'avviso chiamando un metodo OPC UA sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="99b5a-196">Rendere indisponibili le azioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="99b5a-196">Suppress the availability of the default actions.</span></span>

    ![Avvisi della soluzione preconfigurata di connected factory][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="99b5a-198">Questi avvisi vengono generati da regole specificate in un file di configurazione della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="99b5a-199">Queste regole possono generare avvisi quando i valori di OEE o KPI o del nodo OPC UA superano la soglia configurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="99b5a-200">Il **pannello degli avvisi** indica gli avvisi generati in questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="99b5a-201">Per visualizzare i dettagli di un avviso, fare clic su di esso nel pannello.</span><span class="sxs-lookup"><span data-stu-id="99b5a-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="99b5a-202">Per eseguire altre analisi sui dati dell'avviso, fare clic sul grafico nel pannello degli avvisi per aprire l'ambiente di esplorazione di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99b5a-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="99b5a-203">Per risolvere l'avviso, il pannello mette a disposizione diverse azioni.</span><span class="sxs-lookup"><span data-stu-id="99b5a-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="99b5a-204">Scegliere l'opzione appropriata e fare clic sul pulsante di comando per l'esecuzione dell'azione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="99b5a-205">Visualizzare il valore di OEE (Overall Equipment Efficiency)</span><span class="sxs-lookup"><span data-stu-id="99b5a-205">View overall equipment efficiency</span></span>

<span data-ttu-id="99b5a-206">Il valore di OEE valuta l'efficienza del processo di produzione usando parametri operativi chiave correlati alla produzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="99b5a-207">Il valore di OEE è una misura standard di settore calcolata moltiplicando la disponibilità, le prestazioni e la qualità: OEE = disponibilità x prestazioni x qualità.</span><span class="sxs-lookup"><span data-stu-id="99b5a-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE della soluzione preconfigurata di connected factory][cf-img-oee]

1. <span data-ttu-id="99b5a-209">Per visualizzare il valore di OEE per qualsiasi livello della gerarchia, passare alla vista specifica.</span><span class="sxs-lookup"><span data-stu-id="99b5a-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="99b5a-210">Il valore di OEE per la vista verrà visualizzato nel pannello insieme a tutti gli elementi che costituiscono la percentuale OEE.</span><span class="sxs-lookup"><span data-stu-id="99b5a-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="99b5a-211">Per eseguire altre analisi sul valore di OEE per qualsiasi livello della gerarchia di dati, fare clic sulla percentuale OEE, della disponibilità, delle prestazioni o della qualità.</span><span class="sxs-lookup"><span data-stu-id="99b5a-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="99b5a-212">Si aprirà un pannello contestuale con visualizzazioni di Time Series Insights che indicano i dati dell'ultima ora, delle ultime 24 ore e degli ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="99b5a-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualizzazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-visualization]

3. <span data-ttu-id="99b5a-214">Per eseguire altre analisi sui dati dell'avviso, fare clic sul grafico nel pannello degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="99b5a-215">Si aprirà così l'ambiente di esplorazione di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99b5a-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![Ambiente di esplorazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="99b5a-217">Visualizzare gli indicatori di prestazioni chiave</span><span class="sxs-lookup"><span data-stu-id="99b5a-217">View Key Performance Indicators</span></span>

<span data-ttu-id="99b5a-218">La soluzione offre due indicatori di prestazioni chiave, *unità per ogni ora* ed *energia usata in kWh*.</span><span class="sxs-lookup"><span data-stu-id="99b5a-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI della soluzione preconfigurata di connected factory][cf-img-kpi]

1. <span data-ttu-id="99b5a-220">Per visualizzare le unità per ogni ora o l'energia usata per qualsiasi livello della gerarchia, passare alla vista specifica.</span><span class="sxs-lookup"><span data-stu-id="99b5a-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="99b5a-221">Le unità per ogni ora e l'energia usata verranno visualizzate nel pannello.</span><span class="sxs-lookup"><span data-stu-id="99b5a-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="99b5a-222">Per eseguire altre analisi sulle unità per ogni ora o sull'energia usata per qualsiasi livello della gerarchia, fare clic sul misuratore nel pannello **Key Performance Indicators** (Indicatori di prestazioni chiave).</span><span class="sxs-lookup"><span data-stu-id="99b5a-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="99b5a-223">Si aprirà un pannello contestuale con visualizzazioni di Time Series Insights che indicano i dati dell'ultima ora, delle ultime 24 ore e degli ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="99b5a-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="99b5a-224">Analisi dello scenario</span><span class="sxs-lookup"><span data-stu-id="99b5a-224">Scenario review</span></span>

<span data-ttu-id="99b5a-225">In questo scenario sono stati monitorati i valori di OEE e KPI nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="99b5a-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="99b5a-226">È stato quindi usato Time Series Insights per ottenere altre informazioni e analizzare i dati di telemetria per OEE e KPI al fine di rilevare le anomalie.</span><span class="sxs-lookup"><span data-stu-id="99b5a-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="99b5a-227">È stato anche usato il pannello degli avvisi per visualizzare i problemi degli stabilimenti e le azioni disponibili per risolvere l'avviso.</span><span class="sxs-lookup"><span data-stu-id="99b5a-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="99b5a-228">Altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="99b5a-228">Other features</span></span>

<span data-ttu-id="99b5a-229">Le sezioni seguenti descrivono alcune funzionalità aggiuntive della soluzione di connected factory non descritte nello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="99b5a-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="99b5a-230">Applicare filtri</span><span class="sxs-lookup"><span data-stu-id="99b5a-230">Apply filters</span></span>

1. <span data-ttu-id="99b5a-231">Fare clic sulla **freccia di espansione** per visualizzare un elenco dei filtri disponibili nel pannello delle località degli stabilimenti o nel pannello degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="99b5a-232">Verrà visualizzato il pannello dei filtri.</span><span class="sxs-lookup"><span data-stu-id="99b5a-232">The filters panel is displayed for you.</span></span> 

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter]

3. <span data-ttu-id="99b5a-234">Scegliere il filtro necessario.</span><span class="sxs-lookup"><span data-stu-id="99b5a-234">Choose the filter that you require.</span></span> <span data-ttu-id="99b5a-235">È anche possibile digitare testo libero nei campi di filtro.</span><span class="sxs-lookup"><span data-stu-id="99b5a-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="99b5a-236">Il filtro verrà quindi applicato.</span><span class="sxs-lookup"><span data-stu-id="99b5a-236">The filter is then applied for you.</span></span> <span data-ttu-id="99b5a-237">Lo stato del filtro viene visualizzato nel dashboard anche tramite un imbuto visibile nelle tabelle degli stabilimenti e degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="99b5a-239">Un filtro attivo non ha effetto sui valori di OEE e KPI visualizzati, filtra solo il contenuto dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="99b5a-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="99b5a-240">Per cancellare un filtro, fare clic sull'imbuto e quindi sul filtro nel pannello contestuale dei filtri.</span><span class="sxs-lookup"><span data-stu-id="99b5a-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="99b5a-241">Il testo **All** (Tutti) viene visualizzato nelle tabelle degli stabilimenti e degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="99b5a-242">Esplorare un server OPC UA</span><span class="sxs-lookup"><span data-stu-id="99b5a-242">Browse an OPC UA server</span></span>

<span data-ttu-id="99b5a-243">Quando si distribuisce la soluzione preconfigurata, viene effettuato automaticamente il provisioning dei server OPC UA simulati che è possibile esplorare tramite il browser della soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="99b5a-244">Questi server sono *server OPC UA simulati* .</span><span class="sxs-lookup"><span data-stu-id="99b5a-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="99b5a-245">I server simulati consentono di provare facilmente la soluzione preconfigurata senza la necessità di distribuire server fisici reali.</span><span class="sxs-lookup"><span data-stu-id="99b5a-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="99b5a-246">Per connettere un server OPC UA reale alla soluzione, vedere l'esercitazione [Connettere il dispositivo OPC UA alla soluzione preconfigurata di connected factory][lnk-connect-cf].</span><span class="sxs-lookup"><span data-stu-id="99b5a-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="99b5a-247">Fare clic sull'**icona dello stabilimento** nella barra di spostamento del dashboard.</span><span class="sxs-lookup"><span data-stu-id="99b5a-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Browser dei server della soluzione preconfigurata di connected factory][cf-img-server-browser]

2. <span data-ttu-id="99b5a-249">Scegliere uno dei server dall'elenco preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="99b5a-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="99b5a-250">Questo elenco visualizza i server distribuiti nella soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Selezione del server della soluzione preconfigurata di connected factory][cf-img-server-choice]

3. <span data-ttu-id="99b5a-252">Fare clic su **Connect** (Connetti). Verrà visualizzata una finestra di dialogo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="99b5a-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="99b5a-253">Per la simulazione è possibile fare clic su **Proceed** (Continua)</span><span class="sxs-lookup"><span data-stu-id="99b5a-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="99b5a-254">Per espandere uno dei nodi dell'albero dei server, fare clic su di esso.</span><span class="sxs-lookup"><span data-stu-id="99b5a-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="99b5a-255">I nodi che pubblicano i dati di telemetria hanno un segno di spunta accanto.</span><span class="sxs-lookup"><span data-stu-id="99b5a-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Albero dei server della soluzione preconfigurata di connected factory][cf-img-server-tree]

5. <span data-ttu-id="99b5a-257">Fare clic con il pulsante destro del mouse su un elemento per leggere, scrivere, pubblicare o chiamare il nodo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="99b5a-258">Le azioni disponibili variano a seconda delle autorizzazioni e degli attributi del nodo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="99b5a-259">L'opzione di lettura visualizza un pannello contestuale con il valore del nodo specifico.</span><span class="sxs-lookup"><span data-stu-id="99b5a-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="99b5a-260">L'opzione di scrittura visualizza un pannello contestuale in cui è possibile immettere un nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="99b5a-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="99b5a-261">L'opzione di chiamata visualizza un nodo in cui è possibile immettere i parametri per la chiamata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="99b5a-262">Pubblicare un nodo</span><span class="sxs-lookup"><span data-stu-id="99b5a-262">Publish a node</span></span>

<span data-ttu-id="99b5a-263">Quando si esplora un *server OPC UA simulato* è anche possibile scegliere di pubblicare nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="99b5a-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="99b5a-264">È possibile analizzare i dati di telemetria da questi nodi nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="99b5a-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="99b5a-265">Questi *server OPC UA simulati* consentono di provare facilmente la soluzione preconfigurata senza distribuire dispositivi fisici reali.</span><span class="sxs-lookup"><span data-stu-id="99b5a-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="99b5a-266">Passare a un nodo da pubblicare nell'albero del browser dei server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="99b5a-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="99b5a-267">Fare clic con il pulsante destro del mouse sul nodo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-267">Right-click the node.</span></span>

3. <span data-ttu-id="99b5a-268">Scegliere **Publish** (Pubblica).</span><span class="sxs-lookup"><span data-stu-id="99b5a-268">Choose **Publish**.</span></span>

    ![Pubblicare un nodo nella soluzione di connected factory][cf-img-publish-node]

4. <span data-ttu-id="99b5a-270">Verrà visualizzato un pannello contestuale che indica che la pubblicazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="99b5a-271">Il nodo viene visualizzato al livello delle postazioni con un segno di spunta accanto.</span><span class="sxs-lookup"><span data-stu-id="99b5a-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Pubblicazione eseguita nella soluzione preconfigurata di connected factory][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="99b5a-273">Comando e controllo</span><span class="sxs-lookup"><span data-stu-id="99b5a-273">Command and control</span></span>

<span data-ttu-id="99b5a-274">La soluzione di connected factory consente di comandare e gestire i dispositivi industriali direttamente dal cloud.</span><span class="sxs-lookup"><span data-stu-id="99b5a-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="99b5a-275">È possibile usare questa funzionalità per rispondere agli avvisi generati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="99b5a-276">È ad esempio possibile inviare un comando al dispositivo dal cloud.</span><span class="sxs-lookup"><span data-stu-id="99b5a-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="99b5a-277">È possibile trovare i comandi disponibili nel nodo **StationCommands** dell'albero del browser dei server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="99b5a-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="99b5a-278">In questo scenario si apre una valvola di sfiato nella postazione di un gruppo di componenti di una linea di produzione situata a Monaco di Baviera.</span><span class="sxs-lookup"><span data-stu-id="99b5a-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="99b5a-279">Per usare la funzionalità di comando e controllo è necessario il ruolo **Amministratore** per la distribuzione della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="99b5a-280">Passare al nodo **StationCommands** nell'albero del browser dei server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="99b5a-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="99b5a-281">Scegliere il comando che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="99b5a-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="99b5a-282">Fare clic con il pulsante destro del mouse sul nodo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-282">Right-click the node.</span></span>

4. <span data-ttu-id="99b5a-283">Scegliere **Call** (Chiama).</span><span class="sxs-lookup"><span data-stu-id="99b5a-283">Choose **Call**.</span></span>

    ![Comando di chiamata della soluzione preconfigurata di connected factory][cf-img-call-command]

5. <span data-ttu-id="99b5a-285">Viene visualizzato un pannello contestuale che indica il metodo che si sta per chiamare e i dettagli dei parametri applicabili.</span><span class="sxs-lookup"><span data-stu-id="99b5a-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="99b5a-286">Scegliere **Call** (Chiama).</span><span class="sxs-lookup"><span data-stu-id="99b5a-286">Choose **Call**.</span></span>

    ![Contesto di chiamata della soluzione preconfigurata di connected factory][cf-img-call-context]

7. <span data-ttu-id="99b5a-288">Il pannello contestuale viene aggiornato per indicare che la chiamata al metodo ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="99b5a-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="99b5a-289">È possibile verificare che la chiamata abbia avuto esito positivo leggendo il valore del nodo della pressione aggiornato in seguito alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Chiamata eseguita nella soluzione preconfigurata di connected factory][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="99b5a-291">Dietro le quinte</span><span class="sxs-lookup"><span data-stu-id="99b5a-291">Behind the scenes</span></span>

<span data-ttu-id="99b5a-292">Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione crea più risorse nella sottoscrizione di Azure selezionata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="99b5a-293">È possibile visualizzare queste risorse nel [portale][lnk-portal] di Azure.</span><span class="sxs-lookup"><span data-stu-id="99b5a-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="99b5a-294">Il processo di distribuzione crea un **gruppo di risorse** con un nome basato sul nome scelto per la soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="99b5a-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Soluzione preconfigurata nel portale di Azure][img-cf-portal]

<span data-ttu-id="99b5a-296">È possibile visualizzare le impostazioni di ogni risorsa selezionandola nell'elenco di risorse nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="99b5a-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="99b5a-297">È anche possibile visualizzare il codice sorgente per la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="99b5a-298">Il codice sorgente della soluzione preconfigurata di connected factory si trova nel repository GitHub [azure-iot-connected-factory][lnk-cfgithub]:</span><span class="sxs-lookup"><span data-stu-id="99b5a-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="99b5a-299">Al termine, è possibile eliminare la soluzione preconfigurata dalla sottoscrizione di Azure nel sito [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="99b5a-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="99b5a-300">Questo sito consente di eliminare facilmente tutte le risorse di cui è stato effettuato il provisioning quando si è creata la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="99b5a-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="99b5a-301">Per assicurarsi di eliminare tutti gli elementi correlati alla soluzione preconfigurata, eseguire l'eliminazione dal sito [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="99b5a-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="99b5a-302">Non eliminare il gruppo di risorse nel portale.</span><span class="sxs-lookup"><span data-stu-id="99b5a-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99b5a-303">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99b5a-303">Next Steps</span></span>

<span data-ttu-id="99b5a-304">Dopo aver distribuito una soluzione preconfigurata è possibile proseguire con l'introduzione a IoT Suite vedendo gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="99b5a-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="99b5a-305">[Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="99b5a-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="99b5a-306">[Connettere il dispositivo alla soluzione preconfigurata di connected factory][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="99b5a-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="99b5a-307">[Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="99b5a-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md