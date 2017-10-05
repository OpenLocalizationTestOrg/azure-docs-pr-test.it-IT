---
title: "Approfondimento sulla previsione dell'integrità dei veicoli e sulle abitudini di guida - Azure | Documentazione Microsoft"
description: "Usare le funzionalità di Cortana Intelligence per ottenere informazioni dettagliate predittive e in tempo reale sullo stato di integrità del veicolo e sulle abitudini di guida."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="b5766-103">Studio della soluzione di analisi dei dati di telemetria del veicolo: Approfondimento della soluzione</span><span class="sxs-lookup"><span data-stu-id="b5766-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="b5766-104">Questo **menu** contiene i collegamenti alle sezioni dello studio:</span><span class="sxs-lookup"><span data-stu-id="b5766-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="b5766-105">Questa sezione approfondisce ognuna delle fasi rappresentate nell'architettura della soluzione, con istruzioni e indicazioni per la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="b5766-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="b5766-106">Origini dati</span><span class="sxs-lookup"><span data-stu-id="b5766-106">Data Sources</span></span>
<span data-ttu-id="b5766-107">La soluzione usa due origini dati diverse:</span><span class="sxs-lookup"><span data-stu-id="b5766-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="b5766-108">**set di dati di diagnostica e segnali del veicolo simulati** e</span><span class="sxs-lookup"><span data-stu-id="b5766-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="b5766-109">**catalogo dei veicoli**</span><span class="sxs-lookup"><span data-stu-id="b5766-109">**vehicle catalog**</span></span>

<span data-ttu-id="b5766-110">Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="b5766-111">Il simulatore genera informazioni di diagnostica e segnali corrispondenti allo stato del veicolo e allo schema di guida in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="b5766-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="b5766-112">Fare clic su [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) per scaricare la **soluzione Vehicle Telematics Simulator di Visual Studio** ed eseguire le personalizzazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="b5766-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="b5766-113">Il catalogo dei veicoli contiene un set di dati di riferimento con il numero identificativo del veicolo (NIV) per il mapping del modello.</span><span class="sxs-lookup"><span data-stu-id="b5766-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Simulatore di dati telematici del veicolo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="b5766-115">*Figura 1: Simulatore di dati telematici del veicolo*</span><span class="sxs-lookup"><span data-stu-id="b5766-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="b5766-116">Questo è un set di dati in formato JSON contenente lo schema seguente.</span><span class="sxs-lookup"><span data-stu-id="b5766-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="b5766-117">Colonna</span><span class="sxs-lookup"><span data-stu-id="b5766-117">Column</span></span> | <span data-ttu-id="b5766-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5766-118">Description</span></span> | <span data-ttu-id="b5766-119">Valori</span><span class="sxs-lookup"><span data-stu-id="b5766-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5766-120">vin</span><span class="sxs-lookup"><span data-stu-id="b5766-120">VIN</span></span> |<span data-ttu-id="b5766-121">Numero identificativo del veicolo generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="b5766-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="b5766-122">Viene ottenuto da un elenco master di 10.000 numeri identificativi di veicoli generati in modo casuale.</span><span class="sxs-lookup"><span data-stu-id="b5766-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="b5766-123">outsideTemperature</span><span class="sxs-lookup"><span data-stu-id="b5766-123">Outside temperature</span></span> |<span data-ttu-id="b5766-124">Temperatura all'esterno durante la guida del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="b5766-125">Numero da 0 a 100 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="b5766-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="b5766-126">engineTemperature</span><span class="sxs-lookup"><span data-stu-id="b5766-126">Engine temperature</span></span> |<span data-ttu-id="b5766-127">Temperatura del motore del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="b5766-128">Numero da 0 a 500 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="b5766-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="b5766-129">speed</span><span class="sxs-lookup"><span data-stu-id="b5766-129">Speed</span></span> |<span data-ttu-id="b5766-130">Velocità del motore durante la guida del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="b5766-131">Numero da 0 a 100 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="b5766-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="b5766-132">fuel</span><span class="sxs-lookup"><span data-stu-id="b5766-132">Fuel</span></span> |<span data-ttu-id="b5766-133">Livello di carburante del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="b5766-134">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di carburante)</span><span class="sxs-lookup"><span data-stu-id="b5766-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="b5766-135">engineoil</span><span class="sxs-lookup"><span data-stu-id="b5766-135">EngineOil</span></span> |<span data-ttu-id="b5766-136">Livello dell'olio del motore del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="b5766-137">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di olio del motore)</span><span class="sxs-lookup"><span data-stu-id="b5766-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="b5766-138">Tire pressure</span><span class="sxs-lookup"><span data-stu-id="b5766-138">Tire pressure</span></span> |<span data-ttu-id="b5766-139">Pressione degli pneumatici del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="b5766-140">Numero da 0 a 50 generato in modo casuale (indica la percentuale del livello di pressione degli pneumatici)</span><span class="sxs-lookup"><span data-stu-id="b5766-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="b5766-141">odometer</span><span class="sxs-lookup"><span data-stu-id="b5766-141">Odometer</span></span> |<span data-ttu-id="b5766-142">Lettura del contachilometri del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="b5766-143">Numero da 0 a 200000 generato in modo casuale</span><span class="sxs-lookup"><span data-stu-id="b5766-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="b5766-144">accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="b5766-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="b5766-145">Posizione del pedale dell'acceleratore del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="b5766-146">Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello dell'acceleratore)</span><span class="sxs-lookup"><span data-stu-id="b5766-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="b5766-147">parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="b5766-147">Parking_brake_status</span></span> |<span data-ttu-id="b5766-148">Indica se il freno di stazionamento è attivato o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="b5766-149">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-149">True or False</span></span> |
| <span data-ttu-id="b5766-150">headlamp_status</span><span class="sxs-lookup"><span data-stu-id="b5766-150">Headlamp_status</span></span> |<span data-ttu-id="b5766-151">Indica se il fanale anteriore è acceso o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="b5766-152">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-152">True or False</span></span> |
| <span data-ttu-id="b5766-153">brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="b5766-153">Brake_pedal_status</span></span> |<span data-ttu-id="b5766-154">Indica se il pedale del freno è premuto o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="b5766-155">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-155">True or False</span></span> |
| <span data-ttu-id="b5766-156">transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="b5766-156">Transmission_gear_position</span></span> |<span data-ttu-id="b5766-157">Posizione del cambio del veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="b5766-158">Stati: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="b5766-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="b5766-159">ignition_status</span><span class="sxs-lookup"><span data-stu-id="b5766-159">Ignition_status</span></span> |<span data-ttu-id="b5766-160">Indica se il veicolo è acceso o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="b5766-161">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-161">True or False</span></span> |
| <span data-ttu-id="b5766-162">windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="b5766-162">Windshield_wiper_status</span></span> |<span data-ttu-id="b5766-163">Indica se il tergicristallo è attivato o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="b5766-164">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-164">True or False</span></span> |
| <span data-ttu-id="b5766-165">abs</span><span class="sxs-lookup"><span data-stu-id="b5766-165">ABS</span></span> |<span data-ttu-id="b5766-166">Indica se l'ABS è attivato o meno</span><span class="sxs-lookup"><span data-stu-id="b5766-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="b5766-167">true o false</span><span class="sxs-lookup"><span data-stu-id="b5766-167">True or False</span></span> |
| <span data-ttu-id="b5766-168">timestamp</span><span class="sxs-lookup"><span data-stu-id="b5766-168">Timestamp</span></span> |<span data-ttu-id="b5766-169">Timestamp di creazione del punto dati</span><span class="sxs-lookup"><span data-stu-id="b5766-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="b5766-170">Data</span><span class="sxs-lookup"><span data-stu-id="b5766-170">Date</span></span> |
| <span data-ttu-id="b5766-171">city</span><span class="sxs-lookup"><span data-stu-id="b5766-171">City</span></span> |<span data-ttu-id="b5766-172">Località in cui si trova il veicolo</span><span class="sxs-lookup"><span data-stu-id="b5766-172">The location of the vehicle</span></span> |<span data-ttu-id="b5766-173">4 città in questa soluzione: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="b5766-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="b5766-174">Il set di dati di riferimento del modello di veicolo contiene il mapping del numero identificativo del veicolo al modello.</span><span class="sxs-lookup"><span data-stu-id="b5766-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="b5766-175">vin</span><span class="sxs-lookup"><span data-stu-id="b5766-175">VIN</span></span> | <span data-ttu-id="b5766-176">Modello</span><span class="sxs-lookup"><span data-stu-id="b5766-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="b5766-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="b5766-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="b5766-178">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-178">Sedan</span></span> |
| <span data-ttu-id="b5766-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="b5766-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="b5766-180">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-180">Hybrid</span></span> |
| <span data-ttu-id="b5766-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="b5766-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="b5766-182">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-182">Family Saloon</span></span> |
| <span data-ttu-id="b5766-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="b5766-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="b5766-184">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-184">Sedan</span></span> |
| <span data-ttu-id="b5766-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="b5766-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="b5766-186">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-186">Hybrid</span></span> |
| <span data-ttu-id="b5766-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="b5766-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="b5766-188">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-188">Family Saloon</span></span> |
| <span data-ttu-id="b5766-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="b5766-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="b5766-190">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-190">Sedan</span></span> |
| <span data-ttu-id="b5766-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="b5766-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="b5766-192">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-192">Hybrid</span></span> |
| <span data-ttu-id="b5766-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="b5766-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="b5766-194">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-194">Family Saloon</span></span> |
| <span data-ttu-id="b5766-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="b5766-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="b5766-196">Decappottabile</span><span class="sxs-lookup"><span data-stu-id="b5766-196">Convertible</span></span> |
| <span data-ttu-id="b5766-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="b5766-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="b5766-198">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="b5766-198">Station Wagon</span></span> |
| <span data-ttu-id="b5766-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="b5766-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="b5766-200">Utilitaria</span><span class="sxs-lookup"><span data-stu-id="b5766-200">Compact Car</span></span> |
| <span data-ttu-id="b5766-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="b5766-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="b5766-202">SUV di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="b5766-202">Small SUV</span></span> |
| <span data-ttu-id="b5766-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="b5766-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="b5766-204">Auto sportiva</span><span class="sxs-lookup"><span data-stu-id="b5766-204">Sports Car</span></span> |
| <span data-ttu-id="b5766-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="b5766-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="b5766-206">SUV di medie dimensioni</span><span class="sxs-lookup"><span data-stu-id="b5766-206">Medium SUV</span></span> |
| <span data-ttu-id="b5766-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="b5766-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="b5766-208">Station Wagon</span><span class="sxs-lookup"><span data-stu-id="b5766-208">Station Wagon</span></span> |
| <span data-ttu-id="b5766-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="b5766-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="b5766-210">SUV di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="b5766-210">Large SUV</span></span> |
| <span data-ttu-id="b5766-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="b5766-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="b5766-212">SUV di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="b5766-212">Large SUV</span></span> |
| <span data-ttu-id="b5766-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="b5766-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="b5766-214">Coupé</span><span class="sxs-lookup"><span data-stu-id="b5766-214">Coupe</span></span> |
| <span data-ttu-id="b5766-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="b5766-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="b5766-216">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-216">Sedan</span></span> |
| <span data-ttu-id="b5766-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="b5766-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="b5766-218">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-218">Hybrid</span></span> |
| <span data-ttu-id="b5766-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="b5766-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="b5766-220">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-220">Family Saloon</span></span> |
| <span data-ttu-id="b5766-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="b5766-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="b5766-222">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-222">Sedan</span></span> |
| <span data-ttu-id="b5766-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="b5766-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="b5766-224">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-224">Hybrid</span></span> |
| <span data-ttu-id="b5766-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="b5766-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="b5766-226">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-226">Family Saloon</span></span> |
| <span data-ttu-id="b5766-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="b5766-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="b5766-228">Berlina</span><span class="sxs-lookup"><span data-stu-id="b5766-228">Sedan</span></span> |
| <span data-ttu-id="b5766-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="b5766-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="b5766-230">Ibrido</span><span class="sxs-lookup"><span data-stu-id="b5766-230">Hybrid</span></span> |
| <span data-ttu-id="b5766-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="b5766-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="b5766-232">Berlina familiare</span><span class="sxs-lookup"><span data-stu-id="b5766-232">Family Saloon</span></span> |
| <span data-ttu-id="b5766-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="b5766-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="b5766-234">Decappottabile</span><span class="sxs-lookup"><span data-stu-id="b5766-234">Convertible</span></span> |
| <span data-ttu-id="b5766-235">…….</span><span class="sxs-lookup"><span data-stu-id="b5766-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="b5766-236">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="b5766-236">References</span></span>
[<span data-ttu-id="b5766-237">Soluzione Vehicle Telematics Simulator di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5766-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="b5766-238">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="b5766-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="b5766-239">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="b5766-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="b5766-240">Ingestion</span><span class="sxs-lookup"><span data-stu-id="b5766-240">Ingestion</span></span>
<span data-ttu-id="b5766-241">Vengono sfruttate combinazioni di Hub eventi di Azure, Analisi di flusso di Azure e Azure Data Factory per inserire i segnali del veicolo, gli eventi di diagnostica e le analisi in tempo reale e batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="b5766-242">Tutti questi componenti vengono creati e configurati durante la distribuzione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="b5766-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="b5766-243">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b5766-243">Real-time analysis</span></span>
<span data-ttu-id="b5766-244">Gli eventi generati dal simulatore di dati telematici relativi al veicolo vengono pubblicati nell'Hub eventi usando l'SDK di Hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="b5766-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="b5766-245">Il processo di Analisi di flusso inserisce gli eventi dall'hub eventi ed elabora i dati in tempo reale per analizzare l'integrità del veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Dashboard di Hub eventi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="b5766-247">*Figura 4: Dashboard di Hub eventi*</span><span class="sxs-lookup"><span data-stu-id="b5766-247">*Figure 4 - Event Hub dashboard*</span></span>

![Elaborazione dei dati da parte del processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="b5766-249">*Figura 5: Elaborazione dei dati da parte del processo di Analisi di flusso*</span><span class="sxs-lookup"><span data-stu-id="b5766-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="b5766-250">Il processo di Analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="b5766-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="b5766-251">Inserisce i dati dall'hub eventi</span><span class="sxs-lookup"><span data-stu-id="b5766-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="b5766-252">Esegue un join con i dati di riferimento per eseguire il mapping del numero identificativo del veicolo al modello corrispondente</span><span class="sxs-lookup"><span data-stu-id="b5766-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="b5766-253">Li rende persistenti nell'archivio BLOB di Azure per l'analisi in batch avanzata</span><span class="sxs-lookup"><span data-stu-id="b5766-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="b5766-254">La query di Analisi di flusso riportata di seguito viene usata per rendere persistenti i dati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5766-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Query del processo di Analisi di flusso per l'inserimento di dati](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="b5766-256">*Figura 6: Query del processo di Analisi di flusso per l'inserimento di dati*</span><span class="sxs-lookup"><span data-stu-id="b5766-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="b5766-257">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="b5766-257">Batch analysis</span></span>
<span data-ttu-id="b5766-258">Viene anche generato un volume aggiuntivo di set di dati di diagnostica e segnali del veicolo simulati per rendere più completa l'analisi batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="b5766-259">Questo è necessario per garantire un volume di dati rappresentativo per l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="b5766-260">A questo scopo, viene usata una pipeline denominata "PrepareSampleDataPipeline" nel flusso di lavoro di Azure Data Factory per generare una simulazione di segnali e un set di dati di diagnostica del veicolo equivalenti a un anno.</span><span class="sxs-lookup"><span data-stu-id="b5766-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="b5766-261">Fare clic su [Attività personalizzata di Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) per scaricare la soluzione di Visual Studio per l'attività .Net personalizzata di Data factory ed eseguire le personalizzazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="b5766-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="b5766-263">*Figura 7: Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch*</span><span class="sxs-lookup"><span data-stu-id="b5766-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="b5766-264">La pipeline è costituita da un'attività .NET personalizzata di Azure Data Factory, illustrata qui:</span><span class="sxs-lookup"><span data-stu-id="b5766-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Attività PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="b5766-266">*Figure 8: PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="b5766-267">Dopo aver eseguito correttamente la pipeline e aver contrassegnato come "Ready" il set di dati "RawCarEventsTable", viene generato l'equivalente di un anno di dati di diagnostica e segnali del veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="b5766-268">La cartella e il file seguenti creati nell'account di archiviazione vengono visualizzati all'interno del contenitore "connectedcar":</span><span class="sxs-lookup"><span data-stu-id="b5766-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![Output di PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="b5766-270">*Figura 9: Output di PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="b5766-271">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="b5766-271">References</span></span>
[<span data-ttu-id="b5766-272">Azure Event Hub SDK per l'inserimento di flussi</span><span class="sxs-lookup"><span data-stu-id="b5766-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="b5766-273">[Funzionalità di spostamento dei dati di Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Attività DotNet di Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="b5766-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="b5766-274">Soluzione di Visual Studio per l'attività DotNet di Data factory di Azure per la preparazione dei dati di esempio</span><span class="sxs-lookup"><span data-stu-id="b5766-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="b5766-275">Partizionare il set di dati</span><span class="sxs-lookup"><span data-stu-id="b5766-275">Partition the dataset</span></span>
<span data-ttu-id="b5766-276">Il set di dati di diagnostica e segnali del veicolo semistrutturati non elaborati viene partizionato durante la fase di preparazione dei dati in un formato ANNO/MESE.</span><span class="sxs-lookup"><span data-stu-id="b5766-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="b5766-277">Questo partizionamento favorisce l'esecuzione di query più efficienti e un'archiviazione scalabile a lungo termine abilitando il failover da un account BLOB a quello successivo quando il primo account si riempie.</span><span class="sxs-lookup"><span data-stu-id="b5766-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="b5766-278">Questo passaggio della soluzione è applicabile solo all'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="b5766-279">Gestione dati di input e di output:</span><span class="sxs-lookup"><span data-stu-id="b5766-279">Input and output data data management:</span></span>

* <span data-ttu-id="b5766-280">I **dati di output** (con etichetta *PartitionedCarEventsTable*) devono essere mantenuti per un lungo periodo di tempo nella forma di base "meno elaborata" dei dati nel "Data Lake" del cliente.</span><span class="sxs-lookup"><span data-stu-id="b5766-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="b5766-281">I **dati di input** per questa pipeline vengono in genere eliminati perché i dati di output hanno la massima fedeltà all'input, sono semplicemente archiviati (partizionati) meglio per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="b5766-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Flusso di lavoro PartitionCarEvents](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="b5766-283">*Figura 10: Flusso di lavoro PartitionCarEvents*</span><span class="sxs-lookup"><span data-stu-id="b5766-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="b5766-284">I dati non elaborati vengono partizionati usando un'attività Hive HDInsight in "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="b5766-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="b5766-285">I dati di esempio generati nel passaggio 1 per un anno vengono partizionati per ANNO/MESE.</span><span class="sxs-lookup"><span data-stu-id="b5766-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="b5766-286">Le partizioni vengono usate per generare i dati di diagnostica e segnali del veicolo per ogni mese (12 partizioni in totale) di un anno.</span><span class="sxs-lookup"><span data-stu-id="b5766-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Attività PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="b5766-288">*Figura 11: PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="b5766-289">***Script Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="b5766-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="b5766-290">Lo script Hive seguente, denominato "partitioncarevents.hql", è usato per il partizionamento e si trova nella cartella "\demo\src\connectedcar\scripts" del file ZIP scaricato.</span><span class="sxs-lookup"><span data-stu-id="b5766-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="b5766-291">Dopo la corretta esecuzione della pipeline, vengono visualizzate le partizioni seguenti generate nell'account di archiviazione nel contenitore "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="b5766-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Output partizionato](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="b5766-293">*Figura 12: Output partizionato*</span><span class="sxs-lookup"><span data-stu-id="b5766-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="b5766-294">A questo punto, i dati sono ottimizzati, più gestibili e pronti per un'ulteriore elaborazione che permette di ottenere informazioni dettagliate sul batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="b5766-295">Analisi dei dati</span><span class="sxs-lookup"><span data-stu-id="b5766-295">Data Analysis</span></span>
<span data-ttu-id="b5766-296">In questa sezione viene illustrato come combinare Analisi di flusso di Azure, Azure Machine Learning, Azure Data Factory e Azure HDInsight per un'analisi avanzata dell'integrità del veicolo e delle abitudini di guida.</span><span class="sxs-lookup"><span data-stu-id="b5766-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="b5766-297">Sono presenti tre sottosezioni:</span><span class="sxs-lookup"><span data-stu-id="b5766-297">There are three subsections here:</span></span>

1. <span data-ttu-id="b5766-298">**Machine Learning**: questa sottosezione contiene informazioni sull'esperimento di rilevamento anomalie usato nella soluzione per eseguire una stima dei veicoli che richiedono interventi di manutenzione e dei veicoli da richiamare a causa di problemi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b5766-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="b5766-299">**Analisi in tempo reale**: questa sottosezione contiene informazioni riguardanti l'analisi in tempo reale con il linguaggio di query di Analisi di flusso e la messa in funzione dell'esperimento di Machine Learning in tempo reale con un'applicazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b5766-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="b5766-300">**Analisi batch**: questa sottosezione contiene informazioni sulla trasformazione e l'elaborazione dei dati batch con Azure HDInsight e Azure Machine Learning messi in funzione da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5766-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="b5766-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b5766-301">Machine Learning</span></span>
<span data-ttu-id="b5766-302">L'obiettivo è eseguire una stima dei veicoli che richiedono interventi di manutenzione e dei veicoli da richiamare in base a determinate statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="b5766-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="b5766-303">Si parte dai presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5766-303">We make the following assumptions</span></span>

* <span data-ttu-id="b5766-304">Se una delle tre condizioni seguenti è vera, il veicolo richiede un **intervento di manutenzione**:</span><span class="sxs-lookup"><span data-stu-id="b5766-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="b5766-305">La pressione degli pneumatici è bassa</span><span class="sxs-lookup"><span data-stu-id="b5766-305">Tire pressure is low</span></span>
  * <span data-ttu-id="b5766-306">Il livello di olio del motore è basso</span><span class="sxs-lookup"><span data-stu-id="b5766-306">Engine oil level is low</span></span>
  * <span data-ttu-id="b5766-307">La temperatura del motore è elevata</span><span class="sxs-lookup"><span data-stu-id="b5766-307">Engine temperature is high</span></span>
* <span data-ttu-id="b5766-308">Se una delle condizioni seguenti è vera, il veicolo può avere un **problema di sicurezza** e può essere necessario il **richiamo**:</span><span class="sxs-lookup"><span data-stu-id="b5766-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="b5766-309">La temperatura del motore è elevata, ma la temperatura esterna è bassa</span><span class="sxs-lookup"><span data-stu-id="b5766-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="b5766-310">La temperatura del motore è bassa, ma la temperatura esterna è elevata</span><span class="sxs-lookup"><span data-stu-id="b5766-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="b5766-311">In base ai requisiti precedenti, sono stati creati due modelli separati per il rilevamento delle anomalie, uno per gli interventi di manutenzione sul veicolo e uno per il richiamo del veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="b5766-312">In entrambi i modelli l'algoritmo di analisi in componenti principali (PCA) predefinito viene usato per il rilevamento anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="b5766-313">**Modello di rilevamento per la manutenzione**</span><span class="sxs-lookup"><span data-stu-id="b5766-313">**Maintenance detection model**</span></span>

<span data-ttu-id="b5766-314">Se uno dei tre indicatori (pressione degli pneumatici, olio del motore o temperatura del motore) soddisfa la condizione corrispondente, il modello di rilevamento per la manutenzione segnala un'anomalia.</span><span class="sxs-lookup"><span data-stu-id="b5766-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="b5766-315">Di conseguenza, nella compilazione del modello è sufficiente prendere in considerazione queste tre variabili.</span><span class="sxs-lookup"><span data-stu-id="b5766-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="b5766-316">Nell'esperimento in Azure Machine Learning viene usato prima un modulo **Seleziona colonne in set di dati** per estrarre queste tre variabili.</span><span class="sxs-lookup"><span data-stu-id="b5766-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="b5766-317">Viene quindi usato il modulo di rilevamento delle anomalie basato su PCA per compilare il modello di rilevamento delle anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="b5766-318">L'analisi in componenti principali (PCA) è una tecnica consolidata in Machine Learning che può essere applicata alla selezione di funzionalità, alla classificazione e al rilevamento di anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="b5766-319">Converte un set di casi contenente variabili probabilmente correlate in un set di valori denominati componenti principali.</span><span class="sxs-lookup"><span data-stu-id="b5766-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="b5766-320">Lo scopo primario del modello basato su PCA è la proiezione dei dati in uno spazio dimensionale inferiore in modo che caratteristiche e anomalie siano identificabili più facilmente.</span><span class="sxs-lookup"><span data-stu-id="b5766-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="b5766-321">Per ogni nuovo input nel modello di rilevamento, il rilevatore di anomalie calcola prima di tutto la proiezione sugli autovettori e quindi l'errore di ricostruzione normalizzato.</span><span class="sxs-lookup"><span data-stu-id="b5766-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="b5766-322">L'errore normalizzato costituisce il punteggio dell'anomalia.</span><span class="sxs-lookup"><span data-stu-id="b5766-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="b5766-323">A un punteggio maggiore corrisponde una maggiore anomalia dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b5766-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="b5766-324">Nel rilevamento per la manutenzione ogni record può essere considerato come un punto in uno spazio tridimensionale definito dalle coordinate pressione degli pneumatici, olio del motore e temperatura del motore.</span><span class="sxs-lookup"><span data-stu-id="b5766-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="b5766-325">Per acquisire queste anomalie, è possibile usare l'analisi in componenti principali per proiettare i dati originali nello spazio tridimensionale in uno spazio bidimensionale.</span><span class="sxs-lookup"><span data-stu-id="b5766-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="b5766-326">Il parametro relativo al numero di componenti da usare in PCA viene quindi impostato su 2.</span><span class="sxs-lookup"><span data-stu-id="b5766-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="b5766-327">Questo parametro ha un ruolo importante nell'applicazione del rilevamento delle anomalie basato su PCA.</span><span class="sxs-lookup"><span data-stu-id="b5766-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="b5766-328">Dopo aver eseguito la proiezione dei dati con l'analisi PCA, è possibile identificare più facilmente queste anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="b5766-329">**Modello di rilevamento anomalie per il richiamo** : in questo modello i moduli di rilevamento anomalie basati su PCA e Seleziona colonne in set di dati vengono usati in modo simile.</span><span class="sxs-lookup"><span data-stu-id="b5766-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="b5766-330">Nello specifico, vengono prima di tutto estratte le tre variabili (temperatura del motore, temperatura esterna e velocità) usando il modulo **Seleziona colonne in set di dati** .</span><span class="sxs-lookup"><span data-stu-id="b5766-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="b5766-331">Viene inclusa anche la variabile velocità perché la temperatura del motore è in genere correlata alla velocità.</span><span class="sxs-lookup"><span data-stu-id="b5766-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="b5766-332">Viene quindi usato il modulo di rilevamento delle anomalie basato su PCA per proiettare i dati da uno spazio tridimensionale a uno spazio bidimensionale.</span><span class="sxs-lookup"><span data-stu-id="b5766-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="b5766-333">I criteri di richiamo sono soddisfatti ed è quindi necessario richiamare il veicolo quando la temperatura del motore e quella esterna sono correlate negativamente.</span><span class="sxs-lookup"><span data-stu-id="b5766-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="b5766-334">Con un algoritmo di rilevamento delle anomalie basato su PCA è possibile acquisire le anomalie dopo l'analisi PCA.</span><span class="sxs-lookup"><span data-stu-id="b5766-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="b5766-335">Per il training del modello di rilevamento anomalie basato su PCA è sempre necessario usare come dati di input dati normali che non richiedano il richiamo o interventi di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="b5766-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="b5766-336">Nell'esperimento di assegnazione dei punteggi viene usato il modello di rilevamento anomalie sottoposto a training per rilevare se il veicolo richiede o meno la manutenzione o il richiamo.</span><span class="sxs-lookup"><span data-stu-id="b5766-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="b5766-337">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b5766-337">Real-time analysis</span></span>
<span data-ttu-id="b5766-338">La query SQL di Analisi di flusso seguente viene usata per ottenere la media di tutti i parametri importanti del veicolo, ad esempio la velocità, il livello di carburante, la temperatura del motore, la lettura del contachilometri, la pressione degli pneumatici, il livello di olio del motore e altri.</span><span class="sxs-lookup"><span data-stu-id="b5766-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="b5766-339">Le medie vengono usate per rilevare anomalie, emettere avvisi e determinare le condizioni generali di integrità dei veicoli usati in un'area specifica correlando tali informazioni a dati demografici.</span><span class="sxs-lookup"><span data-stu-id="b5766-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Query di Analisi di flusso per l'elaborazione in tempo reale](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="b5766-341">*Figura 13: Query di Analisi di flusso per l'elaborazione in tempo reale*</span><span class="sxs-lookup"><span data-stu-id="b5766-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="b5766-342">Tutte le medie vengono calcolate in una finestra a cascata di 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="b5766-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="b5766-343">In questo caso viene usata la finestra a cascata perché sono necessari intervalli di tempo contigui e non sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="b5766-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="b5766-344">Per altre informazioni sulle funzionalità di "windowing" in Analisi di flusso di Azure, fare clic su [Windowing (Analisi di flusso di Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5766-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="b5766-345">**Stima in tempo reale**</span><span class="sxs-lookup"><span data-stu-id="b5766-345">**Real-time prediction**</span></span>

<span data-ttu-id="b5766-346">Nella soluzione è inclusa un'applicazione per la messa in funzione del modello di Machine Learning in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b5766-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="b5766-347">L'applicazione, denominata "RealTimeDashboardApp" viene creata e configurata nell'ambito della distribuzione della soluzione</span><span class="sxs-lookup"><span data-stu-id="b5766-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="b5766-348">ed esegue le operazioni descritte di seguito:</span><span class="sxs-lookup"><span data-stu-id="b5766-348">The application performs the following:</span></span>

1. <span data-ttu-id="b5766-349">È in attesa di un'istanza di Hub eventi in cui Analisi di flusso pubblica gli eventi in un modello eseguito in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="b5766-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="b5766-350">![Query di Analisi di flusso per la pubblicazione di dati](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figura 14: Query di analisi di flusso per la pubblicazione di dati in un'istanza di Hub eventi di output*</span><span class="sxs-lookup"><span data-stu-id="b5766-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="b5766-351">Per ogni evento ricevuto dall'applicazione:</span><span class="sxs-lookup"><span data-stu-id="b5766-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="b5766-352">i dati vengono elaborati usando l'endpoint del servizio di richiesta-risposta (RRS) di Machine Learning per l'assegnazione dei punteggi,</span><span class="sxs-lookup"><span data-stu-id="b5766-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="b5766-353">l'endpoint RRS viene pubblicato automaticamente nell'ambito della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b5766-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="b5766-354">L'output RRS viene pubblicato in un set di dati di Power BI con le API push.</span><span class="sxs-lookup"><span data-stu-id="b5766-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="b5766-355">Questo modello è anche applicabile a scenari di integrazione di un'applicazione line-of-business con il flusso di analisi in tempo reale per avvisi, notifiche e messaggistica immediata.</span><span class="sxs-lookup"><span data-stu-id="b5766-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="b5766-356">Fare clic su [Download di RealtimeDashboardApp](http://go.microsoft.com/fwlink/?LinkId=717078) per scaricare la soluzione RealtimeDashboardApp di Visual Studio per le personalizzazioni.</span><span class="sxs-lookup"><span data-stu-id="b5766-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="b5766-357">**Per eseguire l'applicazione dashboard in tempo reale**</span><span class="sxs-lookup"><span data-stu-id="b5766-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="b5766-358">Estrarre e salvare in locale. ![Cartella RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figura 16: Cartella RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="b5766-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="b5766-359">Eseguire l'applicazione RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="b5766-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="b5766-360">Fornire credenziali di Power BI valide, accedere e fare clic su Accetta.</span><span class="sxs-lookup"><span data-stu-id="b5766-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Accesso dell'app dashboard in tempo reale a Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Accesso finale dell'app dashboard in tempo reale a Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="b5766-363">*Figura 17: Accesso a Power BI da RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="b5766-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="b5766-364">Per scaricare il set di dati di Power BI, eseguire RealtimeDashboardApp con il parametro "flushdata":</span><span class="sxs-lookup"><span data-stu-id="b5766-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="b5766-365">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="b5766-365">Batch analysis</span></span>
<span data-ttu-id="b5766-366">L'obiettivo di questa sezione è mostrare come Contoso Motors utilizza le funzionalità di calcolo di Azure per sfruttare i Big Data e ottenere informazioni dettagliate sugli stili di guida, sull'utilizzo e sull'integrità del veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="b5766-367">In questo modo è possibile:</span><span class="sxs-lookup"><span data-stu-id="b5766-367">This makes it possible to:</span></span>

* <span data-ttu-id="b5766-368">Migliorare l'esperienza del cliente e abbassare i costi fornendo informazioni dettagliate sulle abitudini e sui comportamenti di guida attenti ai consumi.</span><span class="sxs-lookup"><span data-stu-id="b5766-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="b5766-369">Acquisire informazioni sui clienti e sui relativi stili di guida per gestire il processo decisionale e fornire prodotti e servizi di altissimo livello.</span><span class="sxs-lookup"><span data-stu-id="b5766-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="b5766-370">In questa soluzione vengono esaminate le metriche seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5766-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="b5766-371">**Stile di guida aggressivo**: identifica la tendenza di modelli, località, condizioni di guida e periodo dell'anno per ottenere informazioni dettagliate sugli stili di guida aggressivi.</span><span class="sxs-lookup"><span data-stu-id="b5766-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="b5766-372">Contoso Motors può usare queste informazioni per creare campagne di marketing, nuove funzionalità personalizzate e assicurazioni basate sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b5766-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="b5766-373">**Stile di guida attento ai consumi**: identifica la tendenza dei modelli, località, condizioni di guida e periodo dell'anno per ottenere informazioni dettagliate sugli stili di guida attenti ai consumi.</span><span class="sxs-lookup"><span data-stu-id="b5766-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="b5766-374">Contoso Motors può usare queste informazioni per creare campagne di marketing, nuove funzionalità personalizzate e per segnalare al guidatore abitudini di guida attente ai consumi e all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b5766-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="b5766-375">**Previsioni di richiamo**: identifica i modelli che è necessario richiamare in base all'esperimento di Machine Learning per il rilevamento anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="b5766-376">Di seguito vengono esaminate le singole metriche nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="b5766-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="b5766-377">**Stile di guida aggressivo**</span><span class="sxs-lookup"><span data-stu-id="b5766-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="b5766-378">I segnali del veicolo e i dati di diagnostica partizionati vengono elaborati nella pipeline denominata "AggresiveDrivingPatternPipeline" che usa Hive per determinare modelli, località, veicoli, condizioni di guida e altri parametri che mostrano uno stile di guida aggressivo.</span><span class="sxs-lookup"><span data-stu-id="b5766-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="b5766-379">![Flusso di lavoro per lo stile di guida aggressivo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figura 18: Flusso di lavoro per lo stile di guida aggressivo*</span><span class="sxs-lookup"><span data-stu-id="b5766-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="b5766-380">***Query Hive per lo stile di guida aggressivo***</span><span class="sxs-lookup"><span data-stu-id="b5766-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="b5766-381">Lo script Hive denominato "aggresivedriving.hql" usato per l'analisi dello stile di guida aggressivo si trova nella cartella "\demo\src\connectedcar\scripts" del file ZIP scaricato.</span><span class="sxs-lookup"><span data-stu-id="b5766-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="b5766-382">Usa una combinazione di posizione del cambio, stato del pedale del freno e velocità del veicolo per rilevare un comportamento di guida spericolato/aggressivo in base allo stile di frenata ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="b5766-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="b5766-383">Dopo la corretta esecuzione della pipeline, vengono visualizzate le partizioni seguenti generate nell'account di archiviazione nel contenitore "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="b5766-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Output di AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="b5766-385">*Figura 19: Output di AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="b5766-386">**Stile di guida attento ai consumi**</span><span class="sxs-lookup"><span data-stu-id="b5766-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="b5766-387">I segnali del veicolo e i dati di diagnostica partizionati vengono elaborati nella pipeline denominata "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="b5766-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="b5766-388">Hive viene usato per determinare modelli, località, veicoli, condizioni di guida e così via, che mostrano uno stile di guida attento ai consumi.</span><span class="sxs-lookup"><span data-stu-id="b5766-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Stile di guida attento ai consumi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="b5766-390">*Figura 20: Flusso di lavoro per lo stile di guida attento ai consumi*</span><span class="sxs-lookup"><span data-stu-id="b5766-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="b5766-391">***Query Hive per lo stile di guida attento ai consumi***</span><span class="sxs-lookup"><span data-stu-id="b5766-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="b5766-392">Lo script Hive denominato "fuelefficientdriving.hql" usato per l'analisi dello stile di guida attento ai consumi si trova nella cartella "\demo\src\connectedcar\scripts" del file ZIP scaricato.</span><span class="sxs-lookup"><span data-stu-id="b5766-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="b5766-393">Usa una combinazione di posizione del cambio, stato del pedale del freno, velocità del veicolo e posizione del pedale dell'acceleratore per rilevare un comportamento di guida attento ai consumi in base allo stile di accelerazione e frenata e in base alla velocità.</span><span class="sxs-lookup"><span data-stu-id="b5766-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="b5766-394">Dopo la corretta esecuzione della pipeline, vengono visualizzate le partizioni seguenti generate nell'account di archiviazione nel contenitore "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="b5766-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Output di FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="b5766-396">*Figura 21: Output di FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="b5766-397">**Previsioni di richiamo**</span><span class="sxs-lookup"><span data-stu-id="b5766-397">**Recall Predictions**</span></span>

<span data-ttu-id="b5766-398">L'esperimento di Machine Learning è stato sottoposto a provisioning e pubblicato come servizio Web nell'ambito della distribuzione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="b5766-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="b5766-399">L'endpoint di assegnazione punteggio batch viene usato all'interno di questo flusso di lavoro, registrato come servizio collegato di Data factory e messo in funzione con l'attività di assegnazione punteggio batch di Data factory.</span><span class="sxs-lookup"><span data-stu-id="b5766-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Endpoint di Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="b5766-401">*Figura 22: Endpoint di Machine Learning registrato come servizio collegato in Data factory*</span><span class="sxs-lookup"><span data-stu-id="b5766-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="b5766-402">Il servizio collegato registrato viene usato in DetectAnomalyPipeline per assegnare un punteggio ai dati con il modello di rilevamento delle anomalie.</span><span class="sxs-lookup"><span data-stu-id="b5766-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Attività di assegnazione punteggio batch di Machine Learning in Data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="b5766-404">*Figura 23: Attività di assegnazione punteggio batch di Azure Machine Learning in Data factory*</span><span class="sxs-lookup"><span data-stu-id="b5766-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="b5766-405">Alcuni dei passaggi eseguiti in questa pipeline per la preparazione dei dati ne consentono l'uso con il servizio Web di assegnazione punteggio batch.</span><span class="sxs-lookup"><span data-stu-id="b5766-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline per la stima dei veicoli da richiamare](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="b5766-407">*Figura 24: DetectAnomalyPipeline per la stima dei veicoli da richiamare*</span><span class="sxs-lookup"><span data-stu-id="b5766-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="b5766-408">***Query Hive per il rilevamento delle anomalie***</span><span class="sxs-lookup"><span data-stu-id="b5766-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="b5766-409">Dopo aver completato l'assegnazione dei punteggi, viene usata un'attività HDInsight per elaborare e aggregare i dati categorizzati come anomalie dal modello con un punteggio minimo di probabilità di 0,60.</span><span class="sxs-lookup"><span data-stu-id="b5766-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="b5766-410">Dopo la corretta esecuzione della pipeline, vengono visualizzate le partizioni seguenti generate nell'account di archiviazione nel contenitore "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="b5766-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Output di DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="b5766-412">*Figura 25: Output di DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="b5766-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="b5766-413">Pubblica</span><span class="sxs-lookup"><span data-stu-id="b5766-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="b5766-414">Analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b5766-414">Real-time analysis</span></span>
<span data-ttu-id="b5766-415">Una delle query del processo di Analisi di flusso pubblica gli eventi in un'istanza di Hub eventi di output.</span><span class="sxs-lookup"><span data-stu-id="b5766-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Il processo di Analisi di flusso esegue la pubblicazione in un'istanza di Hub eventi di output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="b5766-417">*Figura 26: Il processo di Analisi di flusso esegue la pubblicazione in un'istanza di Hub eventi di output*</span><span class="sxs-lookup"><span data-stu-id="b5766-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Query di Analisi di flusso per la pubblicazione in un'istanza di Hub eventi di output](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="b5766-419">*Figura 27: Query di Analisi di flusso per la pubblicazione in un'istanza di Hub eventi di output*</span><span class="sxs-lookup"><span data-stu-id="b5766-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="b5766-420">Questo flusso di eventi viene utilizzato dall'applicazione RealTimeDashboardApp inclusa nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="b5766-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="b5766-421">L'applicazione sfrutta il servizio Web di richiesta-risposta di Machine Learning per l'assegnazione dei punteggi in tempo reale e pubblica i dati risultanti in un set di dati di Power BI per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b5766-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="b5766-422">Analisi batch</span><span class="sxs-lookup"><span data-stu-id="b5766-422">Batch analysis</span></span>
<span data-ttu-id="b5766-423">I risultati dell'elaborazione batch e in tempo reale vengono pubblicati nelle tabelle di database SQL di Azure per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b5766-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="b5766-424">Il server SQL Azure, il database e le tabelle vengono creati automaticamente con lo script di installazione.</span><span class="sxs-lookup"><span data-stu-id="b5766-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Copia dei risultati dell'elaborazione batch nel flusso di lavoro di data mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="b5766-426">*Figura 28: Copia dei risultati dell'elaborazione batch nel flusso di lavoro di data mart*</span><span class="sxs-lookup"><span data-stu-id="b5766-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Il processo di Analisi di flusso esegue la pubblicazione in data mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="b5766-428">*Figura 29: Il processo di Analisi di flusso esegue la pubblicazione in data mart*</span><span class="sxs-lookup"><span data-stu-id="b5766-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Impostazione di data mart nel processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="b5766-430">*Figura 30: Impostazione di data mart nel processo di Analisi di flusso*</span><span class="sxs-lookup"><span data-stu-id="b5766-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="b5766-431">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b5766-431">Consume</span></span>
<span data-ttu-id="b5766-432">Power BI offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittive.</span><span class="sxs-lookup"><span data-stu-id="b5766-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="b5766-433">Fare clic qui per informazioni dettagliate su come configurare i report e il dashboard di Power BI.</span><span class="sxs-lookup"><span data-stu-id="b5766-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="b5766-434">L'aspetto finale del dashboard è questo:</span><span class="sxs-lookup"><span data-stu-id="b5766-434">The final dashboard looks like this:</span></span>

![Dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="b5766-436">*Figura 31: Dashboard di Power BI*</span><span class="sxs-lookup"><span data-stu-id="b5766-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="b5766-437">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b5766-437">Summary</span></span>
<span data-ttu-id="b5766-438">Questo documento contiene un'analisi dettagliata e approfondita della soluzione di analisi dei dati di telemetria del veicolo.</span><span class="sxs-lookup"><span data-stu-id="b5766-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="b5766-439">Questa presenta un modello di architettura lambda per l'analisi batch e in tempo reale completa di stime e azioni.</span><span class="sxs-lookup"><span data-stu-id="b5766-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="b5766-440">Il modello si applica a una vasta gamma di casi d'uso che richiedono l'analisi del percorso critico (in tempo reale) e di quello non critico (batch).</span><span class="sxs-lookup"><span data-stu-id="b5766-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

