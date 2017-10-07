---
title: 'visualizzazione dei dati di sensore provenienti dall''IoT Hub di Azure: Power BI aaaReal ora | Documenti Microsoft'
description: "Utilizzare Power BI toovisualize temperatura e umidità i dati raccolti dal sensore hello e inviati tooyour Azure IoT hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: visualizzazione dei dati in tempo reale, visualizzazione dei dati dal vivo, visualizzazione dei dati del sensore
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Visualizzare i dati del sensore in tempo reale da IoT Hub di Azure tramite Power BI

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Si apprenderà come toovisualize in tempo reale dati del sensore che riceve l'hub IoT di Azure da Power BI. Se si desidera visualizzare i dati hello tootry nell'hub IoT con le app Web, vedere [App Web di Azure usare toovisualize sensore in tempo reale dati IoT Hub Azure](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Operazioni da fare

- Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.
- Creare, configurare e di eseguire un processo di flusso Analitica per il trasferimento dei dati dal tooyour hub IoT account Power BI.
- Creare e pubblicare i dati del hello toovisualize report Power BI.

## <a name="what-you-need"></a>Elementi necessari

- Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:
  - Una sottoscrizione di Azure attiva.
  - Un hub IoT di Azure nella sottoscrizione.
  - Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.
- Un account di Power BI. ([Provare gratuitamente Power BI](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Configurare, configurare ed eseguire un processo di analisi di flusso

### <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.

1. In hello portale di Azure, fare clic su Nuovo > Internet of Things > processo di flusso Analitica.
1. Immettere le seguenti informazioni per il processo di hello hello.

   **Nome del processo**: nome hello del processo di hello. nome Hello deve essere globalmente univoco.

   **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   **Percorso**: utilizzare hello stesso percorso per il gruppo di risorse.

   **PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Fare clic su **Crea**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Aggiungere un processo di flusso Analitica toohello input

1. Processo di flusso Analitica hello aperto.
1. In **Topologia processo** fare clic su **Input**.
1. In hello **input** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:

   **Alias di input**: alias univoco hello hello input.

   **Origine**: selezionare **Hub IoT**.

   **Gruppo di consumer**: gruppo di consumer hello selezionare appena creato.
1. Fare clic su **Crea**.

   ![Aggiungere un processo di flusso Analitica tooa input in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Aggiungere un processo di flusso Analitica toohello output

1. In **Topologia processo** fare clic su **Output**.
1. In hello **output** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:

   **Alias di output**: alias univoco di hello per l'output di hello.

   **Sink**: selezionare **Power BI**.
1. Fare clic su **Autorizza** e quindi accedere all'account di Power BI.
1. Una volta autorizzato, immettere hello le seguenti informazioni:

   **Area di lavoro del gruppo**: selezionare l'area di lavoro del gruppo di destinazione.

   **Nome set di dati**: immettere un nome per il set di dati.

   **Nome tabella**: immettere un nome per la tabella.
1. Fare clic su **Crea**.

   ![Aggiungere un processo di flusso Analitica tooa output in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurare la query hello del processo di flusso Analitica hello

1. In **Topologia processo** fare clic su **Query**.
1. Sostituire `[YourInputAlias]` con alias hello di input del processo di hello.
1. Sostituire `[YourOutputAlias]` con alias di output di hello del processo di hello.
1. Fare clic su **Salva**.

   ![Aggiungere un processo di flusso Analitica tooa query in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Eseguire il processo di flusso Analitica hello

Nel processo di flusso Analitica hello, fare clic su **avviare** > **ora** > **avviare**. Quando si avvia il processo di hello, lo stato del processo hello cambia da **arrestato** troppo**esecuzione**.

![Eseguire un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Creare e pubblicare i dati del hello toovisualize report Power BI

1. Verificare che l'applicazione di esempio hello è in esecuzione sul dispositivo. Se non è possibile fare riferimento di esercitazioni toohello in [configurare il dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Accedi tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.
1. Passare toohello gruppo dell'area di lavoro che durante la creazione di output di hello per il processo di flusso Analitica hello è impostata.
1. Fare clic su **Set di dati in streaming**.

   Dovrebbe essere hello elencato set di dati specificato al momento della creazione di output per il processo di flusso Analitica hello hello.
1. In **azioni**, fare clic su hello prima icona toocreate un report.

   ![Creare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Creare una temperatura in tempo reale di grafico tooshow riga nel tempo.
   1. Nella pagina di creazione report hello, aggiungere un grafico a linee.
   1. In hello **campi** riquadro espandere tabella hello specificato al momento della creazione di output di hello per il processo di flusso Analitica hello.
   1. Trascinare **EventEnqueuedUtcTime** troppo**asse** su hello **visualizzazioni** riquadro.
   1. Trascinare **temperatura** troppo**valori**.

      A questo punto viene creato un grafico a linee. Hello asse x Visualizza la data e ora nel fuso orario UTC di hello. asse y Hello Visualizza temperatura sensore hello.

      ![Aggiungere un grafico a linee per temperatura tooa report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Creare un'altra riga grafico tooshow in tempo reale umidità nel tempo. toodo, attenersi alla stessa procedura sopra hello e inserire **EventEnqueuedUtcTime** sull'asse delle x hello e **umidità** sull'asse y hello.

   ![Aggiungere un grafico a linee per umidità tooa report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Fare clic su **salvare** report hello toosave.
1. Fare clic su **File** > **pubblicare tooweb**.
1. Fare clic su **Crea codice di incorporamento**, quindi fare clic su **Pubblica**.

Viene fornito collegamento al report hello che è possibile condividere con tutti gli utenti per l'accesso ai report e report di hello toointegrate di frammento di codice nel blog o nel sito Web.

![Pubblicare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft offre inoltre hello [App per dispositivi mobili di Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) per visualizzare e interagire con i dashboard di Power BI e i report nel dispositivo mobile.

## <a name="next-steps"></a>Passaggi successivi

Utilizzati correttamente dati di Power BI toovisualize sensore in tempo reale dall'hub IoT di Azure.
È un dati toovisualize alternativa provenienti dall'IoT Hub di Azure. Vedere [App Web di Azure usare toovisualize sensore in tempo reale dati IoT Hub Azure](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
