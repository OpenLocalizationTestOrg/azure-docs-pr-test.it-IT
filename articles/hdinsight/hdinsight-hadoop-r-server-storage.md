---
title: Soluzioni di Archiviazione di Azure per R Server in HDInsight - Azure | Documentazione Microsoft
description: Informazioni sulle diverse opzioni di archiviazione disponibili per gli utenti con R Server in HDInsight
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="8fd2a-103">Soluzioni di Archiviazione di Azure per R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fd2a-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="8fd2a-104">Microsoft R Server in HDInsight offre un'ampia gamma di soluzioni di archiviazione per rendere persistenti i dati, i codici o gli oggetti che contengono risultati di analisi.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="8fd2a-105">Di seguito sono indicate alcune opzioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-105">These include the following options:</span></span>

- [<span data-ttu-id="8fd2a-106">BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8fd2a-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="8fd2a-107">Archiviazione di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8fd2a-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="8fd2a-108">Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="8fd2a-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="8fd2a-109">È possibile anche accedere a più account di archiviazione o contenitori di Azure con il cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="8fd2a-110">Archiviazione di File di Azure è un'opzione di archiviazione di dati ideale per l'uso nel nodo perimetrale che consente di montare ad esempio una condivisione di file di Archiviazione di Azure sul file system di Linux.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="8fd2a-111">Tuttavia, le condivisioni File di Azure possono essere montate e usate in qualsiasi sistema dotato di un sistema operativo supportato, ad esempio Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="8fd2a-112">Quando si crea un cluster Hadoop in HDInsight, si specifica un account di **Archiviazione di Azure** o un **archivio Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="8fd2a-113">Un contenitore di archiviazione specifico dell'account include il file system del cluster creato, ad esempio Hadoop Distributed File System.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="8fd2a-114">Per altre informazioni e istruzioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="8fd2a-115">Usare l'Archiviazione di Azure con HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fd2a-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="8fd2a-116">[Usare Data Lake Store con cluster Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="8fd2a-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="8fd2a-117">Per altre informazioni sulle soluzioni di Archiviazione di Azure, vedere [Introduzione ad Archiviazione di Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8fd2a-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="8fd2a-118">Per visualizzare del materiale sussidiario sulla selezione dell'opzione di archiviazione più appropriata per uno scenario specifico, vedere [Quando usare BLOB di Azure, File di Azure o Dischi dati di Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="8fd2a-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="8fd2a-119">Usare gli account di archiviazione BLOB di Azure con R Server</span><span class="sxs-lookup"><span data-stu-id="8fd2a-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="8fd2a-120">Se necessario, è possibile accedere a più account di archiviazione o contenitori di Azure con il cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="8fd2a-121">A tale scopo è necessario specificare gli account di archiviazione aggiuntivi nell'interfaccia utente al momento della creazione del cluster e quindi seguire questa procedura per usarli in R Server.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="8fd2a-122">Per motivi di prestazioni, il cluster HDInsight viene creato nello stesso data center dell'account di archiviazione primario specificato.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="8fd2a-123">L'uso di un account di archiviazione in una località diversa rispetto al cluster HDInsight non è supportato.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="8fd2a-124">Creare un cluster HDInsight con un nome di account di archiviazione **storage1** e un contenitore predefinito denominato **container1**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="8fd2a-125">Si specifica anche un account di archiviazione aggiuntivo denominato **storage2**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="8fd2a-126">Copiare il file mycsv.csv nella directory /share ed eseguire analisi su tale file.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="8fd2a-127">Nel codice R il nodo del nome è stato impostato su **default** e sono stati specificati la directory e il file da elaborare.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="8fd2a-128">Tutti i riferimenti a file e directory puntano all'account di archiviazione wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="8fd2a-129">Si tratta dell'**account di archiviazione predefinito** associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="8fd2a-130">Si supponga ora di voler elaborare un file denominato mySpecial.csv che si trova nella directory /private di **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="8fd2a-131">Nel codice R puntare il nome del riferimento al nodo sull'account di archiviazione **storage2** .</span><span class="sxs-lookup"><span data-stu-id="8fd2a-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="8fd2a-132">Tutti i riferimenti a file e directory ora puntano all'account di archiviazione wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="8fd2a-133">Questo è il **nodo del nome** specificato.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="8fd2a-134">È necessario configurare la directory /user/RevoShare/<SSH username> in **storage2** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="8fd2a-135">Usare un Archivio Azure Data Lake con R Server</span><span class="sxs-lookup"><span data-stu-id="8fd2a-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="8fd2a-136">Per usare archivi Data Lake con l'account HDInsight, è necessario concedere al cluster l'accesso a ogni Archivio Azure Data Lake che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="8fd2a-137">Per istruzioni su come usare il portale di Azure per creare un cluster HDInsight con Azure Data Lake Store come risorsa di archiviazione predefinita o archivio aggiuntivo, vedere [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="8fd2a-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="8fd2a-138">Usare quindi l'archivio nello script R come si usa un account di archiviazione Azure secondario, descritto nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="8fd2a-139">Aggiungere l'accesso del cluster agli archivi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8fd2a-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="8fd2a-140">Per accedere a un Archivio Azure Data Lake, usare un'entità servizio di Azure Active Directory (AAD) associata al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="8fd2a-141">Aggiungere un'entità servizio Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="8fd2a-142">Quando si crea il cluster HDInsight, selezionare **Identità AAD del cluster** nella scheda **Origine dati**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="8fd2a-143">Nella finestra di dialogo **Identità AAD del cluster** selezionare **Crea nuova** in **Selezionare l'entità servizio di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="8fd2a-144">Dopo aver assegnato un nome all'entità servizio, creare una password per tale entità e fare clic su **Gestisci l'accesso ad Archivio Azure Data Lake** per associare l'entità servizio agli archivi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="8fd2a-145">Dopo la creazione del cluster è anche possibile aggiungere l'accesso tramite cluster a uno o più archivi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="8fd2a-146">Aprire la voce portale di Azure per un archivio Data Lake e passare a **Esplora dati > Accesso > Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="8fd2a-147">Come accedere all'archivio Data Lake da R Server</span><span class="sxs-lookup"><span data-stu-id="8fd2a-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="8fd2a-148">Una volta che è stato concesso l'accesso a un Archivio Data Lake, è possibile usarlo in R Server in HDInsight come con un account di archiviazione di Azure secondario.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="8fd2a-149">L'unica differenza è che il prefisso **wasb://** cambia in **adl://** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="8fd2a-150">I comandi seguenti sono usati per configurare l'account di archiviazione di Data Lake con la directory RevoShare e aggiungere il file CSV di esempio dall'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="8fd2a-151">Usare Archiviazione file di Azure con R Server</span><span class="sxs-lookup"><span data-stu-id="8fd2a-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="8fd2a-152">È disponibile anche una pratica opzione di archiviazione dei dati da usare nel nodo perimetrale denominata [File di Azure]((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="8fd2a-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="8fd2a-153">Consente di montare una condivisione file di Archiviazione di Azure nel file system Linux.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="8fd2a-154">Questa opzione può essere utile per l'archiviazione di file di dati, script R e oggetti risultato che potrebbero essere necessari in seguito, soprattutto quando sarà opportuno usare il file system nativo nel nodo perimetrale invece di HDFS.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="8fd2a-155">Un vantaggio importante di File di Azure riguarda la possibilità di montare e usare le condivisioni file in qualsiasi sistema dotato di un sistema operativo supportato, ad esempio Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="8fd2a-156">Ad esempio, può essere usato da un altro cluster HDInsight disponibile all'utente o a un membro del team, da una macchina virtuale di Azure o anche da un sistema locale.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="8fd2a-157">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="8fd2a-157">For more information, see:</span></span>

- [<span data-ttu-id="8fd2a-158">Come usare Archiviazione file di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="8fd2a-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="8fd2a-159">Come usare Archiviazione file di Azure su Windows</span><span class="sxs-lookup"><span data-stu-id="8fd2a-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="8fd2a-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8fd2a-160">Next steps</span></span>

<span data-ttu-id="8fd2a-161">Ora che si conoscono le opzioni di archiviazione per Azure, usare i collegamenti seguenti per scoprire altre modalità di esecuzione delle attività di data science con R Server in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="8fd2a-162">Panoramica: R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="8fd2a-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="8fd2a-163">Articolo introduttivo relativo a Server R su Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8fd2a-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="8fd2a-164">Aggiungere RStudio Server a HDInsight (se non è stato aggiunto durante la creazione del cluster)</span><span class="sxs-lookup"><span data-stu-id="8fd2a-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="8fd2a-165">Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="8fd2a-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

