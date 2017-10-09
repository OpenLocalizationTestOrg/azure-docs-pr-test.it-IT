---
title: aaaTest debug U-SQL processi utilizzando locali eseguire ed e hello Azure Data Lake U-SQL SDK | Documenti Microsoft
description: Informazioni su come toouse Azure Data Lake Tools per Visual Studio e hello Azure Data Lake U-SQL SDK tootest debug U-SQL per i processi nella workstation locale.
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
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="9960f-103">Test e il debug di processi U-SQL utilizzando locale eseguire e hello SDK Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="9960f-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="9960f-104">È possibile utilizzare Azure Data Lake Tools per Visual Studio e i processi di hello Azure Data Lake U-SQL SDK toorun U-SQL nella workstation, come nel servizio Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="9960f-105">Queste due funzionalità eseguite localmente permettono di risparmiare tempo per le operazioni di test e debug dei processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9960f-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="9960f-106">Comprendere cartella dati radice hello e percorso del file hello</span><span class="sxs-lookup"><span data-stu-id="9960f-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="9960f-107">Esecuzione locale sia hello SDK U-SQL richiedono una cartella radice di dati.</span><span class="sxs-lookup"><span data-stu-id="9960f-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="9960f-108">cartella dati radice Hello è "archivio locale" per l'account di calcolo locale hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="9960f-109">Account archivio Azure Data Lake toohello equivalente di un account Data Lake Analitica è.</span><span class="sxs-lookup"><span data-stu-id="9960f-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="9960f-110">Cartella radice di dati diverso cambio tooa è analoga a commutazione tooa archivio diverso account.</span><span class="sxs-lookup"><span data-stu-id="9960f-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="9960f-111">Se si desidera tooaccess comunemente condiviso dati con le cartelle radice di dati diverso, è necessario utilizzare i percorsi assoluti negli script.</span><span class="sxs-lookup"><span data-stu-id="9960f-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="9960f-112">In alternativa, creare collegamenti simbolici di file system (ad esempio, **mklink** in NTFS) in hello dati radice cartella toopoint toohello di dati condivisi.</span><span class="sxs-lookup"><span data-stu-id="9960f-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="9960f-113">cartella dati radice Hello viene utilizzato per:</span><span class="sxs-lookup"><span data-stu-id="9960f-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="9960f-114">Archiviare i metadati, inclusi database, tabelle, funzione con valori di tabella e assembly.</span><span class="sxs-lookup"><span data-stu-id="9960f-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="9960f-115">Cercare hello di input e i percorsi di output che sono definiti come percorsi relativi nel U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9960f-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="9960f-116">Utilizzando i percorsi relativi rende più semplice toodeploy il tooAzure progetti U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9960f-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="9960f-117">Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale.</span><span class="sxs-lookup"><span data-stu-id="9960f-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="9960f-118">percorso relativo di Hello è toohello relativo percorso della cartella radice di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="9960f-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="9960f-119">È consigliabile che si utilizza "/" come script compatibili con lato server hello hello toomake separatore di percorso.</span><span class="sxs-lookup"><span data-stu-id="9960f-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="9960f-120">Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="9960f-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="9960f-121">In questi esempi, C:\LocalRunDataRoot è cartella dati radice hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="9960f-122">Percorso relativo</span><span class="sxs-lookup"><span data-stu-id="9960f-122">Relative path</span></span>|<span data-ttu-id="9960f-123">Percorso assoluto</span><span class="sxs-lookup"><span data-stu-id="9960f-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="9960f-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-124">/abc/def/input.csv</span></span> |<span data-ttu-id="9960f-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="9960f-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-126">abc/def/input.csv</span></span>  |<span data-ttu-id="9960f-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="9960f-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="9960f-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9960f-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="9960f-130">Usare l'esecuzione locale per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9960f-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="9960f-131">Gli Strumenti di Data Lake per Visual Studio offrono un'esperienza di esecuzione locale di U-SQL in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9960f-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="9960f-132">Questa funzionalità permette di:</span><span class="sxs-lookup"><span data-stu-id="9960f-132">By using this feature, you can:</span></span>

- <span data-ttu-id="9960f-133">Eseguire uno script U-SQL in locale, insieme agli assembly C#.</span><span class="sxs-lookup"><span data-stu-id="9960f-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="9960f-134">Eseguire il debug di un assembly C# localmente.</span><span class="sxs-lookup"><span data-stu-id="9960f-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="9960f-135">Creare, visualizzare ed eliminare i cataloghi di U-SQL (database locali, assembly, schemi e tabelle) da Esplora server.</span><span class="sxs-lookup"><span data-stu-id="9960f-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="9960f-136">È inoltre possibile trovare catalogo locale hello anche da Esplora Server.</span><span class="sxs-lookup"><span data-stu-id="9960f-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Catalogo locale dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="9960f-138">programma di installazione del Data Lake Tools Hello crea un toobe cartella C:\LocalRunRoot utilizzata come cartella radice dati predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="9960f-139">il parallelismo di esecuzione locale di Hello predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="9960f-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="9960f-140">tooconfigure locale eseguito in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9960f-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="9960f-141">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9960f-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="9960f-142">Aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="9960f-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="9960f-143">Espandere **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9960f-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="9960f-144">Fare clic su hello **Data Lake** menu e quindi fare clic su **opzioni e impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="9960f-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="9960f-145">Nell'albero a sinistra hello espandere **Azure Data Lake**, quindi espandere **generale**.</span><span class="sxs-lookup"><span data-stu-id="9960f-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Impostazioni di configurazione dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="9960f-147">Per poter eseguire la funzionalità di esecuzione locale è richiesto un progetto U-SQL di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9960f-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="9960f-148">Questa parte è diversa rispetto all'esecuzione di script U-SQL da Azure.</span><span class="sxs-lookup"><span data-stu-id="9960f-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="9960f-149">script U-SQL toorun localmente</span><span class="sxs-lookup"><span data-stu-id="9960f-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="9960f-150">Aprire il progetto U-SQL in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9960f-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="9960f-151">In Esplora soluzioni fare clic con il pulsante destro del mouse su uno script U-SQL e selezionare **Invia script**.</span><span class="sxs-lookup"><span data-stu-id="9960f-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="9960f-152">Selezionare **(Local)** hello Analitica account RunAs toorun lo script in locale.</span><span class="sxs-lookup"><span data-stu-id="9960f-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="9960f-153">È anche possibile fare clic su hello **(Local)** account nella parte superiore di hello della finestra di script e quindi fare clic su **Invia** (o utilizzare hello Ctrl + tasto di scelta rapida di F5).</span><span class="sxs-lookup"><span data-stu-id="9960f-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Processi di invio dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="9960f-155">Eseguire il debug degli script e delle assembly C# in locale</span><span class="sxs-lookup"><span data-stu-id="9960f-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="9960f-156">È possibile eseguire il debug di assembly c# senza l'invio e la relativa registrazione tooAzure Data Lake Analitica Service.</span><span class="sxs-lookup"><span data-stu-id="9960f-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="9960f-157">È possibile impostare i punti di interruzione in entrambi hello file code-behind e in un progetto c# a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="9960f-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="9960f-158">toodebug codice locale nel file code-behind</span><span class="sxs-lookup"><span data-stu-id="9960f-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="9960f-159">Impostare i punti di interruzione nel codice hello file code-behind.</span><span class="sxs-lookup"><span data-stu-id="9960f-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="9960f-160">Premere F5 toodebug hello script in locale.</span><span class="sxs-lookup"><span data-stu-id="9960f-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="9960f-161">Hello seguente procedura funziona solo in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9960f-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="9960f-162">In Visual Studio precedente potrebbe essere necessario toomanually aggiungere i file pdb hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="9960f-163">toodebug codice locale in un progetto di cui viene fatto riferimento in c#</span><span class="sxs-lookup"><span data-stu-id="9960f-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="9960f-164">Creare un progetto c# Assembly e compilarlo toogenerate hello dll di output.</span><span class="sxs-lookup"><span data-stu-id="9960f-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="9960f-165">Registrare dll hello utilizzando un'istruzione U-SQL:</span><span class="sxs-lookup"><span data-stu-id="9960f-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="9960f-166">Impostare i punti di interruzione nel codice c# di hello.</span><span class="sxs-lookup"><span data-stu-id="9960f-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="9960f-167">Premere F5 script di hello toodebug con riferimento a dll c# hello in locale.</span><span class="sxs-lookup"><span data-stu-id="9960f-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="9960f-168">Utilizzo locale esecuzione da hello SDK Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="9960f-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="9960f-169">Inoltre toorunning U-SQL script localmente utilizzando Visual Studio, è possibile utilizzare gli script U-SQL di hello Azure Data Lake U-SQL SDK toorun localmente con le interfacce della riga di comando e di programmazione.</span><span class="sxs-lookup"><span data-stu-id="9960f-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="9960f-170">In questo modo è possibile scalare il test locale di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9960f-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="9960f-171">Sono disponibili altre informazioni sull'[SDK U-SQL di Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9960f-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9960f-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9960f-172">Next steps</span></span>

* <span data-ttu-id="9960f-173">toosee una query più complessa, vedere [analizzare i log di sito Web usando Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="9960f-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="9960f-174">vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data Lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="9960f-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="9960f-175">visualizzazione di esecuzione vertice hello toouse, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="9960f-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
