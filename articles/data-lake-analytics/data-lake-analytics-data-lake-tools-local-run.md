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
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Test e il debug di processi U-SQL utilizzando locale eseguire e hello SDK Azure Data Lake U-SQL

È possibile utilizzare Azure Data Lake Tools per Visual Studio e i processi di hello Azure Data Lake U-SQL SDK toorun U-SQL nella workstation, come nel servizio Azure Data Lake hello. Queste due funzionalità eseguite localmente permettono di risparmiare tempo per le operazioni di test e debug dei processi di U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Comprendere cartella dati radice hello e percorso del file hello

Esecuzione locale sia hello SDK U-SQL richiedono una cartella radice di dati. cartella dati radice Hello è "archivio locale" per l'account di calcolo locale hello. Account archivio Azure Data Lake toohello equivalente di un account Data Lake Analitica è. Cartella radice di dati diverso cambio tooa è analoga a commutazione tooa archivio diverso account. Se si desidera tooaccess comunemente condiviso dati con le cartelle radice di dati diverso, è necessario utilizzare i percorsi assoluti negli script. In alternativa, creare collegamenti simbolici di file system (ad esempio, **mklink** in NTFS) in hello dati radice cartella toopoint toohello di dati condivisi.

cartella dati radice Hello viene utilizzato per:

- Archiviare i metadati, inclusi database, tabelle, funzione con valori di tabella e assembly.
- Cercare hello di input e i percorsi di output che sono definiti come percorsi relativi nel U-SQL. Utilizzando i percorsi relativi rende più semplice toodeploy il tooAzure progetti U-SQL.

Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale. percorso relativo di Hello è toohello relativo percorso della cartella radice di dati specificato. È consigliabile che si utilizza "/" come script compatibili con lato server hello hello toomake separatore di percorso. Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti. In questi esempi, C:\LocalRunDataRoot è cartella dati radice hello.

|Percorso relativo|Percorso assoluto|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Usare l'esecuzione locale per Visual Studio

Gli Strumenti di Data Lake per Visual Studio offrono un'esperienza di esecuzione locale di U-SQL in Visual Studio. Questa funzionalità permette di:

- Eseguire uno script U-SQL in locale, insieme agli assembly C#.
- Eseguire il debug di un assembly C# localmente.
- Creare, visualizzare ed eliminare i cataloghi di U-SQL (database locali, assembly, schemi e tabelle) da Esplora server. È inoltre possibile trovare catalogo locale hello anche da Esplora Server.

    ![Catalogo locale dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

programma di installazione del Data Lake Tools Hello crea un toobe cartella C:\LocalRunRoot utilizzata come cartella radice dati predefinita di hello. il parallelismo di esecuzione locale di Hello predefinito è 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure locale eseguito in Visual Studio

1. Aprire Visual Studio.
2. Aprire **Esplora server**.
3. Espandere **Azure** > **Data Lake Analytics**.
4. Fare clic su hello **Data Lake** menu e quindi fare clic su **opzioni e impostazioni**.
5. Nell'albero a sinistra hello espandere **Azure Data Lake**, quindi espandere **generale**.

    ![Impostazioni di configurazione dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Per poter eseguire la funzionalità di esecuzione locale è richiesto un progetto U-SQL di Visual Studio. Questa parte è diversa rispetto all'esecuzione di script U-SQL da Azure.

### <a name="toorun-a-u-sql-script-locally"></a>script U-SQL toorun localmente
1. Aprire il progetto U-SQL in Visual Studio.   
2. In Esplora soluzioni fare clic con il pulsante destro del mouse su uno script U-SQL e selezionare **Invia script**.
3. Selezionare **(Local)** hello Analitica account RunAs toorun lo script in locale.
È anche possibile fare clic su hello **(Local)** account nella parte superiore di hello della finestra di script e quindi fare clic su **Invia** (o utilizzare hello Ctrl + tasto di scelta rapida di F5).

    ![Processi di invio dell'esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Eseguire il debug degli script e delle assembly C# in locale

È possibile eseguire il debug di assembly c# senza l'invio e la relativa registrazione tooAzure Data Lake Analitica Service. È possibile impostare i punti di interruzione in entrambi hello file code-behind e in un progetto c# a cui fa riferimento.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug codice locale nel file code-behind

1. Impostare i punti di interruzione nel codice hello file code-behind.
2. Premere F5 toodebug hello script in locale.

> [!NOTE]
   > Hello seguente procedura funziona solo in Visual Studio 2015. In Visual Studio precedente potrebbe essere necessario toomanually aggiungere i file pdb hello.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug codice locale in un progetto di cui viene fatto riferimento in c#

1. Creare un progetto c# Assembly e compilarlo toogenerate hello dll di output.
2. Registrare dll hello utilizzando un'istruzione U-SQL:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Impostare i punti di interruzione nel codice c# di hello.
4. Premere F5 script di hello toodebug con riferimento a dll c# hello in locale.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Utilizzo locale esecuzione da hello SDK Data Lake U-SQL

Inoltre toorunning U-SQL script localmente utilizzando Visual Studio, è possibile utilizzare gli script U-SQL di hello Azure Data Lake U-SQL SDK toorun localmente con le interfacce della riga di comando e di programmazione. In questo modo è possibile scalare il test locale di U-SQL.

Sono disponibili altre informazioni sull'[SDK U-SQL di Azure Data Lake](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Passaggi successivi

* toosee una query più complessa, vedere [analizzare i log di sito Web usando Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).
* vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data Lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md).
* visualizzazione di esecuzione vertice hello toouse, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
