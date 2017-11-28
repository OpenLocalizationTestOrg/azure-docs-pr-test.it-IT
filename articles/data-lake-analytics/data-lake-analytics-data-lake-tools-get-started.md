---
title: script di aaaDevelop U-SQL utilizzando Data Lake Tools per Visual Studio | Documenti Microsoft
description: Informazioni su come tooinstall Data Lake di strumenti per Visual Studio e come toodevelop e testare script U-SQL.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d5858-103">Sviluppare script U-SQL tramite Strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5858-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="d5858-104">Informazioni su come account di Azure Data Lake Analitica toocreate Visual Studio toouse, definire i processi in [U-SQL](data-lake-analytics-u-sql-get-started.md)e l'invio del servizio Data Lake Analitica toohello di processi.</span><span class="sxs-lookup"><span data-stu-id="d5858-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="d5858-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5858-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d5858-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5858-106">Prerequisites</span></span>

* <span data-ttu-id="d5858-107">**Visual Studio**: sono supportate tutte le versioni ad eccezione della versione Express.</span><span class="sxs-lookup"><span data-stu-id="d5858-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="d5858-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d5858-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="d5858-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d5858-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="d5858-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5858-110">Visual Studio 2013</span></span>
* <span data-ttu-id="d5858-111">**Microsoft Azure SDK per .NET** versione 2.7.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d5858-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="d5858-112">Installarlo utilizzando hello [installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5858-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="d5858-113">Un account **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5858-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="d5858-114">toocreate un account, vedere [Guida introduttiva di Azure Data Lake Analitica tramite il portale di Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5858-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d5858-115">Installare Strumenti Azure Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5858-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="d5858-116">Scaricare e installare Azure Data Lake Tools per Visual Studio [dall'area Download hello](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="d5858-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="d5858-117">Dopo l'installazione si noti che:</span><span class="sxs-lookup"><span data-stu-id="d5858-117">After installation, note that:</span></span>
* <span data-ttu-id="d5858-118">Hello **Esplora Server** > **Azure** nodo contiene un **Data Lake Analitica** nodo.</span><span class="sxs-lookup"><span data-stu-id="d5858-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="d5858-119">Hello **strumenti** menu è un **Data Lake** elemento.</span><span class="sxs-lookup"><span data-stu-id="d5858-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="d5858-120">Connettere l'account di Azure Data Lake Analitica tooan</span><span class="sxs-lookup"><span data-stu-id="d5858-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="d5858-121">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5858-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="d5858-122">Aprire Esplora server selezionando **Visualizza** > **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="d5858-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="d5858-123">Fare clic con il pulsante destro del mouse su **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d5858-123">Right-click **Azure**.</span></span> <span data-ttu-id="d5858-124">Selezionare quindi **tooMicrosoft sottoscrizione di Azure connettersi** e seguire le istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="d5858-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="d5858-125">In Esplora server selezionare **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5858-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="d5858-126">Verrà visualizzato un elenco degli account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d5858-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="d5858-127">Scrivere il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="d5858-127">Write your first U-SQL script</span></span>

<span data-ttu-id="d5858-128">Dopo il testo Hello è un semplice script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5858-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="d5858-129">Definisce un set di dati di piccole dimensioni e le scritture archivio dataset toohello predefinito Data Lake come un file denominato `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="d5858-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="d5858-130">Inviare un processo di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d5858-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="d5858-131">Selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="d5858-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="d5858-132">Seleziona hello **progetto U-SQL** digitare e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5858-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="d5858-133">Visual Studio crea una soluzione con un file **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="d5858-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="d5858-134">Incollare script precedente hello hello **Script.usql** finestra.</span><span class="sxs-lookup"><span data-stu-id="d5858-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="d5858-135">Nell'angolo superiore sinistro hello di hello **Script.usql** finestra, specificare l'account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="d5858-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="d5858-137">Nell'angolo superiore sinistro hello di hello **Script.usql** selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="d5858-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="d5858-138">Verificare hello **Account Analitica**, quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="d5858-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="d5858-139">Risultati di invio sono disponibili in hello Data Lake Tools per Visual Studio risultati dopo l'invio di hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="d5858-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="d5858-141">toosee hello più recente processo lo stato e aggiornamento schermata ciao, fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="d5858-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="d5858-142">Quando il processo di hello ha esito positivo, viene visualizzato hello **grafico processi**, **operazioni sui metadati**, **cronologia dello stato**, e **diagnostica**:</span><span class="sxs-lookup"><span data-stu-id="d5858-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Grafico delle prestazioni del processo di Analisi Data Lake per Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="d5858-144">**Riepilogo processo** Mostra hello riepilogo del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="d5858-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="d5858-145">**I dettagli dei processi** Mostra informazioni più specifiche sul processo di hello, inclusi script hello, risorse e i vertici.</span><span class="sxs-lookup"><span data-stu-id="d5858-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="d5858-146">**Grafico processi** Visualizza lo stato di avanzamento hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="d5858-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="d5858-147">**Operazioni sui metadati** Mostra tutte le azioni hello che sono state eseguite nel catalogo di hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5858-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="d5858-148">**Dati** Mostra tutti gli input hello e output.</span><span class="sxs-lookup"><span data-stu-id="d5858-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="d5858-149">**Diagnostica** fornisce un'analisi avanzata per l'ottimizzazione dell'esecuzione e delle prestazioni del processo.</span><span class="sxs-lookup"><span data-stu-id="d5858-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="d5858-150">stato del processo toocheck</span><span class="sxs-lookup"><span data-stu-id="d5858-150">toocheck job state</span></span>

1. <span data-ttu-id="d5858-151">In Esplora server selezionare **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5858-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="d5858-152">Espandere nome dell'account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="d5858-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="d5858-153">Fare doppio clic su **Processi**.</span><span class="sxs-lookup"><span data-stu-id="d5858-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="d5858-154">Selezionare il processo hello inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d5858-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="d5858-155">output di hello toosee di un processo</span><span class="sxs-lookup"><span data-stu-id="d5858-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="d5858-156">In Esplora Server, passare toohello processo che è stato inviato.</span><span class="sxs-lookup"><span data-stu-id="d5858-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="d5858-157">Fare clic su hello **dati** scheda.</span><span class="sxs-lookup"><span data-stu-id="d5858-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="d5858-158">In hello **gli output dei processi** scheda, seleziona hello `"/data.csv"` file.</span><span class="sxs-lookup"><span data-stu-id="d5858-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5858-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5858-159">Next steps</span></span>

* [<span data-ttu-id="d5858-160">Eseguire script U-SQL nella workstation per test e debug</span><span class="sxs-lookup"><span data-stu-id="d5858-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="d5858-161">Debug dei processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="d5858-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="d5858-162">Utilizzare hello Azure Data Lake Tools per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d5858-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
