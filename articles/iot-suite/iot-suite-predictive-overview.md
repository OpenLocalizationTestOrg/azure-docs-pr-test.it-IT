---
title: Soluzione preconfigurata di manutenzione predittiva | Documentazione Microsoft
description: Una descrizione della soluzione preconfigurata di manutenzione predittiva di Azure IoT Suite.
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
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="5ce0e-103">Panoramica della soluzione preconfigurata di manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="5ce0e-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="5ce0e-104">La soluzione preconfigurata di *manutenzione predittiva* è una delle [soluzioni preconfigurate][lnk_preconfigured_solutions] di [Microsoft Azure IoT Suite][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="5ce0e-105">Questa soluzione integra una raccolta di dati di telemetria in tempo reale dei dispositivi con un modello predittivo creato utilizzando [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="5ce0e-106">Con Azure IoT Suite, è possibile connettersi agli asset e monitorarli, nonché analizzare i dati di telemetria in tempo reale nei dashboard e nelle visualizzazioni in modo semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="5ce0e-107">Nella soluzione di manutenzione predittiva i dashboard e le visualizzazioni forniscono nuove informazioni con cui è possibile promuovere l'efficienza e aumentare i flussi di profitti.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="5ce0e-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="5ce0e-108">The Scenario</span></span>

<span data-ttu-id="5ce0e-109">Fabrikam è una compagnia aerea locale che si concentra sulle esperienze eccezionali dei clienti a prezzi competitivi.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="5ce0e-110">Una causa di ritardi dei voli sono i problemi di manutenzione e la manutenzione dei motori degli aeromobili è particolarmente complessa.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="5ce0e-111">Fabrikam deve evitare a tutti i costi i guasti dei motori durante il volo, quindi controlla regolarmente i motori e pianifica la manutenzione in base a un programma.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="5ce0e-112">Tuttavia, i motori non sempre si usurano allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="5ce0e-113">Sui motori viene eseguita manutenzione superflua.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="5ce0e-114">Ancora più importante, si verificano problemi che possono forzare a terra un aereo fino a quando non viene eseguita la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="5ce0e-115">Se un aereo si trova in un luogo in cui tecnici esperti o parti di ricambio non sono disponibili, questi problemi possono essere particolarmente costosi.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="5ce0e-116">I motori degli aeromobili Fabrikam sono instrumentati con sensori che controllano le condizioni del motore durante il volo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="5ce0e-117">Fabrikam usa la soluzione di manutenzione predittiva per raccogliere i dati dei sensori raccolti durante il volo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="5ce0e-118">Dopo aver accumulato anni di dati operativi e sui guasti dei motori, i ricercatori di dati di Fabrikam hanno modellato un modo per prevedere la vita utile rimanente (RUL) di un motore di aeromobile.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="5ce0e-119">Il modello usa una correlazione tra i dati provenienti da quattro dei sensori del motore e l'usura del motore che conduce a un eventuale guasto.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="5ce0e-120">Mentre Fabrikam continua a eseguire controlli periodici per garantire la sicurezza, ora può usare i modelli per calcolare il valore RUL per ogni motore dopo ogni volo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="5ce0e-121">Il modello usa i dati di telemetria raccolti dai motori durante il volo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="5ce0e-122">Fabrikam può prevedere i futuri punti di malfunzionamento e pianificare la manutenzione e la riparazione in anticipo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce0e-123">Il modello di soluzione usa dati di usura del motore effettivi.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="5ce0e-124">Prevedendo il momento in cui sarà necessaria la manutenzione, Fabrikam può ottimizzare le proprie operazioni per ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="5ce0e-125">I coordinatori della manutenzione usano utilità di pianificazione per:</span><span class="sxs-lookup"><span data-stu-id="5ce0e-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="5ce0e-126">Pianificare l'esecuzione della manutenzione quando un velivolo si ferma in una determinata località.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="5ce0e-127">Assicurarsi che il velivolo rimanga fuori servizio per un periodo di tempo senza causare interruzioni della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="5ce0e-128">Per pianificare i tecnici di conseguenza e garantire così che i velivoli siano gestiti in modo efficiente senza tempi di attesa.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="5ce0e-129">I responsabili del controllo di inventario ricevono i piani di manutenzione, pertanto possono ottimizzare il processo di ordinazione e l'inventario delle parti di ricambio.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="5ce0e-130">Queste attività consentono a Fabrikam di ridurre al minimo i tempo di fermo a terra dei velivoli e di ridurre i costi operativi, garantendo la sicurezza dei passeggeri e dell'equipaggio.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="5ce0e-131">Per comprendere come [Azure IoT Suite][lnk_iot_suite] fornisce ai clienti le funzionalità necessarie a realizzare il potenziale della manutenzione predittiva, vedere questa [infografica][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="5ce0e-132">Creazione della soluzione di manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="5ce0e-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="5ce0e-133">Per visualizzare queste funzionalità partendo dai dati di telemetria del dispositivo raccolti attraverso i servizi di IoT Suite, la soluzione usa un modello esistente di Azure Machine Learning disponibile.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="5ce0e-134">Microsoft ha creato un [modello di regressione][lnk_regression_model] basato su dati pubblici<sup>\[[1]\]</sup> e le istruzioni dettagliate su come usare il modello.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="5ce0e-135">La soluzione di manutenzione predittiva di Azure IoT usa il modello di regressione creato da questo modello.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="5ce0e-136">Il modello viene distribuito nella sottoscrizione di Azure ed esposto tramite un'API generata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="5ce0e-137">La soluzione include un subset di dati di test che rappresenta 4 (su un totale di 100) motori e 4 (su un totale di 21) flussi di dati dei sensori.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="5ce0e-138">Questi dati sono sufficienti per fornire un risultato esatto dal modello con training.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="5ce0e-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="5ce0e-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="5ce0e-140">Introduzione alla manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="5ce0e-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="5ce0e-141">Questa esercitazione illustra come effettuare il provisioning della soluzione di manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="5ce0e-142">Ne descrive anche le funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="5ce0e-143">È possibile accedere a molte di queste funzionalità tramite il dashboard distribuito con la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="5ce0e-144">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce0e-145">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5ce0e-146">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="5ce0e-147">Accedere a [azureiotsuite.com][lnk-azureiotsuite] con le credenziali dell'account Azure e fare clic su **+** per creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="5ce0e-148">**Selezionare** il riquadro **Manutenzione predittiva**.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="5ce0e-149">Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="5ce0e-150">Selezionare l'**area** e la **sottoscrizione** che si desidera usare per il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="5ce0e-151">Fare clic su **Crea soluzione** per iniziare il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="5ce0e-152">In genere il processo richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="5ce0e-153">Attendere il completamento del processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="5ce0e-154">Fare clic sul riquadro della soluzione con stato **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="5ce0e-155">Notare gli stati **Provisioning** man mano che i servizi di Azure vengono distribuiti nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="5ce0e-156">Al termine del provisioning, lo stato cambierà in **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="5ce0e-157">Fare clic sul riquadro per visualizzare i dettagli della soluzione nel riquadro di destra.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="5ce0e-158">Da questo riquadro è possibile avviare il dashboard della soluzione e accedere all'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce0e-159">In caso di problemi di distribuzione della soluzione preconfigurata, vedere [Autorizzazioni per il sito azureiotsuite.com][lnk-permissions] e le [domande frequenti][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="5ce0e-160">Se i problemi persistono, creare un ticket di servizio nel [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="5ce0e-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="5ce0e-161">Se ci sono dettagli importanti non elencati per la soluzione,</span><span class="sxs-lookup"><span data-stu-id="5ce0e-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="5ce0e-162">è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="5ce0e-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="5ce0e-163">Visualizzare la soluzione</span><span class="sxs-lookup"><span data-stu-id="5ce0e-163">View the solution</span></span>

<span data-ttu-id="5ce0e-164">Questa sezione descrive l'interfaccia utente della soluzione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="5ce0e-165">Dashboard di manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="5ce0e-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="5ce0e-166">Questa pagina dell'applicazione Web usa i controlli JavaScript di Power BI (vedere il [repository di oggetti visivi di Power BI][lnk-powerbi]) per visualizzare:</span><span class="sxs-lookup"><span data-stu-id="5ce0e-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="5ce0e-167">I dati di output dei processi di Analisi di flusso nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="5ce0e-168">La vita utile rimanente Il conteggio dei cicli per motore di aereo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="5ce0e-169">Osservare il comportamento della soluzione cloud</span><span class="sxs-lookup"><span data-stu-id="5ce0e-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="5ce0e-170">Nel portale di Azure passare al gruppo di risorse con il nome della soluzione scelto per visualizzare le risorse di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="5ce0e-171">Quando si esegue il provisioning della soluzione preconfigurata, viene visualizzato un messaggio di posta elettronica con un collegamento all'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="5ce0e-172">È anche possibile passare all'area di lavoro di Machine Learning dalla pagina [azureiotsuite.com][lnk-azureiotsuite] per la soluzione di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="5ce0e-173">Quando lo stato della soluzione è **Ready** (Pronto), in questa pagina è disponibile un riquadro.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="5ce0e-174">Nel portale della soluzione si noterà che l'esempio include quattro dispositivi simulati per rappresentare due aerei con due motori per aereo, ciascuno con quattro sensori.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="5ce0e-175">Quando si accede per la prima volta al portale della soluzione, la simulazione viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="5ce0e-176">Fare clic su **Avvia simulazione** per iniziare la simulazione.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="5ce0e-177">Il dashboard viene popolato con cronologia del sensore, vita utile rimanente, cicli e cronologia della vita utile rimanente.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="5ce0e-178">Quando la vita utile rimanente è inferiore a 160, una soglia arbitraria scelta a scopo dimostrativo, il portale della soluzione mostra un simbolo di avviso accanto alla visualizzazione della vita utile rimanente.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="5ce0e-179">Il portale della soluzione evidenzia anche in giallo il motore dell'aereo.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="5ce0e-180">Si noti come i valori della vita utile rimanente abbiano complessivamente una tendenza generale al ribasso, ma tendano a oscillare in alto o in basso.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="5ce0e-181">Questo comportamento dovuto alle diverse lunghezze dei cicli e all'accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="5ce0e-182">La simulazione completa richiede circa 35 minuti per completare 148 cicli.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="5ce0e-183">La soglia di 160 per la vita utile rimanente viene raggiunta per la prima volta dopo circa 5 minuti ed entrambi i motori la raggiungono a circa 8 minuti.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="5ce0e-184">La simulazione viene eseguita sul set di dati completo per 148 cicli e si stabilizza sui valori finali dei cicli e della vita utile rimanente.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="5ce0e-185">È possibile arrestare la simulazione in qualsiasi punto, ma facendo clic su **Start Simulation** viene riprodotta la simulazione dall'inizio del set di dati.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce0e-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ce0e-186">Next steps</span></span>

<span data-ttu-id="5ce0e-187">Per ulteriori informazioni su come Azure IoT consente scenari di manutenzione predittiva, leggere [Capture value from the Internet of Things][lnk_capture_value] (Acquisire valore da Internet delle cose).</span><span class="sxs-lookup"><span data-stu-id="5ce0e-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="5ce0e-188">Esaminare una [procedura dettagliata][lnk-predictive-walkthrough] della soluzione di manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="5ce0e-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="5ce0e-189">È anche possibile esplorare alcune altre funzionalità delle soluzioni preconfigurate di IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="5ce0e-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="5ce0e-190">[Domande frequenti su IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="5ce0e-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="5ce0e-191">[Sicurezza IoT sin dall'inizio][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="5ce0e-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

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