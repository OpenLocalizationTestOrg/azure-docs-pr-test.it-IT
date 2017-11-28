---
title: "integrità veicolo aaaPredict e abitudini - Azure | Documenti Microsoft"
description: "Utilizzare funzionalità di hello di insights di predittiva e in tempo reale toogain Intelligence Cortana sull'integrità del veicolo e abitudini di Guida."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="1bb34-103">Studio della soluzione di analisi dei dati di telemetria del veicolo</span><span class="sxs-lookup"><span data-stu-id="1bb34-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="1bb34-104">Questo **menu** capitoli toohello questo playbook è collegato.</span><span class="sxs-lookup"><span data-stu-id="1bb34-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="1bb34-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1bb34-105">Overview</span></span>
<span data-ttu-id="1bb34-106">Computer con privilegi avanzati sono stati spostati all'esterno ambiente lab hello e sono ora disattivato nel nostro garage!</span><span class="sxs-lookup"><span data-stu-id="1bb34-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="1bb34-107">Questi automobili all'avanguardia contengono innumerevoli sensori, in modo che possano tootrack possibilità hello e monitorare milioni di eventi al secondo.</span><span class="sxs-lookup"><span data-stu-id="1bb34-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="1bb34-108">È previsto che il 2020, la maggior parte di questi automobili saranno stati connesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="1bb34-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="1bb34-109">Si supponga toccato in queste numerose maggiore sicurezza dei dati tooprovide, affidabilità e un'esperienza migliore determinante!</span><span class="sxs-lookup"><span data-stu-id="1bb34-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="1bb34-110">Grazie a Cortana Intelligence, Microsoft ha trasformato questo sogno in realtà.</span><span class="sxs-lookup"><span data-stu-id="1bb34-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="1bb34-111">Microsoft Business Intelligence di Cortana è di tipo data grande completamente gestito e avanzate suite analitica che consente di tootransform i dati in azione intelligente.</span><span class="sxs-lookup"><span data-stu-id="1bb34-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="1bb34-112">Vogliamo toointroduce si toohello del modello di soluzione Analitica Cortana Intelligence veicolo telemetria.</span><span class="sxs-lookup"><span data-stu-id="1bb34-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="1bb34-113">Questa soluzione illustra come settore automobilistico trae i produttori di automobili e società di assicurazioni può utilizzare le funzionalità di hello di Cortana Intelligence toogain in tempo reale e abitudini predittive informazioni essenziali quanto a integrità veicolo e la Guida.</span><span class="sxs-lookup"><span data-stu-id="1bb34-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="1bb34-114">soluzione Hello viene implementato come un [lambda (modello) architettura](https://en.wikipedia.org/wiki/Lambda_architecture) potenzialità hello della piattaforma di Business Intelligence di Cortana hello per visualizzare in tempo reale e l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="1bb34-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="1bb34-115">soluzione Hello:</span><span class="sxs-lookup"><span data-stu-id="1bb34-115">hello solution:</span></span> 

* <span data-ttu-id="1bb34-116">fornisce un simulatore di dati telematici del veicolo</span><span class="sxs-lookup"><span data-stu-id="1bb34-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="1bb34-117">usa Hub eventi per l'inserimento di milioni di eventi di telemetria del veicolo simulato in Azure</span><span class="sxs-lookup"><span data-stu-id="1bb34-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="1bb34-118">Usa informazioni in tempo reale di flusso Analitica toogain sull'integrità del veicolo</span><span class="sxs-lookup"><span data-stu-id="1bb34-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="1bb34-119">mantiene i dati di hello nell'archiviazione a lungo termine per analitica batch più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="1bb34-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="1bb34-120">sfrutta Machine Learning per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="1bb34-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="1bb34-121">utilizza dati tootransform HDInsight alla scala e orchestrazione toohandle Data Factory, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello</span><span class="sxs-lookup"><span data-stu-id="1bb34-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="1bb34-122">offre alla soluzione un dashboard completo per la visualizzazione di analisi predittive e di dati in tempo reale tramite Power BI</span><span class="sxs-lookup"><span data-stu-id="1bb34-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="1bb34-123">Architettura</span><span class="sxs-lookup"><span data-stu-id="1bb34-123">Architecture</span></span>
<span data-ttu-id="1bb34-124">![Diagramma dell'architettura della soluzione](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 - Architettura della soluzione di analisi dei dati di telemetria del veicolo*</span><span class="sxs-lookup"><span data-stu-id="1bb34-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="1bb34-125">Questa soluzione include seguente hello **componenti di Business Intelligence di Cortana** e viene illustrata la loro integrazione tooend fine:</span><span class="sxs-lookup"><span data-stu-id="1bb34-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="1bb34-126">**Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb34-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="1bb34-127">**Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.</span><span class="sxs-lookup"><span data-stu-id="1bb34-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="1bb34-128">**Machine Learning** per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="1bb34-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="1bb34-129">**HDInsight** tootransform sfruttate dati su larga scala</span><span class="sxs-lookup"><span data-stu-id="1bb34-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="1bb34-130">**Data Factory** gestisce l'orchestrazione, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello.</span><span class="sxs-lookup"><span data-stu-id="1bb34-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="1bb34-131">**Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="1bb34-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="1bb34-132">La soluzione accede a due **origini dati**diverse:</span><span class="sxs-lookup"><span data-stu-id="1bb34-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="1bb34-133">**Simulate segnali veicolo e diagnostica**: un simulatore telematiche veicolo genera informazioni di diagnostica e segnali corrispondenti stato toohello del veicolo hello e hello gestiscono modello in un determinato punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="1bb34-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="1bb34-134">**Catalogo veicolo**: un set di dati di riferimento contenente un mapping toomodel VPN.</span><span class="sxs-lookup"><span data-stu-id="1bb34-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

