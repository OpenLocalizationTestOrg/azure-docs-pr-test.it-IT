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
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Studio della soluzione di analisi dei dati di telemetria del veicolo
Questo **menu** capitoli toohello questo playbook è collegato. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Panoramica
Computer con privilegi avanzati sono stati spostati all'esterno ambiente lab hello e sono ora disattivato nel nostro garage! Questi automobili all'avanguardia contengono innumerevoli sensori, in modo che possano tootrack possibilità hello e monitorare milioni di eventi al secondo. È previsto che il 2020, la maggior parte di questi automobili saranno stati connesso toohello Internet. Si supponga toccato in queste numerose maggiore sicurezza dei dati tooprovide, affidabilità e un'esperienza migliore determinante! Grazie a Cortana Intelligence, Microsoft ha trasformato questo sogno in realtà.

Microsoft Business Intelligence di Cortana è di tipo data grande completamente gestito e avanzate suite analitica che consente di tootransform i dati in azione intelligente. Vogliamo toointroduce si toohello del modello di soluzione Analitica Cortana Intelligence veicolo telemetria. Questa soluzione illustra come settore automobilistico trae i produttori di automobili e società di assicurazioni può utilizzare le funzionalità di hello di Cortana Intelligence toogain in tempo reale e abitudini predittive informazioni essenziali quanto a integrità veicolo e la Guida. 

soluzione Hello viene implementato come un [lambda (modello) architettura](https://en.wikipedia.org/wiki/Lambda_architecture) potenzialità hello della piattaforma di Business Intelligence di Cortana hello per visualizzare in tempo reale e l'elaborazione batch. soluzione Hello: 

* fornisce un simulatore di dati telematici del veicolo
* usa Hub eventi per l'inserimento di milioni di eventi di telemetria del veicolo simulato in Azure 
* Usa informazioni in tempo reale di flusso Analitica toogain sull'integrità del veicolo
* mantiene i dati di hello nell'archiviazione a lungo termine per analitica batch più dettagliato. 
* sfrutta Machine Learning per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.
* utilizza dati tootransform HDInsight alla scala e orchestrazione toohandle Data Factory, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello 
* offre alla soluzione un dashboard completo per la visualizzazione di analisi predittive e di dati in tempo reale tramite Power BI

## <a name="architecture"></a>Architettura
![Diagramma dell'architettura della soluzione](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 - Architettura della soluzione di analisi dei dati di telemetria del veicolo*

Questa soluzione include seguente hello **componenti di Business Intelligence di Cortana** e viene illustrata la loro integrazione tooend fine:

* **Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.
* **Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.
* **Machine Learning** per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.
* **HDInsight** tootransform sfruttate dati su larga scala
* **Data Factory** gestisce l'orchestrazione, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello.
* **Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.

La soluzione accede a due **origini dati**diverse: 

* **Simulate segnali veicolo e diagnostica**: un simulatore telematiche veicolo genera informazioni di diagnostica e segnali corrispondenti stato toohello del veicolo hello e hello gestiscono modello in un determinato punto nel tempo. 
* **Catalogo veicolo**: un set di dati di riferimento contenente un mapping toomodel VPN.

