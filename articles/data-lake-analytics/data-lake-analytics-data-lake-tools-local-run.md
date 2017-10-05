---
title: Eseguire test e debug di processi U-SQL tramite l'esecuzione locale e l'SDK U-SQL di Azure Data Lake | Microsoft Docs
description: Informazioni su come usare gli strumenti di Azure Data Lake per Visual Studio e l'SDK U-SQL di Azure Data Lake per eseguire test e debug dei processi di U-SQL nella workstation locale.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="10bd7-103">Eseguire test e debug di processi U-SQL tramite l'esecuzione locale e l'SDK U-SQL di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="10bd7-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="10bd7-104">È possibile usare Strumenti di Azure Data Lake per Visual Studio e l'SDK U-SQL di Azure Data Lake per eseguire i processi di U-SQL nella workstation, esattamente come nel servizio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="10bd7-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="10bd7-105">Queste due funzionalità eseguite localmente permettono di risparmiare tempo per le operazioni di test e debug dei processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10bd7-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="10bd7-106">Comprendere la cartella data-root e il percorso dei file</span><span class="sxs-lookup"><span data-stu-id="10bd7-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="10bd7-107">Sia l'SDK di U-SQL che l'esecuzione locale richiedono una cartella data-root.</span><span class="sxs-lookup"><span data-stu-id="10bd7-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="10bd7-108">La cartella data-root è un "archivio locale" per l'account di calcolo locale,</span><span class="sxs-lookup"><span data-stu-id="10bd7-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="10bd7-109">equivalente all'account di Azure Data Lake Store di un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="10bd7-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="10bd7-110">Il passaggio a un'altra cartella data-root è identico al passaggio a un account archivio differente.</span><span class="sxs-lookup"><span data-stu-id="10bd7-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="10bd7-111">Se si vuole accedere a dati comunemente condivisi con cartelle data-root diverse, è necessario usare percorsi assoluti negli script.</span><span class="sxs-lookup"><span data-stu-id="10bd7-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="10bd7-112">In alternativa è possibile creare collegamenti simbolici del file system (ad esempio **mklink** in un sistema NTFS) nella cartella data-root che puntino ai dati condivisi.</span><span class="sxs-lookup"><span data-stu-id="10bd7-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="10bd7-113">La cartella data-root viene usata per:</span><span class="sxs-lookup"><span data-stu-id="10bd7-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="10bd7-114">Archiviare i metadati, inclusi database, tabelle, funzione con valori di tabella e assembly.</span><span class="sxs-lookup"><span data-stu-id="10bd7-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="10bd7-115">Cercare i percorsi di input e output che sono definiti come percorsi relativi in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10bd7-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="10bd7-116">L'uso di percorsi relativi semplifica la distribuzione dei progetti di U-SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="10bd7-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="10bd7-117">Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale.</span><span class="sxs-lookup"><span data-stu-id="10bd7-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="10bd7-118">Il percorso relativo è relativo al percorso della cartella data-root specificato.</span><span class="sxs-lookup"><span data-stu-id="10bd7-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="10bd7-119">È consigliabile usare "/" come separatore del percorso per rendere gli script compatibili con il lato server.</span><span class="sxs-lookup"><span data-stu-id="10bd7-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="10bd7-120">Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="10bd7-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="10bd7-121">In questi esempi la cartella data-root è C:\LocalRunDataRoot.</span><span class="sxs-lookup"><span data-stu-id="10bd7-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="10bd7-122">Percorso relativo</span><span class="sxs-lookup"><span data-stu-id="10bd7-122">Relative path</span></span>|<span data-ttu-id="10bd7-123">Percorso assoluto</span><span class="sxs-lookup"><span data-stu-id="10bd7-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="10bd7-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-124">/abc/def/input.csv</span></span> |<span data-ttu-id="10bd7-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="10bd7-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-126">abc/def/input.csv</span></span>  |<span data-ttu-id="10bd7-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="10bd7-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="10bd7-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10bd7-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="10bd7-130">Usare l'esecuzione locale per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10bd7-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="10bd7-131">Gli Strumenti di Data Lake per Visual Studio offrono un'esperienza di esecuzione locale di U-SQL in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10bd7-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="10bd7-132">Questa funzionalità permette di:</span><span class="sxs-lookup"><span data-stu-id="10bd7-132">By using this feature, you can:</span></span>

- <span data-ttu-id="10bd7-133">Eseguire uno script U-SQL in locale, insieme agli assembly C#.</span><span class="sxs-lookup"><span data-stu-id="10bd7-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="10bd7-134">Eseguire il debug di un assembly C# localmente.</span><span class="sxs-lookup"><span data-stu-id="10bd7-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="10bd7-135">Creare, visualizzare ed eliminare i cataloghi di U-SQL (database locali, assembly, schemi e tabelle) da Esplora server.</span><span class="sxs-lookup"><span data-stu-id="10bd7-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="10bd7-136">Il catalogo locale è disponibile anche in Esplora server.</span><span class="sxs-lookup"><span data-stu-id="10bd7-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Catalogo locale dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="10bd7-138">Il programma di installazione di Strumenti di Data Lake crea la cartella C:\LocalRunRoot che diventa la cartella data-root predefinita.</span><span class="sxs-lookup"><span data-stu-id="10bd7-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="10bd7-139">Il parallelismo di esecuzione locale predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="10bd7-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="10bd7-140">Configurare l'esecuzione locale in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10bd7-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="10bd7-141">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10bd7-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="10bd7-142">Aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="10bd7-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="10bd7-143">Espandere **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="10bd7-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="10bd7-144">Aprire il menu **Data Lake** e fare clic su **Opzioni e impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="10bd7-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="10bd7-145">Nella struttura ad albero a sinistra espandere **Azure Data Lake** e **Generale**.</span><span class="sxs-lookup"><span data-stu-id="10bd7-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Impostazioni di configurazione dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="10bd7-147">Per poter eseguire la funzionalità di esecuzione locale è richiesto un progetto U-SQL di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10bd7-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="10bd7-148">Questa parte è diversa rispetto all'esecuzione di script U-SQL da Azure.</span><span class="sxs-lookup"><span data-stu-id="10bd7-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="10bd7-149">Eseguire uno script U-SQL localmente</span><span class="sxs-lookup"><span data-stu-id="10bd7-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="10bd7-150">Aprire il progetto U-SQL in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10bd7-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="10bd7-151">In Esplora soluzioni fare clic con il pulsante destro del mouse su uno script U-SQL e selezionare **Invia script**.</span><span class="sxs-lookup"><span data-stu-id="10bd7-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="10bd7-152">Selezionare **(Locale)** come account di Analytics per eseguire lo script in locale.</span><span class="sxs-lookup"><span data-stu-id="10bd7-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="10bd7-153">È anche possibile fare clic sull'account **(Locale)** nella parte superiore della finestra dello script, quindi selezionare **Invia** (o usare la combinazione di tasti CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="10bd7-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Processi di invio dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="10bd7-155">Eseguire il debug degli script e delle assembly C# in locale</span><span class="sxs-lookup"><span data-stu-id="10bd7-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="10bd7-156">È possibile eseguire il debug degli assembly C# senza inviarli e registrarli al servizio Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="10bd7-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="10bd7-157">È possibile impostare dei punti di interruzione sia nei file dietro il codice, sia nel progetto C# a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="10bd7-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="10bd7-158">Per eseguire il debug del codice locale nel file code-behind</span><span class="sxs-lookup"><span data-stu-id="10bd7-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="10bd7-159">Impostare dei punti di interruzione nel file dietro il codice.</span><span class="sxs-lookup"><span data-stu-id="10bd7-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="10bd7-160">Premere F5 per eseguire il debug dello script in locale.</span><span class="sxs-lookup"><span data-stu-id="10bd7-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="10bd7-161">La procedura seguente funziona solo in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="10bd7-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="10bd7-162">Nella versione precedente di Visual Studio potrebbe essere necessario aggiungere manualmente i file .pdb.</span><span class="sxs-lookup"><span data-stu-id="10bd7-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="10bd7-163">Per eseguire il debug del codice locale in un progetto C# a cui si fa riferimento</span><span class="sxs-lookup"><span data-stu-id="10bd7-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="10bd7-164">Creare un progetto Assembly C# e compilarlo per generare l’output dll.</span><span class="sxs-lookup"><span data-stu-id="10bd7-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="10bd7-165">Registrare la dll utilizzando un'istruzione U-SQL:</span><span class="sxs-lookup"><span data-stu-id="10bd7-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="10bd7-166">Impostare i punti di interruzione nel codice C#.</span><span class="sxs-lookup"><span data-stu-id="10bd7-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="10bd7-167">Premere F5 per eseguire il debug dello script con riferimento alla DLL C# in locale.</span><span class="sxs-lookup"><span data-stu-id="10bd7-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="10bd7-168">Usare l'esecuzione locale dall'SDK U-SQL di Data Lake</span><span class="sxs-lookup"><span data-stu-id="10bd7-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="10bd7-169">Oltre a eseguire gli script U-SQL localmente con Visual Studio, è possibile usare anche l'SDK U-SQL di Azure Data Lake per eseguire gli script U-SQL localmente con le interfacce della riga di comando e di programmazione.</span><span class="sxs-lookup"><span data-stu-id="10bd7-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="10bd7-170">In questo modo è possibile scalare il test locale di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10bd7-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="10bd7-171">Sono disponibili altre informazioni sull'[SDK U-SQL di Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="10bd7-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="10bd7-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10bd7-172">Next steps</span></span>

* <span data-ttu-id="10bd7-173">Per visualizzare una query più complessa, vedere [Analizzare i log dei siti Web con Analisi Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="10bd7-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="10bd7-174">Per visualizzare i dettagli del processo, vedere [Usare Job Browser e Job View (Visualizzazione processo) per i processi di Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="10bd7-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="10bd7-175">Per usare la visualizzazione esecuzioni vertici, vedere [Usare la visualizzazione esecuzioni vertici in Azure Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="10bd7-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
