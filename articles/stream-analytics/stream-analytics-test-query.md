---
title: il test delle query Analitica flusso aaaAzure | Documenti Microsoft
description: Come tootest le query nei processi di flusso Analitica.
keywords: testare query, risolvere i problemi relativi alle query
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Testare le query Analitica di flusso di Azure nel portale di Azure hello

Con Analitica di flusso di Azure, è possibile testare le query in hello portale di Azure senza la necessità di toostart o arrestare un processo.

## <a name="test-hello-input"></a>Input di test hello

1. tootest con dati di input di esempio, uno degli input e quindi scegliere **caricare i dati di esempio dal file**.

    ![Pulsante per il testo delle query nell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Dopo il caricamento di hello è completo, fare clic su **Test** tootest aver fornito dati di esempio di questa query hello.

    ![dati di esempio per il test nell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

output di Hello della query viene visualizzato nel browser hello, con risultati collegamento se si vuole output del test hello toosave per un uso successivo. È ora facilmente e in modo iterativo modificare la query e testarlo ripetutamente toosee come output di hello cambia.

![Output di esempio dell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Con più output in una query, è possibile visualizzare i risultati di hello per entrambi gli output separatamente e attivare o disattivare facilmente tra di essi.

Dopo che si è soddisfatti dei risultati di hello visualizzati nel browser di hello, è possibile salvare la query, avviare il processo e consentire la elabora gli eventi senza errori.

## <a name="get-help"></a>Ottenere aiuto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
