---
title: Visualizzare e risolvere i problemi dei processi dell'analisi di flusso | Microsoft Docs
description: "Informazioni su come visualizzare una pipeline dei processi di Analisi di flusso per risolvere i problemi in modo autonomo mediante la funzionalità Diagramma diagnosi."
keywords: 
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 820b73a5dbf9bb108e189313cf6ee2b924ab04c7
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualizzare e risolvere i problemi di Analisi di flusso
In Analisi di flusso, come in altre tecnologie basate su cloud, è talvolta necessario eseguire operazioni di risoluzione dei problemi per comprendere il motivo per cui un processo non produce l'output previsto o non ne produce alcuno. Tenendo presente questo aspetto, Analisi di flusso di Azure offre la funzionalità per visualizzare un processo di streaming. Questa funzionalità si rivela utile anche come strumento di modellazione e risulta vantaggiosa per gli utenti che hanno la necessità di documentare il proprio lavoro.

Nel pannello di visualizzazione sono visibili non solo gli input, ma anche la query in fase di esecuzione e quindi tutti gli output configurati. È possibile visualizzare con maggiore evidenza i problemi di connettività o configurazione. Può inoltre essere utile avere una rappresentazione visiva della configurazione.

## <a name="using-the-diagnosis-diagram-tool"></a>Uso dello strumento Diagramma diagnosi
Per accedere al visualizzatore, è sufficiente fare clic sul pulsante "Diagramma diagnosi" nell'area "Impostazioni" del processo di Analisi di flusso di Azure.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Gli input e output sono ognuno contraddistinto da un colore per indicare lo stato corrente del componente, come mostrato di seguito.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Se l'utente desidera esaminare i passaggi intermedi della query per comprendere i modelli del flusso di dati all'interno di un processo, lo strumento di visualizzazione mostra la scomposizione della query nei passaggi che la compongono nonché la sequenza del flusso. Facendo clic su ogni passaggio della query, verrà visualizzata la sezione corrispondente in un riquadro di modifica della query, come mostrato di seguito. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione ad Analisi dei flussi di Azure](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

