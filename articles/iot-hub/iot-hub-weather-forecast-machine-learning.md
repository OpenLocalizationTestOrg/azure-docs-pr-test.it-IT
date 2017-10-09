---
title: prevedere l'utilizzo di Azure Machine Learning con i dati dall'IoT Hub aaaWeather | Documenti Microsoft
description: "Possibilità di utilizzare Azure Machine Learning toopredict hello di pioggia dipende umidità e temperatura hello l'hub IoT consente di raccogliere da un sensore dati."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: previsioni meteo machine learning
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Previsioni meteorologiche utilizzando i dati del sensore hello dall'hub IoT in Azure Machine Learning

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Machine learning è una tecnica di analisi scientifica dei dati che consente ai computer imparare dalle tendenze, i risultati ed esistente dati tooforecast future i comportamenti. Azure Machine Learning è un servizio cloud analitica predittiva rende tooquickly possibile creare e distribuire modelli predittivi come soluzioni analitica.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Viene illustrato come toouse Azure Machine Learning toodo previsioni meteorologiche (possibilità di pioggia) utilizzando hello temperatura e umidità dati l'hub IoT di Azure. probabilità Hello pioggia è l'output di hello di un modello di stima weather preparata. modello Hello si basa su probabilità tooforecast dati cronologici in base a temperatura e umidità pioggia.

## <a name="what-you-do"></a>Operazioni da fare

- Distribuire modello di stima hello weather come un servizio web.
- Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.
- Creare un processo di flusso Analitica e configurare il processo di hello per:
  - Leggere i dati di temperatura e umidità dall'hub IoT.
  - Chiamare il possibilità di hello web servizio tooget hello pioggia.
  - Salvare l'archivio di blob di Azure tooan risultato hello.
- Utilizzare Esplora risorse di archiviazione di Microsoft Azure tooview hello previsioni del tempo.

## <a name="what-you-need"></a>Elementi necessari

- Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:
  - Una sottoscrizione di Azure attiva.
  - Un hub IoT di Azure nella sottoscrizione.
  - Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.
- Un account di Azure Machine Learning Studio. ([Prova gratuita di Machine Learning Studio](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Distribuzione modello di stima weather hello come un servizio web

1. Passare toohello [pagina modello di stima weather](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Fare clic su **Apri in Studio** in Microsoft Azure Machine Learning Studio.
   ![Pagina modello di stima hello aprire weather nella raccolta Intelligence Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Fare clic su **eseguire** toovalidate hello passaggi nel modello di hello. Questo passaggio potrebbe richiedere toocomplete 2 minuti.
   ![Modello di stima weather aprire hello in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Fare clic su **SET UP WEB SERVICE** (Imposta servizio Web) > **Predictive Web Service** (Servizio Web predittivo).
   ![Distribuzione del modello di stima weather hello in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Nel diagramma hello, trascinare hello **input del servizio Web** modulo in un punto qualsiasi in prossimità di hello **Score Model** modulo.
1. Connettersi hello **input del servizio Web** modulo toohello **Score Model** modulo.
   ![Collegare due moduli in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Fare clic su **eseguire** toovalidate hello passaggi nel modello di hello.
1. Fare clic su **distribuzione servizio WEB** modello hello toodeploy come servizio web.
1. Nel dashboard di hello del modello di hello, scaricare hello **Excel 2010 o cartella di lavoro precedenti** per **richiesta/risposta**.

   > [!Note]
   > Assicurarsi di scaricare hello **Excel 2010 o cartella di lavoro precedenti** anche se si esegue una versione successiva di Excel nel computer in uso.

   ![Scaricare hello Excel per l'endpoint di risposta richiesta hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Aprire una cartella di lavoro di Excel hello, prendere nota di hello **URL servizio WEB** e **tasto**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Configurare, configurare ed eseguire un processo di analisi di flusso

### <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.

1. In hello [portale di Azure](https://ms.portal.azure.com/), fare clic su **New** > **Internet of Things** > **processo flusso Analitica**.
1. Immettere le seguenti informazioni per il processo di hello hello.

   **Nome del processo**: nome hello del processo di hello. nome Hello deve essere globalmente univoco.

   **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   **Percorso**: utilizzare hello stesso percorso per il gruppo di risorse.

   **PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Fare clic su **Crea**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Aggiungere un processo di flusso Analitica toohello input

1. Processo di flusso Analitica hello aperto.
1. In **Topologia processo** fare clic su **Input**.
1. In hello **input** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:

   **Alias di input**: alias univoco hello hello input.

   **Origine**: selezionare **Hub IoT**.

   **Gruppo di consumer**: gruppo di consumer hello selezionare creato.

   ![Aggiungere un processo di flusso Analitica toohello input in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Fare clic su **Crea**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Aggiungere un processo di flusso Analitica toohello output

1. In **Topologia processo** fare clic su **Output**.
1. In hello **output** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:

   **Alias di output**: alias univoco di hello per l'output di hello.

   **Sink**: selezionare **Archivio BLOB**.

   **Account di archiviazione**: hello account di archiviazione per lo spazio di archiviazione blob. È possibile usare un account di archiviazione esistente o crearne uno nuovo.

   **Contenitore**: contenitore hello in cui è stato salvato blob hello. È possibile usare un contenitore esistente o crearne uno nuovo.

   **Formato di serializzazione eventi**: selezionare **CSV**.

   ![Aggiungere un processo di flusso Analitica toohello output in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Fare clic su **Crea**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Aggiungere un servizio web flusso Analitica processo toocall hello è distribuito di toohello (funzione)

1. In **Topologia processo** fare clic su **Funzioni** > **Aggiungi**.
1. Immettere hello le seguenti informazioni:

   **Alias della funzione**: immettere `machinelearning`.

   **Tipo funzione**: selezionare **Azure ML**.

   **Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**.

   **URL**: immettere l'URL del servizio WEB che si è preso nota verso il basso hello dalla cartella di lavoro di Excel hello.

   **Chiave**: immettere hello chiave di accesso che si è preso nota verso il basso dalla cartella di lavoro di Excel hello.

   ![Aggiungere un processo di flusso Analitica funzione toohello in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Fare clic su **Crea**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurare la query hello del processo di flusso Analitica hello

1. In **Topologia processo** fare clic su **Query**.
1. Sostituire il codice esistente hello con hello seguente codice:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Sostituire `[YourInputAlias]` con alias hello di input del processo di hello.

   Sostituire `[YourOutputAlias]` con alias di output di hello del processo di hello.

1. Fare clic su **Salva**.

### <a name="run-hello-stream-analytics-job"></a>Eseguire il processo di flusso Analitica hello

Nel processo di flusso Analitica hello, fare clic su **avviare** > **ora** > **avviare**. Quando si avvia il processo di hello, lo stato del processo hello cambia da **arrestato** troppo**esecuzione**.

![Eseguire il processo di flusso Analitica hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Utilizzare Esplora risorse di archiviazione di Microsoft Azure tooview hello previsioni del tempo

Eseguire la raccolta di hello client applicazione toostart e l'invio di temperatura e umidità hub IoT tooyour di dati. Per ogni messaggio che riceve l'hub IoT, il processo di flusso Analitica hello chiama hello previsioni meteorologiche web servizio tooproduce hello probabilità pioggia. risultato Hello viene quindi salvato tooyour nell'archiviazione blob di Azure. Azure Storage Explorer è uno strumento che è possibile utilizzare il risultato di hello tooview.

1. [Scaricare e installare Microsoft Azure Storage Explorer](http://storageexplorer.com/).
1. Aprire Azure Storage Explorer.
1. Accedi tooyour account Azure.
1. Selezionare la propria sottoscrizione.
1. Fare clic sulla sottoscrizione in uso > **Account di archiviazione** > account di archiviazione in uso > **contenitori BLOB** > contenitore BLOB in uso.
1. Aprire un risultato di hello toosee file con estensione csv. record di Hello ultima colonna hello probabilità di pioggia.

   ![Ottenere i risultati delle previsioni meteo con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Riepilogo

Azure Machine Learning tooproduce hello probabilità pioggia in base ai dati di temperatura e umidità hello che riceve l'hub IoT utilizzati correttamente.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]