---
title: dashboard di Business Intelligence aaaPower in Analitica di flusso di Azure | Documenti Microsoft
description: Utilizzare un in tempo reale streaming Power BI dashboard toogather business intelligence e analizzare i volumi elevati di dati da un processo di flusso Analitica.
keywords: dashboard di analisi, dashboard in tempo reale
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Analisi di flusso e Power BI: dashboard di analisi in tempo reale per lo streaming dei dati
Azure Analitica di flusso consente tootake sfruttare uno dei principali strumenti di business intelligence, hello [Microsoft Power BI](https://powerbi.com/). Questo articolo illustra come creare strumenti di Business Intelligence usando Power BI come output per i processi di Analisi di flusso di Azure. Verrà inoltre descritto come toocreate e utilizzare un dashboard in tempo reale.

In questo articolo continua dal flusso Analitica hello [delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md) esercitazione. Esso si basa sul flusso di lavoro hello creato in tale esercitazione e si aggiunge un output in modo che è possibile visualizzare fraudolente chiamate telefoniche rilevati da un processo di Streaming Analitica di Power BI. 

È disponibile [un video](https://www.youtube.com/watch?v=SGUpT-a99MA) che illustra questo scenario.


## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, verificare di che aver seguito hello:

* Un account Azure.
* Un account per Power BI. È possibile usare un account aziendale o dell'istituto di istruzione.
* Una versione completa di hello [delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md) esercitazione. esercitazione di Hello include un'applicazione che genera metadati telefonata fittizio. Nell'esercitazione di hello, creare un hub eventi e inviare hello streaming hub di eventi toohello dati chiamata telefonica. Scrivere una query che rileva chiamate fraudolente (chiamate da hello stesso numero di hello stesso periodo di tempo in posizioni diverse). 


## <a name="add-power-bi-output"></a>Aggiungere l’output Power BI
Nell'esercitazione di rilevamento di frodi in tempo reale hello, output di hello viene inviato tooAzure nell'archiviazione Blob. In questa sezione aggiungere un output che invia informazioni tooPower BI.

1. Nel portale di Azure hello, aprire il processo di Streaming Analitica hello creato in precedenza. Se si utilizza nome suggerito hello, il processo di hello viene denominato `sa_frauddetection_job_demo`.

2. Seleziona hello **output** centro hello del dashboard processo hello e quindi selezionare **+ Aggiungi**.

3. In **Alias di output** immettere `CallStream-PowerBI`. È possibile usare un nome diverso. In caso contrario, prendere nota di esso, in quanto è necessario il nome di hello in un secondo momento. 

4. In **Sink** selezionare **Power BI**.

   ![Creare un output per Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Fare clic su **Autorizza**.

    Verrà visualizzata una finestra in cui è possibile specificare le credenziali di Azure per l'account aziendale o dell'istituto di istruzione. 

    ![Immettere le credenziali per l'accesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Immettere le credenziali. Tenere quindi quando si immette le credenziali, anche fornendo d'autorizzazione toohello Streaming Analitica processo tooaccess della superficie di Power BI.

7. Quando si ritorna toohello **nuovo output** pannello immettere hello le seguenti informazioni:

    * **Gruppo dell'area di lavoro**: selezionare un'area di lavoro nel tenant di Power BI in cui si desidera toocreate hello set di dati.
    * **Nome set di dati**: immettere `sa-dataset`. È possibile usare un nome diverso. In questo caso prenderne nota perché servirà in un momento successivo.
    * **Nome tabella**: immettere `fraudulent-calls`. L'output di Power BI da processi di Analisi di flusso può avere al momento solo una tabella in un set di dati.

    ![Area di lavoro PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Se Power BI dispone di un set di dati e tabella che dispone di hello stessi nomi hello quelle specificate nel processo di flusso Analitica hello, hello quelli esistenti viene sovrascritti.
    > È consigliabile non creare in modo esplicito il set di dati e la tabella nell'account di Power BI. Vengono creati automaticamente quando si avvia il processo di flusso Analitica e hello inizia distribuzione output in Power BI. Se la query di processo non viene restituito alcun risultato, tabella e hello set di dati non vengono creati.
    >

8. Fare clic su **Crea**.

set di dati Hello viene creata con hello seguenti impostazioni:

* **defaultRetentionPolicy: BasicFIFO**: dati FIFO, con un massimo di 200.000 righe.
* **defaultMode: pushStreaming**: hello dataset supporta streaming riquadri e gli oggetti visivi report tradizionali (anche noto come push.

Attualmente non è possibile creare set di dati con altri flag.

Per ulteriori informazioni sui set di dati di Power BI, vedere hello [API REST di Power BI](https://msdn.microsoft.com/library/mt203562.aspx) riferimento.


## <a name="write-hello-query"></a>Scrivere query hello

1. Chiude hello **output** blade e blade processo toohello restituito.

2. Fare clic su hello **Query** casella. 

3. Immettere hello seguente query. Questa query è simile toohello self join creato nell'esercitazione di rilevamento di frodi hello. Hello differenza consiste nel fatto che questa query consente di inviare risultati toohello nuovo output creato (`CallStream-PowerBI`). 

    >[!NOTE]
    >Se non si il nome hello input `CallStream` nell'esercitazione di rilevamento di frodi hello, sostituire il nome per `CallStream` in hello **FROM** e **JOIN** clausole query hello.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Fare clic su **Salva**.


## <a name="test-hello-query"></a>Query hello del test
Questa sezione è facoltativa ma consigliata. 

1. Se hello TelcoStreaming app non è attualmente in esecuzione, avviarlo attenendosi alla procedura seguente:

    * Aprire una finestra di comando.
    * Passare toohello cartella in cui sono telcogenerator.exe hello e i file modificati telcodatagen.exe.config.
    * Eseguire hello comando seguente:

            telcodatagen.exe 1000 .2 2

2. In hello **Query** pannello, fare clic su Avanti toohello di hello punti `CallStream` di input e quindi selezionare **dati da un input di esempio**.

3. Specificare che si desidera ottenere i dati di tre minuti e fare clic su **OK**. Attendere fino a quando non si riceverà una notifica che dati hello campionati.

4. Fare clic su **Test** e assicurarsi di ottenere i risultati.


## <a name="run-hello-job"></a>Eseguire il processo di hello

1. Verificare che tale app TelcoStreaming hello è in esecuzione.

2. Chiude hello **Query** blade.

3. Nel Pannello di hello processo, fare clic su **avviare**.

    ![Avviare il processo di flusso Analitica hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Il processo di Streaming Analitica inizia cercando fraudolente chiamate nel flusso in ingresso hello. processo Hello inoltre creati set di dati hello e una tabella in Power BI e inizia a inviare i dati relativi a toothem chiamate fraudolenti hello.


## <a name="create-hello-dashboard-in-power-bi"></a>Creare dashboard hello in Power BI

1. Andare troppo[Powerbi.com](https://powerbi.com) e accedere con l'account aziendale o dell'istituto di istruzione. Query di processo di flusso Analitica hello restituisce risultati, vedrai che il set di dati è già stato creato:

    ![Streaming del set di dati in Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. Nell'area di lavoro fare clic su **+&nbsp;Crea**.

    ![pulsante Crea Hello nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Creare un nuovo dashboard e denominarlo `Fraudulent Calls`.

    ![Creare un dashboard e assegnargli un nome nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Nella parte superiore di hello della finestra hello, fare clic su **Aggiungi riquadro**selezionare **dati in STREAMING personalizzati**, quindi fare clic su **Avanti**.

    ![Set di dati di streaming personalizzato](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. In **YOUR DATSETS** (SET DI DATI PERSONALI) selezionare il set di dati interessato e quindi fare clic su **Avanti**.

    ![Set di dati di streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. In **tipo di visualizzazione**selezionare **scheda**e quindi in hello **campi** elenco, selezionare **fraudulentcalls**.

    ![Dettagli di visualizzazione per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Fare clic su **Avanti**.

8. Immettere i dettagli del riquadro, ad esempio un titolo e un sottotitolo.

    ![Titolo e sottotitolo per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Fare clic su **Apply**.

    Si dispone a questo punto di un contatore di frodi.

    ![Contatore di frodi](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Hello seguire i passaggi del nuovo tooadd un riquadro (a partire dal passaggio 4). Questa volta, hello seguenti:

    * Quando si ottengono troppo**tipo di visualizzazione**selezionare **grafico a linee**. 
    * Aggiungere un asse e selezionare **windowend**. 
    * Aggiungere un valore e selezionare **fraudulentcalls**.
    * Per **toodisplay finestra ora**selezionare hello ultimi 10 minuti.

    ![Creare il riquadro per il grafico a linee](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Fare clic su **Avanti**, aggiungere un titolo e un sottotitolo e fare clic su **Applica**.

    dashboard di Power BI Hello ora offre due visualizzazioni dei dati sulle chiamate fraudolente come rilevato nel flusso di dati hello.

    ![Dashboard di Power BI completo che mostra due riquadri per le chiamate fraudolente](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Altre informazioni su Power BI

Questa esercitazione viene illustrato come toocreate solo alcuni tipi di visualizzazioni per un set di dati. Power BI consente di creare altri strumenti di business intelligence per clienti per l'organizzazione. Per ulteriori informazioni, vedere hello seguenti risorse:

* Per un altro esempio di un dashboard di Power BI, eseguire il controllo hello [Introduzione a Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.
* Per ulteriori informazioni sulla configurazione di Streaming Analitica processo tooPower output BI e utilizzano i gruppi di Power BI, esaminare hello [Power BI](stream-analytics-define-outputs.md#power-bi) sezione di hello [Analitica di flusso di output](stream-analytics-define-outputs.md) articolo. 
* Per informazioni sull'utilizzo di Power BI in generale, vedere [Dashboard in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Informazioni sulle limitazioni e le procedure consigliate
Attualmente, è possibile chiamare Power BI approssimativamente una volta al secondo. Gli oggetti visivi di streaming supportano pacchetti da 15 KB. Tuttavia, gli oggetti visivi streaming esito negativo (ma push continua toowork). A causa di queste limitazioni, Power BI si presta più naturalmente toocases in Azure flusso Analitica svolge un riduce il carico di dati in modo significativo. È consigliabile utilizzare una finestra a cascata o Hopping finestra tooensure che push di dati è al massimo un push al secondo e che la query inserita all'interno di requisiti di velocità effettiva di hello.

È possibile utilizzare la finestra seguente equazione toocompute hello valore toogive hello in secondi:

![Equazione 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Ad esempio:

* Sono presenti 1.000 dispositivi che inviano dati a intervalli di un secondo.
* Si sta utilizzando hello Power BI Pro SKU che supporta 1.000.000 di righe all'ora.
* Si desidera quantità hello toopublish dei dati medi per ogni dispositivo tooPower BI.

Di conseguenza, l'equazione hello diventa:

![Equazione 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

In base a questa configurazione, è possibile modificare i seguenti toohello query originale di hello:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Rinnovare l'autorizzazione
Password hello è stato modificato dopo il processo di creazione o dell'ultima autenticazione, è necessario tooreauthenticate account di Power BI. Se Azure multi-Factor Authentication è configurato per il tenant di Azure Active Directory (Azure AD), è necessario anche l'autorizzazione di Power BI toorenew ogni due settimane. Se non viene rinnovata, si potrebbe verificare sintomi, ad esempio la mancanza di output del processo o un `Authenticate user error` nel log delle operazioni hello.

Analogamente, se un processo viene avviato dopo hello token è scaduto, si verifica un errore e ha esito negativo processo hello. tooresolve questo problema, arrestare il processo di hello che è in esecuzione e passare tooyour output di Power BI. tooavoid perdita di dati, seleziona hello **rinnovare l'autorizzazione** collegamento e quindi riavviare il processo da hello **ora ultimo arresto**.

Dopo l'autorizzazione di hello è stato aggiornato con Power BI, verde viene visualizzato un avviso in hello autorizzazione area tooreflect che problema hello è stato risolto.

## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
