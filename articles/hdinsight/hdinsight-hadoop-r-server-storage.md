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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="b6421-103">Soluzioni di Archiviazione di Azure per R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6421-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="b6421-104">Microsoft R Server in HDInsight presenta una serie di dati toopersist soluzioni di archiviazione, codice o gli oggetti che contengono risultati dall'analisi.</span><span class="sxs-lookup"><span data-stu-id="b6421-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="b6421-105">Tra cui hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6421-105">These include hello following options:</span></span>

- [<span data-ttu-id="b6421-106">BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b6421-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="b6421-107">Archiviazione di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b6421-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="b6421-108">Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="b6421-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="b6421-109">È anche possibile hello dell'accesso a più account di archiviazione Azure o i contenitori con il cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="b6421-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="b6421-110">Archiviazione di File di Azure è un'opzione di archiviazione di dati ideale per l'utilizzo nel nodo edge hello che consente di toomount una condivisione di file di archiviazione di Azure, ad esempio, hello Linux file System.</span><span class="sxs-lookup"><span data-stu-id="b6421-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="b6421-111">Tuttavia, le condivisioni File di Azure possono essere montate e usate in qualsiasi sistema dotato di un sistema operativo supportato, ad esempio Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b6421-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="b6421-112">Quando si crea un cluster Hadoop in HDInsight, si specifica un account di **Archiviazione di Azure** o un **archivio Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="b6421-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="b6421-113">Un contenitore di archiviazione specifico da tale account contiene hello file system per i cluster hello creato (ad esempio, hello Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="b6421-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="b6421-114">Per altre informazioni e istruzioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="b6421-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="b6421-115">Usare l'Archiviazione di Azure con HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6421-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="b6421-116">[Usare Data Lake Store con cluster Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="b6421-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="b6421-117">Per ulteriori informazioni sulle soluzioni di archiviazione di Azure hello, vedere [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6421-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="b6421-118">Per istruzioni sulla selezione di hello più appropriato archiviazione opzione toouse per lo scenario, vedere [determinazione quando toouse BLOB di Azure, i file di Azure o i dischi dati di Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="b6421-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="b6421-119">Usare gli account di archiviazione BLOB di Azure con R Server</span><span class="sxs-lookup"><span data-stu-id="b6421-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="b6421-120">Se necessario, è possibile accedere a più account di archiviazione o contenitori di Azure con il cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="b6421-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="b6421-121">toodo in tal caso, è necessario l'account di archiviazione aggiuntivi toospecify hello in hello dell'interfaccia utente quando si crea cluster hello e quindi seguire questi passaggi toouse con R Server.</span><span class="sxs-lookup"><span data-stu-id="b6421-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="b6421-122">Per motivi di prestazioni, hello cluster HDInsight viene creato in hello stesso data center dell'account di archiviazione primaria hello specificato.</span><span class="sxs-lookup"><span data-stu-id="b6421-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="b6421-123">Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b6421-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="b6421-124">Creare un cluster HDInsight con un nome di account di archiviazione **storage1** e un contenitore predefinito denominato **container1**.</span><span class="sxs-lookup"><span data-stu-id="b6421-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="b6421-125">Si specifica anche un account di archiviazione aggiuntivo denominato **storage2**.</span><span class="sxs-lookup"><span data-stu-id="b6421-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="b6421-126">Copiare la directory /share hello mycsv.csv file toohello ed eseguire analisi su tale file.</span><span class="sxs-lookup"><span data-stu-id="b6421-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="b6421-127">Nel codice R, impostare il nodo di nome hello troppo**impostazione predefinita,** e impostare il tooprocess file e directory.</span><span class="sxs-lookup"><span data-stu-id="b6421-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

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

<span data-ttu-id="b6421-128">Tutti hello account di archiviazione punto toohello riferimenti a file e directory wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b6421-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="b6421-129">Si tratta di hello **account di archiviazione predefinito** che è associato il cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b6421-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="b6421-130">A questo punto, si supponga che si desidera tooprocess un file denominato mySpecial.csv che si trova in /private hello directory di **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="b6421-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="b6421-131">Nel codice R, scegliere hello nome nodo riferimento toohello **storage2** account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b6421-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


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

<span data-ttu-id="b6421-132">Tutti hello file e directory riferimenti ora toohello punto dell'account di archiviazione wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b6421-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="b6421-133">Si tratta di hello **nome nodo** che sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="b6421-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="b6421-134">Hai tooconfigure hello /user RevoShare/<SSH username> directory **storage2** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6421-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="b6421-135">Usare un Archivio Azure Data Lake con R Server</span><span class="sxs-lookup"><span data-stu-id="b6421-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="b6421-136">toouse Data Lake vengono archiviati con l'account di HDInsight, è necessario toogive l'archivio di Azure Data Lake tooeach di accesso del cluster che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="b6421-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="b6421-137">Per istruzioni sulla modalità toouse hello toocreate portale Azure un HDInsight cluster con un account archivio Azure Data Lake come spazio di archiviazione predefinito hello o un archivio aggiuntivo, vedere [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b6421-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="b6421-138">È quindi utilizzare hello archivio nello script R Analogamente a come descritto nella procedura precedente hello, si ha un account di archiviazione secondaria di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6421-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="b6421-139">Aggiungere tooyour accesso cluster che vengono archiviati in Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b6421-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="b6421-140">Per accedere a un Archivio Azure Data Lake, usare un'entità servizio di Azure Active Directory (AAD) associata al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6421-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="b6421-141">tooadd un'entità servizio di Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="b6421-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="b6421-142">Quando si crea il cluster HDInsight, selezionare **identità AAD Cluster** da hello **origine dati** scheda.</span><span class="sxs-lookup"><span data-stu-id="b6421-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="b6421-143">In hello **identità AAD Cluster** nella finestra di dialogo **selezionare entità servizio Active Directory**selezionare **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="b6421-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="b6421-144">Dopo aver creare una password per assegnare un nome di hello dell'entità servizio, fare clic su **Gestisci accesso ADLS** hello tooassociate archivia dell'entità servizio con il Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b6421-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="b6421-145">È inoltre possibile tooadd cluster accesso tooone o altre Data Lake archivi dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="b6421-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="b6421-146">Aprire hello voce portale Azure per un archivio Data Lake e passare troppo**Esplora dati > accesso > Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b6421-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="b6421-147">Come tooaccess hello archivio Data Lake da R Server</span><span class="sxs-lookup"><span data-stu-id="b6421-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="b6421-148">Una volta che è stato concesso l'archivio Data Lake tooa di accesso, è possibile utilizzare l'archivio di hello in R Server su HDInsight hello si trattasse di un account di archiviazione secondaria di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6421-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="b6421-149">Hello solo differenza è il prefisso hello **wasb: / /** cambia troppo**adl: / /** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6421-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


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


<span data-ttu-id="b6421-150">Hello comandi riportati di seguito vengono utilizzati tooconfigure hello account archivio Data Lake con directory RevoShare hello e aggiungere file CSV di esempio hello hello precedente esempio:</span><span class="sxs-lookup"><span data-stu-id="b6421-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="b6421-151">Usare Archiviazione file di Azure con R Server</span><span class="sxs-lookup"><span data-stu-id="b6421-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="b6421-152">È inoltre disponibile un'opzione di archiviazione di dati ideale per l'utilizzo nel nodo edge hello chiamato [file di Azure] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="b6421-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="b6421-153">Consente di toomount un toohello di condivisione file di archiviazione di Azure il sistema di file Linux.</span><span class="sxs-lookup"><span data-stu-id="b6421-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="b6421-154">Questa opzione può essere utile per l'archiviazione dei file di dati, gli script R e gli oggetti risultato che potrebbero essere necessario in un secondo momento, soprattutto quando si rende il senso toouse hello del file system native sul nodo del bordo hello anziché HDFS.</span><span class="sxs-lookup"><span data-stu-id="b6421-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="b6421-155">Dei principali vantaggi dei file di Azure è il file hello condivisioni possono essere montate e utilizzate da qualsiasi sistema che dispone di un sistema operativo supportato, ad esempio Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b6421-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="b6421-156">Ad esempio, può essere usato da un altro cluster HDInsight disponibile all'utente o a un membro del team, da una macchina virtuale di Azure o anche da un sistema locale.</span><span class="sxs-lookup"><span data-stu-id="b6421-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="b6421-157">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="b6421-157">For more information, see:</span></span>

- [<span data-ttu-id="b6421-158">Come toouse archiviazione di File di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="b6421-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="b6421-159">Come toouse archiviazione di File di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="b6421-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="b6421-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6421-160">Next steps</span></span>

<span data-ttu-id="b6421-161">Ora che si conoscono le opzioni di archiviazione di Azure hello, seguente hello utilizzare collegamenti toodiscover modalità di acquisizione di attività di analisi scientifica dei dati eseguita con il Server di R in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6421-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="b6421-162">Panoramica: R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="b6421-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="b6421-163">Articolo introduttivo relativo a Server R su Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b6421-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="b6421-164">Aggiungere RStudio Server tooHDInsight (se non è aggiunto durante la creazione del cluster)</span><span class="sxs-lookup"><span data-stu-id="b6421-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="b6421-165">Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="b6421-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

