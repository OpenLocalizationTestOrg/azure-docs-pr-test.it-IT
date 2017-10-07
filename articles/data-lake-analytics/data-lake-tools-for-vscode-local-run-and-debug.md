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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Esecuzione locale e debug locale di U-SQL con Visual Studio Code

## <a name="prerequisites"></a>Prerequisiti
Verificare di che aver seguito i prerequisiti soddisfatti prima di iniziare queste procedure hello:
- Strumenti di Azure Data Lake per Visual Studio Code. Per istruzioni, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- In c# per Visual Studio Code (se si desidera debug locale tooperform U-SQL).

   ![Installare C# in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Hello esecuzione locale U-SQL e le funzionalità di debug supportano attualmente solo gli utenti di Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Configurare un ambiente di esecuzione locale di hello U-SQL

1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: scaricare dipendenza LocalRun** pacchetti hello toodownload.  

   ![Scaricare i pacchetti hello ADL LocalRun dipendenza](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Individuare i pacchetti di dipendenza hello dal percorso hello nella hello **Output** riquadro, quindi installare BuildTools e Win10SDK 10240. Di seguito è fornito un esempio di percorso:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Individuare i pacchetti di dipendenza hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, seguire le istruzioni di procedura guidata hello.   

  ![Installare BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, seguire le istruzioni di creazione guidata hello.  

  ![Installare Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Impostare la variabile di ambiente hello. Set hello **SCOPE_CPP_SDK** variabile di ambiente:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Riavvio del sistema operativo hello toomake assicurarsi che le impostazioni variabile di ambiente hello abbiano effetto.  

   ![Verificare che sia installato variabile di ambiente SCOPE_CPP_SDK hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Avviare il servizio di esecuzione locale di hello e inviare l'account locale tooa di hello processo U-SQL 
Per l'utente prima di hello, si è hello toodownload richiesta ADL: scaricare LocalRun dipendenza dei pacchetti se non sono già installati.
1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: avvio del servizio eseguire locale**.
2. Selezionare **Accept** hello tooaccept condizioni di licenza Software Microsoft per la prima volta hello. 

   ![Accettazione delle condizioni di licenza Software Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. verrà visualizzata la finestra di console cmd Hello. Per gli utenti prima volta, è necessario tooenter **3**, quindi individuare il percorso di cartella locale hello per i dati di input e output. Per altre opzioni, è possibile utilizzare i valori predefiniti di hello. 

   ![Console dei comandi per esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza, immettere **ADL: processo di invio**, quindi selezionare **locale** account locale tooyour toosubmit hello processo.

   ![Selezionare Local (Locale) in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Dopo aver inviato il processo di hello, è possibile visualizzare i dettagli di invio hello. Selezionare i dettagli di invio hello tooview **jobUrl** in hello **Output** finestra. È anche possibile visualizzare lo stato hello invio del processo dalla console di hello cmd. Immettere **7** nella console cmd hello se si desidera tooknow più dettagli del processo.

   ![Output dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Stato comandi dell'esecuzione locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Avviare un debug locale per il processo di hello U-SQL  
Per l'utente prima di hello, si è hello toodownload richiesta ADL: scaricare LocalRun dipendenza dei pacchetti se non sono già installati.
  
1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza e quindi immettere **ADL: avvio del servizio eseguire locale**. verrà visualizzata la finestra di console cmd Hello. Verificare che tale hello **DataRoot** è impostata.
3. Impostare un punto di interruzione nel code-behind C#.
4. In editor di script hello, selezionare Ctrl + MAIUSC + P tooopen hello comando console e quindi immettere **Debug locale** toostart il servizio di debug locale.

![Risultati debug locale di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Passaggi successivi
- Per informazioni sull'uso di Strumenti Azure Data Lake per Visual Studio Code, vedere [Usare Strumenti Azure Data Lake per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Per informazioni di hello sullo sviluppo di assembly, vedere [assembly sviluppare U-SQL per i processi di Azure Data Lake Analitica](data-lake-analytics-u-sql-develop-assemblies.md).
