---
title: esegue una query utilizzando SELECT INTO aaaDebug Analitica di flusso di Azure | Documenti Microsoft
description: Campionare i dati intermedi di una query mediante istruzioni SELECT INTO in Analisi di flusso
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Eseguire il debug delle query mediante istruzioni SELECT INTO

Nell'elaborazione di dati in tempo reale, conoscere i dati di hello sembra intermedio hello di hello query può essere utile. Poiché gli input o i passaggi di un processo di Analisi di flusso di Azure possono essere letti più volte, è possibile scrivere istruzioni SELECT INTO aggiuntive. Questa operazione restituisce i dati intermedi nell'account di archiviazione e consente di controllare la correttezza di hello dei dati di hello, proprio come *controllare variabili* eseguire durante il debug di un programma.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Utilizzare SELECT INTO toocheck hello flusso di dati

Hello query di esempio seguente in un processo Analitica di flusso di Azure dispone di input del flusso di uno, due input di dati di riferimento e un tooAzure output archiviazione tabella. query Hello unisce i dati di hub eventi hello e due BLOB tooget hello nome e la categoria di informazioni di riferimento:

![Esempio di query SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Si noti che il processo di hello è in esecuzione, ma gli eventi non vengono generati nell'output di hello. In hello **monitoraggio** riquadro, riportato di seguito, si noterà che l'input hello produce dati, ma non si conosce il passaggio di hello **JOIN** causato tutti hello toobe eventi eliminati.

![riquadro monitoraggio Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
In questo caso, è possibile aggiungere alcuni aggiuntivo le istruzioni SELECT INTO troppo "accesso" hello intermedia JOIN risultati e i dati di hello che viene letto dall'input hello.

In questo esempio sono stati aggiunti due nuovi "output temporanei". Può trattarsi di qualsiasi sink desiderato. Qui si usa Archiviazione di Azure come esempio:

![Aggiunta di ulteriori istruzioni SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

È quindi possibile riscrivere la query hello simile al seguente:

![Query SELECT INTO riscritta](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Ora avviare di nuovo il processo di hello e consentire l'esecuzione per alcuni minuti. Quindi eseguire una query temp1 e temp2 con hello tooproduce Visual Studio Cloud Explorer le tabelle seguenti:

**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Come si può notare, temp1 e temp2 dispone di dati e colonna nome hello viene compilato correttamente in temp2. Tuttavia, poiché non sono ancora presenti dati nell'output, c'è qualcosa di sbagliato:

![Tabella SELECT INTO output1 senza dati](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Tramite il campionamento dei dati di hello, può essere quasi certo che il problema di hello sia con hello secondo JOIN. È possibile scaricare i dati di riferimento hello dal blob hello e dare un'occhiata:

![Tabella SELECT INTO riferimento](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Come si può notare, il formato di hello di hello GUID in questi dati di riferimento è diverso dal formato hello di hello [colonna temp2 from]. Per questa ragione i dati di hello non arrivano in USCITA1 come previsto.

È possibile correggere il formato di dati hello, caricarlo tooreference blob e riprovare:

![Tabella SELECT INTO temporanea](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Questa volta, dati hello nell'output di hello sono formattati e compilati come previsto.

![Tabella SELECT INTO finale](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Ottenere aiuto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

