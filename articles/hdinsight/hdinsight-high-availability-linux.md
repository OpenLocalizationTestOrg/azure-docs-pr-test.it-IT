---
title: "disponibilità aaaHigh per Hadoop - HDInsight di Azure | Documenti Microsoft"
description: "Informazioni su come i cluster HDInsight migliorano l'affidabilità e la disponibilità tramite l'uso di un nodo head aggiuntivo. Informazioni su come ciò influisce sulla servizi Hadoop, ad esempio Ambari e Hive, nonché come tooindividually connettersi tooeach nodo head con SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "alta disponibilità di hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Disponibilità e affidabilità dei cluster Hadoop in HDInsight

Cluster HDInsight forniscono due nodi head tooincrease hello disponibilità e l'affidabilità dei servizi di Hadoop e i processi in esecuzione.

Hadoop ottiene alta disponibilità e affidabilità replicando i servizi e i dati su più nodi di un cluster. Tuttavia le distribuzioni standard di Hadoop hanno in genere un singolo nodo head. Qualsiasi interruzione del nodo head singolo hello può causare lavoro toostop di hello del cluster. HDInsight fornisce due headnodes tooimprove Hadoop disponibilità e affidabilità.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Disponibilità e affidabilità dei nodi

I nodi in un cluster HDInsight vengono implementati con macchine virtuali di Azure. Hello nelle sezioni seguenti vengono illustrano i tipi di nodo singolo hello utilizzati con HDInsight. 

> [!NOTE]
> Non tutti i tipi di nodo vengono usati per un tipo di cluster. Ad esempio, un tipo di cluster Hadoop non ha alcun nodo Nimbus. Per ulteriori informazioni sui nodi utilizzato dai tipi di cluster HDInsight, vedere sezione tipi di Cluster hello di hello [cluster basati su Linux creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.

### <a name="head-nodes"></a>Nodi head

tooensure un'elevata disponibilità dei servizi Hadoop, HDInsight fornisce due nodi head. Entrambi i nodi head sono contemporaneamente attivi e in esecuzione all'interno del cluster HDInsight hello. Alcuni servizi, ad esempio HDFS o YARN, sono "attivi"in qualsiasi momento soltanto in un nodo head. Altri servizi, ad esempio HiveServer2 o MetaStore Hive sono attivi su entrambi i nodi head in hello contemporaneamente.

I nodi HEAD (e gli altri nodi in HDInsight) hanno un valore numerico come parte del nome host hello del nodo hello. Ad esempio, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Non associare il valore numerico hello con tratti di un nodo primario o secondario. valore numerico di Hello è presente tooprovide solo un nome univoco per ogni nodo.

### <a name="nimbus-nodes"></a>Nodi Nimbus

I nodi nimbus sono disponibili con i cluster Storm. nodi Nimbus Hello forniscono simili funzionalità toohello Hadoop JobTracker per la distribuzione e il monitoraggio di elaborazione tra i nodi di lavoro. HDInsight offre due nodi Nimbus per i cluster Storm

### <a name="zookeeper-nodes"></a>Nodi Zookeeper

I nodi [ZooKeeper](http://zookeeper.apache.org/) vengono usati per la designazione di leader dei servizi master nei nodi head. Sono anche utilizzati tooinsure che servizi, nodi di dati (lavoratore) e gateway sapere quale nodo head è attivo in un servizio principale. Per impostazione predefinita, HDInsight specifica tre nodi ZooKeeper.

### <a name="worker-nodes"></a>Nodi di lavoro

Nodi di lavoro eseguono analisi di dati effettivi hello quando cluster toohello inviato è un processo. Se un nodo di lavoro non riesce, attività hello che stava eseguendo è il nodo di lavoro tooanother inviato. Per impostazione predefinita, HDInsight crea quattro nodi del ruolo di lavoro. È possibile modificare questo numero toosuit esigenze durante e dopo la creazione del cluster.

### <a name="edge-node"></a>Nodo perimetrale

Analisi dei dati all'interno di cluster hello non partecipa attivamente un nodo del bordo. Viene usato dagli sviluppatori o i data scientist quando lavorano con Hadoop. vite di nodo edge Hello in hello stessa rete virtuale di Azure come hello altri nodi cluster hello e accedere direttamente a tutti gli altri nodi. Hello edge nodo può essere utilizzato senza portare le risorse da servizi critici di Hadoop o i processi di analisi.

Attualmente, il Server di R in HDInsight è hello unico tipo di cluster che fornisce un nodo del bordo per impostazione predefinita. Per il Server di R in HDInsight, hello bordo viene usato il codice R di test in locale nel nodo hello prima di inviarla toohello cluster per l'elaborazione distribuita.

Per informazioni sull'uso di un nodo del bordo con tipi di cluster diverso dal Server di R, vedere hello [utilizzare nodi periferici in HDInsight](hdinsight-apps-use-edge-node.md) documento.

## <a name="accessing-hello-nodes"></a>Accesso ai nodi di hello

Cluster di accesso toohello su hello internet viene fornito tramite un gateway pubblico. L'accesso è limitato tooconnecting toohello i nodi head e (se presente) hello nodo del bordo. Accesso tooservices in esecuzione nei nodi head hello non viene effettuata con più nodi head. Hello gateway pubblica le route richieste toohello nodo head che ospita hello servizio richiesto. Ad esempio, se Ambari è attualmente ospitato nel nodo head secondario hello, gateway hello instrada le richieste in ingresso per il nodo toothat Ambari.

Accesso tramite gateway pubblica hello è limitato tooport 443 (HTTPS), 22 e 23.

* Porta __443__ è usato tooaccess Ambari e altri web dell'interfaccia utente o le API REST ospitate nei nodi head hello.

* Porta __22__ nodo head di tooaccess utilizzati hello primario o nodo di bordo con SSH.

* Porta __23__ è usato tooaccess hello secondario nodo head con SSH. Ad esempio, `ssh username@mycluster-ssh.azurehdinsight.net` si connette toohello primario nodo head del cluster di hello denominato **mycluster**.

Per ulteriori informazioni sull'utilizzo di SSH, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Nomi di dominio completo interni (FQDN) 

I nodi in un cluster HDInsight dispongono di un indirizzo IP e un nome di dominio completo è accessibile solo dal cluster hello interno. Quando si accede ai servizi in cluster hello utilizzando hello interno FQDN o indirizzo IP, è consigliabile utilizzare Ambari tooverify hello IP o FQDN toouse durante l'accesso servizio hello.

Ad esempio, hello Oozie servizio può essere eseguito solo su un nodo head e utilizzando hello `oozie` comando da una sessione SSH richiede servizio toohello di hello URL. Questo URL può essere recuperato da Ambari tramite hello comando seguente:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Questo comando restituisce un toohello simile valore seguente comando, che contiene hello interno URL toouse con hello `oozie` comando:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Per ulteriori informazioni sull'uso di API REST Ambari hello, vedere [monitorare e gestire HDInsight utilizzando l'API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Accesso ad altri tipi di nodo

È possibile connettersi toonodes che sono non direttamente accessibile su internet di hello utilizzando hello dei seguenti metodi:

* **SSH**: una volta connessi tooa nodo head con SSH, è quindi possibile utilizzare SSH da hello nodo head tooconnect tooother i nodi nel cluster hello. Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

* **Tunnel SSH**: se è necessario tooaccess un servizio web ospitato in uno dei nodi di hello che non è esposta toohello internet, è necessario utilizzare un tunnel SSH. Per ulteriori informazioni, vedere hello [utilizzare un tunnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

* **Rete virtuale di Azure**: se hello di HDInsight cluster fa parte di una rete virtuale di Azure, tutte le risorse della stessa rete virtuale possono accedere direttamente ai tutti i nodi cluster hello. Per ulteriori informazioni, vedere hello [estendere HDInsight mediante la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

## <a name="how-toocheck-on-a-service-status"></a>Come toocheck in uno stato di servizio

lo stato di hello toocheck di servizi in esecuzione nei nodi head hello, utilizzare hello dell'interfaccia utente Web Ambari o hello Ambari REST API.

### <a name="ambari-web-ui"></a>Interfaccia utente Web Ambari

interfaccia utente Web Ambari Hello è visualizzabile in https://CLUSTERNAME.azurehdinsight.net. Sostituire **CLUSTERNAME** con nome hello del cluster. Se richiesto, immettere le credenziali utente di hello HTTP per il cluster. è il nome utente HTTP predefinito Hello **admin** e hello password è hello immessi durante la creazione di cluster hello.

Quando si arriva nella pagina Ambari hello, servizi di hello installato sono elencati in a sinistra della pagina hello hello.

![Servizi installati](./media/hdinsight-high-availability-linux/services.png)

Esistono una serie di icone che possono essere visualizzati lo stato successivo tooindicate del servizio tooa. Tutti gli avvisi correlati tooa servizio può essere visualizzato utilizzando hello **avvisi** collegamento nella parte superiore di hello della pagina hello. È possibile selezionare ogni tooview servizio ulteriori informazioni su di esso.

Pagina servizio hello offre informazioni sullo stato di hello e configurazione di ogni servizio, non fornisce informazioni in cui il servizio di hello nodo head è in esecuzione. tooview questa informazioni, utilizzare hello **host** collegamento nella parte superiore di hello della pagina hello. Questa pagina consente di visualizzare gli host in cluster hello, inclusi i nodi head hello.

![elenco di host](./media/hdinsight-high-availability-linux/hosts.png)

Collegamento hello selezionando per uno dei nodi head hello Visualizza servizi hello e componenti in esecuzione su tale nodo.

![Stato dei componenti](./media/hdinsight-high-availability-linux/nodeservices.png)

Per ulteriori informazioni sull'utilizzo Ambari, vedere [Monitor e gestire HDInsight mediante hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>API REST Ambari

API REST Ambari Hello è disponibile sulla hello internet. gateway di Hello HDInsight pubblica gestisce richieste toohello head nodo di routing che attualmente ospita hello API REST.

È possibile utilizzare hello stato hello toocheck del comando di un servizio tramite l'API REST Ambari hello seguenti:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Sostituire **PASSWORD** con password dell'account utente (amministrazione) hello HTTP.
* Sostituire **CLUSTERNAME** con nome hello del cluster di hello.
* Sostituire **SERVICENAME** con nome hello del servizio hello da toocheck hello stato.

Ad esempio, lo stato hello toocheck di hello **HDFS** servizio in un cluster denominato **mycluster**, con una password di **password**, si utilizzerebbe hello comando seguente:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

risposta Hello è simile toohello JSON seguente:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Hello URL indica che il servizio di hello è attualmente in esecuzione in un nodo head denominato **hn0 CLUSTERNAME**.

Hello stato indica che il servizio di hello è attualmente in esecuzione, o **STARTED**.

Se non si conosce quali servizi sono installati nel cluster hello, è possibile utilizzare hello comando tooretrieve un elenco di seguito:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Per ulteriori informazioni sull'uso di API REST Ambari hello, vedere [monitorare e gestire HDInsight utilizzando l'API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Componenti del servizio

Servizi potrebbero contenere componenti che si desidera toocheck hello stato singolarmente. Ad esempio, HDFS contiene componente NameNode hello. tooview informazioni su un componente, il comando hello è:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Se non si conosce quali componenti vengono forniti da un servizio, è possibile utilizzare hello comando tooretrieve un elenco di seguito:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Come tooaccess file di registro in nodi head hello

### <a name="ssh"></a>SSH

Durante il nodo head di tooa connesso tramite SSH, i file di log sono reperibile nella **var/log**. Ad esempio, **/var/log/hadoop-yarn/yarn** contiene i registri per YARN.

Ogni nodo head può contenere le voci di log univoco, è consigliabile controllare entrambi accede hello.

### <a name="sftp"></a>SFTP

È possibile connettersi toohello nodo head usando hello SSH File Transfer Protocol o Secure File Transfer Protocol (SFTP) e scaricare i file di log hello direttamente.

Toousing simili quando ci si connette toohello cluster è necessario fornire un client SSH hello SSH utente account name e hello SSH l'indirizzo del cluster di hello. ad esempio `sftp username@mycluster-ssh.azurehdinsight.net`. Specificare password hello per conto di hello quando richiesto, o fornire una chiave pubblica utilizzando hello `-i` parametro.

Una volta connessi, viene visualizzato un prompt `sftp>` . Da questo prompt è possibile modificare le directory nonché caricare e scaricare i file. Ad esempio, hello seguenti comandi cambiare directory toohello **/var/log/hadoop/hdfs** directory e quindi scaricare tutti i file nella directory hello.

    cd /var/log/hadoop/hdfs
    get *

Per un elenco di comandi disponibili, immettere `help` in hello `sftp>` prompt dei comandi.

> [!NOTE]
> Esistono anche interfacce grafiche che consentono di toovisualize hello file system quando connesso tramite SFTP. Ad esempio, [MobaXTerm](http://mobaxterm.mobatek.net/) consente toobrowse hello file system utilizzando un tooWindows simile interfaccia Explorer.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess con Ambari i file di log, è necessario utilizzare un tunnel SSH. interfacce di Hello web per i singoli servizi hello non vengono esposte pubblicamente hello Internet. Per informazioni sull'utilizzo di un tunnel SSH, vedere hello [usare SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) documento.

Hello dell'interfaccia utente Web Ambari, selezionare servizio hello desiderato tooview registri per (ad esempio, YARN). Utilizzare quindi **collegamenti rapidi** tooselect quali hello tooview nodo head per il registro.

![Utilizzando rapida collega tooview log](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Come tooconfigure hello dimensione del nodo

è possibile selezionare dimensioni Hello di un nodo solo durante la creazione del cluster. È possibile trovare un elenco di hello diverse dimensioni di macchina virtuale disponibile per HDInsight su hello [pagina dei prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Quando si crea un cluster, è possibile specificare dimensioni di hello dei nodi di hello. Hello informazioni riportate di seguito vengono fornite indicazioni sulla modalità toospecify hello dimensione tramite hello [portale di Azure][preview-portal], [Azure PowerShell][azure-powershell], hello e [CLI di Azure][azure-cli]:

* **Portale di Azure**: durante la creazione di un cluster, è possibile impostare dimensioni hello dei nodi di hello usati dal cluster hello:

    ![Immagine della creazione guidata di cluster con la selezione delle dimensioni del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* **CLI di Azure**: quando si utilizza hello `azure hdinsight cluster create` comando, è possibile impostare dimensioni hello head hello, lavoro e i nodi ZooKeeper utilizzando hello `--headNodeSize`, `--workerNodeSize`, e `--zookeeperNodeSize` parametri.

* **Azure PowerShell**: quando si utilizza hello `New-AzureRmHDInsightCluster` cmdlet, è possibile impostare dimensioni hello head hello, lavoro e i nodi ZooKeeper utilizzando hello `-HeadNodeVMSize`, `-WorkerNodeSize`, e `-ZookeeperNodeSize` parametri.

## <a name="next-steps"></a>Passaggi successivi

Utilizzare hello seguendo i collegamenti toolearn ulteriori informazioni sulle operazioni descritte in questo documento.

* [Riferimento REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Installare e configurare hello CLI di Azure](../cli-install-nodejs.md)
* [Installare e configurare Azure PowerShell](/powershell/azure/overview)
* [Gestire HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)
* [provisioning di cluster HDInsight basati su Linux](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
