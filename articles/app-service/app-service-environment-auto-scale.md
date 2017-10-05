---
title: Ridimensionamento automatico e ambiente del servizio app (versione 1)
description: Ridimensionamento automatico e ambiente del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="b9f4b-103">Ridimensionamento automatico e ambiente del servizio app (versione 1)</span><span class="sxs-lookup"><span data-stu-id="b9f4b-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="b9f4b-104">Questo articolo fa riferimento all'ambiente del servizio app v1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="b9f4b-105">Esiste una nuova versione dell'ambiente del servizio app che, oltre ad essere più facile da usare, può essere eseguita in un'infrastruttura più potente.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="b9f4b-106">Per altre informazioni su questa nuova versione, vedere [Introduzione ad Ambiente del servizio app](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="b9f4b-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="b9f4b-107">Gli ambienti del servizio app di Azure supportano il *ridimensionamento automatico*.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="b9f4b-108">È possibile ridimensionare automaticamente singoli pool di lavoro in base alle metriche o alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opzioni di ridimensionamento automatico per un pool di lavoro.][intro]

<span data-ttu-id="b9f4b-110">Il ridimensionamento automatico consente di ottimizzare l'utilizzo delle risorse aumentando o riducendo automaticamente le risorse di un ambiente del servizio app, in base al budget o al profilo di carico.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="b9f4b-111">Configurare il ridimensionamento automatico del pool di lavoro</span><span class="sxs-lookup"><span data-stu-id="b9f4b-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="b9f4b-112">È possibile accedere alla funzionalità di ridimensionamento automatico dalla scheda **Impostazioni** del pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Scheda Impostazioni del pool di lavoro.][settings-scale]

<span data-ttu-id="b9f4b-114">L'interfaccia utente risulterà familiare, perché si tratta della stessa esperienza visualizzata quando si ridimensiona un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Impostazioni di ridimensionamento manuale.][scale-manual]

<span data-ttu-id="b9f4b-116">È anche possibile configurare un profilo di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-116">You can also configure an autoscale profile.</span></span>

![Impostazioni di ridimensionamento automatico.][scale-profile]

<span data-ttu-id="b9f4b-118">I profili di ridimensionamento automatico consentono di impostare i limiti per il piano.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="b9f4b-119">Ciò consente di ottenere prestazioni coerenti impostando un valore del piano con un limite minimo (1) e un tetto di spesa prevedibile impostando un limite massimo (2).</span><span class="sxs-lookup"><span data-stu-id="b9f4b-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Impostazioni di ridimensionamento nel profilo.][scale-profile2]

<span data-ttu-id="b9f4b-121">Dopo aver definito il profilo, è possibile aggiungere regole di ridimensionamento automatico per aumentare o ridurre il numero di istanze nel pool di lavoro entro i limiti definiti nel profilo.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="b9f4b-122">Le regole di ridimensionamento automatico sono basate su metriche.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-122">Autoscale rules are based on metrics.</span></span>

![Regola di ridimensionamento.][scale-rule]

 <span data-ttu-id="b9f4b-124">Per definire le regole di ridimensionamento automatico, è possibile usare qualsiasi metrica del pool di lavoro o del front-end.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="b9f4b-125">Si tratta delle stesse metriche che è possibile monitorare nei grafici del pannello delle risorse o per cui si possono impostare avvisi.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="b9f4b-126">Esempio di ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="b9f4b-126">Autoscale example</span></span>
<span data-ttu-id="b9f4b-127">Per illustrare il ridimensionamento automatico di un ambiente del servizio app, si userà uno scenario con procedure dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="b9f4b-128">Questo articolo descrive tutte le considerazioni necessarie per configurare il ridimensionamento automatico,</span><span class="sxs-lookup"><span data-stu-id="b9f4b-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="b9f4b-129">nonché tutte le interazioni che entrano in gioco quando si configura il ridimensionamento automatico di ambienti del servizio app ospitati in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="b9f4b-130">Introduzione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b9f4b-130">Scenario introduction</span></span>
<span data-ttu-id="b9f4b-131">Diego è amministratore di sistema presso una società e ha eseguito la migrazione di una parte dei carichi di lavoro che gestisce a un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="b9f4b-132">L'ambiente del servizio app è configurato per la scalabilità manuale come segue:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="b9f4b-133">**Front-end:** 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-133">**Front ends:** 3</span></span>
* <span data-ttu-id="b9f4b-134">**Pool di lavoro 1**: 10</span><span class="sxs-lookup"><span data-stu-id="b9f4b-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="b9f4b-135">**Pool di lavoro 2**: 5</span><span class="sxs-lookup"><span data-stu-id="b9f4b-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="b9f4b-136">**Pool di lavoro 3**: 5</span><span class="sxs-lookup"><span data-stu-id="b9f4b-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="b9f4b-137">Il pool di lavoro 1 viene usato per i carichi di lavoro di produzione, mentre il pool di lavoro 2 e il pool di lavoro 3 sono usati per il controllo di qualità e i carichi di lavoro di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="b9f4b-138">I piani del servizio app per il controllo di qualità e lo sviluppo vengono configurati per il ridimensionamento manuale.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="b9f4b-139">Il piano del servizio app di produzione è impostato per il ridimensionamento automatico, in modo da adeguarsi alle variazioni del carico e del traffico.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="b9f4b-140">Diego ha una notevole familiarità con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="b9f4b-141">Sa che le ore di picco di carico sono comprese tra le 9:00 e le 18:00, perché si tratta di un'applicazione di line-of-business (LOB) che i dipendenti usano mentre sono in ufficio.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="b9f4b-142">L'utilizzo si riduce al termine della giornata lavorativa degli utenti.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="b9f4b-143">Al di fuori dagli orari di picco il carico è ancora presente in parte, perché gli utenti possono accedere all'app in modalità remota usando i propri dispositivi mobili o i PC di casa.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="b9f4b-144">Il piano di servizio app è già configurato per il ridimensionamento automatico in base all'utilizzo della CPU con le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Impostazioni specifiche per l'app LOB.][asp-scale]

| <span data-ttu-id="b9f4b-146">**Profilo di ridimensionamento automatico - Giorni feriali - Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="b9f4b-147">**Profilo di ridimensionamento automatico - Fine settimana - Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="b9f4b-148">**Nome:** profilo Giorno feriale</span><span class="sxs-lookup"><span data-stu-id="b9f4b-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="b9f4b-149">**Nome:** profilo Fine settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="b9f4b-150">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9f4b-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="b9f4b-151">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9f4b-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="b9f4b-152">**Profilo:** giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="b9f4b-153">**Profilo:** fine settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="b9f4b-154">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="b9f4b-154">**Type:** Recurrence</span></span> |<span data-ttu-id="b9f4b-155">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="b9f4b-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="b9f4b-156">**Intervallo di destinazione:** da 5 a 20 istanze</span><span class="sxs-lookup"><span data-stu-id="b9f4b-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="b9f4b-157">**Intervallo di destinazione:** da 3 a 10 istanze</span><span class="sxs-lookup"><span data-stu-id="b9f4b-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="b9f4b-158">**Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì</span><span class="sxs-lookup"><span data-stu-id="b9f4b-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="b9f4b-159">**Giorni:** Sabato, Domenica</span><span class="sxs-lookup"><span data-stu-id="b9f4b-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="b9f4b-160">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="b9f4b-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="b9f4b-161">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="b9f4b-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="b9f4b-162">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="b9f4b-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="b9f4b-163">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="b9f4b-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="b9f4b-164">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="b9f4b-165">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="b9f4b-166">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="b9f4b-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="b9f4b-167">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="b9f4b-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="b9f4b-168">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-168">**Metric:** CPU %</span></span> |<span data-ttu-id="b9f4b-169">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="b9f4b-170">**Operazione:** maggiore del 60%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="b9f4b-171">**Operazione:** maggiore del 80%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="b9f4b-172">**Durata:** 5 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="b9f4b-173">**Durata:** 10 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="b9f4b-174">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="b9f4b-175">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-176">**Azione:** aumenta numero di 2</span><span class="sxs-lookup"><span data-stu-id="b9f4b-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="b9f4b-177">**Azione:** aumenta numero di 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="b9f4b-178">**Disattiva regole dopo (minuti):** 15</span><span class="sxs-lookup"><span data-stu-id="b9f4b-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="b9f4b-179">**Disattiva regole dopo (minuti):** 20</span><span class="sxs-lookup"><span data-stu-id="b9f4b-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="b9f4b-180">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="b9f4b-181">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="b9f4b-182">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="b9f4b-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="b9f4b-183">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="b9f4b-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="b9f4b-184">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-184">**Metric:** CPU %</span></span> |<span data-ttu-id="b9f4b-185">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="b9f4b-186">**Operazione:** inferiore al 30%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="b9f4b-187">**Operazione:** inferiore al 20%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="b9f4b-188">**Durata:** 10 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="b9f4b-189">**Durata:** 15 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="b9f4b-190">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="b9f4b-191">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-192">**Azione:** riduci numero di 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="b9f4b-193">**Azione:** riduci numero di 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="b9f4b-194">**Disattiva regole dopo (minuti):** 20</span><span class="sxs-lookup"><span data-stu-id="b9f4b-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="b9f4b-195">**Disattiva regole dopo (minuti):** 10</span><span class="sxs-lookup"><span data-stu-id="b9f4b-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="b9f4b-196">Tasso di inflazione del piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="b9f4b-196">App Service plan inflation rate</span></span>
<span data-ttu-id="b9f4b-197">I piani di servizio app configurati per il ridimensionamento automatico vengono ridimensionati automaticamente in base al tasso massimo su base oraria.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="b9f4b-198">Questa frequenza può essere calcolata in base ai valori specificati nella regola di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="b9f4b-199">È importante comprendere e calcolare il *tasso di inflazione del piano di servizio app* per il ridimensionamento automatico dell'ambiente del servizio app, perché l'operazione di ridimensionamento del pool di lavoro non è istantanea.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="b9f4b-200">Il tasso di inflazione del piano di servizio app viene calcolato come segue:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Calcolo del tasso di inflazione del piano di servizio app.][ASP-Inflation]

<span data-ttu-id="b9f4b-202">In base alla regola Ridimensionamento automatico - Aumento per il profilo Giorno feriale del piano di servizio app di produzione la formula sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di aumento.][Equation1]

<span data-ttu-id="b9f4b-204">Nel caso della regola Ridimensionamento automatico - Aumento per il profilo Fine settimana del piano di servizio app di produzione la formula sarà la seguente:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di aumento.][Equation2]

<span data-ttu-id="b9f4b-206">Questo valore può anche essere calcolato per le operazioni di riduzione.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="b9f4b-207">In base alla regola Ridimensionamento automatico - Riduzione per il profilo Giorno feriale del piano di servizio app di produzione la formula sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di riduzione.][Equation3]

<span data-ttu-id="b9f4b-209">Nel caso della regola Ridimensionamento automatico - Riduzione per il profilo Fine settimana del piano di servizio app di produzione la formula sarà la seguente:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di riduzione.][Equation4]

<span data-ttu-id="b9f4b-211">Il piano di servizio app di produzione può aumentare al tasso massimo di 8 istanze all'ora durante la settimana e di 4 istanze all'ora durante il fine settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="b9f4b-212">e può rilasciare le istanze al tasso massimo di 4 istanze all'ora durante la settimana e di 6 istanze all'ora durante il fine settimana.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="b9f4b-213">Se in un pool di lavoro sono ospitati più piani di servizio app, è necessario calcolare il *tasso di inflazione totale* come somma dei tassi di inflazione per tutti i piani di servizio app ospitati in quel pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Calcolo del tasso di inflazione totale per più piani di servizio app ospitati in un pool di lavoro.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="b9f4b-215">Usare il tasso di inflazione del piano di servizio app per definire le regole di ridimensionamento automatico del pool di lavoro</span><span class="sxs-lookup"><span data-stu-id="b9f4b-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="b9f4b-216">Ai pool di lavoro che ospitano piani di servizio app configurati per il ridimensionamento automatico è necessario allocare un buffer di capacità.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="b9f4b-217">Il buffer consente alle operazioni di ridimensionamento automatico di aumentare e ridurre il piano di servizio app in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="b9f4b-218">Il buffer minimo sarà costituito dal tasso di inflazione totale calcolato per il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="b9f4b-219">Poiché l'applicazione delle operazioni di ridimensionamento dell'ambiente del servizio app richiede tempo, qualsiasi modifica deve tenere conto delle ulteriori variazioni della domanda che possono verificarsi mentre è in corso un'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="b9f4b-220">Per questo motivo è consigliabile usare il tasso di inflazione totale calcolato per il piano di servizio app come numero minimo di istanze aggiunte per ogni operazione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="b9f4b-221">Con queste informazioni Diego può definire le regole e il profilo di ridimensionamento automatico seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Regole del profilo di ridimensionamento automatico per l'esempio LOB.][Worker-Pool-Scale]

| <span data-ttu-id="b9f4b-223">**Profilo di ridimensionamento automatico - Giorni feriali**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="b9f4b-224">**Profilo di ridimensionamento automatico - Fine settimana**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="b9f4b-225">**Nome:** profilo Giorno feriale</span><span class="sxs-lookup"><span data-stu-id="b9f4b-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="b9f4b-226">**Nome:** profilo Fine settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="b9f4b-227">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9f4b-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="b9f4b-228">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9f4b-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="b9f4b-229">**Profilo:** giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="b9f4b-230">**Profilo:** fine settimana</span><span class="sxs-lookup"><span data-stu-id="b9f4b-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="b9f4b-231">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="b9f4b-231">**Type:** Recurrence</span></span> |<span data-ttu-id="b9f4b-232">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="b9f4b-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="b9f4b-233">**Intervallo di destinazione:** da 13 a 25 istanze</span><span class="sxs-lookup"><span data-stu-id="b9f4b-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="b9f4b-234">**Intervallo di destinazione:** da 6 a 15 istanze</span><span class="sxs-lookup"><span data-stu-id="b9f4b-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="b9f4b-235">**Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì</span><span class="sxs-lookup"><span data-stu-id="b9f4b-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="b9f4b-236">**Giorni:** Sabato, Domenica</span><span class="sxs-lookup"><span data-stu-id="b9f4b-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="b9f4b-237">**Ora di inizio:** 7:00</span><span class="sxs-lookup"><span data-stu-id="b9f4b-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="b9f4b-238">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="b9f4b-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="b9f4b-239">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="b9f4b-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="b9f4b-240">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="b9f4b-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="b9f4b-241">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="b9f4b-242">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="b9f4b-243">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="b9f4b-244">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="b9f4b-245">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="b9f4b-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="b9f4b-246">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="b9f4b-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="b9f4b-247">**Operazione:** minore di 8</span><span class="sxs-lookup"><span data-stu-id="b9f4b-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="b9f4b-248">**Operazione:** minore di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="b9f4b-249">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="b9f4b-250">**Durata:** 30 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="b9f4b-251">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="b9f4b-252">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-253">**Azione:** aumenta numero di 8</span><span class="sxs-lookup"><span data-stu-id="b9f4b-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="b9f4b-254">**Azione:** aumenta numero di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="b9f4b-255">**Disattiva regole dopo (minuti):** 180</span><span class="sxs-lookup"><span data-stu-id="b9f4b-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="b9f4b-256">**Disattiva regole dopo (minuti):** 180</span><span class="sxs-lookup"><span data-stu-id="b9f4b-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="b9f4b-257">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="b9f4b-258">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="b9f4b-259">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="b9f4b-260">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="b9f4b-261">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="b9f4b-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="b9f4b-262">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="b9f4b-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="b9f4b-263">**Operazione:** maggiore di 8</span><span class="sxs-lookup"><span data-stu-id="b9f4b-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="b9f4b-264">**Operazione:** maggiore di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="b9f4b-265">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="b9f4b-266">**Durata:** 15 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="b9f4b-267">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="b9f4b-268">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-269">**Azione:** riduci numero di 2</span><span class="sxs-lookup"><span data-stu-id="b9f4b-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="b9f4b-270">**Azione:** riduci numero di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="b9f4b-271">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="b9f4b-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="b9f4b-272">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="b9f4b-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="b9f4b-273">L'intervallo di destinazione definito nel profilo è calcolato in base al numero minimo di istanze definito nel profilo per il piano di servizio app più il buffer.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="b9f4b-274">L'intervallo massimo corrisponde alla somma di tutti gli intervalli massimi per tutti i piani di servizio app ospitati nel pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="b9f4b-275">L'aumento del numero per le regole di aumento deve essere impostato su un valore pari ad almeno 1 volta il tasso di inflazione per il piano di servizio app per l'operazione di aumento.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="b9f4b-276">La riduzione del numero può essere regolata su un valore compreso tra la metà o una volta il tasso di inflazione del piano di servizio app per l'operazione di riduzione.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="b9f4b-277">Ridimensionamento automatico per il pool front-end</span><span class="sxs-lookup"><span data-stu-id="b9f4b-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="b9f4b-278">Le regole per il ridimensionamento automatico front-end sono più semplici rispetto ai pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="b9f4b-279">È prima di tutto necessario</span><span class="sxs-lookup"><span data-stu-id="b9f4b-279">Primarily, you should</span></span>  
<span data-ttu-id="b9f4b-280">assicurarsi che la durata della misurazione e i timer di raffreddamento tengano presente che le operazioni di ridimensionamento in un piano di servizio app non sono istantanee.</span><span class="sxs-lookup"><span data-stu-id="b9f4b-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="b9f4b-281">Per questo scenario, Diego sa che la percentuale di errore aumenta quando i pool front-end raggiungono un utilizzo di CPU dell'80% e imposta la regola di scalabilità automatica in modo da aumentare le istanze come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="b9f4b-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Impostazioni di ridimensionamento automatico per il pool front-end.][Front-End-Scale]

| <span data-ttu-id="b9f4b-283">**Profilo di ridimensionamento automatico - Front-end**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="b9f4b-284">**Nome:** Ridimensionamento automatico - Front-end</span><span class="sxs-lookup"><span data-stu-id="b9f4b-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="b9f4b-285">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9f4b-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="b9f4b-286">**Profilo:** ogni giorno</span><span class="sxs-lookup"><span data-stu-id="b9f4b-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="b9f4b-287">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="b9f4b-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="b9f4b-288">**Intervallo di destinazione:** da 3 a 10 istanze</span><span class="sxs-lookup"><span data-stu-id="b9f4b-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="b9f4b-289">**Giorni:** ogni giorno</span><span class="sxs-lookup"><span data-stu-id="b9f4b-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="b9f4b-290">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="b9f4b-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="b9f4b-291">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="b9f4b-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="b9f4b-292">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="b9f4b-293">**Risorsa:** pool front-end</span><span class="sxs-lookup"><span data-stu-id="b9f4b-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="b9f4b-294">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="b9f4b-295">**Operazione:** maggiore del 60%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="b9f4b-296">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="b9f4b-297">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-298">**Azione:** aumenta numero di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="b9f4b-299">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="b9f4b-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="b9f4b-300">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="b9f4b-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="b9f4b-301">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="b9f4b-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="b9f4b-302">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="b9f4b-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="b9f4b-303">**Operazione:** inferiore al 30%</span><span class="sxs-lookup"><span data-stu-id="b9f4b-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="b9f4b-304">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="b9f4b-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="b9f4b-305">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="b9f4b-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="b9f4b-306">**Azione:** riduci numero di 3</span><span class="sxs-lookup"><span data-stu-id="b9f4b-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="b9f4b-307">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="b9f4b-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
