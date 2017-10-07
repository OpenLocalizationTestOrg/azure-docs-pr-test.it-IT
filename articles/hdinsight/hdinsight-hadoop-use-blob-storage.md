---
title: dati aaaQuery da HDFS compatibile con archiviazione di Azure - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati tooquery da archiviazione di Azure e archivio Azure Data Lake toostore risultati dell'analisi.
keywords: archivio BLOB, HDFS, dati strutturati, dati non strutturati, Data Lake Store, input Hadoop, output Hadoop, archivio Hadoop, input HDFS, output HDFS, archivio HDFS, WASB in Azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Usare una risorsa di archiviazione di Azure con cluster Azure HDInsight

dati tooanalyze nel cluster HDInsight, è possibile archiviare dati hello in archiviazione di Azure, archivio Azure Data Lake o entrambi. Entrambe le opzioni di archiviazione consentono di eliminare il toosafely che cluster HDInsight vengono utilizzate per il calcolo senza perdita di dati utente.

Hadoop supporta una nozione di file system predefinito hello. file system predefinito Hello implica un schema predefinito e l'autorità. Può anche essere percorsi relativi tooresolve utilizzato. Durante il processo di creazione del cluster HDInsight hello, è possibile specificare un contenitore blob in archiviazione di Azure come file system predefinito hello o con HDInsight 3.5, è possibile selezionare l'archiviazione di Azure o archivio Azure Data Lake come sistema di file predefinito hello con alcune eccezioni. Per il supporto di hello dell'utilizzo di archivio Data Lake come predefinite hello e collegato di archiviazione, vedere [disponibilità per il cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

Questo articolo illustra come usare Archiviazione di Azure con i cluster HDInsight. toolearn come archivio Data Lake funziona con i cluster HDInsight, vedere [archivio utilizzare Azure Data Lake con Azure HDInsight cluster](hdinsight-hadoop-use-data-lake-store.md). Per altre informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Archiviazione di Azure è una soluzione di archiviazione affidabile, con finalità generali che si integra facilmente con HDInsight. HDInsight può utilizzare un contenitore blob in archiviazione di Azure come file system predefinito hello per cluster hello. Attraverso un'interfaccia di Hadoop distributed file system (HDFS), set completo di hello dei componenti in HDInsight possibile utilizzare direttamente dati strutturati o archiviati come BLOB.

> [!WARNING]
> Sono disponibili diverse opzioni per la creazione di un account di archiviazione di Azure. Hello nella tabella seguente vengono fornite informazioni su quali opzioni sono supportate con HDInsight:
> 
> | Tipo di account di archiviazione | Livello di archiviazione | Supportato con HDInsight |
> | ------- | ------- | ------- |
> | Account di archiviazione di uso generico | Standard | __Sì__ |
> | &nbsp; | Premium | No |
> | Account di archiviazione BLOB | Accesso frequente | No |
> | &nbsp; | Accesso sporadico | No |

Non è consigliabile utilizzare contenitore blob di hello predefinito per l'archiviazione dei dati di business. L'eliminazione di contenitore di blob predefinito hello dopo ogni tooreduce utilizzare costo di archiviazione è buona norma. Si noti che il contenitore predefinito hello contiene l'applicazione e del sistema log. Verificare i registri di hello tooretrieve che prima di eliminare il contenitore di hello.

La condivisione di un contenitore BLOB tra più cluster non è supportata.

## <a name="hdinsight-storage-architecture"></a>Architettura di archiviazione di HDInsight
Hello seguente diagramma fornisce una visualizzazione astratta dell'architettura di archiviazione di HDInsight dell'utilizzo di archiviazione di Azure hello:

![I cluster Hadoop utilizzano tooaccess HDFS API hello e archiviano dati strutturati nell'archiviazione Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Architettura di archiviazione di HDInsight")

HDInsight fornisce accesso toohello distribuita file system locale associata toohello nodi di calcolo. Questo file system è possibile accedere tramite hello completo URI, ad esempio:

    hdfs://<namenodehost>/<path>

Inoltre, HDInsight consente tooaccess i dati archiviati in archiviazione di Azure. sintassi di Hello è:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Di seguito sono riportate alcune considerazioni sull'uso di un account di Archiviazione di Azure con i cluster HDInsight.

* **Contenitori di account di archiviazione hello che sono connessi tooa cluster:** poiché hello nome e la chiave sono associati ai cluster hello durante la creazione, occorre BLOB toohello accesso completo in tali contenitori.

* **Contenitori pubblici o BLOB pubblici negli account di archiviazione che non sono connessi a cluster tooa:** sono presenti i BLOB di autorizzazione di sola lettura toohello nei contenitori hello.
  
  > [!NOTE]
  > Contenitori pubblici consentono di tooget un elenco di tutti i blob che sono disponibili in tale contenitore e ottenere i metadati del contenitore. BLOB pubblici consentono di BLOB hello tooaccess solo se si conosce l'URL esatto hello. Per ulteriori informazioni, vedere <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">limitare l'accesso toocontainers e blob</a>.
  > 
  > 
* **Contenitori privati negli account di archiviazione che non sono connessi a cluster tooa:** non è possibile accedere BLOB hello in contenitori di hello se non si definisce l'account di archiviazione hello quando si inviano processi WebHCat hello. Questo concetto verrà spiegato più avanti nell'articolo.

account di archiviazione Hello che sono definiti nel processo di creazione hello e le relative chiavi vengono archiviate in %HADOOP_HOME%/conf/core-site.xml nei nodi del cluster hello. comportamento predefinito di Hello di HDInsight è definiti nel file core-Site.XML hello gli account di archiviazione di toouse hello. È possibile modificare questa impostazione usando [Ambari](./hdinsight-hadoop-manage-ambari.md)

Più processi WebHCat, inclusi Hive, MapReduce, lo streaming Hadoop e Pig, possono includere una descrizione degli account di archiviazione e dei metadati (questo è valido solo per Pig con account di archiviazione, non per i metadati). Per altre informazioni, vedere [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Uso di un cluster HDInsight con account di archiviazione e metastore alternativi).

I BLOB possono essere usati per i dati strutturati e non strutturati. I contenitori BLOB archiviano i dati come coppie chiave-valore e non esiste una gerarchia di directory. Tuttavia, il carattere di barra hello (/) può essere utilizzato all'interno di hello toomake nome della chiave appare come se un file viene archiviato in una struttura di directory. Ad esempio, la chiave di un BLOB potrebbe essere *input/log1.txt*. Non effettivo *input* directory esistente, ma a causa di toohello presenza del carattere di barra hello nel nome della chiave hello, con aspetto hello di un percorso di file.

## <a id="benefits"></a>Vantaggi di Archiviazione di Azure
Hello implicita impatto sulle prestazioni del cluster di calcolo non condivisione della posizione e le risorse di archiviazione verrà attenuato modo hello cluster di calcolo hello vengono create le risorse di account di archiviazione toohello Chiudi interno hello regione di Azure, in cui la rete ad alta velocità hello rende efficiente per i nodi di calcolo hello tooaccess hello dati all'interno di archiviazione di Azure.

Esistono numerosi vantaggi associati alla memorizzazione di dati hello in archiviazione di Azure anziché HDFS:

* **Riutilizzo di dati e la condivisione:** dati hello in HDFS si trovano all'interno di cluster di calcolo hello. Solo le applicazioni che hanno accesso toohello hello di calcolo cluster è possibile utilizzare dati hello tramite API di HDFS. Hello dati nell'archiviazione di Azure sono accessibili tramite le API di HDFS hello o hello [API REST dell'archiviazione Blob][blob-storage-restAPI]. Di conseguenza, un set più ampio di applicazioni (inclusi altri cluster di HDInsight) e gli strumenti possono essere tooproduce utilizzato e utilizzare dati di hello.
* **Archiviazione dei dati:** l'archiviazione dei dati nell'archiviazione di Azure consente il cluster di HDInsight hello utilizzati per toobe calcolo eliminato in modo sicuro senza perdita di dati utente.
* **Il costo di archiviazione di dati:** l'archiviazione dei dati in DFS per a lungo termine hello è più costoso rispetto all'archiviazione hello in archiviazione di Azure perché costo hello di un cluster di calcolo è maggiore del costo di hello di archiviazione di Azure. Inoltre, poiché non devono di dati hello toobe ricaricato per la generazione di ogni cluster di calcolo, si sta salvando i costi di caricamento dei dati.
* **Scalabilità orizzontale elastica:** HDFS Sebbene fornisce un sistema di file di scalabilità orizzontale, scala hello è determinata dal numero di hello di nodi creato per il cluster. Modifica scala hello può diventare una maggiore complessità del processo di affidarsi alla scalabilità di funzionalità che si ottengono automaticamente nell'archiviazione di Azure elastica di hello.
* **Replica geografica:** è possibile eseguire la replica geografica di Archiviazione di Azure. Sebbene in questo modo la ridondanza dei dati e ripristino geografico, un percorso di replica geografica toohello failover influisce negativamente sulle prestazioni e potrebbe comportare costi aggiuntivi. Pertanto, si consiglia di replica geografica hello toochoose cautela e solo se il valore di hello dei dati di hello vale la pena costi aggiuntivi hello.

Alcuni pacchetti e i processi MapReduce possono creare i risultati intermedi non è toostore nell'archiviazione di Azure. In tale caso, è possibile scegliere dati hello toostore hello HDFS locale. In effetti, HDInsight utilizza DFS per molti di questi risultati intermedi nei processi Hive e in altri processi.

> [!NOTE]
> La maggior parte dei comandi HDFS, ad esempio <b>ls</b>, <b>copyFromLocal</b> e <b>mkdir</b>, funziona come previsto. Hello solo i comandi specifici toohello HDFS implementazione nativa (ovvero tooas cui DFS), ad esempio <b>fschk</b> e <b>dfsadmin</b>, Mostra un comportamento diverso in archiviazione di Azure.
> 
> 

## <a name="create-blob-containers"></a>Creare dei contenitori BLOB
toouse BLOB, creare innanzitutto un [account di archiviazione Azure][azure-storage-create]. Come parte di questa operazione, specificare un'area di Azure in cui viene creato l'account di archiviazione hello. cluster Hello e account di archiviazione hello deve essere ospitati in hello stessa area. database di SQL Server metastore Hello Hive e Oozie metastore SQL Server database deve trovarsi in hello stessa area.

Ogni volta che viene eseguito, ogni blob che crei appartiene tooa contenitore nell'account di archiviazione di Azure. Può trattarsi di un contenitore BLOB esistente, creato all'esterno di HDInsight, oppure di un contenitore creato per un cluster HDInsight.

contenitore di Blob predefinito Hello archivia informazioni specifiche del cluster, ad esempio i registri e cronologia dei processi. Non condividere un contenitore BLOB predefinito con più cluster HDInsight. Questa operazione potrebbe danneggiare la cronologia processo. È consigliabile toouse un contenitore diverso per ogni cluster e inserire dati condivisa su un account di archiviazione collegato specificato nella distribuzione di tutti i cluster anziché come account di archiviazione predefinito hello. Per altre informazioni sulla configurazione degli account di archiviazione collegati, vedere [Creare cluster HDInsight][hdinsight-creation]. È tuttavia possibile riutilizzare un contenitore di archiviazione predefinito dopo aver eliminato il cluster HDInsight originale di hello. Per i cluster HBase, è possibile mantenere effettivamente schema della tabella HBase hello e i dati creando un nuovo cluster HBase tramite contenitore di blob hello predefinito utilizzato da un cluster HBase che è stato eliminato.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure
Quando si crea un cluster HDInsight da hello portale, è dettagli dell'account archiviazione tooprovide hello hello opzioni (come illustrato di seguito). È inoltre possibile specificare se si desidera un account di archiviazione aggiuntivo associato hello cluster e in tal caso, scegliere da un altro blob di archiviazione di Azure come spazio di archiviazione aggiuntivo hello o archivio Data Lake.

![Origine dati della creazione di HDInsight Hadoop](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> Utilizzo di un account di archiviazione aggiuntivo in un percorso diverso da quello del cluster HDInsight hello non è supportato.


### <a name="use-azure-powershell"></a>Uso di Azure PowerShell
Se si [installato e configurato Azure PowerShell][powershell-install], è possibile utilizzare hello seguente dal prompt dei comandi toocreate di hello Azure PowerShell, un account di archiviazione e un contenitore:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Utilizzare l'interfaccia della riga di comando di Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Se dispone di [installato e configurato Azure CLI hello](../cli-install-nodejs.md), comando che segue hello possono essere utilizzati tooa account di archiviazione e contenitore.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Hello `--type` parametro indica come account di archiviazione hello è stata replicata. Per altre informazioni, vedere [Replica di Archiviazione di Azure](../storage/storage-redundancy.md). Non usare ZRS in quanto ZRS non supporta BLOB di pagine, file, tabelle o code.
> 
> 

Si è richiesta toospecify hello area geografica che viene creato l'account di archiviazione di hello in. È necessario creare account di archiviazione hello in hello stessa area che si prevede di creare il cluster HDInsight.

Una volta creato l'account di archiviazione hello, utilizzare hello chiavi dell'account di archiviazione hello tooretrieve comando seguente:

    azure storage account keys list <storageaccountname>

toocreate un contenitore, usare hello comando seguente:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Accedere ai file in Archiviazione di Azure
schema URI Hello per accedere ai file nell'archiviazione di Azure da HDInsight è:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

schema URI Hello fornisce l'accesso non crittografata (con hello *wasb:* prefisso) e SSL crittografate di accesso (con *wasbs*). Si consiglia di utilizzare *wasbs* laddove possibile, anche quando l'accesso ai dati che si trova all'interno di hello stessa area in Azure.

Hello &lt;BlobStorageContainerName&gt; identifica hello nome del contenitore blob hello in archiviazione di Azure.
Hello &lt;StorageAccountName&gt; identifica il nome di account di archiviazione di Azure hello. È necessario specificare un nome di dominio completo (FQDN).

Se non si specifica &lt;BlobStorageContainerName&gt; né &lt;StorageAccountName&gt; è stata specificata, viene utilizzato il file system di hello predefinito. Per i file hello nel file system di hello predefinito, è possibile utilizzare un percorso relativo o assoluto. Ad esempio, hello *hadoop-mapreduce-examples.jar* file fornito con i cluster HDInsight può essere tooby cui viene fatto riferimento utilizzando uno dei seguenti hello:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> nome del file Hello è <i>hadoop examples.jar</i> nel cluster di HDInsight versioni 2.1 e 1.6.
> 
> 

Hello &lt;percorso&gt; hello nome percorso HDFS file o directory. Poiché i contenitori in Archiviazione di Azure sono semplicemente archivi chiave-valore, non esiste un vero file system gerarchico. Un carattere barra ( / ) all'interno di una chiave BLOB viene interpretato come un separatore di directory. Ad esempio, nome blob hello per *hadoop-mapreduce-examples.jar* è:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Quando si lavora con i BLOB all'esterno di HDInsight, la maggior parte delle utilità non riconosce il formato WASB hello e invece prevede un formato del percorso di base, ad esempio `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Accedere ai BLOB 


### <a name="access-blobs-using-azure-powershell"></a> Usare Azure PowerShell
> [!NOTE]
> comandi Hello in questa sezione forniscono un esempio di base dell'utilizzo di PowerShell tooaccess dati archiviati nel BLOB. Per un esempio più completo personalizzato per l'utilizzo di HDInsight, vedere hello [strumenti HDInsight](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Utilizzare hello comando toolist hello blob cmdlet seguenti:

    Get-Command *blob*

![Elenco dei cmdlet PowerShell correlati al BLOB.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Caricare file
Vedere [caricare dati tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Download dei file
Hello lo script seguente consente di scaricare una cartella di blocco blob toohello corrente. Prima dell'esecuzione dello script hello, modificare hello tooa cartella in cui si dispone delle autorizzazioni di scrittura.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Fornire nome gruppo di risorse hello e nome del cluster hello, è possibile utilizzare hello seguente codice:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Eliminare file
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Elencare file
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Esecuzione di query Hive utilizzando un account di archiviazione non definito
Questo esempio mostra come toolist una cartella dall'account di archiviazione che non è definito durante hello creazione processo.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Utilizzare l'interfaccia della riga di comando di Azure
Utilizzare hello comandi toolist hello relativi blob dei comandi seguenti:

    azure storage blob

**Esempio di utilizzo tooupload CLI di Azure un file**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Esempio di utilizzo toodownload CLI di Azure un file**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Esempio di utilizzo toodelete CLI di Azure un file**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Esempio di utilizzo dei file toolist CLI di Azure**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Usare account di archiviazione aggiuntivi

Durante la creazione di un cluster HDInsight, specificare l'account di archiviazione di Azure hello da tooassociate con esso. In account di archiviazione toothis, è inoltre possibile aggiungere ulteriore spazio di archiviazione di account da hello stessa sottoscrizione di Azure o sottoscrizioni di Azure diversi durante il processo di creazione di hello o dopo aver creato un cluster. Per istruzioni sull'aggiunta di altri account di archiviazione, vedere [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> Utilizzo di un account di archiviazione aggiuntivo in un percorso diverso da quello del cluster HDInsight hello non è supportato.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toouse HDFS compatibile con archiviazione di Azure con HDInsight. In questo modo si toobuild scalabili e a lungo termine, l'archiviazione di soluzioni di acquisizione dei dati e usare HDInsight toounlock hello informazioni all'interno di hello archiviato strutturate e i dati non strutturati.

Per altre informazioni, vedere:

* [Introduzione ad Azure HDInsight][hdinsight-get-started]
* [Introduzione ad Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Utilizzo di firme di accesso condiviso archiviazione Azure toorestrict accesso toodata con HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
