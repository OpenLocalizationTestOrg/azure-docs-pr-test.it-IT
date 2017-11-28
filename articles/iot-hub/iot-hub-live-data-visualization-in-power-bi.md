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
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="7c9ca-104">Visualizzare i dati del sensore in tempo reale da IoT Hub di Azure tramite Power BI</span><span class="sxs-lookup"><span data-stu-id="7c9ca-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="7c9ca-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7c9ca-106">What you learn</span></span>

<span data-ttu-id="7c9ca-107">Si apprenderà come toovisualize in tempo reale dati del sensore che riceve l'hub IoT di Azure da Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="7c9ca-108">Se si desidera visualizzare i dati hello tootry nell'hub IoT con le app Web, vedere [App Web di Azure usare toovisualize sensore in tempo reale dati IoT Hub Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ca-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7c9ca-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="7c9ca-109">What you do</span></span>

- <span data-ttu-id="7c9ca-110">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="7c9ca-111">Creare, configurare e di eseguire un processo di flusso Analitica per il trasferimento dei dati dal tooyour hub IoT account Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="7c9ca-112">Creare e pubblicare i dati del hello toovisualize report Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7c9ca-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7c9ca-113">What you need</span></span>

- <span data-ttu-id="7c9ca-114">Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="7c9ca-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="7c9ca-115">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="7c9ca-116">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="7c9ca-117">Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="7c9ca-118">Un account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-118">A Power BI account.</span></span> <span data-ttu-id="7c9ca-119">([Provare gratuitamente Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="7c9ca-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="7c9ca-120">Configurare, configurare ed eseguire un processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7c9ca-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7c9ca-121">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="7c9ca-122">In hello portale di Azure, fare clic su Nuovo > Internet of Things > processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="7c9ca-123">Immettere le seguenti informazioni per il processo di hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="7c9ca-124">**Nome del processo**: nome hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="7c9ca-125">nome Hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="7c9ca-126">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="7c9ca-127">**Percorso**: utilizzare hello stesso percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="7c9ca-128">**PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Creare un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="7c9ca-130">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="7c9ca-131">Aggiungere un processo di flusso Analitica toohello input</span><span class="sxs-lookup"><span data-stu-id="7c9ca-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="7c9ca-132">Processo di flusso Analitica hello aperto.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="7c9ca-133">In **Topologia processo** fare clic su **Input**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="7c9ca-134">In hello **input** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7c9ca-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="7c9ca-135">**Alias di input**: alias univoco hello hello input.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="7c9ca-136">**Origine**: selezionare **Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="7c9ca-137">**Gruppo di consumer**: gruppo di consumer hello selezionare appena creato.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="7c9ca-138">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-138">Click **Create**.</span></span>

   ![Aggiungere un processo di flusso Analitica tooa input in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="7c9ca-140">Aggiungere un processo di flusso Analitica toohello output</span><span class="sxs-lookup"><span data-stu-id="7c9ca-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="7c9ca-141">In **Topologia processo** fare clic su **Output**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="7c9ca-142">In hello **output** riquadro, fare clic su **Aggiungi**, quindi immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7c9ca-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="7c9ca-143">**Alias di output**: alias univoco di hello per l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="7c9ca-144">**Sink**: selezionare **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="7c9ca-145">Fare clic su **Autorizza** e quindi accedere all'account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="7c9ca-146">Una volta autorizzato, immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7c9ca-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="7c9ca-147">**Area di lavoro del gruppo**: selezionare l'area di lavoro del gruppo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="7c9ca-148">**Nome set di dati**: immettere un nome per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="7c9ca-149">**Nome tabella**: immettere un nome per la tabella.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="7c9ca-150">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-150">Click **Create**.</span></span>

   ![Aggiungere un processo di flusso Analitica tooa output in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="7c9ca-152">Configurare la query hello del processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="7c9ca-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="7c9ca-153">In **Topologia processo** fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="7c9ca-154">Sostituire `[YourInputAlias]` con alias hello di input del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="7c9ca-155">Sostituire `[YourOutputAlias]` con alias di output di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="7c9ca-156">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-156">Click **Save**.</span></span>

   ![Aggiungere un processo di flusso Analitica tooa query in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="7c9ca-158">Eseguire il processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="7c9ca-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="7c9ca-159">Nel processo di flusso Analitica hello, fare clic su **avviare** > **ora** > **avviare**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="7c9ca-160">Quando si avvia il processo di hello, lo stato del processo hello cambia da **arrestato** troppo**esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Eseguire un processo di analisi di flusso in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="7c9ca-162">Creare e pubblicare i dati del hello toovisualize report Power BI</span><span class="sxs-lookup"><span data-stu-id="7c9ca-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="7c9ca-163">Verificare che l'applicazione di esempio hello è in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="7c9ca-164">Se non è possibile fare riferimento di esercitazioni toohello in [configurare il dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="7c9ca-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="7c9ca-165">Accedi tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="7c9ca-166">Passare toohello gruppo dell'area di lavoro che durante la creazione di output di hello per il processo di flusso Analitica hello è impostata.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="7c9ca-167">Fare clic su **Set di dati in streaming**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="7c9ca-168">Dovrebbe essere hello elencato set di dati specificato al momento della creazione di output per il processo di flusso Analitica hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="7c9ca-169">In **azioni**, fare clic su hello prima icona toocreate un report.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Creare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="7c9ca-171">Creare una temperatura in tempo reale di grafico tooshow riga nel tempo.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="7c9ca-172">Nella pagina di creazione report hello, aggiungere un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="7c9ca-173">In hello **campi** riquadro espandere tabella hello specificato al momento della creazione di output di hello per il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="7c9ca-174">Trascinare **EventEnqueuedUtcTime** troppo**asse** su hello **visualizzazioni** riquadro.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="7c9ca-175">Trascinare **temperatura** troppo**valori**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="7c9ca-176">A questo punto viene creato un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-176">Now a line chart is created.</span></span> <span data-ttu-id="7c9ca-177">Hello asse x Visualizza la data e ora nel fuso orario UTC di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="7c9ca-178">asse y Hello Visualizza temperatura sensore hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Aggiungere un grafico a linee per temperatura tooa report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="7c9ca-180">Creare un'altra riga grafico tooshow in tempo reale umidità nel tempo.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="7c9ca-181">toodo, attenersi alla stessa procedura sopra hello e inserire **EventEnqueuedUtcTime** sull'asse delle x hello e **umidità** sull'asse y hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Aggiungere un grafico a linee per umidità tooa report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="7c9ca-183">Fare clic su **salvare** report hello toosave.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="7c9ca-184">Fare clic su **File** > **pubblicare tooweb**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="7c9ca-185">Fare clic su **Crea codice di incorporamento**, quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="7c9ca-186">Viene fornito collegamento al report hello che è possibile condividere con tutti gli utenti per l'accesso ai report e report di hello toointegrate di frammento di codice nel blog o nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Pubblicare un report di Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="7c9ca-188">Microsoft offre inoltre hello [App per dispositivi mobili di Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) per visualizzare e interagire con i dashboard di Power BI e i report nel dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c9ca-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c9ca-189">Next steps</span></span>

<span data-ttu-id="7c9ca-190">Utilizzati correttamente dati di Power BI toovisualize sensore in tempo reale dall'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="7c9ca-191">È un dati toovisualize alternativa provenienti dall'IoT Hub di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c9ca-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="7c9ca-192">Vedere [App Web di Azure usare toovisualize sensore in tempo reale dati IoT Hub Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ca-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
