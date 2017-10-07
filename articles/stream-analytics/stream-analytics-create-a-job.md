---
title: aaaHow toocreate un processo di elaborazione analitica dei dati per flusso Analitica | Documenti Microsoft
description: Creare un processo di elaborazione di analisi dei dati per Analisi di flusso | segmento del percorso di apprendimento.
keywords: elaborazione di analisi dei dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Come toocreate processo un'elaborazione analitica dei dati per flusso Analitica
risorsa di primo livello Hello in Analitica di flusso di Azure è un processo di flusso Analitica.  È costituito da uno o più input di origini dati, una query che esprime la trasformazione dei dati hello e una o più destinazioni di output che i risultati vengono scritti. Insieme questi abilitare analitica di hello utente tooperform dati per flusso di dati degli scenari di elaborazione.

toostart tramite flusso Analitica, iniziare creando un nuovo processo di flusso Analitica.  Si noti che l'azione non ha costi di fatturazione fino a quando non viene avviato il processo di hello.

1. Accedi a hello online [portale di Azure classico](http://manage.windowsazure.com) o hello [portale di Azure](https://portal.azure.com/).
2. Nel portale di hello: **fare clic su nuovo**, quindi fare clic su **Data Services** o **dati Analitica** a seconda del portale e quindi fare clic su **Azure flusso Analitica** o **flusso Analitica** e quindi **creazione rapida**.
   
   ![Procedura guidata del processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Creare un processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Specificare hello configurazione desiderata per il processo di flusso Analitica hello.
   
   * In hello **nome del processo** , immettere un nome tooidentify hello Analitica di flusso del processo. Quando hello **nome del processo** viene convalidato, viene visualizzato un segno di spunta verde nella casella nome del processo di hello. Hello **nome del processo** possono contenere solo caratteri alfanumerici e hello '-' caratteri e deve essere compresa tra 3 e 63 caratteri.
   * Utilizzare **area** nel portale di Azure hello o **percorso** in hello Azure toospecify portale hello posizione geografica in cui si desidera che il processo di hello toorun.
   * Se tramite hello portale di Azure, selezionare o creare un toouse di account di archiviazione come hello **Account di archiviazione di monitoraggio regionale**. Questo account di archiviazione è toostore utilizzati dati di monitoraggio di tutti i processi di flusso Analitica in esecuzione in questa area.
   * Se tramite hello portale di Azure, specificare un nuovo o esistente **gruppo di risorse** toohold relative risorse per l'applicazione.
4. Dopo aver configurate le opzioni di hello nuovo flusso Analitica processo, fare clic su **Crea processo di flusso Analitica**. Può richiedere alcuni minuti per hello Analitica flusso processo toobe creato. stato hello toocheck, è possibile monitorare lo stato di avanzamento hello nell'hub notifiche hello.
   
   ![Processo di elaborazione di analisi dei dati, hub di notifica](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, processo di elaborazione di analisi dei dati, creare un processo](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. il nuovo processo di Hello mostrerà lo stato di **creato**. Si noti che hello **avviare** pulsante è disabilitato. Prima di iniziare il processo di hello, configurare hello processo input, query e output.
   
   ![Elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

