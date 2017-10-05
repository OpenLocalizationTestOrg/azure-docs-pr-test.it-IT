---
title: Copiare dati in e da WASB in Data Lake Store con Distcp| Microsoft Azure
description: Usare lo strumento Distcp per copiare i dati da e nel BLOB di Archiviazione di Azure ad Archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="d4a85-103">Usare Distcp per copiare dati tra i BLOB di archiviazione di Azure e Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4a85-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4a85-104">Con DistCp</span><span class="sxs-lookup"><span data-stu-id="d4a85-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="d4a85-105">Con AdlCopy</span><span class="sxs-lookup"><span data-stu-id="d4a85-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="d4a85-106">Dopo avere creato un cluster HDInsight con accesso a un account Data Lake Store, è possibile usare gli strumenti dell'ecosistema Hadoop, ad esempio Distcp, per copiare i dati **da e in** una risorsa di archiviazione del cluster HDInsight in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d4a85-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="d4a85-107">Questo articolo include istruzioni per eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="d4a85-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4a85-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4a85-108">Prerequisites</span></span>
<span data-ttu-id="d4a85-109">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="d4a85-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="d4a85-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4a85-110">**An Azure subscription**.</span></span> <span data-ttu-id="d4a85-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4a85-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d4a85-112">**Un account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4a85-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="d4a85-113">Per istruzioni su come crearne uno, vedere [Introduzione ad Archivio Data Lake di Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d4a85-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="d4a85-114">**Cluster Azure HDInsight** con accesso a un account di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4a85-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="d4a85-115">Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4a85-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="d4a85-116">Assicurarsi di abilitare il Desktop remoto per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d4a85-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="d4a85-117">Apprendimento rapido con i video</span><span class="sxs-lookup"><span data-stu-id="d4a85-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="d4a85-118">[Guardare questo video](https://mix.office.com/watch/1liuojvdx6sie) su come copiare dati tra i BLOB di archiviazione di Azure e Archivio Data Lake con DistCp.</span><span class="sxs-lookup"><span data-stu-id="d4a85-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="d4a85-119">Usare Distcp da un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="d4a85-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="d4a85-120">Un cluster HDInsight include l'utilità Distcp, che può essere usata per copiare i dati da diverse origini in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4a85-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="d4a85-121">Se il cluster HDInsight è stato configurato per l'uso di Archivio Data Lake come risorsa di archiviazione aggiuntiva, l'utilità Distcp può essere usata senza modifiche anche per copiare dati in e da un account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4a85-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="d4a85-122">Questa sezione illustra come usare l'utilità Distcp.</span><span class="sxs-lookup"><span data-stu-id="d4a85-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="d4a85-123">Dal desktop usare SSH per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="d4a85-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="d4a85-124">Vedere [Connettersi a un cluster HDInsight basato su Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d4a85-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="d4a85-125">Eseguire i comandi dal prompt SSH.</span><span class="sxs-lookup"><span data-stu-id="d4a85-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="d4a85-126">Verificare se è possibile accedere ai BLOB di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a85-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="d4a85-127">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d4a85-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="d4a85-128">Dovrebbe essere visualizzato un elenco di contenuti del BLOB di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d4a85-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="d4a85-129">Analogamente, verificare se è possibile accedere all'account Archivio Data Lake dal cluster.</span><span class="sxs-lookup"><span data-stu-id="d4a85-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="d4a85-130">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d4a85-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="d4a85-131">Dovrebbe essere visualizzato un elenco di file/cartelle nell'account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4a85-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="d4a85-132">Usare Distcp per copiare i dati dal BLOB di archiviazione di Azure all'account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4a85-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="d4a85-133">I contenuti della cartella **/example/data/gutenberg/** in WASB verranno copiati in **/myfolder** nell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d4a85-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="d4a85-134">Analogamente, usare Distcp per copiare dati dall'account Archivio Data Lake al BLOB di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a85-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="d4a85-135">I contenuti di **/myfolder** nell'account Data Lake Store verranno copiati nella cartella **/example/data/gutenberg/** in WASB.</span><span class="sxs-lookup"><span data-stu-id="d4a85-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="d4a85-136">Considerazioni sulle prestazioni per l'uso di DistCp</span><span class="sxs-lookup"><span data-stu-id="d4a85-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="d4a85-137">Dato che il livello di granularità minimo per DistCp corrisponde a un singolo file, l'impostazione del numero massimo di copie simultanee è il parametro più importante per l'ottimizzazione per Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d4a85-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="d4a85-138">A tale scopo è possibile impostare il parametro del numero di mapper ('m') nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d4a85-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="d4a85-139">Questo parametro specifica il numero massimo di mapper che verranno usati per la copia dei dati.</span><span class="sxs-lookup"><span data-stu-id="d4a85-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="d4a85-140">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="d4a85-140">Default value is 20.</span></span>

<span data-ttu-id="d4a85-141">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="d4a85-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="d4a85-142">Come determinare il numero di mapper da usare</span><span class="sxs-lookup"><span data-stu-id="d4a85-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="d4a85-143">Ecco alcune linee guida che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="d4a85-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="d4a85-144">**Passaggio 1: determinare la memoria totale di YARN** - il primo passaggio consiste nel determinare la memoria di YARN disponibile per il cluster in cui viene eseguito il processo DistCp.</span><span class="sxs-lookup"><span data-stu-id="d4a85-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="d4a85-145">Queste informazioni sono disponibili nel portale di Ambari associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="d4a85-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="d4a85-146">Passare a YARN e visualizzare la scheda Configs (Configurazioni) per visualizzare la memoria di YARN.</span><span class="sxs-lookup"><span data-stu-id="d4a85-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="d4a85-147">Per ottenere la memoria totale di YARN, moltiplicare la memoria di YARN per ogni nodo per il numero di nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="d4a85-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="d4a85-148">**Passaggio 2: calcolare il numero di mapper** - il valore di **m** è uguale al quoziente della memoria totale di YARN divisa per le dimensioni del contenitore YARN.</span><span class="sxs-lookup"><span data-stu-id="d4a85-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="d4a85-149">Anche queste informazioni sono disponibili nel portale di Ambari.</span><span class="sxs-lookup"><span data-stu-id="d4a85-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="d4a85-150">Passare a YARN e visualizzare la scheda Configs (Configurazioni).</span><span class="sxs-lookup"><span data-stu-id="d4a85-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="d4a85-151">Le dimensioni del contenitore YARN sono visualizzate in questa finestra.</span><span class="sxs-lookup"><span data-stu-id="d4a85-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="d4a85-152">L'equazione per ottenere il numero di mapper (**m**) è</span><span class="sxs-lookup"><span data-stu-id="d4a85-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="d4a85-153">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="d4a85-153">**Example**</span></span>

<span data-ttu-id="d4a85-154">Si supponga di avere 4 nodi D14v2s nel cluster e di voler tentare il trasferimento di 10 TB di dati da 10 cartelle diverse.</span><span class="sxs-lookup"><span data-stu-id="d4a85-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="d4a85-155">Ogni cartella contiene quantità variabili di dati e le dimensioni dei file all'interno di ogni cartella sono diverse.</span><span class="sxs-lookup"><span data-stu-id="d4a85-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="d4a85-156">Memoria di YARN totale - Dal portale di Ambari si stabilisce che la memoria di YARN è pari a 96 GB per un nodo D14.</span><span class="sxs-lookup"><span data-stu-id="d4a85-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="d4a85-157">Pertanto, la memoria totale di YARN per un cluster a 4 nodi è:</span><span class="sxs-lookup"><span data-stu-id="d4a85-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="d4a85-158">Numero di mapper - Dal portale di Ambari si stabilisce che le dimensioni del contenitore YARN sono 3072 per un nodo del cluster D14.</span><span class="sxs-lookup"><span data-stu-id="d4a85-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="d4a85-159">Il numero di mapper è quindi:</span><span class="sxs-lookup"><span data-stu-id="d4a85-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="d4a85-160">Se altre applicazioni usano la memoria, è possibile scegliere di usare solo una parte della memoria di YARN del cluster per DistCp.</span><span class="sxs-lookup"><span data-stu-id="d4a85-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="d4a85-161">Copia di set di dati di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="d4a85-161">Copying large datasets</span></span>

<span data-ttu-id="d4a85-162">Quando le dimensioni del set di dati da spostare sono molto grandi (ad esempio, maggiori di 1 TB) o se esistono molte cartelle diverse, è consigliabile usare più processi DistCp.</span><span class="sxs-lookup"><span data-stu-id="d4a85-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="d4a85-163">Non si noterà probabilmente alcun miglioramento delle prestazioni, ma in questo modo è possibile distribuire i processi in modo che, se un processo non riesce, sia sufficiente riavviare tale processo specifico invece dell'intero processo.</span><span class="sxs-lookup"><span data-stu-id="d4a85-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="d4a85-164">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="d4a85-164">Limitations</span></span>

* <span data-ttu-id="d4a85-165">DistCp tenta di creare mapper con dimensioni simili per ottimizzare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d4a85-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="d4a85-166">Un aumento del numero di mapper non sempre corrisponde a un miglioramento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d4a85-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="d4a85-167">DistCp è limitato a un solo mapper per file,</span><span class="sxs-lookup"><span data-stu-id="d4a85-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="d4a85-168">quindi non è possibile avere più mapper che file.</span><span class="sxs-lookup"><span data-stu-id="d4a85-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="d4a85-169">Dato che DistCp può assegnare un solo mapper a un file, ciò comporta una limitazione alla concorrenza utilizzabile per la copia di file di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="d4a85-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="d4a85-170">In presenza di un numero ridotto di file di grandi dimensioni, è consigliabile dividerli in blocchi di file da 256 MB per ottenere una maggiore concorrenza potenziale.</span><span class="sxs-lookup"><span data-stu-id="d4a85-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="d4a85-171">Se si esegue la copia da un account di Archiviazione BLOB di Azure, il processo di copia potrebbe essere limitato nell'ambito dell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="d4a85-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="d4a85-172">In questo modo le prestazioni del processo di copia diminuiranno.</span><span class="sxs-lookup"><span data-stu-id="d4a85-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="d4a85-173">Per altre informazioni sui limiti di Archiviazione BLOB di Azure, vedere i limiti di Archiviazione di Azure in [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d4a85-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d4a85-174">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d4a85-174">See also</span></span>
* [<span data-ttu-id="d4a85-175">Copiare i dati da BLOB di archiviazione di Azure ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4a85-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="d4a85-176">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d4a85-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d4a85-177">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d4a85-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d4a85-178">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d4a85-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
