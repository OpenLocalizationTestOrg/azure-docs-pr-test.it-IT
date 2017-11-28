---
title: aaaStream dati dal flusso Analitica in archivio Data Lake | Documenti Microsoft
description: Utilizzare i dati di toostream Analitica di flusso di Azure in archivio Azure Data Lake
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="d02e6-103">Trasmettere i dati dal BLOB di archiviazione di Azure ad Archivio Data Lake usando Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="d02e6-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="d02e6-104">In questo articolo si apprenderà come toouse archivio Azure Data Lake come output per un processo Analitica di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="d02e6-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="d02e6-105">In questo articolo viene illustrato un semplice scenario che legge i dati da un blob di archiviazione di Azure (input) e scrive hello archivio data Lake a tooData (output).</span><span class="sxs-lookup"><span data-stu-id="d02e6-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="d02e6-106">In questo momento, creazione e configurazione di archivio Data Lake restituisce per Analitica di flusso è supportato solo in hello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d02e6-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="d02e6-107">Di conseguenza, alcune parti di questa esercitazione verranno utilizzato hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="d02e6-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d02e6-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d02e6-108">Prerequisites</span></span>
<span data-ttu-id="d02e6-109">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d02e6-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d02e6-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-110">**An Azure subscription**.</span></span> <span data-ttu-id="d02e6-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d02e6-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d02e6-112">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-112">**Azure Storage account**.</span></span> <span data-ttu-id="d02e6-113">Si utilizzerà un contenitore di blob da dati tooinput account per un processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="d02e6-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="d02e6-114">Per questa esercitazione, si supponga di avere un account di archiviazione denominato **storageforasa** e un contenitore nell'account hello chiamato **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="d02e6-115">Dopo aver creato il contenitore di hello, caricare un tooit file dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="d02e6-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="d02e6-116">**Account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="d02e6-117">Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d02e6-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="d02e6-118">Si supponga di avere un account Data Lake denominato **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="d02e6-119">Creare un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="d02e6-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="d02e6-120">Iniziare creando un processo di Analisi di flusso che include un'origine di input e una destinazione di output.</span><span class="sxs-lookup"><span data-stu-id="d02e6-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="d02e6-121">Per questa esercitazione, origine hello è un contenitore blob di Azure e la destinazione hello è archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d02e6-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="d02e6-122">Accesso toohello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d02e6-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d02e6-123">Nel riquadro di sinistra hello, fare clic su **i processi di flusso Analitica**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="d02e6-124">![Creare un processo di Analisi di flusso](./media/data-lake-store-stream-analytics/create.job.png "Creare un processo di Analisi di flusso")</span><span class="sxs-lookup"><span data-stu-id="d02e6-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="d02e6-125">Assicurarsi che si crea un processo in hello stessa area come account di archiviazione hello o comporta costi aggiuntivi per lo spostamento dei dati tra aree.</span><span class="sxs-lookup"><span data-stu-id="d02e6-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="d02e6-126">Creare un Blob di input per il processo di hello</span><span class="sxs-lookup"><span data-stu-id="d02e6-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="d02e6-127">Pagina hello Open per il processo di flusso Analitica hello, hello nel riquadro di sinistra fare clic su hello **input** scheda e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="d02e6-128">![Aggiungere un processo di input tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "aggiungere un processo tooyour input")</span><span class="sxs-lookup"><span data-stu-id="d02e6-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="d02e6-129">In hello **nuovo input** pannello fornire hello seguenti valori.</span><span class="sxs-lookup"><span data-stu-id="d02e6-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="d02e6-130">![Aggiungere un processo di input tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "aggiungere un processo tooyour input")</span><span class="sxs-lookup"><span data-stu-id="d02e6-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="d02e6-131">Per **alias di Input**, immettere un nome univoco per l'input processo hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="d02e6-132">Per **Tipo di origine** selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="d02e6-133">Per **Origine** selezionare **Archiviazione BLOB**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="d02e6-134">Per **Sottoscrizione** selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="d02e6-135">Per **account di archiviazione**, selezionare l'account di archiviazione di hello creato come parte dei prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="d02e6-136">Per **contenitore**, selezionare il contenitore hello creati in hello selezionato di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d02e6-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="d02e6-137">In **Formato di serializzazione eventi** scegliere **CSV**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="d02e6-138">Per **Delimitatore** selezionare **scheda**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="d02e6-139">Per **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="d02e6-140">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-140">Click **Create**.</span></span> <span data-ttu-id="d02e6-141">portale Hello ora aggiunge input hello e verifica tooit connessione hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="d02e6-142">Creare un archivio Data Lake di output per il processo di hello</span><span class="sxs-lookup"><span data-stu-id="d02e6-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="d02e6-143">Aprire la pagina hello per il processo di flusso Analitica hello, fare clic su hello **output** scheda e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="d02e6-144">![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.1.png "aggiungere un processo tooyour output")</span><span class="sxs-lookup"><span data-stu-id="d02e6-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="d02e6-145">In hello **nuovo output** pannello fornire hello seguenti valori.</span><span class="sxs-lookup"><span data-stu-id="d02e6-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="d02e6-146">![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.2.png "aggiungere un processo tooyour output")</span><span class="sxs-lookup"><span data-stu-id="d02e6-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="d02e6-147">Per **alias di Output**, immettere un nome univoco per l'output del processo hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="d02e6-148">Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d02e6-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="d02e6-149">Per **Sink** selezionare **Data Lkae Store**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="d02e6-150">Sarà richiesto tooauthorize accedere tooData Lake archivio account.</span><span class="sxs-lookup"><span data-stu-id="d02e6-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="d02e6-151">Fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="d02e6-152">In hello **nuovo output** pannello hello tooprovide seguente i valori di continuare.</span><span class="sxs-lookup"><span data-stu-id="d02e6-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="d02e6-153">![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.3.png "aggiungere un processo tooyour output")</span><span class="sxs-lookup"><span data-stu-id="d02e6-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="d02e6-154">Per **nome Account**, selezionare account archivio Data Lake hello sia già stato creato in cui si desidera hello processo output toobe inviati.</span><span class="sxs-lookup"><span data-stu-id="d02e6-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="d02e6-155">Per **modello prefisso del percorso**, immettere toowrite di percorso utilizzato un file del file all'interno di hello specificati account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d02e6-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="d02e6-156">Per **formato data**, se si utilizza un token di data nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="d02e6-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="d02e6-157">Per **formato ora**, se è stato usato un token di tempo nel percorso di prefisso hello, specificare il formato di ora hello in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="d02e6-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="d02e6-158">In **Formato di serializzazione eventi** scegliere **CSV**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="d02e6-159">Per **Delimitatore** selezionare **scheda**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="d02e6-160">Per **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="d02e6-161">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-161">Click **Create**.</span></span> <span data-ttu-id="d02e6-162">portale Hello ora aggiunge l'output di hello e verifica tooit connessione hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="d02e6-163">Eseguire il processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="d02e6-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="d02e6-164">un processo di flusso Analitica toorun, è necessario eseguire una query da hello **Query** scheda. Per questa esercitazione, è possibile eseguire query di esempio hello sostituendo i segnaposto hello con hello processo gli alias di input e outpui, come illustrato nella cattura di schermata hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d02e6-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="d02e6-165">![Eseguire query](./media/data-lake-store-stream-analytics/run.query.png "Eseguire query")</span><span class="sxs-lookup"><span data-stu-id="d02e6-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="d02e6-166">Fare clic su **salvare** hello superiore hello e quindi da hello **Panoramica** scheda, fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="d02e6-167">Nella finestra di dialogo hello selezionare **ora personalizzato**, quindi impostare hello data e ora correnti.</span><span class="sxs-lookup"><span data-stu-id="d02e6-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="d02e6-168">![Impostare l'ora del processo](./media/data-lake-store-stream-analytics/run.query.2.png "Impostare l'ora del processo")</span><span class="sxs-lookup"><span data-stu-id="d02e6-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="d02e6-169">Fare clic su **avviare** processo hello toostart.</span><span class="sxs-lookup"><span data-stu-id="d02e6-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="d02e6-170">Può richiedere il processo hello toostart di tooa alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="d02e6-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="d02e6-171">tootrigger hello toopick hello dati del processo da blob hello, copiare un contenitore blob di toohello file di dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="d02e6-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="d02e6-172">È possibile ottenere un file di dati di esempio da hello [Git Repository di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="d02e6-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="d02e6-173">Per questa esercitazione, copia il file hello **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="d02e6-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="d02e6-174">È possibile utilizzare vari client, ad esempio [Azure Storage Explorer](http://storageexplorer.com/), contenitore blob tooa di tooupload dati.</span><span class="sxs-lookup"><span data-stu-id="d02e6-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="d02e6-175">Da hello **Panoramica** scheda **monitoraggio**, vedere la modalità di elaborazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="d02e6-176">![Monitorare il processo](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorare il processo")</span><span class="sxs-lookup"><span data-stu-id="d02e6-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="d02e6-177">Infine, è possibile verificare che i dati di output di hello processo sono disponibili account archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="d02e6-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="d02e6-178">![Verificare l'output](./media/data-lake-store-stream-analytics/run.query.4.png "Verificare l'output")</span><span class="sxs-lookup"><span data-stu-id="d02e6-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="d02e6-179">Nel riquadro di esplorazione di dati hello, si noti che hello output scritto tooa percorso della cartella come specificato nel hello archivio Data Lake impostazioni di output (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="d02e6-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="d02e6-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d02e6-180">See also</span></span>
* [<span data-ttu-id="d02e6-181">Creare un toouse cluster HDInsight archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d02e6-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
