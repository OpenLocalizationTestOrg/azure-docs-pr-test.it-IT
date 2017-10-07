---
title: soluzioni di archiviazione aaaAzure per Server di R in HDInsight - Azure | Documenti Microsoft
description: Informazioni su hello archiviazione diverse opzioni disponibili toousers con R Server in HDInsight
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Soluzioni di Archiviazione di Azure per R Server su HDInsight

Microsoft R Server in HDInsight presenta una serie di dati toopersist soluzioni di archiviazione, codice o gli oggetti che contengono risultati dall'analisi. Tra cui hello le opzioni seguenti:

- [BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Archiviazione di Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/)
- [Archiviazione file di Azure](https://azure.microsoft.com/services/storage/files/)

È anche possibile hello dell'accesso a più account di archiviazione Azure o i contenitori con il cluster HDI. Archiviazione di File di Azure è un'opzione di archiviazione di dati ideale per l'utilizzo nel nodo edge hello che consente di toomount una condivisione di file di archiviazione di Azure, ad esempio, hello Linux file System. Tuttavia, le condivisioni File di Azure possono essere montate e usate in qualsiasi sistema dotato di un sistema operativo supportato, ad esempio Windows o Linux. 

Quando si crea un cluster Hadoop in HDInsight, si specifica un account di **Archiviazione di Azure** o un **archivio Data Lake**. Un contenitore di archiviazione specifico da tale account contiene hello file system per i cluster hello creato (ad esempio, hello Hadoop Distributed File System). Per altre informazioni e istruzioni, vedere:

- [Usare l'Archiviazione di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Usare Data Lake Store con cluster Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md). 

Per ulteriori informazioni sulle soluzioni di archiviazione di Azure hello, vedere [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md). 

Per istruzioni sulla selezione di hello più appropriato archiviazione opzione toouse per lo scenario, vedere [determinazione quando toouse BLOB di Azure, i file di Azure o i dischi dati di Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Usare gli account di archiviazione BLOB di Azure con R Server

Se necessario, è possibile accedere a più account di archiviazione o contenitori di Azure con il cluster HDI. toodo in tal caso, è necessario l'account di archiviazione aggiuntivi toospecify hello in hello dell'interfaccia utente quando si crea cluster hello e quindi seguire questi passaggi toouse con R Server.

> [!WARNING]
> Per motivi di prestazioni, hello cluster HDInsight viene creato in hello stesso data center dell'account di archiviazione primaria hello specificato. Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello.

1. Creare un cluster HDInsight con un nome di account di archiviazione **storage1** e un contenitore predefinito denominato **container1**.
2. Si specifica anche un account di archiviazione aggiuntivo denominato **storage2**.  
3. Copiare la directory /share hello mycsv.csv file toohello ed eseguire analisi su tale file.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. Nel codice R, impostare il nodo di nome hello troppo**impostazione predefinita,** e impostare il tooprocess file e directory.  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

Tutti hello account di archiviazione punto toohello riferimenti a file e directory wasb://container1@storage1.blob.core.windows.net. Si tratta di hello **account di archiviazione predefinito** che è associato il cluster di HDInsight hello.

A questo punto, si supponga che si desidera tooprocess un file denominato mySpecial.csv che si trova in /private hello directory di **container2** in **storage2**.

Nel codice R, scegliere hello nome nodo riferimento toohello **storage2** account di archiviazione.


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

Tutti hello file e directory riferimenti ora toohello punto dell'account di archiviazione wasb://container2@storage2.blob.core.windows.net. Si tratta di hello **nome nodo** che sono stati specificati.

Hai tooconfigure hello /user RevoShare/<SSH username> directory **storage2** come indicato di seguito:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Usare un Archivio Azure Data Lake con R Server

toouse Data Lake vengono archiviati con l'account di HDInsight, è necessario toogive l'archivio di Azure Data Lake tooeach di accesso del cluster che si desidera toouse. Per istruzioni sulla modalità toouse hello toocreate portale Azure un HDInsight cluster con un account archivio Azure Data Lake come spazio di archiviazione predefinito hello o un archivio aggiuntivo, vedere [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

È quindi utilizzare hello archivio nello script R Analogamente a come descritto nella procedura precedente hello, si ha un account di archiviazione secondaria di Azure.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Aggiungere tooyour accesso cluster che vengono archiviati in Azure Data Lake
Per accedere a un Archivio Azure Data Lake, usare un'entità servizio di Azure Active Directory (AAD) associata al cluster HDInsight.

tooadd un'entità servizio di Azure Active Directory:

1. Quando si crea il cluster HDInsight, selezionare **identità AAD Cluster** da hello **origine dati** scheda.

2. In hello **identità AAD Cluster** nella finestra di dialogo **selezionare entità servizio Active Directory**selezionare **Crea nuovo**.

Dopo aver creare una password per assegnare un nome di hello dell'entità servizio, fare clic su **Gestisci accesso ADLS** hello tooassociate archivia dell'entità servizio con il Data Lake.

È inoltre possibile tooadd cluster accesso tooone o altre Data Lake archivi dopo la creazione del cluster. Aprire hello voce portale Azure per un archivio Data Lake e passare troppo**Esplora dati > accesso > Aggiungi**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Come tooaccess hello archivio Data Lake da R Server

Una volta che è stato concesso l'archivio Data Lake tooa di accesso, è possibile utilizzare l'archivio di hello in R Server su HDInsight hello si trattasse di un account di archiviazione secondaria di Azure. Hello solo differenza è il prefisso hello **wasb: / /** cambia troppo**adl: / /** come indicato di seguito:


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


Hello comandi riportati di seguito vengono utilizzati tooconfigure hello account archivio Data Lake con directory RevoShare hello e aggiungere file CSV di esempio hello hello precedente esempio:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Usare Archiviazione file di Azure con R Server

È inoltre disponibile un'opzione di archiviazione di dati ideale per l'utilizzo nel nodo edge hello chiamato [file di Azure] ((https://azure.microsoft.com/services/storage/files/). Consente di toomount un toohello di condivisione file di archiviazione di Azure il sistema di file Linux. Questa opzione può essere utile per l'archiviazione dei file di dati, gli script R e gli oggetti risultato che potrebbero essere necessario in un secondo momento, soprattutto quando si rende il senso toouse hello del file system native sul nodo del bordo hello anziché HDFS. 

Dei principali vantaggi dei file di Azure è il file hello condivisioni possono essere montate e utilizzate da qualsiasi sistema che dispone di un sistema operativo supportato, ad esempio Windows o Linux. Ad esempio, può essere usato da un altro cluster HDInsight disponibile all'utente o a un membro del team, da una macchina virtuale di Azure o anche da un sistema locale. Per altre informazioni, vedere:

- [Come toouse archiviazione di File di Azure con Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Come toouse archiviazione di File di Azure in Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Passaggi successivi

Ora che si conoscono le opzioni di archiviazione di Azure hello, seguente hello utilizzare collegamenti toodiscover modalità di acquisizione di attività di analisi scientifica dei dati eseguita con il Server di R in HDInsight.

* [Panoramica: R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-overview.md)
* [Articolo introduttivo relativo a Server R su Hadoop.](hdinsight-hadoop-r-server-get-started.md)
* [Aggiungere RStudio Server tooHDInsight (se non è aggiunto durante la creazione del cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-compute-contexts.md)

