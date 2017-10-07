---
title: script di aaaDevelop U-SQL utilizzando Data Lake Tools per Visual Studio | Documenti Microsoft
description: Informazioni su come tooinstall Data Lake di strumenti per Visual Studio e come toodevelop e testare script U-SQL.
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
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Sviluppare script U-SQL tramite Strumenti Data Lake per Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Informazioni su come account di Azure Data Lake Analitica toocreate Visual Studio toouse, definire i processi in [U-SQL](data-lake-analytics-u-sql-get-started.md)e l'invio del servizio Data Lake Analitica toohello di processi. Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Prerequisiti

* **Visual Studio**: sono supportate tutte le versioni ad eccezione della versione Express.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Microsoft Azure SDK per .NET** versione 2.7.1 o successiva.  Installarlo utilizzando hello [installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Un account **Data Lake Analytics**. toocreate un account, vedere [Guida introduttiva di Azure Data Lake Analitica tramite il portale di Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Installare Strumenti Azure Data Lake per Visual Studio 

Scaricare e installare Azure Data Lake Tools per Visual Studio [dall'area Download hello](http://aka.ms/adltoolsvs). Dopo l'installazione si noti che:
* Hello **Esplora Server** > **Azure** nodo contiene un **Data Lake Analitica** nodo. 
* Hello **strumenti** menu è un **Data Lake** elemento.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Connettere l'account di Azure Data Lake Analitica tooan

1. Aprire Visual Studio.
2. Aprire Esplora server selezionando **Visualizza** > **Esplora Server**.
3. Fare clic con il pulsante destro del mouse su **Azure**. Selezionare quindi **tooMicrosoft sottoscrizione di Azure connettersi** e seguire le istruzioni di hello.
4. In Esplora server selezionare **Azure** > **Data Lake Analytics**. Verrà visualizzato un elenco degli account Data Lake Analytics.


## <a name="write-your-first-u-sql-script"></a>Scrivere il primo script U-SQL

Dopo il testo Hello è un semplice script U-SQL. Definisce un set di dati di piccole dimensioni e le scritture archivio dataset toohello predefinito Data Lake come un file denominato `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>Inviare un processo di Data Lake Analytics

1. Selezionare **File** > **Nuovo** > **Progetto**.

2. Seleziona hello **progetto U-SQL** digitare e quindi fare clic su **OK**. Visual Studio crea una soluzione con un file **Script.usql**.

3. Incollare script precedente hello hello **Script.usql** finestra.

4. Nell'angolo superiore sinistro hello di hello **Script.usql** finestra, specificare l'account Data Lake Analitica hello.

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. Nell'angolo superiore sinistro hello di hello **Script.usql** selezionare **Invia**.
6. Verificare hello **Account Analitica**, quindi selezionare **Invia**. Risultati di invio sono disponibili in hello Data Lake Tools per Visual Studio risultati dopo l'invio di hello è stata completata.

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello più recente processo lo stato e aggiornamento schermata ciao, fare clic su **aggiornamento**. Quando il processo di hello ha esito positivo, viene visualizzato hello **grafico processi**, **operazioni sui metadati**, **cronologia dello stato**, e **diagnostica**:

    ![Grafico delle prestazioni del processo di Analisi Data Lake per Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Riepilogo processo** Mostra hello riepilogo del processo di hello.   
   * **I dettagli dei processi** Mostra informazioni più specifiche sul processo di hello, inclusi script hello, risorse e i vertici.
   * **Grafico processi** Visualizza lo stato di avanzamento hello del processo di hello.
   * **Operazioni sui metadati** Mostra tutte le azioni hello che sono state eseguite nel catalogo di hello U-SQL.
   * **Dati** Mostra tutti gli input hello e output.
   * **Diagnostica** fornisce un'analisi avanzata per l'ottimizzazione dell'esecuzione e delle prestazioni del processo.

### <a name="toocheck-job-state"></a>stato del processo toocheck

1. In Esplora server selezionare **Azure** > **Data Lake Analytics**. 
2. Espandere nome dell'account Data Lake Analitica hello.
3. Fare doppio clic su **Processi**.
4. Selezionare il processo hello inviati in precedenza.

### <a name="toosee-hello-output-of-a-job"></a>output di hello toosee di un processo

1. In Esplora Server, passare toohello processo che è stato inviato.
2. Fare clic su hello **dati** scheda.
3. In hello **gli output dei processi** scheda, seleziona hello `"/data.csv"` file.

## <a name="next-steps"></a>Passaggi successivi

* [Eseguire script U-SQL nella workstation per test e debug](data-lake-analytics-data-lake-tools-local-run.md)
* [Debug dei processi U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Utilizzare hello Azure Data Lake Tools per Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
