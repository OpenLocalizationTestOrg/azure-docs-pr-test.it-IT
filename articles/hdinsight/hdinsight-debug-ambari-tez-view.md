---
title: aaaUse Ambari Tez visualizzazione con HDInsight - Azure | Documenti Microsoft
description: Informazioni su come hello toouse Ambari Tez visualizzare processi Tez toodebug in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Utilizzare viste Ambari toodebug Tez processi in HDInsight

interfaccia utente Web Ambari per HDInsight Hello contiene una visualizzazione di Tez che può essere utilizzati i processi toounderstand e debug che utilizzano Tez. visualizzazione di Tez Hello consente processo hello toovisualize come un grafico degli elementi connessi, analizza ogni elemento e recuperare le statistiche e informazioni di registrazione.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Prerequisiti

* Un cluster HDInsight basato su Linux. Per la procedura di creazione di un cluster, vedere [Esercitazione di Hadoop: Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Un moderno Web browser che supporta HTML5.

## <a name="understanding-tez"></a>Informazioni su Tez

Tez è un framework estendibile per l'elaborazione dati in Hadoop, che garantisce una maggiore velocità rispetto alla tradizionale elaborazione di MapReduce. Per i cluster HDInsight basati su Linux, è il motore predefinito hello per l'Hive.

Tez crea indirizzate aciclico Graph (DAG) che descrive l'ordine di hello delle azioni necessarie per processi. Singole azioni vengono chiamate i vertici ed eseguire una parte di hello processo globale. l'esecuzione effettiva Hello del lavoro hello descritto da un vertice viene chiamata un'attività e può essere distribuita in più nodi nel cluster hello.

### <a name="understanding-hello-tez-view"></a>Hello informazioni sulla visualizzazione Tez

Hello Tez visualizzazione fornisce informazioni cronologiche e informazioni sui processi in esecuzione. Queste informazioni mostrano in che modo un processo viene distribuito tra i cluster. Vengono inoltre visualizzati i contatori utilizzati da attività e i vertici e informazioni sull'errore correlate toohello processo. Può offrire informazioni utili in hello seguenti scenari:

* Monitoraggio dei processi con esecuzione prolungata, visualizzazione hello lo stato di avanzamento della mappa e ridurre le attività.
* Analisi dei dati cronologici per i processi di esito positivo o negativo toolearn come l'elaborazione potrebbe essere migliorata o perché non è riuscito.

## <a name="generate-a-dag"></a>Generare un DAG

Hello Tez vista contiene dati solo se un processo che utilizza hello Tez motore è attualmente in esecuzione o è stato eseguito in precedenza. Le query Hive semplici possono essere risolte senza usare Tez. Query più complesse che eseguono filtraggio, raggruppamento, ordinamento, unione e così via. Utilizzare il motore di Tez hello.

Utilizzare i seguenti passaggi toorun una query Hive che utilizza Tez hello:

1. In un web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster HDInsight.

2. Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **viste** icona. La presente icona ha l'aspetto di una serie di quadrati. Nell'elenco a discesa hello che viene visualizzato, selezionare **Hive vista**.

    ![Selezione della visualizzazione Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Quando viene caricato hello vista Hive, seguente hello Incolla query hello Editor di Query e quindi fare clic su **eseguire**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Una volta completato il processo di hello, verrà visualizzato l'output di hello visualizzati in hello **risultati della Query processo** sezione. i risultati di Hello saranno simile toohello seguente testo:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Seleziona hello **Log** scheda. Viene visualizzato toohello di informazioni simili seguente testo:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Salvare hello **id App** valore, questo valore viene utilizzato nella sezione successiva hello.

## <a name="use-hello-tez-view"></a>Utilizzare hello Tez visualizzazione

1. Scegliere dal menu a hello nella parte superiore di hello della pagina hello hello **viste** icona. Nell'elenco a discesa hello che viene visualizzato, selezionare **Tez vista**.

    ![Selezione della visualizzazione Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Quando viene caricato hello Tez visualizzazione, viene visualizzato un elenco di query hive che sono attualmente in esecuzione o sono stati eseguiti nel cluster hello.

    ![Tutti i DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Se si dispone di una sola voce, è per query hello che è stato eseguito nella sezione precedente hello. Se si dispone di più voci, è possibile cercare utilizzando i campi di hello nella parte superiore di hello della pagina hello.

4. Seleziona hello **ID Query** per una query Hive. Informazioni sulle query hello.

    ![DAG Details](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. le schede di Hello in questa pagina consentono di hello tooview le seguenti informazioni:

    * **Eseguire una query Dettagli**: informazioni dettagliate su query Hive hello.
    * **Tempistiche**: informazioni sulla durata di ogni fase dell'elaborazione.
    * **Configurazioni**: configurazione di hello utilizzata per la query.

    Da __Dettagli Query__ è possibile utilizzare hello collegamenti toofind informazioni hello __applicazione__ o hello __DAG__ per questa query.
    
    * Hello __applicazione__ collegamento Visualizza le informazioni su hello applicazione YARN per questa query. Da qui è possibile accedere hello YARN registri delle applicazioni.
    * Hello __DAG__ collegamento Visualizza le informazioni su un grafo aciclico diretto hello per questa query. Da qui è possibile visualizzare una rappresentazione grafica di hello DAG. È inoltre possibile trovare informazioni sui vertici hello all'interno di hello DAG.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come hello toouse Tez Visualizza, altre informazioni, vedere [utilizzando Hive in HDInsight](hdinsight-use-hive.md).

Per informazioni tecniche relative a Tez dettagliate, vedere hello [pagina Tez in Hortonworks](http://hortonworks.com/hadoop/tez/).

Per ulteriori informazioni sull'uso di Ambari con HDInsight, vedere [gestione dei cluster HDInsight tramite interfaccia utente Web Ambari hello](hdinsight-hadoop-manage-ambari.md)
