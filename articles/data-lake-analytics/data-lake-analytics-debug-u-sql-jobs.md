---
title: Debug dei processi U-SQL | Documentazione Microsoft
description: Informazioni su come eseguire il debug del vertice non riuscito di U-SQL con Visual Studio.
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
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="a8220-103">Eseguire il debug del codice C# definito dall'utente per i processi U-SQL non riusciti</span><span class="sxs-lookup"><span data-stu-id="a8220-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="a8220-104">U-SQL offre un modello estendibilità che usa C#, pertanto è possibile scrivere il codice per aggiungere funzionalità quali un estrattore o riduttore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a8220-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="a8220-105">Per altre informazioni vedere [Guida alla programmabilità di U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="a8220-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="a8220-106">In pratica un codice per cui potrebbe essere necessario il debug e i sistemi di dati di grandi dimensioni possono offrire solo informazioni sul debug del runtime quali i file di log.</span><span class="sxs-lookup"><span data-stu-id="a8220-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="a8220-107">Strumenti Azure Data Lake per Visual Studio offre una funzionalità denominata **Debug del vertice con errore**, che consente di clonare un processo non riuscito dal cloud nel computer locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="a8220-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="a8220-108">Il clone locale acquisisce tutto l'ambiente cloud, inclusi eventuali dati di input e il codice utente.</span><span class="sxs-lookup"><span data-stu-id="a8220-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="a8220-109">Nel video seguente viene illustrata la funzione Debug del vertice con errore in Strumenti Azure Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8220-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="a8220-110">Se non sono già installati Visual Studio richiede i due aggiornamenti seguenti: [Aggiornamento di Microsoft Visual C++ 2015 Redistributable 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Universal C Runtime per Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="a8220-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="a8220-111">Scaricare il vertice con errori nel computer locale</span><span class="sxs-lookup"><span data-stu-id="a8220-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="a8220-112">Quando si apre un processo non riuscito in Strumenti Azure Data Lake per Visual Studio, viene visualizzata una barra di avviso gialla con messaggi di errore dettagliati nella scheda errore.</span><span class="sxs-lookup"><span data-stu-id="a8220-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="a8220-113">Fare clic su **Scarica** per scaricare tutte le risorse e i flussi di input necessari.</span><span class="sxs-lookup"><span data-stu-id="a8220-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="a8220-114">Se il download non viene completato, fare clic su **Riprova**.</span><span class="sxs-lookup"><span data-stu-id="a8220-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="a8220-115">Fare clic su **Apri** dopo aver completato il download per generare l'ambiente di debug locale.</span><span class="sxs-lookup"><span data-stu-id="a8220-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="a8220-116">Viene creata e aperta automaticamente una nuova istanza di Visual Studio con una soluzione di debug.</span><span class="sxs-lookup"><span data-stu-id="a8220-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Vertice download visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="a8220-118">I processi possono includere i file di origine code-behind o assembly registrati e questi due tipi presentano diversi scenari di debug.</span><span class="sxs-lookup"><span data-stu-id="a8220-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="a8220-119">Eseguire il debug di un processo non riuscito con code-behind</span><span class="sxs-lookup"><span data-stu-id="a8220-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="a8220-120">Eseguire il debug di un processo non riuscito con assembly</span><span class="sxs-lookup"><span data-stu-id="a8220-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="a8220-121">Debug di un processo con errori con code-behind</span><span class="sxs-lookup"><span data-stu-id="a8220-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="a8220-122">Se un processo U-SQL non riesce e include il codice utente, in genere denominato `Script.usql.cs` in un progetto U-SQL, il codice sorgente viene importato nella soluzione di debug.</span><span class="sxs-lookup"><span data-stu-id="a8220-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="a8220-123">Da qui è possibile usare gli strumenti di debug di Visual Studio, come espressioni di controllo, variabili e così via, per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a8220-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="a8220-124">Prima del debug, assicurarsi di selezionare le **Common Language Runtime Exceptions** (Eccezioni di Common Language Runtime) nella finestra Impostazioni eccezioni (**CTRL + ALT + E**).</span><span class="sxs-lookup"><span data-stu-id="a8220-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Impostazione visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="a8220-126">Premere **F5** per eseguire il codice code-behind,</span><span class="sxs-lookup"><span data-stu-id="a8220-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="a8220-127">che verrà eseguito fino a quando non viene interrotto da un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="a8220-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="a8220-128">Aprire il file `ADLTool_Codebehind.usql.cs` e impostare i punti di interruzione, quindi premere **F5** per eseguire nel dettaglio il debug del codice.</span><span class="sxs-lookup"><span data-stu-id="a8220-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Eccezione di debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="a8220-130">Debug di un processo con errori con assembly</span><span class="sxs-lookup"><span data-stu-id="a8220-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="a8220-131">Se si usano gli assembly registrati nello script U-SQL, il sistema non riesce a recuperare automaticamente il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="a8220-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="a8220-132">In questo caso, aggiungere manualmente il file di codice sorgente degli assembly alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="a8220-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="a8220-133">Configurare la soluzione</span><span class="sxs-lookup"><span data-stu-id="a8220-133">Configure the solution</span></span>

1. <span data-ttu-id="a8220-134">Fare clic con il pulsante destro del mouse su **Solution 'VertexDebug' (Soluzione "VertexDebug") > Aggiungi > Progetto esistente...** per individuare il codice sorgente degli assembly e aggiungere il progetto alla soluzione di debug.</span><span class="sxs-lookup"><span data-stu-id="a8220-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL debug add project](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="a8220-136">Fare clic con il pulsante destro del mouse su **LocalVertexHost > Proprietà** nella soluzione, quindi copiare il percorso **Directory di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="a8220-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="a8220-137">Fare clic con il pulsante destro del mouse sul **progetto con codice sorgente assembly > Proprietà**, selezionare la scheda **Genera** a sinistra e incollare il percorso copiato in **Output > Percorso output**.</span><span class="sxs-lookup"><span data-stu-id="a8220-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Percorso pdb impostato per il debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="a8220-139">Premere **CTRL + ALT + E**, controllare le **eccezioni di Common Language Runtime** nella finestra Impostazioni eccezioni.</span><span class="sxs-lookup"><span data-stu-id="a8220-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="a8220-140">Avviare il debug</span><span class="sxs-lookup"><span data-stu-id="a8220-140">Start debug</span></span>

1. <span data-ttu-id="a8220-141">Fare clic con il tasto destro del mouse sul **progetto con codice sorgente assembly > Ricrea** per inviare i file con estensione PDB alla directory di lavoro `LocalVertexHost`.</span><span class="sxs-lookup"><span data-stu-id="a8220-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="a8220-142">Premere **F5**. Il progetto verrà eseguito fino a quando non sarà interrotto da un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="a8220-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="a8220-143">È possibile che venga visualizzato il messaggio di avviso seguente, che è possibile ignorare.</span><span class="sxs-lookup"><span data-stu-id="a8220-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="a8220-144">L'accesso alla schermata di debug può richiedere fino a un minuto.</span><span class="sxs-lookup"><span data-stu-id="a8220-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Avviso visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="a8220-146">Aprire il codice sorgente e impostare i punti di interruzione, quindi premere **F5** per eseguire nel dettaglio il debug del codice.</span><span class="sxs-lookup"><span data-stu-id="a8220-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="a8220-147">È anche possibile usare gli strumenti di debug di Visual Studio, come espressioni di controllo, variabili e così via, per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a8220-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="a8220-148">Ricreare il progetto di codice sorgente assembly dopo ogni modifica al codice per generare i file con estensione PDB aggiornati.</span><span class="sxs-lookup"><span data-stu-id="a8220-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="a8220-149">Dopo il debug, se il progetto viene completato correttamente la finestra di output mostra il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="a8220-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Debug U-SQL in Azure Data Lake Analytics completato correttamente](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="a8220-151">Inviare di nuovo il processo</span><span class="sxs-lookup"><span data-stu-id="a8220-151">Resubmit the job</span></span>

<span data-ttu-id="a8220-152">Dopo aver completato il debug è possibile inviare nuovamente il processo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="a8220-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="a8220-153">Per i processi con soluzioni code-behind, copiare il codice C# nel file di origine code-behind, in genere `Script.usql.cs`.</span><span class="sxs-lookup"><span data-stu-id="a8220-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="a8220-154">Per i processi con gli assembly, registrare gli assembly DLL aggiornati nel database ADLA:</span><span class="sxs-lookup"><span data-stu-id="a8220-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="a8220-155">In Esplora server o Cloud Explorer espandere il nodo **Account ADLA > Database**.</span><span class="sxs-lookup"><span data-stu-id="a8220-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="a8220-156">Fare clic con il pulsante destro del mouse su **Assembly** e registrare i nuovi assembly DLL con il database ADLA: ![assembly di debug U-SQL di Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="a8220-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="a8220-157">Inviare di nuovo il processo.</span><span class="sxs-lookup"><span data-stu-id="a8220-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8220-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8220-158">Next steps</span></span>

- [<span data-ttu-id="a8220-159">Guida di programmabilità di U-SQL</span><span class="sxs-lookup"><span data-stu-id="a8220-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="a8220-160">Sviluppare operatori U-SQL definiti dall'utente per i processi di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a8220-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="a8220-161">Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8220-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
