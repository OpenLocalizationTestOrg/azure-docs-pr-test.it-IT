---
title: aaaUse Tez UI con HDInsight - basati su Windows Azure | Documenti Microsoft
description: Informazioni su come i processi di hello toouse UI Tez toodebug Tez in HDInsight di HDInsight basati su Windows.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Utilizzare i processi di UI Tez toodebug Tez hello in HDInsight basati su Windows
Hello UI Tez è una pagina web che possono essere utilizzati i processi toounderstand e debug che utilizzano Tez come motore di esecuzione hello nei cluster HDInsight basati su Windows. Hello Tez UI consente processo hello toovisualize come un grafico degli elementi connessi, analizza ogni elemento e recuperare le statistiche e informazioni di registrazione.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Prerequisiti
* Un cluster HDInsight basato su Windows. Per la procedura di creazione di un nuovo cluster, vedere [Introduzione all'uso di HDInsight basato su Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Hello UI Tez è disponibile solo in cluster HDInsight basati su Windows creati dopo l'8 febbraio 2016.
  >
  >
* Un client Desktop remoto basato su Windows.

## <a name="understanding-tez"></a>Informazioni su Tez
Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce. Per i cluster HDInsight basati su Windows, è un motore facoltativo che è possibile abilitare per l'Hive usando hello comando seguente come parte della query Hive:

    set hive.execution.engine=tez;

Quando il lavoro viene inviato tooTez, viene creato un indirizzate aciclico Graph (DAG) che descrive l'ordine di hello di esecuzione delle azioni hello richiesto dal processo hello. Singole azioni vengono chiamate i vertici ed eseguire una parte di hello processo globale. l'esecuzione effettiva Hello del lavoro hello descritto da un vertice viene chiamata un'attività e può essere distribuita in più nodi nel cluster hello.

### <a name="understanding-hello-tez-ui"></a>Hello comprensione Tez UI
Hello UI Tez è una pagina web che fornisce informazioni sui processi in esecuzione o che hanno in precedenza è stata eseguita con Tez. Consente di hello tooview DAG generati da Tez, come viene distribuito tra i cluster, i contatori, ad esempio la memoria utilizzata da attività e i vertici e informazioni sull'errore. Può offrire informazioni utili in hello seguenti scenari:

* Monitoraggio dei processi con esecuzione prolungata, visualizzazione hello lo stato di avanzamento della mappa e ridurre le attività.
* Analisi dei dati cronologici per i processi di esito positivo o negativo toolearn come l'elaborazione potrebbe essere migliorata o perché non è riuscito.

## <a name="generate-a-dag"></a>Generare un DAG
Hello Tez UI conterrà dati solo se un processo che utilizza hello Tez motore è attualmente in esecuzione o è stato eseguito in hello precedente. Le query Hive semplici in genere possono essere risolte senza usare Tez, ma quelle più complesse che eseguono operazioni di filtro, raggruppamento, ordinamento, join e così via di solito richiedono Tez.

Utilizzare hello seguendo i passaggi toorun una query Hive che verrà eseguito utilizzando Tez.

1. In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster HDInsight.
2. Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **Editor Hive**. Verrà visualizzata una pagina con hello seguenti query di esempio.

        Select * from hivesampletable

    Cancellare la query di esempio hello e sostituirlo con il seguente hello.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Seleziona hello **Invia** pulsante. Hello **sessione del processo** sezione hello parte inferiore della pagina hello verrà visualizzato lo stato di hello di query hello. Una volta hello troppo modifiche allo stato**completato**selezionare hello **Visualizza dettagli** collegare tooview hello risultati. Hello **Output processo** dovrebbe essere simile toohello seguenti:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Utilizzare hello Tez UI
> [!NOTE]
> Hello UI Tez è disponibile solo da desktop hello hello head dei nodi del cluster, è necessario utilizzare i nodi head toohello tooconnect del Desktop remoto.
>
>

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight. Selezionare hello hello superiore del Pannello di HDInsight hello **Desktop remoto** icona. Verrà visualizzata blade desktop remoto hello

    ![Icona Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Dal Pannello di hello Desktop remoto, selezionare **Connetti** nodo head del cluster toohello tooconnect. Quando richiesto, utilizzare hello cluster utente nome e la password tooauthenticate hello connessione di Desktop remoto.

    ![Icona Connetti di Desktop remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Se non è stato abilitato connessione Desktop remoto, fornire un nome utente, password e la data di scadenza, quindi selezionare **abilitare** tooenable Desktop remoto. Una volta è stata abilitata, è possibile utilizzare hello precedenti passaggi tooconnect.
   >
   >
3. Una volta connessi, aprire Internet Explorer sul desktop remoto di hello, icona dell'ingranaggio hello selezionare nella parte superiore di hello destra del browser hello e quindi selezionare **impostazioni visualizzazione compatibilità**.
4. Dalla parte inferiore di hello del **impostazioni visualizzazione compatibilità**, deselezionare la casella di controllo hello per **visualizzare i siti intranet in vista di compatibilità** e **gli elenchi di compatibilità di utilizzare Microsoft**, e quindi selezionare **Chiudi**.
5. In Internet Explorer passare toohttp://headnodehost:8188/tezui / #/. Verrà visualizzata hello Tez UI

    ![Interfaccia utente di Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Quando viene caricato hello Tez UI, verrà visualizzato un elenco di DAG attualmente in esecuzione o sono stati eseguiti nel cluster hello. visualizzazione predefinita Hello include hello Dag Name, Id, autore, stato, ora di inizio, ora di fine, durata, ID dell'applicazione e coda. È possibile aggiungere più colonne utilizzando l'icona dell'ingranaggio hello in hello destra della pagina hello.

    Se si dispone di una sola voce, sia per le query hello che è stato eseguito nella sezione precedente hello. Se si dispone di più voci, è possibile eseguire la ricerca specificando i criteri di ricerca nei campi hello sopra hello DAG, quindi premere **invio**.
6. Seleziona hello **Dag Name** per hello la voce più recente DAG. Verrà visualizzato informazioni hello DAG, nonché toodownload opzione hello un file zip dei file JSON che contengono informazioni hello DAG.

    ![DAG Details](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Sopra hello **dettagli DAG** sono numerosi collegamenti che possono essere utilizzati toodisplay informazioni hello DAG.

   * **DAG Counters** (Contatori DAG) visualizza informazioni sui contatori per il DAG.
   * **Graphical View** (Visualizzazione grafica) visualizza una rappresentazione grafica del DAG.
   * **Tutti i vertici** Visualizza un elenco di vertici hello in questo DAG.
   * **Tutte le attività** Visualizza un elenco di attività hello per tutti i vertici in questo DAG.
   * **Tutti TaskAttempts** Visualizza informazioni su hello tenta toorun attività per questa DAG.

     > [!NOTE]
     > Se si scorre una visualizzazione della colonna hello per vertici, attività e TaskAttempts, si noti che sono presenti collegamenti tooview **contatori** e **consente di visualizzare o scaricare i log** per ogni riga.
     >
     >

     Se si è verificato un errore con il processo di hello, hello DAG dettagli verrà visualizzato lo stato non riuscito, insieme ai collegamenti tooinformation sull'operazione non riuscita di hello. Informazioni di diagnostica verranno visualizzate sotto i dettagli di hello DAG.
8. Selezionare **Graphical View** (Visualizzazione grafica). Verrà visualizzata una rappresentazione grafica di hello DAG. È possibile posizionare il mouse hello sopra ogni vertice in hello vista toodisplay le informazioni.

    ![Graphical View](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Facendo clic su un vertice caricherà hello **dettagli del Vertex** per quell'elemento. Fare clic su hello **1 mappa** dettagli del vertex toodisplay per questo elemento. Selezionare **conferma** navigazione hello tooconfirm.

    ![Vertex Details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Si noti che è ora possibile i collegamenti nella parte superiore di hello della pagina hello toovertices correlate e attività.

    > [!NOTE]
    > Può arrivare in questa pagina inoltre tornando troppo**DAG dettagli**, se si seleziona **dettagli del Vertex**e quindi selezionando hello **1 mappa** vertice.
    >
    >

    * **Vertex Counters** (Contatori vertice) visualizza informazioni sui contatori per il vertice.
    * **Tasks** (Attività) visualizza le attività per il vertice.
    * **Attività tentativi** consente di visualizzare informazioni sulle attività di toorun tentativi per questo vertice.
    * **Sources &amp; Sinks** (Origini e sink) visualizza le origini dati e i sink per il vertice.

      > [!NOTE]
      > Come con menu precedente hello, è possibile scorrere visualizzazione della colonna hello per le attività, i tentativi di attività e origini & Sinks__ toodisplay collega toomore informazioni per ogni elemento.
      >
      >
11. Selezionare **attività**, e quindi selezionare hello elemento **00_000000**. Verranno visualizzati i dati di **Task Details** (Dettagli attività) per questa attività. Da questa schermata è possibile visualizzare **Task Counters** (Contatori attività) e **Task Attempts** (Tentativi attività).

    ![Dettagli dell'attività](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso come hello toouse Tez Visualizza, altre informazioni, vedere [utilizzando Hive in HDInsight](hdinsight-use-hive.md).

Per informazioni tecniche relative a Tez dettagliate, vedere hello [pagina Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).
