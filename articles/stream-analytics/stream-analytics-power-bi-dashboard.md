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
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="c1790-104">Analisi di flusso e Power BI: dashboard di analisi in tempo reale per lo streaming dei dati</span><span class="sxs-lookup"><span data-stu-id="c1790-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="c1790-105">Azure Analitica di flusso consente tootake sfruttare uno dei principali strumenti di business intelligence, hello [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="c1790-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="c1790-106">Questo articolo illustra come creare strumenti di Business Intelligence usando Power BI come output per i processi di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="c1790-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="c1790-107">Verrà inoltre descritto come toocreate e utilizzare un dashboard in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="c1790-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="c1790-108">In questo articolo continua dal flusso Analitica hello [delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c1790-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="c1790-109">Esso si basa sul flusso di lavoro hello creato in tale esercitazione e si aggiunge un output in modo che è possibile visualizzare fraudolente chiamate telefoniche rilevati da un processo di Streaming Analitica di Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="c1790-110">È disponibile [un video](https://www.youtube.com/watch?v=SGUpT-a99MA) che illustra questo scenario.</span><span class="sxs-lookup"><span data-stu-id="c1790-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c1790-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c1790-111">Prerequisites</span></span>

<span data-ttu-id="c1790-112">Prima di iniziare, verificare di che aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="c1790-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="c1790-113">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="c1790-113">An Azure account.</span></span>
* <span data-ttu-id="c1790-114">Un account per Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-114">An account for Power BI.</span></span> <span data-ttu-id="c1790-115">È possibile usare un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c1790-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="c1790-116">Una versione completa di hello [delle frodi in tempo reale](stream-analytics-real-time-fraud-detection.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c1790-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="c1790-117">esercitazione di Hello include un'applicazione che genera metadati telefonata fittizio.</span><span class="sxs-lookup"><span data-stu-id="c1790-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="c1790-118">Nell'esercitazione di hello, creare un hub eventi e inviare hello streaming hub di eventi toohello dati chiamata telefonica.</span><span class="sxs-lookup"><span data-stu-id="c1790-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="c1790-119">Scrivere una query che rileva chiamate fraudolente (chiamate da hello stesso numero di hello stesso periodo di tempo in posizioni diverse).</span><span class="sxs-lookup"><span data-stu-id="c1790-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="c1790-120">Aggiungere l’output Power BI</span><span class="sxs-lookup"><span data-stu-id="c1790-120">Add Power BI output</span></span>
<span data-ttu-id="c1790-121">Nell'esercitazione di rilevamento di frodi in tempo reale hello, output di hello viene inviato tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="c1790-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="c1790-122">In questa sezione aggiungere un output che invia informazioni tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="c1790-123">Nel portale di Azure hello, aprire il processo di Streaming Analitica hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c1790-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="c1790-124">Se si utilizza nome suggerito hello, il processo di hello viene denominato `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="c1790-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="c1790-125">Seleziona hello **output** centro hello del dashboard processo hello e quindi selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c1790-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="c1790-126">In **Alias di output** immettere `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="c1790-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="c1790-127">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="c1790-127">You can use a different name.</span></span> <span data-ttu-id="c1790-128">In caso contrario, prendere nota di esso, in quanto è necessario il nome di hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c1790-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="c1790-129">In **Sink** selezionare **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c1790-129">Under **Sink**, select **Power BI**.</span></span>

   ![Creare un output per Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="c1790-131">Fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="c1790-131">Click **Authorize**.</span></span>

    <span data-ttu-id="c1790-132">Verrà visualizzata una finestra in cui è possibile specificare le credenziali di Azure per l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c1790-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Immettere le credenziali per l'accesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="c1790-134">Immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="c1790-134">Enter your credentials.</span></span> <span data-ttu-id="c1790-135">Tenere quindi quando si immette le credenziali, anche fornendo d'autorizzazione toohello Streaming Analitica processo tooaccess della superficie di Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="c1790-136">Quando si ritorna toohello **nuovo output** pannello immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c1790-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="c1790-137">**Gruppo dell'area di lavoro**: selezionare un'area di lavoro nel tenant di Power BI in cui si desidera toocreate hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="c1790-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="c1790-138">**Nome set di dati**: immettere `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="c1790-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="c1790-139">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="c1790-139">You can use a different name.</span></span> <span data-ttu-id="c1790-140">In questo caso prenderne nota perché servirà in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="c1790-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="c1790-141">**Nome tabella**: immettere `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="c1790-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="c1790-142">L'output di Power BI da processi di Analisi di flusso può avere al momento solo una tabella in un set di dati.</span><span class="sxs-lookup"><span data-stu-id="c1790-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Area di lavoro PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="c1790-144">Se Power BI dispone di un set di dati e tabella che dispone di hello stessi nomi hello quelle specificate nel processo di flusso Analitica hello, hello quelli esistenti viene sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="c1790-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="c1790-145">È consigliabile non creare in modo esplicito il set di dati e la tabella nell'account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="c1790-146">Vengono creati automaticamente quando si avvia il processo di flusso Analitica e hello inizia distribuzione output in Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="c1790-147">Se la query di processo non viene restituito alcun risultato, tabella e hello set di dati non vengono creati.</span><span class="sxs-lookup"><span data-stu-id="c1790-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="c1790-148">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c1790-148">Click **Create**.</span></span>

<span data-ttu-id="c1790-149">set di dati Hello viene creata con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="c1790-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="c1790-150">**defaultRetentionPolicy: BasicFIFO**: dati FIFO, con un massimo di 200.000 righe.</span><span class="sxs-lookup"><span data-stu-id="c1790-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="c1790-151">**defaultMode: pushStreaming**: hello dataset supporta streaming riquadri e gli oggetti visivi report tradizionali (anche noto come</span><span class="sxs-lookup"><span data-stu-id="c1790-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="c1790-152">push.</span><span class="sxs-lookup"><span data-stu-id="c1790-152">push).</span></span>

<span data-ttu-id="c1790-153">Attualmente non è possibile creare set di dati con altri flag.</span><span class="sxs-lookup"><span data-stu-id="c1790-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="c1790-154">Per ulteriori informazioni sui set di dati di Power BI, vedere hello [API REST di Power BI](https://msdn.microsoft.com/library/mt203562.aspx) riferimento.</span><span class="sxs-lookup"><span data-stu-id="c1790-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="c1790-155">Scrivere query hello</span><span class="sxs-lookup"><span data-stu-id="c1790-155">Write hello query</span></span>

1. <span data-ttu-id="c1790-156">Chiude hello **output** blade e blade processo toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="c1790-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="c1790-157">Fare clic su hello **Query** casella.</span><span class="sxs-lookup"><span data-stu-id="c1790-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="c1790-158">Immettere hello seguente query.</span><span class="sxs-lookup"><span data-stu-id="c1790-158">Enter hello following query.</span></span> <span data-ttu-id="c1790-159">Questa query è simile toohello self join creato nell'esercitazione di rilevamento di frodi hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="c1790-160">Hello differenza consiste nel fatto che questa query consente di inviare risultati toohello nuovo output creato (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="c1790-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="c1790-161">Se non si il nome hello input `CallStream` nell'esercitazione di rilevamento di frodi hello, sostituire il nome per `CallStream` in hello **FROM** e **JOIN** clausole query hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

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

4. <span data-ttu-id="c1790-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c1790-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="c1790-163">Query hello del test</span><span class="sxs-lookup"><span data-stu-id="c1790-163">Test hello query</span></span>
<span data-ttu-id="c1790-164">Questa sezione è facoltativa ma consigliata.</span><span class="sxs-lookup"><span data-stu-id="c1790-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="c1790-165">Se hello TelcoStreaming app non è attualmente in esecuzione, avviarlo attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c1790-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="c1790-166">Aprire una finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="c1790-166">Open a command window.</span></span>
    * <span data-ttu-id="c1790-167">Passare toohello cartella in cui sono telcogenerator.exe hello e i file modificati telcodatagen.exe.config.</span><span class="sxs-lookup"><span data-stu-id="c1790-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="c1790-168">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c1790-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="c1790-169">In hello **Query** pannello, fare clic su Avanti toohello di hello punti `CallStream` di input e quindi selezionare **dati da un input di esempio**.</span><span class="sxs-lookup"><span data-stu-id="c1790-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="c1790-170">Specificare che si desidera ottenere i dati di tre minuti e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1790-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="c1790-171">Attendere fino a quando non si riceverà una notifica che dati hello campionati.</span><span class="sxs-lookup"><span data-stu-id="c1790-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="c1790-172">Fare clic su **Test** e assicurarsi di ottenere i risultati.</span><span class="sxs-lookup"><span data-stu-id="c1790-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="c1790-173">Eseguire il processo di hello</span><span class="sxs-lookup"><span data-stu-id="c1790-173">Run hello job</span></span>

1. <span data-ttu-id="c1790-174">Verificare che tale app TelcoStreaming hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c1790-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="c1790-175">Chiude hello **Query** blade.</span><span class="sxs-lookup"><span data-stu-id="c1790-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="c1790-176">Nel Pannello di hello processo, fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="c1790-176">In hello job blade, click **Start**.</span></span>

    ![Avviare il processo di flusso Analitica hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="c1790-178">Il processo di Streaming Analitica inizia cercando fraudolente chiamate nel flusso in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="c1790-179">processo Hello inoltre creati set di dati hello e una tabella in Power BI e inizia a inviare i dati relativi a toothem chiamate fraudolenti hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="c1790-180">Creare dashboard hello in Power BI</span><span class="sxs-lookup"><span data-stu-id="c1790-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="c1790-181">Andare troppo[Powerbi.com](https://powerbi.com) e accedere con l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c1790-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="c1790-182">Query di processo di flusso Analitica hello restituisce risultati, vedrai che il set di dati è già stato creato:</span><span class="sxs-lookup"><span data-stu-id="c1790-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Streaming del set di dati in Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="c1790-184">Nell'area di lavoro fare clic su **+&nbsp;Crea**.</span><span class="sxs-lookup"><span data-stu-id="c1790-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![pulsante Crea Hello nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="c1790-186">Creare un nuovo dashboard e denominarlo `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="c1790-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Creare un dashboard e assegnargli un nome nell'area di lavoro di Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="c1790-188">Nella parte superiore di hello della finestra hello, fare clic su **Aggiungi riquadro**selezionare **dati in STREAMING personalizzati**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c1790-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Set di dati di streaming personalizzato](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="c1790-190">In **YOUR DATSETS** (SET DI DATI PERSONALI) selezionare il set di dati interessato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c1790-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Set di dati di streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="c1790-192">In **tipo di visualizzazione**selezionare **scheda**e quindi in hello **campi** elenco, selezionare **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="c1790-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Dettagli di visualizzazione per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="c1790-194">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c1790-194">Click **Next**.</span></span>

8. <span data-ttu-id="c1790-195">Immettere i dettagli del riquadro, ad esempio un titolo e un sottotitolo.</span><span class="sxs-lookup"><span data-stu-id="c1790-195">Fill in tile details like a title and subtitle.</span></span>

    ![Titolo e sottotitolo per il nuovo riquadro](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="c1790-197">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c1790-197">Click **Apply**.</span></span>

    <span data-ttu-id="c1790-198">Si dispone a questo punto di un contatore di frodi.</span><span class="sxs-lookup"><span data-stu-id="c1790-198">Now you have a fraud counter!</span></span>

    ![Contatore di frodi](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="c1790-200">Hello seguire i passaggi del nuovo tooadd un riquadro (a partire dal passaggio 4).</span><span class="sxs-lookup"><span data-stu-id="c1790-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="c1790-201">Questa volta, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1790-201">This time, do hello following:</span></span>

    * <span data-ttu-id="c1790-202">Quando si ottengono troppo**tipo di visualizzazione**selezionare **grafico a linee**.</span><span class="sxs-lookup"><span data-stu-id="c1790-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="c1790-203">Aggiungere un asse e selezionare **windowend**.</span><span class="sxs-lookup"><span data-stu-id="c1790-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="c1790-204">Aggiungere un valore e selezionare **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="c1790-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="c1790-205">Per **toodisplay finestra ora**selezionare hello ultimi 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="c1790-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Creare il riquadro per il grafico a linee](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="c1790-207">Fare clic su **Avanti**, aggiungere un titolo e un sottotitolo e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="c1790-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="c1790-208">dashboard di Power BI Hello ora offre due visualizzazioni dei dati sulle chiamate fraudolente come rilevato nel flusso di dati hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Dashboard di Power BI completo che mostra due riquadri per le chiamate fraudolente](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="c1790-210">Altre informazioni su Power BI</span><span class="sxs-lookup"><span data-stu-id="c1790-210">Learn more about Power BI</span></span>

<span data-ttu-id="c1790-211">Questa esercitazione viene illustrato come toocreate solo alcuni tipi di visualizzazioni per un set di dati.</span><span class="sxs-lookup"><span data-stu-id="c1790-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="c1790-212">Power BI consente di creare altri strumenti di business intelligence per clienti per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c1790-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="c1790-213">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="c1790-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="c1790-214">Per un altro esempio di un dashboard di Power BI, eseguire il controllo hello [Introduzione a Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span><span class="sxs-lookup"><span data-stu-id="c1790-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="c1790-215">Per ulteriori informazioni sulla configurazione di Streaming Analitica processo tooPower output BI e utilizzano i gruppi di Power BI, esaminare hello [Power BI](stream-analytics-define-outputs.md#power-bi) sezione di hello [Analitica di flusso di output](stream-analytics-define-outputs.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c1790-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="c1790-216">Per informazioni sull'utilizzo di Power BI in generale, vedere [Dashboard in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="c1790-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="c1790-217">Informazioni sulle limitazioni e le procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="c1790-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="c1790-218">Attualmente, è possibile chiamare Power BI approssimativamente una volta al secondo.</span><span class="sxs-lookup"><span data-stu-id="c1790-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="c1790-219">Gli oggetti visivi di streaming supportano pacchetti da 15 KB.</span><span class="sxs-lookup"><span data-stu-id="c1790-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="c1790-220">Tuttavia, gli oggetti visivi streaming esito negativo (ma push continua toowork).</span><span class="sxs-lookup"><span data-stu-id="c1790-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="c1790-221">A causa di queste limitazioni, Power BI si presta più naturalmente toocases in Azure flusso Analitica svolge un riduce il carico di dati in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="c1790-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="c1790-222">È consigliabile utilizzare una finestra a cascata o Hopping finestra tooensure che push di dati è al massimo un push al secondo e che la query inserita all'interno di requisiti di velocità effettiva di hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="c1790-223">È possibile utilizzare la finestra seguente equazione toocompute hello valore toogive hello in secondi:</span><span class="sxs-lookup"><span data-stu-id="c1790-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equazione 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="c1790-225">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c1790-225">For example:</span></span>

* <span data-ttu-id="c1790-226">Sono presenti 1.000 dispositivi che inviano dati a intervalli di un secondo.</span><span class="sxs-lookup"><span data-stu-id="c1790-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="c1790-227">Si sta utilizzando hello Power BI Pro SKU che supporta 1.000.000 di righe all'ora.</span><span class="sxs-lookup"><span data-stu-id="c1790-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="c1790-228">Si desidera quantità hello toopublish dei dati medi per ogni dispositivo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="c1790-229">Di conseguenza, l'equazione hello diventa:</span><span class="sxs-lookup"><span data-stu-id="c1790-229">As a result, hello equation becomes:</span></span>

![Equazione 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="c1790-231">In base a questa configurazione, è possibile modificare i seguenti toohello query originale di hello:</span><span class="sxs-lookup"><span data-stu-id="c1790-231">Given this configuration, you can change hello original query toohello following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="c1790-232">Rinnovare l'autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c1790-232">Renew authorization</span></span>
<span data-ttu-id="c1790-233">Password hello è stato modificato dopo il processo di creazione o dell'ultima autenticazione, è necessario tooreauthenticate account di Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="c1790-234">Se Azure multi-Factor Authentication è configurato per il tenant di Azure Active Directory (Azure AD), è necessario anche l'autorizzazione di Power BI toorenew ogni due settimane.</span><span class="sxs-lookup"><span data-stu-id="c1790-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="c1790-235">Se non viene rinnovata, si potrebbe verificare sintomi, ad esempio la mancanza di output del processo o un `Authenticate user error` nel log delle operazioni hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="c1790-236">Analogamente, se un processo viene avviato dopo hello token è scaduto, si verifica un errore e ha esito negativo processo hello.</span><span class="sxs-lookup"><span data-stu-id="c1790-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="c1790-237">tooresolve questo problema, arrestare il processo di hello che è in esecuzione e passare tooyour output di Power BI.</span><span class="sxs-lookup"><span data-stu-id="c1790-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="c1790-238">tooavoid perdita di dati, seleziona hello **rinnovare l'autorizzazione** collegamento e quindi riavviare il processo da hello **ora ultimo arresto**.</span><span class="sxs-lookup"><span data-stu-id="c1790-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="c1790-239">Dopo l'autorizzazione di hello è stato aggiornato con Power BI, verde viene visualizzato un avviso in hello autorizzazione area tooreflect che problema hello è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="c1790-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="c1790-240">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="c1790-240">Get help</span></span>
<span data-ttu-id="c1790-241">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c1790-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1790-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1790-242">Next steps</span></span>
* [<span data-ttu-id="c1790-243">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="c1790-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c1790-244">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c1790-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c1790-245">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c1790-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c1790-246">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c1790-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c1790-247">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c1790-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
