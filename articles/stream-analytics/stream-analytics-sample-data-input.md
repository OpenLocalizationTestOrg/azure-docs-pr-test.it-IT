---
title: gli input di campionamento aaa Analitica di flusso di Azure | Documenti Microsoft
description: Individuare i problemi durante la risoluzione dei processi di analisi di flusso.
keywords: risoluzione dei problemi relativi all'input, campionamento dell'input
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Campionamento del flusso di input della funzione di analisi di flusso di Azure

Tramite Azure flusso Analitica, è possibile campionare eventi di input che provengono da un file e le query di test nel portale di hello senza toostart o arrestare un processo.

## <a name="testing-your-query"></a>Test di una query

Nel riquadro dettagli processo flusso Analitica hello aprire hello **editor di Query** pannello facendo clic sul nome della query hello in **Query**. (In questo scenario di esempio, poiché non è ancora stata creata alcuna query, fare clic su hello **< >** segnaposto.)

![editor di query Hello Analitica di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

Pannello di Hello editor avanzato per la creazione della query viene visualizzato come lo era nella versione precedente di hello. Ora pannello hello è stato aggiornato con un nuovo riquadro a sinistra che mostra hello input e output utilizzati dalla query hello e definito per il processo.

![editor di query flusso Analitica Hello input e restituisce gli elenchi](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Sono inoltre visibili altri input e output, che non sono definiti. Provengono da hello nuovo modello di query iniziale. Sono modificato, o addirittura eliminato completamente, come si modifica la query hello. È possibile ignorarli senza problemi per il momento.

tootest con dati di input di esempio, uno degli input e quindi scegliere **caricare i dati di esempio dal file**.

![Hello flusso Analitica query editor caricamento dati di esempio di file (comando)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Dopo il caricamento di hello è completo, fare clic su **Test** tootest questa query hello campionare i dati appena immessa.

![pulsante di Test dell'editor di query di Hello Analitica di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Se si desidera l'output del test hello toosave per un uso successivo, nel browser hello con risultati di download toohello un collegamento viene visualizzato l'output di hello della query. È ora facilmente e in modo iterativo modificare la query e testarlo ripetutamente toosee come output di hello cambia.

![Output di esempio dell'editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

In hello immagine precedente, è stato aggiunto un secondo output, chiamato **HighAvgTempOutput**.

Quando si utilizza più output in una query, è possibile visualizzare i risultati di hello per ogni output separatamente e attivare o disattivare facilmente tra di essi.

Dopo che si è soddisfatti dei risultati di hello, è possibile salvare la query, avviare il processo, tranquillamente e guardare magic hello di flusso Analitica.

## <a name="get-help"></a>Ottenere aiuto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
