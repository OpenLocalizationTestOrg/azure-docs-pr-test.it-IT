---
title: aaaAdd un tipo di dati di input i processi di flusso Analitica tooyour | Documenti Microsoft
description: Informazioni su come toohook backup un tooyour di origine dati Analitica di flusso di processo come flusso dati di input dai dati di riferimento o hub eventi dall'archiviazione BLOB.
keywords: input di dati, flusso di dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Aggiungere un flusso dati di input o riferimento dati tooa Analitica flusso processo
Informazioni su come toohook backup un tooyour di origine dati Analitica di flusso di processo come flusso dati di input dai dati di riferimento o hub eventi dall'archiviazione Blob.

I processi di flusso Analitica Azure possono essere connesso tooone dati di input o altre, ciascuno dei quali definisce un'origine dati esistente tooan di connessione. Come origine dati toothat vengono inviati dati, è utilizzata dal processo di flusso Analitica hello ed elaborato in tempo reale come flusso di dati. Flusso Analitica dispone di prima classe integrazione con [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) e [archiviazione Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) all'interno e all'esterno di sottoscrizione del processo di hello.

In questo articolo è un passaggio hello [percorso di apprendimento Analitica flusso](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Input di dati: dati di streaming e dati di riferimento
Esistono due tipi di input distinti in Analisi di flusso: dati di riferimento e flussi di dati.

* **Flussi di dati**: i processi di flusso Analitica devono includere almeno un dati flusso input toobe utilizzati e trasformati da processo hello. L'archivio BLOB di Azure e Hub eventi di Azure sono supportati come origini di input del flusso dei dati. Hub eventi di Azure sono flussi di eventi toocollect utilizzati da dispositivi connessi, servizi e applicazioni. Si può usare l'archivio BLOB di Azure come origine di input per l'inserimento di dati in blocco come flusso.  
* **Dati di riferimento**: l’analisi di flusso supporta un secondo tipo di input ausiliario denominato dati di riferimento.  Come toodata anziché in movimento, i dati sono statici o a modifica lenta.  In genere utilizzato per l'esecuzione di ricerche e correlazioni con flussi di dati toocreate un set di dati più completo.  Archiviazione Blob di Azure è attualmente origine di input hello è supportato solo per i dati di riferimento.  

un processo di flusso Analitica tooyour input tooadd:

1. Nel portale di Azure hello fare clic su **input** e quindi fare clic su **aggiungere un Input** nel processo di flusso Analitica.
   
    ![Portale di Azure classico - aggiungere un input.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    In hello portale di Azure, fare clic su hello **input** riquadro nel processo di flusso Analitica.  
   
    ![Portale di Azure - aggiungere un input di dati.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Specificare il tipo di hello dell'input hello: entrambi **flusso di dati** o **dati di riferimento**.
   
    ![Aggiungere i dati corretti hello di input, flusso o fare riferimento a](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Aggiungere i dati corretti hello di input, flusso o fare riferimento a](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Se la creazione di un input del flusso di dati, specificare il tipo di origine hello per l'input hello.  Questo passaggio può essere ignorato durante la creazione dei dati di riferimento, poiché al momento è supportato soltanto l’archivio BLOB.
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Specificare un nome descrittivo per questo hello input nella casella di Alias di Input.  Questo nome verrà utilizzato nella query del processo in un secondo momento nel toorefer toohello input.
   
    Compilare il resto di hello di origine dei dati tooyour proprietà tooconnect hello necessarie per la connessione. Questi campi variano in base al tipo di origine e di input e vengono definiti in modo dettagliato [qui](stream-analytics-create-a-job.md).  
   
    ![Aggiungere l'input di dati dell'hub eventi](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Specificare le impostazioni di serializzazione hello per dati di input hello:
   
   * toomake che le query funzionino come hello previsto, specificare hello **il formato di serializzazione di eventi** dei dati in arrivo.  I formati di serializzazione supportati sono JSON, CSV e Avro.
   * Verificare hello **codifica** per i dati di hello.  UTF-8 è hello formato di codifica è supportata solo in questo momento.
     
     ![Impostazioni di serializzazione di dati per l'input di dati hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Impostazioni di serializzazione di dati per l'input di dati hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Dopo aver completato la creazione di input hello, flusso Analitica verificherà che è possibile connettere l'origine di input toohello.  È possibile visualizzare lo stato di hello di hello operazione di connessione di Test nell'hub di notifica hello.
   
    ![Test della connessione di hello flusso di dati di input](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Test della connessione di hello flusso di dati di input](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Ottenere aiuto per gli input dei dati di streaming
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

