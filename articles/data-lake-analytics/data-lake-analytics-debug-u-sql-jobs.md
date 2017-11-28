---
title: i processi aaaDebug U-SQL | Documenti Microsoft
description: "Informazioni su come toodebug U-SQL non è stato possibile vertice tramite Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="9684c-103">Eseguire il debug del codice C# definito dall'utente per i processi U-SQL non riusciti</span><span class="sxs-lookup"><span data-stu-id="9684c-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="9684c-104">U-SQL fornisce un modello di estendibilità Usa c#, pertanto è possibile scrivere la funzionalità di tooadd di codice, ad esempio un estrazione personalizzato o del reducer.</span><span class="sxs-lookup"><span data-stu-id="9684c-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="9684c-105">vedere, più toolearn [Guida programmabilità U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="9684c-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="9684c-106">In pratica un codice per cui potrebbe essere necessario il debug e i sistemi di dati di grandi dimensioni possono offrire solo informazioni sul debug del runtime quali i file di log.</span><span class="sxs-lookup"><span data-stu-id="9684c-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="9684c-107">Azure Data Lake Tools per Visual Studio fornisce una funzionalità denominata **non è stato possibile eseguire il Debug del vertice**, che consente di duplicare un processo non riuscito dal computer locale hello cloud tooyour per il debug.</span><span class="sxs-lookup"><span data-stu-id="9684c-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="9684c-108">clone locale Hello acquisisce l'ambiente cloud intera hello, inclusi eventuali dati di input e il codice utente.</span><span class="sxs-lookup"><span data-stu-id="9684c-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="9684c-109">Hello video seguente viene illustrato non è stato possibile vertice eseguire il Debug in Azure Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9684c-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="9684c-110">Visual Studio richiede hello seguenti due aggiornamenti, se non sono già installati: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Universal C Runtime per Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="9684c-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="9684c-111">Macchina toolocal vertice di download non riuscito</span><span class="sxs-lookup"><span data-stu-id="9684c-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="9684c-112">Quando si apre un processo non riuscito in Azure Data Lake Tools per Visual Studio, verrà visualizzata una barra di avviso gialla con messaggi di errore dettagliato nella scheda errore hello.</span><span class="sxs-lookup"><span data-stu-id="9684c-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="9684c-113">Fare clic su **scaricare** toodownload tutti hello necessarie risorse e i flussi di input.</span><span class="sxs-lookup"><span data-stu-id="9684c-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="9684c-114">Se non viene completato il download di hello, fare clic su **ripetere**.</span><span class="sxs-lookup"><span data-stu-id="9684c-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="9684c-115">Fare clic su **aprire** dopo il completamento di download di hello toogenerate un ambiente di debug locale.</span><span class="sxs-lookup"><span data-stu-id="9684c-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="9684c-116">Viene creata e aperta automaticamente una nuova istanza di Visual Studio con una soluzione di debug.</span><span class="sxs-lookup"><span data-stu-id="9684c-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Vertice download visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="9684c-118">I processi possono includere i file di origine code-behind o assembly registrati e questi due tipi presentano diversi scenari di debug.</span><span class="sxs-lookup"><span data-stu-id="9684c-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="9684c-119">Eseguire il debug di un processo non riuscito con code-behind</span><span class="sxs-lookup"><span data-stu-id="9684c-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="9684c-120">Eseguire il debug di un processo non riuscito con assembly</span><span class="sxs-lookup"><span data-stu-id="9684c-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="9684c-121">Debug di un processo con errori con code-behind</span><span class="sxs-lookup"><span data-stu-id="9684c-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="9684c-122">Se un processo U-SQL non riesce e il processo di hello include il codice utente (in genere denominato `Script.usql.cs` in un progetto U-SQL), che il codice sorgente viene importato in hello il debug delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9684c-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="9684c-123">Da qui è possibile utilizzare hello Visual Studio debug strumenti (espressioni di controllo, variabili e così via) tootroubleshoot hello problema.</span><span class="sxs-lookup"><span data-stu-id="9684c-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="9684c-124">Prima di debug, è che toocheck **eccezioni Common Language Runtime** nella finestra Impostazioni eccezioni hello (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="9684c-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Impostazione visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="9684c-126">Premere **F5** toorun hello codice il codice sottostante.</span><span class="sxs-lookup"><span data-stu-id="9684c-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="9684c-127">che verrà eseguito fino a quando non viene interrotto da un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9684c-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="9684c-128">Aprire hello `ADLTool_Codebehind.usql.cs` file e impostare i punti di interruzione, quindi premere **F5** codice hello toodebug dettagliate.</span><span class="sxs-lookup"><span data-stu-id="9684c-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Eccezione di debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="9684c-130">Debug di un processo con errori con assembly</span><span class="sxs-lookup"><span data-stu-id="9684c-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="9684c-131">Se si utilizzano gli assembly registrati in script U-SQL, sistema hello Impossibile ottenere il codice sorgente hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9684c-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="9684c-132">In questo caso, è possibile aggiungere manualmente la soluzione toohello degli assembly hello origine codice file.</span><span class="sxs-lookup"><span data-stu-id="9684c-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="9684c-133">Configurare la soluzione hello</span><span class="sxs-lookup"><span data-stu-id="9684c-133">Configure hello solution</span></span>

1. <span data-ttu-id="9684c-134">Fare doppio clic su **soluzione 'VertexDebug' > aggiungere > progetto esistente...**  toofind hello codice sorgente degli assembly e aggiungere toohello progetto hello il debug delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9684c-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL debug add project](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="9684c-136">Fare doppio clic su **LocalVertexHost > proprietà** in hello di soluzione e copia hello **la Directory di lavoro** percorso.</span><span class="sxs-lookup"><span data-stu-id="9684c-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="9684c-137">Fare doppio clic su **progetto del codice sorgente assembly > proprietà**selezionare hello **compilare** scheda a sinistra e incollare il percorso di hello copiato come **Output > percorso di Output**.</span><span class="sxs-lookup"><span data-stu-id="9684c-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Percorso pdb impostato per il debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="9684c-139">Premere **CTRL + ALT + E**, controllare le **eccezioni di Common Language Runtime** nella finestra Impostazioni eccezioni.</span><span class="sxs-lookup"><span data-stu-id="9684c-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="9684c-140">Avviare il debug</span><span class="sxs-lookup"><span data-stu-id="9684c-140">Start debug</span></span>

1. <span data-ttu-id="9684c-141">Fare doppio clic su **progetto del codice sorgente assembly > ricompilare** toohello i file con estensione pdb toooutput `LocalVertexHost` directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9684c-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="9684c-142">Premere **F5** e hello progetto verrà eseguito fino a quando non è stato arrestato da un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9684c-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="9684c-143">Si può vedere hello seguente messaggio di avviso, è possibile ignorare.</span><span class="sxs-lookup"><span data-stu-id="9684c-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="9684c-144">Può richiedere tooa tooget minuti toohello debug schermata verso l'alto.</span><span class="sxs-lookup"><span data-stu-id="9684c-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Avviso visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="9684c-146">Aprire il codice sorgente e impostare i punti di interruzione, quindi premere **F5** codice hello toodebug dettagliate.</span><span class="sxs-lookup"><span data-stu-id="9684c-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="9684c-147">È inoltre possibile utilizzare hello Visual Studio debug strumenti (espressioni di controllo, variabili e così via) tootroubleshoot hello problema.</span><span class="sxs-lookup"><span data-stu-id="9684c-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="9684c-148">Ricompilare progetto del codice sorgente hello assembly ogni volta dopo aver modificato i file con estensione pdb toogenerate aggiornati di codice hello.</span><span class="sxs-lookup"><span data-stu-id="9684c-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="9684c-149">Dopo il debug, se il progetto hello viene completata correttamente finestra di output di hello Visualizza hello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="9684c-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Debug U-SQL in Azure Data Lake Analytics completato correttamente](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="9684c-151">Inviare di nuovo il processo di hello</span><span class="sxs-lookup"><span data-stu-id="9684c-151">Resubmit hello job</span></span>

<span data-ttu-id="9684c-152">Dopo aver completato il debug, eseguire nuovamente il processo non riuscito di hello.</span><span class="sxs-lookup"><span data-stu-id="9684c-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="9684c-153">Per i processi con soluzioni di codice, copiare il codice c# in file di origine code-behind hello (in genere `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="9684c-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="9684c-154">Per i processi con gli assembly, registrare l'assembly DLL hello aggiornato nel database ADLA:</span><span class="sxs-lookup"><span data-stu-id="9684c-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="9684c-155">In Esplora Server o Cloud Explorer espandere hello **account ADLA > database** nodo.</span><span class="sxs-lookup"><span data-stu-id="9684c-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="9684c-156">Fare doppio clic su **assembly** e registrare il nuovo assembly DLL con database ADLA hello: ![debug U-SQL di Azure Data Lake Analitica registrare assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="9684c-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="9684c-157">Inviare di nuovo il processo.</span><span class="sxs-lookup"><span data-stu-id="9684c-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9684c-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9684c-158">Next steps</span></span>

- [<span data-ttu-id="9684c-159">Guida di programmabilità di U-SQL</span><span class="sxs-lookup"><span data-stu-id="9684c-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="9684c-160">Sviluppare operatori U-SQL definiti dall'utente per i processi di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9684c-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="9684c-161">Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9684c-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
