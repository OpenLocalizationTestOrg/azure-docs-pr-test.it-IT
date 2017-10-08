---
title: integrazione di flusso Analitica e Machine Learning aaaAzure | Documenti Microsoft
description: Come toouse una funzione definita dall'utente e Machine Learning in un processo di flusso Analitica
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
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="0dea9-103">Analisi del sentiment con Analisi di flusso di Azure e Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0dea9-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="0dea9-104">In questo articolo viene descritto come tooquickly impostare un semplice processo Analitica di flusso di Azure che si integra Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dea9-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="0dea9-105">Utilizzare un modello di analitica sentiment di Machine Learning da dati di testo Cortana Intelligence Gallery tooanalyze streaming hello e determinare il punteggio sentiment hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="0dea9-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="0dea9-106">Utilizzo di hello Cortana Intelligence Suite consente di eseguire questa operazione senza preoccuparsi delle complessità hello di compilazione di un modello di valutazione analitica.</span><span class="sxs-lookup"><span data-stu-id="0dea9-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="0dea9-107">È possibile applicare le operazioni da tooscenarios questo articolo come i seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dea9-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="0dea9-108">Analisi in tempo reale del sentiment su flussi di dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="0dea9-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="0dea9-109">Analisi dei record delle chat dei client con il personale di supporto.</span><span class="sxs-lookup"><span data-stu-id="0dea9-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="0dea9-110">Valutazione dei commenti per forum, blog e video.</span><span class="sxs-lookup"><span data-stu-id="0dea9-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="0dea9-111">Molti altri scenari di punteggio predittivo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="0dea9-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="0dea9-112">In uno scenario reale, si otterrebbe dati hello direttamente da un flusso di dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="0dea9-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="0dea9-113">esercitazione di hello toosimplify, abbiamo scritto, in modo che hello il processo di Streaming Analitica Ottiene TWEET da un file CSV in archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="0dea9-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="0dea9-114">È possibile creare un file CSV oppure è possibile utilizzare un file CSV di esempio, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="0dea9-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![tweet di esempio in un file CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="0dea9-116">processo di Streaming Analitica Hello che si crea l'applicazione hello sentiment analitica modello come una funzione definita dall'utente (UDF) sui dati di testo di esempio hello dall'archivio blob hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="0dea9-117">output di Hello (risultato hello di analisi del sentiment hello) viene scritto toohello stesso archivio di blob in un file CSV diverso.</span><span class="sxs-lookup"><span data-stu-id="0dea9-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="0dea9-118">Hello nella figura seguente viene illustrata questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="0dea9-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="0dea9-119">Come indicato, per uno scenario più realistico è possibile sostituire l'archivio BLOB con il flusso di dati di Twitter provenienti da un input di Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0dea9-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="0dea9-120">Inoltre, è possibile creare un [Microsoft Power BI](https://powerbi.microsoft.com/) visualizzazione in tempo reale di valutazione di aggregazione hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Panoramica dell'integrazione di Machine Learning in Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="0dea9-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0dea9-122">Prerequisites</span></span>
<span data-ttu-id="0dea9-123">Prima di iniziare, verificare di che aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="0dea9-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="0dea9-124">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="0dea9-124">An active Azure subscription.</span></span>
* <span data-ttu-id="0dea9-125">Un file CSV contenente alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="0dea9-125">A CSV file with some data in it.</span></span> <span data-ttu-id="0dea9-126">È possibile scaricare file hello illustrato in precedenza da [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), oppure è possibile creare un file.</span><span class="sxs-lookup"><span data-stu-id="0dea9-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="0dea9-127">Questo articolo si presuppone che si usi file hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="0dea9-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="0dea9-128">In generale, attività di hello toocomplete illustrate in questo articolo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dea9-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="0dea9-129">Creare un account di archiviazione di Azure e un contenitore di archiviazione blob e caricare un contenitore di toohello file di input in formato CSV.</span><span class="sxs-lookup"><span data-stu-id="0dea9-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="0dea9-130">Aggiungere un modello di valutazione analitica dall'area di lavoro in Azure Machine Learning tooyour Cortana Intelligence Gallery hello e distribuire questo modello come un servizio web nell'area di lavoro Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="0dea9-131">Creare un processo di flusso Analitica che chiama il servizio web come funzione valutazione toodetermine ordine hello input di testo.</span><span class="sxs-lookup"><span data-stu-id="0dea9-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="0dea9-132">Avviare il processo di flusso Analitica hello e controllare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="0dea9-133">Creare un contenitore di archiviazione e caricare il file di input CSV hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="0dea9-134">Per questo passaggio, è possibile utilizzare qualsiasi file CSV, ad esempio hello uno disponibili da GitHub.</span><span class="sxs-lookup"><span data-stu-id="0dea9-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="0dea9-135">Nel portale di Azure hello, fare clic su **New** &gt; **archiviazione** &gt; **account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![creare un nuovo account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="0dea9-137">Specificare un nome (`samldemo` nell'esempio hello).</span><span class="sxs-lookup"><span data-stu-id="0dea9-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="0dea9-138">nome Hello può utilizzare solo lettere minuscole e numeri e deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="0dea9-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="0dea9-139">Specificare un gruppo di risorse esistente e specificare un percorso.</span><span class="sxs-lookup"><span data-stu-id="0dea9-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="0dea9-140">Per il percorso, è consigliabile che tutte le risorse di hello create in questa esercitazione usare hello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="0dea9-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![specificare i dettagli dell'account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="0dea9-142">Nel portale di Azure hello, selezionare account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="0dea9-143">Nel Pannello di account di archiviazione hello, fare clic su **contenitori** e quindi fare clic su  **+ &nbsp;contenitore** toocreate nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="0dea9-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![Creare un contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="0dea9-145">Specificare un nome per il contenitore di hello (`azuresamldemoblob` nell'esempio hello) e verificare che **tipo di accesso** è troppo**Blob**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="0dea9-146">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-146">When you're done, click **OK**.</span></span>

    ![specificare i dettagli del contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="0dea9-148">In hello **contenitori** blade, hello selezionare nuovo contenitore, che apre il pannello hello per tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="0dea9-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="0dea9-149">Fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-149">Click **Upload**.</span></span>

    ![Pulsante 'Carica' per un contenitore](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="0dea9-151">In hello **caricamento blob** pannello, specificare i file CSV hello che si desidera toouse per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0dea9-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="0dea9-152">Per **Blob tipo**selezionare **blob in blocchi** e blocco hello set dimensioni too4 MB, che è sufficiente per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0dea9-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![caricare il file BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="0dea9-154">Fare clic su hello **caricare** pulsante nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="0dea9-155">Aggiungere modello di hello valutazione analitica da hello Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="0dea9-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="0dea9-156">Ora che i dati di esempio hello sono in un blob, è possibile abilitare modello di analisi del sentiment hello in Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="0dea9-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="0dea9-157">Passare toohello [modello analitica predittiva sentiment](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) pagina hello Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="0dea9-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="0dea9-158">Fare clic su **Open in Studio** (Apri in Studio).</span><span class="sxs-lookup"><span data-stu-id="0dea9-158">Click **Open in Studio**.</span></span>  
   
   ![Analisi di flusso e Machine Learning, aprire Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="0dea9-160">Accedi toogo toohello area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0dea9-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="0dea9-161">Selezionare una località.</span><span class="sxs-lookup"><span data-stu-id="0dea9-161">Select a location.</span></span>

4. <span data-ttu-id="0dea9-162">Fare clic su **eseguire** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="0dea9-163">esecuzione del processo di Hello, che richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="0dea9-163">hello process runs, which takes about a minute.</span></span>

   ![eseguire l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="0dea9-165">Dopo il processo di hello è stata eseguita correttamente, selezionare **distribuzione servizio Web** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![distribuire l'esperimento in Machine Learning Studio come servizio Web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="0dea9-167">toovalidate che hello sentiment modello analitica è toouse pronti, fare clic su hello **Test** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0dea9-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="0dea9-168">Immettere testo, ad esempio "Mi piace Microsoft".</span><span class="sxs-lookup"><span data-stu-id="0dea9-168">Provide text input such as "I love Microsoft".</span></span> 

   ![testare l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="0dea9-170">Se il test di hello funziona, viene visualizzato un toohello simile risultato esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0dea9-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![risultati del test in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="0dea9-172">In hello **app** colonna, fare clic su hello **Excel 2010 o cartella di lavoro precedenti** toodownload collegamento una cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="0dea9-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="0dea9-173">cartella di lavoro Hello contiene un'API hello chiave e l'URL di hello che è necessario tooset successive il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Analisi di flusso e Machine Learning, panoramica rapida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="0dea9-175">Creare un processo di flusso Analitica che utilizza il modello di Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="0dea9-176">È ora possibile creare un processo di flusso Analitica che legge hello esempio TWEET da file CSV hello nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="0dea9-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="0dea9-177">Creazione del processo di hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-177">Create hello job</span></span>

1. <span data-ttu-id="0dea9-178">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0dea9-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="0dea9-179">Fare clic su **Nuovo** > **Internet delle cose** > **Processo di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Percorso del portale Azure per ottenere il nuovo processo di flusso Analitica tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="0dea9-181">Nome del processo hello `azure-sa-ml-demo`, specificare una sottoscrizione, specificare un gruppo di risorse esistente o crearne uno nuovo e selezionare il percorso di hello per processo hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![specificare le impostazioni per il nuovo processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="0dea9-183">Configurazione input processo hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-183">Configure hello job input</span></span>
<span data-ttu-id="0dea9-184">processo Hello Ottiene l'input da file CSV hello caricato archiviazione tooblob precedenti.</span><span class="sxs-lookup"><span data-stu-id="0dea9-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="0dea9-185">Dopo il processo di hello è stato creato in **processo topologia** nel Pannello di hello processo, fare clic su hello **input** casella.</span><span class="sxs-lookup"><span data-stu-id="0dea9-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Casella 'Input' nel pannello del processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="0dea9-187">In hello **input** pannello, fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![Pulsante per l'aggiunta di un processo di flusso Analitica input toohello 'add'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="0dea9-189">Compilare hello **nuovo input** pannello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="0dea9-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="0dea9-190">**Alias di input**: utilizza il nome di hello `datainput`.</span><span class="sxs-lookup"><span data-stu-id="0dea9-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="0dea9-191">**Tipo di origine**: selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="0dea9-192">**Origine**: selezionare **Archiviazione BLOB**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="0dea9-193">**Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="0dea9-194">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-194">**Storage account**.</span></span> <span data-ttu-id="0dea9-195">Selezionare l'account di archiviazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0dea9-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="0dea9-196">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-196">**Container**.</span></span> <span data-ttu-id="0dea9-197">Contenitore hello selezionare creato in precedenza (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="0dea9-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="0dea9-198">**Formato di serializzazione eventi**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-198">**Event serialization format**.</span></span> <span data-ttu-id="0dea9-199">Selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-199">Select **CSV**.</span></span>

    ![Impostazioni per il nuovo input del processo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="0dea9-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="0dea9-202">Configurare l'output del processo hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-202">Configure hello job output</span></span>
<span data-ttu-id="0dea9-203">Hello processo Invia risultati toohello stesso blob di archiviazione in cui si ottiene input.</span><span class="sxs-lookup"><span data-stu-id="0dea9-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="0dea9-204">In **processo topologia** nel Pannello di hello processo, fare clic su hello **output** casella.</span><span class="sxs-lookup"><span data-stu-id="0dea9-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Creare un nuovo output per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="0dea9-206">In hello **output** pannello, fare clic su **+ Aggiungi**, quindi aggiungere un output con alias hello `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="0dea9-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="0dea9-207">In **Sink** selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="0dea9-208">Compilare il resto di hello di hello output impostazioni mediante hello stessi valori utilizzati per l'archiviazione blob hello input:</span><span class="sxs-lookup"><span data-stu-id="0dea9-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="0dea9-209">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-209">**Storage account**.</span></span> <span data-ttu-id="0dea9-210">Selezionare l'account di archiviazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0dea9-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="0dea9-211">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-211">**Container**.</span></span> <span data-ttu-id="0dea9-212">Contenitore hello selezionare creato in precedenza (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="0dea9-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="0dea9-213">**Formato di serializzazione eventi**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-213">**Event serialization format**.</span></span> <span data-ttu-id="0dea9-214">Selezionare **CSV**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-214">Select **CSV**.</span></span>

   ![Impostazioni per il nuovo output del processo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="0dea9-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="0dea9-217">Aggiungere una funzione di Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="0dea9-218">In precedenza è stato pubblicato un servizio web tooa del modello di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dea9-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="0dea9-219">In questo scenario, quando si esegue il processo di analisi di flusso hello, invia tweet ogni esempio dal servizio web di input toohello hello per l'analisi di valutazione.</span><span class="sxs-lookup"><span data-stu-id="0dea9-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="0dea9-220">servizio web Machine Learning Hello restituisce un sentiment (`positive`, `neutral`, o `negative`) e la probabilità di tweet hello viene positivo.</span><span class="sxs-lookup"><span data-stu-id="0dea9-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="0dea9-221">In questa sezione dell'esercitazione hello, si definisce una funzione nel processo di analisi di flusso hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="0dea9-222">funzione Hello può essere richiamato toosend un servizio web di toohello tweet e tornare risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="0dea9-223">Assicurarsi di disporre di hello web service URL e la chiave API che è stato scaricato in precedenza nella cartella di lavoro di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="0dea9-224">Pannello della panoramica processo toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="0dea9-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="0dea9-225">In **Impostazioni** selezionare **Funzioni** e quindi fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Aggiungere un processo di flusso Analitica toohello (funzione)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="0dea9-227">Immettere `sentiment` come hello funzione alias e compilare il resto di hello del pannello hello utilizzando questi valori:</span><span class="sxs-lookup"><span data-stu-id="0dea9-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="0dea9-228">**Tipo funzione**: selezionare **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="0dea9-229">**Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="0dea9-230">In questo modo, è un URL di probabilità tooenter hello e una chiave.</span><span class="sxs-lookup"><span data-stu-id="0dea9-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="0dea9-231">**URL**: Incolla in hello URL del servizio web.</span><span class="sxs-lookup"><span data-stu-id="0dea9-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="0dea9-232">**Chiave**: Incolla nella chiave hello API.</span><span class="sxs-lookup"><span data-stu-id="0dea9-232">**Key**: Paste in hello API key.</span></span>
  
    ![Impostazioni per l'aggiunta di un processo di flusso Analitica Machine Learning toohello (funzione)](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="0dea9-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="0dea9-235">Creare un query tootransform hello dati</span><span class="sxs-lookup"><span data-stu-id="0dea9-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="0dea9-236">Flusso Analitica utilizza un input di query dichiarativo basato su SQL tooexamine hello ed elaborarlo.</span><span class="sxs-lookup"><span data-stu-id="0dea9-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="0dea9-237">In questa sezione creare una query che legge ogni tweet dall'input e quindi richiama l'analisi del sentiment tooperform funzione hello Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dea9-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="0dea9-238">query Hello quindi invia l'output di hello risultato toohello che sia definita (archiviazione blob).</span><span class="sxs-lookup"><span data-stu-id="0dea9-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="0dea9-239">Pannello della panoramica processo toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="0dea9-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="0dea9-240">In **processo topologia**, fare clic su hello **Query** casella.</span><span class="sxs-lookup"><span data-stu-id="0dea9-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="0dea9-242">Immettere hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="0dea9-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="0dea9-243">query Hello richiama la funzione di hello creato in precedenza (`sentiment`) nell'analisi del sentiment tooperform ordine su ogni tweet hello input.</span><span class="sxs-lookup"><span data-stu-id="0dea9-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="0dea9-244">Fare clic su **salvare** query hello toosave.</span><span class="sxs-lookup"><span data-stu-id="0dea9-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="0dea9-245">Avviare il processo di flusso Analitica hello e controllare l'output di hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="0dea9-246">È ora possibile avviare il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="0dea9-247">Avviare il processo di hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-247">Start hello job</span></span>
1. <span data-ttu-id="0dea9-248">Pannello della panoramica processo toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="0dea9-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="0dea9-249">Fare clic su **avviare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-249">Click **Start** at hello top of hello blade.</span></span>

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="0dea9-251">In hello **inizio processo**selezionare **personalizzato**, quindi selezionare toowhen precedente di un giorno caricato archiviazione tooblob file CSV di hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="0dea9-252">Al termine, fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="0dea9-253">Controllare l'output di hello</span><span class="sxs-lookup"><span data-stu-id="0dea9-253">Check hello output</span></span>
1. <span data-ttu-id="0dea9-254">Il processo di hello let eseguito per qualche minuto finché non viene visualizzata l'attività in hello **monitoraggio** casella.</span><span class="sxs-lookup"><span data-stu-id="0dea9-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="0dea9-255">Se si dispone di uno strumento utilizzato normalmente contenuto hello tooexamine dell'archiviazione blob, utilizzare tale hello tooexamine strumento `azuresamldemoblob` contenitore.</span><span class="sxs-lookup"><span data-stu-id="0dea9-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="0dea9-256">In alternativa, hello in hello portale di Azure come segue:</span><span class="sxs-lookup"><span data-stu-id="0dea9-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="0dea9-257">Nel portale di hello trovare hello `samldemo` storage account e all'interno di account hello, trovare hello `azuresamldemoblob` contenitore.</span><span class="sxs-lookup"><span data-stu-id="0dea9-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="0dea9-258">Viene visualizzato due file nel contenitore hello: hello file che contiene hello esempio TWEET e un file CSV generato dal processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="0dea9-259">Fare clic sul file hello generato e quindi selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="0dea9-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Scaricare l'output del processo CSV dall'archivio BLOB](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="0dea9-261">Aprire hello ha generato il file CSV.</span><span class="sxs-lookup"><span data-stu-id="0dea9-261">Open hello generated CSV file.</span></span> <span data-ttu-id="0dea9-262">Viene visualizzato un output simile al seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0dea9-262">You see something like hello following example:</span></span>  
   
   ![Analisi di flusso e Machine Learning, visualizzazione CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="0dea9-264">Visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="0dea9-264">View metrics</span></span>
<span data-ttu-id="0dea9-265">È possibile osservare anche le metriche correlate alla funzione Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dea9-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="0dea9-266">Hello seguendo le metriche correlate alla funzione viene visualizzato in hello **monitoraggio** casella nel pannello processo hello:</span><span class="sxs-lookup"><span data-stu-id="0dea9-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="0dea9-267">**Funzione richieste** indica il numero di hello di richieste inviate tooa servizio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dea9-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="0dea9-268">**Funzione eventi** indica il numero di hello di eventi nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="0dea9-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="0dea9-269">Per impostazione predefinita, ogni tooa richiesta servizio web Machine Learning contiene backup too1, eventi 000.</span><span class="sxs-lookup"><span data-stu-id="0dea9-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="0dea9-270">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0dea9-270">Next steps</span></span>

* [<span data-ttu-id="0dea9-271">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="0dea9-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0dea9-272">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0dea9-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0dea9-273">Integrare API REST e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0dea9-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="0dea9-274">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0dea9-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



