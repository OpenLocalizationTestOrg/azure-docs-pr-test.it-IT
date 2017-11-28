---
title: Strumenti Azure Data Lake per Visual Studio - Esecuzione locale e debug locale di U-SQL con Visual Studio Code | Microsoft Docs
description: Informazioni su come eseguire il debug toouse Azure Data Lake Tools per Visual Studio Code toolocal locali e di esecuzione.
Keywords: Percorso di toostorage di caricamento di VScode, strumenti di Azure Data Lake, esecuzione, file di archiviazione locale di debug, eseguire il Debug locale, anteprima locale
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
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="4c171-104">Esecuzione locale e debug locale di U-SQL con Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4c171-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c171-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c171-105">Prerequisites</span></span>
<span data-ttu-id="4c171-106">Verificare di che aver seguito i prerequisiti soddisfatti prima di iniziare queste procedure hello:</span><span class="sxs-lookup"><span data-stu-id="4c171-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="4c171-107">Strumenti di Azure Data Lake per Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4c171-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="4c171-108">Per istruzioni, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="4c171-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="4c171-109">In c# per Visual Studio Code (se si desidera debug locale tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="4c171-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Installare C# in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="4c171-111">Hello esecuzione locale U-SQL e le funzionalità di debug supportano attualmente solo gli utenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="4c171-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="4c171-112">Configurare un ambiente di esecuzione locale di hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="4c171-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="4c171-113">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: scaricare dipendenza LocalRun** pacchetti hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="4c171-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Scaricare i pacchetti hello ADL LocalRun dipendenza](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="4c171-115">Individuare i pacchetti di dipendenza hello dal percorso hello nella hello **Output** riquadro, quindi installare BuildTools e Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="4c171-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="4c171-116">Di seguito è fornito un esempio di percorso:</span><span class="sxs-lookup"><span data-stu-id="4c171-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="4c171-117">![Individuare i pacchetti di dipendenza hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="4c171-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="4c171-118">a.</span><span class="sxs-lookup"><span data-stu-id="4c171-118">a.</span></span> <span data-ttu-id="4c171-119">tooinstall BuildTools, seguire le istruzioni di procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Installare BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="4c171-121">b.</span><span class="sxs-lookup"><span data-stu-id="4c171-121">b.</span></span> <span data-ttu-id="4c171-122">tooinstall Win10SDK 10240, seguire le istruzioni di creazione guidata hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Installare Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="4c171-124">Impostare la variabile di ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-124">Set up hello environment variable.</span></span> <span data-ttu-id="4c171-125">Set hello **SCOPE_CPP_SDK** variabile di ambiente:</span><span class="sxs-lookup"><span data-stu-id="4c171-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="4c171-126">Riavvio del sistema operativo hello toomake assicurarsi che le impostazioni variabile di ambiente hello abbiano effetto.</span><span class="sxs-lookup"><span data-stu-id="4c171-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Verificare che sia installato variabile di ambiente SCOPE_CPP_SDK hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="4c171-128">Avviare il servizio di esecuzione locale di hello e inviare l'account locale tooa di hello processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="4c171-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="4c171-129">Per l'utente prima di hello, si è hello toodownload richiesta ADL: scaricare LocalRun dipendenza dei pacchetti se non sono già installati.</span><span class="sxs-lookup"><span data-stu-id="4c171-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="4c171-130">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: avvio del servizio eseguire locale**.</span><span class="sxs-lookup"><span data-stu-id="4c171-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="4c171-131">Selezionare **Accept** hello tooaccept condizioni di licenza Software Microsoft per la prima volta hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Accettazione delle condizioni di licenza Software Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="4c171-133">verrà visualizzata la finestra di console cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-133">hello cmd console opens.</span></span> <span data-ttu-id="4c171-134">Per gli utenti prima volta, è necessario tooenter **3**, quindi individuare il percorso di cartella locale hello per i dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="4c171-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="4c171-135">Per altre opzioni, è possibile utilizzare i valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-135">For other options, you can use hello default values.</span></span> 

   ![Console dei comandi per esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="4c171-137">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza, immettere **ADL: processo di invio**, quindi selezionare **locale** account locale tooyour toosubmit hello processo.</span><span class="sxs-lookup"><span data-stu-id="4c171-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Selezionare Local (Locale) in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="4c171-139">Dopo aver inviato il processo di hello, è possibile visualizzare i dettagli di invio hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="4c171-140">Selezionare i dettagli di invio hello tooview **jobUrl** in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="4c171-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="4c171-141">È anche possibile visualizzare lo stato hello invio del processo dalla console di hello cmd.</span><span class="sxs-lookup"><span data-stu-id="4c171-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="4c171-142">Immettere **7** nella console cmd hello se si desidera tooknow più dettagli del processo.</span><span class="sxs-lookup"><span data-stu-id="4c171-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="4c171-143">![Output dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Stato comandi dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="4c171-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="4c171-144">Avviare un debug locale per il processo di hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="4c171-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="4c171-145">Per l'utente prima di hello, si è hello toodownload richiesta ADL: scaricare LocalRun dipendenza dei pacchetti se non sono già installati.</span><span class="sxs-lookup"><span data-stu-id="4c171-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="4c171-146">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: avvio del servizio eseguire locale**.</span><span class="sxs-lookup"><span data-stu-id="4c171-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="4c171-147">verrà visualizzata la finestra di console cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="4c171-147">hello cmd console opens.</span></span> <span data-ttu-id="4c171-148">Verificare che tale hello **DataRoot** è impostata.</span><span class="sxs-lookup"><span data-stu-id="4c171-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="4c171-149">Impostare un punto di interruzione nel code-behind C#.</span><span class="sxs-lookup"><span data-stu-id="4c171-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="4c171-150">In editor di script hello, selezionare Ctrl + MAIUSC + P tooopen hello comando console e quindi immettere **Debug locale** toostart il servizio di debug locale.</span><span class="sxs-lookup"><span data-stu-id="4c171-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Risultati debug locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="4c171-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c171-152">Next steps</span></span>
- <span data-ttu-id="4c171-153">Per informazioni sull'uso di Strumenti Azure Data Lake per Visual Studio Code, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="4c171-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="4c171-154">Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c171-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="4c171-155">Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4c171-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="4c171-156">Per informazioni di hello sullo sviluppo di assembly, vedere [assembly sviluppare U-SQL per i processi di Azure Data Lake Analitica](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="4c171-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
