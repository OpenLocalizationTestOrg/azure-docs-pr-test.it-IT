---
title: Trasmettere i dati da Analisi di flusso a Data Lake Store | Azure
description: Usare Analisi di flusso di Azure per trasmettere i dati in Archivio Azure Data Lake
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
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="c5951-103">Trasmettere i dati dal BLOB di archiviazione di Azure ad Archivio Data Lake usando Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c5951-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="c5951-104">In questo articolo viene descritto come usare Archivio Azure Data Lake come output per un processo di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5951-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="c5951-105">Questo articolo illustra uno scenario semplice in cui i dati vengono letti da un BLOB di Archiviazione di Azure (input) e scritti in Archivio Data Lake (output).</span><span class="sxs-lookup"><span data-stu-id="c5951-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="c5951-106">Attualmente la creazione e la configurazione di output di Archivio Data Lake per l'Analisi di flusso è supportata solo nel [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c5951-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="c5951-107">Di conseguenza, alcune parti di questa esercitazione useranno il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="c5951-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="c5951-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5951-108">Prerequisites</span></span>
<span data-ttu-id="c5951-109">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c5951-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="c5951-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5951-110">**An Azure subscription**.</span></span> <span data-ttu-id="c5951-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5951-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="c5951-112">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5951-112">**Azure Storage account**.</span></span> <span data-ttu-id="c5951-113">Per l'input dei dati per un processo di Analisi di flusso viene usato un contenitore BLOB da questo account.</span><span class="sxs-lookup"><span data-stu-id="c5951-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="c5951-114">Per questa esercitazione, si supponga di disporre di un account di archiviazione **storageforasa** e di un contenitore incluso nell'account denominato **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="c5951-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="c5951-115">Dopo aver creato il contenitore, caricare un file di dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c5951-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="c5951-116">**Account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5951-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="c5951-117">Seguire le istruzioni fornite in [Introduzione ad Archivio Azure Data Lake tramite il portale di Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c5951-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="c5951-118">Si supponga di avere un account Data Lake denominato **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="c5951-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="c5951-119">Creare un processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="c5951-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="c5951-120">Iniziare creando un processo di Analisi di flusso che include un'origine di input e una destinazione di output.</span><span class="sxs-lookup"><span data-stu-id="c5951-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="c5951-121">Per questa esercitazione, l'origine è un contenitore BLOB di Azure e la destinazione è Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c5951-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="c5951-122">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5951-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c5951-123">Nel riquadro sinistro, fare clic su **Processi di Analisi di flusso**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5951-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="c5951-124">![Creare un processo di Analisi di flusso](./media/data-lake-store-stream-analytics/create.job.png "Creare un processo di Analisi di flusso")</span><span class="sxs-lookup"><span data-stu-id="c5951-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5951-125">Assicurarsi di creare il processo nella stessa area dell'account di archiviazione per non incorrere in costi aggiuntivi per lo spostamento dei dati tra le aree.</span><span class="sxs-lookup"><span data-stu-id="c5951-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="c5951-126">Creare un input BLOB per il processo</span><span class="sxs-lookup"><span data-stu-id="c5951-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="c5951-127">Aprire la pagina per il processo di Analisi di flusso, nel riquadro sinistro fare clic sulla scheda **Input** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5951-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="c5951-128">![Aggiungere un input al processo](./media/data-lake-store-stream-analytics/create.input.1.png "Aggiungere un input al processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="c5951-129">Nel pannello **Nuovo input** specificare i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="c5951-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="c5951-130">![Aggiungere un input al processo](./media/data-lake-store-stream-analytics/create.input.2.png "Aggiungere un input al processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="c5951-131">In **Alias dell'input** inserire un nome univoco per l'input del processo.</span><span class="sxs-lookup"><span data-stu-id="c5951-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="c5951-132">Per **Tipo di origine** selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="c5951-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="c5951-133">Per **Origine** selezionare **Archiviazione BLOB**.</span><span class="sxs-lookup"><span data-stu-id="c5951-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="c5951-134">Per **Sottoscrizione** selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="c5951-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="c5951-135">Per **Account di archiviazione** selezionare l'account di archiviazione creato come parte dei prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="c5951-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="c5951-136">Per **Contenitore** selezionare il contenitore creato nell'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="c5951-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="c5951-137">In **Formato di serializzazione eventi** scegliere **CSV**.</span><span class="sxs-lookup"><span data-stu-id="c5951-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="c5951-138">Per **Delimitatore** selezionare **scheda**.</span><span class="sxs-lookup"><span data-stu-id="c5951-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="c5951-139">Per **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="c5951-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="c5951-140">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c5951-140">Click **Create**.</span></span> <span data-ttu-id="c5951-141">Il portale ora aggiunge l'input e verifica la connessione allo stesso.</span><span class="sxs-lookup"><span data-stu-id="c5951-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="c5951-142">Creare un output di Archivio Data Lake per il processo</span><span class="sxs-lookup"><span data-stu-id="c5951-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="c5951-143">Aprire la pagina per il processo di Analisi di flusso, fare clic sulla scheda **Output** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5951-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="c5951-144">![Aggiungere un output al processo](./media/data-lake-store-stream-analytics/create.output.1.png "Aggiungere un output al processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="c5951-145">Nel pannello **Nuovo output** specificare i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="c5951-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="c5951-146">![Aggiungere un output al processo](./media/data-lake-store-stream-analytics/create.output.2.png "Aggiungere un output al processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="c5951-147">In **Alias dell'output** inserire un nome univoco per l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="c5951-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="c5951-148">È un nome descrittivo usato nelle query per indirizzare l'output delle query ad Archivio Data Lake in uso.</span><span class="sxs-lookup"><span data-stu-id="c5951-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="c5951-149">Per **Sink** selezionare **Data Lkae Store**.</span><span class="sxs-lookup"><span data-stu-id="c5951-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="c5951-150">Verrà richiesto di autorizzare l'accesso all'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c5951-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="c5951-151">Fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="c5951-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="c5951-152">Nel pannello **Nuovo output** continuare a specificare i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="c5951-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="c5951-153">![Aggiungere un output al processo](./media/data-lake-store-stream-analytics/create.output.3.png "Aggiungere un output al processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="c5951-154">Per **Nome account** selezionare l'account Data Lake Store già creato a cui si desidera inviare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="c5951-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="c5951-155">In **Schema prefisso percorso** immettere un percorso di file usato per scrivere i file nell'account Data Lake Store specificato.</span><span class="sxs-lookup"><span data-stu-id="c5951-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="c5951-156">Per **Formato data**, se nel percorso di prefisso viene usato un token di data, è possibile selezionare il formato della data in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="c5951-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="c5951-157">Per **Formato ora**, se nel percorso di prefisso viene usato un token di ora, specificare il formato dell'ora in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="c5951-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="c5951-158">In **Formato di serializzazione eventi** scegliere **CSV**.</span><span class="sxs-lookup"><span data-stu-id="c5951-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="c5951-159">Per **Delimitatore** selezionare **scheda**.</span><span class="sxs-lookup"><span data-stu-id="c5951-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="c5951-160">Per **Codifica** selezionare **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="c5951-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="c5951-161">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c5951-161">Click **Create**.</span></span> <span data-ttu-id="c5951-162">Il portale ora aggiunge l'output e verifica la connessione allo stesso.</span><span class="sxs-lookup"><span data-stu-id="c5951-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="c5951-163">Eseguire il processo di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="c5951-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="c5951-164">Per eseguire un processo di Analisi di flusso, è necessario eseguire una query dalla scheda **Query**.</span><span class="sxs-lookup"><span data-stu-id="c5951-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="c5951-165">Per questa esercitazione, è possibile eseguire la query di esempio sostituendo i segnaposto con gli alias di input e output del processo, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="c5951-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="c5951-166">![Eseguire query](./media/data-lake-store-stream-analytics/run.query.png "Eseguire query")</span><span class="sxs-lookup"><span data-stu-id="c5951-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="c5951-167">Fare clic su **Salva** nella parte superiore dello schermo, quindi sulla scheda **Panoramica** e su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="c5951-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="c5951-168">Nella finestra di dialogo selezionare **Ora personalizzata**, quindi selezionare la data e l'ora correnti.</span><span class="sxs-lookup"><span data-stu-id="c5951-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="c5951-169">![Impostare l'ora del processo](./media/data-lake-store-stream-analytics/run.query.2.png "Impostare l'ora del processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="c5951-170">Fare clic su **Avvia** per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="c5951-170">Click **Start** to start the job.</span></span> <span data-ttu-id="c5951-171">L'avvio del processo può richiedere un paio di minuti.</span><span class="sxs-lookup"><span data-stu-id="c5951-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="c5951-172">Per attivare la raccolta dei dati dal BLOB da parte del processo, copiare un file dati campione nel contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5951-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="c5951-173">È possibile ottenere un file di dati di esempio dal [repository Git di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="c5951-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="c5951-174">Per questa esercitazione verrà copiato il file **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="c5951-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="c5951-175">È possibile usare vari tipi di client, ad esempio [Azure Storage Explorer](http://storageexplorer.com/), per caricare i dati in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5951-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="c5951-176">Nella scheda **Panoramica**, in **Monitoraggio** è possibile visualizzare come sono stati elaborati i dati.</span><span class="sxs-lookup"><span data-stu-id="c5951-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="c5951-177">![Monitorare il processo](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorare il processo")</span><span class="sxs-lookup"><span data-stu-id="c5951-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="c5951-178">Infine, è possibile verificare la disponibilità dei dati di output del processo nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c5951-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="c5951-179">![Verificare l'output](./media/data-lake-store-stream-analytics/run.query.4.png "Verificare l'output")</span><span class="sxs-lookup"><span data-stu-id="c5951-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="c5951-180">Nel riquadro Esplora dati l'output viene scritto in un percorso di cartella come specificato nelle impostazioni di output di Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="c5951-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="c5951-181">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c5951-181">See also</span></span>
* [<span data-ttu-id="c5951-182">Creare un cluster HDInsight per usare Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="c5951-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
