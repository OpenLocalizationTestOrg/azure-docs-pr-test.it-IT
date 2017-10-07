---
title: aaaAutoscaling e v1 ambiente del servizio App
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
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="644dc-103">Ridimensionamento automatico e ambiente del servizio app (versione 1)</span><span class="sxs-lookup"><span data-stu-id="644dc-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="644dc-104">Questo articolo è sull'ambiente del servizio App v1 hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="644dc-105">È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente.</span><span class="sxs-lookup"><span data-stu-id="644dc-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="644dc-106">informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="644dc-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="644dc-107">Gli ambienti del servizio app di Azure supportano il *ridimensionamento automatico*.</span><span class="sxs-lookup"><span data-stu-id="644dc-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="644dc-108">È possibile ridimensionare automaticamente singoli pool di lavoro in base alle metriche o alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="644dc-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opzioni di ridimensionamento automatico per un pool di lavoro.][intro]

<span data-ttu-id="644dc-110">La scalabilità automatica consente di ottimizzare l'utilizzo delle risorse mediante automaticamente l'espansione e riduzione di un toofit di ambiente del servizio App profilo budget e di carico.</span><span class="sxs-lookup"><span data-stu-id="644dc-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="644dc-111">Configurare il ridimensionamento automatico del pool di lavoro</span><span class="sxs-lookup"><span data-stu-id="644dc-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="644dc-112">È possibile accedere a funzionalità di scalabilità automatica hello da hello **impostazioni** tab di pool di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Scheda Impostazioni del pool di lavoro hello.][settings-scale]

<span data-ttu-id="644dc-114">Da qui, hello interfaccia deve essere piuttosto familiare perché è hello pianificare la stessa esperienza che viene visualizzato quando si scala di un servizio App.</span><span class="sxs-lookup"><span data-stu-id="644dc-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![Impostazioni di ridimensionamento manuale.][scale-manual]

<span data-ttu-id="644dc-116">È anche possibile configurare un profilo di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="644dc-116">You can also configure an autoscale profile.</span></span>

![Impostazioni di ridimensionamento automatico.][scale-profile]

<span data-ttu-id="644dc-118">Profili di scalabilità automatica sono limiti di tooset utili sulla scala.</span><span class="sxs-lookup"><span data-stu-id="644dc-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="644dc-119">Ciò consente di ottenere prestazioni coerenti impostando un valore del piano con un limite minimo (1) e un tetto di spesa prevedibile impostando un limite massimo (2).</span><span class="sxs-lookup"><span data-stu-id="644dc-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Impostazioni di ridimensionamento nel profilo.][scale-profile2]

<span data-ttu-id="644dc-121">Dopo aver definito un profilo, è possibile aggiungere tooscale regole di scalabilità automatica verso l'alto o verso il basso il numero di hello di istanze nel pool di lavoro hello all'interno dei limiti di hello definiti dal profilo hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="644dc-122">Le regole di ridimensionamento automatico sono basate su metriche.</span><span class="sxs-lookup"><span data-stu-id="644dc-122">Autoscale rules are based on metrics.</span></span>

![Regola di ridimensionamento.][scale-rule]

 <span data-ttu-id="644dc-124">Qualsiasi metrica front-end o un pool di lavoro può essere toodefine utilizzate regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="644dc-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="644dc-125">Queste metriche sono hello stesse metriche è possibile monitorare in diagrammi di pannello risorse hello o impostare gli avvisi per.</span><span class="sxs-lookup"><span data-stu-id="644dc-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="644dc-126">Esempio di ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="644dc-126">Autoscale example</span></span>
<span data-ttu-id="644dc-127">Per illustrare il ridimensionamento automatico di un ambiente del servizio app, si userà uno scenario con procedure dettagliate.</span><span class="sxs-lookup"><span data-stu-id="644dc-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="644dc-128">Questo articolo illustra tutte le considerazioni necessarie hello quando si configura scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="644dc-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="644dc-129">articolo Hello illustra hello interazioni che entrano riprodurre quando si analizzano la scalabilità automatica gli ambienti del servizio App che sono ospitati nell'ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="644dc-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="644dc-130">Introduzione dello scenario</span><span class="sxs-lookup"><span data-stu-id="644dc-130">Scenario introduction</span></span>
<span data-ttu-id="644dc-131">Frank è un sysadmin per un'azienda che ha eseguito la migrazione di una parte dei carichi di lavoro hello che egli gestisce tooan ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="644dc-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="644dc-132">Hello servizio App di ambiente è configurato scala toomanual come segue:</span><span class="sxs-lookup"><span data-stu-id="644dc-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="644dc-133">**Front-end:** 3</span><span class="sxs-lookup"><span data-stu-id="644dc-133">**Front ends:** 3</span></span>
* <span data-ttu-id="644dc-134">**Pool di lavoro 1**: 10</span><span class="sxs-lookup"><span data-stu-id="644dc-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="644dc-135">**Pool di lavoro 2**: 5</span><span class="sxs-lookup"><span data-stu-id="644dc-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="644dc-136">**Pool di lavoro 3**: 5</span><span class="sxs-lookup"><span data-stu-id="644dc-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="644dc-137">Il pool di lavoro 1 viene usato per i carichi di lavoro di produzione, mentre il pool di lavoro 2 e il pool di lavoro 3 sono usati per il controllo di qualità e i carichi di lavoro di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="644dc-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="644dc-138">Hello App piani di servizio per il controllo della qualità e sviluppo sono configurati toomanual scala.</span><span class="sxs-lookup"><span data-stu-id="644dc-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="644dc-139">produzione Hello piano di servizio App è impostato toodeal tooautoscale con le variazioni del carico e il traffico.</span><span class="sxs-lookup"><span data-stu-id="644dc-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="644dc-140">Frank è dimestichezza con l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="644dc-141">Questi conosce ore di punta hello per il carico siano tra 9:00:00 e le 18.00 poiché si tratta di un'applicazione di line-of-business (LOB) che i dipendenti usano mentre si trovano in office hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="644dc-142">L'utilizzo si riduce al termine della giornata lavorativa degli utenti.</span><span class="sxs-lookup"><span data-stu-id="644dc-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="644dc-143">Di fuori ore di punta, è ancora presente un carico in quanto gli utenti possono accedere in remoto hello app usando i dispositivi mobili o home PC.</span><span class="sxs-lookup"><span data-stu-id="644dc-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="644dc-144">produzione di Hello piano di servizio App è già configurato tooautoscale in base all'utilizzo della CPU con hello seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="644dc-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![Impostazioni specifiche per l'app LOB.][asp-scale]

| <span data-ttu-id="644dc-146">**Profilo di ridimensionamento automatico - Giorni feriali - Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="644dc-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="644dc-147">**Profilo di ridimensionamento automatico - Fine settimana - Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="644dc-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="644dc-148">**Nome:** profilo Giorno feriale</span><span class="sxs-lookup"><span data-stu-id="644dc-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="644dc-149">**Nome:** profilo Fine settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="644dc-150">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="644dc-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="644dc-151">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="644dc-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="644dc-152">**Profilo:** giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="644dc-153">**Profilo:** fine settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="644dc-154">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="644dc-154">**Type:** Recurrence</span></span> |<span data-ttu-id="644dc-155">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="644dc-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="644dc-156">**Intervallo di destinazione:** 5 istanze too20</span><span class="sxs-lookup"><span data-stu-id="644dc-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="644dc-157">**Intervallo di destinazione:** 3 istanze too10</span><span class="sxs-lookup"><span data-stu-id="644dc-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="644dc-158">**Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì</span><span class="sxs-lookup"><span data-stu-id="644dc-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="644dc-159">**Giorni:** Sabato, Domenica</span><span class="sxs-lookup"><span data-stu-id="644dc-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="644dc-160">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="644dc-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="644dc-161">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="644dc-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="644dc-162">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="644dc-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="644dc-163">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="644dc-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="644dc-164">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="644dc-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="644dc-165">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="644dc-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="644dc-166">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="644dc-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="644dc-167">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="644dc-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="644dc-168">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-168">**Metric:** CPU %</span></span> |<span data-ttu-id="644dc-169">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="644dc-170">**Operazione:** maggiore del 60%</span><span class="sxs-lookup"><span data-stu-id="644dc-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="644dc-171">**Operazione:** maggiore del 80%</span><span class="sxs-lookup"><span data-stu-id="644dc-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="644dc-172">**Durata:** 5 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="644dc-173">**Durata:** 10 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="644dc-174">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="644dc-175">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-176">**Azione:** aumenta numero di 2</span><span class="sxs-lookup"><span data-stu-id="644dc-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="644dc-177">**Azione:** aumenta numero di 1</span><span class="sxs-lookup"><span data-stu-id="644dc-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="644dc-178">**Disattiva regole dopo (minuti):** 15</span><span class="sxs-lookup"><span data-stu-id="644dc-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="644dc-179">**Disattiva regole dopo (minuti):** 20</span><span class="sxs-lookup"><span data-stu-id="644dc-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="644dc-180">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="644dc-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="644dc-181">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="644dc-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="644dc-182">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="644dc-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="644dc-183">**Risorsa:** produzione (Ambiente del servizio app)</span><span class="sxs-lookup"><span data-stu-id="644dc-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="644dc-184">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-184">**Metric:** CPU %</span></span> |<span data-ttu-id="644dc-185">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="644dc-186">**Operazione:** inferiore al 30%</span><span class="sxs-lookup"><span data-stu-id="644dc-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="644dc-187">**Operazione:** inferiore al 20%</span><span class="sxs-lookup"><span data-stu-id="644dc-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="644dc-188">**Durata:** 10 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="644dc-189">**Durata:** 15 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="644dc-190">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="644dc-191">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-192">**Azione:** riduci numero di 1</span><span class="sxs-lookup"><span data-stu-id="644dc-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="644dc-193">**Azione:** riduci numero di 1</span><span class="sxs-lookup"><span data-stu-id="644dc-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="644dc-194">**Disattiva regole dopo (minuti):** 20</span><span class="sxs-lookup"><span data-stu-id="644dc-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="644dc-195">**Disattiva regole dopo (minuti):** 10</span><span class="sxs-lookup"><span data-stu-id="644dc-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="644dc-196">Tasso di inflazione del piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="644dc-196">App Service plan inflation rate</span></span>
<span data-ttu-id="644dc-197">Piani di servizio App che sono tooautoscale configurato a tale scopo una velocità massima di ogni ora.</span><span class="sxs-lookup"><span data-stu-id="644dc-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="644dc-198">Questa velocità può essere calcolata in base ai valori hello specificati nella regola di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="644dc-199">Comprensione e il calcolo hello *tasso di un piano di servizio App* è importante per la scalabilità automatica di servizio App ambiente perché il pool di lavoro tooa modifiche di scala non hanno effetto immediato.</span><span class="sxs-lookup"><span data-stu-id="644dc-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="644dc-200">frequenza di un piano di servizio App Hello viene calcolata come segue:</span><span class="sxs-lookup"><span data-stu-id="644dc-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![Calcolo del tasso di inflazione del piano di servizio app.][ASP-Inflation]

<span data-ttu-id="644dc-202">Basato su hello Autoscale-regola di scalabilità verticale per il profilo del giorno feriale hello di produzione hello piano di servizio App:</span><span class="sxs-lookup"><span data-stu-id="644dc-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di aumento.][Equation1]

<span data-ttu-id="644dc-204">Nel caso di hello di scalabilità automatica: regola di scalabilità verticale per il profilo del fine settimana hello di produzione hello piano di servizio App, hello formula hello viene risolto in:</span><span class="sxs-lookup"><span data-stu-id="644dc-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di aumento.][Equation2]

<span data-ttu-id="644dc-206">Questo valore può anche essere calcolato per le operazioni di riduzione.</span><span class="sxs-lookup"><span data-stu-id="644dc-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="644dc-207">In base a hello Autoscale-regola di scalabilità verso il basso per il profilo del giorno feriale hello di produzione hello piano di servizio App, ciò si presenterebbe come segue:</span><span class="sxs-lookup"><span data-stu-id="644dc-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di riduzione.][Equation3]

<span data-ttu-id="644dc-209">Nel caso di hello di scalabilità automatica: regola scalabilità verso il basso per il profilo del fine settimana hello di produzione hello piano di servizio App, hello formula hello viene risolto in:</span><span class="sxs-lookup"><span data-stu-id="644dc-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di riduzione.][Equation4]

<span data-ttu-id="644dc-211">produzione Hello piano di servizio App può raggiungere una velocità massima di otto istanze all'ora durante la settimana hello e quattro le istanze all'ora durante il weekend hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="644dc-212">È possibile rilasciare le istanze di una velocità massima di quattro istanze/ora settimana hello e sei istanze/ora durante il fine settimana.</span><span class="sxs-lookup"><span data-stu-id="644dc-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="644dc-213">Se più piani di servizio App sono ospitati in un pool di lavoro, è necessario hello toocalculate *frequenza un totale* come somma hello hello un tasso di per hello tutti i piani di servizio App che vengono hosting del pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="644dc-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![Calcolo del tasso di inflazione totale per più piani di servizio app ospitati in un pool di lavoro.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="644dc-215">Hello utilizzare servizio App di pianificare le regole di scalabilità automatica di un tasso toodefine lavoro pool</span><span class="sxs-lookup"><span data-stu-id="644dc-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="644dc-216">Pool di lavoro che ospitano i piani di servizio App che sono configurati tooautoscale necessario allocare un buffer di capacità.</span><span class="sxs-lookup"><span data-stu-id="644dc-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="644dc-217">buffer Hello consente toogrow di operazioni di scalabilità automatica hello e ridurre il piano di servizio App in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="644dc-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="644dc-218">minima del buffer Hello sarebbe hello calcolato totale App servizio prevede un tasso.</span><span class="sxs-lookup"><span data-stu-id="644dc-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="644dc-219">Le operazioni di ridimensionamento di servizio App ambiente richiedono alcuni tooapply ora, qualsiasi modifica dovrebbe tenere in considerazione ulteriori modifiche di richiesta che poteva verificarsi durante un'operazione di scala è in corso.</span><span class="sxs-lookup"><span data-stu-id="644dc-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="644dc-220">tooaccommodate questa latenza, si consiglia di utilizzare hello calcolato totale App servizio prevede un tasso come numero minimo di hello di istanze che vengono aggiunti per ogni operazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="644dc-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="644dc-221">Con queste informazioni, Frank possono definire hello seguente profilo di scalabilità automatica e le regole:</span><span class="sxs-lookup"><span data-stu-id="644dc-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![Regole del profilo di ridimensionamento automatico per l'esempio LOB.][Worker-Pool-Scale]

| <span data-ttu-id="644dc-223">**Profilo di ridimensionamento automatico - Giorni feriali**</span><span class="sxs-lookup"><span data-stu-id="644dc-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="644dc-224">**Profilo di ridimensionamento automatico - Fine settimana**</span><span class="sxs-lookup"><span data-stu-id="644dc-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="644dc-225">**Nome:** profilo Giorno feriale</span><span class="sxs-lookup"><span data-stu-id="644dc-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="644dc-226">**Nome:** profilo Fine settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="644dc-227">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="644dc-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="644dc-228">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="644dc-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="644dc-229">**Profilo:** giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="644dc-230">**Profilo:** fine settimana</span><span class="sxs-lookup"><span data-stu-id="644dc-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="644dc-231">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="644dc-231">**Type:** Recurrence</span></span> |<span data-ttu-id="644dc-232">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="644dc-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="644dc-233">**Intervallo di destinazione:** istanze too25 13</span><span class="sxs-lookup"><span data-stu-id="644dc-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="644dc-234">**Intervallo di destinazione:** 6 istanze too15</span><span class="sxs-lookup"><span data-stu-id="644dc-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="644dc-235">**Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì</span><span class="sxs-lookup"><span data-stu-id="644dc-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="644dc-236">**Giorni:** Sabato, Domenica</span><span class="sxs-lookup"><span data-stu-id="644dc-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="644dc-237">**Ora di inizio:** 7:00</span><span class="sxs-lookup"><span data-stu-id="644dc-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="644dc-238">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="644dc-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="644dc-239">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="644dc-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="644dc-240">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="644dc-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="644dc-241">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="644dc-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="644dc-242">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="644dc-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="644dc-243">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="644dc-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="644dc-244">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="644dc-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="644dc-245">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="644dc-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="644dc-246">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="644dc-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="644dc-247">**Operazione:** minore di 8</span><span class="sxs-lookup"><span data-stu-id="644dc-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="644dc-248">**Operazione:** minore di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="644dc-249">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="644dc-250">**Durata:** 30 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="644dc-251">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="644dc-252">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-253">**Azione:** aumenta numero di 8</span><span class="sxs-lookup"><span data-stu-id="644dc-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="644dc-254">**Azione:** aumenta numero di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="644dc-255">**Disattiva regole dopo (minuti):** 180</span><span class="sxs-lookup"><span data-stu-id="644dc-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="644dc-256">**Disattiva regole dopo (minuti):** 180</span><span class="sxs-lookup"><span data-stu-id="644dc-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="644dc-257">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="644dc-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="644dc-258">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="644dc-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="644dc-259">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="644dc-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="644dc-260">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="644dc-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="644dc-261">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="644dc-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="644dc-262">**Metrica:** Pool di lavoro disponibili</span><span class="sxs-lookup"><span data-stu-id="644dc-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="644dc-263">**Operazione:** maggiore di 8</span><span class="sxs-lookup"><span data-stu-id="644dc-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="644dc-264">**Operazione:** maggiore di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="644dc-265">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="644dc-266">**Durata:** 15 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="644dc-267">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="644dc-268">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-269">**Azione:** riduci numero di 2</span><span class="sxs-lookup"><span data-stu-id="644dc-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="644dc-270">**Azione:** riduci numero di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="644dc-271">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="644dc-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="644dc-272">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="644dc-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="644dc-273">intervallo di destinazione definito nel profilo hello Hello viene calcolato da istanze di hello minimo definite nel profilo per il piano di servizio App hello + buffer.</span><span class="sxs-lookup"><span data-stu-id="644dc-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="644dc-274">intervallo massimo Hello sarebbe somma hello di tutti gli intervalli massimo hello per tutti i piani di servizio App ospitati nel pool di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="644dc-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="644dc-275">conteggio di aumento per l'aumento di hello regole Hello deve essere set tooat almeno 1 X la frequenza di un piano di servizio App per la scala backup.</span><span class="sxs-lookup"><span data-stu-id="644dc-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="644dc-276">Conteggio di riduzione può essere adattata toosomething compreso tra 1/2 X o X 1 hello velocità di un piano di servizio App per la scalabilità verso il basso.</span><span class="sxs-lookup"><span data-stu-id="644dc-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="644dc-277">Ridimensionamento automatico per il pool front-end</span><span class="sxs-lookup"><span data-stu-id="644dc-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="644dc-278">Le regole per il ridimensionamento automatico front-end sono più semplici rispetto ai pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="644dc-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="644dc-279">È prima di tutto necessario</span><span class="sxs-lookup"><span data-stu-id="644dc-279">Primarily, you should</span></span>  
<span data-ttu-id="644dc-280">Assicurarsi che la durata della misurazione hello e timer di raffreddamento hello considera che le operazioni di ridimensionamento in un piano di servizio App non sono istantanee.</span><span class="sxs-lookup"><span data-stu-id="644dc-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="644dc-281">Per questo scenario, Frank SA tale tasso di errore hello aumenta dopo front-end di raggiungere l'80% della CPU e imposta la scalabilità automatica hello istanze tooincrease regola nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="644dc-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![Impostazioni di ridimensionamento automatico per il pool front-end.][Front-End-Scale]

| <span data-ttu-id="644dc-283">**Profilo di ridimensionamento automatico - Front-end**</span><span class="sxs-lookup"><span data-stu-id="644dc-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="644dc-284">**Nome:** Ridimensionamento automatico - Front-end</span><span class="sxs-lookup"><span data-stu-id="644dc-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="644dc-285">**Ridimensiona in base a:** regole per la pianificazione e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="644dc-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="644dc-286">**Profilo:** ogni giorno</span><span class="sxs-lookup"><span data-stu-id="644dc-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="644dc-287">**Tipo:** ricorrenza</span><span class="sxs-lookup"><span data-stu-id="644dc-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="644dc-288">**Intervallo di destinazione:** 3 istanze too10</span><span class="sxs-lookup"><span data-stu-id="644dc-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="644dc-289">**Giorni:** ogni giorno</span><span class="sxs-lookup"><span data-stu-id="644dc-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="644dc-290">**Ora di inizio:** 9:00</span><span class="sxs-lookup"><span data-stu-id="644dc-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="644dc-291">**Fuso orario:** UTC -08</span><span class="sxs-lookup"><span data-stu-id="644dc-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="644dc-292">**Regola di ridimensionamento automatico (aumento)**</span><span class="sxs-lookup"><span data-stu-id="644dc-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="644dc-293">**Risorsa:** pool front-end</span><span class="sxs-lookup"><span data-stu-id="644dc-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="644dc-294">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="644dc-295">**Operazione:** maggiore del 60%</span><span class="sxs-lookup"><span data-stu-id="644dc-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="644dc-296">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="644dc-297">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-298">**Azione:** aumenta numero di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="644dc-299">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="644dc-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="644dc-300">**Regola di ridimensionamento automatico (riduzione)**</span><span class="sxs-lookup"><span data-stu-id="644dc-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="644dc-301">**Risorsa:** Pool di lavoro 1</span><span class="sxs-lookup"><span data-stu-id="644dc-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="644dc-302">**Metrica:** % CPU</span><span class="sxs-lookup"><span data-stu-id="644dc-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="644dc-303">**Operazione:** inferiore al 30%</span><span class="sxs-lookup"><span data-stu-id="644dc-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="644dc-304">**Durata:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="644dc-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="644dc-305">**Aggregazione temporale:** media</span><span class="sxs-lookup"><span data-stu-id="644dc-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="644dc-306">**Azione:** riduci numero di 3</span><span class="sxs-lookup"><span data-stu-id="644dc-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="644dc-307">**Disattiva regole dopo (minuti):** 120</span><span class="sxs-lookup"><span data-stu-id="644dc-307">**Cool down (minutes):** 120</span></span> |

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
