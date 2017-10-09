---
title: manutenzione aaaPredictive preconfigurato soluzione | Documenti Microsoft
description: Una descrizione di manutenzione predittiva di hello Azure IoT Suite preconfigurato soluzione.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="75158-103">Panoramica della soluzione preconfigurata di manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="75158-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="75158-104">Hello *manutenzione predittiva* [preconfigurato soluzione] [ lnk_preconfigured_solutions] è uno dei hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] preconfigurato soluzioni.</span><span class="sxs-lookup"><span data-stu-id="75158-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="75158-105">Questa soluzione integra una raccolta di dati di telemetria in tempo reale dei dispositivi con un modello predittivo creato utilizzando [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="75158-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="75158-106">Con Azure IoT Suite, è possibile rapidamente e facilmente connettersi asset monitoraggio tooand e analizzare dati di telemetria in tempo reale nei dashboard e visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="75158-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="75158-107">Nella soluzione di manutenzione predittiva hello, visualizzazioni e dashboard hello offrono nuova informazione che può unità efficienza e migliorare i profitti.</span><span class="sxs-lookup"><span data-stu-id="75158-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="75158-108">Hello Scenario</span><span class="sxs-lookup"><span data-stu-id="75158-108">hello Scenario</span></span>

<span data-ttu-id="75158-109">Fabrikam è una compagnia aerea locale che si concentra sulle esperienze eccezionali dei clienti a prezzi competitivi.</span><span class="sxs-lookup"><span data-stu-id="75158-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="75158-110">Una causa di ritardi dei voli sono i problemi di manutenzione e la manutenzione dei motori degli aeromobili è particolarmente complessa.</span><span class="sxs-lookup"><span data-stu-id="75158-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="75158-111">Fabrikam deve evitare malfunzionamenti del motore durante la fase di trasferimento tutti i costi, in modo che controlla regolarmente i motori e pianificazioni in base tooa piano di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="75158-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="75158-112">Tuttavia, aereo motori non sempre accenti hello stesso.</span><span class="sxs-lookup"><span data-stu-id="75158-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="75158-113">Sui motori viene eseguita manutenzione superflua.</span><span class="sxs-lookup"><span data-stu-id="75158-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="75158-114">Ancora più importante, si verificano problemi che possono forzare a terra un aereo fino a quando non viene eseguita la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="75158-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="75158-115">Se un aereo si trova nella posizione in cui hello destra tecnici o pezzi di ricambio non sono disponibili, questi problemi possono risultare particolarmente onerosa.</span><span class="sxs-lookup"><span data-stu-id="75158-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="75158-116">motori di Hello di aereo Fabrikam vengono instrumentati con sensori che consentono di monitorare le condizioni del motore durante la fase di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="75158-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="75158-117">Fabrikam Usa hello manutenzione predittiva soluzione toocollect hello sensore dati raccolti durante il volo hello.</span><span class="sxs-lookup"><span data-stu-id="75158-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="75158-118">Dopo aver anni accumulo di motore operativo e dati di errore, gli esperti di dati di Fabrikam hanno modellata un hello toopredict modo vita utile rimanente (RUL) di un motore aereo.</span><span class="sxs-lookup"><span data-stu-id="75158-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="75158-119">modello di Hello utilizza una correlazione tra dati provenienti da quattro dei sensori motore hello e usura motore che provoca l'errore tooeventual.</span><span class="sxs-lookup"><span data-stu-id="75158-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="75158-120">Mentre è ancora sicurezza tooensure di un controllo periodico tooperform Fabrikam, ora possibile usare hello modelli toocompute hello RUL per ogni motore dopo ogni volo.</span><span class="sxs-lookup"><span data-stu-id="75158-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="75158-121">modello di Hello utilizza dati di telemetria hello raccolti dai motori di hello durante il volo hello.</span><span class="sxs-lookup"><span data-stu-id="75158-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="75158-122">Fabrikam può prevedere i futuri punti di malfunzionamento e pianificare la manutenzione e la riparazione in anticipo.</span><span class="sxs-lookup"><span data-stu-id="75158-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="75158-123">modello di soluzione Hello utilizza dati usura motore effettivo.</span><span class="sxs-lookup"><span data-stu-id="75158-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="75158-124">Per stimare il punto di hello quando è necessaria una manutenzione, Fabrikam possibile ottimizzare i costi di tooreduce operazioni.</span><span class="sxs-lookup"><span data-stu-id="75158-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="75158-125">I coordinatori della manutenzione usano utilità di pianificazione per:</span><span class="sxs-lookup"><span data-stu-id="75158-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="75158-126">Piano di manutenzione toocoincide con un aereo arresto in una determinata posizione.</span><span class="sxs-lookup"><span data-stu-id="75158-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="75158-127">Verificare un tempo sufficiente sia disponibile per hello aereo toobe fuori servizio senza provocare interruzioni di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="75158-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="75158-128">tooschedule tooensure di tecnici che aereo viene gestiti in modo efficiente senza tempo di attesa.</span><span class="sxs-lookup"><span data-stu-id="75158-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="75158-129">I responsabili del controllo di inventario ricevono i piani di manutenzione, pertanto possono ottimizzare il processo di ordinazione e l'inventario delle parti di ricambio.</span><span class="sxs-lookup"><span data-stu-id="75158-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="75158-130">Queste attività ora terra aereo toominimize di Fabrikam e ridurre i costi operativi assicurando sicurezza hello di passeggeri e personale.</span><span class="sxs-lookup"><span data-stu-id="75158-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="75158-131">toounderstand come [Azure IoT Suite] [ lnk_iot_suite] fornisce ai clienti funzionalità hello necessario potenziale hello toorealize della manutenzione predittiva, esaminare questo [infografica] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="75158-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="75158-132">La modalità di compilazione di soluzioni di manutenzione predittiva hello</span><span class="sxs-lookup"><span data-stu-id="75158-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="75158-133">soluzione Hello utilizza un modello di Azure Machine Learning esistente come un modello tooshow queste funzionalità di utilizzo dal dispositivo telemetria raccolto tramite servizi IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="75158-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="75158-134">Microsoft ha creato un [modello di regressione] [ lnk_regression_model] di un motore aereo in base ai dati disponibili pubblicamente<sup>\[1\]</sup>e dettagliate informazioni aggiuntive su come toouse hello modello.</span><span class="sxs-lookup"><span data-stu-id="75158-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="75158-135">Hello soluzione manutenzione predittiva IoT di Azure Usa il modello di regressione hello creato da questo modello.</span><span class="sxs-lookup"><span data-stu-id="75158-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="75158-136">modello Hello è distribuito nella sottoscrizione di Azure ed esposta attraverso un'API generata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="75158-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="75158-137">soluzione Hello include un subset di dati che rappresenta 4 (pari a 100 totale) di testing hello motori e flussi di dati del sensore hello 4 (pari a 21 totale).</span><span class="sxs-lookup"><span data-stu-id="75158-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="75158-138">Questi dati sono sufficiente tooprovide risultati corretti dal modello con training hello.</span><span class="sxs-lookup"><span data-stu-id="75158-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="75158-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="75158-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="75158-140">Introduzione alla manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="75158-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="75158-141">Questa esercitazione viene illustrato come tooprovision hello soluzione manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="75158-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="75158-142">Illustra anche funzionalità di base della soluzione di manutenzione predittiva hello hello.</span><span class="sxs-lookup"><span data-stu-id="75158-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="75158-143">È possibile accedere a molte di queste funzionalità tramite il dashboard di soluzione hello che distribuisce insieme soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="75158-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="75158-144">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="75158-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="75158-145">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="75158-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75158-146">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="75158-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="75158-147">Accesso troppo[azureiotsuite.com] [ lnk-azureiotsuite] di Azure utilizzando le credenziali dell'account e fare clic su  **+**  toocreate una soluzione.</span><span class="sxs-lookup"><span data-stu-id="75158-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="75158-148">Fare clic su **selezionare** hello **manutenzione predittiva** riquadro.</span><span class="sxs-lookup"><span data-stu-id="75158-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="75158-149">Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="75158-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="75158-150">Seleziona hello **area** e **sottoscrizione** si desidera toouse tooprovision hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="75158-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="75158-151">Fare clic su **crea soluzione** hello toobegin processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="75158-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="75158-152">Questo processo è in genere richiede diversi minuti toorun.</span><span class="sxs-lookup"><span data-stu-id="75158-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="75158-153">Attendere hello toocomplete processo di provisioning</span><span class="sxs-lookup"><span data-stu-id="75158-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="75158-154">Fare clic sul riquadro hello per la soluzione con **Provisioning** stato.</span><span class="sxs-lookup"><span data-stu-id="75158-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="75158-155">Hello preavviso **Provisioning stati** come servizi di Azure vengono distribuiti nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75158-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="75158-156">Una volta al termine del provisioning, hello modifiche allo stato troppo**pronto**.</span><span class="sxs-lookup"><span data-stu-id="75158-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="75158-157">Fare clic su dettagli di hello riquadro toosee hello della soluzione nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="75158-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="75158-158">In questo riquadro è possibile avviare hello soluzione dashboard e accesso hello Machine Learning dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="75158-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="75158-159">Se si verificano problemi di distribuzione di soluzioni hello preconfigurato, esaminare [le autorizzazioni nel sito azureiotsuite.com hello] [ lnk-permissions] hello e [domande frequenti su] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="75158-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="75158-160">Se persistono problemi hello, creare un ticket di servizio in hello [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="75158-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="75158-161">Sono presenti dettagli che ci si aspetta toosee che non sono elencati per la soluzione?</span><span class="sxs-lookup"><span data-stu-id="75158-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="75158-162">è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="75158-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="75158-163">Visualizza soluzione hello</span><span class="sxs-lookup"><span data-stu-id="75158-163">View hello solution</span></span>

<span data-ttu-id="75158-164">In questa sezione descrive la soluzione hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="75158-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="75158-165">Dashboard di manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="75158-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="75158-166">Questa pagina in un'applicazione hello web utilizza PowerBI JavaScript controlli (vedere hello [repository PowerBI-visuals][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="75158-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="75158-167">dati di output di Hello dai processi di flusso Analitica hello nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="75158-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="75158-168">Hello RUL e ciclo di conteggio per il motore di aereo.</span><span class="sxs-lookup"><span data-stu-id="75158-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="75158-169">Osservare il comportamento di hello della soluzione cloud hello</span><span class="sxs-lookup"><span data-stu-id="75158-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="75158-170">In hello portale di Azure, passare il gruppo di risorse toohello con il nome di soluzione hello scelto tooview le risorse di provisioning.</span><span class="sxs-lookup"><span data-stu-id="75158-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="75158-171">Quando si esegue il provisioning di soluzione hello preconfigurato, viene visualizzato un messaggio di posta elettronica con un'area di lavoro di collegamento toohello Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="75158-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="75158-172">È inoltre possibile passare l'area di lavoro Machine Learning toohello da hello [azureiotsuite.com] [ lnk-azureiotsuite] pagina per la soluzione di provisioning.</span><span class="sxs-lookup"><span data-stu-id="75158-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="75158-173">Un riquadro è disponibile in questa pagina quando la soluzione hello è in hello **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="75158-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="75158-174">Nel portale di soluzione hello, è possibile visualizzare che tale esempio hello viene eseguito il provisioning con due aereo di quattro dispositivi simulati toorepresent con due motori per aereo, ognuno con quattro sensori.</span><span class="sxs-lookup"><span data-stu-id="75158-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="75158-175">Quando si esce prima di tutto il portale di soluzione toohello, simulazione hello è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="75158-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="75158-176">Fare clic su **avviare simulazione** simulazione hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="75158-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="75158-177">Hello cronologia sensore, RUL, cicli e RUL cronologia popolare dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="75158-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="75158-178">Quando RUL è inferiore a 160 (una valore soglia arbitraria scelta per scopi dimostrativi), il portale di soluzione hello viene visualizzato un avviso simbolo successivo toohello RUL visualizzare.</span><span class="sxs-lookup"><span data-stu-id="75158-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="75158-179">portale di soluzione Hello evidenzia inoltre motore aereo hello in giallo.</span><span class="sxs-lookup"><span data-stu-id="75158-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="75158-180">Si noti come valori RUL hello presentano una tendenza verso il basso generale globale, ma tendono toobounce su e giù.</span><span class="sxs-lookup"><span data-stu-id="75158-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="75158-181">Questo comportamento è dovuta diverse lunghezze di ciclo hello e accuratezza del modello hello.</span><span class="sxs-lookup"><span data-stu-id="75158-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="75158-182">simulazione completa Hello richiede circa 35 minuti toocomplete 148 cicli.</span><span class="sxs-lookup"><span data-stu-id="75158-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="75158-183">Hello 160 RUL viene raggiunta la soglia per hello prima volta in circa 5 minuti e motori di raggiunto la soglia di hello circa 8 minuti.</span><span class="sxs-lookup"><span data-stu-id="75158-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="75158-184">simulazione di Hello attraversa hello set di dati completo per i cicli di 148 e si posiziona su valori di ciclo e RUL finali.</span><span class="sxs-lookup"><span data-stu-id="75158-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="75158-185">È possibile arrestare la simulazione di hello in qualsiasi punto, ma facendo clic su **avviare simulazione** riproduzioni hello simulazione dall'inizio di hello del set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="75158-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75158-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75158-186">Next steps</span></span>

<span data-ttu-id="75158-187">informazioni su come IoT di Azure consente scenari di manutenzione predittiva, leggere toolearn [acquisire valore hello Internet of Things][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="75158-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="75158-188">Richiedere un [procedura dettagliata] [ lnk-predictive-walkthrough] della soluzione di manutenzione predittiva hello.</span><span class="sxs-lookup"><span data-stu-id="75158-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="75158-189">È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:</span><span class="sxs-lookup"><span data-stu-id="75158-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="75158-190">[Domande frequenti su IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="75158-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="75158-191">[Sicurezza di IoT da hello messa a terra][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="75158-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/