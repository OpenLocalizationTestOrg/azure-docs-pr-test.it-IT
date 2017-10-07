---
title: aaaTips per l'utilizzo di Hadoop in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Suggerimenti di implementazione per l'utilizzo di cluster HDInsight basati su Linux (Hadoop) in un ambiente familiare di Linux in esecuzione in hello cloud di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Informazioni sull'uso di HDInsight in Linux

I cluster HDInsight di Azure forniscono Hadoop in un ambiente familiare di Linux in esecuzione in hello cloud di Azure. Per la maggior parte delle operazioni, dovrebbe funzionare esattamente come qualsiasi altra installazione di Hadoop in Linux. Questo documento indica le differenze specifiche che è opportuno conoscere.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Prerequisiti

Numero di passaggi hello in questo documento utilizzano hello seguente utilità, che potrebbe essere necessario toobe installato nel sistema.

* [cURL](https://curl.haxx.se/) -utilizzato toocommunicate con servizi basati sul web
* [jq](https://stedolan.github.io/jq/) -documenti JSON tooparse utilizzati
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (anteprima) - tooremotely utilizzati gestire servizi di Azure

## <a name="users"></a>Utenti

A meno che non sia [aggiunto al dominio](hdinsight-domain-joined-introduction.md), HDInsight deve essere considerato un sistema a **utente singolo**. Cluster di hello con autorizzazioni di amministratore, viene creato un singolo account utente SSH. È possibile creare altri account SSH, ma dispongono anche di cluster toohello accesso di amministratore.

HDInsight aggiunto al dominio offre il supporto per più utenti e impostazioni di autorizzazioni e ruoli più granulari. Per altre informazioni, vedere [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire cluster HDInsight aggiunti al dominio).

## <a name="domain-names"></a>Nomi di dominio

Hello completo toouse (FQDN) di nome di dominio durante la connessione toohello cluster da internet è hello  **&lt;clustername >. cluster>.azurehdinsight.NET** o (SSH)  **&lt;clustername-ssh >. cluster>.azurehdinsight.NET**.

Internamente, ogni nodo nel cluster hello ha un nome assegnato durante la configurazione del cluster. i nomi di toofind hello cluster, vedere hello **host** pagina hello dell'interfaccia utente Web Ambari. È inoltre possibile utilizzare hello tooreturn un elenco di host da hello Ambari REST API seguenti:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Sostituire **PASSWORD** con password hello hello dell'account dell'amministratore, e **CLUSTERNAME** con nome hello del cluster. Questo comando restituisce un documento JSON che contiene un elenco di host hello hello cluster. Jq è usato tooextract hello `host_name` valore dell'elemento per ogni host.

Se è necessario il nome hello toofind del nodo hello per un servizio specifico, è possibile eseguire una query Ambari per il componente. Host di hello toofind per nodo del nome hello HDFS, ad esempio, utilizzare hello comando seguente:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Questo comando restituisce un documento JSON che descrive il servizio hello e quindi jq estrae solo hello `host_name` valore per gli host hello.

## <a name="remote-access-tooservices"></a>Accesso remoto tooservices

* **Ambari (Web)**: https://&lt;nomecluster>.azurehdinsight.net

    Eseguire l'autenticazione con l'utente amministratore di cluster hello e la password e quindi accedere tooAmbari.

    L'autenticazione è crittografato, utilizzare HTTPS toohelp assicurarsi sempre che hello connessione sia protetta.

    > [!IMPORTANT]
    > Alcune delle interfacce utente disponibili tramite Ambari hello accedere utilizzando un nome di dominio interno di nodi. Dominio interno i nomi non sono accessibili pubblicamente tramite hello internet. Quando si tenta di alcune funzionalità tooaccess su hello Internet possono verificarsi errori di "server non trovato".
    >
    > funzionalità complete di hello toouse di hello Ambari web dell'interfaccia utente, utilizzare un SSH tunnel tooproxy web traffico toohello nodo head del cluster. Vedere [tooaccess usare SSH Tunneling Ambari web dell'interfaccia utente, ResourceManager, JobHistory, NameNode, Oozie e altre interfacce utente web](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)**: https://&lt;nomecluster&gt;.azurehdinsight.net/ambari

    > [!NOTE]
    > Eseguire l'autenticazione tramite password e l'utente amministratore di cluster hello.
    >
    > L'autenticazione è crittografato, utilizzare HTTPS toohelp assicurarsi sempre che hello connessione sia protetta.

* **WebHCat (Templeton)**: https://&lt;nomecluster>.azurehdinsight.net/templeton

    > [!NOTE]
    > Eseguire l'autenticazione tramite password e l'utente amministratore di cluster hello.
    >
    > L'autenticazione è crittografato, utilizzare HTTPS toohelp assicurarsi sempre che hello connessione sia protetta.

* **SSH** - &lt;nome cluster>-ssh.azurehdinsight.net sulla porta 22 o 23. Porta 22 è usato tooconnect toohello nodo head primario, mentre 23 è usato tooconnect toohello secondario. Per ulteriori informazioni sui nodi head hello, vedere [cluster disponibilità e affidabilità di Hadoop in HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > È possibile accedere solo i nodi head del cluster hello tramite SSH da un computer client. Una volta connessi, è possibile accedere quindi i nodi di lavoro hello tramite SSH da un nodo head.

## <a name="file-locations"></a>Percorsi dei file

I file relativi alla Hadoop sono reperibili nei nodi del cluster hello in `/usr/hdp`. Questa directory contiene hello seguente sottodirectory:

* **2.2.4.9-1**: nome della directory hello è versione hello di hello Hortonworks Data Platform utilizzato da HDInsight. numero di Hello il cluster può essere diverso da quello hello elencati di seguito.
* **corrente**: questa directory contiene i collegamenti toosubdirectories in hello **2.2.4.9-1** directory. La directory esiste in modo che non si dispone di numero di versione di hello tooremember.

I dati di esempio e i file con estensione jar sono disponibili nel file system Hadoop Distributed File System (HDFS) in `/example` e `/HdiSamples`

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, Archiviazione di Azure e Data Lake Store

Nella maggior parte delle distribuzioni di Hadoop, HDFS viene supportata dall'archiviazione locale nel computer hello hello cluster. L'uso di sistema locale può essere costoso per una soluzione basata su cloud dove viene addebitata una tariffa oraria o al minuto per le risorse di calcolo.

HDInsight utilizza BLOB in archiviazione di Azure né archivio Azure Data Lake come archivio predefinito hello. Questi servizi offrono hello seguenti vantaggi:

* Archiviazione a lungo termine economica
* Accessibilità da servizi esterni, ad esempio siti Web, utilità di caricamento e download di file, SDK di linguaggi diversi e Web browser

> [!WARNING]
> HDInsight supporta solo account di archiviazione di Azure __per uso generico__. Non supporta attualmente hello __nell'archiviazione Blob__ tipo di account.

Un account di archiviazione di Azure può contenere fino too4.75 TB, anche se ogni BLOB (o file da una prospettiva di HDInsight) possono avere al massimo too195 GB. Archivio Azure Data Lake può aumentare in modo dinamico toohold trilioni dei file, con maggiori rispetto a un petabyte di singoli file. Per altre informazioni, leggere gli articoli di approfondimento sui [BLOB](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) e su [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Quando si utilizza l'archiviazione di Azure o archivio Data Lake, non è necessario toodo nulla da dati hello tooaccess di HDInsight. Ad esempio, hello comando seguente vengono elencati i file di hello `/example/data` cartella indipendentemente dal fatto che viene memorizzata nell'archiviazione di Azure o archivio Data Lake:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI e schema

Alcuni comandi potrebbero richiedere lo schema di hello toospecify come parte di hello URI quando si accede a un file. Ad esempio, hello componente Storm HDFS richiede lo schema di hello toospecify. Quando si utilizza l'archiviazione non predefiniti (archiviazione aggiunto come cluster di archiviazione "aggiuntive" toohello), è necessario utilizzare sempre lo schema di hello come parte di hello URI.

Quando si utilizza __di archiviazione di Azure__, utilizzare uno dei seguenti schemi URI hello:

* `wasb:///`: per accedere allo spazio di archiviazione predefinito usando la comunicazione non crittografata.

* `wasbs:///`: per accedere allo spazio di archiviazione predefinito usando la comunicazione crittografata.  schema di wasbs Hello è supportato solo da HDInsight versione 3.6 in poi.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: usato durante la comunicazione con un account di archiviazione non predefinito, ad esempio quando si dispone di un account di archiviazione aggiuntivo o quando si accede a dati archiviati in un account di archiviazione pubblicamente accessibile.

Quando si utilizza __archivio Data Lake__, utilizzare uno dei seguenti schemi URI hello:

* `adl:///`: Accesso hello predefinito archivio Data Lake per cluster hello.

* `adl://<storage-name>.azuredatalakestore.net/`: usato durante la comunicazione con un Data Lake Store non predefinito. Nonché tooaccess dati all'esterno della directory radice hello del cluster HDInsight.

> [!IMPORTANT]
> Quando si utilizza l'archivio Data Lake come archivio predefinito hello per HDInsight, è necessario specificare un percorso all'interno di hello archivio toouse come radice hello di archiviazione di HDInsight. percorso predefinito di Hello è `/clusters/<cluster-name>/`.
>
> Quando si utilizza `/` o `adl:///` tooaccess dati, è possibile accedere solo dati memorizzati nella directory principale di hello (ad esempio, `/clusters/<cluster-name>/`) del cluster di hello. tooaccess i dati in un punto qualsiasi nell'archivio hello utilizzare hello `adl://<storage-name>.azuredatalakestore.net/` formato.

### <a name="what-storage-is-hello-cluster-using"></a>Quali archiviazione sta utilizzando cluster hello

È possibile utilizzare la configurazione archiviazione Ambari tooretrieve hello predefinita per i cluster di hello. Comando curl utilizzando le informazioni di configurazione di tooretrieve HDFS seguente hello utilizzare e filtrarli utilizzando [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Restituisce il primo server di toohello configurazione applicata di hello (`service_config_version=1`), che contiene queste informazioni. Potrebbe essere necessario toolist tutte le versioni di configurazione toofind hello più recente.

Questo comando restituisce un toohello simile valore URI seguente:

* `wasb://<container-name>@<account-name>.blob.core.windows.net` se si usa un account di archiviazione di Azure.

    nome dell'account Hello è hello nome dell'account di archiviazione di Azure hello, mentre il nome di contenitore hello è il contenitore di blob hello radice hello dell'archiviazione cluster hello.

* `adl://home` se si usa Azure Data Lake Store. Nome archivio Data Lake hello tooget, utilizzare hello in seguito a chiamata REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Questo comando restituisce hello dopo il nome host: `<data-lake-store-account-name>.azuredatalakestore.net`.

    directory di hello tooget all'interno di archivio di hello radice hello per HDInsight, utilizzare hello in seguito a chiamata REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Questo comando restituisce un toohello simile percorso seguente percorso: `/clusters/<hdinsight-cluster-name>/`.

È anche possibile trovare informazioni sull'archiviazione hello hello portale di Azure usando hello alla procedura seguente:

1. In hello [portale di Azure](https://portal.azure.com/), selezionare il cluster HDInsight.

2. Da hello **proprietà** selezionare **gli account di archiviazione**. informazioni sull'archiviazione Hello per cluster hello viene visualizzati.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Come accedere ai file dall'esterno di HDInsight

Sono disponibili un vari modi dati tooaccess dal cluster HDInsight hello esterno. di seguito Hello sono alcuni collegamenti tooutilities e gli SDK che possono essere utilizzati toowork con i dati:

Se si utilizza __di archiviazione di Azure__, vedere i seguenti collegamenti per individuare i modi che è possibile accedere ai dati hello:

* [Interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): comandi dell'interfaccia della riga di comando per l'uso con Azure. Dopo l'installazione, utilizzare hello `az storage` comando per informazioni sull'utilizzo di archiviazione, o `az storage blob` per comandi specifici del blob.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): uno script Python per l'uso con i BLOB in Archiviazione di Azure.
* Vari SDK:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [API REST di archiviazione](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Se si utilizza __archivio Azure Data Lake__, vedere i seguenti collegamenti per individuare i modi che è possibile accedere ai dati hello:

* [Web browser](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Interfaccia della riga di comando di Azure 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [API REST WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Strumenti di Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Ridimensionamento del cluster

scalabilità funzionalità cluster di Hello consente toodynamically modificare il numero di hello di nodi di dati utilizzato da un cluster. È possibile eseguire operazioni di ridimensionamento mentre altri processi sono in esecuzione nel cluster.

tipi di cluster diverso Hello dipendono dal ridimensionamento come indicato di seguito:

* **Hadoop**: in caso di ridimensionamento verso il basso il numero di hello di nodi in un cluster, alcuni dei servizi di hello cluster hello vengono riavviati. Operazioni di ridimensionamento può provocare i processi in esecuzione o in sospeso toofail al completamento di hello di hello l'operazione di ridimensionamento. È possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.
* **HBase**: server locali sono automaticamente bilanciato entro pochi minuti dopo il completamento dell'operazione di ridimensionamento hello. server di bilanciamento toomanually internazionali, utilizzare hello alla procedura seguente:

    1. Connettere il cluster di HDInsight toohello tramite SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Utilizzare hello seguendo la shell di HBase toostart hello:

            hbase shell

    3. Una volta caricate hello shell di HBase, utilizzare hello seguenti server a livello regionale toomanually saldo hello:

            balancer

* **Storm**: al termine dell'operazione di ridimensionamento, ribilanciare qualsiasi topologia Storm in esecuzione. Ribilanciamento consente hello topologia tooreadjust parallelismo impostazioni nuovo numero di nodi nel cluster hello hello. toorebalance le topologie in esecuzione, utilizzare uno dei hello le opzioni seguenti:

    * **SSH**: toohello server di connessione e comando che segue hello utilizzare toorebalance una topologia:

            storm rebalance TOPOLOGYNAME

        È anche possibile specificare gli hint parallelismo hello toooverride parametri originariamente forniti da topologia hello. Ad esempio, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` la riconfigurazione hello i processi di lavoro di topologia too5 3 executor per il componente blu beccuccio hello ed 10 executor per il componente giallo fulmine hello.

    * **Interfaccia utente di Storm**: toorebalance i passaggi seguenti hello utilizzare una topologia con hello Storm UI.

        1. Aprire **https://CLUSTERNAME.azurehdinsight.net/stormui** nel web browser, dove CLUSTERNAME è il nome di hello del cluster Storm. Se richiesto, immettere nome amministratore (amministrazione) del cluster HDInsight hello e la password specificata durante la creazione di cluster hello.
        2. Selezionare la topologia di hello si desidera toorebalance, quindi seleziona hello **ribilanciare** pulsante. Immettere un intervallo di hello prima di eseguita l'operazione di ribilanciamento hello.

Per informazioni specifiche sul ridimensionamento del cluster HDInsight, vedere:

* [Gestire i cluster Hadoop in HDInsight con hello portale di Azure](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Gestire cluster Hadoop in HDInsight usando Azure PowerShell](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Come si installa Hue (o un altro componente Hadoop)?

HDInsight è un servizio gestito. Se Azure rileva un problema con il cluster hello, può eliminare hello in mancanza di nodo e creare un nodo tooreplace è. Se si installa manualmente operazioni nel cluster hello, essi non vengono mantenuti quando si esegue questa operazione. Usare invece le [azioni script di HDInsight](hdinsight-hadoop-customize-cluster.md). Un'azione di script può essere utilizzato toomake hello dopo le modifiche:

* Installare e configurare un servizio o un sito Web, ad esempio Spark o Hue.
* Installare e configurare un componente che richiede modifiche alla configurazione su più nodi nel cluster hello. ad esempio una variabile di ambiente necessaria, la creazione di una directory di registrazione o la creazione di un file di configurazione.

Le azioni script sono script Bash. script Hello eseguire durante il provisioning del cluster e può essere tooinstall utilizzato e configurare i componenti aggiuntivi nel cluster di hello. Gli script di esempio sono disponibili per l'installazione di hello seguenti componenti:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph,](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Per informazioni su come sviluppare azioni script personalizzate, vedere [Sviluppo di azioni script con HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>File con estensione jar

Alcune tecnologie Hadoop vengono fornite in file con estensione jar indipendenti contenenti funzioni usate come parte di un processo MapReduce o dall'interno di Pig o Hive. Mentre questi può essere installati usando le azioni di Script, spesso non richiedono alcuna installazione e possono essere caricati toohello cluster dopo il provisioning e utilizzata direttamente. Se si desidera componente hello che toomake resta ricreazione del cluster di hello, è possibile archiviare file jar hello in spazio di archiviazione di hello predefinito per il cluster (WASB o ADL).

Ad esempio, se si desidera toouse hello versione [DataFu](http://datafu.incubator.apache.org/), è possibile scaricare un file jar contenente il progetto hello e caricarlo cluster HDInsight toohello. Seguire la documentazione di hello DataFu sulla toouse dalla Pig o Hive.

> [!IMPORTANT]
> Alcuni componenti che sono file jar autonomo sono disponibili con HDInsight, ma non sono presenti nel percorso di hello. Se si sta cercando un componente specifico, è possibile utilizzare per tale hello seguire toosearch sul cluster:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Questo comando restituisce il percorso di hello di qualsiasi file jar corrispondenti.

toouse una versione diversa di un componente, caricamento hello versione è necessario e utilizzarla nei processi utente.

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto di Microsoft consente tooisolate e risolvere i problemi correlati toothese componenti.
>
> I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Per i progetti Apache sono anche disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/) e [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Passaggi successivi

* [Eseguire la migrazione da HDInsight basati su Windows basato su tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare processi MapReduce con HDInsight](hdinsight-use-mapreduce.md)
