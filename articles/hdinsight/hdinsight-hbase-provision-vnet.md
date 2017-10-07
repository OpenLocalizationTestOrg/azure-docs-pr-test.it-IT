---
title: aaaCreate HBase cluster in una rete virtuale - Azure | Documenti Microsoft
description: Introduzione all'uso di HBase in Azure HDInsight. Informazioni su come cluster di HDInsight HBase toocreate nella rete virtuale di Azure.
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Creare cluster HBase su HDInsight nella rete virtuale di Azure
Informazioni su come toocreate HBase di HDInsight di Azure cluster in un [rete virtuale di Azure][1].

Con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare direttamente con HBase. Hello vantaggi includono:

* Connettività diretta di hello web applicazione toohello i nodi del cluster HBase di hello, che consente la comunicazione tramite RPC HBase Java chiamare le API (RPC).
* Miglioramento delle prestazioni, poiché il traffico non deve attraversare più gateway e servizi di bilanciamento del carico.
* Hello possibilità tooprocess informazioni riservate in modo più sicuro senza esporre un endpoint pubblico.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Workstation con Azure PowerShell**. Vedere [Installare e usare Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Creare cluster HBase nella rete virtuale
In questa sezione si crea un cluster HBase basati su Linux con account di archiviazione Azure dipendenti di hello in una rete virtuale di Azure utilizzando un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Per altri metodi di creazione del cluster e informazioni sulle impostazioni di hello, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md). Per ulteriori informazioni sull'utilizzo di un toocreate modello Hadoop cluster in HDInsight, vedere [cluster creare Hadoop in HDInsight mediante modelli di gestione risorse di Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Alcune proprietà sono hardcoded nel modello di hello. ad esempio:
>
> * **Location**: Stati Uniti orientali 2
> * **Versione del cluster**: 3.5
> * **Cluster worker node count**: 2
> * **Default storage account**: stringa univoca
> * **Virtual network name**: &lt;Nome cluster&gt;-vnet
> * **Virtual network address space**: 10.0.0.0/16
> * **Subnet name**: subnet1
> * **Subnet address range**: 10.0.0.0/24
>
> &lt;Nome del cluster > viene sostituito con il nome di cluster hello è fornire quando si utilizza il modello di hello.
>
>

1. Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure. modello Hello nella [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Da hello **distribuzione personalizzata** pannello immettere hello le proprietà seguenti:

   * **Sottoscrizione**: selezionare un cluster di HDInsight hello toocreate sottoscrizione di Azure usata, hello dipendenti account di archiviazione e rete virtuale di Azure hello.
   * **Gruppo di risorse**: selezionare **Crea nuovo** e assegnare un nome al nuovo gruppo di risorse.
   * **Percorso**: selezionare un percorso per il gruppo di risorse hello.
   * **ClusterName**: immettere un nome per toobe di cluster Hadoop hello creato.
   * **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.
   * **Nome utente SSH e password**: nome utente predefinito hello **sshuser**.  È possibile rinominarlo.
   * **Accetto le condizioni di hello indicate in precedenza toohello**: (Select)
3. Fare clic su **Acquista**. Dovrà trascorrere circa toocreate circa 20 minuti di un cluster. Una volta creato il cluster hello, è possibile fare clic su Pannello cluster hello in tooopen portale hello è.

Dopo aver completato l'esercitazione hello, è consigliabile cluster hello toodelete. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato. Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso. Per istruzioni hello di eliminazione di un cluster, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin utilizzo con il nuovo cluster HBase, è possibile utilizzare procedure hello in [informazioni introduttive sull'utilizzo di HBase con Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Connettere il cluster di HBase toohello utilizzando le API di HBase Java RPC
1. Creazione di un'infrastruttura come servizio (IaaS) macchina virtuale nella stessa rete virtuale hello e hello stessa subnet. Per le istruzioni su come creare una nuova macchina virtuale IaaS, vedere [Creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Quando hello procedura riportata in questo documento, è necessario utilizzare i seguenti valori per la configurazione di rete hello hello:

   * **Virtual network**: &lt;Nome cluster&gt;-vnet
   * **Subnet**: subnet1

   > [!IMPORTANT]
   > Sostituire &lt;nome Cluster > con nome hello utilizzato per la creazione del cluster HDInsight hello nei passaggi precedenti.
   >
   >

   Utilizzando questi valori, hello macchina virtuale viene inserita in hello stessa subnet del cluster HDInsight hello e rete virtuale. Questa configurazione consente loro toodirectly comunicare tra loro. È un modo toocreate un cluster di HDInsight con un nodo del bordo vuoto. nodo del bordo Hello può essere cluster hello toomanage utilizzato.  Per altre informazioni, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).

2. Quando si utilizza un tooHBase tooconnect di applicazione Java in modalità remota, è necessario utilizzare il nome di dominio completo hello (FQDN). toodetermine, è necessario ottenere suffisso DNS specifico della connessione di hello dei cluster HBase hello. toodo, che è possibile utilizzare uno dei seguenti metodi hello:

   * Utilizzare un toomake browser Web chiamata Ambari:

     Sfoglia toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / ospita? minimal_response = true. Verrà utilizzato un file JSON con i suffissi DNS hello.
   * Usare Ambari hello:

     1. Sfoglia troppo https://&lt;ClusterName >. cluster>.azurehdinsight.NET.
     2. Fare clic su **host** menu principale di hello.
   * Utilizzare le chiamate REST toomake Curl:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Trovare la voce "host_name" hello in hello restituiti i dati di JavaScript Object Notation (JSON). Contiene hello FQDN per i nodi nel cluster hello hello. ad esempio:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     Hello di hello dominio nome che inizia con il nome del cluster hello è il suffisso DNS hello. Ad esempio, mycluster.b1.cloudapp.net.
   * Uso di Azure PowerShell

     Hello utilizzare seguente hello tooregister script di PowerShell Azure **Get ClusterDetail** funzione, che può essere utilizzato tooreturn hello DNS suffisso:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Dopo l'esecuzione di uno script Azure PowerShell hello, utilizzare hello comando che segue il suffisso DNS hello tooreturn utilizzando hello **Get ClusterDetail** (funzione). Quando si usa il comando, specificare il nome del cluster HBase di HDInsight e il nome e la password dell'amministratore.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Questo comando restituisce il suffisso DNS hello. Ad esempio, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify che hello macchina virtuale possono comunicare con hello cluster HBase, utilizzare il comando hello `ping headnode0.<dns suffix>` dalla macchina virtuale hello. Ad esempio, eseguire il ping di headnode0.mycluster.b1.cloudapp.net

toouse queste informazioni in un'applicazione Java, è possibile seguire i passaggi di hello in [utilizzare Maven toobuild Java le applicazioni che utilizzano HBase di HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate un'applicazione. un'applicazione hello toohave connettere tooa remoto HBase server, modificare hello **hbase-Site.XML** file in questo hello toouse esempio FQDN per Zookeeper. ad esempio:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Per ulteriori informazioni sulla risoluzione dei nomi in reti virtuali di Azure, compresa la modalità toouse il proprio server DNS, vedere [risoluzione DNS (Name)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come un cluster HBase toocreate. toolearn informazioni, vedere:

* [Introduzione all'uso di HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md)
* [Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Introduzione all'uso di HBase con Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Analizzare i sentimenti Twitter con HBase in HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Panoramica di Rete virtuale][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Dettagli di provisioning per il nuovo cluster di HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilizzare l'azione Script toocustomize un cluster HBase"

[azure-preview-portal]: https://portal.azure.com
