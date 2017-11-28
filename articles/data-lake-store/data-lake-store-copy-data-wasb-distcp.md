---
title: aaaCopy dati tooand da WASB in archivio Data Lake tramite Distcp | Documenti Microsoft
description: Utilizzare Distcp strumento toocopy dati tooand dall'archivio di Azure archiviazione BLOB tooData Lake
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
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="84d42-103">Utilizzare i dati di toocopy Distcp tra il BLOB di archiviazione di Azure e archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="84d42-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84d42-104">Con DistCp</span><span class="sxs-lookup"><span data-stu-id="84d42-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="84d42-105">Con AdlCopy</span><span class="sxs-lookup"><span data-stu-id="84d42-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="84d42-106">Dopo aver creato un cluster HDInsight che dispone di un account di accesso tooa archivio Data Lake, è possibile usare strumenti di ecosistema Hadoop come dati toocopy Distcp **tooand da** un'archiviazione del cluster HDInsight (WASB) in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="84d42-107">In questo articolo vengono fornite istruzioni su come tooachieve questo.</span><span class="sxs-lookup"><span data-stu-id="84d42-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84d42-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="84d42-108">Prerequisites</span></span>
<span data-ttu-id="84d42-109">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="84d42-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="84d42-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="84d42-110">**An Azure subscription**.</span></span> <span data-ttu-id="84d42-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84d42-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="84d42-112">**Un account Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="84d42-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="84d42-113">Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="84d42-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="84d42-114">**Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="84d42-115">Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84d42-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="84d42-116">Assicurarsi di abilitare Desktop remoto per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="84d42-117">Apprendimento rapido con i video</span><span class="sxs-lookup"><span data-stu-id="84d42-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="84d42-118">[Guardare questo video](https://mix.office.com/watch/1liuojvdx6sie) sulla toocopy dati tra il BLOB di archiviazione di Azure e archivio Data Lake tramite DistCp.</span><span class="sxs-lookup"><span data-stu-id="84d42-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="84d42-119">Usare Distcp da un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="84d42-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="84d42-120">Un cluster HDInsight viene fornito con l'utilità Distcp hello, che può essere utilizzato toocopy dati provenienti da origini diverse in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84d42-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="84d42-121">Se è stata configurata l'archivio Data Lake toouse cluster HDInsight hello come un'ulteriore spazio di archiviazione, hello Distcp utilità può essere utilizzato di casella toocopy tooand di dati da un account archivio Data Lake anche.</span><span class="sxs-lookup"><span data-stu-id="84d42-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="84d42-122">In questa sezione verranno esaminate come toouse hello Distcp utilità.</span><span class="sxs-lookup"><span data-stu-id="84d42-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="84d42-123">Dal desktop, usare SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="84d42-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="84d42-124">Vedere [cluster HDInsight basati su Linux di Connect tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="84d42-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="84d42-125">Eseguire i comandi di hello dal prompt dei comandi di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="84d42-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="84d42-126">Verificare se sia possibile accedere hello BLOB di archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="84d42-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="84d42-127">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="84d42-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="84d42-128">Ciò dovrebbe fornire un elenco del contenuto nel blob di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="84d42-129">Analogamente, verificare se è possibile accedere hello account archivio Data Lake dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="84d42-130">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="84d42-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="84d42-131">Ciò dovrebbe fornire un elenco di file e cartelle in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="84d42-132">Utilizzare dati toocopy Distcp WASB tooa account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="84d42-133">Verranno copiati contenuto hello di hello **esempio/data/gutenberg/** cartella WASB troppo**/myfolder** in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="84d42-134">Analogamente, utilizzare dati toocopy Distcp tooWASB account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="84d42-135">Verranno copiati contenuto hello di **/myfolder** in archivio Data Lake hello account troppo**esempio/data/gutenberg/** cartella WASB.</span><span class="sxs-lookup"><span data-stu-id="84d42-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="84d42-136">Considerazioni sulle prestazioni per l'uso di DistCp</span><span class="sxs-lookup"><span data-stu-id="84d42-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="84d42-137">Poiché DistCp's più basso granularità è un singolo file, impostazione hello massimo del numero di copie simultanee è hello più importante parametro toooptimize è in archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d42-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="84d42-138">Questa funzionalità è controllata impostando il numero di hello di BizTalk Mapper (sto ') del parametro nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="84d42-139">Questo parametro specifica numero massimo di hello di BizTalk Mapper che verrà utilizzato toocopy dati.</span><span class="sxs-lookup"><span data-stu-id="84d42-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="84d42-140">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="84d42-140">Default value is 20.</span></span>

<span data-ttu-id="84d42-141">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="84d42-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="84d42-142">Come è possibile determinare il numero di hello di BizTalk Mapper toouse?</span><span class="sxs-lookup"><span data-stu-id="84d42-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="84d42-143">Ecco alcune linee guida che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="84d42-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="84d42-144">**Passaggio 1: Determinare il totale memoria YARN** -hello primo passaggio consiste cluster disponibili toohello toodetermine hello YARN memoria in cui viene eseguito il processo di DistCp hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="84d42-145">Queste informazioni sono disponibili nel portale di Ambari hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="84d42-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="84d42-146">Passare tooYARN e visualizzare hello configurazioni scheda toosee hello YARN memoria.</span><span class="sxs-lookup"><span data-stu-id="84d42-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="84d42-147">tooget hello YARN memoria totale, moltiplicare hello memoria YARN per ogni nodo con il numero di hello di nodi nel cluster di cui si dispone.</span><span class="sxs-lookup"><span data-stu-id="84d42-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="84d42-148">**Passaggio 2: Calcolare il numero di hello di BizTalk Mapper** -hello valore **m** è il quoziente toohello uguale totale di memoria YARN diviso hello dimensione del contenitore YARN.</span><span class="sxs-lookup"><span data-stu-id="84d42-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="84d42-149">informazioni sulle dimensioni YARN contenitore Hello è disponibile nel portale nonché di hello Ambari.</span><span class="sxs-lookup"><span data-stu-id="84d42-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="84d42-150">Passare tooYARN e hello di scheda configurazioni di visualizzazione hello dimensione del contenitore YARN viene visualizzato in questa finestra.</span><span class="sxs-lookup"><span data-stu-id="84d42-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="84d42-151">Hello tooarrive equazione numero hello di BizTalk Mapper (**m**) è</span><span class="sxs-lookup"><span data-stu-id="84d42-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="84d42-152">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="84d42-152">**Example**</span></span>

<span data-ttu-id="84d42-153">Si supponga di avere un 4 nodi D14v2s cluster hello e che si sta tentando di tootransfer 10TB di dati da 10 cartelle diverse.</span><span class="sxs-lookup"><span data-stu-id="84d42-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="84d42-154">Ciascuna delle cartelle hello contenere quantità variabili di dati e delle dimensioni del file hello all'interno di ogni cartella sono diverse.</span><span class="sxs-lookup"><span data-stu-id="84d42-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="84d42-155">Memoria totale di YARN - dal portale Ambari si determina che la memoria YARN hello hello è 96GB per un nodo D14.</span><span class="sxs-lookup"><span data-stu-id="84d42-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="84d42-156">Pertanto, la memoria totale di YARN per un cluster a 4 nodi è:</span><span class="sxs-lookup"><span data-stu-id="84d42-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="84d42-157">Numero di BizTalk Mapper - dal portale Ambari è determinare la dimensione del contenitore YARN hello 3072 per un nodo del cluster D14 hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="84d42-158">Il numero di mapper è quindi:</span><span class="sxs-lookup"><span data-stu-id="84d42-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="84d42-159">Se altre applicazioni utilizzano memoria, quindi è possibile utilizzare tooonly una parte della memoria YARN del cluster per DistCp.</span><span class="sxs-lookup"><span data-stu-id="84d42-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="84d42-160">Copia di set di dati di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="84d42-160">Copying large datasets</span></span>

<span data-ttu-id="84d42-161">Le dimensioni hello di hello dataset toobe spostate è molto grande (ad esempio > 1TB) o se si dispone di molte cartelle diverse, è consigliabile utilizzare più processi DistCp.</span><span class="sxs-lookup"><span data-stu-id="84d42-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="84d42-162">Non è probabile alcun miglioramento delle prestazioni, ma verrà distribuito processi hello in modo che se un processo non riesce, sarà sufficiente toorestart tale processo specifico anziché l'intero processo di hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="84d42-163">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="84d42-163">Limitations</span></span>

* <span data-ttu-id="84d42-164">DistCp tenta toocreate Mapper delle prestazioni toooptimize dimensioni simili.</span><span class="sxs-lookup"><span data-stu-id="84d42-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="84d42-165">Aumentare il numero di hello BizTalk Mapper non può sempre aumentare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="84d42-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="84d42-166">DistCp è limitato tooonly uno mapper per ogni file.</span><span class="sxs-lookup"><span data-stu-id="84d42-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="84d42-167">quindi non è possibile avere più mapper che file.</span><span class="sxs-lookup"><span data-stu-id="84d42-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="84d42-168">Poiché DistCp possibile assegnare solo un mapping tooa file, ciò limita quantità hello di concorrenza che può essere utilizzati toocopy file di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="84d42-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="84d42-169">Se si dispone di un numero ridotto di file di grandi dimensioni, quindi è consigliabile dividerli in toogive blocchi di file da 256MB è maggiore concorrenza potenziale.</span><span class="sxs-lookup"><span data-stu-id="84d42-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="84d42-170">Se si copia da un account di archiviazione Blob di Azure, il processo di copia può essere limitato sul lato di archiviazione blob di hello.</span><span class="sxs-lookup"><span data-stu-id="84d42-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="84d42-171">Si riducono le prestazioni di hello del processo di copia.</span><span class="sxs-lookup"><span data-stu-id="84d42-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="84d42-172">toolearn ulteriori informazioni sui limiti di hello dell'archiviazione Blob di Azure, vedere i limiti di archiviazione di Azure in [sottoscrizione di Azure e limiti dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="84d42-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="84d42-173">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="84d42-173">See also</span></span>
* [<span data-ttu-id="84d42-174">Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake</span><span class="sxs-lookup"><span data-stu-id="84d42-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="84d42-175">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84d42-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="84d42-176">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84d42-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="84d42-177">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84d42-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
