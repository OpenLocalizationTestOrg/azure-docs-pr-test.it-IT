---
title: aaaHue con Hadoop in cluster basati su HDInsight Linux - Azure | Documenti Microsoft
description: "Informazioni su come cluster di tonalità tooinstall in HDInsight e utilizzare tunneling tooroute hello richieste tooHue. Utilizzare l'archiviazione di tonalità toobrowse ed eseguire Hive o Pig."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Installare e usare Hue nei cluster Hadoop di HDInsight

Informazioni su come cluster di tonalità tooinstall in HDInsight e utilizzare tunneling tooroute hello richieste tooHue.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>Informazioni su Hue
La tonalità corrisponde che toointeract utilizzato da un set di applicazioni Web con un cluster Hadoop. Può usare l'archiviazione di hello toobrowse tonalità associata a un cluster Hadoop (nel caso di hello di cluster HDInsight, WASB), eseguire i processi Hive e script Pig e così via. Hello componenti seguenti sono disponibili con le installazioni di tonalità in un cluster HDInsight Hadoop.

* Editor Hive Beeswax
* Pig
* Metastore Manager
* Oozie
* FileBrowser (che discute contenitore predefinito tooWASB)
* Job Browser

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.
>
> I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Installare Hue mediante azioni script

Hello script tooinstall tonalità in un cluster HDInsight basati su Linux è disponibile all'indirizzo https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. È possibile utilizzare questo tooinstall script tonalità nei cluster con BLOB di archiviazione di Azure (WASB) o archivio Azure Data Lake come spazio di archiviazione predefinito.

In questa sezione vengono fornite istruzioni su come toouse hello script durante il provisioning di cluster di hello utilizzando hello portale di Azure.

> [!NOTE]
> Azure PowerShell, hello CLI di Azure, HDInsight .NET SDK hello o modelli di gestione risorse di Azure possono anche essere azioni script tooapply utilizzato. È inoltre possibile applicare tooalready azioni script i cluster in esecuzione. Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Avviare il provisioning di un cluster attenendosi alla procedura hello in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md), ma non viene completato il provisioning.

   > [!NOTE]
   > cluster di tonalità tooinstall in HDInsight, hello nodo head consigliato dimensione è di almeno A4 (8 core, 14 GB di memoria).
   >
   >
2. In hello **configurazione facoltativa** pannello seleziona **azioni Script**e fornire informazioni di hello, come illustrato di seguito:

    ![Specificare i parametri di azione script per Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Specificare i parametri di azione script per Hue")

   * **NOME**: immettere un nome descrittivo per l'azione script hello.
   * **URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: selezionare questa opzione
   * **LAVORO**: lasciare vuoto questo campo.
   * **ZOOKEEPER**: lasciare vuoto questo campo.
   * **PARAMETRI**: lasciare vuoto questo campo.
3. Nella parte inferiore di hello di hello **azioni Script**, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti. Infine, utilizzare hello **selezionare** pulsante nella parte inferiore di hello di hello **configurazione facoltativa** informazioni di configurazione facoltativa hello toosave blade.
4. Continuano il provisioning del cluster di hello, come descritto in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Usare Hue con i cluster HDInsight

Tunneling SSH è tooaccess delle modalità solo tonalità di hello in cluster hello dopo che è in esecuzione. Tunneling tramite SSH consente hello traffico toogo direttamente toohello nodo head di hello del cluster in cui è in esecuzione la tonalità. Al termine cluster hello provisioning, utilizzare hello seguire passaggi toouse tonalità di un cluster HDInsight Linux.

> [!NOTE]
> È consigliabile utilizzare Firefox web browser toofollow hello istruzioni riportate di seguito.
>
>

1. Utilizzare le informazioni di hello in [tooaccess usare SSH Tunneling Ambari web dell'interfaccia utente, ResourceManager, JobHistory, NameNode, Oozie e l'altra interfaccia utente web](hdinsight-linux-ambari-ssh-tunnel.md) toocreate un SSH tunnel dal cluster HDInsight toohello sistema client e quindi configurare il Web browser toouse hello tunnel SSH come proxy.

2. Dopo aver creato un tunnel SSH e configurato il traffico tooproxy browser attraverso di esso, è necessario trovare il nome host hello del nodo head primario hello. Ciò si realizza tramite la connessione cluster toohello tramite SSH sulla porta 22. Ad esempio, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` in **USERNAME** è il nome utente SSH e **CLUSTERNAME** hello nome del cluster.

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una volta connessi, utilizzare hello dopo il nome di dominio completo di comando tooobtain hello del nodo head primario hello:

        hostname -f

    Verrà restituito una nome simile toohello che segue:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Si tratta dell'host di hello del nodo head primario hello sito Web di tonalità hello in cui si trova.
4. Utilizzare il portale tonalità hello di hello browser tooopen in http://HOSTNAME:8888. Sostituire il nome host con nome hello ottenuto nel passaggio precedente hello.

   > [!NOTE]
   > Quando si accede per hello prima volta, sarà richiesta toocreate toolog un account nel portale di tonalità toohello. è possibile specificare le credenziali di Hello saranno limitato toohello portal e non sono correlati toohello credenziali di amministratore o SSH utente specificato quando il cluster di hello effettuare il provisioning.
   >
   >

    ![Portale di account di accesso toohello tonalità](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "specificare le credenziali per il portale di tonalità")

### <a name="run-a-hive-query"></a>Eseguire una query Hive
1. Dal portale di tonalità hello, fare clic su **gli editor di Query**, quindi fare clic su **Hive** editor dell'Hive tooopen hello.

    ![Usare Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Usare Hive")
2. In hello **Assist** scheda **Database**, dovrebbe essere **hivesampletable**. Si tratta di una tabella di esempio inclusa in tutti i cluster Hadoop in HDInsight. Immettere una query di esempio nel riquadro di destra hello e visualizzare l'output di hello in hello **risultati** scheda nel riquadro di hello sotto, come illustrato nella cattura di schermata hello.

    ![Eseguire query Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Eseguire query Hive")

    È inoltre possibile utilizzare hello **grafico** scheda toosee una rappresentazione visiva del risultato hello.

### <a name="browse-hello-cluster-storage"></a>Sfoglia risorsa di archiviazione cluster hello
1. Dal portale di tonalità hello, fare clic su **File Browser** nell'angolo superiore destro di hello hello barra dei menu.
2. Per impostazione predefinita viene visualizzata browser file hello hello **/utente/myuser** directory. Fare clic sulla barra hello immediatamente prima di directory utente hello nella radice di hello percorso toogo toohello del contenitore di archiviazione di Azure hello associato hello cluster.

    ![Usare il browser file](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Usare il browser file")
3. Fare clic su un file o cartella toosee hello operazioni disponibili. Hello utilizzare **caricare** pulsante nella directory corrente di hello angolo destro tooupload file toohello. Hello utilizzare **New** pulsante toocreate nuovi file o directory.

> [!NOTE]
> Visualizzatore file di tonalità Hello può mostrare solo il contenuto di hello del contenitore predefinito hello associato al cluster HDInsight hello. Qualsiasi account/contenitori di archiviazione aggiuntive che potrebbero avere associato il cluster hello non sarà accessibili tramite browser file hello. Tuttavia, altri contenitori hello associati hello cluster sarà sempre accessibili per i processi Hive hello. Ad esempio, se si immette il comando hello `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` nell'editor di hello Hive, è possibile visualizzare il contenuto di hello di anche altri contenitori. In questo comando **newcontainer** non è associata a un cluster di contenitore di hello predefinito.
>
>

## <a name="important-considerations"></a>Considerazioni importanti
1. Hello script utilizzato tooinstall tonalità installato solo nel nodo head primario hello del cluster di hello.

2. Durante l'installazione, vengono riavviati più servizi Hadoop (HDFS, YARN, MR2, Oozie) per l'aggiornamento della configurazione di hello. Al termine dello script hello l'installazione di tonalità, operazione può richiedere del tempo per altri toostart servizi Hadoop. Ciò potrebbe influire inizialmente sulle prestazioni di Hue. Una volta avviati tutti i servizi, Hue sarà completamente funzionale.
3. Tonalità non riconosce i processi Tez, hello predefinito corrente per l'Hive. Se si desidera toouse MapReduce come hello Hive motore di esecuzione, aggiornare hello toouse di script hello comando nello script seguente:

        set hive.execution.engine=mr;

4. Con i cluster Linux, è possibile disporre di uno scenario in cui i servizi eseguono nel nodo head primario hello e hello Gestione risorse potrebbe essere in esecuzione su hello secondario. Questo scenario potrebbe causare errori (mostrati sotto) quando si utilizza dettagli tooview tonalità di processi in esecuzione nel cluster hello. Tuttavia, è possibile visualizzare i dettagli dei processi hello quando hello è stato completato.

   ![Errore nel portale di Hue](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Errore nel portale di Hue")

   Questo è dovuto tooa problema noto. In alternativa, modificare Ambari in modo hello active Resource Manager viene eseguito anche nel nodo head primario hello.
5. Hue riconosce WebHDFS mentre i cluster HDInsight usano Archiviazione di Azure Storage tramite `wasb://`. In tal caso, uno script personalizzato di hello utilizzato con script azione Installa WebWasb, che è un servizio WebHDFS compatibile per la comunicazione con tooWASB. In questo caso, anche se il portale di tonalità hello afferma HDFS in posizioni (ad esempio quando si sposta il puntatore del mouse su hello **File Browser**), devono essere interpretata come WASB.

## <a name="next-steps"></a>Passaggi successivi
* [Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilizzare cluster personalizzazione tooinstall che cluster Giraph in HDInsight Hadoop. Giraph consente grafico tooperform elaborazione utilizzando Hadoop e può essere utilizzato con Azure HDInsight.
* [Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilizzare cluster personalizzazione tooinstall che cluster Solr in HDInsight Hadoop. Solr consente operazioni di ricerca avanzate tooperform sui dati archiviati.
* [Installare R nei cluster HDInsight](hdinsight-hadoop-r-scripts-linux.md). Utilizzare cluster personalizzazione tooinstall R nei cluster HDInsight Hadoop. R è un linguaggio open source e un ambiente per l'elaborazione statistica. Fornisce centinaia di funzioni statistiche predefinite e un proprio linguaggio che combina aspetti di programmazione funzionale con aspetti di programmazione orientata agli oggetti. Offre inoltre funzionalità complete di grafica.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
