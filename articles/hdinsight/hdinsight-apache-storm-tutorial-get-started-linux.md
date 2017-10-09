---
title: esempi di aaaStorm starter su Apache Storm in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toodo analitica di dati ed elaborare i dati in tempo reale usando Apache Storm hello esempi storm starter in HDInsight.
keywords: storm starter, esempio di apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Introduzione a Apache Storm in HDInsight utilizzando hello storm starter esempi

Informazioni su come toouse Apache Storm HDInsight con hello esempi storm starter.

Apache Storm è un sistema di calcolo in tempo reale scalabile, a tolleranza di errore e distribuito per l'elaborazione di flussi di dati. Con Storm in Azure HDInsight è possibile creare un cluster Storm basato sul cloud che esegue analisi di Big Data in tempo reale.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Familiarità con SSH e SCP**. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Creare un cluster di Storm

Utilizzare hello seguire toocreate passi un elevato numero di cluster HDInsight:

1. Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo**, **Intelligence + Analitica**, quindi selezionare **HDInsight**.

    ![Creazione di un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Da hello **nozioni di base** pannello immettere hello le seguenti informazioni:

    * **Nome del cluster**: nome hello del cluster HDInsight hello.
    * **Sottoscrizione**: selezionare hello toouse di sottoscrizione.
    * **Nome utente account di accesso del cluster** e **password dell'account di accesso Cluster**: accesso hello quando si accede a cluster hello tramite HTTPS. Usare questi servizi tooaccess credenziali, ad esempio hello dell'interfaccia utente Web Ambari o l'API REST.
    * **Secure Shell (SSH) username**: hello account di accesso quando si accede a cluster hello su SSH. Per impostazione predefinita la password di hello è hello come password di accesso cluster hello.
    * **Gruppo di risorse**: hello gruppo toocreate hello cluster della risorsa in.
    * **Percorso**: hello Azure area toocreate hello cluster.

    ![Selezionare la sottoscrizione](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Selezionare **Cluster tipo**, e quindi set hello seguendo i valori hello **configurazione Cluster** pannello:

    * **Tipo di cluster**: Storm

    * **Sistema operativo**: Linux

    * **Versione**: Storm 1.1.0 (HDI 3.6)

    * **Livello cluster**: Standard

    Infine, utilizzare hello **selezionare** pulsante toosave impostazioni.

    ![Selezionare il tipo di cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Dopo aver selezionato il tipo di cluster hello, utilizzare hello __selezionare__ tooset hello cluster tipo di pulsante. Successivamente, utilizzare hello __Avanti__ configurazione di base toofinish pulsante.

5. Da hello **archiviazione** pannello selezionare o creare un account di archiviazione. Per i passaggi hello in questo documento, lasciare hello altri campi in questo pannello valori predefiniti di hello. Hello utilizzare __Avanti__ configurazione dell'archiviazione toosave pulsante.

    ![Configurare le impostazioni di account di archiviazione hello per HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Da hello **riepilogo** pannello, verificare la configurazione per il cluster hello hello. Hello utilizzare __modifica__ collegamenti toochange eventuali impostazioni non sono corrette. Infine, utilizzare the__Create__ pulsante toocreate hello cluster.

    ![Riepilogo della configurazione del cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Può richiedere di cluster hello toocreate di too20 minuti.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Eseguire un esempio di Storm Starter in HDInsight

1. Connettere il cluster di HDInsight toohello tramite SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Se si utilizza un toosecure password account utente SSH, si è tooenter richiesto è. Se si utilizza una chiave pubblica, è necessario utilizzare hello `-i` toospecify parametro hello chiave privata corrispondente. ad esempio `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilizzare hello comando toostart una topologia di esempio seguente:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > Nelle versioni precedenti di HDInsight, nome della classe hello della topologia hello è `storm.starter.WordCountTopology` anziché `org.apache.storm.starter.WordCountTopology`.

    Questo comando avvia una topologia di hello esempio WordCount su cluster hello, con un nome descrittivo 'wordcount'. In modo casuale genera frasi e occorrenza hello conteggio di ogni parola nella frase hello.

    > [!NOTE]
    > Quando si inviano cluster toohello topologie, è prima necessario copiare i file jar hello contenente cluster hello prima di utilizzare hello `storm` comando. Hello utilizzare `scp` file hello toocopy di comando. Ad esempio, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > Esempio WordCount Hello e altri esempi di storm starter, sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Se si è interessati in visualizzazione origine hello per esempi di hello storm starter, è possibile trovare codice hello [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Questo collegamento riguarda Storm 1.1, che viene offerto con HDInsight 3.6. Per altre versioni di Storm, utilizzare hello __ramo__ pulsante nella parte superiore di hello di hello pagina tooselect una versione diversa di Storm.

## <a name="monitor-hello-topology"></a>Monitoraggio hello topologia

Ciao Storm UI fornisce un'interfaccia web per l'utilizzo con l'esecuzione di topologie ed è incluso nel cluster HDInsight.

Utilizzare hello seguente topologia di hello toomonitor passaggi utilizzando hello UI Storm:

1. hello toodisplay dell'interfaccia utente Storm, aprire un toohttps://CLUSTERNAME.azurehdinsight.net/stormui browser web. Sostituire **CLUSTERNAME** con nome hello del cluster.

    > [!NOTE]
    > Se richiesto tooprovide un nome utente e una password, immettere Amministrazione cluster hello (amministratore) e la password utilizzati quando la creazione di cluster di hello.

2. In **riepilogo topologia**selezionare hello **wordcount** voce hello **nome** colonna. Informazioni sulla topologia di hello.

    ![Dashboard di Storm con informazioni sulla topologia di Storm Starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    In questa pagina vengono hello le seguenti informazioni:

    * **Statistiche di topologia** -informazioni di base sulle prestazioni di topologia hello, organizzati in intervalli di tempo.

        > [!NOTE]
        > Se si seleziona un intervallo di tempo specifico tempo finestra modifiche hello per le informazioni visualizzate in altre sezioni della pagina hello.

    * **Spouts** -spouts, inclusi l'ultimo errore hello restituiti da ogni beccuccio informazioni di base.

    * **Bolts** : informazioni di base sui bolt.

    * **Configurazione della topologia** -informazioni dettagliate su configurazione della topologia hello.

    Questa pagina fornisce inoltre le azioni che possono essere eseguite sulla topologia di hello:

    * **Activate** : riprende l'elaborazione di una topologia disattivata.

    * **Deactivate** : sospende una topologia in esecuzione.

    * **Ribilanciare** -consente di regolare il parallelismo hello della topologia hello. È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello. Ribilanciamento regola toocompensate di parallelismo per il numero di hello aumentato o diminuito di nodi nel cluster hello. Per ulteriori informazioni, vedere [comprensione parallelismo hello di una topologia di Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kill** -termina una topologia di Storm dopo hello specificato timeout.

3. In questa pagina, selezionare una voce da hello **Spouts** o **bulloni** sezione. Informazioni sul componente selezionato hello viene visualizzate.

    ![Storm Dashboard con informazioni sui componenti selezionati.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Questa pagina consente di visualizzare hello le seguenti informazioni:

    * **Statistiche beccuccio/fulmine** -informazioni di base sulle prestazioni del componente hello, organizzati in intervalli di tempo.

        > [!NOTE]
        > Se si seleziona un intervallo di tempo specifico tempo finestra modifiche hello per le informazioni visualizzate in altre sezioni della pagina hello.

    * **Statistiche di input** (bullone solo) - informazioni sui componenti che producono dati utilizzati dalle fulmine hello.

    * **Output stats** : informazioni sui dati generati dal bolt.

    * **Executors** : informazioni sulle istanze del componente.

    * **Errors** : errori generati dal componente.

4. Quando si visualizzano i dettagli di hello di un fulmine beccuccio, selezionare una voce da hello **porta** colonna hello **executor** sezione tooview dettagli per un'istanza specifica del componente hello.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    In questo esempio hello word **sette** si è verificato 1493957 volte. Questo conteggio è quante volte si è verificato parola hello poiché questa topologia è stata avviata.

## <a name="stop-hello-topology"></a>Arrestare la topologia hello

Restituire toohello **riepilogo topologia** pagina topologia di conteggio parole hello e quindi selezionare hello **Kill** pulsante hello **azioni topologia** sezione. Quando richiesto, immettere 10 per hello toowait di secondi prima di arrestare topologia hello. Dopo il periodo di timeout hello topologia hello non viene più visualizzata quando si visita hello **dell'interfaccia utente Storm** sezione dashboard hello.

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Se si verifica un problema di creazione del cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Passaggi successivi

In questa esercitazione Apache Storm state hello nozioni fondamentali sulle operazioni con Storm in HDInsight. Per ulteriori informazioni come troppo[topologie basate sul linguaggio di sviluppo utilizzando Maven](hdinsight-storm-develop-java-topology.md).

Se si ha già familiarità con lo sviluppo basato su Java topologie e si desidera toodeploy un tooHDInsight topologia esistente, vedere [distribuire e gestire le topologie di Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Uno sviluppatore .NET può creare le topologie C# o C#/Java ibride con Virtual Studio. Per altre informazioni, vedere [Sviluppare topologie C# per Apache Storm in HDInsight con gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Per le topologie di esempio che possono essere utilizzate con Storm in HDInsight, vedere hello seguono esempi:

* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
