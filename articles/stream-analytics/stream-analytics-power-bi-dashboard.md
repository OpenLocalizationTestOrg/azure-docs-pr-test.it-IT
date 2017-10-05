---
title: Dashboard di Power BI in Analisi di flusso di Azure | Microsoft Docs
description: Utilizzare un dashboard di Power BI streaming in tempo reale per raccogliere intelligence aziendali e analizzare i dati di volumi elevati di un processo di Analisi di flusso.
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
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="b7c1e-104">Analisi di flusso e Power BI: dashboard di analisi in tempo reale per lo streaming dei dati</span><span class="sxs-lookup"><span data-stu-id="b7c1e-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="b7c1e-105">Analisi di flusso di Azure permette di usare uno dei principali strumenti di Business Intelligence, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="b7c1e-106">Questo articolo illustra come creare strumenti di Business Intelligence usando Power BI come output per i processi di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="b7c1e-107">Illustra anche come creare e usare un dashboard in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="b7c1e-108">Questo articolo continua dall'esercitazione sul [rilevamento delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md) in Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="b7c1e-109">Esso si basa sul flusso di lavoro creato in tale esercitazione e aggiunge un output di Power BI in modo che sia possibile visualizzare le chiamate telefoniche fraudolente rilevate da un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="b7c1e-110">È disponibile [un video](https://www.youtube.com/watch?v=SGUpT-a99MA) che illustra questo scenario.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b7c1e-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b7c1e-111">Prerequisites</span></span>

<span data-ttu-id="b7c1e-112">Prima di iniziare, verificare di disporre degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="b7c1e-113">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-113">An Azure account.</span></span>
* <span data-ttu-id="b7c1e-114">Un account per Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-114">An account for Power BI.</span></span> <span data-ttu-id="b7c1e-115">È possibile usare un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="b7c1e-116">Una versione completata dell'esercitazione sul [rilevamento delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="b7c1e-117">L'esercitazione include un'app che genera metadati di telefonate fittizie.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="b7c1e-118">Nell'esercitazione si crea un hub eventi e si inviano i dati delle telefonate all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="b7c1e-119">Si scrive una query che rileva le chiamate fraudolente (chiamate effettuate dallo stesso numero nello stesso momento da posizioni diverse).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="b7c1e-120">Aggiungere l’output Power BI</span><span class="sxs-lookup"><span data-stu-id="b7c1e-120">Add Power BI output</span></span>
<span data-ttu-id="b7c1e-121">Nell'esercitazione sul rilevamento delle frodi in tempo reale l'output viene inviato all'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="b7c1e-122">In questa sezione si aggiunge un output che invia informazioni a Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="b7c1e-123">Nel portale di Azure aprire il processo di Analisi di flusso creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="b7c1e-124">Se si usa il nome suggerito, il processo è denominato `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="b7c1e-125">Selezionare la casella **Output** al centro del dashboard del processo e quindi selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="b7c1e-126">In **Alias di output** immettere `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="b7c1e-127">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-127">You can use a different name.</span></span> <span data-ttu-id="b7c1e-128">In questo caso, tenerne traccia, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="b7c1e-129">In **Sink** selezionare **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-129">Under **Sink**, select **Power BI**.</span></span>

   ![Creare un output per Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="b7c1e-131">Fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-131">Click **Authorize**.</span></span>

    <span data-ttu-id="b7c1e-132">Verrà visualizzata una finestra in cui è possibile specificare le credenziali di Azure per l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Immettere le credenziali per l'accesso a Power BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="b7c1e-134">Immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-134">Enter your credentials.</span></span> <span data-ttu-id="b7c1e-135">È necessario considerare che quando si immettono le credenziali, si autorizza il processo di Analisi di flusso ad accedere all'area di Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="b7c1e-136">Quando si torna al pannello **Nuovo output** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="b7c1e-137">**Area di lavoro del gruppo**: selezionare un'area di lavoro nel tenant Power BI in cui si desidera creare il set di dati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="b7c1e-138">**Nome set di dati**: immettere `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="b7c1e-139">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-139">You can use a different name.</span></span> <span data-ttu-id="b7c1e-140">In questo caso prenderne nota perché servirà in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="b7c1e-141">**Nome tabella**: immettere `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="b7c1e-142">L'output di Power BI da processi di Analisi di flusso può avere al momento solo una tabella in un set di dati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Area di lavoro PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="b7c1e-144">Se Power BI dispone di un set di dati e di una tabella con gli stessi nomi specificati nel processo di Analisi di flusso, i dati esistenti vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="b7c1e-145">È consigliabile non creare in modo esplicito il set di dati e la tabella nell'account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="b7c1e-146">Vengono creati automaticamente quando il processo di Analisi di flusso viene avviato e inizia a generare output in Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="b7c1e-147">Se la query del processo non genera alcun risultato, il set di dati e la tabella non vengono creati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="b7c1e-148">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-148">Click **Create**.</span></span>

<span data-ttu-id="b7c1e-149">Il set di dati viene creato con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="b7c1e-150">**defaultRetentionPolicy: BasicFIFO**: dati FIFO, con un massimo di 200.000 righe.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="b7c1e-151">**defaultMode: pushStreaming**: il set di dati supporta sia i riquadri in streaming che gli oggetti visivi tradizionali basati sui report, detti anche</span><span class="sxs-lookup"><span data-stu-id="b7c1e-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="b7c1e-152">push.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-152">push).</span></span>

<span data-ttu-id="b7c1e-153">Attualmente non è possibile creare set di dati con altri flag.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="b7c1e-154">Per altre informazioni sui set di dati di Power BI, vedere le informazioni di riferimento sull'[API REST di Power BI](https://msdn.microsoft.com/library/mt203562.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="b7c1e-155">Scrivere la query</span><span class="sxs-lookup"><span data-stu-id="b7c1e-155">Write the query</span></span>

1. <span data-ttu-id="b7c1e-156">Chiudere il pannello **Output** e tornare al pannello del processo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="b7c1e-157">Fare clic sulla casella **Query**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="b7c1e-158">Immettere la query seguente.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-158">Enter the following query.</span></span> <span data-ttu-id="b7c1e-159">Questa query è simile alla query self-join che è stata creata nell'esercitazione sul rilevamento delle frodi.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="b7c1e-160">La differenza è che questa query invia i risultati al nuovo output creato (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="b7c1e-161">Se non è stato assegnato un nome all'input `CallStream` nell'esercitazione sul rilevamento delle frodi, sostituire il nome per `CallStream` nelle clausole **FROM** e **JOIN** della query.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="b7c1e-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="b7c1e-163">Testare la query</span><span class="sxs-lookup"><span data-stu-id="b7c1e-163">Test the query</span></span>
<span data-ttu-id="b7c1e-164">Questa sezione è facoltativa ma consigliata.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="b7c1e-165">Se l'app TelcoStreaming non è attualmente in esecuzione, avviarla seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="b7c1e-166">Aprire una finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-166">Open a command window.</span></span>
    * <span data-ttu-id="b7c1e-167">Passare alla cartella in cui si trovano il file telcogenerator.exe e il file modificato telcodatagen.exe.config.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="b7c1e-168">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="b7c1e-169">Nel pannello **Query** fare clic sui puntini di sospensione accanto all'input `CallStream` e quindi selezionare **Campiona dati da input**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="b7c1e-170">Specificare che si desidera ottenere i dati di tre minuti e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="b7c1e-171">Attendere fino a quando non si riceve la notifica che i dati sono stati campionati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="b7c1e-172">Fare clic su **Test** e assicurarsi di ottenere i risultati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="b7c1e-173">Eseguire il processo</span><span class="sxs-lookup"><span data-stu-id="b7c1e-173">Run the job</span></span>

1. <span data-ttu-id="b7c1e-174">Assicurarsi che l'app TelcoStreaming sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="b7c1e-175">Chiudere il pannello **Query**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="b7c1e-176">Nel pannello del processo fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-176">In the job blade, click **Start**.</span></span>

    ![Avviare il processo di analisi di flusso](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="b7c1e-178">Il processo di Analisi di flusso inizia a cercare le chiamate fraudolente nel flusso in ingresso.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="b7c1e-179">Il processo crea anche il set di dati e la tabella in Power BI e inizia a inviare loro i dati relativi alle chiamate fraudolente.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="b7c1e-180">Creare il dashboard in Power BI</span><span class="sxs-lookup"><span data-stu-id="b7c1e-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="b7c1e-181">Passare a [Powerbi.com](https://powerbi.com) e accedere con l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="b7c1e-182">Se la query del processo di Analisi di flusso produce risultati, si noterà che il set di dati è già creato:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Streaming del set di dati in Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="b7c1e-184">Nell'area di lavoro fare clic su **+&nbsp;Crea**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Pulsante Crea nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="b7c1e-186">Creare un nuovo dashboard e denominarlo `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Creare un dashboard e assegnargli un nome nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="b7c1e-188">Nella parte superiore della finestra, fare clic su **Aggiungi riquadro**, selezionare **DATI IN STREAMING PERSONALIZZATI**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Set di dati di streaming personalizzato](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="b7c1e-190">In **YOUR DATSETS** (SET DI DATI PERSONALI) selezionare il set di dati interessato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Set di dati di streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="b7c1e-192">In **Tipo di visualizzazione** selezionare **Scheda** e quindi nell'elenco **Campi** selezionare **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![Dettagli di visualizzazione per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="b7c1e-194">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-194">Click **Next**.</span></span>

8. <span data-ttu-id="b7c1e-195">Immettere i dettagli del riquadro, ad esempio un titolo e un sottotitolo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-195">Fill in tile details like a title and subtitle.</span></span>

    ![Titolo e sottotitolo per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="b7c1e-197">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-197">Click **Apply**.</span></span>

    <span data-ttu-id="b7c1e-198">Si dispone a questo punto di un contatore di frodi.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-198">Now you have a fraud counter!</span></span>

    ![Contatore di frodi](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="b7c1e-200">Seguire di nuovo la procedura per aggiungere un riquadro (partendo dal passaggio 4).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="b7c1e-201">Questa volta eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-201">This time, do the following:</span></span>

    * <span data-ttu-id="b7c1e-202">Quando si accede a **Tipo di visualizzazione** selezionare **Grafico a linee**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="b7c1e-203">Aggiungere un asse e selezionare **windowend**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="b7c1e-204">Aggiungere un valore e selezionare **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="b7c1e-205">Per **Intervallo di tempo da visualizzare**  selezionare gli ultimi 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![Creare il riquadro per il grafico a linee](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="b7c1e-207">Fare clic su **Avanti**, aggiungere un titolo e un sottotitolo e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="b7c1e-208">Il dashboard di Power BI offre ora due visualizzazioni di dati sulle chiamate fraudolente in base al rilevamento nei dati di streaming.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![Dashboard di Power BI completo che mostra due riquadri per le chiamate fraudolente](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="b7c1e-210">Altre informazioni su Power BI</span><span class="sxs-lookup"><span data-stu-id="b7c1e-210">Learn more about Power BI</span></span>

<span data-ttu-id="b7c1e-211">Questa esercitazione mostra come creare solo alcuni tipi di visualizzazioni per un set di dati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="b7c1e-212">Power BI consente di creare altri strumenti di business intelligence per clienti per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="b7c1e-213">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="b7c1e-214">Per visualizzare un altro esempio di dashboard Power BI, guardare il video [Introduzione a Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) .</span><span class="sxs-lookup"><span data-stu-id="b7c1e-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="b7c1e-215">Per altre informazioni sulla configurazione dell'output di Analisi di flusso in Power BI e sull'uso dei gruppi di Power BI, vedere la sezione [Power BI](stream-analytics-define-outputs.md#power-bi) dell'articolo relativo agli [output di Analisi di flusso](stream-analytics-define-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="b7c1e-216">Per informazioni sull'utilizzo di Power BI in generale, vedere [Dashboard in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="b7c1e-217">Informazioni sulle limitazioni e le procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="b7c1e-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="b7c1e-218">Attualmente, è possibile chiamare Power BI approssimativamente una volta al secondo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="b7c1e-219">Gli oggetti visivi di streaming supportano pacchetti da 15 KB.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="b7c1e-220">Oltre tale limite, gli oggetti visivi di streaming hanno esito negativo, ma il push continua a funzionare.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="b7c1e-221">A causa di queste limitazioni, Power BI è più adatto ai casi in cui Analisi di flusso di Azure riduce notevolmente il carico di dati.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="b7c1e-222">È consigliabile usare la finestra a cascata o la finestra di salto per assicurarsi che il push di dati avvenga al massimo una volta al secondo e che la query rientri nei requisiti di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="b7c1e-223">Per calcolare il valore e visualizzare la finestra in secondi, è possibile usare questa equazione:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Equazione 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="b7c1e-225">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-225">For example:</span></span>

* <span data-ttu-id="b7c1e-226">Sono presenti 1.000 dispositivi che inviano dati a intervalli di un secondo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="b7c1e-227">Si usa lo SKU di Power BI Pro che supporta 1.000.000 righe l'ora.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="b7c1e-228">Si vuole pubblicare la quantità di dati medi per ogni dispositivo in Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="b7c1e-229">L'equazione diventa quindi la seguente:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-229">As a result, the equation becomes:</span></span>

![Equazione 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="b7c1e-231">Con questa configurazione è possibile modificare la query originale come segue:</span><span class="sxs-lookup"><span data-stu-id="b7c1e-231">Given this configuration, you can change the original query to the following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="b7c1e-232">Rinnovare l'autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b7c1e-232">Renew authorization</span></span>
<span data-ttu-id="b7c1e-233">Se la password è stata modificata dopo la creazione o l'ultima autenticazione del processo, è necessario autenticare nuovamente l'account Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="b7c1e-234">Se Azure Multi-Factor Authentication è configurato nel tenant di Azure Active Directory (Azure AD), è anche necessario rinnovare l'autorizzazione di Power BI ogni due settimane.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="b7c1e-235">Se non viene rinnovata, si potrebbero verificare problemi come la mancanza di output dei processi o un `Authenticate user error` nei log delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="b7c1e-236">Se si tenta di avviare un processo dopo che il token è scaduto, si verifica un errore e l'avvio del processo ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="b7c1e-237">Per risolvere questo problema, arrestare il processo in esecuzione e passare all'output di Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="b7c1e-238">Per evitare la perdita di dati, fare clic sul collegamento **Rinnova autorizzazione** e riavviare il processo selezionando **Ora ultimo arresto**.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="b7c1e-239">Dopo aver aggiornato l'autorizzazione con Power BI, viene visualizzato un avviso verde nell'area di autorizzazione che indica che il problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="b7c1e-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="b7c1e-240">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="b7c1e-240">Get help</span></span>
<span data-ttu-id="b7c1e-241">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b7c1e-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7c1e-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7c1e-242">Next steps</span></span>
* [<span data-ttu-id="b7c1e-243">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b7c1e-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b7c1e-244">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b7c1e-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b7c1e-245">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b7c1e-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b7c1e-246">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b7c1e-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b7c1e-247">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b7c1e-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
