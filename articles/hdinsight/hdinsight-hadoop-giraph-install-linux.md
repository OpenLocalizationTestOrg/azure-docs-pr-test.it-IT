---
title: aaaInstall e utilizzare Giraph in HDInsight (Hadoop) - Azure | Documenti Microsoft
description: "Informazioni su come i cluster usando le azioni Script tooinstall Giraph in HDInsight basati su Linux. Azioni script consentono di cluster hello toocustomize durante la creazione, modifica della configurazione del cluster o l'installazione di servizi e le utilità."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Installare Giraph nei cluster HDInsight Hadoop e usare i grafici di Giraph tooprocess su larga scala

Informazioni su come tooinstall Giraph Apache in un cluster HDInsight. Hello script azione di HDInsight consente toocustomize il cluster eseguendo uno script bash. Gli script possono essere utilizzato toocustomize cluster durante e dopo la creazione del cluster.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>Che cos'è Giraph?

[Apache Giraph](http://giraph.apache.org/) consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight. È possibile usare i grafici per modellare le relazioni tra gli oggetti, Ad esempio, le connessioni hello tra i router in una rete di grandi dimensioni come hello Internet o le relazioni tra gli utenti su social network. Elaborazione Graph consente tooreason sulle relazioni hello tra gli oggetti in un grafico, ad esempio:

* Identificare possibili amici sulla base delle relazioni correnti.

* Identificazione hello itinerario più breve tra due computer in una rete.

* Calcolare il numero di dimensioni di hello pagina delle pagine Web.

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati: supporto di Microsoft consente tooisolate e risolvere i problemi correlati toothese componenti.
>
> I componenti personalizzati, ad esempio Giraph, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Supporto Microsoft potrebbe essere in grado di tooresolving problema di hello. In caso contrario, è necessario consultare le community open source, da cui è possibile ottenere supporto approfondito per la tecnologia specifica. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>Quali script hello esegue

Questo script esegue hello seguenti azioni:

* Installa troppo Giraph`/usr/hdp/current/giraph`

* Hello copie `giraph-examples.jar` toodefault archiviazione (WASB) per il cluster di file:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Installare Giraph mediante azioni script

Un tooinstall di script di esempio Giraph in un cluster HDInsight è disponibile in hello seguente posizione:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

In questa sezione vengono fornite istruzioni su come toouse hello script di esempio durante la creazione di cluster hello utilizzando hello portale di Azure.

> [!NOTE]
> Un'azione di script può essere applicata utilizzando uno dei seguenti metodi hello:
> * Azure PowerShell
> * Hello CLI di Azure
> * Hello HDInsight .NET SDK
> * Modelli di Gestione risorse di Azure
> 
> È inoltre possibile applicare tooalready azioni script i cluster in esecuzione. Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).

1. Avviare la creazione di un cluster attenendosi alla procedura hello in [cluster HDInsight basati su Linux creare](hdinsight-hadoop-create-linux-clusters-portal.md), ma non completare la creazione.

2. In hello **configurazione facoltativa** pannello seleziona **azioni Script**e fornire hello le seguenti informazioni:

   * **NOME**: immettere un nome descrittivo per l'azione script hello.

   * **URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: selezionare questa voce

   * **LAVORO**: lasciare questa voce deselezionata

   * **ZOOKEEPER**: lasciare questa voce deselezionata

   * **PARAMETRI**: lasciare questo campo vuoto

3. Nella parte inferiore di hello di hello **azioni Script**, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti. Infine, utilizzare hello **selezionare** pulsante nella parte inferiore di hello di hello **configurazione facoltativa** informazioni di configurazione facoltativa hello toosave blade.

4. Continuare con la creazione di cluster hello come descritto in [cluster HDInsight basati su Linux creare](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Come si usa Giraph in HDInsight?

Dopo aver creato il cluster hello, utilizzare hello passaggi toorun hello SimpleShortestPathsComputation esempio incluso in Giraph seguente. Questo esempio viene utilizzato basic hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementazione per trovare il percorso più breve di hello tra gli oggetti in un grafico.

1. Connettere il cluster di HDInsight toohello tramite SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Comando che segue hello utilizzare toocreate un file denominato **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Utilizzare hello segue testo come contenuto di hello di questo file:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, utilizzando il formato di hello `[source_id, source_value,[[dest_id], [edge_value],...]]`. Ogni riga rappresenta una relazione tra un oggetto `source_id` e uno o più oggetti `dest_id`. Hello `edge_value` può essere considerato come livello di attendibilità hello o una distanza di connessione hello tra `source_id` e `dest\_id`.

    Disegnare out, e utilizza il valore hello (o peso) come distanza hello tra oggetti, dati hello potrebbero essere simile hello seguente diagramma:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. file hello toosave, usare **Ctrl + X**, quindi **Y**e infine **invio** tooaccept nome del file hello.

4. Utilizzare hello seguente dati hello toostore nell'account di archiviazione primario per il cluster HDInsight:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Eseguire l'esempio SimpleShortestPathsComputation hello utilizzando hello comando seguente:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    parametri di Hello utilizzati con questo comando vengono descritti in hello nella tabella seguente:

   | . | Risultato |
   | --- | --- |
   | `jar` |file jar Hello contenente esempi di hello. |
   | `org.apache.giraph.GiraphRunner` |classe Hello utilizzato negli esempi di hello toostart. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |esempio Hello utilizzato. In questo esempio calcola percorso più breve di hello tra ID 1 e tutti gli altri ID grafico hello. |
   | `-ca mapred.job.tracker` |nodo head Hello per cluster hello. |
   | `-vif` |Hello toouse di formato di input per i dati di input hello. |
   | `-vip` |file di dati di input Hello. |
   | `-vof` |formato di output di Hello. In questo caso, ID e valore come testo normale. |
   | `-op` |percorso di output di Hello. |
   | `-w 2` |numero di Hello di toouse processi di lavoro. In questo esempio, 2. |

    Per ulteriori informazioni su questi e altri parametri utilizzati con Giraph esempi, vedere hello [delle Guide rapide Giraph](http://giraph.apache.org/quick_start.html).

6. Al termine il processo di hello, risultati di hello vengono archiviati in hello **/example/out/shotestpaths** directory. Hello nomi file di output iniziano con **parte-m -** e terminare con un numero che indica in primo luogo, in secondo luogo, hello file e così via. Utilizzare hello output hello tooview del comando seguente:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    output di Hello risulterà simile toohello seguente testo:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    esempio SimpleShortestPathComputation Hello è hardcoded toostart con ID 1 oggetto e trovare gli oggetti tooother percorso più brevi hello. output di Hello è nel formato hello `destination_id` e `distance`. Hello `distance` è hello valore (o peso), dei bordi hello percorsi compreso tra 1 ID oggetto e hello ID di destinazione.

    Visualizzazione dei dati, è possibile verificare i risultati di hello viaggiando percorsi più brevi hello tra ID 1 e tutti gli altri oggetti. percorso più breve di Hello tra ID 1 e 4 ID è 5. Questo valore è hello totale distanza <span style="color:orange">ID 1 e 3</span>e quindi <span style="color:red">ID 3 e 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Passaggi successivi

* [Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).

* [Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md).
