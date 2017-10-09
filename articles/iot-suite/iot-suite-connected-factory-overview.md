---
title: Panoramica di factory di connesso aaaAzure IoT Suite | Documenti Microsoft
description: Una descrizione di hello Azure IoT Suite connesso soluzione factory preconfigurato.
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="81266-103">Introduzione a soluzioni factory preconfigurato hello connesso</span><span class="sxs-lookup"><span data-stu-id="81266-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="81266-104">Azure IoT Suite [preconfigurato soluzioni] [ lnk-preconfigured-solutions] combinare più Azure IoT servizi toodeliver end-to-end soluzioni che implementano i comuni scenari di business IoT.</span><span class="sxs-lookup"><span data-stu-id="81266-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="81266-105">Hello *factory connesso* soluzione preconfigurata si connette i dispositivi industriali tooand monitoraggi.</span><span class="sxs-lookup"><span data-stu-id="81266-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="81266-106">È possibile utilizzare hello soluzione tooanalyze hello flusso di dati dai dispositivi e toodrive operativo produttività e la redditività.</span><span class="sxs-lookup"><span data-stu-id="81266-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="81266-107">Questa esercitazione viene illustrato il modo in cui tooprovision hello connesse factory preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="81266-108">Illustra anche funzionalità di base della soluzione hello preconfigurato hello.</span><span class="sxs-lookup"><span data-stu-id="81266-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="81266-109">Molte di queste funzionalità accessibili dalla soluzione hello *dashboard* che distribuisce come parte della soluzione preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="81266-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Dashboard della soluzione preconfigurata di connected factory][img-cf-home]

<span data-ttu-id="81266-111">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="81266-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="81266-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="81266-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="81266-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="81266-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="81266-114">Eseguire il provisioning hello soluzione</span><span class="sxs-lookup"><span data-stu-id="81266-114">Provision hello solution</span></span>

1. <span data-ttu-id="81266-115">Accedere utilizzando le credenziali dell'account Azure tooazureiotsuite.com e fare clic su "**+**" toocreate una soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="81266-116">Fare clic su **selezionare** su hello **factory connesso** riquadro.</span><span class="sxs-lookup"><span data-stu-id="81266-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="81266-117">Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di connected factory.</span><span class="sxs-lookup"><span data-stu-id="81266-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="81266-118">Seleziona hello **sottoscrizione** e **area** si desidera toouse tooprovision hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="81266-119">Fare clic su **crea soluzione** hello toobegin processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="81266-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="81266-120">Questo processo è in genere richiede diversi minuti toorun.</span><span class="sxs-lookup"><span data-stu-id="81266-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="81266-121">Durante l'attesa per hello toocomplete processo di provisioning</span><span class="sxs-lookup"><span data-stu-id="81266-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="81266-122">Fare clic sul riquadro hello per la soluzione con **Provisioning** stato.</span><span class="sxs-lookup"><span data-stu-id="81266-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="81266-123">Hello preavviso **Provisioning stati** come servizi di Azure vengono distribuiti nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81266-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="81266-124">Una volta al termine del provisioning, hello modifiche allo stato troppo**pronto**.</span><span class="sxs-lookup"><span data-stu-id="81266-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="81266-125">Fare clic su dettagli di hello riquadro toosee hello della soluzione nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="81266-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="81266-126">Se si verificano problemi di distribuzione di soluzioni hello preconfigurato, esaminare [le autorizzazioni nel sito azureiotsuite.com hello] [ lnk-permissions] hello e [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="81266-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="81266-127">Se persistono problemi hello, creare un ticket di servizio in hello [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="81266-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="81266-128">Sono presenti dettagli che ci si aspetta toosee che non sono elencati per la soluzione?</span><span class="sxs-lookup"><span data-stu-id="81266-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="81266-129">è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="81266-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="81266-130">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="81266-130">Scenario overview</span></span>

<span data-ttu-id="81266-131">Quando si distribuisce hello connesso factory preconfigurato soluzione, viene popolato preliminarmente con le risorse che consentono di toostep tramite uno scenario comune industriale.</span><span class="sxs-lookup"><span data-stu-id="81266-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="81266-132">In questo scenario, le factory diverse connesso report soluzione toohello toocompute necessari valori dei dati di hello efficienza di apparecchiature (OEE) e indicatori di prestazioni chiave (KPI).</span><span class="sxs-lookup"><span data-stu-id="81266-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="81266-133">Hello nelle sezioni seguenti illustrano come fare per:</span><span class="sxs-lookup"><span data-stu-id="81266-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="81266-134">Monitorare stabilimenti, linee di produzione, OEE delle postazioni e valori KPI</span><span class="sxs-lookup"><span data-stu-id="81266-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="81266-135">Analizzare i dati di telemetria hello generati da tali dispositivi utilizzando Azure ora serie Insights</span><span class="sxs-lookup"><span data-stu-id="81266-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="81266-136">Agire sui problemi toofix avvisi</span><span class="sxs-lookup"><span data-stu-id="81266-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="81266-137">Una funzionalità chiave di questo scenario è che è possibile eseguire in modalità remota tutte queste azioni dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="81266-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="81266-138">Non è necessario dispositivi toohello accesso fisico.</span><span class="sxs-lookup"><span data-stu-id="81266-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="81266-139">Dashboard di soluzione hello View</span><span class="sxs-lookup"><span data-stu-id="81266-139">View hello solution dashboard</span></span>

<span data-ttu-id="81266-140">dashboard di soluzione Hello consente soluzione hello distribuito toomanage.</span><span class="sxs-lookup"><span data-stu-id="81266-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="81266-141">Si tratta di una rappresentazione gerarchica della configurazione globale degli stabilimenti.</span><span class="sxs-lookup"><span data-stu-id="81266-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="81266-142">È ad esempio possibile visualizzare OEE e KPI, pubblicare nuovi nodi per la telemetria e attivare avvisi.</span><span class="sxs-lookup"><span data-stu-id="81266-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="81266-143">Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen portale soluzione factory connesso in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="81266-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. <span data-ttu-id="81266-145">Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="81266-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="81266-146">toonavigate tooother aree del portale di hello, utilizzare il menu di hello sulla parte sinistra della pagina hello hello.</span><span class="sxs-lookup"><span data-stu-id="81266-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Dashboard della soluzione preconfigurata di connected factory][cf-img-menu]

<span data-ttu-id="81266-148">dashboard Hello Visualizza hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="81266-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="81266-149">Oggetto **elenco Factory** pannello che mostra lo stato di hello, la posizione e configurazione di produzione corrente nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="81266-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="81266-150">Quando si esegue prima soluzione hello, esistono numerosi dispositivi simulati.</span><span class="sxs-lookup"><span data-stu-id="81266-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="81266-151">simulazione di linea di produzione Hello è composta da tre reale OPC UA server per ogni linea di produzione che eseguano attività simulata e condividere i dati.</span><span class="sxs-lookup"><span data-stu-id="81266-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="81266-152">Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="81266-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="81266-153">Oggetto **mappa** che consente di visualizzare hello posizione di ogni dispositivo connesso toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="81266-154">soluzione hello è possibile utilizzare informazioni tooplot di hello API di Bing mappe nella mappa hello.</span><span class="sxs-lookup"><span data-stu-id="81266-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="81266-155">Se la sottoscrizione è abilitata per l'API di Bing Mappe per le aziende, questa funzionalità viene usata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="81266-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="81266-156">In caso contrario, vedere hello [domande frequenti su] [ lnk-faq] toolearn come toomake hello dinamici della mappa.</span><span class="sxs-lookup"><span data-stu-id="81266-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="81266-157">Un pannello degli **avvisi** che visualizza gli avvisi generati quando un valore OEE/KPI o di telemetria supera una soglia specifica.</span><span class="sxs-lookup"><span data-stu-id="81266-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="81266-158">Un **efficienza apparecchiature** pannello che mostra i valori OEE hello per l'intera azienda hello o hello factory/produzione riga/stazione si sta visualizzando.</span><span class="sxs-lookup"><span data-stu-id="81266-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="81266-159">Questo valore viene aggregato dal livello di organizzazione toohello visualizzazione hello stazione.</span><span class="sxs-lookup"><span data-stu-id="81266-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="81266-160">Figura OEE Hello e i relativi elementi costitutivi possono essere ulteriormente analizzati.</span><span class="sxs-lookup"><span data-stu-id="81266-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="81266-161">**Indicatori di prestazioni chiave** pannello che visualizza il numero di hello di unità prodotte e di energia utilizzata dall'intera azienda hello o hello factory/produzione/stazione si sta visualizzando.</span><span class="sxs-lookup"><span data-stu-id="81266-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="81266-162">Questi valori vengono aggregati da un livello di organizzazione toohello visualizzazione stazione.</span><span class="sxs-lookup"><span data-stu-id="81266-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="81266-163">Visualizzare gli stabilimenti</span><span class="sxs-lookup"><span data-stu-id="81266-163">View factories</span></span>

<span data-ttu-id="81266-164">Hello *factory* pannello Mostra hello posizione geografica di tutte le factory hello nei soluzione hello, stato e configurazione di produzione corrente.</span><span class="sxs-lookup"><span data-stu-id="81266-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="81266-165">Dall'elenco di percorsi hello, è possibile passare toohello altri livelli nella gerarchia di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="81266-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="81266-166">righe Hello hello elenco sono collegamenti ipertestuali che collegano i dettagli delle linee di produzione hello in tale posizione.</span><span class="sxs-lookup"><span data-stu-id="81266-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="81266-167">È quindi possibile toodrill i dettagli di linea di produzione hello e toohello visualizzazione a livello di espansione verso il basso.</span><span class="sxs-lookup"><span data-stu-id="81266-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="81266-168">È inoltre possibile applicare un elenco di filtri toohello.</span><span class="sxs-lookup"><span data-stu-id="81266-168">You can also apply a filter toohello list.</span></span>

![Stabilimenti della soluzione preconfigurata di connected factory][cf-img-factories] 

1. <span data-ttu-id="81266-170">Hello **pannello Factory** Mostra hello elenco di factory per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="81266-171">elenco di factory Hello viene inizialmente sei factory creata dal processo di provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="81266-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="81266-172">È possibile aggiungere soluzioni toohello altri dispositivi simulati e fisico.</span><span class="sxs-lookup"><span data-stu-id="81266-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="81266-173">dettagli di hello tooview di una factory, fare clic su riga hello nell'elenco di factory hello.</span><span class="sxs-lookup"><span data-stu-id="81266-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="81266-174">dettagli di hello tooview di una linea di produzione, fare clic su riga hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="81266-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="81266-175">hello tooview pubblicato nodi OPC UA una stazione in linea di produzione hello, fare clic sulla riga hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="81266-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="81266-176">Dettagli tooview in un nodo specifico nella stazione hello, fare clic su riga hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="81266-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="81266-177">Questa azione avvia il pannello contesto hello con visualizzazioni ora serie Insights.</span><span class="sxs-lookup"><span data-stu-id="81266-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="81266-178">Fare clic su questi ulteriori analisi di grafici toodo nell'ambiente di hello ora serie Insights explorer.</span><span class="sxs-lookup"><span data-stu-id="81266-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="81266-179">Visualizzare la mappa</span><span class="sxs-lookup"><span data-stu-id="81266-179">View map</span></span>

<span data-ttu-id="81266-180">Se la sottoscrizione ha accesso toohello API di Bing mappe, hello *factory* mappa Mostra la posizione geografica hello e lo stato di tutte le factory hello in soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="81266-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="81266-181">toodrill i dettagli di percorso hello, fare clic su percorsi hello visualizzati nella mappa hello.</span><span class="sxs-lookup"><span data-stu-id="81266-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Mappa della soluzione preconfigurata di connected factory][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="81266-183">Visualizzare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="81266-183">View alerts</span></span>

<span data-ttu-id="81266-184">Hello **avviso** pannello mostra gli avvisi generati a causa di tooa segnalati valore o un valore calcolato di OEE/KPI superare la soglia configurata.</span><span class="sxs-lookup"><span data-stu-id="81266-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="81266-185">Questo consente di visualizzare gli avvisi a ogni livello della gerarchia di hello, dalla visualizzazione globale toohello hello stazione visualizzazione a livello.</span><span class="sxs-lookup"><span data-stu-id="81266-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="81266-186">avvisi di Hello contengono una descrizione dell'avviso hello, data, ora, posizione e numero di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="81266-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="81266-187">È possibile ottenere informazioni dettagliate nei dati toohello che ha determinato avviso hello utilizzando hello dati di Insights di serie di tempo.</span><span class="sxs-lookup"><span data-stu-id="81266-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="81266-188">Hello ora serie Insights dati viene visualizzati nella hello avvisi, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="81266-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="81266-189">Se si è un amministratore, è possibile eseguire le azioni predefinite agli avvisi di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81266-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="81266-190">Avviso di hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="81266-190">Close hello alert.</span></span>
* <span data-ttu-id="81266-191">Confermare l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="81266-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="81266-192">È anche possibile eseguire operazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="81266-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="81266-193">Ad esempio, per hello pressione OPC UA nodo di hello Assembly, è possibile:</span><span class="sxs-lookup"><span data-stu-id="81266-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="81266-194">Visualizzare informazioni di supporto in una pagina Web in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="81266-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="81266-195">Mitigare causa hello dell'avviso hello chiamando un metodo OPC UA sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="81266-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="81266-196">Esclusione di disponibilità hello di azioni predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="81266-196">Suppress hello availability of hello default actions.</span></span>

    ![Avvisi della soluzione preconfigurata di connected factory][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="81266-198">Gli avvisi vengono generati da regole che vengono specificate in un file di configurazione nella soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="81266-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="81266-199">Queste regole possono generare avvisi quando hello OEE o cifre di indicatore KPI o i valori del nodo UA OPC superano la soglia configurata.</span><span class="sxs-lookup"><span data-stu-id="81266-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="81266-200">Hello **pannello avvisi** Mostra hello gli avvisi generati in questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="81266-201">dettagli di hello tooview di un avviso, fare clic su avviso hello nel Pannello di hello avvisi.</span><span class="sxs-lookup"><span data-stu-id="81266-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="81266-202">toofurther analizzare i dati di avviso hello, fare clic su grafico hello nell'ambiente di hello pannello avviso tooopen hello ora serie Insights explorer.</span><span class="sxs-lookup"><span data-stu-id="81266-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="81266-203">avviso di hello tooaddress, sono disponibili nel Pannello di avviso hello diverse azioni.</span><span class="sxs-lookup"><span data-stu-id="81266-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="81266-204">Scegliere hello opzione appropriata per l'utente e fare clic su hello eseguire pulsante di comando di azione.</span><span class="sxs-lookup"><span data-stu-id="81266-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="81266-205">Visualizzare il valore di OEE (Overall Equipment Efficiency)</span><span class="sxs-lookup"><span data-stu-id="81266-205">View overall equipment efficiency</span></span>

<span data-ttu-id="81266-206">Tariffe OEE hello l'efficienza del processo di produzione di hello utilizzando una chiave parametri operativi correlate alla produzione.</span><span class="sxs-lookup"><span data-stu-id="81266-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="81266-207">OEE è uno standard misura calcolata moltiplicando la tariffa di disponibilità hello, velocità delle prestazioni e la percentuale di qualità: OEE = disponibilità x qualità delle prestazioni x.</span><span class="sxs-lookup"><span data-stu-id="81266-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE della soluzione preconfigurata di connected factory][cf-img-oee]

1. <span data-ttu-id="81266-209">tooview OEE di qualsiasi livello di gerarchia hello, passare toohello di visualizzazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="81266-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="81266-210">OEE per la visualizzazione viene visualizzato nel Pannello di hello insieme a tutti gli elementi che costituiscono hello percentuale OEE hello.</span><span class="sxs-lookup"><span data-stu-id="81266-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="81266-211">toofurther analizzare hello OEE di qualsiasi livello di dati della gerarchia hello, fare clic su hello OEE, disponibilità, prestazioni o la percentuale di qualità.</span><span class="sxs-lookup"><span data-stu-id="81266-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="81266-212">Contesto verrà visualizzato un pannello con tempo serie Insights spenta visualizzazioni che mostrano i dati da hello ultima ora, ultime 24 ore e ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="81266-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualizzazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-visualization]

3. <span data-ttu-id="81266-214">toofurther analizzare i dati di avviso hello, fare clic su grafico hello nel Pannello di avviso di hello.</span><span class="sxs-lookup"><span data-stu-id="81266-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="81266-215">Questa azione apre l'ambiente di hello ora serie Insights explorer.</span><span class="sxs-lookup"><span data-stu-id="81266-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Ambiente di esplorazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="81266-217">Visualizzare gli indicatori di prestazioni chiave</span><span class="sxs-lookup"><span data-stu-id="81266-217">View Key Performance Indicators</span></span>

<span data-ttu-id="81266-218">soluzione Hello fornisce due indicatori di prestazioni chiave, *unità per ora* e *energia nelle kWh*.</span><span class="sxs-lookup"><span data-stu-id="81266-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI della soluzione preconfigurata di connected factory][cf-img-kpi]

1. <span data-ttu-id="81266-220">tooview unità per ogni ora o energia usata per qualsiasi livello nella gerarchia di hello, passare toohello di visualizzazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="81266-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="81266-221">unità di Hello per ora e di energia usate visualizzato nel Pannello di hello.</span><span class="sxs-lookup"><span data-stu-id="81266-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="81266-222">tooanalyze unità per ogni ora o energia usata per qualsiasi livello nella gerarchia di hello ulteriormente, fare clic su misuratore hello in hello **indicatori di prestazioni chiave** pannello.</span><span class="sxs-lookup"><span data-stu-id="81266-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="81266-223">Verrà visualizzato un pannello di contesto con visualizzazioni ora serie Insights con tecnologia consentendo dati tooview hello ultima ora, hello ultime 24 ore e ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="81266-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="81266-224">Analisi dello scenario</span><span class="sxs-lookup"><span data-stu-id="81266-224">Scenario review</span></span>

<span data-ttu-id="81266-225">In questo scenario, i valori OEE e indicatori KPI di factory, nel dashboard di hello è stata monitorata.</span><span class="sxs-lookup"><span data-stu-id="81266-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="81266-226">Quindi utilizzato tooprovide ora serie approfondimenti più informazioni toohelp esaminare ulteriormente i dati di telemetria hello per toohelp OEE e indicatori KPI con il rilevamento di anomalie.</span><span class="sxs-lookup"><span data-stu-id="81266-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="81266-227">Sono stati usati anche i problemi di hello pannello avviso tooview con le factory e avviso di hello azioni disponibili tooyou tooresolve hello è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="81266-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="81266-228">Altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="81266-228">Other features</span></span>

<span data-ttu-id="81266-229">Hello le sezioni seguenti vengono descritte alcune funzionalità aggiuntive di hello connesso factory soluzione che non sono descritti nello scenario precedente hello.</span><span class="sxs-lookup"><span data-stu-id="81266-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="81266-230">Applicare filtri</span><span class="sxs-lookup"><span data-stu-id="81266-230">Apply filters</span></span>

1. <span data-ttu-id="81266-231">Fare clic su hello **freccia di espansione** toodisplay un elenco dei filtri disponibili nel Pannello di percorsi di factory hello o pannello avvisi hello.</span><span class="sxs-lookup"><span data-stu-id="81266-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="81266-232">Pannello filtri Hello è visualizzato per l'utente.</span><span class="sxs-lookup"><span data-stu-id="81266-232">hello filters panel is displayed for you.</span></span> 

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter]

3. <span data-ttu-id="81266-234">Scegliere Filtro hello necessari.</span><span class="sxs-lookup"><span data-stu-id="81266-234">Choose hello filter that you require.</span></span> <span data-ttu-id="81266-235">È inoltre possibile tootype testo libero nei campi filtro hello.</span><span class="sxs-lookup"><span data-stu-id="81266-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="81266-236">Hello filtro viene applicato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="81266-236">hello filter is then applied for you.</span></span> <span data-ttu-id="81266-237">lo stato del filtro Hello viene inoltre visualizzato nel dashboard di hello tramite un grafico a imbuto consente di visualizzare nella factory hello e segnala le tabelle.</span><span class="sxs-lookup"><span data-stu-id="81266-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="81266-239">Un filtro attivo non influisce sulla hello visualizzato valori OEE e indicatori KPI, ma solo di filtrare il contenuto di elenco hello.</span><span class="sxs-lookup"><span data-stu-id="81266-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="81266-240">tooclear un filtro, fare clic su grafico a imbuto hello e fare clic su filtro nel riquadro del contesto filtro hello.</span><span class="sxs-lookup"><span data-stu-id="81266-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="81266-241">testo Hello **tutti** viene visualizzato nella factory hello e gli avvisi di tabelle.</span><span class="sxs-lookup"><span data-stu-id="81266-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="81266-242">Esplorare un server OPC UA</span><span class="sxs-lookup"><span data-stu-id="81266-242">Browse an OPC UA server</span></span>

<span data-ttu-id="81266-243">Quando si distribuisce la soluzione hello preconfigurato, automaticamente effettuato il provisioning di server OPC UA simulati che è possibile esplorare tramite browser soluzione hello</span><span class="sxs-lookup"><span data-stu-id="81266-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="81266-244">Questi server sono *server OPC UA simulati* .</span><span class="sxs-lookup"><span data-stu-id="81266-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="81266-245">Server simulato semplificano automaticamente tooexperiment con la soluzione hello preconfigurato senza hello necessità toodeploy reale server fisici.</span><span class="sxs-lookup"><span data-stu-id="81266-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="81266-246">Se si desidera tooconnect una soluzione di toohello server OPC UA reale, vedere hello [connettere la soluzione di factory preconfigurato OPC UA dispositivo connesso toohello] [ lnk-connect-cf] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81266-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="81266-247">Fare clic su hello **icona factory** nella barra di navigazione del dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="81266-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Browser dei server della soluzione preconfigurata di connected factory][cf-img-server-browser]

2. <span data-ttu-id="81266-249">Scegliere uno dei server hello da elenco preconfigurato hello.</span><span class="sxs-lookup"><span data-stu-id="81266-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="81266-250">Questo elenco Mostra i server hello che vengono distribuiti automaticamente nella soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="81266-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Selezione del server della soluzione preconfigurata di connected factory][cf-img-server-choice]

3. <span data-ttu-id="81266-252">Fare clic su **Connect** (Connetti). Verrà visualizzata una finestra di dialogo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="81266-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="81266-253">Per la simulazione di hello è sicuro tooclick **continua**</span><span class="sxs-lookup"><span data-stu-id="81266-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="81266-254">tooexpand uno qualsiasi dei nodi di hello nell'albero di server hello, farvi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="81266-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="81266-255">I nodi che pubblicano i dati di telemetria hanno un segno di spunta accanto.</span><span class="sxs-lookup"><span data-stu-id="81266-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Albero dei server della soluzione preconfigurata di connected factory][cf-img-server-tree]

5. <span data-ttu-id="81266-257">Fare doppio clic su un elemento di tooread, scrivere, pubblicare o chiamare tale nodo.</span><span class="sxs-lookup"><span data-stu-id="81266-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="81266-258">Hello azioni disponibili tooyou dipendono le autorizzazioni e gli attributi di hello del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="81266-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="81266-259">Hello lettura opzione toodisplays un pannello del contesto che mostra il valore di hello di nodo specifico hello.</span><span class="sxs-lookup"><span data-stu-id="81266-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="81266-260">Hello scrivere opzione consente di visualizzare un pannello del contesto in cui è possibile immettere un nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="81266-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="81266-261">opzione di chiamata Hello Visualizza un nodo in cui è possibile immettere i parametri di hello per chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="81266-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="81266-262">Pubblicare un nodo</span><span class="sxs-lookup"><span data-stu-id="81266-262">Publish a node</span></span>

<span data-ttu-id="81266-263">Quando si Esplora un *server OPC UA simulato*, è anche possibile scegliere toopublish nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="81266-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="81266-264">È possibile analizzare i dati di telemetria hello da questi nodi nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="81266-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="81266-265">Questi *simulato Server OPC UA* renderlo tooexperiment semplice con la soluzione hello preconfigurato senza distribuire i dispositivi fisici reali.</span><span class="sxs-lookup"><span data-stu-id="81266-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="81266-266">Sfoglia tooa nodo nell'albero del server OPC UA browser che si desidera toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="81266-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="81266-267">Fare clic sul nodo hello.</span><span class="sxs-lookup"><span data-stu-id="81266-267">Right-click hello node.</span></span>

3. <span data-ttu-id="81266-268">Scegliere **Publish** (Pubblica).</span><span class="sxs-lookup"><span data-stu-id="81266-268">Choose **Publish**.</span></span>

    ![Pubblicare un nodo nella soluzione di connected factory][cf-img-publish-node]

4. <span data-ttu-id="81266-270">Verrà visualizzato un pannello di contesto che indica che hello pubblicazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="81266-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="81266-271">nodo Hello viene visualizzato nella visualizzazione di livello stazione hello con un segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="81266-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Pubblicazione eseguita nella soluzione preconfigurata di connected factory][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="81266-273">Comando e controllo</span><span class="sxs-lookup"><span data-stu-id="81266-273">Command and control</span></span>

<span data-ttu-id="81266-274">factory connesso Hello consente di comando e controllare i dispositivi di settore direttamente dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="81266-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="81266-275">È possibile utilizzare questo tooalerts toorespond funzionalità generato per dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="81266-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="81266-276">Ad esempio, è possibile inviare un dispositivo toohello comando dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="81266-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="81266-277">È possibile trovare i comandi disponibili hello in hello **StationCommands** nodo nell'albero di browser server OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="81266-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="81266-278">In questo scenario, si apre una versione valvola sulla stazione di assembly hello di una linea di produzione Monaco.</span><span class="sxs-lookup"><span data-stu-id="81266-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="81266-279">funzionalità di comando e controllo di hello toouse, è necessario essere in hello **amministratore** ruolo per hello preconfigurato distribuzione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="81266-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="81266-280">Sfoglia toohello **StationCommands** nodo nell'albero del browser server OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="81266-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="81266-281">Scegliere il comando hello che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="81266-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="81266-282">Fare clic sul nodo hello.</span><span class="sxs-lookup"><span data-stu-id="81266-282">Right-click hello node.</span></span>

4. <span data-ttu-id="81266-283">Scegliere **Call** (Chiama).</span><span class="sxs-lookup"><span data-stu-id="81266-283">Choose **Call**.</span></span>

    ![Comando di chiamata della soluzione preconfigurata di connected factory][cf-img-call-command]

5. <span data-ttu-id="81266-285">Viene indicato quale metodo si sta toocall ed eventuali dettagli del parametro è applicabile, viene visualizzato un riquadro contesto.</span><span class="sxs-lookup"><span data-stu-id="81266-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="81266-286">Scegliere **Call** (Chiama).</span><span class="sxs-lookup"><span data-stu-id="81266-286">Choose **Call**.</span></span>

    ![Contesto di chiamata della soluzione preconfigurata di connected factory][cf-img-call-context]

7. <span data-ttu-id="81266-288">Pannello contesto Hello è tooinform aggiornato che hello chiamata al metodo ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="81266-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="81266-289">È possibile verificare chiamata hello ha avuto esito positivo, leggere il valore di hello del nodo di pressione hello aggiornati in seguito chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="81266-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Chiamata eseguita nella soluzione preconfigurata di connected factory][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="81266-291">Background hello</span><span class="sxs-lookup"><span data-stu-id="81266-291">Behind hello scenes</span></span>

<span data-ttu-id="81266-292">Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione hello crea più risorse hello Azure sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="81266-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="81266-293">È possibile visualizzare queste risorse in Azure hello [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="81266-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="81266-294">il processo di distribuzione Hello crea un **gruppo di risorse** con un nome basato sul nome hello scelto per la soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="81266-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Soluzione preconfigurata in hello portale di Azure][img-cf-portal]

<span data-ttu-id="81266-296">È possibile visualizzare le impostazioni di hello di ogni risorsa selezionandolo nell'elenco di hello delle risorse nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="81266-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="81266-297">È anche possibile visualizzare il codice sorgente hello per soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="81266-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="81266-298">Hello factory connesso preconfigurato soluzione codice sorgente è in hello [azure iot-connessione-factory] [ lnk-cfgithub] repository GitHub:</span><span class="sxs-lookup"><span data-stu-id="81266-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="81266-299">Al termine, è possibile eliminare la soluzione hello preconfigurato dalla sottoscrizione di Azure su hello [azureiotsuite.com] [ lnk-azureiotsuite] sito.</span><span class="sxs-lookup"><span data-stu-id="81266-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="81266-300">Questo sito consente tooeasily Elimina che tutte le risorse che è sono eseguito il provisioning durante la creazione di soluzioni hello preconfigurato di hello.</span><span class="sxs-lookup"><span data-stu-id="81266-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="81266-301">tooensure di eliminare tutti gli elementi correlati soluzione toohello preconfigurato, l'eliminazione hello [azureiotsuite.com] [ lnk-azureiotsuite] sito.</span><span class="sxs-lookup"><span data-stu-id="81266-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="81266-302">Non eliminare il gruppo di risorse hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="81266-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81266-303">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81266-303">Next Steps</span></span>

<span data-ttu-id="81266-304">Dopo aver distribuito una soluzione appropriata preconfigurato, è possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="81266-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="81266-305">[Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="81266-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="81266-306">[Connettere la soluzione di factory connesso preconfigurato toohello dispositivo][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="81266-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="81266-307">[Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="81266-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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