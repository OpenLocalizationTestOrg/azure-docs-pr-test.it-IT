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
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Eseguire il debug del codice C# definito dall'utente per i processi U-SQL non riusciti

U-SQL fornisce un modello di estendibilità Usa c#, pertanto è possibile scrivere la funzionalità di tooadd di codice, ad esempio un estrazione personalizzato o del reducer. vedere, più toolearn [Guida programmabilità U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). In pratica un codice per cui potrebbe essere necessario il debug e i sistemi di dati di grandi dimensioni possono offrire solo informazioni sul debug del runtime quali i file di log.

Azure Data Lake Tools per Visual Studio fornisce una funzionalità denominata **non è stato possibile eseguire il Debug del vertice**, che consente di duplicare un processo non riuscito dal computer locale hello cloud tooyour per il debug. clone locale Hello acquisisce l'ambiente cloud intera hello, inclusi eventuali dati di input e il codice utente.

Hello video seguente viene illustrato non è stato possibile vertice eseguire il Debug in Azure Data Lake Tools per Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio richiede hello seguenti due aggiornamenti, se non sono già installati: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Universal C Runtime per Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Macchina toolocal vertice di download non riuscito

Quando si apre un processo non riuscito in Azure Data Lake Tools per Visual Studio, verrà visualizzata una barra di avviso gialla con messaggi di errore dettagliato nella scheda errore hello.

1. Fare clic su **scaricare** toodownload tutti hello necessarie risorse e i flussi di input. Se non viene completato il download di hello, fare clic su **ripetere**.

2. Fare clic su **aprire** dopo il completamento di download di hello toogenerate un ambiente di debug locale. Viene creata e aperta automaticamente una nuova istanza di Visual Studio con una soluzione di debug.

![Vertice download visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

I processi possono includere i file di origine code-behind o assembly registrati e questi due tipi presentano diversi scenari di debug.

- [Eseguire il debug di un processo non riuscito con code-behind](#debug-job-failed-with-code-behind)
- [Eseguire il debug di un processo non riuscito con assembly](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Debug di un processo con errori con code-behind

Se un processo U-SQL non riesce e il processo di hello include il codice utente (in genere denominato `Script.usql.cs` in un progetto U-SQL), che il codice sorgente viene importato in hello il debug delle soluzioni.  Da qui è possibile utilizzare hello Visual Studio debug strumenti (espressioni di controllo, variabili e così via) tootroubleshoot hello problema.

> [!NOTE]
> Prima di debug, è che toocheck **eccezioni Common Language Runtime** nella finestra Impostazioni eccezioni hello (**Ctrl + Alt + E**).

![Impostazione visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Premere **F5** toorun hello codice il codice sottostante. che verrà eseguito fino a quando non viene interrotto da un'eccezione.

2. Aprire hello `ADLTool_Codebehind.usql.cs` file e impostare i punti di interruzione, quindi premere **F5** codice hello toodebug dettagliate.

    ![Eccezione di debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Debug di un processo con errori con assembly

Se si utilizzano gli assembly registrati in script U-SQL, sistema hello Impossibile ottenere il codice sorgente hello automaticamente. In questo caso, è possibile aggiungere manualmente la soluzione toohello degli assembly hello origine codice file.

### <a name="configure-hello-solution"></a>Configurare la soluzione hello

1. Fare doppio clic su **soluzione 'VertexDebug' > aggiungere > progetto esistente...**  toofind hello codice sorgente degli assembly e aggiungere toohello progetto hello il debug delle soluzioni.

    ![Azure Data Lake Analytics U-SQL debug add project](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Fare doppio clic su **LocalVertexHost > proprietà** in hello di soluzione e copia hello **la Directory di lavoro** percorso.

3. Fare doppio clic su **progetto del codice sorgente assembly > proprietà**selezionare hello **compilare** scheda a sinistra e incollare il percorso di hello copiato come **Output > percorso di Output**.

    ![Percorso pdb impostato per il debug U-SQL in Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Premere **CTRL + ALT + E**, controllare le **eccezioni di Common Language Runtime** nella finestra Impostazioni eccezioni.

### <a name="start-debug"></a>Avviare il debug

1. Fare doppio clic su **progetto del codice sorgente assembly > ricompilare** toohello i file con estensione pdb toooutput `LocalVertexHost` directory di lavoro.

2. Premere **F5** e hello progetto verrà eseguito fino a quando non è stato arrestato da un'eccezione. Si può vedere hello seguente messaggio di avviso, è possibile ignorare. Può richiedere tooa tooget minuti toohello debug schermata verso l'alto.

    ![Avviso visual studio debug U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Aprire il codice sorgente e impostare i punti di interruzione, quindi premere **F5** codice hello toodebug dettagliate.

È inoltre possibile utilizzare hello Visual Studio debug strumenti (espressioni di controllo, variabili e così via) tootroubleshoot hello problema.

> [!NOTE]
> Ricompilare progetto del codice sorgente hello assembly ogni volta dopo aver modificato i file con estensione pdb toogenerate aggiornati di codice hello.

Dopo il debug, se il progetto hello viene completata correttamente finestra di output di hello Visualizza hello seguente messaggio:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Debug U-SQL in Azure Data Lake Analytics completato correttamente](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Inviare di nuovo il processo di hello

Dopo aver completato il debug, eseguire nuovamente il processo non riuscito di hello.

1. Per i processi con soluzioni di codice, copiare il codice c# in file di origine code-behind hello (in genere `Script.usql.cs`).
2. Per i processi con gli assembly, registrare l'assembly DLL hello aggiornato nel database ADLA:
    1. In Esplora Server o Cloud Explorer espandere hello **account ADLA > database** nodo.
    2. Fare doppio clic su **assembly** e registrare il nuovo assembly DLL con database ADLA hello: ![debug U-SQL di Azure Data Lake Analitica registrare assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Inviare di nuovo il processo.

## <a name="next-steps"></a>Passaggi successivi

- [Guida di programmabilità di U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Sviluppare operatori U-SQL definiti dall'utente per i processi di Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
