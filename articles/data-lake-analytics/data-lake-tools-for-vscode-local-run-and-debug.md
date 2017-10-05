---
title: Strumenti Azure Data Lake per Visual Studio - Esecuzione locale e debug locale di U-SQL con Visual Studio Code | Microsoft Docs
description: Informazioni su come usare Strumenti Azure Data Lake per Visual Studio Code per l'esecuzione locale e il debug locale.
Keywords: VScode, Strumenti Azure Data Lake, Esecuzione locale, debug locale, Debug Locale, anteprima file di archiviazione, caricamento nel percorso di archiviazione
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="1be16-104">Esecuzione locale e debug locale di U-SQL con Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1be16-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be16-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1be16-105">Prerequisites</span></span>
<span data-ttu-id="1be16-106">Prima di iniziare queste procedure, verificare che i prerequisiti seguenti siano disponibili:</span><span class="sxs-lookup"><span data-stu-id="1be16-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="1be16-107">Strumenti di Azure Data Lake per Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1be16-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="1be16-108">Per istruzioni, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="1be16-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="1be16-109">C# per Visual Studio Code (per eseguire il debug locale di U-SQL).</span><span class="sxs-lookup"><span data-stu-id="1be16-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Installare C# in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="1be16-111">Attualmente le funzionalità di esecuzione locale e debug locale di U-SQL supportano solo gli utenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="1be16-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="1be16-112">Configurare un ambiente di esecuzione locale di U-SQL</span><span class="sxs-lookup"><span data-stu-id="1be16-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="1be16-113">Premere CTRL+MAIUSC+P per aprire il riquadro comandi, quindi digitare **ADL: Download LocalRun Dependency** (ADL: scarica dipendenza esecuzione locale) per scaricare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1be16-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![Scaricare i pacchetti di dipendenza ADL LocalRun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="1be16-115">Trovare i pacchetti di dipendenza nel percorso visualizzato nel pannello **Output**, quindi installare BuildTools e Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="1be16-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="1be16-116">Di seguito è fornito un esempio di percorso:</span><span class="sxs-lookup"><span data-stu-id="1be16-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="1be16-117">![Individuare i pacchetti di dipendenza](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="1be16-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="1be16-118">a.</span><span class="sxs-lookup"><span data-stu-id="1be16-118">a.</span></span> <span data-ttu-id="1be16-119">Per installare BuildTools, seguire le istruzioni della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="1be16-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![Installare BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="1be16-121">b.</span><span class="sxs-lookup"><span data-stu-id="1be16-121">b.</span></span> <span data-ttu-id="1be16-122">Per installare Win10SDK 10240, seguire le istruzioni della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="1be16-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Installare Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="1be16-124">Configurare la variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="1be16-124">Set up the environment variable.</span></span> <span data-ttu-id="1be16-125">Impostare la variabile di ambiente **SCOPE_CPP_SDK** per:</span><span class="sxs-lookup"><span data-stu-id="1be16-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="1be16-126">Riavviare il sistema operativo per assicurarsi che le impostazioni della variabile di ambiente abbiano effetto.</span><span class="sxs-lookup"><span data-stu-id="1be16-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![Assicurarsi che la variabile di ambiente SCOPE_CPP_SDK sia installata](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="1be16-128">Avviare il servizio di esecuzione locale e inviare il processo U-SQL a un account locale</span><span class="sxs-lookup"><span data-stu-id="1be16-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="1be16-129">Al primo utilizzo viene chiesto di scaricare i pacchetti di dipendenza LocalRun se non sono già installati.</span><span class="sxs-lookup"><span data-stu-id="1be16-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="1be16-130">Premere CTRL+MAIUSC+P per aprire il riquadro comandi e immettere **ADL: Start Local Run Service** (ADL: avvia servizio di esecuzione locale).</span><span class="sxs-lookup"><span data-stu-id="1be16-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="1be16-131">Selezionare **Accetto** per accettare le condizioni di licenza software Microsoft per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="1be16-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Accettare le condizioni di licenza software Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="1be16-133">Viene aperta la console dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1be16-133">The cmd console opens.</span></span> <span data-ttu-id="1be16-134">Dato che si accede per la prima volta immettere **3** e quindi individuare il percorso di cartella locale per l'input e l'output di dati.</span><span class="sxs-lookup"><span data-stu-id="1be16-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="1be16-135">Per le altre opzioni è possibile usare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="1be16-135">For other options, you can use the default values.</span></span> 

   ![Console dei comandi per esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="1be16-137">Premere CTRL+MAIUSC+P per aprire il riquadro comandi, immettere **ADL: Submit Job** (ADL: Invia processo), quindi selezionare **Local** (Locale) per inviare il processo all'account locale.</span><span class="sxs-lookup"><span data-stu-id="1be16-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Selezionare Local (Locale) in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="1be16-139">Dopo aver inviato il processo è possibile visualizzare i dettagli di invio.</span><span class="sxs-lookup"><span data-stu-id="1be16-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="1be16-140">Per visualizzare i dettagli di invio selezionare **jobUrl** nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="1be16-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="1be16-141">È possibile visualizzare lo stato di invio del processo anche dalla console dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1be16-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="1be16-142">Immettere **7** nella console dei comandi se si desidera conoscere ulteriori dettagli del processo.</span><span class="sxs-lookup"><span data-stu-id="1be16-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="1be16-143">![Output dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Stato comandi dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="1be16-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="1be16-144">Avviare il debug locale per il processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="1be16-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="1be16-145">Al primo utilizzo viene chiesto di scaricare i pacchetti di dipendenza LocalRun se non sono già installati.</span><span class="sxs-lookup"><span data-stu-id="1be16-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="1be16-146">Premere CTRL+MAIUSC+P per aprire il riquadro comandi e immettere **ADL: Start Local Run Service** (ADL: avvia servizio di esecuzione locale).</span><span class="sxs-lookup"><span data-stu-id="1be16-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="1be16-147">Viene aperta la console dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1be16-147">The cmd console opens.</span></span> <span data-ttu-id="1be16-148">Assicurarsi che **DataRoot** sia impostata.</span><span class="sxs-lookup"><span data-stu-id="1be16-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="1be16-149">Impostare un punto di interruzione nel code-behind C#.</span><span class="sxs-lookup"><span data-stu-id="1be16-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="1be16-150">Tornare all'editor di script, premere CTRL+MAIUSC+P per aprire il riquadro comandi e immettere **Local Debug** (Debug locale) per avviare il servizio di debug locale.</span><span class="sxs-lookup"><span data-stu-id="1be16-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Risultati debug locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="1be16-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1be16-152">Next steps</span></span>
- <span data-ttu-id="1be16-153">Per informazioni sull'uso di Strumenti Azure Data Lake per Visual Studio Code, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="1be16-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="1be16-154">Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1be16-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="1be16-155">Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1be16-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="1be16-156">Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="1be16-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
