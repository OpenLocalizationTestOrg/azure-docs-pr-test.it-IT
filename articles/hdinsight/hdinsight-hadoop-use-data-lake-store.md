---
title: aaaUse archivio Data Lake con Hadoop in HDInsight di Azure | Documenti Microsoft
description: Informazioni su come tooquery dati dall'archivio Azure Data Lake e toostore risultati dell'analisi.
keywords: archiviazione BLOB, hdfs, dati strutturati, dati non strutturati, Data Lake Store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Usare Data Lake Store con cluster Azure HDInsight

dati tooanalyze nel cluster HDInsight, è possibile archiviare dati hello sia in [di archiviazione di Azure](../storage/common/storage-introduction.md), [archivio Azure Data Lake](../data-lake-store/data-lake-store-overview.md), o entrambi. Entrambe le opzioni di archiviazione consentono di eliminare il toosafely che cluster HDInsight vengono utilizzate per il calcolo senza perdita di dati utente.

Questo articolo illustra come usare Data Lake Store con i cluster HDInsight. toolearn come archiviazione di Azure funziona con i cluster HDInsight, vedere [cluster di archiviazione di Azure usare con Azure HDInsight](hdinsight-hadoop-use-blob-storage.md). Per altre informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!NOTE]
> L'accesso a Data Lake Store avviene sempre tramite un canale protetto, pertanto non è presente un nome di schema del file system `adls`. Viene usato sempre `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Disponibilità per i cluster HDInsight

Hadoop supporta una nozione di file system predefinito hello. file system predefinito Hello implica un schema predefinito e l'autorità. Può anche essere percorsi relativi tooresolve utilizzato. Durante il processo di creazione del cluster HDInsight hello, è possibile specificare un contenitore blob in archiviazione di Azure come file system predefinito hello o con HDInsight 3.5 e versioni successive, è possibile selezionare l'archiviazione di Azure o archivio Azure Data Lake come sistema di file hello predefinito con un alcune eccezioni. 

I cluster HDInsight possono usare Data Lake Store in due modi:

* Come spazio di archiviazione predefinito hello
* Come risorsa di archiviazione aggiuntiva, con BLOB del servizio di archiviazione di Azure come risorsa predefinita.

Al momento, solo alcuni hello HDInsight cluster tipi/versioni supportano l'utilizzo di archivio Data Lake come spazio di archiviazione predefinito e account di archiviazione aggiuntivi:

| Tipo di cluster HDInsight | Data Lake Store come risorsa di archiviazione predefinita | Data Lake Store come risorsa di archiviazione aggiuntiva| Note |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight versione 3.6 | Sì | Sì | |
| HDInsight versione 3.5 | Sì | Sì | Con l'eccezione hello di HBase|
| HDInsight versione 3.4 | No | Sì | |
| HDInsight versione 3.3 | No | No | |
| HDInsight versione 3.2 | No | Sì | |
| HDInsight Premium (livello)| No | No | |
| Storm | | |È possibile utilizzare i dati di archivio Data Lake toowrite da una topologia di Storm. È anche possibile usare Data Lake Store per archiviare dati di riferimento che possono essere letti da una topologia Storm.|

Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influiscono sulle prestazioni o hello possibilità tooread o scrivere tooAzure archiviazione dal cluster di hello.


## <a name="use-data-lake-store-as-default-storage"></a>Usare Data Lake Store come risorsa di archiviazione predefinita

Quando HDInsight viene distribuito con l'archivio Data Lake come spazio di archiviazione predefinito, vengono archiviati i file correlati al cluster hello in archivio Data Lake nella seguente posizione hello:

    adl://mydatalakestore/<cluster_root_path>/

dove `<cluster_root_path>` hello nome di una cartella in cui si crea in archivio Data Lake. Se si specifica un percorso radice per ogni cluster, è possibile utilizzare hello stesso account archivio Data Lake per più di un cluster. Pertanto, è possibile disporre di una configurazione in cui:

* Cluster1 possibile utilizzare il percorso di hello`adl://mydatalakestore/cluster1storage`
* Cluster2 possibile utilizzare il percorso di hello`adl://mydatalakestore/cluster2storage`

Si noti che entrambi hello utilizzare cluster hello stesso account archivio Data Lake **mydatalakestore**. Ogni cluster dispone di accesso tooits proprietari filesystem radice nell'archivio Data Lake. Hello esperienza di distribuzione del portale di Azure in particolare viene richiesto un nome di cartella toouse come **/clusters/\<clustername >** per il percorso radice hello.

toobe toouse in grado di un archivio Data Lake come spazio di archiviazione predefinito, è necessario concedere toohello di accesso dell'entità servizio hello seguenti percorsi:

- radice di account archivio Data Lake Hello.  ad esempio adl://mydatalakestore/.
- cartella Hello per tutte le cartelle di cluster.  ad esempio adl://mydatalakestore/clusters.
- cartella Hello cluster hello.  ad esempio adl://mydatalakestore/clusters/cluster1storage.

Per altre informazioni su come creare un'entità servizio e concedere l'accesso, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Usare Data Lake Store come risorsa di archiviazione aggiuntiva

È possibile utilizzare l'archivio Data Lake come ulteriore spazio di archiviazione per cluster hello anche. In questi casi, spazio di archiviazione predefinito hello cluster può essere un Blob di archiviazione di Azure o un account archivio Data Lake. Se si eseguono i processi di HDInsight sui dati hello archiviati nell'archivio Data Lake come ulteriore spazio di archiviazione, è necessario utilizzare i file toohello di hello percorso completo. ad esempio:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Si noti che non esiste alcun **cluster_root_path** nell'URL hello ora. Ciò avviene perché l'archivio Data Lake non è un archivio predefinito in questo caso è sufficiente toodo fornire hello percorso toohello file.

toobe toouse in grado di un archivio Data Lake come ulteriore spazio di archiviazione, è necessario solo toogrant hello servizio principale toohello percorsi di accesso in cui sono archiviati i file.  ad esempio:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Per altre informazioni su come creare un'entità servizio e concedere l'accesso, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Usare più di un account di Data Lake Store

Aggiunta di un account archivio Data Lake come aggiuntive e più di un archivio Data Lake account vengono effettuati mediante l'assegnazione di autorizzazioni di cluster HDInsight hello del dati negli account archivio Data Lake di uno o più. Vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurare l'accesso a Data Lake Store

tooconfigure accesso archivio Data Lake dal cluster HDInsight, è necessario disporre di un'entità servizio di Azure Active directory (Azure AD). Solo un amministratore di Azure AD può creare un'entità servizio. entità servizio Hello deve essere creata con un certificato. Per altre informazioni, vedere [Configurare l'accesso a Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Creare un'entità servizio con certificato autofirmato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Se si intende archivio Azure Data Lake di toouse come spazio di archiviazione aggiuntivo per il cluster HDInsight, è consigliabile farlo durante la creazione di cluster hello come descritto in questo articolo. Aggiunta archivio Azure Data Lake come tooan ulteriore spazio di archiviazione cluster HDInsight esistente è una complessità del processo e soggetta a tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Accedere ai file dal cluster hello

Esistono diversi modi per accedere a file hello in archivio Data Lake da un cluster HDInsight.

* **Usa il nome completo di hello**. Con questo approccio, si fornita i file toohello percorso completo di hello che si desidera tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Utilizzando il formato di percorso abbreviato hello**. Con questo approccio, è sostituire percorso hello backup principale del cluster toohello adl: / / /. Nell'esempio hello sopra, in tal caso, è possibile sostituire `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` con `adl:///`.

        adl:///<file path>

* **Percorso relativo hello utilizzando**. Con questo approccio, si fornisce solo hello relativo percorso toohello file che si desidera tooaccess. Ad esempio, se hello file toohello percorso completo è:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    È possibile accedere hello stesso file sample.log usando invece il percorso relativo.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Creare cluster HDInsight con accesso tooData Lake archivio

Utilizzare i seguenti collegamenti per informazioni dettagliate su come cluster di HDInsight con toocreate accedere archivio Lake tooData hello.

* [Uso del portale](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Uso di PowerShell con Data Lake Store come risorsa di archiviazione predefinita](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Uso di PowerShell con Data Lake Store come risorsa di archiviazione aggiuntiva](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Uso di modelli di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso toouse archivio HDFS compatibili con Azure Data Lake con HDInsight. In questo modo si toobuild scalabili e a lungo termine, l'archiviazione di soluzioni di acquisizione dei dati e usare HDInsight toounlock hello informazioni all'interno di hello archiviato strutturate e i dati non strutturati.

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
