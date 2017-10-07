---
title: Genera dati tooconfigure aaaHow per i processi di flusso Analitica | Documenti Microsoft
description: Configurare gli output per i processi di Analisi di flusso | segmento del percorso di apprendimento.
keywords: output dei dati, spostamento dei dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>La modalità di output tooconfigure dati per i processi di flusso Analitica

I processi di flusso Analitica Azure possono essere connesso tooone o più output di dati, che definiscono un sink di dati esistente tooan connessione. Durante il processo di flusso Analitica elabora e trasforma i dati in ingresso, un flusso di dati di eventi di output viene scritto l'output del processo tooyour.

Output di dati di flusso Analitica può essere utilizzato toosource di dashboard in tempo reale o avvisi, trigger flussi di lavoro lo spostamento dei dati o semplicemente i dati di archiviazione per l'elaborazione batch in un secondo momento. L'analisi di flusso dispone dell'integrazione di prima classe con diversi servizi di Azure, che sono documentati in dettaglio di seguito.

tooadd un processo di flusso Analitica tooyour output:

1. In hello [portale di Azure](https://portal.azure.com), aprire il processo e fare clic su **output** e quindi fare clic su **Aggiungi** nel Pannello di output di hello che viene visualizzato.
   
    ![Aggiungere output](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Specificare un nome descrittivo per l'output di hello **Alias di Output** casella. Questo nome può essere utilizzato nella query del processo in un secondo momento nell'output di toohello toorefer.  
   
    Compilare il resto di hello dell'output di hello necessario connessione proprietà tooconnect tooyour.  Questi campi variano in base al tipo di output e vengono definiti in modo dettagliato di seguito.  
   
    ![Scegliere il tipo di spostamento dei dati](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. In base al tipo di output di hello, potrebbe essere necessario toospecify come dati hello viene serializzati o formattati. le impostazioni di serializzazione specifici Hello per ogni tipo di output sono documentate di seguito.
   
    Compilare il resto di hello di origine dei dati tooyour proprietà tooconnect hello necessarie per la connessione. Questi campi variano in base al tipo del tipo di input e di origine e sono definiti in modo dettagliato in hello [articolo Crea processo](stream-analytics-create-a-job.md).  

> [!Note]
>
> Qualsiasi processo di aggiunta toohello elemento di output, deve esistere prima hello processo viene avviato e gli eventi di inizio propagazione. Ad esempio, se si utilizza l'archiviazione Blob come output, il processo di hello non creerà un account di archiviazione automaticamente. È necessario che toobe creato dall'utente hello prima dell'avvio del processo ASA hello.
> 
 

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

