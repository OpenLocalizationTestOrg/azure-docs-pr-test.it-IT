---
title: gli strumenti Analitica di flusso di Azure per Visual Studio aaaUse | Documenti Microsoft
description: Guida introduttiva di esercitazione per hello Azure flusso Analitica Tools per Visual Studio
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Usare gli strumenti di Analisi di flusso di Azure per Visual Studio
## <a name="introduction"></a>Introduzione
In questa esercitazione, è illustrato come toouse strumenti Analitica flusso di Azure per Visual Studio toocreate, creare, testare localmente, gestire e debug di processi di flusso Analitica. 

Dopo aver completato questa esercitazione, si sarà in grado di:
* Usare gli strumenti di Analisi di flusso di Azure per Visual Studio.
* Configurare e distribuire un processo di Analisi di flusso.
* Testare il processo in locale con dati di esempio locali.
* Utilizzare Monitoraggio tootroubleshoot problemi.
* Esportare tooprojects processi esistenti.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:
* Completare i passaggi di hello che precedono "Creazione di un processo di flusso Analitica" in hello [compilare una soluzione IoT utilizzando esercitazione Analitica flusso](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Usare Visual Studio 2015, Visual Studio 2013 Update 4 oppure Visual Studio 2012. Sono supportate le edizioni Enterprise (Ultimate/Premium), Professional e Community. L'edizione Express non è supportata. Visual Studio 2017 non è supportato. 
* Hello utilizzare Azure SDK per .NET versione 2.7.1 o versione successiva. Installarlo utilizzando hello [installazione guidata piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Installare hello [flusso Analitica Tools per Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Creare un progetto di Analisi di flusso
1. In Visual Studio, fare clic su hello **File** dal menu **nuovo progetto**. 

2. Nell'elenco di modelli hello hello sinistra, selezionare **Analitica flusso** e quindi fare clic su **l'applicazione Azure flusso Analitica**.

3. Immettere hello **nome**, **percorso**, e **Nome soluzione** come avviene per altri progetti.

    ![Finestra Nuovo progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Verrà generato un progetto **Toll** in **Esplora soluzioni**.

    ![Progetto Toll generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Scegliere la sottoscrizione corretta hello
1. In Visual Studio, fare clic su hello **vista** menu e aprire **Esplora Server**.

2. Accedere con l'account Azure. 

## <a name="define-hello-input-sources"></a>Definire le origini di input hello
1.  In **Esplora**, espandere hello **input** nodo e rinominare **Input.json** troppo**EntryStream.json**. Fare doppio clic su **EntryStream.json**.
2.  Hello **Alias di Input** è ora **EntryStream**. alias di input Hello utilizzato nello script di query hello. 
3.  In **Tipo di origine** selezionare **Flusso dati**.
4.  In **Origine** selezionare **Hub eventi**.
5.  In **Service Bus Namespace**selezionare hello **TollData** opzione.
6.  In **Nome hub eventi** selezionare **voce**.
7.  In **nome criterio Hub eventi**selezionare **RootManageSharedAccessKey** (valore predefinito di hello).
8.  In **Formato di serializzazione eventi** selezionare **Json**. 
9.  In **Codifica** selezionare **UTF-8**. Le impostazioni dovrebbero essere simile hello seguente schermata:

    ![Finestra di input](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. procedura guidata hello toofinish, fare clic su **salvare**. È ora possibile aggiungere un altro flusso di uscita hello di toocreate origine di input. Pulsante destro del mouse hello **input** nodo e selezionare **nuovo elemento**.

    ![Nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Nella finestra hello selezionare **Input Analitica del flusso di Azure**e modificare hello **nome** troppo**ExitStream.json**. Fare clic su **Aggiungi**.

    ![Finestra Aggiungi nuovo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Fare doppio clic su **ExitStream.json** nel progetto hello e seguire hello stessi passaggi per il flusso di voce hello. Tooenter assicurarsi di essere **uscire** per hello **nome Hub eventi** come illustrato nella seguente schermata hello:

    ![Finestra ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    A questo punto sono presenti due flussi di input definiti:

    ![Flussi di input di entrata e di uscita](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Successivamente, aggiungere l'input di dati di riferimento per i file blob hello che contiene dati di registrazione dell'automobile.

13. Pulsante destro del mouse hello **input** nodo nel progetto hello e quindi seguire hello stessi passaggi anche per gli input flusso hello. In **Alias di input** immettere **Registrazione** e in **Tipo di origine** selezionare **Dati di riferimento**.

    ![Finestra Registrazione](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. In **Account di archiviazione**selezionare hello **tolldata** opzione. In **Contenitore** selezionare **tolldata** e in **Modello percorso** immettere **registration.json**. Il nome file fa distinzione tra maiuscole e minuscole e deve contenere solo lettere minuscole.
15. procedura guidata hello toofinish, fare clic su **salvare**.

Ora sono definiti tutti gli input hello.

## <a name="define-hello-output"></a>Definire l'output di hello
1.  In **Esplora**, espandere hello **input** nodo e fare doppio clic su **Output.json**.

2.  In **Alias di output** immettere **output**. 
3.  In **Sink** selezionare **Database SQL**.
4.  In **Database** selezionare **TollDataDB**.
5.  In **Nome utente** immettere **tolladmin**. 
6.  In **Password** immettere **123toll!**.
7.  In **Tabella** immettere **TollDataRefJoin**.
8.  Fare clic su **Salva**.

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Creare una query di Analisi di flusso
In questa esercitazione tenta tooanswer diverse domande aziendali tootoll correlate a dati. Viene inoltre costruito query Analitica di flusso che può essere usata nelle risposte di flusso Analitica tooprovide pertinente.
Prima di iniziare il primo processo di flusso Analitica, analizziamo una semplice sintassi di query di scenario e hello.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Introduzione toohello linguaggio di query Analitica di flusso
Si supponga che è necessario numero hello toocount dei veicoli che immette un casello. Poiché in questo esempio è un flusso continuo di eventi, occorre toodefine un periodo di tempo. Modificare toobe domanda hello "quanti veicoli immettere un casello ogni tre minuti?" Toocount in questo modo sono in genere di dati di cui tooas hello a cascata conteggio.

Esaminare query flusso Analitica hello che risponda a questa domanda:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Flusso Analitica Usa un linguaggio di query che è simile a SQL e aggiunge alcune estensioni toospecify ora aspetti delle query hello.

Per ulteriori informazioni, vedere [gestione del tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) costrutti utilizzati nella query hello da MSDN.

Ora che è stato scritto della prima query Analitica di flusso, è ora tootest è. Utilizzare i file di dati di esempio hello si trova nella cartella TollApp nel seguente percorso hello:

..\TollApp\TollApp\Data

Questa cartella contiene i seguenti file hello:
*   Entry.json
*   Exit.json
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Numero di hello dei veicoli immettendo un casello
Nel progetto hello, fare doppio clic su **Script.asaql** tooopen script hello hello **Editor di Query**. Copiare e incollare script hello nella sezione precedente hello in editor hello. Hello Editor di Query supporta IntelliSense, colorazione della sintassi e indicatore di errore hello.

![Editor di query](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Eseguire test locali delle query di Analisi di flusso

1. toocompile hello query toosee se si verifica un errore di sintassi, fare clic sul progetto hello e selezionare **compilare**. 

2. toovalidate questa query nei dati di esempio, è possibile utilizzare i dati di esempio locale. Input hello e scegliere **aggiungere input locale**.

    ![Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Nella finestra popup hello, selezionare i dati di esempio hello dal percorso locale. Fare clic su **Salva**.

    ![Finestra Add local input (Aggiungi input locale)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Un file denominato **local_EntryStream.json** viene aggiunto automaticamente tooyour cartella di input.

    ![Cartella tooinputs aggiunta di file](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. In hello **Editor di Query**, fare clic su **eseguire localmente**. Oppure è possibile premere F5 di hello.

    ![Esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Output esecuzione locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Premere alcun output di hello tooview chiave in hello **il risultato di esecuzione locale** finestra in Visual Studio. 

    ![Finestra Risultato esecuzione locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Fare clic su **Apri cartella risultato** dei file di output di hello toocheck entrambi in formato CSV e JSON.

    ![Output di Apri cartella risultati](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Dati di input di esempio hello
È inoltre possibile dati di input di esempio di file locale tooa di origini di input. 
1. Fare clic sul file di configurazione di input hello e selezionare **dati di esempio**. 

   ![Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    È possibile campionare solo l'hub eventi o l'hub IoT per ora. Non sono supportate altre origini di input.

2. Nella finestra popup hello immettere dati di esempio hello toosave hello percorso locale utilizzato. Fare clic su **Esempio**.

    ![Finestra Dati di esempio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    È possibile visualizzare lo stato di avanzamento hello in hello **Output** finestra. 

    ![Finestra Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Inviare un tooAzure query Analitica di flusso
1. In hello **Editor di Query**, fare clic su **inviare tooAzure** nell'editor di script hello.

    ![Inviare tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Selezionare **Creare un nuovo processo di analisi di flusso di Azure**. Immettere hello **nome del processo**e seleziona hello corretto **sottoscrizione**. Fare clic su **Submit**.

    ![Finestra di invio del processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Avviare un processo
Dopo aver creato il processo, visualizzazione dei processi hello viene aperto automaticamente. 
1. hello toostart di processo, fare clic su hello **freccia verde** pulsante.

    ![Avviare un processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Selezionare l'impostazione predefinita hello e fare clic su **avviare**.
 
    ![Finestra Avvia processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    processo Hello **stato** cambia troppo**esecuzione**, e **gli eventi di Input** e **gli eventi di Output** vengono visualizzati.

    ![Stato In esecuzione in Riepilogo processo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Controllare i risultati di hello in Visual Studio
1. In Visual Studio, aprire **Esplora Server** rapida hello e **TollDataRefJoin** tabella.
2. Selezionare **Mostra dati tabella** toosee output di hello del processo.
   
    ![Selezione di Mostra dati tabella in Esplora server](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Visualizzazione hello processo metriche
È possibile trovare alcune statistiche di base sul processo in **Job Metrics** (Metriche di processo). 

![Finestra Job Metrics (Metriche di processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Processo di hello elenco in Esplora Server
In **Esplora server** fare clic su **Processi di Analisi di flusso** e quindi fare clic su **Aggiorna**. processo Hello viene visualizzata sotto **i processi di flusso Analitica**.

![Processi di Analisi di flusso elencati in Esplora server](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Visualizzazione processo hello aperto
visualizzazione dei processi tooopen hello, espandere il nodo del processo e fare doppio clic su hello **Visualizza processo** nodo.

![Nodo Job View (Visualizzazione processo)](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Esportare un progetto di tooa processo esistente
Esistono due modi, è possibile esportare un progetto di tooa processo esistente.

In **Esplora Server**, rapida del nodo del processo hello in hello **i processi di flusso Analitica** nodo e selezionare **esportare tooNew flusso Analitica progetto**.

![Esportazione tooNew flusso Analitica progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

progetto Hello viene generato in **Esplora**.

![Progetto generato in Esplora soluzioni](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
È inoltre possibile utilizzare la visualizzazione processi hello e fare clic su **generare progetto**.

![Genera progetto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Problemi noti e limitazioni
 
- Non è disponibile alcun supporto per l'output di Power BI e dell'archivio Azure Data Lake.
- Non è disponibile alcun supporto dell'editor per l'aggiunta o la modifica di funzioni JavaScript definite dall'utente.

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi di flusso di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
