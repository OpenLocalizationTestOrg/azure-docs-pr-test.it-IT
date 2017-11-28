---
title: Previsioni meteo usando Azure Machine Learning con i dati dell'hub IoT | Microsoft Docs
description: "Usare Azure Machine Learning per stimare la probabilità di pioggia in base ai dati di temperatura e umidità che l'hub IoT riceve da un sensore."
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="7038e-104">Previsioni meteo usando i dati sensore dell'hub IoT in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7038e-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="7038e-106">L'apprendimento automatico o machine learning è una tecnica di analisi scientifica dei dati che consente ai computer di apprendere dai dati esistenti per prevedere comportamenti, tendenze e risultati futuri.</span><span class="sxs-lookup"><span data-stu-id="7038e-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="7038e-107">Azure Machine Learning è un servizio di analisi predittiva basato sul cloud che consente di creare e distribuire rapidamente modelli predittivi come soluzioni di analisi.</span><span class="sxs-lookup"><span data-stu-id="7038e-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="7038e-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7038e-108">What you learn</span></span>

<span data-ttu-id="7038e-109">Si apprende come usare Azure Machine Learning per formulare previsioni meteo (possibilità di pioggia) usando i dati di temperatura e umidità dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="7038e-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="7038e-110">La probabilità di pioggia è l'output di un modello preparato di previsioni meteo.</span><span class="sxs-lookup"><span data-stu-id="7038e-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="7038e-111">Il modello usa dati cronologici per prevedere la probabilità di pioggia in base alla temperatura e all'umidità.</span><span class="sxs-lookup"><span data-stu-id="7038e-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7038e-112">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="7038e-112">What you do</span></span>

- <span data-ttu-id="7038e-113">Distribuire il modello di previsioni meteo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7038e-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="7038e-114">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="7038e-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="7038e-115">Creare un processo di Analisi di flusso e configurarlo per:</span><span class="sxs-lookup"><span data-stu-id="7038e-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="7038e-116">Leggere i dati di temperatura e umidità dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7038e-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="7038e-117">Chiamare il servizio Web per definire la probabilità di pioggia.</span><span class="sxs-lookup"><span data-stu-id="7038e-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="7038e-118">Salvare il risultato in un'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7038e-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="7038e-119">Usare Microsoft Azure Storage Explorer per visualizzare le previsioni meteo.</span><span class="sxs-lookup"><span data-stu-id="7038e-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7038e-120">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7038e-120">What you need</span></span>

- <span data-ttu-id="7038e-121">Completare l'esercitazione [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che prevede i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7038e-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="7038e-122">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="7038e-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="7038e-123">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7038e-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="7038e-124">Un'applicazione client che invia messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="7038e-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="7038e-125">Un account di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="7038e-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="7038e-126">([Prova gratuita di Machine Learning Studio](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="7038e-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="7038e-127">Distribuire il modello di previsioni meteo come servizio Web</span><span class="sxs-lookup"><span data-stu-id="7038e-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="7038e-128">Andare alla [pagina del modello di previsioni meteo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="7038e-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="7038e-129">Fare clic su **Apri in Studio** in Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="7038e-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="7038e-130">![Aprire la pagina del modello di previsioni meteo in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="7038e-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="7038e-131">Fare clic su **RUN** (Esegui) per convalidare i passaggi nel modello.</span><span class="sxs-lookup"><span data-stu-id="7038e-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="7038e-132">Il completamento di questo passaggio può richiedere fino a 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="7038e-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="7038e-133">![Aprire il modello di previsioni meteo in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7038e-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7038e-134">Fare clic su **SET UP WEB SERVICE** (Imposta servizio Web) > **Predictive Web Service** (Servizio Web predittivo).</span><span class="sxs-lookup"><span data-stu-id="7038e-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="7038e-135">![Distribuire il modello di previsioni meteo in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7038e-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7038e-136">Nel diagramma trascinare il modulo **Web service input** (Input servizio Web) accanto al modulo **Score Model** (Modello di punteggio).</span><span class="sxs-lookup"><span data-stu-id="7038e-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="7038e-137">Collegare il modulo **Web service input** (Input servizio Web) al modulo **Score Model** (Modello di punteggio).</span><span class="sxs-lookup"><span data-stu-id="7038e-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="7038e-138">![Collegare due moduli in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7038e-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7038e-139">Fare clic su **RUN** (Esegui) per convalidare i passaggi nel modello.</span><span class="sxs-lookup"><span data-stu-id="7038e-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="7038e-140">Fare clic su **DEPLOY WEB SERVICE** (Distribuisci servizio Web) per distribuire il modello come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7038e-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="7038e-141">Nel dashboard del modello scaricare **Excel 2010 or earlier workbook** (Cartella di lavoro di Excel 2010 o versioni precedenti) per **REQUEST/RESPONSE** (Richiesta/risposta).</span><span class="sxs-lookup"><span data-stu-id="7038e-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="7038e-142">Verificare di scaricare la cartella **Excel 2010 or earlier workbook** anche se nel computer è in esecuzione una versione di Excel successiva.</span><span class="sxs-lookup"><span data-stu-id="7038e-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Scaricare la cartella di lavoro di Excel per l'endpoint REQUEST/RESPONSE](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="7038e-144">Aprire la cartella di lavoro di Excel e annotare i valori **WEB SERVICE URL** (URL servizio Web) e **ACCESS KEY** (Chiave di accesso).</span><span class="sxs-lookup"><span data-stu-id="7038e-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="7038e-145">Configurare, configurare ed eseguire un processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7038e-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7038e-146">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7038e-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="7038e-147">Nel [portale di Azure](https://ms.portal.azure.com/) fare clic su **Nuovo** > **Internet delle cose** > **Processo di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="7038e-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="7038e-148">Immettere le seguenti informazioni per il processo.</span><span class="sxs-lookup"><span data-stu-id="7038e-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="7038e-149">**Nome processo**: il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="7038e-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="7038e-150">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="7038e-150">The name must be globally unique.</span></span>

   <span data-ttu-id="7038e-151">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7038e-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="7038e-152">**Percorso**: utilizzare lo stesso percorso del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7038e-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="7038e-153">**Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'hub IoT dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="7038e-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="7038e-155">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7038e-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="7038e-156">Aggiungere un input al processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7038e-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="7038e-157">Aprire il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7038e-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="7038e-158">In **Topologia processo** fare clic su **Input**.</span><span class="sxs-lookup"><span data-stu-id="7038e-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="7038e-159">Nel riquadro **Input** fare clic su **Aggiungi**, quindi immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7038e-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="7038e-160">**Alias di input**: l'alias univoco per l'input.</span><span class="sxs-lookup"><span data-stu-id="7038e-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="7038e-161">**Origine**: selezionare **Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="7038e-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="7038e-162">**Gruppo di consumer**: selezionare il gruppo di consumer creato.</span><span class="sxs-lookup"><span data-stu-id="7038e-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Aggiungere un input al processo di Analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="7038e-164">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7038e-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="7038e-165">Aggiungere un output al processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7038e-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="7038e-166">In **Topologia processo** fare clic su **Output**.</span><span class="sxs-lookup"><span data-stu-id="7038e-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="7038e-167">Nel riquadro **Output** fare clic su **Aggiungi**, quindi immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7038e-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="7038e-168">**Alias di output**: l'alias univoco per l'output.</span><span class="sxs-lookup"><span data-stu-id="7038e-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="7038e-169">**Sink**: selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="7038e-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="7038e-170">**Account di archiviazione**: l'account per l'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="7038e-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="7038e-171">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7038e-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="7038e-172">**Contenitore**: il contenitore in cui viene salvato l'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="7038e-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="7038e-173">È possibile usare un contenitore esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7038e-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="7038e-174">**Formato di serializzazione eventi**: selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="7038e-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Aggiungere un output al processo di Analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="7038e-176">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7038e-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="7038e-177">Aggiungere una funzione al processo di Analisi di flusso per chiamare il servizio Web che è stato distribuito</span><span class="sxs-lookup"><span data-stu-id="7038e-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="7038e-178">In **Topologia processo** fare clic su **Funzioni** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7038e-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="7038e-179">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7038e-179">Enter the following information:</span></span>

   <span data-ttu-id="7038e-180">**Alias della funzione**: immettere `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="7038e-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="7038e-181">**Tipo funzione**: selezionare **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="7038e-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="7038e-182">**Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="7038e-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="7038e-183">**URL**: immettere l'URL del servizio Web annotato dalla cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="7038e-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="7038e-184">**Chiave**: immettere la chiave di accesso annotata in precedenza dalla cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="7038e-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Aggiungere una funzione al processo di Analisi di flusso in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="7038e-186">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7038e-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="7038e-187">Configurare la query del processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7038e-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="7038e-188">In **Topologia processo** fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="7038e-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="7038e-189">Sostituire il codice esistente con il seguente:</span><span class="sxs-lookup"><span data-stu-id="7038e-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="7038e-190">Sostituire `[YourInputAlias]` con l'alias di input del processo.</span><span class="sxs-lookup"><span data-stu-id="7038e-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="7038e-191">Sostituire `[YourOutputAlias]` con l'alias di output del processo.</span><span class="sxs-lookup"><span data-stu-id="7038e-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="7038e-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7038e-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="7038e-193">Eseguire il processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7038e-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="7038e-194">Nel processo di analisi di flusso, **Avvia** > **Ora** > **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="7038e-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="7038e-195">Dopo aver avviato correttamente il processo, lo stato del processo passa da **Interrotto** a **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="7038e-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Eseguire il processo di Analisi di flusso](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="7038e-197">Usare Microsoft Azure Storage Explorer per visualizzare le previsioni meteo</span><span class="sxs-lookup"><span data-stu-id="7038e-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="7038e-198">Eseguire l'applicazione client per avviare la raccolta e l'invio dei dati di temperatura e umidità all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7038e-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="7038e-199">Ogni volta che l'hub IoT riceve un messaggio il processo di Analisi di flusso chiama il servizio Web di previsioni meteo per elaborare la probabilità di pioggia.</span><span class="sxs-lookup"><span data-stu-id="7038e-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="7038e-200">Il risultato viene quindi salvato nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7038e-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="7038e-201">Azure Storage Explorer è uno strumento che consente di visualizzare il risultato.</span><span class="sxs-lookup"><span data-stu-id="7038e-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="7038e-202">[Scaricare e installare Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7038e-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="7038e-203">Aprire Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="7038e-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="7038e-204">Accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="7038e-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="7038e-205">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7038e-205">Select your subscription.</span></span>
1. <span data-ttu-id="7038e-206">Fare clic sulla sottoscrizione in uso > **Account di archiviazione** > account di archiviazione in uso > **contenitori BLOB** > contenitore BLOB in uso.</span><span class="sxs-lookup"><span data-stu-id="7038e-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="7038e-207">Aprire il file con estensione csv per visualizzare il risultato.</span><span class="sxs-lookup"><span data-stu-id="7038e-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="7038e-208">L'ultima colonna registra la probabilità di pioggia.</span><span class="sxs-lookup"><span data-stu-id="7038e-208">The last column records the chance of rain.</span></span>

   ![Ottenere i risultati delle previsioni meteo con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="7038e-210">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7038e-210">Summary</span></span>

<span data-ttu-id="7038e-211">Azure Machine Learning è stato usato per stimare la probabilità di pioggia in base ai dati di temperatura e umidità ricevuti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7038e-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]