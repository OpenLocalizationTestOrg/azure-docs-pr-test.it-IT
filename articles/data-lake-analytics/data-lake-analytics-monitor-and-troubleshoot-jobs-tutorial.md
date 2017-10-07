---
title: i processi di Azure Data Lake Analitica aaaTroubleshoot tramite il portale di Azure | Documenti Microsoft
description: 'Informazioni su come toouse hello i processi di Data Lake Analitica tootroubleshoot portale di Azure. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Risolvere i problemi dei processi di Analisi di Azure Data Lake mediante il portale di Azure
Informazioni su come toouse hello i processi di Data Lake Analitica tootroubleshoot portale di Azure.

In questa esercitazione, è un problema di file di origine mancanti del programma di installazione e utilizzare problema hello tootroubleshoot di hello portale di Azure.

## <a name="submit-a-data-lake-analytics-job"></a>Inviare un processo di Data Lake Analytics

Inviare hello processo U-SQL seguente:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Hello file di origine definiti nello script hello è **/Samples/Data/SearchLog.tsv1**, in cui deve essere **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Risoluzione dei problemi hello processo

**toosee tutti i processi di hello**

1. Dal portale di Azure hello, fare clic su **Microsoft Azure** nell'angolo superiore sinistro di hello.
2. Fare clic sul riquadro hello con il nome dell'account Data Lake Analitica.  riepilogo dei processi Hello è mostrato sul hello **gestione dei processi** riquadro.

    ![Azure Data Lake Analytics - Gestione dei processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    il processo di Hello Management offre immediatamente hello lo stato del processo. Si noti che è presente un processo non riuscito.
3. Fare clic su hello **gestione dei processi** riquadro processi hello toosee. i processi di Hello sono classificati in **esecuzione**, **in coda**, e **finito**. Verrà visualizzato il processo non riuscito in hello **finito** sezione. Deve essere primo elenco hello. Quando si dispone di molti processi, è possibile fare clic su **filtro** toohelp si toolocate processi.

    ![Azure Data Lake Analytics - Filtrare i processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Fare clic su hello processo non riuscito da hello elenco tooopen hello i dettagli dei processi in un nuovo pannello:

    ![Azure Data Lake Analytics - Processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Hello preavviso **inviare di nuovo** pulsante. Dopo aver risolto il problema di hello, è possibile inviare di nuovo il processo di hello.
5. Fare clic sulla parte evidenziata da hello precedente schermata tooopen hello i dettagli dell'errore.  Verrà visualizzato qualcosa di simile a quanto segue:

    ![Azure Data Lake Analytics - Dettagli del processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Indica la cartella di origine hello non viene trovata.
6. Fare clic su **Duplicate Script**.
7. Hello aggiornamento **FROM** seguente toohello percorso:

    "/Samples/Data/SearchLog.tsv"
8. Fare clic su **Submit Job**.

## <a name="see-also"></a>Vedere anche
* [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Introduzione ad Azure Data Lake Analytics con Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introduzione ad Azure Data Lake Analytics e U-SQL con Visual Studio](data-lake-analytics-u-sql-get-started.md)
* [Gestire Analisi di Azure Data Lake tramite il portale di Azure](data-lake-analytics-manage-use-portal.md)
