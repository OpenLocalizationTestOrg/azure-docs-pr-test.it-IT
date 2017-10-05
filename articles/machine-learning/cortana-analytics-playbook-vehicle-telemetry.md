---
title: "Previsione dell'integrità dei veicoli e abitudini di guida - Azure | Documentazione Microsoft"
description: "Usare le funzionalità di Cortana Intelligence per ottenere informazioni dettagliate predittive e in tempo reale sullo stato di integrità del veicolo e sulle abitudini di guida."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="b07a5-103">Studio della soluzione di analisi dei dati di telemetria del veicolo</span><span class="sxs-lookup"><span data-stu-id="b07a5-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="b07a5-104">Questo **menu** contiene i collegamenti alle sezioni dello studio.</span><span class="sxs-lookup"><span data-stu-id="b07a5-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="b07a5-105">Overview</span><span class="sxs-lookup"><span data-stu-id="b07a5-105">Overview</span></span>
<span data-ttu-id="b07a5-106">I super computer sono usciti dai laboratori e ora sono parcheggiati nel nostro garage!</span><span class="sxs-lookup"><span data-stu-id="b07a5-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="b07a5-107">Questi automobili all'avanguardia contengono una miriade di sensori, fornendo agli utenti la possibilità di tenere traccia di milioni di eventi al secondo e monitorarli.</span><span class="sxs-lookup"><span data-stu-id="b07a5-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="b07a5-108">Si prevede che entro il 2020 la maggior parte di queste automobili sarà connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="b07a5-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="b07a5-109">Sarà così possibile a questa grande quantità di dati per offrire maggiore sicurezza, affidabilità e una migliore esperienza di guida.</span><span class="sxs-lookup"><span data-stu-id="b07a5-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="b07a5-110">Grazie a Cortana Intelligence, Microsoft ha trasformato questo sogno in realtà.</span><span class="sxs-lookup"><span data-stu-id="b07a5-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="b07a5-111">Microsoft Cortana Intelligence è una famiglia di prodotti completamente gestita di Big Data e analisi avanzata che consente di trasformare i dati in azioni intelligenti.</span><span class="sxs-lookup"><span data-stu-id="b07a5-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="b07a5-112">In questo articolo verrà presentato il modello di soluzione per l'analisi dei dati di telemetria del veicolo di Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="b07a5-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="b07a5-113">Questa soluzione mostra come le concessionarie, i produttori di automobili e le compagnie assicurative possono usare le funzionalità di Cortana Intelligence per ottenere informazioni predittive in tempo reale sullo stato di integrità dei veicoli e sulle abitudini di guida.</span><span class="sxs-lookup"><span data-stu-id="b07a5-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="b07a5-114">La soluzione viene implementata come un [modello di architettura lambda](https://en.wikipedia.org/wiki/Lambda_architecture) che mostra tutto il potenziale della piattaforma Cortana Intelligence per l'elaborazione in tempo reale e batch.</span><span class="sxs-lookup"><span data-stu-id="b07a5-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="b07a5-115">La soluzione:</span><span class="sxs-lookup"><span data-stu-id="b07a5-115">The solution:</span></span> 

* <span data-ttu-id="b07a5-116">fornisce un simulatore di dati telematici del veicolo</span><span class="sxs-lookup"><span data-stu-id="b07a5-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="b07a5-117">usa Hub eventi per l'inserimento di milioni di eventi di telemetria del veicolo simulato in Azure</span><span class="sxs-lookup"><span data-stu-id="b07a5-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="b07a5-118">usa analisi di flusso per ottenere informazioni in tempo reale sull'integrità del veicolo</span><span class="sxs-lookup"><span data-stu-id="b07a5-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="b07a5-119">rende persistenti i dati nell'archiviazione a lungo termine per un'analisi batch avanzata.</span><span class="sxs-lookup"><span data-stu-id="b07a5-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="b07a5-120">sfrutta il Machine Learning per il rilevamento di anomalie in tempo reale e l'elaborazione batch per ottenere informazioni predittive.</span><span class="sxs-lookup"><span data-stu-id="b07a5-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="b07a5-121">sfrutta HDInsight per trasformare i dati in scala e Data Factory per gestire l'orchestrazione, la pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="b07a5-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="b07a5-122">offre alla soluzione un dashboard completo per la visualizzazione di analisi predittive e di dati in tempo reale tramite Power BI</span><span class="sxs-lookup"><span data-stu-id="b07a5-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="b07a5-123">Architettura</span><span class="sxs-lookup"><span data-stu-id="b07a5-123">Architecture</span></span>
<span data-ttu-id="b07a5-124">![Diagramma dell'architettura della soluzione](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 - Architettura della soluzione di analisi dei dati di telemetria del veicolo*</span><span class="sxs-lookup"><span data-stu-id="b07a5-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="b07a5-125">Questa soluzione include i seguenti **componenti di Cortana Intelligence** e ne illustra l'integrazione end-to-end:</span><span class="sxs-lookup"><span data-stu-id="b07a5-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="b07a5-126">**Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="b07a5-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="b07a5-127">**Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.</span><span class="sxs-lookup"><span data-stu-id="b07a5-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="b07a5-128">**Machine Learning** per il rilevamento di anomalie in tempo reale e l'elaborazione batch per ottenere informazioni predittive.</span><span class="sxs-lookup"><span data-stu-id="b07a5-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="b07a5-129">**HDInsight** per trasformare i dati su larga scala</span><span class="sxs-lookup"><span data-stu-id="b07a5-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="b07a5-130">**Data Factory** gestisce l'orchestrazione, la pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="b07a5-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="b07a5-131">**Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="b07a5-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="b07a5-132">La soluzione accede a due **origini dati**diverse:</span><span class="sxs-lookup"><span data-stu-id="b07a5-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="b07a5-133">**Segnali e diagnostica simulati del veicolo**: un simulatore di dati telematici del veicolo genera informazioni di diagnostica e segnali che corrispondono allo stato del veicolo e al modello di guida in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="b07a5-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="b07a5-134">**Catalogo del veicolo**: un set di dati di riferimento contenente il VIN (Vehicle Identification Number, numero di identificazione del veicolo) per il mapping del modello</span><span class="sxs-lookup"><span data-stu-id="b07a5-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

