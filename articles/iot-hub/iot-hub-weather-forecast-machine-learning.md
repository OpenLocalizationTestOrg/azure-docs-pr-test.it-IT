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
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="08206-104">Previsioni meteorologiche utilizzando i dati del sensore hello dall'hub IoT in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="08206-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="08206-106">Machine learning è una tecnica di analisi scientifica dei dati che consente ai computer imparare dalle tendenze, i risultati ed esistente dati tooforecast future i comportamenti.</span><span class="sxs-lookup"><span data-stu-id="08206-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="08206-107">Azure Machine Learning è un servizio cloud analitica predittiva rende tooquickly possibile creare e distribuire modelli predittivi come soluzioni analitica.</span><span class="sxs-lookup"><span data-stu-id="08206-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="08206-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="08206-108">What you learn</span></span>

<span data-ttu-id="08206-109">Viene illustrato come toouse Azure Machine Learning toodo previsioni meteorologiche (possibilità di pioggia) utilizzando hello temperatura e umidità dati l'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="08206-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="08206-110">probabilità Hello pioggia è l'output di hello di un modello di stima weather preparata.</span><span class="sxs-lookup"><span data-stu-id="08206-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="08206-111">modello Hello si basa su probabilità tooforecast dati cronologici in base a temperatura e umidità pioggia.</span><span class="sxs-lookup"><span data-stu-id="08206-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="08206-112">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="08206-112">What you do</span></span>

- <span data-ttu-id="08206-113">Distribuire modello di stima hello weather come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="08206-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="08206-114">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="08206-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="08206-115">Creare un processo di flusso Analitica e configurare il processo di hello per:</span><span class="sxs-lookup"><span data-stu-id="08206-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="08206-116">Leggere i dati di temperatura e umidità dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08206-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="08206-117">Chiamare il possibilità di hello web servizio tooget hello pioggia.</span><span class="sxs-lookup"><span data-stu-id="08206-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="08206-118">Salvare l'archivio di blob di Azure tooan risultato hello.</span><span class="sxs-lookup"><span data-stu-id="08206-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="08206-119">Utilizzare Esplora risorse di archiviazione di Microsoft Azure tooview hello previsioni del tempo.</span><span class="sxs-lookup"><span data-stu-id="08206-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08206-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="08206-120">What you need</span></span>

- <span data-ttu-id="08206-121">Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="08206-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="08206-122">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="08206-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="08206-123">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="08206-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="08206-124">Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="08206-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="08206-125">Un account di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="08206-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="08206-126">([Prova gratuita di Machine Learning Studio](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="08206-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="08206-127">Distribuzione modello di stima weather hello come un servizio web</span><span class="sxs-lookup"><span data-stu-id="08206-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="08206-128">Passare toohello [pagina modello di stima weather](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="08206-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="08206-129">Fare clic su **Apri in Studio** in Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="08206-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="08206-130">![Pagina modello di stima hello aprire weather nella raccolta Intelligence Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="08206-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="08206-131">Fare clic su **eseguire** toovalidate hello passaggi nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="08206-132">Questo passaggio potrebbe richiedere toocomplete 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="08206-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="08206-133">![Modello di stima weather aprire hello in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="08206-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="08206-134">Fare clic su **SET UP WEB SERVICE** (Imposta servizio Web) > **Predictive Web Service** (Servizio Web predittivo).</span><span class="sxs-lookup"><span data-stu-id="08206-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="08206-135">![Distribuzione del modello di stima weather hello in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="08206-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="08206-136">Nel diagramma hello, trascinare hello **input del servizio Web** modulo in un punto qualsiasi in prossimità di hello **Score Model** modulo.</span><span class="sxs-lookup"><span data-stu-id="08206-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="08206-137">Connettersi hello **input del servizio Web** modulo toohello **Score Model** modulo.</span><span class="sxs-lookup"><span data-stu-id="08206-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="08206-138">![Collegare due moduli in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="08206-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="08206-139">Fare clic su **eseguire** toovalidate hello passaggi nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="08206-140">Fare clic su **distribuzione servizio WEB** modello hello toodeploy come servizio web.</span><span class="sxs-lookup"><span data-stu-id="08206-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="08206-141">Nel dashboard di hello del modello di hello, scaricare hello **Excel 2010 o cartella di lavoro precedenti** per **richiesta/risposta**.</span><span class="sxs-lookup"><span data-stu-id="08206-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="08206-142">Assicurarsi di scaricare hello **Excel 2010 o cartella di lavoro precedenti** anche se si esegue una versione successiva di Excel nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="08206-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Scaricare hello Excel per l'endpoint di risposta richiesta hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="08206-144">Aprire una cartella di lavoro di Excel hello, prendere nota di hello **URL servizio WEB** e **tasto**.</span><span class="sxs-lookup"><span data-stu-id="08206-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="08206-145">Configurare, configurare ed eseguire un processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="08206-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="08206-146">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="08206-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="08206-147">In hello [portale di Azure](https://ms.portal.azure.com/), fare clic su **New** > **Internet of Things** > **processo flusso Analitica**.</span><span class="sxs-lookup"><span data-stu-id="08206-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="08206-148">Immettere le seguenti informazioni per il processo di hello hello.</span><span class="sxs-lookup"><span data-stu-id="08206-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="08206-149">**Nome del processo**: nome hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="08206-150">nome Hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="08206-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="08206-151">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08206-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="08206-152">**Percorso**: utilizzare hello stesso percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="08206-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="08206-153">**PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="08206-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="08206-155">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08206-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="08206-156">Aggiungere un processo di flusso Analitica toohello input</span><span class="sxs-lookup"><span data-stu-id="08206-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="08206-157">Processo di flusso Analitica hello aperto.</span><span class="sxs-lookup"><span data-stu-id="08206-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="08206-158">In **Topologia processo** fare clic su **Input**.</span><span class="sxs-lookup"><span data-stu-id="08206-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="08206-159">In hello **input** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="08206-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="08206-160">**Alias di input**: alias univoco hello hello input.</span><span class="sxs-lookup"><span data-stu-id="08206-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="08206-161">**Origine**: selezionare **Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="08206-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="08206-162">**Gruppo di consumer**: gruppo di consumer hello selezionare creato.</span><span class="sxs-lookup"><span data-stu-id="08206-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Aggiungere un processo di flusso Analitica toohello input in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="08206-164">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08206-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="08206-165">Aggiungere un processo di flusso Analitica toohello output</span><span class="sxs-lookup"><span data-stu-id="08206-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="08206-166">In **Topologia processo** fare clic su **Output**.</span><span class="sxs-lookup"><span data-stu-id="08206-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="08206-167">In hello **output** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="08206-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="08206-168">**Alias di output**: alias univoco di hello per l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="08206-169">**Sink**: selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="08206-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="08206-170">**Account di archiviazione**: hello account di archiviazione per lo spazio di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="08206-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="08206-171">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="08206-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="08206-172">**Contenitore**: contenitore hello in cui è stato salvato blob hello.</span><span class="sxs-lookup"><span data-stu-id="08206-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="08206-173">È possibile usare un contenitore esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="08206-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="08206-174">**Formato di serializzazione eventi**: selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="08206-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Aggiungere un processo di flusso Analitica toohello output in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="08206-176">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08206-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="08206-177">Aggiungere un servizio web flusso Analitica processo toocall hello è distribuito di toohello (funzione)</span><span class="sxs-lookup"><span data-stu-id="08206-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="08206-178">In **Topologia processo** fare clic su **Funzioni** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="08206-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="08206-179">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="08206-179">Enter hello following information:</span></span>

   <span data-ttu-id="08206-180">**Alias della funzione**: immettere `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="08206-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="08206-181">**Tipo funzione**: selezionare **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="08206-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="08206-182">**Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="08206-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="08206-183">**URL**: immettere l'URL del servizio WEB che si è preso nota verso il basso hello dalla cartella di lavoro di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="08206-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="08206-184">**Chiave**: immettere hello chiave di accesso che si è preso nota verso il basso dalla cartella di lavoro di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="08206-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Aggiungere un processo di flusso Analitica funzione toohello in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="08206-186">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08206-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="08206-187">Configurare la query hello del processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="08206-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="08206-188">In **Topologia processo** fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="08206-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="08206-189">Sostituire il codice esistente hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="08206-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="08206-190">Sostituire `[YourInputAlias]` con alias hello di input del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="08206-191">Sostituire `[YourOutputAlias]` con alias di output di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="08206-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="08206-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="08206-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="08206-193">Eseguire il processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="08206-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="08206-194">Nel processo di flusso Analitica hello, fare clic su **avviare** > **ora** > **avviare**.</span><span class="sxs-lookup"><span data-stu-id="08206-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="08206-195">Quando si avvia il processo di hello, lo stato del processo hello cambia da **arrestato** troppo**esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="08206-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Eseguire il processo di flusso Analitica hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="08206-197">Utilizzare Esplora risorse di archiviazione di Microsoft Azure tooview hello previsioni del tempo</span><span class="sxs-lookup"><span data-stu-id="08206-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="08206-198">Eseguire la raccolta di hello client applicazione toostart e l'invio di temperatura e umidità hub IoT tooyour di dati.</span><span class="sxs-lookup"><span data-stu-id="08206-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="08206-199">Per ogni messaggio che riceve l'hub IoT, il processo di flusso Analitica hello chiama hello previsioni meteorologiche web servizio tooproduce hello probabilità pioggia.</span><span class="sxs-lookup"><span data-stu-id="08206-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="08206-200">risultato Hello viene quindi salvato tooyour nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="08206-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="08206-201">Azure Storage Explorer è uno strumento che è possibile utilizzare il risultato di hello tooview.</span><span class="sxs-lookup"><span data-stu-id="08206-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="08206-202">[Scaricare e installare Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="08206-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="08206-203">Aprire Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="08206-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="08206-204">Accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="08206-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="08206-205">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="08206-205">Select your subscription.</span></span>
1. <span data-ttu-id="08206-206">Fare clic sulla sottoscrizione in uso > **Account di archiviazione** > account di archiviazione in uso > **contenitori BLOB** > contenitore BLOB in uso.</span><span class="sxs-lookup"><span data-stu-id="08206-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="08206-207">Aprire un risultato di hello toosee file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="08206-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="08206-208">record di Hello ultima colonna hello probabilità di pioggia.</span><span class="sxs-lookup"><span data-stu-id="08206-208">hello last column records hello chance of rain.</span></span>

   ![Ottenere i risultati delle previsioni meteo con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="08206-210">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="08206-210">Summary</span></span>

<span data-ttu-id="08206-211">Azure Machine Learning tooproduce hello probabilità pioggia in base ai dati di temperatura e umidità hello che riceve l'hub IoT utilizzati correttamente.</span><span class="sxs-lookup"><span data-stu-id="08206-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]