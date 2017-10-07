---
title: cluster aaaManage Hadoop in HDInsight con PowerShell - Azure | Documenti Microsoft
description: "Informazioni su come attività amministrative tooperform per hello cluster Hadoop in HDInsight con Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Gestire cluster Hadoop in HDInsight tramite Azure PowerShell
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell è un ambiente di scripting potente che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Azure. In questo articolo si apprenderà come toomanage di cluster Hadoop in HDInsight di Azure tramite una console di Azure PowerShell locale tramite hello utilizzato Windows PowerShell. Per hello l'elenco dei cmdlet HDInsight PowerShell hello, vedere [riferimento ai cmdlet di HDInsight][hdinsight-powershell-reference].

**Prerequisiti**

Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Installare Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Se è installato Azure PowerShell versione 0.9x, è necessario disinstallarlo prima di installare una versione più recente.

versione di hello toocheck di hello installato PowerShell:

    Get-Module *azure*

toouninstall hello versione meno recente, eseguire programmi e funzionalità nel Pannello di controllo hello.

## <a name="create-clusters"></a>Creare i cluster
Vedere [Creare cluster basati su Linux in HDInsight tramite Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Elencare cluster
Utilizzare hello seguente toolist comando tutti i cluster nella sottoscrizione corrente hello:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Mostrare cluster
Utilizzare i seguenti comandi tooshow dettagli di un cluster specifico nella sottoscrizione corrente hello hello:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Eliminare cluster
Utilizzare hello successivo comando toodelete un cluster:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Inoltre, è possibile eliminare un cluster tramite la rimozione di gruppo di risorse hello contenente cluster hello. Si noti, questa operazione eliminerà tutte le risorse di hello gruppo hello inclusi account di archiviazione predefinito hello.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Ridimensionare i cluster
scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.

> [!NOTE]
> Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive. Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.  Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:

* Hadoop

    È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione. È inoltre possibile avviare nuovi processi mentre è in corso hello operazione. Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.

    Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati. In questo modo tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento. È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.
* HBase

    Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione. Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello. Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo toohello nodo head del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione. Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.

    A tale scopo, è possibile scegliere tra due opzioni:

  * Interfaccia utente Web di Storm
  * Interfaccia della riga di comando (CLI)

    Consultare toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.

    interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:

    ![Ribilanciamento scala di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

hello toochange dimensioni del cluster Hadoop usando Azure PowerShell, eseguire hello comando seguente da un computer client:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Concedere/Revocare l'accesso
Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Per impostazione predefinita, a questi servizi è concesso l'accesso. È possibile revocare o concedere l'accesso hello. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Per concedere o revocare l'accesso hello, sarà necessario reimpostare la password e nome utente di hello del cluster.
>
>

Questa operazione può anche essere eseguita tramite hello portale. Vedere [HDInsight amministrare tramite hello Azure portal][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Aggiornare le credenziali utente HTTP
È hello stessa stored procedure come [accesso Grant/revoke HTTP](#grant/revoke-access). Se il cluster hello è stata concessa hello accesso HTTP, è necessario revocare.  E quindi concedere l'accesso di hello con nuove credenziali utente HTTP.

## <a name="find-hello-default-storage-account"></a>Trovare l'account di archiviazione predefinito hello
Hello lo script di Powershell seguente viene illustrato come tooget hello Nome account di archiviazione predefinito e hello chiave account di archiviazione predefinito per un cluster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Trovare il gruppo di risorse hello
In modalità di gestione risorse di hello, ogni cluster HDInsight appartiene tooan gruppo di risorse di Azure.  gruppo di risorse toofind hello:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Inviare i processi
**processi MapReduce toosubmit**

Vedere [esempi di MapReduce di Hadoop in HDInsight basato su Windows](hdinsight-run-samples.md).

**processi Hive toosubmit**

Vedere [Esecuzione di query Hive tramite PowerShell](hdinsight-hadoop-use-hive-powershell.md)

**processi Pig toosubmit**

Vedere [Eseguire processi Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**toosubmit Sqoop processi**

Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop.md).

**processi di Oozie toosubmit**

Vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Carica l'archiviazione Blob di dati tooAzure
Vedere [caricare dati tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Vedere anche
* [Documentazione di riferimento dei cmdlet di HDInsight][hdinsight-powershell-reference]
* [Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]
* [Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]
* [Creare cluster HDInsight][hdinsight-provision]
* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]
* [Introduzione ad Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
