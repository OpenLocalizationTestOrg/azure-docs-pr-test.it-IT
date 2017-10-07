---
title: la replica cluster HBase di aaaConfigure nelle reti virtuali - Azure | Documenti Microsoft
description: "Informazioni su come la replica di HBase tooconfigure per il bilanciamento del carico, la disponibilità elevata, senza tempi di inattività migrazione o aggiornamento da una tooanother versione di HDInsight e il ripristino di emergenza."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Configurare la replica di cluster HBase nelle reti virtuali

Informazioni su come tooconfigure HBase replica all'interno di una rete virtuale (VNet) o tra due reti virtuali.

La replica di cluster usa una metodologia con push dell'origine. Un cluster HBase può essere un'origine o una destinazione o può soddisfare entrambi i ruoli in una sola volta. La replica è asincrona e obiettivo hello di replica è coerenza finale. Quando origine hello riceve una famiglia di colonna tooa Modifica abilitata la replica, tale modifica è propagata tooall i cluster di destinazione. Quando i dati vengono replicati da un cluster tooanother, il cluster di origine hello e tutti i cluster che è sono già utilizzata da dati hello vengono rilevati tooprevent cicli di replica.

In questa esercitazione si configurerà una replica origine-destinazione. Per altre topologie di cluster, vedere la [guida di riferimento relativa a Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

Casi di utilizzo della replica di HBase per una singola rete virtuale:

* Bilanciamento del carico, ad esempio, l'esecuzione di analisi o i processi MapReduce nel cluster di destinazione hello e l'inserimento di dati nel cluster di origine hello
* Disponibilità elevata
* Migrazione dei dati da un tooanother di cluster HBase
* L'aggiornamento di un cluster Azure HDInsight da una versione tooanother

Casi di utilizzo della replica di HBase per due reti virtuali:

* Ripristino di emergenza
* Bilanciamento del carico e partizionamento di un'applicazione hello
* Disponibilità elevata

È possibile replicare i cluster tramite gli script [Azione script](hdinsight-hadoop-customize-cluster-linux.md) disponibili in [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Configurare ambienti hello

Sono disponibili tre opzioni di configurazione:

- Due cluster HBase in una rete virtuale di Azure
- Hello di due cluster HBase in due reti virtuali diverse nella stessa area geografica
- Due cluster HBase in due reti virtuali differenti in due aree differenti (replica geografica)

toomake, ambienti di hello tooconfigure più semplici, sono stati creati alcuni [modelli di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Se si preferiscono ambienti hello tooconfigure utilizzando altri metodi, vedere:

- [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Creare cluster HBase nella rete virtuale di Azure](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Configurare una rete virtuale

Fare clic su hello seguente immagine toocreate due HBase cluster in hello stessa rete virtuale. modello Hello viene archiviato [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Configurare due reti virtuali in hello stessa area geografica

Fare clic su hello seguente immagine toocreate due reti virtuali con rete virtuale per il peering e due cluster HBase in hello stessa area. modello Hello viene archiviato [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Questo scenario richiede il [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md). modello di Hello consente peering reti virtuali.   

La replica di HBase utilizza indirizzi IP delle macchine virtuali ZooKeeper hello. È necessario configurare gli indirizzi IP statici per i nodi di HBase ZooKeeper destinazione hello.

**indirizzi IP statici tooconfigure**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra hello **gruppi di risorse**.
3. Scegliere il gruppo di risorse contenente cluster HBase di destinazione hello. Si tratta di gruppo di risorse hello specificato quando si utilizza l'ambiente di hello Gestione risorse modello toocreate hello. È possibile utilizzare hello filtro toonarrow elenco hello verso il basso. È possibile visualizzare un elenco di risorse che contiene due reti virtuali hello.
4. Fare clic su rete virtuale hello contenente cluster HBase di destinazione hello. Ad esempio, fare clic su **xxxx-vnet2**. Vengono visualizzati tre dispositivi i cui nomi iniziano con **nic-zookeepermode -**. Tali dispositivi sono le macchine virtuali ZooKeeper hello tre.
5. Fare clic su una delle macchine virtuali ZooKeeper hello.
6. Fare clic su **Configurazioni IP**.
7. Fare clic su **ipConfig1** dall'elenco di hello.
8. Fare clic su **statico**e annotare l'indirizzo IP effettivo hello. Quando si esegue la replica di tooenable hello script azione, è necessario l'indirizzo IP hello.

  ![Replica di HBase in HDInsight - Indirizzo IP statico di ZooKeeper](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Ripetere il passaggio 6 tooset hello indirizzo IP per hello altri due nodi ZooKeeper.

Scenario di rete virtuale cross hello, è necessario utilizzare hello **- ip** passare quando si chiama hello **hdi_enable_replication.sh** script azione.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Configurare due reti virtuali in due aree differenti

Fare clic su hello seguente immagine toocreate due reti virtuali in due aree diverse. modello Hello viene archiviato in un contenitore Blob di Azure pubblico.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Creare un gateway VPN tra due reti virtuali hello. Per istruzioni, vedere [Creare una rete virtuale con una connessione da sito a sito](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

La replica di HBase utilizza indirizzi IP delle macchine virtuali ZooKeeper hello. È necessario configurare gli indirizzi IP statici per i nodi di HBase ZooKeeper destinazione hello. indirizzo IP statico tooconfigure, nella sezione hello "Configura due reti virtuali in hello stessa area" in questo articolo.

Scenario di rete virtuale cross hello, è necessario utilizzare hello **- ip** passare quando si chiama hello **hdi_enable_replication.sh** script azione.

## <a name="load-test-data"></a>Dati del test di carico

Quando si esegue la replica di un cluster, è necessario specificare tooreplicate tabelle hello. In questa sezione si caricherà alcuni dati in cluster di origine hello. Nella sezione successiva hello, verrà abilitata la replica tra due cluster hello.

Seguire le istruzioni hello [HBase esercitazione: Introduzione all'uso di Apache HBase con basati su Linux, Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **contatti** tabella e inserire alcuni dati nella tabella hello.

## <a name="enable-replication"></a>Abilitare la replica

Hello alla procedura seguente viene illustrato come toocall hello script dell'azione script da hello portale di Azure. Per l'esecuzione di un'azione di script tramite Azure PowerShell e hello Azure interfaccia della riga di comando (CLI), vedere [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md).

**replica di HBase tooenable da hello portale di Azure**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Aprire cluster HBase di origine hello.
3. Scegliere dal menu cluster hello **azioni Script**.
4. Fare clic su **inviare nuove** dalla parte superiore di hello del pannello hello.
5. Selezionare o immettere hello le seguenti informazioni:

  - **Nome**: immettere **Abilitazione replica**.
  - **URL dello script Bash**: immettere **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **Intestazione**: Selezionata. Deselezionare hello altri tipi di nodo.
  - **I parametri**: esempio hello parametri abilitare la replica per tutte le tabelle esistenti hello di esempio e copiare tutti i dati di hello dal cluster di destinazione toohello hello origine cluster:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Fare clic su **Crea**. script Hello può richiedere del tempo, soprattutto quando argomento - copydata hello è utilizzata.

Argomenti obbligatori:

|Nome|Descrizione|
|----|-----------|
|-s, --src-cluster | Specificare il nome DNS hello dei cluster HBase di origine hello. Ad esempio: -s hbsrccluster, --src-cluster=hbsrccluster |
|-d, - dst-cluster | Specificare il nome DNS hello della destinazione hello cluster HBase (replica). Ad esempio: -s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | Specificare la password di amministratore di hello per Ambari cluster HBase di origine hello. |
|-dp, --dst-ambari-password | Specificare la password di amministratore di hello per Ambari nel cluster HBase di destinazione hello.|

Argomenti facoltativi:

|Nome|Descrizione|
|----|-----------|
|-su, --src-ambari-user | Specificare nome utente amministratore hello per Ambari cluster HBase di origine hello. valore predefinito di Hello è **admin**. |
|-du, --dst-ambari-user | Specificare nome utente amministratore hello per Ambari nel cluster HBase di destinazione hello. valore predefinito di Hello è **admin**. |
|-t, --table-list | Specificare hello toobe di tabelle replicate. Ad esempio: --table-list="table1;table2;table3". Se non si specificano tabelle, vengono replicate tutte le tabelle HBase esistenti.|
|-m, --machine | Specificare il nodo head hello in hello script verranno eseguiti. il valore di Hello è hn1 o hn0. Poiché hn0 è usato con maggiore frequenza, è consigliabile usare hn1. Utilizzare questa opzione quando si esegue uno script hello $0 come un'azione di script dal portale di HDInsight hello o Azure PowerShell.|
|-ip | Questo argomento è obbligatorio quando si vuole abilitare la replica tra due reti virtuali. Questo argomento viene utilizzato come un commutatore toouse hello statico gli indirizzi IP di ZooKeeper nodi dal cluster di replica anziché nomi di dominio completi. Hello statico IP necessario toobe preconfigurato prima di abilitare la replica. |
|-cp, -copydata | Abilitare la migrazione di hello dei dati esistenti nelle tabelle di hello in cui la replica è abilitata. |
|-rpm, -replicate-phoenix-meta | Abilita la replica sulle tabelle di sistema Phoenix. <br><br>*Questa opzione deve essere usata con attenzione.* È consigliabile ricreare le tabelle di Phoenix nei cluster di replica prima di usare questo script. |
|-h, --help | Visualizza le informazioni sull'utilizzo. |

Hello sezione print_usage() di hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fornisce una spiegazione dettagliata dei parametri.

Al termine dell'azione script hello correttamente distribuito, è possibile utilizzare cluster HBase SSH tooconnect toohello destinazione e verificare dati hello sono stati replicati.

### <a name="replication-scenarios"></a>Scenari di replica

Hello elenco seguente mostra alcuni casi di utilizzo generale e le relative impostazioni di parametro:

- **Abilitare la replica in tutte le tabelle tra cluster hello due**. Questo scenario non richiede copia hello la migrazione dei dati esistenti nelle tabelle di hello e Usa tabelle Phoenix. Utilizzare hello seguenti parametri:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Abilitare la replica su tabelle specifiche**. Utilizzare hello seguendo replica tooenable parametri table1, table2 e TABELLA3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Abilitare la replica su tabelle specifiche e copiare i dati esistenti hello**. Utilizzare hello seguendo replica tooenable parametri table1, table2 e TABELLA3:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Abilitare la replica in tutte le tabelle con la replica dei metadati phoenix da origine toodestination**. La replica dei metadati di Phoenix non è perfetta e deve essere usata con cautela.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Copia e migrazione dei dati

Sono disponibili due script azione script distinti per la copia o la migrazione dei dati dopo aver abilitato la replica:

- [Script per tabelle di piccole dimensioni](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (pochi gigabyte nella copia di dimensione e complessiva è toofinish previsto in meno di un'ora)

- [Script per tabelle di grandi dimensioni](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (previsto più di un'ora toocopy tootake)

È possibile seguire hello stessa procedura nel [abilitare la replica](#enable-replication) toocall hello script azione hello seguenti parametri:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Hello sezione print_usage() di hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fornisce una descrizione dettagliata dei parametri.

### <a name="scenarios"></a>Scenari

- **Copiare tabelle specifiche (test1, test2 e test3) per tutte le righe modificate finora (timestamp corrente)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  oppure

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Copiare tabelle specifiche con un intervallo di tempo specificato**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Disabilitare la replica

replica toodisable, utilizzare un altro script dell'azione script si trova in [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). È possibile seguire hello stessa procedura nel [abilitare la replica](#enable-replication) toocall hello script azione hello seguenti parametri:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Hello sezione print_usage() di hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fornisce una spiegazione dettagliata dei parametri.

### <a name="scenarios"></a>Scenari

- **Disabilitare la replica in tutte le tabelle**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  oppure

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Disabilitare la replica in tabelle specifiche (table1, table2 e table3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si è appreso come la replica di HBase tooconfigure tra due Data Center. toolearn ulteriori informazioni su HDInsight e HBase, vedere:

* [Introduzione ad Apache HBase in HDInsight][hdinsight-hbase-get-started]
* [Panoramica su HBase di HDInsight][hdinsight-hbase-overview]
* [Creare cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]
* [Analisi dei sentimenti Twitter in tempo reale con HBase][hdinsight-hbase-twitter-sentiment]
* [Analisi dei dati dei sensori con Storm e HBase in HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
