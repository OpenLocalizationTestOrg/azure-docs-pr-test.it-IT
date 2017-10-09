---
title: il programma di installazione aaaCluster per Hadoop, Spark, Kafka, HBase o R Server - HDInsight di Azure | Documenti Microsoft
description: Configurare il cluster Hadoop, Kafka, Spark, HBase, R Server o Storm per HDInsight da un browser, hello CLI di Azure, Azure PowerShell, REST o SDK.
keywords: impostazione del cluster hadoop, impostazione del cluster kafka, impostazione del cluster spark, caratteristiche del cluster in hadoop
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Configurare i cluster di HDInsight con Hadoop, Spark, Kafka e altro ancora

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Informazioni su come tooset e configurare i cluster di HDInsight Hadoop, Spark, Kafka, Hive interattivo, HBase, R Server o Storm. Inoltre, informazioni su come toocustomize cluster e aggiungere protezione unendo tooa dominio.

Un cluster Hadoop è costituito da alcune macchine virtuali (nodi) che vengono usate per l'elaborazione distribuita di attività. HDInsight di Azure gestisce i dettagli di implementazione dell'installazione e configurazione dei singoli nodi, in modo da avere solo le informazioni di configurazione generale di tooprovide. 

> [!IMPORTANT]
>La fatturazione di cluster HDInsight inizia dopo che un cluster viene creato e si arresta quando viene eliminato il cluster hello. La fatturazione avviene con tariffa oraria, perciò si deve sempre eliminare il cluster in uso quando non lo si usa più. Informazioni su come troppo[eliminare un cluster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Metodi di installazione del cluster
Hello nella tabella seguente sono illustrati hello diversi metodi che è possibile utilizzare tooset di un cluster HDInsight.

| Cluster creati con | Web browser | Riga di comando | API REST | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Portale di Azure](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Data factory di Azure](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Interfaccia della riga di comando di Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Modelli di Gestione risorse di Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Creazione rapida: configurazione base del cluster
Questo articolo vengono illustrati il programma di installazione di hello [portale di Azure](https://portal.azure.com), in cui è possibile creare un cluster HDInsight mediante *creazione rapida* o *personalizzato*. 

Seguire le istruzioni hello schermata toodo un programma di installazione del cluster di base. Di seguito sono riportati dettagli relativi a:

* [Nome del gruppo di risorse](#resource-group-name)
* [Tipi di cluster e configurazione](#cluster-types) 
* [Account di accesso del cluster e nome utente SSH](#cluster-login-and-ssh-username)
* [Posizione](#location)

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere [Ritiro di HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Nome del gruppo di risorse 

[Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) consente di lavorare con le risorse di hello dell'applicazione come tooas un gruppo, a cui si fa riferimento un gruppo di risorse di Azure. È possibile distribuire, aggiornare, monitorare o eliminare tutte le risorse di hello per l'applicazione in una singola operazione coordinata.

## <a name="cluster-types"></a> Tipi di cluster e configurazione
Azure HDInsight offre attualmente seguente hello cluster tipi, ognuno con un set di componenti tooprovide alcune funzionalità.

> [!IMPORTANT]
> I cluster HDInsight sono disponibili i vari tipi, ognuno per un carico di lavoro o una tecnologia specifici. Non è toocreate alcun metodo supportato per un cluster che combina più tipi, ad esempio Storm e HBase in un cluster. Se la soluzione richiede tecnologie che vengono distribuite tra più tipi di cluster HDInsight, un [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network) possono connettersi a tipi di cluster hello necessario. 
>
>

| Tipo di cluster | Funzionalità |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Query batch e analisi dei dati archiviati |
| [HBase](hdinsight-hbase-overview.md) |Elaborazione di grandi quantità di dati NoSQL senza schema |
| [Storm](hdinsight-storm-overview.md) |Elaborazione di eventi in tempo reale |
| [Spark](hdinsight-apache-spark-overview.md) |Elaborazione in memoria, query interattive, elaborazione di flussi di micro batch |
| [Kafka (anteprima)](hdinsight-apache-kafka-introduction.md) | Una piattaforma di streaming distribuita che può essere utilizzati toobuild in tempo reale streaming pipeline di dati e applicazioni |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Ampia gamma di statistiche di Big Data, modellazione predittiva e funzionalità di Machine Learning |
| [Interactive Hive (anteprima)](hdinsight-hadoop-use-interactive-hive.md) |Caching in memoria per query Hive interattive e più rapide |

### <a name="number-of-nodes-for-each-cluster-type"></a>Numero di nodi per ogni tipo di cluster
Ogni tipo di cluster ha il proprio numero di nodi, una terminologia specifica per i nodi e dimensioni predefinite delle macchine virtuali. In hello nella tabella seguente, il numero di hello di nodi per ogni tipo di nodo è racchiuso tra parentesi.

| Tipo | Nodi | Diagramma |
| --- | --- | --- |
| Hadoop |Nodo head (2), nodo dati (1+) |![Nodi del cluster HDInsight Hadoop](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Server head (2), server di area (1+), nodo master/ZooKeeper (3) |![Nodi del cluster HDInsight HBase](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nodo Nimbus (2), server supervisore (1+), nodo ZooKeeper (3) |![Nodi del cluster HDInsight Storm](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Nodo head (2), nodo Worker (1+), nodo ZooKeeper (3), gratuito per le macchine virtuali ZooKeeper con dimensioni A1 |![Nodi del cluster HDInsight Spark](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Per ulteriori informazioni, vedere [nodo dimensioni di macchina virtuale e di configurazione per i cluster predefinite](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) in "Quali sono i componenti di hello Hadoop e le versioni in HDInsight?"

### <a name="hdinsight-version"></a>Versione HDInsight
Scegliere la versione di hello di HDInsight per questo cluster. Per altre informazioni, vedere [Versioni supportate di HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Livello cluster: livelli di servizio HDInsight

HDInsight di Azure fornisce offerte di cloud hello big data nei due livelli di servizio: Standard e Premium.  Per altre informazioni, vedere [HDInsight Standard e HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Hello seguente schermata mostra hello informazioni sul portale di Azure per la scelta di tipi di cluster.

![Configurazione di HDInsight Premium](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Account di accesso del cluster e nome utente SSH
Con i cluster HDInsight è possibile configurare due account utente durante la creazione del cluster:

* Utente HTTP: nome utente predefinito di hello è *admin*. Usa configurazione di base hello in hello portale di Azure. In alcuni casi, viene chiamato "utente cluster".
* Utente SSH (Linux cluster): tooconnect utilizzati toohello cluster tramite SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Posizione (regioni) per cluster e risorse di archiviazione

Non è necessario in modo esplicito di percorso di cluster hello toospecify: hello cluster è in hello stessa posizione di archiviazione predefinita hello. Per un elenco delle aree geografiche supportate, fare clic su hello **area** elenco a discesa in [prezzi di HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Endpoint di archiviazione per i cluster

Anche se un'installazione locale di Hadoop, hello Hadoop Distributed File System (HDFS) viene utilizzato per l'archiviazione nel cluster hello, in hello cloud di utilizzare gli endpoint di archiviazione connesso toocluster. I cluster HDInsight usano [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) o [i BLOB in Archiviazione di Azure](hdinsight-hadoop-use-blob-storage.md). Tramite l'archiviazione di Azure o archivio Data Lake, significa che è possibile eliminare il cluster di HDInsight hello usato per il calcolo, pur mantenendo i dati. 

> [!WARNING]
> Non è possibile utilizzare un account di archiviazione aggiuntivi in una posizione diversa dal cluster HDInsight hello.

Durante la configurazione per l'endpoint di archiviazione predefinito hello si specifica un contenitore blob di un account di archiviazione di Azure o un archivio Data Lake. Hello spazio di archiviazione predefinito contiene applicazioni e sistema i log. Facoltativamente, è possibile specificare altri account di archiviazione di Azure collegato e gli account archivio Data Lake hello cluster possono accedere. cluster HDInsight Hello e archiviazione dipendenti hello devono trovarsi nello hello nello stesso percorso di Azure.

![Impostazioni di archiviazione del cluster: endpoint di archiviazione compatibili con HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Metastore facoltativi
È possibile creare dei metastore Hive o Oozie facoltativi. Tuttavia, non tutti i tipi di cluster supportano i metastore e Azure SQL Data Warehouse non è compatibile con i metastore. 

> [!IMPORTANT]
> Quando si crea un metastore personalizzato, non utilizzare trattini, trattini o spazi nel nome del database hello. Ciò può provocare hello cluster creazione processo toofail.

### <a name="use-hiveoozie-metastore"></a>Metastore Hive

Se si desidera tooretain tabelle Hive dopo l'eliminazione di un cluster HDInsight, utilizzare un metastore personalizzato. È quindi possibile collegare i cluster di HDInsight tooanother metastore hello.

Un metastore HDInsight creato per una versione del cluster HDInsight non può essere condiviso in versioni diverse del cluster HDInsight. Per un elenco di versioni di HDInsight, vedere [Versioni supportate di HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Metastore Oozie

tooincrease prestazioni quando si utilizza Oozie, utilizzare un metastore personalizzato. Un metastore può anche fornire accesso ai dati del processo tooOozie dopo l'eliminazione del cluster. 

> [!IMPORTANT]
> Non è possibile riutilizzare un metastore Oozie personalizzato. toouse un metastore Oozie personalizzato, è necessario fornire un Database SQL di Azure vuoto durante la creazione di cluster di HDInsight hello.

## <a name="configure-cluster-size"></a>Configurare le dimensioni del cluster

Verrà addebitato per l'utilizzo per nodo, purché sia presente il cluster hello. La fatturazione inizia quando viene creato un cluster e si arresta quando viene eliminato il cluster hello. I cluster non possono essere deallocati o messi in attesa.

costo Hello del cluster HDInsight è determinato dal numero di hello di nodi e le dimensioni delle macchine virtuali hello per i nodi di hello. 

Diversi tipi di cluster hanno diversi tipi, numeri e dimensioni di nodi:
* Tipo predefinito di cluster Hadoop: 
    * Due *nodi head*  
    * Quattro *nodi dati*
* Tipo predefinito di cluster Storm: 
    * Due *nodi Nimbus*
    * Tre *nodi ZooKeeper*
    * Quattro *nodi Supervisor* 

Se si sta solo provando HDInsight, è consigliabile usare un nodo di dati. Per altre informazioni sui prezzi di HDInsight, vedere [Prezzi di HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> limite delle dimensioni del cluster Hello varia tra le sottoscrizioni di Azure. Contatto [supporto per la fatturazione Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) limite hello tooincrease.
>

Quando si utilizza hello tooconfigure portale Azure hello cluster, dimensioni nodo hello sono disponibile tramite hello **piani tariffari del nodo** blade. Nel portale di hello, è inoltre possibile visualizzare hello costo associato con dimensioni di un nodo diverso hello. 

![Dimensioni dei nodi delle VM di HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Dimensioni delle macchine virtuali 
Quando si distribuiscono i cluster, scegliere le risorse di calcolo basate sulla soluzione hello Prevedi toodeploy. macchine virtuali seguenti Hello vengono utilizzate per i cluster HDInsight:
* Macchine virtuali serie A e D1-4: [Dimensioni delle macchine virtuali Linux per l'uso generico](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* Macchine virtuali serie D11-14: [Dimensioni ottimizzate per la memoria delle macchine virtuali Linux](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind il valore è necessario utilizzare toospecify una dimensione di macchina virtuale durante la creazione di un cluster mediante hello SDK diversi o quando si utilizza Azure PowerShell, vedere [VM di dimensioni toouse per i cluster HDInsight](../cloud-services/cloud-services-sizes-specs.md#size-tables). In questo articolo collegato, utilizzare il valore di hello in hello **dimensioni** colonna delle tabelle di hello.

> [!IMPORTANT]
> Se si prevedono più di 32 nodi di lavoro in un cluster, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.
>
>

Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md). Per informazioni sui prezzi di hello diverse dimensioni, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Personalizzare la configurazione del cluster
Compilazioni di programma di installazione di cluster personalizzato su hello rapida creare le impostazioni e aggiunge hello le opzioni seguenti:
- [Applicazioni HDInsight](#hdinsight-applications)
- [Dimensione del cluster](#cluster-size)
- Impostazioni avanzate
  - [Azioni script](#customize-clusters-using-script-action)
  - [Rete virtuale](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Installare applicazioni HDInsight in cluster

Un'applicazione HDInsight è un'applicazione che gli utenti possono installare in un cluster HDInsight basato su Linux. È possibile usare applicazioni fornite da Microsoft o terze parti o sviluppate in modo indipendente. Per altre informazioni, vedere [Installare applicazioni Hadoop di terze parti in Azure HDInsight](hdinsight-apps-install-applications.md).

La maggior parte delle applicazioni di HDInsight hello vengono installata in un nodo del bordo vuoto.  Un nodo del bordo vuoto è una macchina virtuale Linux con hello stessi strumenti client installato e configurato come nodo head hello. È possibile utilizzare il nodo di edge hello per l'accesso a cluster hello, il testing delle applicazioni client e l'hosting di applicazioni client. Per altre informazioni, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Impostazioni avanzate: azioni Script

L'uso di script durante la creazione consente di installare componenti aggiuntivi o personalizzare la configurazione di un cluster. Tali script vengono richiamati mediante **genera Script azione**, che è un'opzione di configurazione che può essere usata da hello portale di Azure, i cmdlet di HDInsight Windows PowerShell o hello HDInsight .NET SDK. Per altre informazioni, vedere [Personalizzare cluster HDInsight mediante le azioni script](hdinsight-hadoop-customize-cluster-linux.md).

Alcuni componenti di Java native, ad esempio Mahout e a catena, possono essere eseguiti nel cluster hello come file Java Archive (JAR). I file JAR possono essere distribuita tooAzure archiviazione e inviate tooHDInsight cluster con i meccanismi di invio processi Hadoop. Per altre informazioni, vedere [Inviare processi Hadoop a livello di codice](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Se si presentano problemi di distribuzione di cluster di tooHDInsight file JAR o chiamata file JAR nel cluster HDInsight, contattare [supporto Microsoft](https://azure.microsoft.com/support/options/).
>
> Cascading non è supportato da HDInsight, quindi in caso di problemi non è possibile rivolgersi al Supporto Microsoft. Per gli elenchi di componenti supportati, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight](hdinsight-component-versioning.md).
>
>

In alcuni casi, si desidera hello tooconfigure i seguenti file di configurazione durante il processo di creazione di hello:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Per altre informazioni, vedere [Personalizzare cluster HDInsight tramite Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Impostazioni avanzate: estendere i cluster con una rete virtuale
Se la soluzione richiede tecnologie che vengono distribuite tra più tipi di cluster HDInsight, un [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network) possono connettersi a tipi di cluster hello necessario. Questa configurazione consente ai cluster hello e qualsiasi codice in cui si distribuisce toothem, toodirectly comunicare tra loro.

Per altre informazioni sull'uso di una rete virtuale di Azure con HDInsight, vedere [Estendere HDInsight con le reti virtuali di Azure](hdinsight-extend-hadoop-virtual-network.md).

Per un esempio dell'uso di due tipi di cluster in una rete virtuale di Azure, vedere [Analizzare i dati del sensore con Storm e HBase](hdinsight-storm-sensor-data-analysis.md). Per ulteriori informazioni sull'uso di HDInsight con una rete virtuale, inclusi i requisiti di configurazione specifiche per la rete virtuale hello, vedere [HDInsight estendere le funzionalità tramite la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Risolvere i problemi relativi al controllo di accesso

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi

- [Quali sono i cluster Hadoop HDInsight ed ecosistema Hadoop hello?](hdinsight-hadoop-introduction.md)
- [Introduzione all'uso di Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Lavorare da un computer Windows in Hadoop su HDInsight](hdinsight-hadoop-windows-tools.md)
