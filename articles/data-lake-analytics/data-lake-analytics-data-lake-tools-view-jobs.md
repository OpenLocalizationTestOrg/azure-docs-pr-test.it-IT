---
title: aaaUse processo Browser e visualizzazione dei processi per i processi di Azure Data Lake Analitica | Documenti Microsoft
description: 'Informazioni su come toouse processo Browser e visualizzazione dei processi per i processi di Azure Data Lake Analitica. '
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Usare Job Browser e Job View (Visualizzazione processo) per i processi di Azure Data Lake Analytics
gli archivi di servizio di Azure Data Lake Analitica Hello inviato i processi in un [archivio query](#query-store). In questo articolo viene illustrato come toouse processo Browser e visualizzazione dei processi in Azure Data Lake Tools per hello toofind Visual Studio cronologico processo informazioni. 

Per impostazione predefinita, il servizio Data Lake Analitica hello archivia i processi di hello per 30 giorni. è possibile configurare il periodo di scadenza Hello dal portale di Azure hello configurando i criteri di scadenza hello personalizzato. Non sarà in grado di tooaccess informazioni sul processo di hello dopo la scadenza. 

## <a name="prerequisites"></a>Prerequisiti
Vedere [Prerequisiti di Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Aprire hello processo Browser
Accesso hello processo Browser tramite **Esplora Server > Azure > Data Lake Analitica > processi** in Visual Studio.  Utilizza hello processo Browser, è possibile accedere archivio query hello di un account Data Lake Analitica. Processo Browser Visualizza archivio Query in hello a sinistra, che mostra informazioni sul processo di base e visualizzazione dei processi in cui destra hello dettagliate informazioni sul processo.

## <a name="job-view"></a>Job View (Visualizzazione processo)
Visualizzazione dei processi Mostra hello informazioni dettagliate di un processo. tooopen un processo, è possibile fare doppio clic su un processo in hello processo Browser o aprirla dal menu Data Lake hello facendo clic su Visualizza processo. Verrà visualizzata una finestra di dialogo popolato con URL processo hello.

![Job Browser di Data Lake Tools per Visual Studio](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

La finestra di dialogo Job View (Visualizzazione processo) contiene:

* Riepilogo dei processi
  
    Aggiorna vista processo hello toosee hello informazioni più recenti di processi in esecuzione.
  
  * Stato del processo (grafico):
    
      Lo stato del processo descrive fasi processo hello:
    
      ![Stato delle fasi del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Preparazione: Caricare cloud toohello di script, la compilazione e l'ottimizzazione di script hello mediante il servizio di compilazione hello.
    * In coda: I processi sono in coda presamico sono in attesa di risorse sufficienti o i processi di hello superano massimo processi simultanei di hello al limite di account. impostazione di priorità Hello determina la sequenza hello di processi in coda - hello hello più basso, priorità più alta hello hello.
    * Esecuzione: hello processo effettivamente è in esecuzione nell'account Data Lake Analitica.
    * Completamento: processo hello è completato (ad esempio, finalizzazione del file hello).
      
      processo Hello può avere esito negativo in ogni fase. Ad esempio, errori di compilazione in fase di preparazione hello, errori di timeout nella fase di hello in coda e gli errori di esecuzione in fase di esecuzione hello e così via.
  * Basic Information
    
      informazioni di base processo Hello viene visualizzata nella parte inferiore di hello del Pannello di riepilogo dei processi di hello.
    
      ![Stato delle fasi del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Job Result (Risultato processo): indica l'esito positivo o negativo. processo Hello potrebbe non riuscire in ogni fase.
    * Total Duration (Durata totale): il tempo reale tra l'ora di invio e l'ora di fine.
    * Tempo di calcolo totale: somma hello ogni vertice del tempo di esecuzione, è possibile considerare che come hello ora che il processo di hello viene eseguita in solo un vertice. Fare riferimento tooTotal vertici toofind ulteriori informazioni su vertice.
    * Ora di invio/inizio/fine: tempo hello quando il servizio Data Lake Analitica hello riceve hello toorun di invio/Avvia processo processo/Termina processo hello correttamente o No.
    * In coda/Compilation/esecuzione: Il tempo di clock impiegato durante la fase di hello in coda/preparazione/esecuzione.
    * Account: account Data Lake Analitica hello utilizzato per l'esecuzione processo hello.
    * Autore: utente hello che ha inviato il processo di hello, può essere un reale un account utente o un account di sistema.
    * Priorità: hello priorità processo hello. Hello hello numero inferiore, priorità più alta hello hello. Influisce solo sulla sequenza hello dei processi di hello in coda hello. L'impostazione di una priorità più elevata non ha la precedenza sui processi in esecuzione.
    * Parallelismo: hello richiesto numero massimo di simultanee Azure Data Lake Analitica unità (ADLAUs), noto anche come vertici. Attualmente, un vertice è uguale tooone VM con due core virtuali e 6 GB di RAM, anche se questo è stato possibile aggiornare in futuro Data Lake Analitica degli aggiornamenti.
    * Byte a sinistra: Byte toobe elaborati fino a quando non viene completato il processo di hello.
    * Byte letti/scritti: byte che sono stati letti/scritti dall'inizio dell'esecuzione del processo hello.
    * Totale vertici: processo hello viene suddivisa molti elementi di lavoro, ogni elemento di lavoro viene chiamato un vertice. Questo valore viene descritto come processo di hello quanti elementi di lavoro è costituito. Un vertice può essere considerato come un'unità di processo di base, nota anche come Azure Data Lake Analytics Unit (ADLAU); i vertici possono essere eseguiti in parallelismo. 
    * Completato o in esecuzione o non riuscita: hello numero di vertici completato o in esecuzione o non è riuscita. Vertici possono non riuscire a causa di errori di sistema e codice utente tooboth, ma i tentativi di sistema hello non vertici automaticamente più volte. Se ancora non riuscito dopo avere ritentato un vertice hello, l'intero processo hello avrà esito negativo.
* Grafico del processo
  
    Uno script U-SQL rappresenta la logica di trasformazione dei dati di input toooutput dati hello. script Hello viene compilato e ottimizzato il piano di esecuzione fisica tooa in fase di preparazione hello. Grafico processi è piano di esecuzione fisica tooshow hello.  Hello seguente diagramma illustra il processo di hello:
  
    ![Stato delle fasi del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Un processo è suddiviso in più elementi di lavoro. Ogni elemento di lavoro è chiamato vertice. vertici Hello sono raggruppati come vertice Super (noto anche come fase) e visualizzati come grafico processi. le etichette di Hello verde fase nel grafico processo hello mostrano fasi hello.
  
    Ogni vertice in una fase esegue hello stesso tipo di lavoro con diverse parti di hello stessi dati. Ad esempio, se si dispone di un file con 1 TB di dati e centinaia di vertici leggono i dati nel file, ogni vertice sta leggendo un blocco. I quali vengono raggruppati in hello stessa fase ed eseguono stessa funzionano in diverse parti di stesso file di input.
  
  * <a name="state-information"></a>Informazioni sulla fase
    
      In una determinata fase, vengono visualizzati alcuni numeri manifesto hello.
    
      ![Fase del grafico del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Estrarre: nome hello di una fase, denominata da un metodo dell'operazione numero e hello.
    * 84 vertici: hello conteggio totale dei vertici in questa fase. Figura Hello indica il numero di elementi di lavoro è suddivisa in questa fase.
    * s/vertex 12.90: hello vertice medio tempo di esecuzione per questa fase. Questo valore viene calcolato da SUM (tempo di esecuzione di ogni vertice)/(conteggio totale vertici). Che indica se è possibile assegnare tutti i vertici hello eseguiti con parallelismo, completamento della fase intero hello in 12.90 s. Inoltre, se tutti hello lavoro in questa fase viene eseguita in modo seriale, il costo di hello sarebbe #vertices * tempo medio.
    * 850,895 rows written (850,895 righe scritte): il conteggio totale delle righe scritte in questa fase.
    * R/W (L/S): la quantità di dati letti/scritti in questa fase, espressa in byte.
    * Colori: Lo stato di diversi vertice hello fase tooindicate vengono utilizzati i colori.
      
      * Verde indica vertice hello è riuscita.
      * Arancione indica vertice hello viene ripetuta. vertice Hello eseguito un nuovo tentativo non riuscito, ma viene ritentata automaticamente e dal sistema di hello e hello complessivo fase viene completata correttamente. Se vertice hello ritentata ma ancora non riuscito, colori hello diventa rosso e hello intero processo non riuscito.
      * Rosso indica non riuscita, il che significa un vertice determinati era stata ritentata più volte dal sistema hello ma ancora non riuscito. In questo caso verrà toofail intero processo hello.
      * Il blu indica che un determinato vertice è in esecuzione.
      * Il bianco indica hello è in attesa del vertice. vertice Hello potrebbe essere in attesa toobe pianificato dopo un ADLAU diventa disponibile, o può essere attesa per l'input perché i relativi dati di input non siano pronti.
      
      È possibile trovare altre informazioni per la fase di hello spostando il cursore del mouse da uno stato:
      
      ![Dettagli della fase del grafico del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Vertici: Vengono illustrati i dettagli di vertici hello, ad esempio, il numero di vertici in totale, vertici quanti sono stati completati, sono che non è riuscita o è ancora in esecuzione o in attesa e così via.
  * Data read cross/intra pod (Lettura dati tra pod/nel pod): i file e i dati vengono archiviati in più pod nel file system distribuito. valore Hello descrive la quantità di dati non è stato letto hello stesso contenitore o cross pod.
  * Tempo di calcolo totale: somma hello ogni vertice tempo di esecuzione in fase di hello, è possibile durante l'esecuzione di hello tempo impiegata se tutte le attività in fase di hello in solo un vertice.
  * Dati e le righe di lettura/scrittura: indica la quantità dei dati o le righe sono stati letti/scritti o necessario toobe leggere.
  * Vertex read failures (Errori di lettura vertici): descrive il numero di vertici con esito negativo durante la lettura dei dati.
  * Elimina vertice duplicato: se un vertice è troppo lenta, sistema di hello può pianificare più vertici toorun hello stesso elemento di lavoro. Vertici reductant verranno eliminati una volta che uno dei vertici hello completata correttamente. Vertice duplicati Elimina numero hello di record di vertici che vengono rimossi come duplicati in fase di hello.
  * Revoca vertex: vertice hello è stata completata, ma ottenere nuovamente in seguito a causa di motivi toosome. Ad esempio, se perde il vertice a valle intermedia dei dati di input, viene chiesto toorerun vertice upstream hello.
  * Esecuzioni di pianificazione vertex: tempo totale di hello vertici hello sono state pianificate.
  * I dati di vertici Media/Min/Max letti: hello minimo/medio/massimo di ogni vertice leggere i dati.
  * Durata: hello il tempo di clock che impiega una fase, è necessario tooload profilo toosee questo valore.
  * Riproduzione del processo
    
      Data Lake Analitica esegue i processi e gli archivi hello vertici in esecuzione le informazioni dei processi di hello, ad esempio quando vengono avviati i vertici hello, arrestato, non è riuscita e come vengono ripetute, e così via. Le informazioni di hello automaticamente registrate in archivio query hello e archiviate in un profilo del processo. È possibile scaricare il profilo di processo tramite "Carica profilo" nella visualizzazione processi hello ed è possibile visualizzare hello riproduzione processo dopo aver scaricato hello processo profilo.
    
      La riproduzione di processo è una visualizzazione di sintesi di cosa è successo cluster hello. Consente di controllare lo stato di avanzamento del processo e rilevare visivamente eventuali colli di bottiglia o anomalie delle prestazioni in un periodo molto breve, in genere inferiore a 30 secondi.
  * Visualizzazione della mappa termica del processo 
    
      È possibile selezionare la mappa di calore processo di riepilogo a discesa di visualizzazione hello nel grafico di processo. 
    
      ![Visualizzazione della mappa termica del grafico del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Mostra mappa di calore dei / o, ora e la velocità effettiva hello di un processo tramite cui trova in cui il processo di hello impiega la maggior parte del tempo di hello, o se il processo è un processo di limiti dei / o e così via.
    
      ![Esempio di mappa termica del grafico del processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Stato: hello stato di esecuzione processo, vedere le informazioni in [fase informazioni](#stage-information).
    * Dati letti/scritti: mappa di calore hello del totale dei dati letti/scritti in ogni fase.
    * Tempo di calcolo: mappa di calore hello di SUM (tempo di esecuzione ogni vertice), è possibile considerare questo il tempo necessario se viene eseguito tutto il lavoro in fase di hello con vertice solo 1.
    * Tempo medio di esecuzione per ogni nodo: mappa di calore hello di SUM (tempo di esecuzione ogni vertice) / (numero di vertici). Ovvero se è possibile assegnare tutti i vertici hello eseguiti con parallelismo, fase intero hello verrà eseguita in questo periodo di tempo.
    * Velocità effettiva di Input/Output: mappa di calore hello di velocità effettiva di input/output di ogni fase, è possibile verificare se il processo è un processo di binding i/o mediante l'oggetto.
* Operazioni sui metadati
  
    È possibile eseguire alcune operazioni sui metadati nello script U-SQL, ad esempio creare un database, eliminare una tabella e così via. Queste operazioni vengono visualizzate in Metadata Operation (Operazione sui metadati) dopo la compilazione. Qui è possibile trovare asserzioni, creare e cancellare entità.
  
    ![Operazioni sui metadati di visualizzazione processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Cronologia dello stato
  
    Hello cronologia dello stato viene inoltre visualizzata nella finestra di riepilogo dei processi, ma è possibile ottenere ulteriori dettagli. È possibile trovare hello dettagliata informazioni, ad esempio quando viene preparata processo hello, in coda, avviato, è terminata. È inoltre possibile trovare quante volte è stato compilato il processo di hello (hello CcsAttempts: 1), quando è in realtà cluster di hello processo inviato toohello (hello dettaglio: invio processo toocluster) e così via.
  
    ![Cronologia dello stato di visualizzazione processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnostica
  
    strumento Hello individua automaticamente l'esecuzione del processo. e invierà avvisi in caso di errori o problemi di prestazioni nei processi. Si noti che è necessario toodownload profilo tooget informazioni complete di seguito. 
  
    ![Diagnostica di visualizzazione processo di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Warnings (Avvisi): viene visualizzato un avviso del compilatore. È possibile scegliere "x problemi" collegamento toohave ulteriori dettagli quando viene visualizzato l'avviso hello.
  * Vertex run too long (Esecuzione prolungata vertice): se si verifica il timeout di uno dei vertici, ad esempio dopo 5 ore, i problemi vengono indicati qui.
  * Resource usage (Uso risorse): se il parallelismo assegnato è maggiore o minore rispetto al valore necessario, i problemi vengono indicati qui. Anche cui è possibile fare clic su risorse utilizzo toosee ulteriori informazioni ed eseguire scenari di simulazione toofind una migliore allocazione delle risorse (per ulteriori informazioni, vedere questa Guida).
  * Memory check (Controllo memoria): se uno dei vertici usa più di 5 GB di memoria, i problemi vengono visualizzati qui. Il sistema potrebbe arrestare l'esecuzione del processo se viene usata una quantità di memoria superiore al limite di sistema.

## <a name="job-detail"></a>Dettagli processo
Dettagli processo Mostra informazioni dettagliate del processo di hello, inclusi Script, le risorse e visualizzazione esecuzione vertice di hello.

![Azure Data Lake Analytics di Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Hello script U-SQL del processo di hello viene archiviato nell'archivio query hello. È possibile visualizzare script U-SQL originale hello e inviare nuovamente se necessario.
* Risorse
  
    È possibile trovare l'output di compilazione processo hello archiviato nell'archivio query hello tramite le risorse. Ad esempio, è possibile trovare "algebra.xml" è utilizzato tooshow hello grafico processi, gli assembly hello che è stato registrato e così via di seguito.
* Vertex execution view (Visualizzazione esecuzioni vertici)
  
    Mostra i dettagli di esecuzione dei vertici. Hello profilo processo consente di archiviare ogni log di esecuzione di vertici, ad esempio dati totali letti/scritti, runtime, lo stato e così via. Tramite questa visualizzazione è possibile ottenere altre informazioni su come è stato eseguito un processo. Per ulteriori informazioni, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Passaggi successivi
* informazioni di diagnostica toolog, vedere [accesso ai log di diagnostica per Azure Data Lake Analitica](data-lake-analytics-diagnostic-logs.md)
* toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).
* visualizzazione di esecuzione vertice toouse, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

