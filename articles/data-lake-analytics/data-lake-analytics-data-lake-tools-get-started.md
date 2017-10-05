---
title: Sviluppare script U-SQL tramite Strumenti Data Lake per Visual Studio | Microsoft Docs
description: Informazioni su come installare Strumenti Data Lake per Visual Studio e come sviluppare e testare script U-SQL.
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
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="bcddd-103">Sviluppare script U-SQL tramite Strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcddd-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="bcddd-104">Informazioni su come usare Visual Studio per creare account Azure Data Lake Analytics, definire processi in [U-SQL](data-lake-analytics-u-sql-get-started.md) e inviare processi al servizio Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcddd-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="bcddd-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcddd-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bcddd-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bcddd-106">Prerequisites</span></span>

* <span data-ttu-id="bcddd-107">**Visual Studio**: sono supportate tutte le versioni ad eccezione della versione Express.</span><span class="sxs-lookup"><span data-stu-id="bcddd-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="bcddd-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bcddd-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="bcddd-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bcddd-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="bcddd-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bcddd-110">Visual Studio 2013</span></span>
* <span data-ttu-id="bcddd-111">**Microsoft Azure SDK per .NET** versione 2.7.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="bcddd-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="bcddd-112">Eseguire l'installazione usando [Installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="bcddd-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="bcddd-113">Un account **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="bcddd-114">Per creare un account, vedere [Introduzione ad Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bcddd-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="bcddd-115">Installare Strumenti Azure Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcddd-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="bcddd-116">Scaricare e installare Strumenti Azure Data Lake per Visual Studio dall'[Area download](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="bcddd-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="bcddd-117">Dopo l'installazione si noti che:</span><span class="sxs-lookup"><span data-stu-id="bcddd-117">After installation, note that:</span></span>
* <span data-ttu-id="bcddd-118">Il nodo **Esplora server** > **Azure** contiene un nodo **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="bcddd-119">Il menu **Strumenti** include una voce **Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="bcddd-120">Connettersi a un account Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="bcddd-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="bcddd-121">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bcddd-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="bcddd-122">Aprire Esplora server selezionando **Visualizza** > **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="bcddd-123">Fare clic con il pulsante destro del mouse su **Azure**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-123">Right-click **Azure**.</span></span> <span data-ttu-id="bcddd-124">Scegliere quindi **Connetti a sottoscrizione di Microsoft Azure** e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="bcddd-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="bcddd-125">In Esplora server selezionare **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="bcddd-126">Verrà visualizzato un elenco degli account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcddd-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="bcddd-127">Scrivere il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="bcddd-127">Write your first U-SQL script</span></span>

<span data-ttu-id="bcddd-128">Il testo seguente è un semplice script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bcddd-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="bcddd-129">Definisce un set di dati di piccole dimensioni e scrive tale set di dati nell'istanza predefinita di Data Lake Store come file denominato `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="bcddd-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="bcddd-130">Inviare un processo di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="bcddd-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="bcddd-131">Selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="bcddd-132">Selezionare il tipo di **Progetto U-SQL** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="bcddd-133">Visual Studio crea una soluzione con un file **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="bcddd-134">Incollare lo script precedente nella finestra **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="bcddd-135">Nell'angolo superiore sinistro della finestra **Script.usql** specificare l'account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcddd-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="bcddd-137">Nell'angolo superiore sinistro della finestra **Script.usql** selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="bcddd-138">Verificare il nome presente in **Account Analytics** e quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="bcddd-139">Al termine dell'invio, nella finestra dei risultati di Strumenti Data Lake per Visual Studio saranno disponibili i risultati dell'operazione di invio.</span><span class="sxs-lookup"><span data-stu-id="bcddd-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="bcddd-141">Per visualizzare lo stato più aggiornato del processo e aggiornare la schermata, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="bcddd-142">Quando il processo ha esito positivo, vengono visualizzate le schede **Grafico del processo**, **Operazioni metadati**, **Cronologia dello stato** e **Diagnostica**:</span><span class="sxs-lookup"><span data-stu-id="bcddd-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Grafico delle prestazioni del processo di Analisi Data Lake per Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="bcddd-144">**Riepilogo processo** mostra il riepilogo del processo.</span><span class="sxs-lookup"><span data-stu-id="bcddd-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="bcddd-145">**Dettagli processo** mostra informazioni più specifiche sul processo, inclusi script, risorse e vertici.</span><span class="sxs-lookup"><span data-stu-id="bcddd-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="bcddd-146">**Grafico del processo** visualizza l'andamento del processo.</span><span class="sxs-lookup"><span data-stu-id="bcddd-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="bcddd-147">**Operazioni metadati** mostra tutte le azioni eseguite nel catalogo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bcddd-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="bcddd-148">**Dati** mostra tutti gli input e gli output.</span><span class="sxs-lookup"><span data-stu-id="bcddd-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="bcddd-149">**Diagnostica** fornisce un'analisi avanzata per l'ottimizzazione dell'esecuzione e delle prestazioni del processo.</span><span class="sxs-lookup"><span data-stu-id="bcddd-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="bcddd-150">Per controllare lo stato del processo</span><span class="sxs-lookup"><span data-stu-id="bcddd-150">To check job state</span></span>

1. <span data-ttu-id="bcddd-151">In Esplora server selezionare **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="bcddd-152">Espandere il nome dell'account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcddd-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="bcddd-153">Fare doppio clic su **Processi**.</span><span class="sxs-lookup"><span data-stu-id="bcddd-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="bcddd-154">Selezionare il processo inviato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bcddd-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="bcddd-155">Per visualizzare l'output di un processo</span><span class="sxs-lookup"><span data-stu-id="bcddd-155">To see the output of a job</span></span>

1. <span data-ttu-id="bcddd-156">In Esplora server cercare il processo inviato.</span><span class="sxs-lookup"><span data-stu-id="bcddd-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="bcddd-157">Fare clic sulla scheda **Dati** .</span><span class="sxs-lookup"><span data-stu-id="bcddd-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="bcddd-158">Nella scheda **Output del processo** selezionare il file `"/data.csv"`.</span><span class="sxs-lookup"><span data-stu-id="bcddd-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcddd-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bcddd-159">Next steps</span></span>

* [<span data-ttu-id="bcddd-160">Eseguire script U-SQL nella workstation per test e debug</span><span class="sxs-lookup"><span data-stu-id="bcddd-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="bcddd-161">Debug dei processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="bcddd-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="bcddd-162">Usare gli strumenti di Azure Data Lake per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bcddd-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
