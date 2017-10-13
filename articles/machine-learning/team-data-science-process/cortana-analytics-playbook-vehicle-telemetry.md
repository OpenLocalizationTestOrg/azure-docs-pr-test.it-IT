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
ms.openlocfilehash: af8b3d5bf891c93c30a05c5f02d86639a466dde5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Studio della soluzione di analisi dei dati di telemetria del veicolo
Questo **menu** contiene i collegamenti alle sezioni dello studio. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Overview
I super computer sono usciti dai laboratori e ora sono parcheggiati nel nostro garage! Questi automobili all'avanguardia contengono una miriade di sensori, fornendo agli utenti la possibilità di tenere traccia di milioni di eventi al secondo e monitorarli. Si prevede che entro il 2020 la maggior parte di queste automobili sarà connessa a Internet. Sarà così possibile a questa grande quantità di dati per offrire maggiore sicurezza, affidabilità e una migliore esperienza di guida. Grazie a Cortana Intelligence, Microsoft ha trasformato questo sogno in realtà.

Microsoft Cortana Intelligence è una famiglia di prodotti completamente gestita di Big Data e analisi avanzata che consente di trasformare i dati in azioni intelligenti. In questo articolo verrà presentato il modello di soluzione per l'analisi dei dati di telemetria del veicolo di Cortana Intelligence. Questa soluzione mostra come le concessionarie, i produttori di automobili e le compagnie assicurative possono usare le funzionalità di Cortana Intelligence per ottenere informazioni predittive in tempo reale sullo stato di integrità dei veicoli e sulle abitudini di guida. 

La soluzione viene implementata come un [modello di architettura lambda](https://en.wikipedia.org/wiki/Lambda_architecture) che mostra tutto il potenziale della piattaforma Cortana Intelligence per l'elaborazione in tempo reale e batch. La soluzione: 

* fornisce un simulatore di dati telematici del veicolo
* usa Hub eventi per l'inserimento di milioni di eventi di telemetria del veicolo simulato in Azure 
* usa analisi di flusso per ottenere informazioni in tempo reale sull'integrità del veicolo
* rende persistenti i dati nell'archiviazione a lungo termine per un'analisi batch avanzata. 
* sfrutta il Machine Learning per il rilevamento di anomalie in tempo reale e l'elaborazione batch per ottenere informazioni predittive.
* sfrutta HDInsight per trasformare i dati in scala e Data Factory per gestire l'orchestrazione, la pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch. 
* offre alla soluzione un dashboard completo per la visualizzazione di analisi predittive e di dati in tempo reale tramite Power BI

## <a name="architecture"></a>Architettura
![Diagramma dell'architettura della soluzione](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 - Architettura della soluzione di analisi dei dati di telemetria del veicolo*

Questa soluzione include i seguenti **componenti di Cortana Intelligence** e ne illustra l'integrazione end-to-end:

* **Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.
* **Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.
* **Machine Learning** per il rilevamento di anomalie in tempo reale e l'elaborazione batch per ottenere informazioni predittive.
* **HDInsight** per trasformare i dati su larga scala
* **Data Factory** gestisce l'orchestrazione, la pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch.
* **Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva.

La soluzione accede a due **origini dati**diverse: 

* **Segnali e diagnostica simulati del veicolo**: un simulatore di dati telematici del veicolo genera informazioni di diagnostica e segnali che corrispondono allo stato del veicolo e al modello di guida in un determinato momento. 
* **Catalogo del veicolo**: un set di dati di riferimento contenente il VIN (Vehicle Identification Number, numero di identificazione del veicolo) per il mapping del modello

