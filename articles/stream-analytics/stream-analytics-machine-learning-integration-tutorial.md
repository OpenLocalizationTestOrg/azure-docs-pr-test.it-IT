---
title: Integrazione di Analisi di flusso di Azure e Machine Learning | Documentazione Microsoft
description: Come usare una funzione definita dall'utente e Machine Learning in un processo di analisi di flusso
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="e23e7-103">Analisi del sentiment con Analisi di flusso di Azure e Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e23e7-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="e23e7-104">Questo articolo descrive come configurare rapidamente un semplice processo di Analisi di flusso di Azure che integra Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e23e7-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="e23e7-105">Verrà usato un modello di Machine Learning per l'analisi del sentiment proveniente dalla raccolta Cortana Intelligence per analizzare il flusso di dati di testo e determinare il punteggio del sentiment in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="e23e7-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="e23e7-106">Cortana Intelligence Suite consente di eseguire questa operazione senza doversi preoccupare delle complessità della creazione di un modello di analisi del sentiment.</span><span class="sxs-lookup"><span data-stu-id="e23e7-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="e23e7-107">È possibile applicare le informazioni apprese in questo articolo a scenari come i seguenti:</span><span class="sxs-lookup"><span data-stu-id="e23e7-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="e23e7-108">Analisi in tempo reale del sentiment su flussi di dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="e23e7-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="e23e7-109">Analisi dei record delle chat dei client con il personale di supporto.</span><span class="sxs-lookup"><span data-stu-id="e23e7-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="e23e7-110">Valutazione dei commenti per forum, blog e video.</span><span class="sxs-lookup"><span data-stu-id="e23e7-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="e23e7-111">Molti altri scenari di punteggio predittivo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="e23e7-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="e23e7-112">In uno scenario reale, si potrebbero ottenere i dati direttamente da un flusso di dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="e23e7-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="e23e7-113">Per semplificare la presentazione, l'esercitazione è stata scritta in modo che il processo di Analisi di flusso ottenga i tweet da un file CSV in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e23e7-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="e23e7-114">È possibile creare un file CSV personalizzato oppure usare un file CSV di esempio, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="e23e7-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![tweet di esempio in un file CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="e23e7-116">Il processo di Analisi di flusso creato applica il modello di analisi del sentiment come funzione definita dall'utente (UDF) ai dati del testo di esempio dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e23e7-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="e23e7-117">L'output (il risultato dell'analisi del sentiment) viene scritto nello stesso archivio BLOB in un file CSV diverso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="e23e7-118">La figura seguente illustra questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="e23e7-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="e23e7-119">Come indicato, per uno scenario più realistico è possibile sostituire l'archivio BLOB con il flusso di dati di Twitter provenienti da un input di Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e23e7-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="e23e7-120">È anche possibile compilare una visualizzazione in tempo reale del sentimento di aggregazione in [Microsoft Power BI](https://powerbi.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="e23e7-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Panoramica dell'integrazione di Machine Learning in Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="e23e7-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e23e7-122">Prerequisites</span></span>
<span data-ttu-id="e23e7-123">Prima di iniziare, verificare di disporre degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e23e7-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="e23e7-124">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="e23e7-124">An active Azure subscription.</span></span>
* <span data-ttu-id="e23e7-125">Un file CSV contenente alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="e23e7-125">A CSV file with some data in it.</span></span> <span data-ttu-id="e23e7-126">È possibile scaricare il file mostrato in precedenza da [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv) oppure creare un file personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e23e7-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="e23e7-127">In questo articolo si presuppone l'uso del file da GitHub.</span><span class="sxs-lookup"><span data-stu-id="e23e7-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="e23e7-128">In generale, per completare le attività illustrate in questo articolo, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e23e7-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="e23e7-129">Creare un account di archiviazione di Azure e un contenitore di archiviazione BLOB, quindi caricare un file di input in formato CSV nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="e23e7-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="e23e7-130">Aggiungere un modello di analisi del sentiment dalla raccolta Cortana Intelligence all'area di lavoro di Azure Machine Learning e distribuire questo modello come servizio Web nell'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e23e7-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="e23e7-131">Creare un processo di Analisi di flusso che chiami questo servizio Web come funzione per determinare il sentiment per l'input di testo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="e23e7-132">Avviare il processo di Analisi di flusso e controllare l'output.</span><span class="sxs-lookup"><span data-stu-id="e23e7-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="e23e7-133">Creare un contenitore di archiviazione e caricare il file di input CSV</span><span class="sxs-lookup"><span data-stu-id="e23e7-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="e23e7-134">Per questo passaggio, è possibile usare qualsiasi file CSV, ad esempio quello disponibile da GitHub.</span><span class="sxs-lookup"><span data-stu-id="e23e7-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="e23e7-135">Nel portale di Azure fare clic su **Nuovo** &gt; **Archiviazione** &gt; **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![creare un nuovo account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="e23e7-137">Specificare un nome (`samldemo` nell'esempio).</span><span class="sxs-lookup"><span data-stu-id="e23e7-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="e23e7-138">Il nome può contenere solo lettere minuscole e numeri e deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="e23e7-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="e23e7-139">Specificare un gruppo di risorse esistente e specificare un percorso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="e23e7-140">Per quanto riguarda il percorso, è consigliabile che tutte le risorse create in questa esercitazione usino lo stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![specificare i dettagli dell'account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="e23e7-142">Selezionare l'account di archiviazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e23e7-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="e23e7-143">Nel pannello dell'account di archiviazione fare clic su **Contenitori** e quindi su **+&nbsp;Contenitore** per creare un archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e23e7-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![Creare un contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="e23e7-145">Specificare quindi un nome per il contenitore (`azuresamldemoblob` nell'esempio) e verificare che **Tipo di accesso** sia impostato su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="e23e7-146">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-146">When you're done, click **OK**.</span></span>

    ![specificare i dettagli del contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="e23e7-148">Nel pannello **Contenitori** selezionare il nuovo contenitore, in modo da aprire il pannello per tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="e23e7-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="e23e7-149">Fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-149">Click **Upload**.</span></span>

    ![Pulsante 'Carica' per un contenitore](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="e23e7-151">Nel pannello **Carica BLOB** specificare il file CSV che si vuole usare per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e23e7-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="e23e7-152">In **Tipo BLOB** selezionare **BLOB in blocchi** e impostare le dimensioni del blocco su 4 MB, sufficienti per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e23e7-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![caricare il file BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="e23e7-154">Fare clic sul pulsante **Carica** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="e23e7-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="e23e7-155">Aggiungere il modello di analisi dei sentimenti dalla raccolta Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="e23e7-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="e23e7-156">Ora che i dati di esempio sono in un BLOB, è possibile abilitare il modello di analisi del sentiment nella raccolta Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="e23e7-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="e23e7-157">Passare alla pagina del [modello di analisi predittiva del sentiment](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) nella raccolta Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="e23e7-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="e23e7-158">Fare clic su **Open in Studio** (Apri in Studio).</span><span class="sxs-lookup"><span data-stu-id="e23e7-158">Click **Open in Studio**.</span></span>  
   
   ![Analisi di flusso e Machine Learning, aprire Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="e23e7-160">Effettuare l'accesso per passare all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e23e7-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="e23e7-161">Selezionare una località.</span><span class="sxs-lookup"><span data-stu-id="e23e7-161">Select a location.</span></span>

4. <span data-ttu-id="e23e7-162">Fare clic su **Esegui** in basso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="e23e7-163">Il processo viene eseguito e richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="e23e7-163">The process runs, which takes about a minute.</span></span>

   ![eseguire l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="e23e7-165">Al termine dell'esecuzione del processo, selezionare **Deploy Web Service** (Distribuisci servizio Web) nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="e23e7-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![distribuire l'esperimento in Machine Learning Studio come servizio Web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="e23e7-167">Per verificare che il modello di analisi del sentiment sia pronto per l'uso, fare clic sul pulsante **Test**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="e23e7-168">Immettere testo, ad esempio "Mi piace Microsoft".</span><span class="sxs-lookup"><span data-stu-id="e23e7-168">Provide text input such as "I love Microsoft".</span></span> 

   ![testare l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="e23e7-170">Se il test funziona, viene visualizzato un risultato simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e23e7-170">If the test works, you see a result similar to the following example:</span></span>

   ![risultati del test in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="e23e7-172">Nella colonna **Apps** (App) fare clic sul collegamento **Excel 2010 or earlier workbook** (Cartella di lavoro di Excel 2010 o versione precedente) per scaricare una cartella di Excel.</span><span class="sxs-lookup"><span data-stu-id="e23e7-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="e23e7-173">La cartella di lavoro contiene la chiave API e l'URL necessari in seguito per configurare il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Analisi di flusso e Machine Learning, panoramica rapida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="e23e7-175">Creare un processo di Analisi di flusso che usi il modello di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e23e7-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="e23e7-176">È ora possibile creare un processo di Analisi di flusso che legge i tweet di esempio dal file CSV nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e23e7-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="e23e7-177">Creare il processo</span><span class="sxs-lookup"><span data-stu-id="e23e7-177">Create the job</span></span>

1. <span data-ttu-id="e23e7-178">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e23e7-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="e23e7-179">Fare clic su **Nuovo** > **Internet delle cose** > **Processo di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Percorso del portale di Azure per ottenere un nuovo processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="e23e7-181">Assegnare il nome `azure-sa-ml-demo` al processo, specificare una sottoscrizione, specificare un gruppo di risorse esistente o crearne uno nuovo e selezionare il percorso per il processo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![specificare le impostazioni per il nuovo processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="e23e7-183">Configurare l'input del processo</span><span class="sxs-lookup"><span data-stu-id="e23e7-183">Configure the job input</span></span>
<span data-ttu-id="e23e7-184">Il processo ottiene l'input dal file CSV caricato in precedenza nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e23e7-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="e23e7-185">Dopo aver creato il processo, in **Topologia processo** nel pannello del processo, fare clic sulla casella **Input**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![Casella 'Input' nel pannello del processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="e23e7-187">Nel pannello **Input** fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![Pulsante 'Aggiungi' per aggiungere un input al processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="e23e7-189">Compilare il pannello **Nuovo input** con questi valori:</span><span class="sxs-lookup"><span data-stu-id="e23e7-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="e23e7-190">**Alias di input**: usare il nome `datainput`.</span><span class="sxs-lookup"><span data-stu-id="e23e7-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="e23e7-191">**Tipo di origine**: selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="e23e7-192">**Origine**: selezionare **Archiviazione BLOB**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="e23e7-193">**Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="e23e7-194">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-194">**Storage account**.</span></span> <span data-ttu-id="e23e7-195">Selezionare l'account di archiviazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e23e7-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="e23e7-196">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-196">**Container**.</span></span> <span data-ttu-id="e23e7-197">Selezionare il contenitore creato in precedenza (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="e23e7-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="e23e7-198">**Formato di serializzazione eventi**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-198">**Event serialization format**.</span></span> <span data-ttu-id="e23e7-199">Selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-199">Select **CSV**.</span></span>

    ![Impostazioni per il nuovo input del processo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="e23e7-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="e23e7-202">Configurare l'output del processo</span><span class="sxs-lookup"><span data-stu-id="e23e7-202">Configure the job output</span></span>
<span data-ttu-id="e23e7-203">Il processo invia i risultati allo stesso archivio BLOB da cui ottiene l'input.</span><span class="sxs-lookup"><span data-stu-id="e23e7-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="e23e7-204">In **Topologia processo**, nel pannello del processo, fare clic sulla casella **Output**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![Creare un nuovo output per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="e23e7-206">Nel pannello **Output** fare clic su **+ Aggiungi** e quindi aggiungere un output con l'alias `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="e23e7-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="e23e7-207">In **Sink** selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="e23e7-208">Compilare quindi il resto delle impostazioni di output usando gli stessi valori usati per l'archivio BLOB per l'input:</span><span class="sxs-lookup"><span data-stu-id="e23e7-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="e23e7-209">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-209">**Storage account**.</span></span> <span data-ttu-id="e23e7-210">Selezionare l'account di archiviazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e23e7-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="e23e7-211">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-211">**Container**.</span></span> <span data-ttu-id="e23e7-212">Selezionare il contenitore creato in precedenza (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="e23e7-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="e23e7-213">**Formato di serializzazione eventi**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-213">**Event serialization format**.</span></span> <span data-ttu-id="e23e7-214">Selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-214">Select **CSV**.</span></span>

   ![Impostazioni per il nuovo output del processo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="e23e7-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="e23e7-217">Aggiungere la funzione di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e23e7-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="e23e7-218">In precedenza è stato pubblicato un modello di Machine Learning in un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="e23e7-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="e23e7-219">In questo scenario, quando si esegue il processo di Analisi di flusso, il processo invia ogni tweet di esempio dall'input al servizio Web per l'analisi del sentiment.</span><span class="sxs-lookup"><span data-stu-id="e23e7-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="e23e7-220">Il servizio Web di Machine Learning restituisce un sentiment (`positive`, `neutral` o `negative`) e la probabilità che il tweet sia positivo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="e23e7-221">In questa sezione dell'esercitazione si definisce una funzione nel processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="e23e7-222">La funzione può essere richiamata per inviare un tweet al servizio Web e ottenere la risposta.</span><span class="sxs-lookup"><span data-stu-id="e23e7-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="e23e7-223">Assicurarsi di avere a disposizione l'URL del servizio Web e la chiave API scaricati in precedenza nella cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="e23e7-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="e23e7-224">Tornare al pannello della panoramica del processo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="e23e7-225">In **Impostazioni** selezionare **Funzioni** e quindi fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Aggiungere una funzione al processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="e23e7-227">Immettere `sentiment` come alias di funzione e compilare il resto del pannello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="e23e7-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="e23e7-228">**Tipo funzione**: selezionare **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="e23e7-229">**Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="e23e7-230">Questa impostazione offre la possibilità di immettere l'URL e la chiave.</span><span class="sxs-lookup"><span data-stu-id="e23e7-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="e23e7-231">**URL**: incollare l'URL del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="e23e7-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="e23e7-232">**Chiave**: incollare la chiave API.</span><span class="sxs-lookup"><span data-stu-id="e23e7-232">**Key**: Paste in the API key.</span></span>
  
    ![Impostazioni per l'aggiunta di una funzione di Machine Learning al processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="e23e7-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="e23e7-235">Creare una query per trasformare i dati</span><span class="sxs-lookup"><span data-stu-id="e23e7-235">Create a query to transform the data</span></span>

<span data-ttu-id="e23e7-236">Analisi di flusso usa una query dichiarativa basata su SQL per esaminare l'input ed elaborarlo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="e23e7-237">In questa sezione si creerà una query che legge ogni tweet dall'input e quindi richiama la funzione di Machine Learning per eseguire l'analisi del sentiment.</span><span class="sxs-lookup"><span data-stu-id="e23e7-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="e23e7-238">La query invia quindi il risultato all'output definito (archivio BLOB).</span><span class="sxs-lookup"><span data-stu-id="e23e7-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="e23e7-239">Tornare al pannello della panoramica del processo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="e23e7-240">In **Topologia processo** fare clic sulla casella **Query**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="e23e7-242">Immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="e23e7-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="e23e7-243">La query richiama la funzione creata in precedenza (`sentiment`) per eseguire l'analisi del sentiment su ogni tweet nell'input.</span><span class="sxs-lookup"><span data-stu-id="e23e7-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="e23e7-244">Fare clic su **Salva** per salvare la query.</span><span class="sxs-lookup"><span data-stu-id="e23e7-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="e23e7-245">Avviare il processo di Analisi di flusso e controllare l'output</span><span class="sxs-lookup"><span data-stu-id="e23e7-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="e23e7-246">È ora possibile avviare il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="e23e7-247">Avviare il processo</span><span class="sxs-lookup"><span data-stu-id="e23e7-247">Start the job</span></span>
1. <span data-ttu-id="e23e7-248">Tornare al pannello della panoramica del processo.</span><span class="sxs-lookup"><span data-stu-id="e23e7-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="e23e7-249">Fare clic su **Avvia** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="e23e7-249">Click **Start** at the top of the blade.</span></span>

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="e23e7-251">In **Avvia processo** selezionare **Personalizzato** e quindi selezionare il giorno precedente al caricamento del file CSV nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e23e7-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="e23e7-252">Al termine, fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="e23e7-253">Controllare l'output</span><span class="sxs-lookup"><span data-stu-id="e23e7-253">Check the output</span></span>
1. <span data-ttu-id="e23e7-254">Consentire l'esecuzione per alcuni minuti fino a quando non vengono visualizzate attività nella casella **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="e23e7-255">Se si usa normalmente uno strumento per esaminare il contenuto dell'archivio BLOB, è possibile usare questo strumento per esaminare il contenitore `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="e23e7-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="e23e7-256">In alternativa, seguire questa procedura nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e23e7-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="e23e7-257">Nel portale trovare l'account di archiviazione `samldemo` e all'interno dell'account trovare il contenitore `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="e23e7-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="e23e7-258">Vengono visualizzati due file nel contenitore: il file che contiene i tweet di esempio e un file CSV generato dal processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e23e7-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="e23e7-259">Fare clic con il pulsante destro del mouse sul file generato e quindi scegliere **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="e23e7-259">Right-click the generated file and then select **Download**.</span></span> 

   ![Scaricare l'output del processo CSV dall'archivio BLOB](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="e23e7-261">Aprire il file CSV generato.</span><span class="sxs-lookup"><span data-stu-id="e23e7-261">Open the generated CSV file.</span></span> <span data-ttu-id="e23e7-262">Il contenuto visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e23e7-262">You see something like the following example:</span></span>  
   
   ![Analisi di flusso e Machine Learning, visualizzazione CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="e23e7-264">Visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="e23e7-264">View metrics</span></span>
<span data-ttu-id="e23e7-265">È possibile osservare anche le metriche correlate alla funzione Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e23e7-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="e23e7-266">Le seguenti metriche correlate alla funzione vengono visualizzate nella casella **Monitoraggio** nel pannello del processo:</span><span class="sxs-lookup"><span data-stu-id="e23e7-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="e23e7-267">**Richieste della funzione** indica il numero di richieste inviate al servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e23e7-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="e23e7-268">**Eventi della funzione** indica il numero di eventi nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="e23e7-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="e23e7-269">Per impostazione predefinita, ogni richiesta a un servizio Web di Machine Learning contiene fino a 1.000 eventi.</span><span class="sxs-lookup"><span data-stu-id="e23e7-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="e23e7-270">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e23e7-270">Next steps</span></span>

* [<span data-ttu-id="e23e7-271">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="e23e7-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e23e7-272">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="e23e7-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e23e7-273">Integrare API REST e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e23e7-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="e23e7-274">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="e23e7-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



