---
title: "approfondire aaaDeep stimare integrità veicolo e Guida abitudini - Azure | Documenti Microsoft"
description: "Utilizzare funzionalità di hello di insights di predittiva e in tempo reale toogain Intelligence Cortana sull'integrità del veicolo e abitudini di Guida."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="cbca3-103">Playbook soluzione analitica telemetria di veicolo: approfondimento soluzione hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="cbca3-104">Questo **menu** collegamenti toohello sezioni di questo playbook:</span><span class="sxs-lookup"><span data-stu-id="cbca3-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="cbca3-105">Questa sezione drill-down in ognuna delle fasi di hello rappresentate hello architettura della soluzione con le istruzioni e i puntatori per la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="cbca3-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="cbca3-106">Origini dati</span><span class="sxs-lookup"><span data-stu-id="cbca3-106">Data Sources</span></span>
<span data-ttu-id="cbca3-107">soluzione Hello utilizza due origini dati diverse:</span><span class="sxs-lookup"><span data-stu-id="cbca3-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="cbca3-108">**set di dati di diagnostica e segnali del veicolo simulati** e</span><span class="sxs-lookup"><span data-stu-id="cbca3-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="cbca3-109">**catalogo dei veicoli**</span><span class="sxs-lookup"><span data-stu-id="cbca3-109">**vehicle catalog**</span></span>

<span data-ttu-id="cbca3-110">Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="cbca3-111">Genera informazioni di diagnostica ed segnala stato toohello corrispondente del veicolo hello e toohello gestiscono modello in un determinato punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="cbca3-112">Fare clic su [veicolo telematiche simulatore](http://go.microsoft.com/fwlink/?LinkId=717075) hello toodownload **veicolo telematiche simulatore soluzione Visual Studio** per le personalizzazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="cbca3-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="cbca3-113">catalogo veicolo Hello contiene un set di dati di riferimento con un mapping toomodel VPN.</span><span class="sxs-lookup"><span data-stu-id="cbca3-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Simulatore di dati telematici del veicolo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="cbca3-115">*Figura 1: Simulatore di dati telematici del veicolo*</span><span class="sxs-lookup"><span data-stu-id="cbca3-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="cbca3-116">Si tratta di un set di dati in formato JSON che contiene hello seguente schema.</span><span class="sxs-lookup"><span data-stu-id="cbca3-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="cbca3-117">Colonna</span><span class="sxs-lookup"><span data-stu-id="cbca3-117">Column</span></span> | <span data-ttu-id="cbca3-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cbca3-118">Description</span></span> | <span data-ttu-id="cbca3-119">Valori</span><span class="sxs-lookup"><span data-stu-id="cbca3-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbca3-120">vin</span><span class="sxs-lookup"><span data-stu-id="cbca3-120">VIN</span></span> |<span data-ttu-id="cbca3-121">Numero identificativo del veicolo generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="cbca3-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="cbca3-122">Viene ottenuto da un elenco master di 10.000 numeri identificativi di veicoli generati in modo casuale.</span><span class="sxs-lookup"><span data-stu-id="cbca3-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="cbca3-123">outsideTemperature</span><span class="sxs-lookup"><span data-stu-id="cbca3-123">Outside temperature</span></span> |<span data-ttu-id="cbca3-124">Hello all'esterno di temperatura in cui è piedi veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="cbca3-125">Numero da 0 a 100 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="cbca3-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="cbca3-126">engineTemperature</span><span class="sxs-lookup"><span data-stu-id="cbca3-126">Engine temperature</span></span> |<span data-ttu-id="cbca3-127">temperatura del motore di Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="cbca3-128">Numero da 0 a 500 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="cbca3-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="cbca3-129">Velocità</span><span class="sxs-lookup"><span data-stu-id="cbca3-129">Speed</span></span> |<span data-ttu-id="cbca3-130">velocità del motore di Hello determina in quali hello veicolo</span><span class="sxs-lookup"><span data-stu-id="cbca3-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="cbca3-131">Numero da 0 a 100 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="cbca3-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="cbca3-132">fuel</span><span class="sxs-lookup"><span data-stu-id="cbca3-132">Fuel</span></span> |<span data-ttu-id="cbca3-133">livello di carburante Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="cbca3-134">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di carburante)</span><span class="sxs-lookup"><span data-stu-id="cbca3-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="cbca3-135">engineoil</span><span class="sxs-lookup"><span data-stu-id="cbca3-135">EngineOil</span></span> |<span data-ttu-id="cbca3-136">livello di petrolio motore Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="cbca3-137">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di olio del motore)</span><span class="sxs-lookup"><span data-stu-id="cbca3-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="cbca3-138">Tire pressure</span><span class="sxs-lookup"><span data-stu-id="cbca3-138">Tire pressure</span></span> |<span data-ttu-id="cbca3-139">pressione tire Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="cbca3-140">Numero da 0 a 50 generato in modo casuale (indica la percentuale del livello di pressione degli pneumatici)</span><span class="sxs-lookup"><span data-stu-id="cbca3-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="cbca3-141">odometer</span><span class="sxs-lookup"><span data-stu-id="cbca3-141">Odometer</span></span> |<span data-ttu-id="cbca3-142">lettura di chilometraggio Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="cbca3-143">Numero da 0 a 200000 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="cbca3-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="cbca3-144">accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="cbca3-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="cbca3-145">posizione pedali Hello di tasti di scelta rapida del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="cbca3-146">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello dell'acceleratore)</span><span class="sxs-lookup"><span data-stu-id="cbca3-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="cbca3-147">parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="cbca3-147">Parking_brake_status</span></span> |<span data-ttu-id="cbca3-148">Indica se il veicolo hello è disattivato o meno</span><span class="sxs-lookup"><span data-stu-id="cbca3-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="cbca3-149">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-149">True or False</span></span> |
| <span data-ttu-id="cbca3-150">headlamp_status</span><span class="sxs-lookup"><span data-stu-id="cbca3-150">Headlamp_status</span></span> |<span data-ttu-id="cbca3-151">Indica dove proiettore hello è attiva o non</span><span class="sxs-lookup"><span data-stu-id="cbca3-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="cbca3-152">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-152">True or False</span></span> |
| <span data-ttu-id="cbca3-153">brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="cbca3-153">Brake_pedal_status</span></span> |<span data-ttu-id="cbca3-154">Indica se viene premuto pedale freni hello o non</span><span class="sxs-lookup"><span data-stu-id="cbca3-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="cbca3-155">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-155">True or False</span></span> |
| <span data-ttu-id="cbca3-156">transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="cbca3-156">Transmission_gear_position</span></span> |<span data-ttu-id="cbca3-157">posizione di ingranaggio trasmissione Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="cbca3-158">Stati: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="cbca3-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="cbca3-159">ignition_status</span><span class="sxs-lookup"><span data-stu-id="cbca3-159">Ignition_status</span></span> |<span data-ttu-id="cbca3-160">Indica se il veicolo hello è in esecuzione o arrestato</span><span class="sxs-lookup"><span data-stu-id="cbca3-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="cbca3-161">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-161">True or False</span></span> |
| <span data-ttu-id="cbca3-162">windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="cbca3-162">Windshield_wiper_status</span></span> |<span data-ttu-id="cbca3-163">Indica se è attivato Tergicristallo parabrezza hello o non</span><span class="sxs-lookup"><span data-stu-id="cbca3-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="cbca3-164">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-164">True or False</span></span> |
| <span data-ttu-id="cbca3-165">abs</span><span class="sxs-lookup"><span data-stu-id="cbca3-165">ABS</span></span> |<span data-ttu-id="cbca3-166">Indica se l'ABS è attivato o meno</span><span class="sxs-lookup"><span data-stu-id="cbca3-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="cbca3-167">true o false</span><span class="sxs-lookup"><span data-stu-id="cbca3-167">True or False</span></span> |
| <span data-ttu-id="cbca3-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="cbca3-168">Timestamp</span></span> |<span data-ttu-id="cbca3-169">timestamp di Hello quando viene creato il punto di dati hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="cbca3-170">Date</span><span class="sxs-lookup"><span data-stu-id="cbca3-170">Date</span></span> |
| <span data-ttu-id="cbca3-171">city</span><span class="sxs-lookup"><span data-stu-id="cbca3-171">City</span></span> |<span data-ttu-id="cbca3-172">percorso di Hello del veicolo hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-172">hello location of hello vehicle</span></span> |<span data-ttu-id="cbca3-173">4 città in questa soluzione: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="cbca3-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="cbca3-174">set di dati riferimento modello veicolo Hello contiene mapping del modello toohello VPN.</span><span class="sxs-lookup"><span data-stu-id="cbca3-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="cbca3-175">vin</span><span class="sxs-lookup"><span data-stu-id="cbca3-175">VIN</span></span> | <span data-ttu-id="cbca3-176">Modello</span><span class="sxs-lookup"><span data-stu-id="cbca3-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="cbca3-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="cbca3-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="cbca3-178">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-178">Sedan</span></span> |
| <span data-ttu-id="cbca3-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="cbca3-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="cbca3-180">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-180">Hybrid</span></span> |
| <span data-ttu-id="cbca3-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="cbca3-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="cbca3-182">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-182">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="cbca3-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="cbca3-184">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-184">Sedan</span></span> |
| <span data-ttu-id="cbca3-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="cbca3-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="cbca3-186">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-186">Hybrid</span></span> |
| <span data-ttu-id="cbca3-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="cbca3-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="cbca3-188">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-188">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="cbca3-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="cbca3-190">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-190">Sedan</span></span> |
| <span data-ttu-id="cbca3-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="cbca3-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="cbca3-192">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-192">Hybrid</span></span> |
| <span data-ttu-id="cbca3-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="cbca3-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="cbca3-194">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-194">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="cbca3-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="cbca3-196">Decappottabile</span><span class="sxs-lookup"><span data-stu-id="cbca3-196">Convertible</span></span> |
| <span data-ttu-id="cbca3-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="cbca3-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="cbca3-198">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="cbca3-198">Station Wagon</span></span> |
| <span data-ttu-id="cbca3-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="cbca3-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="cbca3-200">Utilitaria</span><span class="sxs-lookup"><span data-stu-id="cbca3-200">Compact Car</span></span> |
| <span data-ttu-id="cbca3-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="cbca3-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="cbca3-202">SUV di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="cbca3-202">Small SUV</span></span> |
| <span data-ttu-id="cbca3-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="cbca3-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="cbca3-204">Auto sportiva</span><span class="sxs-lookup"><span data-stu-id="cbca3-204">Sports Car</span></span> |
| <span data-ttu-id="cbca3-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="cbca3-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="cbca3-206">SUV di medie dimensioni</span><span class="sxs-lookup"><span data-stu-id="cbca3-206">Medium SUV</span></span> |
| <span data-ttu-id="cbca3-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="cbca3-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="cbca3-208">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="cbca3-208">Station Wagon</span></span> |
| <span data-ttu-id="cbca3-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="cbca3-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="cbca3-210">SUV di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="cbca3-210">Large SUV</span></span> |
| <span data-ttu-id="cbca3-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="cbca3-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="cbca3-212">SUV di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="cbca3-212">Large SUV</span></span> |
| <span data-ttu-id="cbca3-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="cbca3-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="cbca3-214">Coupé</span><span class="sxs-lookup"><span data-stu-id="cbca3-214">Coupe</span></span> |
| <span data-ttu-id="cbca3-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="cbca3-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="cbca3-216">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-216">Sedan</span></span> |
| <span data-ttu-id="cbca3-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="cbca3-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="cbca3-218">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-218">Hybrid</span></span> |
| <span data-ttu-id="cbca3-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="cbca3-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="cbca3-220">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-220">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="cbca3-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="cbca3-222">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-222">Sedan</span></span> |
| <span data-ttu-id="cbca3-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="cbca3-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="cbca3-224">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-224">Hybrid</span></span> |
| <span data-ttu-id="cbca3-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="cbca3-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="cbca3-226">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-226">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="cbca3-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="cbca3-228">Berlina</span><span class="sxs-lookup"><span data-stu-id="cbca3-228">Sedan</span></span> |
| <span data-ttu-id="cbca3-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="cbca3-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="cbca3-230">Ibrido</span><span class="sxs-lookup"><span data-stu-id="cbca3-230">Hybrid</span></span> |
| <span data-ttu-id="cbca3-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="cbca3-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="cbca3-232">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="cbca3-232">Family Saloon</span></span> |
| <span data-ttu-id="cbca3-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="cbca3-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="cbca3-234">Decappottabile</span><span class="sxs-lookup"><span data-stu-id="cbca3-234">Convertible</span></span> |
| <span data-ttu-id="cbca3-235">…….</span><span class="sxs-lookup"><span data-stu-id="cbca3-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="cbca3-236">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="cbca3-236">References</span></span>
[<span data-ttu-id="cbca3-237">Soluzione Vehicle Telematics Simulator di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbca3-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="cbca3-238">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="cbca3-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="cbca3-239">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="cbca3-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="cbca3-240">Ingestion</span><span class="sxs-lookup"><span data-stu-id="cbca3-240">Ingestion</span></span>
<span data-ttu-id="cbca3-241">Combinazioni di hub eventi di Azure, flusso Analitica e Data Factory vengono sfruttate tooingest hello veicolo segnali, gli eventi di diagnostica hello e in tempo reale e analitica del batch.</span><span class="sxs-lookup"><span data-stu-id="cbca3-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="cbca3-242">Tutti questi componenti creati e configurati come parte della distribuzione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="cbca3-243">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="cbca3-243">Real-time analysis</span></span>
<span data-ttu-id="cbca3-244">Hello gli eventi generati dal simulatore telematiche veicolo hello vengono pubblicati con Hub eventi toohello hello SDK Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="cbca3-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="cbca3-245">il processo di flusso Analitica Hello inserisce questi eventi dalla hello Hub eventi e processi hello dati integrità del veicolo hello tooanalyze in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cbca3-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Dashboard di Hub eventi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="cbca3-247">*Figura 4: Dashboard di Hub eventi*</span><span class="sxs-lookup"><span data-stu-id="cbca3-247">*Figure 4 - Event Hub dashboard*</span></span>

![Elaborazione dei dati da parte del processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="cbca3-249">*Figura 5: Elaborazione dei dati da parte del processo di Analisi di flusso*</span><span class="sxs-lookup"><span data-stu-id="cbca3-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="cbca3-250">processo di flusso Analitica Hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="cbca3-251">Inserisce i dati da hello Hub eventi</span><span class="sxs-lookup"><span data-stu-id="cbca3-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="cbca3-252">esegue un join con hello modello dati di riferimento toomap hello veicolo VPN toohello corrispondente</span><span class="sxs-lookup"><span data-stu-id="cbca3-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="cbca3-253">Li rende persistenti nell'archivio BLOB di Azure per l'analisi in batch avanzata</span><span class="sxs-lookup"><span data-stu-id="cbca3-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="cbca3-254">Hello seguente query Analitica di flusso è usato toopersist hello dati nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbca3-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Query del processo di Analisi di flusso per l'inserimento di dati](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="cbca3-256">*Figura 6: Query del processo di Analisi di flusso per l'inserimento di dati*</span><span class="sxs-lookup"><span data-stu-id="cbca3-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="cbca3-257">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="cbca3-257">Batch analysis</span></span>
<span data-ttu-id="cbca3-258">Viene anche generato un volume aggiuntivo di set di dati di diagnostica e segnali del veicolo simulati per rendere più completa l'analisi batch.</span><span class="sxs-lookup"><span data-stu-id="cbca3-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="cbca3-259">Questo è necessario tooensure un volume di dati rappresentativo validi per l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="cbca3-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="cbca3-260">A tale scopo, si sta usando una pipeline denominata "PrepareSampleDataPipeline" in toogenerate del flusso di lavoro di Azure Data Factory hello segnali veicolo simulata e set di dati diagnostici relativi a un anno.</span><span class="sxs-lookup"><span data-stu-id="cbca3-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="cbca3-261">Fare clic su [attività personalizzata di Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) hello toodownload attività Data Factory personalizzata DotNet soluzione di Visual Studio per le personalizzazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="cbca3-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="cbca3-263">*Figura 7: Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch*</span><span class="sxs-lookup"><span data-stu-id="cbca3-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="cbca3-264">Hello pipeline è costituita da .net personalizzato ADF attività Mostra qui:</span><span class="sxs-lookup"><span data-stu-id="cbca3-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Attività PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="cbca3-266">*Figure 8: PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="cbca3-267">Una volta pipeline hello viene eseguita correttamente e set di dati "RawCarEventsTable" è contrassegnato "Pronto", un anno vale la pena di segnali veicolo simulata e di diagnostica vengono generati i dati.</span><span class="sxs-lookup"><span data-stu-id="cbca3-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="cbca3-268">Verrà visualizzata hello seguente cartella e il file creato nell'account di archiviazione nel contenitore "connectedcar" hello:</span><span class="sxs-lookup"><span data-stu-id="cbca3-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Output di PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="cbca3-270">*Figura 9: Output di PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="cbca3-271">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="cbca3-271">References</span></span>
[<span data-ttu-id="cbca3-272">Azure Event Hub SDK per l'inserimento di flussi</span><span class="sxs-lookup"><span data-stu-id="cbca3-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="cbca3-273">[Funzionalità di spostamento dei dati di Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Attività DotNet di Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="cbca3-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="cbca3-274">Soluzione di Visual Studio per l'attività DotNet di Data factory di Azure per la preparazione dei dati di esempio</span><span class="sxs-lookup"><span data-stu-id="cbca3-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="cbca3-275">Set di dati di partizione hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-275">Partition hello dataset</span></span>
<span data-ttu-id="cbca3-276">segnali raw veicolo semistrutturati Hello e set di dati diagnostici vengono partizionati in fase di preparazione dei dati hello in un formato di mese/anno.</span><span class="sxs-lookup"><span data-stu-id="cbca3-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="cbca3-277">Questo partizionamento Alza di livello più efficiente l'esecuzione di query e archiviazione a lungo termine scalabile abilitando errore failover da un blob account toohello successivamente come primo account hello è piena.</span><span class="sxs-lookup"><span data-stu-id="cbca3-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="cbca3-278">Questo passaggio nella soluzione hello è applicabile toobatch solo elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cbca3-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="cbca3-279">Gestione dati di input e di output:</span><span class="sxs-lookup"><span data-stu-id="cbca3-279">Input and output data data management:</span></span>

* <span data-ttu-id="cbca3-280">Hello **i dati di output** (con etichetta *PartitionedCarEventsTable*) è toobe mantenere per un lungo periodo di tempo come modulo fondamentali / "rawest" hello, di dati "Data Lake" del cliente hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="cbca3-281">Hello **dati di input** toothis pipeline verrebbe in genere eliminata come dati di output di hello sono toohello di fedeltà completo di input: appena archiviato (partizionata) meglio per l'utilizzo successivo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Flusso di lavoro PartitionCarEvents](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="cbca3-283">*Figura 10: Flusso di lavoro PartitionCarEvents*</span><span class="sxs-lookup"><span data-stu-id="cbca3-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="cbca3-284">dati non elaborati Hello sono partizionati usando un'attività Hive di HDInsight in "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="cbca3-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="cbca3-285">i dati di esempio Hello generati nel passaggio 1 per un anno vengono partizionati per anno/mese.</span><span class="sxs-lookup"><span data-stu-id="cbca3-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="cbca3-286">le partizioni di Hello sono utilizzati toogenerate veicolo segnali e dati di diagnostica per ogni mese (totale 12 partizioni) di un anno.</span><span class="sxs-lookup"><span data-stu-id="cbca3-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Attività PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="cbca3-288">*Figura 11: PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="cbca3-289">***Script Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="cbca3-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="cbca3-290">Hello seguenti script Hive, denominato "partitioncarevents.hql", viene utilizzato per il partizionamento e si trova nella cartella "\demo\src\connectedcar\scripts" hello di zip scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="cbca3-291">Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Output partizionato](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="cbca3-293">*Figura 12: Output partizionato*</span><span class="sxs-lookup"><span data-stu-id="cbca3-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="cbca3-294">dati Hello ora è ottimizzato, è più gestibile e pronto per l'ulteriore elaborazione insights batch rich toogain.</span><span class="sxs-lookup"><span data-stu-id="cbca3-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="cbca3-295">Analisi dei dati</span><span class="sxs-lookup"><span data-stu-id="cbca3-295">Data Analysis</span></span>
<span data-ttu-id="cbca3-296">In questa sezione viene visualizzato come toocombine Analitica di flusso di Azure, Azure Machine Learning, Data Factory di Azure e Azure HDInsight per rich avanzate abitudini analitica integrità veicolo e la Guida.</span><span class="sxs-lookup"><span data-stu-id="cbca3-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="cbca3-297">Sono presenti tre sottosezioni:</span><span class="sxs-lookup"><span data-stu-id="cbca3-297">There are three subsections here:</span></span>

1. <span data-ttu-id="cbca3-298">**Machine Learning**: in questa sottosezione contiene informazioni su esperimento di rilevamento di anomalie hello che è stata usata in questo veicoli toopredict soluzioni che richiedono manutenzione e che richiedono richiami a causa di problemi toosafety veicoli di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="cbca3-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="cbca3-299">**Analisi in tempo reale**: in questa sottosezione contiene informazioni relative alle hello in tempo reale analitica utilizzando il linguaggio di Query di flusso Analitica hello e operatività apprendimento hello sperimentare in tempo reale mediante un'applicazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="cbca3-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="cbca3-300">**Batch analysis**: in questa sottosezione contiene informazioni riguardanti hello di trasformazione e di elaborazione dei dati di batch hello utilizzando Azure HDInsight e operativi da Azure Data Factory di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cbca3-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="cbca3-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cbca3-301">Machine Learning</span></span>
<span data-ttu-id="cbca3-302">Il nostro obiettivo è veicoli hello toopredict che richiedono manutenzione o il richiamo in base a determinate statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="cbca3-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="cbca3-303">Rendiamo hello seguenti presupposti</span><span class="sxs-lookup"><span data-stu-id="cbca3-303">We make hello following assumptions</span></span>

* <span data-ttu-id="cbca3-304">Se uno dei seguenti tre condizioni hello è vere, veicoli hello richiedono **manutenzione manutenzione**:</span><span class="sxs-lookup"><span data-stu-id="cbca3-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="cbca3-305">La pressione degli pneumatici è bassa</span><span class="sxs-lookup"><span data-stu-id="cbca3-305">Tire pressure is low</span></span>
  * <span data-ttu-id="cbca3-306">Il livello di olio del motore è basso</span><span class="sxs-lookup"><span data-stu-id="cbca3-306">Engine oil level is low</span></span>
  * <span data-ttu-id="cbca3-307">La temperatura del motore è elevata</span><span class="sxs-lookup"><span data-stu-id="cbca3-307">Engine temperature is high</span></span>
* <span data-ttu-id="cbca3-308">Se uno di hello seguenti condizioni è vere, potrebbero essere veicoli hello un **problema di sicurezza** e richiedono **richiamo**:</span><span class="sxs-lookup"><span data-stu-id="cbca3-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="cbca3-309">La temperatura del motore è elevata, ma la temperatura esterna è bassa</span><span class="sxs-lookup"><span data-stu-id="cbca3-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="cbca3-310">La temperatura del motore è bassa, ma la temperatura esterna è elevata</span><span class="sxs-lookup"><span data-stu-id="cbca3-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="cbca3-311">In base ai requisiti precedenti hello, è stata creata anomalie di toodetect due modelli separati, uno per il rilevamento di manutenzione veicolo e uno per il rilevamento di richiamo vehicle.</span><span class="sxs-lookup"><span data-stu-id="cbca3-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="cbca3-312">In entrambi questi modelli, algoritmo di analisi in componenti principali (PCA) incorporato hello viene utilizzato per il rilevamento di anomalie.</span><span class="sxs-lookup"><span data-stu-id="cbca3-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="cbca3-313">**Modello di rilevamento per la manutenzione**</span><span class="sxs-lookup"><span data-stu-id="cbca3-313">**Maintenance detection model**</span></span>

<span data-ttu-id="cbca3-314">Se uno dei tre indicatori pressione tire, olio motore o temperatura del motore - soddisfa la condizione corrispondente, il modello di rilevamento di hello manutenzione segnala un'anomalia.</span><span class="sxs-lookup"><span data-stu-id="cbca3-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="cbca3-315">Di conseguenza, è necessario solo tooconsider questi tre variabili di compilazione del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="cbca3-316">In questo esperimento in Azure Machine Learning, viene utilizzata una **selezionare le colonne nel set di dati** tooextract modulo queste tre variabili.</span><span class="sxs-lookup"><span data-stu-id="cbca3-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="cbca3-317">Quindi utilizziamo hello anomalie basato su PCA modulo toobuild hello anomalie rilevamento modello di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="cbca3-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="cbca3-318">Analisi in componenti principali (PCA) è una tecnica consolidata in machine learning che può essere il rilevamento di anomalie, classificazione e selezione toofeature applicato.</span><span class="sxs-lookup"><span data-stu-id="cbca3-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="cbca3-319">Converte un set di casi contenente variabili probabilmente correlate in un set di valori denominati componenti principali.</span><span class="sxs-lookup"><span data-stu-id="cbca3-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="cbca3-320">Hello concetto principale alla base della modellazione basato su PCA è tooproject dati in uno spazio inferiore-dimensionale, in modo che le funzionalità e anomalie più facilmente identificabili.</span><span class="sxs-lookup"><span data-stu-id="cbca3-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="cbca3-321">Per ogni nuovo input hello troppo modello di rilevamento, il rilevamento di anomalie hello Calcola prima relativa proiezione di hello autovettori e quindi Calcola hello normalizzato errore ricostruzione.</span><span class="sxs-lookup"><span data-stu-id="cbca3-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="cbca3-322">Questo errore normalizzato è il punteggio di anomalie hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="cbca3-323">Errore di hello superiore Hello, hello più anomali hello istanza è.</span><span class="sxs-lookup"><span data-stu-id="cbca3-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="cbca3-324">Problema di rilevamento di manutenzione hello, ogni record può essere considerato come un punto in uno spazio 3D definito da pressione tire, olio motore e temperatura del motore coordinate.</span><span class="sxs-lookup"><span data-stu-id="cbca3-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="cbca3-325">toocapture queste anomalie, è possibile hello originale dati progetto nello spazio 3D hello in uno spazio 2 dimensioni utilizzando PCA.</span><span class="sxs-lookup"><span data-stu-id="cbca3-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="cbca3-326">Pertanto, viene impostato il parametro hello numero di componenti toouse in PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="cbca3-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="cbca3-327">Questo parametro ha un ruolo importante nell'applicazione del rilevamento delle anomalie basato su PCA.</span><span class="sxs-lookup"><span data-stu-id="cbca3-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="cbca3-328">Dopo aver eseguito la proiezione dei dati con l'analisi PCA, è possibile identificare più facilmente queste anomalie.</span><span class="sxs-lookup"><span data-stu-id="cbca3-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="cbca3-329">**Modello di rilevamento di anomalie di richiamo** nel modello di rilevamento di anomalie richiamo hello, utilizziamo hello selezionare le colonne nel set di dati e delle anomalie basato su PCA moduli di rilevamento in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="cbca3-330">Nello specifico, abbiamo estrarre innanzitutto tre variabili - temperatura del motore, temperatura esterna e velocità - utilizzando hello **selezionare le colonne nel set di dati** modulo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="cbca3-331">È inoltre includere velocità hello variabile poiché temperatura del motore di hello è in genere correlato toohello velocità.</span><span class="sxs-lookup"><span data-stu-id="cbca3-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="cbca3-332">È quindi utilizzare dati di hello tooproject modulo rilevamento delle anomalie basato su PCA dallo spazio di 3-dimensionale hello in uno spazio 2 dimensioni.</span><span class="sxs-lookup"><span data-stu-id="cbca3-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="cbca3-333">Hello richiamo criteri vengono soddisfatti e modo veicolo hello è necessario tenere presente quando temperatura del motore e la temperatura esterna sono correlate elevata negativamente.</span><span class="sxs-lookup"><span data-stu-id="cbca3-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="cbca3-334">Utilizza l'algoritmo di rilevamento delle anomalie basato su PCA, è possibile acquisire eventuali anomalie hello dopo l'esecuzione di PCA.</span><span class="sxs-lookup"><span data-stu-id="cbca3-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="cbca3-335">Durante il training di un modello, è necessario toouse dati normale, che non richiedono manutenzione o un richiamo come modello di rilevamento delle anomalie basato su PCA tootrain hello hello dati di input.</span><span class="sxs-lookup"><span data-stu-id="cbca3-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="cbca3-336">In hello esperimento di assegnazione dei punteggi, utilizziamo toodetect modello rilevamento anomalie di hello training veicolo hello richiede manutenzione o il richiamo o meno.</span><span class="sxs-lookup"><span data-stu-id="cbca3-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="cbca3-337">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="cbca3-337">Real-time analysis</span></span>
<span data-ttu-id="cbca3-338">Hello flusso Analitica nella Query SQL seguente viene utilizzato il Media hello tooget di tutte hello parametri veicolo importanti come velocità del veicolo, livello di carburante, temperatura del motore, lettura chilometraggio, pressione tire, livello di motore petrolio e altri.</span><span class="sxs-lookup"><span data-stu-id="cbca3-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="cbca3-339">medie Hello vengono utilizzati toodetect anomalie, generano avvisi e determinare hello condizioni di integrità complessivo dei veicoli usati in area specifica e quindi ne esegue la correlazione toodemographics.</span><span class="sxs-lookup"><span data-stu-id="cbca3-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Query di Analisi di flusso per l'elaborazione in tempo reale](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="cbca3-341">*Figura 13: Query di Analisi di flusso per l'elaborazione in tempo reale*</span><span class="sxs-lookup"><span data-stu-id="cbca3-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="cbca3-342">Tutti i valori medi di hello vengono calcolate su un TumblingWindow 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="cbca3-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="cbca3-343">In questo caso viene usata la finestra a cascata perché sono necessari intervalli di tempo contigui e non sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="cbca3-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="cbca3-344">Fare clic su toolearn ulteriori informazioni su tutte le funzionalità di "Windowing" hello in Azure flusso Analitica, [Windowing (Analitica del flusso di Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbca3-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="cbca3-345">**Stima in tempo reale**</span><span class="sxs-lookup"><span data-stu-id="cbca3-345">**Real-time prediction**</span></span>

<span data-ttu-id="cbca3-346">Un'applicazione è inclusa come parte del modello di soluzione toooperationalize hello machine learning hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cbca3-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="cbca3-347">Questa applicazione denominata "RealTimeDashboardApp" viene creata e configurata come parte della distribuzione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="cbca3-348">un'applicazione Hello esegue l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="cbca3-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="cbca3-349">È in ascolto tooan istanza dell'Hub di eventi in cui Analitica flusso pubblica eventi hello in un modello in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="cbca3-350">![Query Analitica di flusso per la pubblicazione di dati hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *figura 14: query Analitica di flusso per la pubblicazione di hello dati tooan istanza dell'Hub di eventi di output*</span><span class="sxs-lookup"><span data-stu-id="cbca3-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="cbca3-351">Per ogni evento ricevuto dall'applicazione:</span><span class="sxs-lookup"><span data-stu-id="cbca3-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="cbca3-352">Processi hello dati utilizzando l'endpoint di Machine Learning richiesta-risposta di punteggio (RR).</span><span class="sxs-lookup"><span data-stu-id="cbca3-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="cbca3-353">endpoint RR Hello viene pubblicato automaticamente come parte della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="cbca3-354">output di Hello RR è set di dati di Power BI tooa pubblicati tramite push hello API.</span><span class="sxs-lookup"><span data-stu-id="cbca3-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="cbca3-355">Questo modello è inoltre applicabile tooscenarios in cui si desidera toointegrate un'applicazione Line of Business (LoB) con il flusso in tempo reale analitica hello, per gli scenari, ad esempio gli avvisi, notifiche e messaggistica.</span><span class="sxs-lookup"><span data-stu-id="cbca3-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="cbca3-356">Fare clic su [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload RealtimeDashboardApp soluzione Visual Studio per le personalizzazioni.</span><span class="sxs-lookup"><span data-stu-id="cbca3-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="cbca3-357">**hello tooexecute applicazione Dashboard in tempo reale**</span><span class="sxs-lookup"><span data-stu-id="cbca3-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="cbca3-358">Estrarre e salvare in locale. ![Cartella RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figura 16: Cartella RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="cbca3-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="cbca3-359">Eseguire un'applicazione hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="cbca3-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="cbca3-360">Fornire credenziali di Power BI valide, accedere e fare clic su Accetta.</span><span class="sxs-lookup"><span data-stu-id="cbca3-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Dashboard in tempo reale app Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Dashboard in tempo reale app fine Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="cbca3-363">*Figura 17: RealtimeDashboardApp: Accedi tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="cbca3-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="cbca3-364">Se si desidera il set di dati di tooflush hello Power BI, eseguire hello RealtimeDashboardApp con il parametro "flushdata" hello:</span><span class="sxs-lookup"><span data-stu-id="cbca3-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="cbca3-365">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="cbca3-365">Batch analysis</span></span>
<span data-ttu-id="cbca3-366">obiettivo Hello è tooshow come motori di Contoso utilizza hello calcolo di Azure funzionalità tooharness dati toogain dettagliate sull'ottimizzazione del modello, il comportamento di utilizzo e integrità vehicle.</span><span class="sxs-lookup"><span data-stu-id="cbca3-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="cbca3-367">In questo modo è possibile:</span><span class="sxs-lookup"><span data-stu-id="cbca3-367">This makes it possible to:</span></span>

* <span data-ttu-id="cbca3-368">Migliorare l'esperienza dei clienti hello e renderlo più economica, fornendo informazioni sulla Guida dell'utente e i comportamenti di Guida efficiente di carburante</span><span class="sxs-lookup"><span data-stu-id="cbca3-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="cbca3-369">Conoscere in modo proattivo di clienti e le decisioni di business toogovern modelli di Guida e fornire hello meglio in classe prodotti e servizi</span><span class="sxs-lookup"><span data-stu-id="cbca3-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="cbca3-370">In questa soluzione, destinazione hello seguenti metriche:</span><span class="sxs-lookup"><span data-stu-id="cbca3-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="cbca3-371">**Aggressivo piedi comportamento**: identifica tendenza hello di modelli di hello, posizioni, condizioni di Guida e tempo di insights di toogain anno hello aggressiva modelli determinante.</span><span class="sxs-lookup"><span data-stu-id="cbca3-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="cbca3-372">Contoso Motors può usare queste informazioni per creare campagne di marketing, nuove funzionalità personalizzate e assicurazioni basate sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="cbca3-373">**Comportamento determinante efficiente alimentano**: identifica tendenza hello di modelli di hello, percorsi, le condizioni di Guida e tempo di insights di toogain anno hello modelli determinante efficiente carburante.</span><span class="sxs-lookup"><span data-stu-id="cbca3-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="cbca3-374">Motori di Contoso può utilizzare queste informazioni per campagne di marketing piedi nuove funzionalità e proattivo driver toohello reporting per costo abitudini determinante descrittive validità e di ambiente.</span><span class="sxs-lookup"><span data-stu-id="cbca3-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="cbca3-375">**Tenere presente i modelli**: identifica i modelli che richiedono richiamate da operatività esperimento di machine learning rilevamento di anomalie di hello</span><span class="sxs-lookup"><span data-stu-id="cbca3-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="cbca3-376">Esaminare i dettagli di hello di ognuna di queste metriche,</span><span class="sxs-lookup"><span data-stu-id="cbca3-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="cbca3-377">**Stile di guida aggressivo**</span><span class="sxs-lookup"><span data-stu-id="cbca3-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="cbca3-378">Hello partizionati segnali veicolo e dati di diagnostica vengono elaborati nella pipeline hello denominata "AggresiveDrivingPatternPipeline" utilizzando i modelli di hello toodetermine Hive, percorso, veicolo, determinano le condizioni e gli altri parametri che presenta aggressiva modello di Guida.</span><span class="sxs-lookup"><span data-stu-id="cbca3-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="cbca3-379">![Flusso di lavoro per lo stile di guida aggressivo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figura 18: Flusso di lavoro per lo stile di guida aggressivo*</span><span class="sxs-lookup"><span data-stu-id="cbca3-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="cbca3-380">***Query Hive per lo stile di guida aggressivo***</span><span class="sxs-lookup"><span data-stu-id="cbca3-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="cbca3-381">Hello script Hive denominato "aggresivedriving.hql" usato per l'analisi aggressiva modello condizione Guida si trova nella cartella "\demo\src\connectedcar\scripts" di zip scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="cbca3-382">Utilizza la combinazione hello del veicolo trasmissione ingranaggio posizione, stato pedali freni e velocità toodetect reckless/aggressiva determinano il comportamento in base a frenatura modello ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="cbca3-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="cbca3-383">Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Output di AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="cbca3-385">*Figura 19: Output di AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="cbca3-386">**Stile di guida attento ai consumi**</span><span class="sxs-lookup"><span data-stu-id="cbca3-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="cbca3-387">Hello partizionata segnali veicolo e dati di diagnostica vengono elaborati nella pipeline hello denominata "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="cbca3-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="cbca3-388">Hive è usato toodetermine hello modelli, percorso, veicolo, condizioni di Guida e altre proprietà con carburante efficiente determinante.</span><span class="sxs-lookup"><span data-stu-id="cbca3-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Stile di guida attento ai consumi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="cbca3-390">*Figura 20: Flusso di lavoro per lo stile di guida attento ai consumi*</span><span class="sxs-lookup"><span data-stu-id="cbca3-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="cbca3-391">***Query Hive per lo stile di guida attento ai consumi***</span><span class="sxs-lookup"><span data-stu-id="cbca3-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="cbca3-392">Hello script Hive denominato "fuelefficientdriving.hql" usato per l'analisi aggressiva modello condizione Guida si trova nella cartella "\demo\src\connectedcar\scripts" di zip scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="cbca3-393">Combinazione di hello di trasmissione a forma di ingranaggio posizione del veicolo, stato pedali freni, velocità e carburante toodetect pedali posizione di tasti di scelta rapida efficiente comportamento Guida basato sull'accelerazione, frenatura, utilizza e velocizzare i modelli.</span><span class="sxs-lookup"><span data-stu-id="cbca3-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="cbca3-394">Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Output di FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="cbca3-396">*Figura 21: Output di FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="cbca3-397">**Previsioni di richiamo**</span><span class="sxs-lookup"><span data-stu-id="cbca3-397">**Recall Predictions**</span></span>

<span data-ttu-id="cbca3-398">Hello esperimento di machine learning è stato eseguito il provisioning e pubblicata come servizio web come parte della distribuzione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="cbca3-399">punto finale di punteggio batch di Hello viene usata in questo flusso di lavoro operativi utilizzando l'attività di punteggio batch di data factory e registrato come un servizio di data factory collegato.</span><span class="sxs-lookup"><span data-stu-id="cbca3-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Endpoint di Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="cbca3-401">*Figura 22: Endpoint di Machine Learning registrato come servizio collegato in Data factory*</span><span class="sxs-lookup"><span data-stu-id="cbca3-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="cbca3-402">servizio collegato registrato Hello viene utilizzato nei dati di hello DetectAnomalyPipeline tooscore hello utilizzando il modello di rilevamento delle anomalie di hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Attività di assegnazione punteggio batch di Machine Learning in Data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="cbca3-404">*Figura 23: Attività di assegnazione punteggio batch di Azure Machine Learning in Data factory*</span><span class="sxs-lookup"><span data-stu-id="cbca3-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="cbca3-405">Esistono alcuni passaggi eseguiti nella pipeline per la preparazione dei dati, in modo che può essere operationalized con il servizio web di punteggio batch di hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline per la stima dei veicoli da richiamare](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="cbca3-407">*Figura 24: DetectAnomalyPipeline per la stima dei veicoli da richiamare*</span><span class="sxs-lookup"><span data-stu-id="cbca3-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="cbca3-408">***Query Hive per il rilevamento delle anomalie***</span><span class="sxs-lookup"><span data-stu-id="cbca3-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="cbca3-409">Una volta completato il punteggio di hello, un'attività di HDInsight è tooprocess utilizzati e i dati di aggregazione hello sono classificati come anomalie dal modello hello con un punteggio di probabilità di 0.60 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="cbca3-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="cbca3-410">Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Output di DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="cbca3-412">*Figura 25: Output di DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="cbca3-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="cbca3-413">Pubblica</span><span class="sxs-lookup"><span data-stu-id="cbca3-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="cbca3-414">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="cbca3-414">Real-time analysis</span></span>
<span data-ttu-id="cbca3-415">Una delle query hello nel processo di flusso Analitica hello pubblica output di hello eventi tooan istanza dell'Hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="cbca3-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Processo di flusso Analitica pubblica output tooan istanza dell'Hub eventi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="cbca3-417">*Figura 26-processo di flusso Analitica pubblica output tooan istanza dell'Hub eventi*</span><span class="sxs-lookup"><span data-stu-id="cbca3-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Istanza di Hub di eventi di output flusso Analitica query toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="cbca3-419">*Figura 27-istanza di Hub di eventi di output flusso Analitica query toopublish toohello*</span><span class="sxs-lookup"><span data-stu-id="cbca3-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="cbca3-420">Questo flusso di eventi è utilizzato da hello che realtimedashboardapp inclusi nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="cbca3-421">L'applicazione utilizza il servizio web di Machine Learning richiesta-risposta hello per il punteggio in tempo reale e pubblica hello dati risultante tooa Power BI dataset per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="cbca3-422">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="cbca3-422">Batch analysis</span></span>
<span data-ttu-id="cbca3-423">risultati Hello del batch di hello ed elaborazione in tempo reale sono tabelle di Database SQL di Azure toohello pubblicati per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cbca3-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="cbca3-424">Hello Azure SQL Server, Database e tabelle hello vengono create automaticamente come parte dello script di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Flusso di lavoro mart toodata di copiare i risultati di elaborazione batch](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="cbca3-426">*Figura 28-risultati copia toodata mart flusso di lavoro di elaborazione Batch*</span><span class="sxs-lookup"><span data-stu-id="cbca3-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Processo di flusso Analitica pubblica toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="cbca3-428">*Figura 29-processo di flusso Analitica pubblica toodata mart*</span><span class="sxs-lookup"><span data-stu-id="cbca3-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Impostazione di data mart nel processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="cbca3-430">*Figura 30: Impostazione di data mart nel processo di Analisi di flusso*</span><span class="sxs-lookup"><span data-stu-id="cbca3-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="cbca3-431">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="cbca3-431">Consume</span></span>
<span data-ttu-id="cbca3-432">Power BI offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittive.</span><span class="sxs-lookup"><span data-stu-id="cbca3-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="cbca3-433">Fare clic qui per informazioni dettagliate su come configurare i report di Power BI hello e dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="cbca3-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="cbca3-434">dashboard di Hello finale è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cbca3-434">hello final dashboard looks like this:</span></span>

![Dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="cbca3-436">*Figura 31: Dashboard di Power BI*</span><span class="sxs-lookup"><span data-stu-id="cbca3-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="cbca3-437">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cbca3-437">Summary</span></span>
<span data-ttu-id="cbca3-438">Questo documento contiene un drill-down dettagliato di hello veicolo telemetria Analitica soluzione.</span><span class="sxs-lookup"><span data-stu-id="cbca3-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="cbca3-439">Questa presenta un modello di architettura lambda per l'analisi batch e in tempo reale completa di stime e azioni.</span><span class="sxs-lookup"><span data-stu-id="cbca3-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="cbca3-440">Questo modello viene applicato tooa ampia gamma di casi d'uso che richiedono percorso a caldo (in tempo reale) e analitica freddo percorso (batch).</span><span class="sxs-lookup"><span data-stu-id="cbca3-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

