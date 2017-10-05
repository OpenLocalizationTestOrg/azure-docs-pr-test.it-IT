---
title: Visualizzazione in tempo reale dei dati del sensore dall'hub IoT di Azure - Power BI | Microsoft Docs
description: "Usare Power BI per visualizzare i dati di temperatura e umidità raccolti dal sensore e inviati all'hub IoT di Azure."
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
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="d8e71-104">Visualizzare i dati del sensore in tempo reale da IoT Hub di Azure tramite Power BI</span><span class="sxs-lookup"><span data-stu-id="d8e71-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="d8e71-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="d8e71-106">What you learn</span></span>

<span data-ttu-id="d8e71-107">Informazioni su come visualizzare i dati del sensore in tempo reale che l'hub IoT di Azure riceve da Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e71-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="d8e71-108">Se si desidera provare a visualizzare i dati nell'hub IoT con le app Web, consultare [Usare App Web di Azure per visualizzare i dati del sensore in tempo reale da Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d8e71-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d8e71-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="d8e71-109">What you do</span></span>

- <span data-ttu-id="d8e71-110">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="d8e71-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="d8e71-111">Creare, configurare ed eseguire un processo di analisi di flusso per il trasferimento dei dati dall'hub IoT all'account Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e71-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="d8e71-112">Creare e pubblicare un report di Power BI per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="d8e71-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d8e71-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="d8e71-113">What you need</span></span>

- <span data-ttu-id="d8e71-114">Completare l'esercitazione [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che prevede i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8e71-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="d8e71-115">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="d8e71-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="d8e71-116">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d8e71-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="d8e71-117">Un'applicazione client che invia messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e71-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="d8e71-118">Un account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e71-118">A Power BI account.</span></span> <span data-ttu-id="d8e71-119">([Provare gratuitamente Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="d8e71-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="d8e71-120">Configurare, configurare ed eseguire un processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d8e71-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="d8e71-121">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="d8e71-122">Nel portale di Azure, fare clic su Nuovo > Internet delle cose > Processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="d8e71-123">Immettere le seguenti informazioni per il processo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="d8e71-124">**Nome processo**: il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="d8e71-125">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="d8e71-125">The name must be globally unique.</span></span>

   <span data-ttu-id="d8e71-126">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d8e71-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="d8e71-127">**Percorso**: utilizzare lo stesso percorso del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d8e71-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="d8e71-128">**Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'hub IoT dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="d8e71-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="d8e71-130">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="d8e71-131">Aggiungere un input al processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d8e71-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="d8e71-132">Aprire il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="d8e71-133">In **Topologia processo** fare clic su **Input**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="d8e71-134">Nel riquadro **Input** fare clic su **Aggiungi**, quindi immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8e71-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="d8e71-135">**Alias di input**: l'alias univoco per l'input.</span><span class="sxs-lookup"><span data-stu-id="d8e71-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="d8e71-136">**Origine**: selezionare **Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="d8e71-137">**Gruppo di consumer**: selezionare il gruppo di consumer appena creato.</span><span class="sxs-lookup"><span data-stu-id="d8e71-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="d8e71-138">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-138">Click **Create**.</span></span>

   ![Aggiungere un input al processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="d8e71-140">Aggiungere un output al processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d8e71-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="d8e71-141">In **Topologia processo** fare clic su **Output**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="d8e71-142">Nel riquadro **Output** fare clic su **Aggiungi**, quindi immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8e71-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="d8e71-143">**Alias di output**: l'alias univoco per l'output.</span><span class="sxs-lookup"><span data-stu-id="d8e71-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="d8e71-144">**Sink**: selezionare **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="d8e71-145">Fare clic su **Autorizza** e quindi accedere all'account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e71-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="d8e71-146">Dopo aver concesso l'autorizzazione immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d8e71-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="d8e71-147">**Area di lavoro del gruppo**: selezionare l'area di lavoro del gruppo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d8e71-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="d8e71-148">**Nome set di dati**: immettere un nome per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="d8e71-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="d8e71-149">**Nome tabella**: immettere un nome per la tabella.</span><span class="sxs-lookup"><span data-stu-id="d8e71-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="d8e71-150">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-150">Click **Create**.</span></span>

   ![Aggiungere un output al processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="d8e71-152">Configurare la query del processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d8e71-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="d8e71-153">In **Topologia processo** fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="d8e71-154">Sostituire `[YourInputAlias]` con l'alias di input del processo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="d8e71-155">Sostituire `[YourOutputAlias]` con l'alias di output del processo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="d8e71-156">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-156">Click **Save**.</span></span>

   ![Aggiungere una query al processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="d8e71-158">Eseguire il processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d8e71-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="d8e71-159">Nel processo di analisi di flusso, **Avvia** > **Ora** > **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="d8e71-160">Dopo aver avviato correttamente il processo, lo stato del processo passa da **Interrotto** a **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Eseguire un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="d8e71-162">Creare e pubblicare un report di Power BI per visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="d8e71-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="d8e71-163">Verificare che l'applicazione di esempio sia in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="d8e71-164">Se non lo fosse, è possibile fare riferimento alle esercitazioni descritte in [Configurare il dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="d8e71-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="d8e71-165">Accedere all'account [Power BI](https://powerbi.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="d8e71-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="d8e71-166">Passare all'area di lavoro del gruppo impostata quando è stato creato l'output del processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="d8e71-167">Fare clic su **Set di dati in streaming**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="d8e71-168">Dovrebbero essere elencati i set di dati specificati durante la creazione di output per il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="d8e71-169">In **AZIONI**, fare clic sulla prima icona per creare un report.</span><span class="sxs-lookup"><span data-stu-id="d8e71-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Creare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="d8e71-171">Creare un grafico a linee per visualizzare la temperatura in tempo reale nel tempo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="d8e71-172">Nella pagina di creazione del report, aggiungere un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="d8e71-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="d8e71-173">Nel riquadro **Campi** espandere la tabella specificata durante la creazione di output per il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="d8e71-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="d8e71-174">Trascinare **EventEnqueuedUtcTime** in **Asse** sul riquadro **Visualizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="d8e71-175">Trascinare la **temperatura** in **Valori**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="d8e71-176">A questo punto viene creato un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="d8e71-176">Now a line chart is created.</span></span> <span data-ttu-id="d8e71-177">L'asse x mostra data e ora per il fuso orario UTC.</span><span class="sxs-lookup"><span data-stu-id="d8e71-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="d8e71-178">L'asse y mostra la temperatura dal sensore.</span><span class="sxs-lookup"><span data-stu-id="d8e71-178">The y-axis displays temperature from the sensor.</span></span>

      ![Aggiungere un grafico a linee per la temperatura a un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="d8e71-180">Creare un altro grafico a linee in modo da visualizzare in tempo reale l'umidità nel tempo.</span><span class="sxs-lookup"><span data-stu-id="d8e71-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="d8e71-181">A tale scopo, attenersi alla stessa procedura precedente e inserire **EventEnqueuedUtcTime** sull'asse x e l'**umidità** sull'asse y.</span><span class="sxs-lookup"><span data-stu-id="d8e71-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Aggiungere un grafico a linee per l'umidità a un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="d8e71-183">Fare clic su **Salva** per salvare il report.</span><span class="sxs-lookup"><span data-stu-id="d8e71-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="d8e71-184">Fare clic su **File** > **Pubblica sul Web**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="d8e71-185">Fare clic su **Crea codice di incorporamento**, quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d8e71-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="d8e71-186">Viene indicato il collegamento al report che è possibile condividere con utenti che debbano accedere al report e un frammento di codice per integrare il report nel blog o nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="d8e71-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Pubblicare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="d8e71-188">Microsoft offre anche le [App per dispositivi mobili di Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) per la visualizzazione e l'interazione con i dashboard di Power BI e i report sul tuo dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="d8e71-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8e71-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8e71-189">Next steps</span></span>

<span data-ttu-id="d8e71-190">Si è utilizzato correttamente Power BI per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e71-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="d8e71-191">Esiste un modo alternativo per visualizzare i dati dall'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e71-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="d8e71-192">Vedere [Usare App Web di Azure per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d8e71-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
