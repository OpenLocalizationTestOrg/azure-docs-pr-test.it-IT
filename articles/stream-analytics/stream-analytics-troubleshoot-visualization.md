---
title: aaaVisualize e risolvere i problemi relativi a processi di flusso Analitica | Documenti Microsoft
description: "Informazioni su come un processo di flusso Analitica toovisualize della pipeline per la risoluzione dei problemi mediante funzionalità diagramma di diagnostica hello di Self-Service."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualizzare e risolvere i problemi di Analisi di flusso
Nel flusso Analitica, come con altre tecnologie basate su cloud, risoluzione dei problemi è talvolta toolook necessari in un processo perché non produrre output previsto hello (o qualsiasi output a tale scopo). A tal fine, Analitica di flusso fornisce le funzionalità di hello per la visualizzazione di un processo di streaming. È inoltre utile come strumento di modellazione e ha vantaggio hello per quelle che richiedono la documentazione del proprio lavoro.

In visualizzazione hello input hello pannello sono visibili e query hello in esecuzione e quindi tutti gli output di hello configurato. Problemi di connettività o di configurazione possono diventare più evidenti e può anche essere utile toosee una rappresentazione visiva della configurazione.

## <a name="using-hello-diagnosis-diagram-tool"></a>Lo strumento hello diagnosi diagramma
questo visualizzatore, è sufficiente fare clic sul pulsante "Diagramma diagnosi" di hello tooaccess hello blade "Impostazioni" di hello del processo di flusso Analitica hello.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Ogni input e output è codificato tramite colori tooindicate hello stato corrente del componente, come illustrato di seguito.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Con toolook query intermedi passaggi toounderstand hello dati flusso modelli all'interno di un processo di consenso dell'utente hello, strumento di visualizzazione hello fornisce una visualizzazione di riepilogo hello delle query hello in relativi passaggi dei componenti e di sequenza del flusso di hello. Facendo clic su ogni passaggio della query mostrerà la sezione corrispondente di hello in una query, la modifica di riquadro, come illustrato. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

